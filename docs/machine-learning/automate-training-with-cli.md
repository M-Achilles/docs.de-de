---
title: Automatisieren des Modelltrainings mit der ML.NET-CLI
description: Erfahren Sie, wie Sie mit dem ML.NET-CLI-Tool automatisch das beste Modell über die Befehlszeile trainieren können.
author: CESARDELATORRE
ms.date: 04/17/2019
ms.custom: how-to
ms.openlocfilehash: e5f75dc70ea5a76951d8698ea9c0d07cb2d4ddec
ms.sourcegitcommit: d6e27023aeaffc4b5a3cb4b88685018d6284ada4
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 07/09/2019
ms.locfileid: "67663926"
---
# <a name="automate-model-training-with-the-mlnet-cli"></a>Automatisieren des Modelltrainings mit der ML.NET-CLI

Die ML.NET-CLI „demokratisiert“ ML.NET für .NET-Entwickler beim Erlernen von ML.NET.

Um die ML.NET-API selbst zu verwenden (ohne ML.NET AutoML-CLI), müssen Sie einen Trainer (Implementierung eines Machine Learning-Algorithmus für eine bestimmte Aufgabe) und den Satz von Datentransformationen (Featureentwicklung) auswählen, die auf Ihre Daten angewendet werden. Die optimale Pipeline variiert für jedes Dataset, und die Auswahl des optimalen Algorithmus aus allen Optionen erhöht die Komplexität. Darüber hinaus muss für jeden Algorithmus ein Satz an Hyperparametern optimiert werden. Daher kann es manchmal Wochen oder Monate dauern, ein Machine Learning-Modell zu optimieren, um die beste Kombination aus Featureentwicklung, Lernalgorithmen und Hyperparametern zu finden.

Dieser Prozess kann mit der ML.NET CLI automatisiert werden, die die intelligente ML.NET AutoML-Engine implementiert.

> [!NOTE]
> Dieses Thema bezieht sich auf die ML.NET-**CLI** und ML.NET **AutoML**, die derzeit als Vorschau verfügbar sind, und das Material kann jederzeit geändert werden.

## <a name="what-is-the-mlnet-command-line-interface-cli"></a>Was ist die ML.NET-Befehlszeilenschnittstelle (CLI)?

Sie können die ML.NET-CLI über jede Eingabeaufforderung (Windows, Mac oder Linux) ausführen, um qualitativ hochwertige ML.NET-Modelle und Quellcode basierend auf Ihren Trainingsdatasets zu generieren.

Wie in der folgenden Abbildung dargestellt, ist es einfach, ein qualitativ hochwertiges ML.NET-Modell (serialisierte ZIP-Datei des Modells) plus den Beispiel-C#-Code zu generieren, um dieses Modell auszuführen/zu bewerten. Darüber hinaus wird der C#-Code zum Erstellen/Trainieren dieses Modells generiert, sodass Sie suchen und iterieren können, welcher Algorithmus und welche Einstellungen für dieses generierte „beste Modell“ verwendet wurden.

![Bild](media/automate-training-with-cli/cli-high-level-process.png "AutoML-Engine, die in der ML.NET-CLI arbeitet")

Sie können diese Objekte aus Ihren eigenen Datasets generieren, ohne selbst zu codieren. Damit steigern Sie also auch Ihre Produktivität, selbst wenn Sie ML.NET bereits kennen.

Derzeit unterstützt die ML.NET-CLI folgende Aufgaben:

- `binary-classification`
- `multiclass-classification`
- `regression`
- Zukünftig: weitere Machine Learning-Aufgaben wie `recommendation`, `ranking`, `anomaly-detection`, `clustering`

Beispiel für die Verwendung:

```console
> mlnet auto-train --task binary-classification --dataset "customer-feedback.tsv" --label-column-name Sentiment
```

![Bild](media/automate-training-with-cli/cli-model-generation.gif)

Sie können sie auf die gleiche Weise auf *Windows PowerShell*, *macOS-/Linux-Bash oder *Windows CMD* ausführen. Die tabellarische automatische Vervollständigung (Parametervorschläge) funktioniert jedoch nicht unter *Windows-CMD*.

## <a name="output-assets-generated"></a>Generierte Ausgabeobjekte

Der CLI-Befehl `auto-train` generiert die folgenden Objekte im Ausgabeordner:

