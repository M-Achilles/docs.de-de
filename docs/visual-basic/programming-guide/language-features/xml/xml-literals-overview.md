---
title: Übersicht zu XML-Literalen (Visual Basic)
ms.date: 07/20/2015
helpviewer_keywords:
- XML literals [Visual Basic], about XML literals
- declaring XML literals [Visual Basic]
- LINQ to XML [Visual Basic], XML literals
- literals [Visual Basic], XML
ms.assetid: 37987c15-4ab8-471b-bd45-399816bfb57f
ms.openlocfilehash: 4024f4ad2b2aa8cb1897e83d87a7a00b1ba25e67
ms.sourcegitcommit: 68653db98c5ea7744fd438710248935f70020dfb
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/22/2019
ms.locfileid: "69964706"
---
# <a name="xml-literals-overview-visual-basic"></a>Übersicht zu XML-Literalen (Visual Basic)
Mithilfe eines *XML* -Literals können Sie XML direkt in den Visual Basic-Code einbinden. Die XML-Literalsyntax stellt-Objekte dar [!INCLUDE[sqltecxlinq](~/includes/sqltecxlinq-md.md)] und ähnelt der Syntax von XML 1,0. Dadurch wird das programmgesteuerte Erstellen von XML-Elementen und-Dokumenten vereinfacht, da der Code die gleiche Struktur wie der endgültige XML-Code aufweist.  
  
 Visual Basic kompiliert XML-Literale in [!INCLUDE[sqltecxlinq](~/includes/sqltecxlinq-md.md)] -Objekte. [!INCLUDE[sqltecxlinq](~/includes/sqltecxlinq-md.md)]stellt ein einfaches Objektmodell zum Erstellen und Bearbeiten von XML bereit, und dieses Modell lässt [!INCLUDE[vbteclinqext](~/includes/vbteclinqext-md.md)]sich gut in integrieren. Weitere Informationen finden Sie unter <xref:System.Xml.Linq.XElement>.  
  
 Sie können einen Visual Basic Ausdruck in ein XML-Literalformat einbetten. Zur Laufzeit erstellt die Anwendung ein [!INCLUDE[sqltecxlinq](~/includes/sqltecxlinq-md.md)] -Objekt für jedes literalobjekt, das die Werte der eingebetteten Ausdrücke einbezieht. Auf diese Weise können Sie dynamischen Inhalt innerhalb eines XML-Literals angeben. Weitere Informationen finden Sie unter [eingebettete Ausdrücke in XML](../../../../visual-basic/programming-guide/language-features/xml/embedded-expressions-in-xml.md).  
  
 Weitere Informationen zu den Unterschieden zwischen der XML-Literalsyntax und der Syntax von XML 1,0 finden Sie unter [XML-Literale und die XML 1,0-Spezifikation](../../../../visual-basic/programming-guide/language-features/xml/xml-literals-and-the-xml-1-0-specification.md).  
  
