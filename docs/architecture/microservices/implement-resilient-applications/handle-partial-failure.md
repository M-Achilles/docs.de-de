---
title: Behandeln von Teilfehlern
description: Erfahren Sie, wie Teilfehler ordnungsgemäß behandelt werden. Ein Microservice ist möglicherweise nicht voll funktionsfähig, kann aber möglicherweise noch weitere nützliche Aufgaben ausführen.
ms.date: 10/16/2018
ms.openlocfilehash: a667ad2e1456db7b5846023de27d3797dad58731
ms.sourcegitcommit: f20dd18dbcf2275513281f5d9ad7ece6a62644b4
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 07/30/2019
ms.locfileid: "68674697"
---
# <a name="handle-partial-failure"></a>Behandeln von Teilfehlern

In verteilten Systemen wie Anwendungen, die auf Microservices basieren, gibt es ein allgegenwärtiges Risiko für Teilfehler. Zum Beispiel kann ein einzelner Microservice oder Container fehlschlagen oder für eine kurze Zeit nicht verfügbar sein, oder eine einzelne VM oder ein Server kann abstürzen. Da Clients und Dienste separate Vorgänge sind, kann ein Dienst möglicherweise nicht schnell genug auf die Anforderung eines Clients reagieren. Der Dienst ist möglicherweise überlastet und antwortet sehr langsam auf Anforderungen, oder er ist aufgrund von Netzwerkproblemen vorübergehend nicht verfügbar.

Nehmen Sie sich ein Beispiel an der Seite „Auftragsdetails“ der Beispielanwendung „eShopOnContainers“. Wenn der Microservice für Bestellungen nicht mehr reagiert, wenn der Benutzer versucht, einen Auftrag zu übermitteln, würde eine schlechte Implementierung des Clientprozesses (die MVC-Webanwendung) Threads auf unbestimmte Zeit blockieren, da er auf eine Antwort wartet, z.B. wenn der Clientcode synchrone RPCs ohne Timeout verwendet. Dies reduziert nicht nur die Benutzerfreundlichkeit, denn zusätzlich verbraucht oder blockiert jeder Wartevorgang ohne Reaktion einen Thread. Threads sind in hochgradig skalierbaren Anwendungen jedoch sehr wertvoll. Wenn viele Threads blockiert werden, sind für die Laufzeit der Anwendung irgendwann keine Threads mehr verfügbar. In diesem Fall kann es dazu kommen, dass die Anwendung wie in Abbildung 8-1 dargestellt global statt nur teilweise nicht mehr reagiert.

![Diagramm zum vorherigen Abschnitt](./media/image1.png)

**Abbildung 8-1**. Teilfehler treten wegen Abhängigkeiten auf, die die Verfügbarkeit von Dienstthreads beeinflussen

In einer großen, auf Microservices basierten Anwendung können Teilfehler vor allem verstärkt werden, wenn der Großteil der internen Interaktionen von Microservices auf synchronen HTTP-Aufrufen basiert (dies gilt als Antimuster). Stellen Sie sich ein System vor, das täglich Millionen von eingehenden Aufrufen empfängt. Wenn Ihr System schlecht entworfen ist und auf langen Ketten von synchronen HTTP-Aufrufen basiert, können diese eingehenden Aufrufe in vielen weiteren Millionen von ausgehenden Aufrufen (z.B. ein Verhältnis von 1:4) an dutzende interne Microservices als synchrone Abhängigkeiten resultieren. Diese Situation wird in Abbildung 8-2 veranschaulicht, insbesondere in Abhängigkeit \#3.

![Ein falscher Entwurf für den Web-App-Microservice, der von einer Kette von Abhängigkeiten von anderen Microservices abhängig ist](./media/image2.png)

**Abbildung 8-2**. Die Auswirkungen eines falschen Entwurfs mit langen Ketten von HTTP-Anforderungen

Zeitweilige Fehler sind in einem verteilten und cloudbasierten System garantiert, auch wenn jede Abhängigkeit eine hervorragende Verfügbarkeit aufweist. Diese Tatsache müssen Sie berücksichtigen.

Wenn Sie keine Techniken für die Fehlertoleranz entwerfen oder implementieren, können selbst kleine Ausfälle verstärkt werden. Wegen dieser ausbreitenden Wirkung würden zum Beispiel 50 Abhängigkeiten mit einer Verfügbarkeit von 99,99% für mehrere Stunden im Monat ausfallen. Wenn eine Microserviceabhängigkeit beim Behandeln einer großen Anzahl von Anforderungen fehlschlägt, kann dieser Fehler schnell alle verfügbaren Anforderungsthreads in jedem Dienst beanspruchen und die gesamte Anwendung zum Abstürzen bringen.

![Teilfehler können durch verkettete Abhängigkeiten deutlich verstärkt werden](./media/image3.png)

**Abbildung 8-3**. Teilfehler, der durch Microservices mit langen Ketten von synchronen HTTP-Aufrufen verstärkt wurde

Zur Minimierung dieses Problems wird im Abschnitt [Asynchrone Integration von Microservices erzwingt die Autonomie eines Microservice](../architect-microservice-container-applications/communication-in-microservice-architecture.md#asynchronous-microservice-integration-enforces-microservices-autonomy) dieses Handbuchs empfohlen, die asynchrone Kommunikation in allen internen Microservices zu verwenden.

Darüber hinaus ist es wichtig, dass Sie Ihre Microservices und Clientanwendungen dafür entwerfen, Teilfehler zu behandeln – d.h. robuste Microservices und Clientanwendungen zu erstellen.

>[!div class="step-by-step"]
>[Zurück](index.md)
>[Weiter](partial-failure-strategies.md)
