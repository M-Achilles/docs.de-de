---
title: Kryptografische Dienste
ms.date: 03/30/2017
ms.technology: dotnet-standard
helpviewer_keywords:
- cryptography [.NET Framework]
- pattern of derived class inheritance
- digital signatures
- asymmetric cryptographic algorithms
- digital signatures, public-key systems
- public keys
- decryption [.NET Framework]
- private keys
- MAC algorithms
- cryptographic algorithms
- private keys, overview
- encryption [.NET Framework]
- security [.NET Framework], encryption
- cryptographic services
- symmetric cryptographic algorithms
- hash
- message authentication codes
- derived class inheritance
- cryptography [.NET Framework], about
- random number generation
ms.assetid: f96284bc-7b73-44b5-ac59-fac613ad09f8
author: mairaw
ms.author: mairaw
ms.openlocfilehash: c026174e881768af245860d1b719184dc47f1798
ms.sourcegitcommit: d6e27023aeaffc4b5a3cb4b88685018d6284ada4
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 07/09/2019
ms.locfileid: "67663990"
---
# <a name="cryptographic-services"></a>Kryptografische Dienste

<a name="top"></a> Öffentliche Netzwerke wie das Internet bieten keine sichere Kommunikation zwischen Entitäten. Bei einer Kommunikation über derartige Netzwerke besteht die Gefahr, dass Unbefugte Inhalte lesen oder sogar Änderungen daran vornehmen. Die Kryptografie schützt Daten vor der Anzeige, stellt Möglichkeiten bereit, mit denen erkannt werden kann, ob Daten geändert wurden, und bietet sichere Kommunikation über ansonsten unsichere Kanäle. So können Daten beispielsweise mithilfe eines kryptografischen Algorithmus verschlüsselt, im verschlüsselten Zustand übertragen und später beim vorgesehenen Empfänger wieder entschlüsselt werden. Wenn ein Dritter die verschlüsselten Daten abfängt, sind diese schwer zu entziffern.

In .NET Framework werden viele Aspekte der Kryptografie von den Klassen im <xref:System.Security.Cryptography?displayProperty=nameWithType> -Namespace verwaltet. Einige davon sind Wrapper für die nicht verwaltete Microsoft Cryptography API (CryptoAPI), bei anderen handelt es sich um rein verwaltete Implementierungen. Sie müssen kein Experte in Sachen Kryptografie sein, um diese Klassen verwenden zu können. Wenn Sie eine neue Instanz einer Verschlüsselungsalgorithmusklasse erstellen, werden der Einfachheit halber automatisch Schlüssel erzeugt. Die Standardeigenschaften sind dabei auf möglichst hohe Sicherheit und hohen Schutz ausgelegt.

Diese Übersicht bietet eine Zusammenfassung der Verschlüsselungsmethoden und Methoden, die von .NET Framework, einschließlich der ClickOnce-Manifeste, Suite B und Cryptography Next Generation (CNG) unterstützt, die seit .NET Framework 3.5 unterstützt.

Diese Übersicht enthält folgende Abschnitte:

