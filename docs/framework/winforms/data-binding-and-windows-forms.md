---
title: Datenbindung und Windows Forms
ms.date: 03/30/2017
helpviewer_keywords:
- master-details lists
- data [Windows Forms], data binding
- reports [Windows Forms], Windows Forms
- lookup tables [Windows Forms], data binding
- data [Windows Forms], complex data binding
- data binding [Windows Forms], Windows Forms
- data [Windows Forms], simple data binding
- Windows Forms controls, data binding
- data-bound controls [Windows Forms], Windows Forms
ms.assetid: 419aac5e-819b-4aad-88b0-73a2f8c0bd27
ms.openlocfilehash: 240b68f901f819313fcae7aab0474abd5535c30d
ms.sourcegitcommit: c7a7e1468bf0fa7f7065de951d60dfc8d5ba89f5
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/14/2019
ms.locfileid: "65592307"
---
# <a name="data-binding-and-windows-forms"></a>Datenbindung und Windows Forms
In Windows Forms können Sie nicht nur an herkömmliche Datenquellen binden, sondern auch an beinahe alle Strukturen, die Daten enthalten. Sie können an ein Array von Werten binden, die Sie zur Laufzeit berechnen, aus einer Datei lesen oder aus den Werten anderer Steuerelemente ableiten.  
  
 Darüber hinaus können Sie jede Eigenschaft eines beliebigen Steuerelements an die Datenquelle binden. Bei der herkömmlichen Datenbindung binden Sie die Anzeigeeigenschaft, z. B. die <xref:System.Windows.Forms.Control.Text%2A>-Eigenschaft eines <xref:System.Windows.Forms.TextBox>-Steuerelements, normalerweise an die Datenquelle. Mit .NET Framework können Sie auch weitere Eigenschaften durch Bindung festzulegen. Mithilfe der Bindung können Sie folgende Aufgaben ausführen:  
  
- Festlegen der Grafik eines Bildsteuerelements.  
  
- Festlegen der Hintergrundfarbe für ein oder mehrere Steuerelemente.  
  
- Festlegen der Größe von Steuerelementen.  
  
 Datenbindung ist grundsätzlich ein automatisches Verfahren zum Festlegen der Laufzeitzugriffseigenschaften eines Steuerelements in einem Formular.  
  
## <a name="types-of-data-binding"></a>Typen der Datenbindung  
 Windows Forms nutzt zwei Typen der Datenbindung: einfache Bindung und komplexe Bindung. Jeder Typ bietet verschiedene Vorteile.  
  
|Typ der Datenbindung|Beschreibung|  
|--------------------------|-----------------|  
|Einfache Datenbindung|Die Fähigkeit eines Steuerelements zur Bindung an ein einzelnes Datenelement, z. B. ein Wert in einer Spalte in einer Dataset-Tabelle. Dies ist der Bindungstyp, der für Steuerelemente, wie z. B. ein <xref:System.Windows.Forms.TextBox>-Steuerelement oder ein <xref:System.Windows.Forms.Label>-Steuerelement typisch ist. Diese Steuerelemente zeigen normalerweise nur einen einzelnen Wert an. Tatsächlich kann jede Eigenschaft eines Steuerelements an ein Feld in einer Datenbank gebunden werden. Bietet umfassende Unterstützung für dieses Feature in Visual Studio.<br /><br /> Weitere Informationen finden Sie unter:<br /><br /> -   [Auf Datenbindung bezogene Schnittstellen](interfaces-related-to-data-binding.md)<br />-   [Vorgehensweise: Navigieren Sie durch Daten in Windows Forms](how-to-navigate-data-in-windows-forms.md)<br />-   [Vorgehensweise: Erstellen eines einfach gebundenen Steuerelements in Windows Forms](how-to-create-a-simple-bound-control-on-a-windows-form.md)|  
|Komplexe Datenbindung|Die Fähigkeit eines Steuerelements zur Bindung an mehr als ein Datenelement, in der Regel mehr als ein Datensatz in einer Datenbank. Komplexe Bindung wird auch als listenbasierte Bindung bezeichnet. Beispiele für Steuerelemente, die komplexe Bindung unterstützen, sind die Steuerelemente <xref:System.Windows.Forms.DataGridView>, <xref:System.Windows.Forms.ListBox> und <xref:System.Windows.Forms.ComboBox>. Ein Beispiel für komplexe Datenbindung, finden Sie unter [Vorgehensweise: Binden eines Windows Forms-Kombinationsfeld oder das ListBox-Steuerelement an Daten](./controls/how-to-bind-a-windows-forms-combobox-or-listbox-control-to-data.md).|  
  