- Eine serialisierte ZIP-Datei des Modells („bestes Modell“), die sofort für die Ausführung von Vorhersagen verwendet werden kann.
- C#-Lösung mit:
  - C#-Code, um das generierte Modell auszuführen/zu bewerten (um mit diesem Modell Vorhersagen in Ihren Endbenutzer-Apps zu treffen).
  - C#-Code mit dem Trainingscode, der zur Erstellung dieses Modells verwendet wird (zu Lernzwecken oder zum erneuten Trainieren des Modells).
- Protokolldatei mit Informationen über alle Iterationen/Sweep-Vorgänge über die verschiedenen ausgewerteten Algorithmen, einschließlich ihrer detaillierten Konfiguration/Pipeline.

Die ersten beiden Objekte können direkt in Ihren Endbenutzer-App (ASP.NET Core-Web-App, Dienste, Desktop-App usw.) verwendet werden, um mit dem generierten ML-Modell Vorhersagen zu treffen.

Das dritte Objekt, der Trainingscode, zeigt Ihnen, welchen ML.NET-API-Code die CLI zum Trainieren des generierten Modells verwendet hat, sodass Sie Ihr Modell erneut trainieren und untersuchen und iterieren können, welchen spezifischen Trainer/Algorithmus und Hyperparameter die CLI und AutoML im Hintergrund ausgewählt haben.

## <a name="understanding-the-quality-of-the-model"></a>Verstehen der Qualität des Modells

Wenn Sie mit dem CLI-Tool ein "bestes Modell" erstellen, werden Qualitätsmetriken angezeigt (wie Genauigkeit und Bestimmtheitsmaß), die für die von Ihnen angestrebte ML-Aufgabe geeignet sind.

Hier fassen wir diese Metriken zusammen, die nach ML-Aufgaben gruppiert sind, damit Sie die Qualität Ihres automatisch generierten „besten Modells“ verstehen können.

### <a name="metrics-for-binary-classification-models"></a>Metriken für binäre Klassifizierungsmodelle

Im Folgenden wird die Metrikliste der binären ML-Klassifizierungsaufgaben für die fünf besten, von der CLI gefundenen Modelle angezeigt:

![Bild](media/automate-training-with-cli/cli-binary-classification-metrics.png)

Die Genauigkeit ist eine beliebte Metrik für Klassifizierungsprobleme. Allerdings ist die Genauigkeit nicht immer die beste Metrik, um das beste Modell auszuwählen, wie in den folgenden Referenzen erläutert. Es gibt Fälle, in denen Sie die Qualität Ihres Modells mit zusätzlichen Metriken bewerten müssen.

Um die Metriken zu untersuchen und zu verstehen, die von der CLI ausgegeben werden, lesen Sie [Metriken für die binäre Klassifizierung](resources/metrics.md#metrics-for-binary-classification).

### <a name="metrics-for-multi-class-classification-models"></a>Metriken für Multiklassen-Klassifizierungsmodelle

Im Folgenden wird die Metrikliste der ML-Aufgabe für die Multiklassenklassifizierung für die fünf besten Modelle angezeigt, die von der CLI ermittelt wurden:

![Bild](media/automate-training-with-cli/cli-multiclass-classification-metrics.png)

Um die Metriken zu untersuchen und zu verstehen, die von der CLI ausgegeben werden, lesen Sie [Metriken für die Multiklassenklassifizierung](resources/metrics.md#metrics-for-multi-class-classification).

### <a name="metrics-for-regression-models"></a>Metriken für Regressionsmodelle

Ein Regressionsmodell eignet sich gut für die Daten, wenn die Unterschiede zwischen den beobachteten Werten und den vorhergesagten Werten des Modells klein und zufällig sind. Die Regression kann mit bestimmten Metriken ausgewertet werden.

Es wird eine ähnliche Metrikliste für die fünf besten, von der CLI gefundenen Modelle angezeigt. In diesem speziellen Fall bezogen auf eine ML-Regressionsaufgabe:

![Bild](media/automate-training-with-cli/cli-regression-metrics.png)

Um die Metriken zu untersuchen und zu verstehen, die von der CLI ausgegeben werden, lesen Sie [Metriken für die Regression](resources/metrics.md#metrics-for-regression).

## <a name="see-also"></a>Siehe auch

- [Vorgehensweise: Installieren des ML.NET-CLI-Tools](how-to-guides/install-ml-net-cli.md)
- [Tutorial: Automatisches Generieren eines binären Klassifizierers mit der ML.NET-CLI](tutorials/mlnet-cli.md)
- [Befehlsreferenz für die ML.NET-CLI](reference/ml-net-cli-reference.md)
- [Telemetrie in der ML.NET-CLI](resources/ml-net-cli-telemetry.md)