## <a name="simple-literals"></a>Einfache Literale  
 Sie können ein- [!INCLUDE[sqltecxlinq](~/includes/sqltecxlinq-md.md)] Objekt im Visual Basic Code erstellen, indem Sie ein gültiges XML eingeben oder einfügen. Ein XML-Elementliteral <xref:System.Xml.Linq.XElement> gibt ein-Objekt zurück. Weitere Informationen finden Sie unter [XML](../../../../visual-basic/language-reference/xml-literals/xml-element-literal.md) - [Elementliterale und XML-Literale und in der XML 1,0-Spezifikation](../../../../visual-basic/programming-guide/language-features/xml/xml-literals-and-the-xml-1-0-specification.md). Im folgenden Beispiel wird ein XML-Element erstellt, das über mehrere untergeordnete Elemente verfügt.  
  
 [!code-vb[VbXMLSamples#5](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbXMLSamples/VB/XMLSamples2.vb#5)]  
  
 Sie können ein XML-Dokument erstellen, indem Sie ein XML `<?xml version="1.0"?>`-wahrsten mit starten, wie im folgenden Beispiel gezeigt. Ein XML-Dokumentliteral <xref:System.Xml.Linq.XDocument> gibt ein-Objekt zurück. Weitere Informationen finden Sie unter [XML Document Literale](../../../../visual-basic/language-reference/xml-literals/xml-document-literal.md).  
  
 [!code-vb[VbXMLSamples#6](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbXMLSamples/VB/XMLSamples2.vb#6)]  
  
> [!NOTE]
> Die XML-Literalsyntax in Visual Basic ist nicht identisch mit der Syntax in der XML 1,0-Spezifikation. Weitere Informationen finden Sie unter [XML-Literale und die XML 1,0-Spezifikation](../../../../visual-basic/programming-guide/language-features/xml/xml-literals-and-the-xml-1-0-specification.md).  
  
## <a name="line-continuation"></a>Zeilen Fortsetzung  
 Ein XML-Literalwert kann sich über mehrere Zeilen erstrecken, ohne Zeilen Fortsetzungs Zeichen (die Zeichenfolge mit Leerzeichen) zu verwenden. Dies erleichtert das Vergleichen von XML-Literalen im Code mit XML-Dokumenten.  
  
 Der Compiler behandelt Zeilen Fortsetzungs Zeichen als Teil eines XML-Literals. Daher sollten Sie die Leerzeichen-unterstrich-Sequenz nur dann verwenden, wenn Sie in [!INCLUDE[sqltecxlinq](~/includes/sqltecxlinq-md.md)] das-Objekt gehört.  
  
 Sie benötigen jedoch Zeilen Fortsetzungs Zeichen, wenn ein mehrzeiligen Ausdruck in einem eingebetteten Ausdruck vorhanden ist. Weitere Informationen finden Sie unter [eingebettete Ausdrücke in XML](../../../../visual-basic/programming-guide/language-features/xml/embedded-expressions-in-xml.md).  
  
## <a name="embedding-queries-in-xml-literals"></a>Einbetten von Abfragen in XML-Literale  
 Sie können eine Abfrage in einem eingebetteten Ausdruck verwenden. Wenn Sie dies tun, werden die von der Abfrage zurückgegebenen Elemente dem XML-Element hinzugefügt. Auf diese Weise können Sie einen dynamischen Inhalt, z. b. das Ergebnis der Abfrage eines Benutzers, einem XML-Literalzeichen hinzufügen.  
  
 Im folgenden Code wird z. b. eine eingebettete Abfrage verwendet, um XML-Elemente aus `phoneNumbers2` den Membern des Arrays zu erstellen und diese `contact2`Elemente dann als untergeordnete Elemente von hinzuzufügen.  
  
 [!code-vb[VbXMLSamples#7](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbXMLSamples/VB/XMLSamples2.vb#7)]  
  
## <a name="how-the-compiler-creates-objects-from-xml-literals"></a>So erstellt der Compiler Objekte aus XML-Literalen  
 Der Visual Basic-Compiler übersetzt XML-Literale in Aufrufe der [!INCLUDE[sqltecxlinq](~/includes/sqltecxlinq-md.md)] entsprechenden Konstruktoren, um das [!INCLUDE[sqltecxlinq](~/includes/sqltecxlinq-md.md)] Objekt zu erstellen. Der Visual Basic-Compiler übersetzt z. b. das folgende Codebeispiel in einen Aufruf des <xref:System.Xml.Linq.XProcessingInstruction> Konstruktors für die XML-Versions Anweisung, Aufrufe des <xref:System.Xml.Linq.XElement> Konstruktors für `<contact>`, `<name>`und `<phone>` . -Elemente und Aufrufe an den <xref:System.Xml.Linq.XAttribute> -Konstruktor für `type` das-Attribut. Insbesondere, wenn die Attribute im folgenden Beispiel angegeben sind, ruft der Visual Basic Compiler den <xref:System.Xml.Linq.XAttribute.%23ctor%28System.Xml.Linq.XName%2CSystem.Object%29> Konstruktor zweimal auf. Der erste `type` übergibt den Wert für den `name` -Parameter und den Wert `home` für den `value` -Parameter. Die zweite übergibt `type` auch den Wert für den `name` -Parameter, jedoch den Wert `work` für den `value` -Parameter.  
  
 [!code-vb[VbXMLSamples#6](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbXMLSamples/VB/XMLSamples2.vb#6)]  
  
## <a name="see-also"></a>Siehe auch

- <xref:System.Xml.Linq.XElement>
- [Erstellen von XML in Visual Basic](../../../../visual-basic/programming-guide/language-features/xml/creating-xml.md)
- [Eingebettete Ausdrücke in XML](../../../../visual-basic/programming-guide/language-features/xml/embedded-expressions-in-xml.md)
- [XML-Dokumentliteral](../../../../visual-basic/language-reference/xml-literals/xml-document-literal.md)
- [XML-Elementliteral](../../../../visual-basic/language-reference/xml-literals/xml-element-literal.md)
- [XML-Literale](../../../../visual-basic/language-reference/xml-literals/index.md)
