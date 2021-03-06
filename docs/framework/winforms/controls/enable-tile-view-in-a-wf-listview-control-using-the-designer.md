---
title: 'Vorgehensweise: Aktivieren der Tile-Ansicht in einem ListView-Steuerelement in Windows Forms mithilfe des Designers'
ms.date: 03/30/2017
helpviewer_keywords:
- tile view feature
- ListView control [Windows Forms], tile view
- tiling [Windows Forms], Windows Forms, controls
ms.assetid: 12f0816a-52b8-41ee-a6d9-ded3a8a5817a
ms.openlocfilehash: 8a45a8a484bd373f53585b1b113a51e59b30fca2
ms.sourcegitcommit: cf9515122fce716bcfb6618ba366e39b5a2eb81e
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/15/2019
ms.locfileid: "69040361"
---
# <a name="how-to-enable-tile-view-in-a-windows-forms-listview-control-using-the-designer"></a>Vorgehensweise: Aktivieren der Tile-Ansicht in einem ListView-Steuerelement in Windows Forms mithilfe des Designers
Mit der Kachel Ansicht des <xref:System.Windows.Forms.ListView> -Steuer Elements können Sie eine visuelle Balance zwischen grafischen und Textinformationen bereitstellen. Die textbasierten Daten, die für ein Element in der Ansicht "Nebeneinander" angezeigt werden, sind die gleichen wie die Spalteninformationen, die für die Detailansicht definiert wurden. Die Kachel Ansicht funktioniert in Kombination mit den Funktionen "Gruppieren" oder " <xref:System.Windows.Forms.ListView> Einfügemarke" im Steuerelement.

 In der Kachel Ansicht werden ein 32 x 32-Symbol und mehrere Textzeilen verwendet, wie in der folgenden Abbildung dargestellt.

 ![Kachel Ansicht in einem ListView-Steuer] Element (./media/enable-tile-view-in-a-wf-listview-control-using-the-designer/tile-view-in-listview-control.gif "Symbole und Text der Kachel Ansicht")

 Mit den Eigenschaften und Methoden der Kachel Ansicht können Sie angeben, welche Spalten Felder für die einzelnen Elemente angezeigt werden sollen. Darüber hinaus können Sie die Größe und Darstellung aller Elemente innerhalb eines Kachel Ansichts Fensters gemeinsam steuern. Aus Gründen der Übersichtlichkeit ist die erste Textzeile in einer Kachel immer der Name des Elements. Sie kann nicht geändert werden.

 Das folgende Verfahren erfordert ein **Windows-Anwendungs** Projekt mit einem Formular, <xref:System.Windows.Forms.ListView> das ein-Steuerelement enthält. Weitere Informationen zum Einrichten eines solchen Projekts finden [Sie unter Gewusst wie: Erstellen Sie ein Windows Forms-](/visualstudio/ide/step-1-create-a-windows-forms-application-project) Anwendungs [Projekt, und Gewusst wie: Fügen Sie Windows Forms](how-to-add-controls-to-windows-forms.md)Steuerelemente hinzu.

> [!NOTE]
> Die Ansicht "Nebeneinander" steht unter [!INCLUDE[WinXpFamily](../../../../includes/winxpfamily-md.md)] nur zur Verfügung, wenn die Anwendung die <xref:System.Windows.Forms.Application.EnableVisualStyles%2A?displayProperty=nameWithType>-Methode aufruft. Unter älteren Betriebssystemen hat Code in Bezug auf die Ansicht "Nebeneinander" keine Auswirkungen, und das <xref:System.Windows.Forms.ListView>-Steuerelement wird in der Ansicht "Große Symbole" angezeigt. Weitere Informationen finden Sie unter <xref:System.Windows.Forms.ListView.View%2A?displayProperty=nameWithType>.

## <a name="to-set-tile-view-in-the-designer"></a>So legen Sie die Kachel Ansicht im Designer fest

1. Wählen Sie in Visual Studio das <xref:System.Windows.Forms.ListView> Steuerelement auf dem Formular aus.

2. Wählen Sie im Fenster **Eigenschaften** die Eigenschaft <xref:System.Windows.Forms.ListView.View%2A> aus, und wählen Sie dann die **Kachel**aus.

## <a name="see-also"></a>Siehe auch

- <xref:System.Windows.Forms.ListView.TileSize%2A>
- [Übersicht über das ListView-Steuerelement](listview-control-overview-windows-forms.md)