## <a name="bindingsource-component"></a>BindingSource-Komponente  
 Um die Datenbindung zu vereinfachen, ermöglicht Ihnen Windows Forms die Bindung einer Datenquelle an die <xref:System.Windows.Forms.BindingSource>-Komponente und dann das Binden von Steuerelementen an die <xref:System.Windows.Forms.BindingSource>. Sie können die <xref:System.Windows.Forms.BindingSource> in einfachen oder komplexen Bindungsszenarios verwenden. In beiden Fällen fungiert die <xref:System.Windows.Forms.BindingSource> als Mittler zwischen der Datenquelle und gebundenen Steuerelementen und stellt Änderungsbenachrichtigung, Währungsverwaltung und andere Dienste bereit.  
  
## <a name="common-scenarios-that-employ-data-binding"></a>Allgemeine Szenarien, die Datenbindung nutzen  
 Fast jede kommerzielle Anwendung liest Informationen aus Datenquellen der einen oder anderen Art, in der Regel durch Datenbindung. Die folgende Liste zeigt einige der häufigsten Szenarien, die die Datenbindung als Methode zur Darstellung und Bearbeitung von Daten nutzen.  
  
|Szenario|Beschreibung|  
|--------------|-----------------|  
|Berichterstellung|Berichte bieten eine flexible Möglichkeit, Ihre Daten in einem gedruckten Dokument anzuzeigen und zusammenzufassen. Es ist üblich, einen Bericht zu erstellen, der ausgewählte Inhalte einer Datenquelle auf dem Bildschirm oder auf einem Drucker ausgibt. Allgemeine Berichte enthalten Listen, Rechnungen oder Zusammenfassungen. Elemente werden normalerweise in Listenspalten formatiert, wobei Unterelemente unter den einzelnen Listenelementen organisiert werden. Sie sollten aber das Layout auswählen, das Ihren Daten am besten entspricht.|  
|Dateneingabe|Eine gängige Methode, um große Mengen verknüpfter Daten einzugeben oder Benutzer aufzufordern, Informationen einzugeben, ist ein Dateneingabeformular. Benutzer können Informationen eingeben oder mit Textfeldern, Optionsfeldern, Dropdownlisten und Kontrollkästchen eine Auswahl treffen. Informationen werden dann an eine Datenbank übermittelt und dort gespeichert. Die Struktur der Datenbank basiert auf den eingegebenen Informationen.|  
|Master-/Detailbeziehung|Eine Master-/Detailanwendung ist ein Format zur Anzeige verknüpfter Daten. Es gibt zwei Tabellen mit Daten sowie eine sie verknüpfende Beziehung – im klassischen Geschäfsbeispiel eine Tabelle "Kunden" und eine Tabelle "Bestellungen" mit einer Beziehung, durch die Kunden und ihre Bestellungen verknüpft werden. Weitere Informationen zum Erstellen einer Master-/detailanwendung mit zwei Windows Forms <xref:System.Windows.Forms.DataGridView> Steuerelemente finden Sie [Vorgehensweise: Erstellen Sie eine Master-/Detailformulars mit zwei DataGridView-Steuerelementen in Windows Forms](./controls/create-a-master-detail-form-using-two-datagridviews.md)|  
|Suchtabelle|Ein weiteres gängiges Szenario für die Datenanzeige und -bearbeitung ist die Suchtabelle. Häufig wird als Teil einer größeren Datenanzeige ein <xref:System.Windows.Forms.ComboBox>-Steuerelement zum Anzeigen und Bearbeiten von Daten verwendet. Wichtig ist, dass sich die Daten, die im <xref:System.Windows.Forms.ComboBox>-Steuerelement angezeigt werden, von den Daten unterscheiden, die in die Datenbank geschrieben werden. Angenommen, Sie haben ein <xref:System.Windows.Forms.ComboBox>-Steuerelement, das die in einem Lebensmittelladen verfügbaren Artikel anzeigt. In diesem Fall würden Sie auch gerne die Bezeichnungen der Produkte (Brot, Milch, Eier) sehen. Um das Abrufen von Informationen innerhalb der Datenbank und die Datenbanknormalisierung zu vereinfachen, würden Sie die Informationen für die einzelnen Elemente einer bestimmten Bestellung aber wahrscheinlich als Artikelnummern (#501, #603 usw.) speichern. Dadurch besteht eine implizite Verbindung zwischen dem "Anzeigenamen" des Lebensmittels im <xref:System.Windows.Forms.ComboBox>-Steuerelement des Formulars und der verknüpften Artikelnummer in einer Bestellung. Dies ist der zentrale Aspekt der Tabellensuche. Weitere Informationen finden Sie unter [Vorgehensweise: Erstellen einer Suchtabelle mit der BindingSource-Komponente in Windows Forms](./controls/how-to-create-a-lookup-table-with-the-windows-forms-bindingsource-component.md).|  
  
## <a name="see-also"></a>Siehe auch

- <xref:System.Windows.Forms.Binding>
- [Windows Forms-Datenbindung](windows-forms-data-binding.md)
- [Vorgehensweise: Binden des DataGrid-Steuerelements in Windows Forms an eine Datenquelle](./controls/how-to-bind-the-windows-forms-datagrid-control-to-a-data-source.md)
- [BindingSource-Komponente](./controls/bindingsource-component.md)