- [Kryptografische Grundelemente](#primitives)

- [Verschlüsselung mit geheimem Schlüssel](#secret_key)

- [Verschlüsselung mit öffentlichem Schlüssel](#public_key)

- [Digital Signatures](#digital_signatures)

- [Hashwerte](#hash_values)

- [Random Number Generation](#random_numbers)

- [ClickOnce-Manifeste](#clickonce)

- [Suite B-Unterstützung](#suite_b)

- [Verwandte Themen](#related_topics)

Weitere Informationen zur Kryptografie sowie zu Microsoft-Diensten, -Komponenten und -Tools, mit deren Hilfe Sie Ihre Anwendungen mit kryptografischer Sicherheit versehen können, finden Sie in dieser Dokumentation im Abschnitt Sicherheit unter Win32- und COM-Entwicklung.

<a name="primitives"></a>

## <a name="cryptographic-primitives"></a>Kryptografische Grundelemente

Eine typische Situation für den Einsatz von Kryptografie ist die Kommunikation zwischen zwei Teilnehmern (Alice und Bob) über einen unsicheren Kanal. Alice und Bob möchten sicherstellen, dass ihre Kommunikation bei eventuellen Abhörversuchen unverständlich bleibt. Da sich Alice und Bob an Remotestellen befinden, muss außerdem gewährleistet sein, dass die Informationen, die Alice von Bob empfängt, während der Übertragung nicht geändert wurden. Alice muss außerdem sicher sein, dass die Informationen tatsächlich von Bob stammen und nicht von jemandem, der Bobs Identität angenommen hat.

Die Kryptografie wird für folgende Zielsetzungen verwendet:

- Vertraulichkeit: Um die Identität oder Daten eines Benutzers zu schützen, gelesen werden.

- Datenintegrität: Zum Schutz der Daten nicht geändert werden.

- Authentifizierung: Um sicherzustellen, dass Daten von einem bestimmten Teilnehmer stammen.

- Non-repudiation: Um zu verhindern, dass eine bestimmte Partei leugnen, dass sie eine Nachricht gesendet.

Um diese Ziele zu erreichen, können Sie aus einer Kombination von Algorithmen und Vorgehensweisen, die als kryptografische Grundelemente bezeichnet werden, ein kryptografisches Schema erstellen. In der nachstehenden Tabelle sind die kryptografischen Grundelemente und deren Verwendungszweck aufgeführt.

|Kryptografisches Grundelement|Mit|
|-----------------------------|---------|
|Verschlüsselung mit geheimem Schlüssel (symmetrische Kryptografie)|Transformiert die Daten und verhindert, dass sie von Dritten gelesen werden. Bei diesem Verschlüsselungstyp werden die Daten mit einem einzigen, gemeinsam genutzten, geheimen Schlüssel ver- und entschlüsselt.|
|Verschlüsselung mit öffentlichem Schlüssel (asymmetrische Kryptografie)|Transformiert die Daten und verhindert, dass sie von Dritten gelesen werden. Bei diesem Verschlüsselungstyp werden die Daten mit einem Paar aus öffentlichem und privatem Schlüssel ver- und entschlüsselt.|
|Kryptografische Signatur|Stellt sicher, dass die Daten von einem bestimmten Teilnehmer stammen. Dazu wird eine digitale Signatur erstellt, die diesen Teilnehmer eindeutig bezeichnet. Bei diesem Prozess werden auch Hashfunktionen verwendet.|
|Kryptografische Hashs|Ordnet Daten beliebiger Länge einer Bytefolge fester Länge zu. Hashs sind statistisch eindeutig; eine unterschiedliche 2-Byte-Sequenz erzielt nicht denselben Hashwert.|

[Zurück nach oben](#top)

<a name="secret_key"></a>

## <a name="secret-key-encryption"></a>Verschlüsselung mit geheimem Schlüssel

Bei Verschlüsselungsalgorithmen mit geheimem Schlüssel werden die Daten mit einem einzigen geheimen Schlüssel ver- und entschlüsselt. Der Schlüssel muss vor dem Zugriff Unbefugter geschützt werden, da jeder, der im Besitz des Schlüssels ist, Ihre Daten entschlüsseln oder eigene Daten verschlüsseln und als Ihre Daten ausgeben kann.

Die Verschlüsselung mit geheimem Schlüssel wird auch als symmetrische Verschlüsselung bezeichnet, da für das Ver- und Entschlüsseln derselbe Schlüssel verwendet wird. Die Verschlüsselungsalgorithmen mit geheimem Schlüssel sind im Vergleich zu den Algorithmen mit öffentlichem Schlüssel außergewöhnlich schnell und gut für die kryptografische Transformation großer Datenstreams geeignet. Asymmetrische Verschlüsselungsalgorithmen wie RSA sind hinsichtlich der Datenmenge, die verschlüsselt werden kann, mathematisch eingeschränkt. Symmetrische Verschlüsselungsalgorithmen haben diese Probleme im Allgemeinen nicht.

Ein Algorithmus mit geheimem Schlüssel, eine so genannte Blockchiffre, wird zum Verschlüsseln von jeweils einem Datenblock verwendet. Blockverschlüsselungsverfahren wie DES (Data Encryption Standard), TripleDES und AES (Advanced Encryption Standard transformieren einen Eingabeblock mit *n* Bytes in einen Ausgabeblock mit verschlüsselten Bytes kryptografisch. Wenn eine Bytefolge ver- oder entschlüsselt werden soll, muss das blockweise geschehen. Da *n* klein ist (8 Bytes bei DES und TripleDES, 16 Bytes [Standard], 24 Bytes oder 32 Bytes bei AES), müssen Werte, die größer als *n* sind, jeweils blockweise verschlüsselt werden. Datenwerte, die kleiner als *n* sind, müssen auf *n* erweitert werden, um verarbeitet werden zu können.

Eine einfache Form einer Blockchiffre wird als ECB-Modus (Electronic Codebook) bezeichnet. Der ECB-Modus gilt als nicht sicher, da zum Initialisieren des ersten Klartextblocks kein Initialisierungsvektor verwendet wird. Bei einem geheimen Schlüssel *k*wird ein Eingabeblock mit Klartext mithilfe einer einfachen Blockchiffre ohne Initialisierungsvektor in denselben Ausgabeblock mit verschlüsseltem Text transformiert. Wenn der Klartexteingabestream doppelte Blöcke enthält, befinden sich diese somit auch im verschlüsselten Textausgabestream. Diese doppelten Ausgabeblöcke weisen darauf hin, dass für die schwache Codierung nicht autorisierte Benutzer die möglicherweise eingesetzten Algorithmen verwendet haben, und geben die möglichen Angriffsformen an. Der ECB-Verschlüsselungsverfahrensmodus kann daher recht leicht analysiert und somit der Schlüssel leicht erkannt werden.

Für die Blockchiffreklassen in der Basisklassenbibliothek wird ein Standardverkettungsmodus mit der Bezeichnung Cipher Block Chaining (CBC) verwendet. Sie können diese Standardeinstellung jedoch ändern, wenn Sie möchten.

Bei CBC-Verschlüsselungsverfahren wurden die bei ECB-Verschlüsselungsverfahren vorhandenen Probleme durch die Verwendung eines Initialisierungsvektors (IV) zum Verschlüsseln des ersten Klartextblocks behoben. Mit jedem nachfolgenden Klartextblock wird vor der Verschlüsselung eine bitweise`XOR`-Operation mit dem vorherigen verschlüsselten Block durchgeführt. Somit hängt jeder verschlüsselte Block von allen vorhergehenen Blöcken ab. Mit diesem System ist es nicht möglich, anhand häufig verwendeter Nachrichtenheader, die einem Unbefugten bekannt sein könnten, den Schlüssel zurückzuentwickeln.

Eine Möglichkeit, mit einem CBC-Verschlüsselungsverfahren verschlüsselte Daten unbefugt zu entschlüsseln, ist das Ausprobieren jedes möglichen Schlüssels. Je nach Größe des verwendeten Schlüssels ist diese Suchmethode jedoch selbst mit dem schnellsten Rechner äußerst zeitaufwendig und daher nicht realisierbar. Größere Schlüssel sind schwieriger zu entschlüsseln. Obwohl mit dem Verschlüsseln das Lesen verschlüsselter Daten für Unbefugte theoretisch nicht völlig ausgeschlossen ist, treibt es doch den Kostenaufwand in die Höhe. Wenn es mit einer umfassenden Suche drei Monate dauert, Daten zu entziffern, die nur ein paar Tage lang von Bedeutung sind, ist diese Suchmethode unbrauchbar.

Die Verschlüsselung mit geheimem Schlüssel hat den Nachteil, dass sich zwei Teilnehmer auf einen Schlüssel und einen Initialisierungsvektor geeinigt und die entsprechenden Werte ausgetauscht haben müssen. Der Initialisierungsvektor ist nicht geheim und kann mit der Nachricht in Klartext übermittelt werden. Der Schlüssel muss jedoch vor Unbefugten geheim gehalten werden. Aufgrund dieser Probleme wird die Verschlüsselung mit geheimem Schlüssel oft in Verbindung mit der Verschlüsselung mit öffentlichem Schlüssel eingesetzt, um die Werte von Schlüssel und Initialisierungsvektor vertraulich zu kommunizieren.

Vorausgesetzt, dass Alice und Bob um zwei Teilnehmer, die über einen unsicheren Kanal miteinander kommunizieren möchten handelt, können sie die Verschlüsselung mit geheimem Schlüssel wie folgt verwenden: Alice und Bob stimmen auf einen bestimmten Algorithmus (z. B. AES) mit einem bestimmten Schlüssel und Initialisierungsvektor zu verwenden. Alice verfasst eine Nachricht und erstellt einen Netzwerkstream (eventuell eine benannte Pipe oder eine Netzwerk-e-Mail) auf dem die Nachricht zu senden. Danach verschlüsselt sie mithilfe des Schlüssels und des Initialisierungsvektors den Text und sendet die verschlüsselten Nachricht und den Initialisierungsvektor über das Intranet an Bob. Bob empfängt den verschlüsselten Text und entschlüsselt ihn mit dem Initialisierungsvektor und dem zuvor vereinbarten Schlüssel. Wenn die Übertragung abgefangen wird, kann der unbefugte Dritte die Originalnachricht nicht entschlüsseln, da er den Schlüssel nicht kennt. In diesem Szenario muss nur der Schlüssel geheim bleiben. In der Realität würde entweder Alice oder Bob einen geheimen (symmetrischen) Schlüssel erzeugen und ihn mithilfe der asymmetrischen Verschlüsselung (mit öffentlichem Schlüssel) an die Gegenseite übertragen. Weitere Informationen zur Verschlüsselung mit öffentlichem Schlüssel finden Sie im nachfolgenden Abschnitt.

.NET Framework bietet die folgenden Klassen, die Verschlüsselungsalgorithmen mit geheimem Schlüssel implementieren:

- <xref:System.Security.Cryptography.AesManaged> (eingeführt in .NET Framework 3.5).

- <xref:System.Security.Cryptography.DESCryptoServiceProvider>.

- <xref:System.Security.Cryptography.HMACSHA1> (Technisch gesehen handelt es sich hierbei um einen Algorithmus mit geheimem Schlüssel, da er einen Nachrichtenauthentifizierungscode darstellt, der mithilfe einer kryptografischen Hashfunktion und einem geheimen Schlüssel berechnet wird. Siehe [Hashwerte](#hash_values)weiter unten in diesem Thema.)

- <xref:System.Security.Cryptography.RC2CryptoServiceProvider>.

- <xref:System.Security.Cryptography.RijndaelManaged>

- <xref:System.Security.Cryptography.TripleDESCryptoServiceProvider>.

[Zurück nach oben](#top)

<a name="public_key"></a>

## <a name="public-key-encryption"></a>Verschlüsselung mit öffentlichem Schlüssel

Bei der Verschlüsselung mit öffentlichem Schlüssel werden zwei Schlüssel verwendet, nämlich ein privater Schlüssel, der vor Unbefugten geheim gehalten werden muss, und ein öffentlicher Schlüssel, der jedem zugänglich sein kann. Der öffentliche und der private Schlüssel sind mathematisch miteinander verknüpft. Mit dem öffentlichen Schlüssel verschlüsselte Daten können nur mit dem privaten Schlüssel entschlüsselt werden, und mit dem privaten Schlüssel signierte Daten können nur mit dem öffentlichen Schlüssel überprüft werden. Der öffentliche Schlüssel kann jedem zugänglich sein, da er zum Verschlüsseln von Daten verwendet wird, die an den Inhaber des privaten Schlüssels gesendet werden. Kryptografische Algorithmen mit öffentlichem Schlüssel werden auch als asymmetrische Algorithmen bezeichnet, da ein Schlüssel für das Verschlüsseln der Daten und ein anderer für das Entschlüsseln erforderlich ist. Eine grundlegende kryptografische Regel verhindert die Schlüsselwiederverwendung, und beide Schlüssel müssen für jede Kommunikationssitzung eindeutig sein. In der Praxis jedoch sind asymmetrische Schlüssel im Allgemeinen langlebig.

Zwei Teilnehmer (Alice und Bob) könnten die Verschlüsselung mit öffentlichem Schlüssel wie folgt verwenden: Zuerst erzeugt Alice ein öffentliches/privates Schlüsselpaar. Wenn Bob Alice eine verschlüsselte Nachricht senden möchte, bittet er Alice um den öffentlichen Schlüssel. Alice sendet Bob ihren öffentlichen Schlüssel über ein unsicheres Netzwerk, und Bob verschlüsselt damit eine Nachricht. Bob sendet die verschlüsselte Nachricht an Alice, die sie mit ihrem privaten Schlüssel entschlüsselt. Wenn Bob den Schlüssel von Alice über einen unsicheren Kanal (z. B. ein öffentliches Netzwerk) erhalten hat, ist Bob im Hinblick auf einen Man-in-the-middle-Angriff gefährdet. Daher muss Bob bei Alice nachfragen, ob es sich um die richtige Kopie des öffentlichen Schlüssels handelt.

Während der Übertragung des öffentlichen Schlüssels von Alice hätte ein Unbefugter den Schlüssel abfangen können. Außerdem hätte derselbe Unbefugte auch die verschlüsselte Nachricht von Bob abfangen können. Er kann die Nachricht mit dem öffentlichen Schlüssel jedoch nicht entschlüsseln. Die Nachricht kann nur mit Alices privatem Schlüssel entschlüsselt werden, der nicht übertragen wurde. Alice benutzt für die Verschlüsselung der Rückantwort an Bob nicht ihren privaten Schlüssel, da jeder mit dem öffentlichen Schlüssel die Nachricht entschlüsseln könnte. Wenn Alice eine Rückantwort an Bob senden möchte, bittet sie Bob um dessen öffentlichen Schlüssel und verschlüsselt ihre Nachricht damit. Bob wiederum entschlüsselt die Nachricht mit seinem zugehörigen privaten Schlüssel.

In diesem Szenario würden Alice und Bob die (asymmetrische) Verschlüsselung mit öffentlichem Schlüssel zum Übertragen eines geheimen (symmetrischen) Schlüssels verwenden und für die restliche Sitzung die Verschlüsselung mit geheimem Schlüssel.

In der folgenden Liste werden Kryptographiealgorithmen mit öffentlichem und geheimem Schlüssel verglichen:

- Für kryptografische Algorithmen mit öffentlichem Schlüssel wird eine feste Puffergröße verwendet, während solche mit geheimem Schlüssel Puffer mit variabler Länge erfordern.

- Algorithmen mit öffentlichem Schlüssel können nicht zum Verketten von Daten in Streams verwendet werden, wie das bei Algorithmen mit geheimem Schlüssel möglich ist, da nur kleine Datenmengen verschlüsselt werden können. Daher wird bei asymmetrischen Operationen ein anderes Streamingmodell als bei symmetrischen Operationen verwendet.

- Bei der Verschlüsselung mit öffentlichem Schlüssel steht eine größere Schlüssellänge (Bereich von möglichen Werten für den Schlüssel) als bei der Verschlüsselung mit geheimem Schlüssel zur Verfügung. Daher ist die Verschlüsselung mit öffentlichem Schlüssel weniger anfällig für Brute-Force-Attacken, bei denen alle möglichen Schlüssel ausprobiert werden.

- Öffentliche Schlüssel sind problemlos zu verteilen, da sie nicht geschützt werden müssen, vorausgesetzt, es gibt eine Möglichkeit, die Identität des Absenders zu überprüfen.

- Einige Algorithmen mit öffentlichem Schlüssel (wie RSA und DAS, jedoch nicht Diffie-Hellman) können zum Erstellen digitaler Signaturen verwendet werden, mit denen die Identität des Absenders der Daten überprüft wird.

- Algorithmen mit öffentlichem Schlüssel sind im Vergleich zu Algorithmen mit geheimem Schlüssel extrem langsam und für die Verschlüsselung großer Datenmengen nicht geeignet. Algorithmen mit öffentlichem Schlüssel sind nur für die Übertragung sehr kleiner Datenmengen sinnvoll. In der Regel werden bei der Verschlüsselung mit öffentlichem Schlüssel ein Schlüssel und ein Initialisierungsvektor verschlüsselt, die in einem Algorithmus mit geheimem Schlüssel verwendet werden sollen. Nach der Übertragung von Schlüssel und Initialisierungsvektor wird für die restliche Sitzung die Verschlüsselung mit geheimem Schlüssel verwendet.

.NET Framework bietet die folgenden Klassen, die Algorithmen für Verschlüsselung mit öffentlichem Schlüssel implementieren:

- <xref:System.Security.Cryptography.DSACryptoServiceProvider>

- <xref:System.Security.Cryptography.RSACryptoServiceProvider>

- <xref:System.Security.Cryptography.ECDiffieHellman> (Basisklasse)

- <xref:System.Security.Cryptography.ECDiffieHellmanCng>

- <xref:System.Security.Cryptography.ECDiffieHellmanCngPublicKey> (Basisklasse)

- <xref:System.Security.Cryptography.ECDiffieHellmanKeyDerivationFunction> (Basisklasse)

- <xref:System.Security.Cryptography.ECDsaCng>

RSA ermöglicht sowohl die Verschlüsselung als auch die Signatur. DSA kann dagegen nur für die Signatur und Diffie-Hellman nur für die Erzeugung von Schlüsseln verwendet werden. Algorithmen mit öffentlichem Schlüssel sind im Hinblick auf ihre Verwendung stärker eingeschränkt als Algorithmen mit privatem Schlüssel.

[Zurück nach oben](#top)

<a name="digital_signatures"></a>

## <a name="digital-signatures"></a>Digitale Signaturen

Algorithmen mit öffentlichem Schlüssel können auch für digitale Signaturen verwendet werden. Digitale Signaturen authentifizieren die Identität eines Absenders (wenn Sie dem öffentlichen Schlüssel des Absenders vertrauen) und schützen die Datenintegrität. Mit dem von Alice erzeugten öffentlichen Schlüssel kann der Empfänger von Alices Daten überprüfen, dass sie tatsächlich von Alice gesendet wurden. Dazu vergleicht er die digitale Signatur mit Alices Daten mit ihrem öffentlichen Schlüssel.

Um die Kryptografie mit öffentlichem Schlüssel zum digitalen Signieren einer Nachricht zu verwenden, wendet Alice zunächst einen Hashalgorithmus auf die Nachricht an, um einen Message Digest zu erstellen. Der Message Digest ist eine komprimierte und eindeutige Darstellung von Daten. Danach verschlüsselt Alice den Message Digest mit ihrem privaten Schlüssel und erstellt so ihre persönliche Signatur. Beim Empfang der Nachricht und der Signatur entschlüsselt Bob die Signatur mit dem öffentlichen Schlüssel von Alice, um den Message Digest wiederherzustellen. Dann wendet er denselben Hashalgorithmus auf die Nachricht an, den auch Alice verwendet hat. Wenn der von Bob ermittelte Message Digest exakt mit dem von Alice empfangenen Message Digest übereinstimmt, kann Bob sicher sein, dass die Nachricht vom Besitzer des privaten Schlüssels stammt und die Daten nicht modifiziert wurden. Wenn Bob darauf vertraut, dass Alice der Besitzer des privaten Schlüssels ist, weiß er, dass die Nachricht von Alice stammt.

> [!NOTE]
> Eine Signatur kann von jedem überprüft werden, da der öffentliche Schlüssel des Absenders allgemein bekannt und in der Regel im digitalen Signaturformat enthalten ist. Mit dieser Methode wird die Nachricht nicht geheim gehalten. Hierzu muss sie zusätzlich verschlüsselt werden.

.NET Framework bietet die folgenden Klassen, die digitale Signaturalgorithmen implementiert:

- <xref:System.Security.Cryptography.DSACryptoServiceProvider>

- <xref:System.Security.Cryptography.RSACryptoServiceProvider>

- <xref:System.Security.Cryptography.ECDsa> (Basisklasse)

- <xref:System.Security.Cryptography.ECDsaCng>

 [Zurück nach oben](#top)

<a name="hash_values"></a>

## <a name="hash-values"></a>Hashwerte

Mit Hashalgorithmen werden kleineren binären Werten fester Länge, die als Hashwerte bezeichnet werden, binäre Werte beliebiger Länge zugeordnet. Ein Hashwert ist eine numerische Darstellung eines Datenelements. Wenn ein Klartextabsatz gehasht ist und nur ein Buchstabe geändert wird, ergibt sich bei einem nachfolgenden Hashvorgang ein anderer Wert. Wenn der Hashvorgang kryptografisch stark ist, ändert sich der zugehörige Wert erheblich. Wenn sich beispielsweise ein einzelnes Bit einer Nachricht ändert, kann eine starke Hashfunktion ein um 50 % anderes Ergebnis liefern. Viele Eingabewerte ergeben möglicherweise denselben Hashausgabewert. Dennoch ist es rechnerisch unmöglich, zwei verschiedene Eingabewerte zu ermitteln, die denselben Hashwert bilden.

Zwei Teilnehmer (Alice und Bob) könnten eine Hashfunktion verwenden, um die Nachrichtenintegrität sicherzustellen. Sie würden einen Hashalgorithmus zum Signieren ihrer Nachrichten auswählen. Alice schreibt eine Nachricht und erstellt dann mithilfe des ausgewählten Algorithmus einen Hash dieser Nachricht. Die Teilnehmer würden dann eine der folgenden Methoden verwenden:

- Alice sendet die Klartext-Nachricht und die Hashnachricht (digitale Signatur) an Bob. Bob empfängt die Nachricht, wendet den Hashalgorithmus darauf an und vergleicht seinen Hashwert mit dem von Alice empfangenen Hashwert. Wenn die Hashwerte identisch sind, wurde die Nachricht nicht geändert. Wenn die Werte nicht identisch sind, wurde die Nachricht geändert, nachdem sie von Alice geschrieben wurde.

  Leider wird mit dieser Methode nicht die Echtheit des Absenders angegeben. Jeder kann die Identität von Alice annehmen und eine Nachricht an Bob senden. Derselbe Hashalgorithmus kann zum Signieren der Nachricht verwendet werden, und Bob kann lediglich feststellen, dass die Nachricht mit ihrer Signatur übereinstimmt. Dies ist eine Form eines Man-in-the-middle-Angriffs. Weitere Informationen finden Sie unter [Beispiel für sichere Cryptography Next Generation (CNG) Kommunikation](https://docs.microsoft.com/previous-versions/cc488018(v=vs.100)).

- Alice sendet die Klartext-Nachricht über einen unsicheren öffentlichen Kanal an Bob. Sie sendet die Hashnachricht über einen sicheren privaten Kanal an Bob. Bob empfängt die Klartext-Meldung, wendet den Hashalgorithmus darauf an, und vergleicht den Hash mit dem privat ausgetauschten Hash. Wenn die Hashs zusammenpassen, weiß Bob zwei Dinge:

  - Die Nachricht wurde nicht geändert.

  - Der Absender der Nachricht (Alice) ist authentisch.

  Damit dieses System funktioniert, muss Alice den originalen Hashwert geheim halten. Nur Bob darf ihn kennen.

- Alice sendet die Klartext-Nachricht über einen unsicheren öffentlichen Kanal an Bob und platziert die Haschnachricht auf ihrer öffentlich zugänglichen Website.

  Mit dieser Methode wird eine Manipulation der Nachricht verhindert, da jeder an einer Änderung des Hashwerts gehindert wird. Obwohl die Nachricht und deren Hash von jedem gelesen werden kann, kann der Hashwert nur von Alice geändert werden. Ein Angreifer, der die Identität von Alice annehmen will, müsste Zugriff auf die Website von Alice haben.

Mit keiner der vorherigen Methoden wird verhindert, dass Dritte die Nachrichten von Alice lesen, da sie als Klartext übertragen werden. Vollständige Sicherheit ist in der Regel nur mit digitalen Signaturen (Signieren von Nachrichten) und Verschlüsselung möglich.

.NET Framework bietet die folgenden Klassen, die Hashalgorithmen implementiert:

- <xref:System.Security.Cryptography.HMACSHA1>.

- <xref:System.Security.Cryptography.MACTripleDES>

- <xref:System.Security.Cryptography.MD5CryptoServiceProvider>

- <xref:System.Security.Cryptography.RIPEMD160>

- <xref:System.Security.Cryptography.SHA1Managed>

- <xref:System.Security.Cryptography.SHA256Managed>

- <xref:System.Security.Cryptography.SHA384Managed>

- <xref:System.Security.Cryptography.SHA512Managed>.

- HMAC-Varianten aller SHA-Algorithmen (Secure Hash Algorithm), MD5-Algorithmen (Message Digest 5) und RIPEMD-160-Algorithmen.

- CryptoServiceProvider-Implementierungen (Wrapper für verwalteten Code) aller SHA-Algorithmen.

- CNG-Implementierungen (Cryptography Next Generation) aller MD5- und SHA-Algorithmen.

> [!NOTE]
> Fehler im Design von MD5 wurden 1996 erkannt und stattdessen SHA-1 empfohlen. 2004 wurden weitere Fehler festgestellt, und der MD5-Algorithmus galt nicht mehr als sicher. Der SHA-1-Algorithmus wurde ebenfalls als unsicher eingestuft, und nun wird stattdessen SHA-2 empfohlen.

[Zurück nach oben](#top)

<a name="random_numbers"></a>

## <a name="random-number-generation"></a>Zufallszahlengenerierung

Die Zufallszahlengenerierung ist wichtiger Bestandteil vieler kryptografischer Vorgänge. Kryptografische Schlüssel müssen z. B. möglichst zufällig erzeugt werden, sodass ein Replizieren unmöglich ist. Mit Generatoren für kryptografische Zufallszahlen müssen Ausgabewerte erzeugt werden, die rechnerisch mit einer Wahrscheinlichkeit von weniger als 0,5 vorhergesagt werden können. Deshalb darf jede Methode zur Vorhersage des nächsten Ausgabebits nicht besser sein als eine bloße Vermutung. Die Klassen in .NET Framework verwenden Zufallszahlengeneratoren kryptografische Schlüssel zu generieren.

Die <xref:System.Security.Cryptography.RNGCryptoServiceProvider> -Klasse ist die Implementierung eines Algorithmus mit Zufallszahlengenerator.

[Zurück nach oben](#top)

<a name="clickonce"></a>

## <a name="clickonce-manifests"></a>ClickOnce-Manifeste

Die folgenden kryptografischen Klassen in .NET Framework 3.5 können Sie abrufen und überprüfen die Informationen zu manifestsignaturen für Anwendungen, die mit bereitgestellt werden [ClickOnce-Technologie](/visualstudio/deployment/clickonce-security-and-deployment):

- Die <xref:System.Security.Cryptography.ManifestSignatureInformation> -Klasse ruft Informationen zu einer Manifestsignatur ab, wenn Sie deren <xref:System.Security.Cryptography.ManifestSignatureInformation.VerifySignature%2A> -Methodenüberladungen verwenden.

- Sie können die <xref:System.Security.ManifestKinds> -Enumeration verwenden, um die Manifeste anzugeben, die überprüft werden sollen. Das Ergebnis der Überprüfung ist einer der <xref:System.Security.Cryptography.SignatureVerificationResult> -Enumerationswerte.

- Die <xref:System.Security.Cryptography.ManifestSignatureInformationCollection> -Klasse stellt eine schreibgeschützte Auflistung der <xref:System.Security.Cryptography.ManifestSignatureInformation> -Objekte der überprüften Signatur bereit.

 Außerdem stellen die folgenden Klassen bestimmte Signaturinformationen bereit:

- <xref:System.Security.Cryptography.StrongNameSignatureInformation> Enthält die Informationen zur starken Namenssignatur für ein Manifest.

- <xref:System.Security.Cryptography.X509Certificates.AuthenticodeSignatureInformation> Stellt die Informationen zur Authenticode-Signatur für ein Manifest dar.

- <xref:System.Security.Cryptography.X509Certificates.TimestampInformation> Enthält Informationen zum Zeitstempel einer Authenticode-Signatur.

- <xref:System.Security.Cryptography.X509Certificates.TrustStatus> Liefert eine einfache Möglichkeit, um zu überprüfen, ob eine Authenticode-Signatur vertrauenswürdig ist.

[Zurück nach oben](#top)

<a name="suite_b"></a>

## <a name="suite-b-support"></a>Suite B-Unterstützung

.NET Framework 3.5 unterstützt die Suite B-Satz kryptografischer Algorithmen, die von der National Security Agency (NSA) veröffentlicht. Weitere Informationen zur Suite B finden Sie im [NSA-Suite-B-Kryptographie-Merkblatt](https://www.nsa.gov/what-we-do/information-assurance/).

Dazu gehören die folgenden Algorithmen:

- AES-Algorithmus (Advanced Encryption Standard) mit Schlüsselgrößen von 128, 192 und 256 Bit für die Verschlüsselung.

- SHA-1, SHA-256, SHA-384 und SHA-512 für Hashverfahren. (Die letzten beiden werden meist unter der Bezeichnung SHA-2 zusammengefasst.)

- ECDSA (Elliptic Curve Digital Signature Algorithm) unter Verwendung von Kurven von 256-Bit-, 384-Bit- und 521-Bit-Primzahlenmodulen für Signaturen. Die NSA-Dokumentation definiert diese Kurven ausdrücklich und nennt sie P-256, P-384 und P-521. Dieser Algorithmus wird von der <xref:System.Security.Cryptography.ECDsaCng> -Klasse bereitgestellt. Er ermöglicht das Signieren mit einem privaten Schlüssel und das Überprüfen mit einem öffentlichen Schlüssel.

- ECDH-Algorithmus (Elliptic Curve Diffie-Hellman) mit Kurven von 256-Bit-, 384-Bit- und 521-Bit-Primzahlenmodulen für den Schlüsselaustausch und Geheimvertrag. Dieser Algorithmus wird von der <xref:System.Security.Cryptography.ECDiffieHellmanCng> -Klasse bereitgestellt.

Wrapper für verwalteten Code für die FIPS-zertifizierten (Federal Information Processing Standard) Implementierungen von AES, SHA-256, SHA-384 und SHA-512 sind in den neuen Klassen <xref:System.Security.Cryptography.AesCryptoServiceProvider>, <xref:System.Security.Cryptography.SHA256CryptoServiceProvider>, <xref:System.Security.Cryptography.SHA384CryptoServiceProvider>und <xref:System.Security.Cryptography.SHA512CryptoServiceProvider> verfügbar.

[Zurück nach oben](#top)

<a name="cng"></a>

## <a name="cryptography-next-generation-cng-classes"></a>CNG-Klassen (Cryptography Next Generation)

Die CNG-Klassen (Cryptography Next Generation) stellen einen verwalteten Wrapper um die systemeigenen CNG-Funktionen bereit. (CNG ist der Ersatz für CryptoAPI.) "Cng" ist Teil des Namens dieser Klassen. Zentrales Element dieser CNG-Wrapperklassen ist die <xref:System.Security.Cryptography.CngKey> -Schlüsselcontainerklasse, die die Speicherung und Verwendung von CNG-Schlüsseln abstrahiert. Diese Klasse ermöglicht es, ein Schlüsselpaar oder einen öffentlichen Schlüssel sicher zu speichern und mittels eines einfachen Zeichenfolgennamens auf diesen zu verweisen. Die ECDSA-basierte <xref:System.Security.Cryptography.ECDsaCng> -Signaturklasse und die <xref:System.Security.Cryptography.ECDiffieHellmanCng> -Verschlüsselungsklasse können <xref:System.Security.Cryptography.CngKey> -Objekte verwenden.

Die <xref:System.Security.Cryptography.CngKey> -Klasse wird für eine Vielzahl zusätzlicher Operationen verwendet, einschließlich dem Öffnen, Erstellen, Löschen und Exportieren von Schlüsseln. Sie stellt auch den Zugriff auf das zugrunde liegende Schlüsselhandle bereit, das für den direkten Aufruf systemeigener Funktionen verwendet wird.

.NET Framework 3.5 enthält auch eine Reihe von CNG-Klassen, wie die folgende Unterstützung:

- <xref:System.Security.Cryptography.CngProvider> verwaltet einen Schlüsselspeicheranbieter.

- <xref:System.Security.Cryptography.CngAlgorithm> verwaltet einen CNG-Algorithmus.

- <xref:System.Security.Cryptography.CngProperty> verwaltet häufig verwendete Schlüsseleigenschaften.

[Zurück nach oben](#top)

<a name="related_topics"></a>

## <a name="related-topics"></a>Verwandte Themen

|Titel|Beschreibung|
|-----------|-----------------|
|[Kryptografiemodell](../../../docs/standard/security/cryptography-model.md)|Beschreibt das Implementieren von Kryptografie in der Basisklassenbibliothek.|
|[Exemplarische Vorgehensweise: Erstellen einer kryptografischen Anwendung](../../../docs/standard/security/walkthrough-creating-a-cryptographic-application.md)|Veranschaulicht grundlegende Verschlüsselungs- und Entschlüsselungsaufgaben.|
|[Konfigurieren kryptografischer Klassen](../../../docs/framework/configure-apps/configure-cryptography-classes.md)|Beschreibt das Zuordnen von Algorithmusnamen zu kryptografischen Klassen und von Objektbezeichnern zu einem kryptografischen Algorithmus.|
