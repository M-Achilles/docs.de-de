---
title: Übersicht über Panel-Elemente
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
- cpp
helpviewer_keywords:
- Panel control [WPF], about Panel control
- controls [WPF], Panel
ms.assetid: f73644af-9941-4611-8754-6d4cef03fc44
ms.openlocfilehash: 5fe464f2b79fa1f7b0674c049110d32f2ad32335
ms.sourcegitcommit: 68653db98c5ea7744fd438710248935f70020dfb
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/22/2019
ms.locfileid: "69944821"
---
# <a name="panels-overview"></a>Übersicht über Panel-Elemente
<xref:System.Windows.Controls.Panel>Elemente sind Komponenten, die das Rendering von Elementen steuern – ihre Größe und Größe, ihre Position und die Anordnung ihres untergeordneten Inhalts. Bietet eine Reihe vordefinierter <xref:System.Windows.Controls.Panel> Elemente sowie die Möglichkeit, benutzerdefinierte <xref:System.Windows.Controls.Panel> Elemente zu erstellen. [!INCLUDE[TLA#tla_winclient](../../../../includes/tlasharptla-winclient-md.md)]  
  
 Dieses Thema enthält folgende Abschnitte:  
  
- [Die Panel-Klasse](#Panels_view_from_10000_feet)  
  
- [Allgemeine Member von Panel-Elementen](#Panels_declared_members)  
  
- [Abgeleitete Panel-Elemente](#Panels_derived_elements)  
  
- [Panels der Benutzeroberfläche](#Panels_main_UI_elements)  
  
- [Geschachtelte Panel-Elemente](#Panels_nested_panel_elements)  
  
- [Benutzerdefinierte Panel-Elemente](#Panels_custom_panel_elements)  
  
- [Unterstützung für Lokalisierung/Globalisierung](#Panels_global_localization)  
  
<a name="Panels_view_from_10000_feet"></a>   
## <a name="the-panel-class"></a>Die Panel-Klasse  
 <xref:System.Windows.Controls.Panel>ist die Basisklasse für alle-Elemente, die Layoutunterstützung in [!INCLUDE[TLA#tla_winclient](../../../../includes/tlasharptla-winclient-md.md)]bereitstellen. Abgeleitete <xref:System.Windows.Controls.Panel> Elemente werden verwendet, um Elemente in [!INCLUDE[TLA#tla_xaml](../../../../includes/tlasharptla-xaml-md.md)] -und-Code zu positionieren und anzuordnen.  
  
 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] enthält eine umfassende Auflistung abgeleiteter Panelimplementierungen, die komplexe Layouts zulassen. Diese abgeleiteten Klassen machen Eigenschaften und Methoden verfügbar, die die meisten [!INCLUDE[TLA#tla_ui](../../../../includes/tlasharptla-ui-md.md)]-Standardszenarios zulassen. Entwickler, die kein untergeordnetes Anstellungs Verhalten finden, das Ihren Anforderungen entspricht, können neue Layouts erstellen, <xref:System.Windows.FrameworkElement.ArrangeOverride%2A> indem <xref:System.Windows.FrameworkElement.MeasureOverride%2A> Sie die-Methode und die-Methode überschreiben. Weitere Informationen über das Verhalten benutzerdefinierter Layouts finden Sie unter [Benutzerdefinierte Panel-Elemente](#Panels_custom_panel_elements).  
  
<a name="Panels_declared_members"></a>   
## <a name="panel-common-members"></a>Allgemeine Panel-Elemente  
 Alle <xref:System.Windows.Controls.Panel> -Elemente unterstützen die von <xref:System.Windows.FrameworkElement.Margin%2A> <xref:System.Windows.FrameworkElement.LayoutTransform%2A> <xref:System.Windows.FrameworkElement.Height%2A> <xref:System.Windows.FrameworkElement.Width%2A> <xref:System.Windows.FrameworkElement>definierten Basis Größen und Positionierungs Eigenschaften, einschließlich <xref:System.Windows.FrameworkElement.HorizontalAlignment%2A>, <xref:System.Windows.FrameworkElement.VerticalAlignment%2A>,,, und. Weitere Informationen zum Positionieren von Eigenschaften, die <xref:System.Windows.FrameworkElement>durch definiert werden, finden Sie unter [Ausrichtung, Ränder und Auffüllen (Übersicht](../advanced/alignment-margins-and-padding-overview.md)).  
  
 <xref:System.Windows.Controls.Panel>macht zusätzliche Eigenschaften verfügbar, die für das Verständnis und die Verwendung von Layouts von entscheidender Bedeutung sind. Die <xref:System.Windows.Controls.Panel.Background%2A> -Eigenschaft wird verwendet, um den Bereich zwischen den Begrenzungen eines abgeleiteten Panel-Elements <xref:System.Windows.Media.Brush>mit einem auszufüllen. <xref:System.Windows.Controls.Panel.Children%2A>stellt die untergeordnete Auflistung von Elementen dar <xref:System.Windows.Controls.Panel> , aus denen die besteht. <xref:System.Windows.Controls.Panel.InternalChildren%2A>stellt den Inhalt der <xref:System.Windows.Controls.Panel.Children%2A> Auflistung zuzüglich der durch die Datenbindung generierten Elemente dar. Beide bestehen aus einer <xref:System.Windows.Controls.UIElementCollection> untergeordneten Elemente, die im über <xref:System.Windows.Controls.Panel>geordneten Element gehostet werden.  
  
 Panel macht auch eine <xref:System.Windows.Controls.Panel.ZIndex%2A?displayProperty=nameWithType> angefügte Eigenschaft verfügbar, die verwendet werden kann, um in einem <xref:System.Windows.Controls.Panel>abgeleiteten eine schichtweise zu erreichen Elemente der Auflistung eines Panels <xref:System.Windows.Controls.Panel.Children%2A> mit einem höheren <xref:System.Windows.Controls.Panel.ZIndex%2A?displayProperty=nameWithType> Wert werden vor denen mit einem niedrigeren <xref:System.Windows.Controls.Panel.ZIndex%2A?displayProperty=nameWithType> Wert angezeigt. Dies ist besonders nützlich für Bereiche wie <xref:System.Windows.Controls.Canvas> und <xref:System.Windows.Controls.Grid> , die es untergeordneten Elementen ermöglichen, denselben Koordinatenraum gemeinsam zu verwenden.  
  
 <xref:System.Windows.Controls.Panel>definiert auch die <xref:System.Windows.Controls.Panel.OnRender%2A> -Methode, die verwendet werden kann, um das Standard Darstellungs Verhalten <xref:System.Windows.Controls.Panel>eines zu überschreiben.  
  
#### <a name="attached-properties"></a>Angefügte Eigenschaften  
 Abgeleitete Panel-Elemente machen umfassenden Gebrauch von angefügten Eigenschaften. Eine angefügte Eigenschaft ist eine spezielle Form der Abhängigkeits Eigenschaft, die nicht über die Eigenschaft "Wrapper" der herkömmlichen Common Language Runtime (CLR) verfügt. Angefügte Eigenschaften haben eine besondere Syntax in [!INCLUDE[TLA#tla_xaml](../../../../includes/tlasharptla-xaml-md.md)], die in einigen der folgenden Beispiele dargestellt sind.  
  
 Ein Zweck einer angefügten Eigenschaft ist es, untergeordnete Elemente zum Speichern eindeutiger Werte einer Eigenschaft zuzulassen, die eigentlich durch ein übergeordnetes Element definiert ist. Diese Anwendung dieser Funktion besitzt untergeordnete Elemente, die das übergeordnete Element darüber informieren, wie sie in [!INCLUDE[TLA#tla_ui](../../../../includes/tlasharptla-ui-md.md)] dargestellt werden wollen, was sehr nützlich für das Anwendungslayout ist. Weitere Informationen finden Sie unter [Übersicht über angefügte Eigenschaften](../advanced/attached-properties-overview.md).  
  
<a name="Panels_derived_elements"></a>   
## <a name="derived-panel-elements"></a>Abgeleitete Panel-Elemente  
 Viele Objekte werden von <xref:System.Windows.Controls.Panel>abgeleitet, aber nicht alle sind für die Verwendung als Stammlayoutanbieter vorgesehen. Es gibt sechs definierte Panel-Klassen<xref:System.Windows.Controls.Canvas>( <xref:System.Windows.Controls.DockPanel>, <xref:System.Windows.Controls.Grid>, <xref:System.Windows.Controls.StackPanel>, <xref:System.Windows.Controls.VirtualizingStackPanel>, und <xref:System.Windows.Controls.WrapPanel>), die speziell zum Erstellen von Anwendungen [!INCLUDE[TLA2#tla_ui](../../../../includes/tla2sharptla-ui-md.md)]entwickelt wurden.  
  
 Jedes Panel-Element kapselt seine eigene besondere Funktionalität, wie in der folgenden Tabelle dargestellt.  
  
|Elementname|Benutzeroberflächen-Panel?|Beschreibung|  
|------------------|---------------|-----------------|  
|<xref:System.Windows.Controls.Canvas>|Ja|Definiert einen Bereich, in dem Sie untergeordnete Elemente explizit durch Koordinaten relativ zum <xref:System.Windows.Controls.Canvas> Bereich positionieren können.|  
|<xref:System.Windows.Controls.DockPanel>|Ja|Definiert einen Bereich, in dem Sie untergeordnete Elemente entweder horizontal oder vertikal relativ zueinander anordnen können.|  
|<xref:System.Windows.Controls.Grid>|Ja|Definiert einen flexiblen Rasterbereich mit Spalten und Zeilen. Untergeordnete Elemente eines <xref:System.Windows.Controls.Grid> können mithilfe der <xref:System.Windows.FrameworkElement.Margin%2A> -Eigenschaft exakt positioniert werden.|  
|<xref:System.Windows.Controls.StackPanel>|Ja|Ordnet untergeordnete Elemente in einer einzelnen Zeile an, die horizontal oder vertikal ausgerichtet werden kann.|  
|<xref:System.Windows.Controls.Primitives.TabPanel>|Nein|Behandelt das Layout von Registerkarten Schaltflächen in einem <xref:System.Windows.Controls.TabControl>.|  
|<xref:System.Windows.Controls.Primitives.ToolBarOverflowPanel>|Nein|Ordnet den Inhalt in <xref:System.Windows.Controls.ToolBar> einem-Steuerelement an.|  
|<xref:System.Windows.Controls.Primitives.UniformGrid>|Nein|<xref:System.Windows.Controls.Primitives.UniformGrid>wird zum Anordnen von untergeordneten Elementen in einem Raster mit allen gleichen Zellgrößen verwendet.|  
|<xref:System.Windows.Controls.VirtualizingPanel>|Nein|Stellt eine Basisklasse für Panels bereit, die ihre untergeordnete Auflistung „virtualisieren“ kann.|  
|<xref:System.Windows.Controls.VirtualizingStackPanel>|Ja|Ordnet Inhalt an und virtualisiert ihn in einer einzelnen Zeile, die horizontal oder vertikal ausgerichtet werden kann.|  
|<xref:System.Windows.Controls.WrapPanel>|Ja|<xref:System.Windows.Controls.WrapPanel>positioniert untergeordnete Elemente in sequenzieller Position von links nach rechts und unterbricht den Inhalt in die nächste Zeile am Rand des enthaltenden Felds. Die nachfolgende Reihenfolge erfolgt nacheinander von oben nach unten oder von rechts nach links, abhängig vom Wert <xref:System.Windows.Controls.WrapPanel.Orientation%2A> der-Eigenschaft.|  
  
<a name="Panels_main_UI_elements"></a>   
## <a name="user-interface-panels"></a>Panels der Benutzeroberfläche  
 In [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] sind sechs Panel-Klassen verfügbar, die für die unter [!INCLUDE[TLA2#tla_ui](../../../../includes/tla2sharptla-ui-md.md)] Stützung von <xref:System.Windows.Controls.Canvas>Szenarien optimiert sind: <xref:System.Windows.Controls.VirtualizingStackPanel>, <xref:System.Windows.Controls.DockPanel>, <xref:System.Windows.Controls.WrapPanel> <xref:System.Windows.Controls.Grid>, <xref:System.Windows.Controls.StackPanel>, und. Diese Panel-Elemente sind einfach zu verwenden und vielseitig und erweiterbar genug für die meisten Anwendungen.  
  
 Jedes abgeleitete <xref:System.Windows.Controls.Panel> Element behandelt Größenbeschränkungen anders. Wenn Sie verstehen <xref:System.Windows.Controls.Panel> , wie Einschränkungen in der horizontalen oder vertikalen Richtung behandelt werden, kann das Layout besser vorhersagbar werden.  
  
|**Panelname**|**X-Dimension**|**Y-Dimension**|  
|--------------------|----------------------|----------------------|  
|<xref:System.Windows.Controls.Canvas>|Eingeschränkt auf Inhalt|Eingeschränkt auf Inhalt|  
|<xref:System.Windows.Controls.DockPanel>|Beschränkt|Beschränkt|  
|<xref:System.Windows.Controls.StackPanel>(Vertikale Ausrichtung)|Beschränkt|Eingeschränkt auf Inhalt|  
|<xref:System.Windows.Controls.StackPanel>(Horizontale Ausrichtung)|Eingeschränkt auf Inhalt|Beschränkt|  
|<xref:System.Windows.Controls.Grid>|Beschränkt|Eingeschränkt, außer in Fällen, <xref:System.Windows.GridUnitType.Auto> in denen auf Zeilen und Spalten anwenden|  
|<xref:System.Windows.Controls.WrapPanel>|Eingeschränkt auf Inhalt|Eingeschränkt auf Inhalt|  
  
 Eine ausführlichere Beschreibung und Verwendungsbeispiele für jedes dieser Elemente finden Sie weiter unten.  
  
<a name="Panels_overview_Canvas_subsection"></a>   
### <a name="canvas"></a>Canvas  
 Das <xref:System.Windows.Controls.Canvas> -Element ermöglicht die Positionierung von Inhalten gemäß absoluten *x-* und *y-* Koordinaten. Elemente können in einer eindeutigen Position gezeichnet werden; alternativ bestimmt die Reihenfolge, in der Sie im Markup erscheinen, die Reihenfolge, in der die Elemente gezeichnet werden, wenn Elemente die gleichen Koordinaten verwenden.  
  
 <xref:System.Windows.Controls.Canvas>bietet die flexibelste Layoutunterstützung <xref:System.Windows.Controls.Panel>für alle. Die Eigenschaften Height und Width werden verwendet, um den Bereich der Canvas zu definieren, und den Elementen in werden absolute Koordinaten relativ zum Bereich des über <xref:System.Windows.Controls.Canvas>geordneten Elements zugewiesen. Vier angefügte Eigenschaften <xref:System.Windows.Controls.Canvas.Left%2A?displayProperty=nameWithType>, <xref:System.Windows.Controls.Canvas.Top%2A?displayProperty=nameWithType> <xref:System.Windows.Controls.Canvas.Right%2A?displayProperty=nameWithType> , und <xref:System.Windows.Controls.Canvas.Bottom%2A?displayProperty=nameWithType>, ermöglichen eine genaue Steuerung der Objekt Platzierung innerhalb <xref:System.Windows.Controls.Canvas>einer, sodass der Entwickler Elemente exakt auf dem Bildschirm positionieren und anordnen kann.  
  
#### <a name="cliptobounds-within-a-canvas"></a>ClipToBounds innerhalb eines Canvas  
 <xref:System.Windows.Controls.Canvas>kann untergeordnete Elemente an beliebiger Position auf dem Bildschirm positionieren, auch bei Koordinaten, die sich außerhalb <xref:System.Windows.FrameworkElement.Height%2A> des <xref:System.Windows.FrameworkElement.Width%2A>eigenen definierten und befinden. <xref:System.Windows.Controls.Canvas> Außerdem wird nicht von der Größe der untergeordneten Elemente beeinflusst. Folglich ist es möglich, dass ein untergeordnetes Element andere Elemente außerhalb des umgebenden Rechtecks des übergeordneten <xref:System.Windows.Controls.Canvas>Elements überschreibt. Das Standardverhalten von <xref:System.Windows.Controls.Canvas> besteht darin, dass untergeordnete Elemente außerhalb der Grenzen des übergeordneten <xref:System.Windows.Controls.Canvas>Elements gezeichnet werden können. Wenn dieses Verhalten nicht erwünscht ist, <xref:System.Windows.UIElement.ClipToBounds%2A> kann die-Eigenschaft auf `true`festgelegt werden. Dies bewirkt <xref:System.Windows.Controls.Canvas> , dass ein Clip an eine eigene Größe durchgesetzt wird. <xref:System.Windows.Controls.Canvas>ist das einzige Layoutelement, das es ermöglicht, dass untergeordnete Elemente außerhalb ihrer Grenzen gezeichnet werden.  
  
 Diese Verhalten wird grafisch im [Width Properties Comparison Sample (Beispiel des Vergleich der Width-Eigenschaften)](https://go.microsoft.com/fwlink/?LinkID=160050) dargestellt.  
  
#### <a name="defining-and-using-a-canvas"></a>Definieren und Verwenden eines Canvas  
 Eine <xref:System.Windows.Controls.Canvas> kann einfach mithilfe [!INCLUDE[TLA#tla_xaml](../../../../includes/tlasharptla-xaml-md.md)] von-oder-Code instanziiert werden. Im folgenden Beispiel wird veranschaulicht, wie <xref:System.Windows.Controls.Canvas> verwendet wird, um Inhalt absolut zu positionieren. Dieser Code erzeugt drei 100-Pixel-Quadrate. Das erste Quadrat ist rot, und die obere linke Position (*x, y*) ist als (0, 0) festgelegt. Das zweite Quadrat ist grün, und die obere linke Position ist (100, 100), direkt unterhalb und rechts vom ersten Quadrat. Das dritte Quadrat ist blau, und die obere linke Position ist (50, 50), daher umfasst es den unteren rechten Quadranten des ersten Quadrats und den oberen linken Quadranten des zweiten. Da das dritte Quadrat zuletzt angeordnet wird, erscheint es als obenliegend – das bedeutet, dass die überlappenden Teile die Farbe des dritten Quadrats annehmen.  
  
 [!code-csharp[CanvasOvwSample#1](~/samples/snippets/csharp/VS_Snippets_Wpf/CanvasOvwSample/CSharp/Canvas_Ovw_Sample.cs#1)]
 [!code-vb[CanvasOvwSample#1](~/samples/snippets/visualbasic/VS_Snippets_Wpf/CanvasOvwSample/VisualBasic/canvas_vb.vb#1)]
 [!code-xaml[CanvasOvwSample#1](~/samples/snippets/xaml/VS_Snippets_Wpf/CanvasOvwSample/XAML/default.xaml#1)]  
  
 Die kompilierte Anwendung gibt ein neues [!INCLUDE[TLA2#tla_ui](../../../../includes/tla2sharptla-ui-md.md)] aus, das folgendermaßen aussieht.  
  
 ![Ein typisches Canvas-Element. ](./media/panel-intro-canvas.PNG "panel_intro_canvas")  
  
<a name="Panels_overview_DockPanel_subsection"></a>   
### <a name="dockpanel"></a>DockPanel  
 Das <xref:System.Windows.Controls.DockPanel> -Element verwendet <xref:System.Windows.Controls.DockPanel.Dock%2A?displayProperty=nameWithType> die angefügte-Eigenschaft, die in untergeordneten Inhalts Elementen festgelegt ist, um Inhalt an den Rändern eines Containers zu positionieren. Wenn <xref:System.Windows.Controls.DockPanel.Dock%2A?displayProperty=nameWithType> auf <xref:System.Windows.Controls.Dock.Top> oder<xref:System.Windows.Controls.Dock.Bottom>festgelegt ist, positioniert es untergeordnete Elemente oberhalb oder unter einander. Wenn <xref:System.Windows.Controls.DockPanel.Dock%2A?displayProperty=nameWithType> auf <xref:System.Windows.Controls.Dock.Left> oder<xref:System.Windows.Controls.Dock.Right>festgelegt ist, positioniert es untergeordnete Elemente links oder rechts voneinander. Die <xref:System.Windows.Controls.DockPanel.LastChildFill%2A> -Eigenschaft bestimmt die Position des letzten Elements, das als <xref:System.Windows.Controls.DockPanel>untergeordnetes Element hinzugefügt wurde.  
  
 Sie können verwenden <xref:System.Windows.Controls.DockPanel> , um eine Gruppe verwandter Steuerelemente wie z. b. eine Reihe von Schaltflächen zu positionieren. Alternativ können Sie damit auch ein "schwenken" [!INCLUDE[TLA2#tla_ui](../../../../includes/tla2sharptla-ui-md.md)]erstellen, ähnlich dem, das in Microsoft Outlook gefunden wurde.  
  
#### <a name="sizing-to-content"></a>Anpassen der Größe an Inhalt  
 Wenn seine <xref:System.Windows.FrameworkElement.Height%2A> - <xref:System.Windows.FrameworkElement.Width%2A> Eigenschaft und die-Eigenschaft <xref:System.Windows.Controls.DockPanel> nicht angegeben sind, werden die Größen für den Inhalt der Die Größe kann sich erhöhen oder verringern, um die Größe der untergeordneten Elemente aufnehmen zu können. Wenn diese Eigenschaften jedoch angegeben werden und kein Platz mehr für das nächste angegebene untergeordnete Element vorhanden ist, <xref:System.Windows.Controls.DockPanel> wird dieses untergeordnete Element oder nachfolgende untergeordnete Elemente von nicht angezeigt, und nachfolgende untergeordnete Elemente werden nicht gemessen.  
  
#### <a name="lastchildfill"></a>LastChildFill  
 Standardmäßig wird der verbleibende, nicht <xref:System.Windows.Controls.DockPanel> zugeordnete Speicherplatz durch das letzte untergeordnete Element eines-Elements "ausgefüllt". Wenn dieses Verhalten nicht erwünscht ist, legen Sie <xref:System.Windows.Controls.DockPanel.LastChildFill%2A> die- `false`Eigenschaft auf fest.  
  
#### <a name="defining-and-using-a-dockpanel"></a>Definieren und Verwenden von DockPanel  
 Im folgenden Beispiel wird veranschaulicht, wie Sie den Speicher <xref:System.Windows.Controls.DockPanel>mithilfe eines partitionieren. Fünf <xref:System.Windows.Controls.Border> Elemente werden als untergeordnete Elemente eines über <xref:System.Windows.Controls.DockPanel>geordneten Elements hinzugefügt. Jede verwendet eine andere Positionierungs Eigenschaft eines <xref:System.Windows.Controls.DockPanel> zum Partitionieren von Speicherplatz. Das letzte Element „füllt“ den verbleibenden, nicht zugeordneten Platz.  
  
 [!code-cpp[DockPanelOvwSample#1](~/samples/snippets/cpp/VS_Snippets_Wpf/DockPanelOvwSample/CPP/DockPanel_Ovw_Sample.cpp#1)]
 [!code-csharp[DockPanelOvwSample#1](~/samples/snippets/csharp/VS_Snippets_Wpf/DockPanelOvwSample/CSharp/DockPanel_Ovw_Sample.cs#1)]
 [!code-vb[DockPanelOvwSample#1](~/samples/snippets/visualbasic/VS_Snippets_Wpf/DockPanelOvwSample/VisualBasic/dockpanel_vb.vb#1)]
 [!code-xaml[DockPanelOvwSample#1](~/samples/snippets/xaml/VS_Snippets_Wpf/DockPanelOvwSample/XAML/default.xaml#1)]  
  
 Die kompilierte Anwendung gibt ein neues [!INCLUDE[TLA2#tla_ui](../../../../includes/tla2sharptla-ui-md.md)] aus, das folgendermaßen aussieht.  
  
 ![Ein typisches DockPanel-Szenario.](./media/panel-intro-dockpanel.PNG "Panel_intro_dockpanel")  
  
<a name="Panels_overview_Grid_subsection"></a>   
### <a name="grid"></a>Raster  
 Das <xref:System.Windows.Controls.Grid> -Element führt die Funktionalität eines absoluten Positions-und tabellarischen Daten Steuer Elements zusammen. Mit <xref:System.Windows.Controls.Grid> einem können Sie Elemente problemlos positionieren und formatieren. <xref:System.Windows.Controls.Grid>ermöglicht das Definieren von flexiblen Zeilen-und Spalten Gruppierungen und bietet sogar einen Mechanismus zum Freigeben von Größen Informationen zwischen <xref:System.Windows.Controls.Grid> mehreren Elementen.  
  
#### <a name="how-is-grid-different-from-table"></a>Wie unterscheidet sich Grid von Table?  
 <xref:System.Windows.Documents.Table>und <xref:System.Windows.Controls.Grid> verfügen über einige allgemeine Funktionen, aber beide sind für unterschiedliche Szenarien am besten geeignet. Eine <xref:System.Windows.Documents.Table> ist für die Verwendung innerhalb von fortlaufendem Inhalt vorgesehen (Weitere Informationen zu fortlaufendem Inhalt finden Sie unter [Übersicht über Fluss Dokumente](../advanced/flow-document-overview.md) ). Raster eignen sich am besten für den Einsatz in Formularen (also eigentlich überall dort, wo es keinen fortlaufenden Inhalt gibt). In einer <xref:System.Windows.Documents.FlowDocument> <xref:System.Windows.Documents.Table> unterstützt <xref:System.Windows.Controls.Grid> das Verhalten von fortlaufenden Inhalten wie Paginierung, Spalten Umfluss und Inhalts Auswahl, während dies nicht der gibt. Auf der anderen Seite wird am besten außerhalb von a <xref:System.Windows.Documents.FlowDocument> <xref:System.Windows.Controls.Grid> verwendet, <xref:System.Windows.Documents.Table> z. a. durch Hinzufügen von Elementen auf der Grundlage einer Zeilen-und Spalten Indizierung. <xref:System.Windows.Controls.Grid> Das <xref:System.Windows.Controls.Grid> -Element ermöglicht das Schichten von untergeordneten Inhalten, sodass mehr als ein Element in einer einzelnen "Zelle" vorhanden sein kann. <xref:System.Windows.Documents.Table>unterstützt keine Schichten. Untergeordnete Elemente eines <xref:System.Windows.Controls.Grid> können in Bezug auf den Bereich ihrer "Cell"-Begrenzungen absolut positioniert werden. <xref:System.Windows.Documents.Table>Diese Funktion wird von nicht unterstützt. Schließlich ist ein <xref:System.Windows.Controls.Grid> heller gewichtet als ein <xref:System.Windows.Documents.Table>.  
  
#### <a name="sizing-behavior-of-columns-and-rows"></a>Größenanpassungsverhalten von Spalten und Zeilen  
 Spalten und Zeilen, die innerhalb <xref:System.Windows.Controls.Grid> eines definiert sind, <xref:System.Windows.GridUnitType.Star> können die Größe der Größe nutzen, um den verbleibenden Platz proportional zu verteilen. Wenn <xref:System.Windows.GridUnitType.Star> als Höhe oder Breite einer Zeile oder Spalte ausgewählt ist, erhält diese Spalte bzw. Zeile einen gewichteten Anteil des verbleibenden verfügbaren Speicherplatzes. Dies steht im Gegensatz zu <xref:System.Windows.GridUnitType.Auto>, wodurch der Speicherplatz gleichmäßig basierend auf der Größe des Inhalts in einer Spalte oder Zeile verteilt wird. Dieser Wert wird als `*` oder `2*` ausgedrückt, wenn [!INCLUDE[TLA#tla_xaml](../../../../includes/tlasharptla-xaml-md.md)] verwendet wird. Im ersten Fall würde die Zeile oder Spalte den verfügbaren Platz einmal erhalten, im zweiten Fall zweimal, usw. Durch die Kombination dieser Technik zum proportionalen Verteilen von <xref:System.Windows.FrameworkElement.HorizontalAlignment%2A> Speicher <xref:System.Windows.FrameworkElement.VerticalAlignment%2A> Platz mit `Stretch` einem-Wert und einem-Wert ist es möglich, den Layoutbereich anhand des Prozentsatzes des Bildschirm Raums <xref:System.Windows.Controls.Grid>ist das einzige Layoutpanel, mit dem Speicherplatz auf diese Weise verteilt werden kann.  
  
#### <a name="defining-and-using-a-grid"></a>Definieren und Verwenden eines Rasters  
 Im folgenden Beispiel wird veranschaulicht, wie Sie [!INCLUDE[TLA2#tla_ui](../../../../includes/tla2sharptla-ui-md.md)] einen ähnlich dem Erstellen, der im Dialogfeld "ausführen" im Windows-Startmenü verfügbar ist.  
  
 [!code-csharp[GridRunDialog#1](~/samples/snippets/csharp/VS_Snippets_Wpf/GridRunDialog/CSharp/window1.xaml.cs#1)]
 [!code-vb[GridRunDialog#1](~/samples/snippets/visualbasic/VS_Snippets_Wpf/GridRunDialog/VisualBasic/grid_vb.vb#1)]  
  
 Die kompilierte Anwendung gibt ein neues [!INCLUDE[TLA2#tla_ui](../../../../includes/tla2sharptla-ui-md.md)] aus, das folgendermaßen aussieht.  
  
 ![Ein typisches Grid-Element.](./media/avalon-run-dialog.PNG "Avalon_run_dialog")  
  
<a name="Panels_overview_StackPanel_subsection"></a>   
### <a name="stackpanel"></a>StackPanel  
 Mit <xref:System.Windows.Controls.StackPanel> einem können Sie Elemente in einer zugewiesenen Richtung "stapeln". Die Standardrichtung eines Stapels ist vertikal. Die <xref:System.Windows.Controls.StackPanel.Orientation%2A> -Eigenschaft kann zum Steuern des Inhalts Flusses verwendet werden.  
  
#### <a name="stackpanel-vs-dockpanel"></a>StackPanel vs. DockPanel  
 Obwohl <xref:System.Windows.Controls.DockPanel> auch untergeordnete <xref:System.Windows.Controls.DockPanel> Elemente "stapeln" können und <xref:System.Windows.Controls.StackPanel> in einigen Verwendungs Szenarien keine analogen Ergebnisse liefern. Beispielsweise kann sich die Reihenfolge der untergeordneten Elemente auf ihre Größe <xref:System.Windows.Controls.DockPanel> in einer, aber <xref:System.Windows.Controls.StackPanel>nicht in einem auswirken. Dies liegt daran <xref:System.Windows.Controls.StackPanel> <xref:System.Double.PositiveInfinity>, dass Measures in der Richtung Stapeln, während <xref:System.Windows.Controls.DockPanel> nur die verfügbare Größe misst.  
  
 Im folgenden Beispiel wird dieser Hauptunterschied veranschaulicht.  
  
 [!code-cpp[StackPanelOvw4#1](~/samples/snippets/cpp/VS_Snippets_Wpf/StackPanelOvw4/CPP/StackPanel_Ovw_Sample4.cpp#1)]
 [!code-csharp[StackPanelOvw4#1](~/samples/snippets/csharp/VS_Snippets_Wpf/StackPanelOvw4/CSharp/StackPanel_Ovw_Sample4.cs#1)]
 [!code-vb[StackPanelOvw4#1](~/samples/snippets/visualbasic/VS_Snippets_Wpf/StackPanelOvw4/VisualBasic/StackPanelSamp.vb#1)]
 [!code-xaml[StackPanelOvw4#1](~/samples/snippets/xaml/VS_Snippets_Wpf/StackPanelOvw4/XAML/default.xaml#1)]  
  
 Der Unterschied im Renderingverhalten wird auf diesem Bild abgebildet.  
  
 ![Verschaffen StackPanel vs. DockPanel Screenshot](./media/layout-smiley-stackpanel.PNG "Layout_smiley_stackpanel")  
  
#### <a name="defining-and-using-a-stackpanel"></a>Definieren und Verwenden eines StackPanels  
 Im folgenden Beispiel wird veranschaulicht, wie mit <xref:System.Windows.Controls.StackPanel> einem eine Reihe von vertikal positionierten Schaltflächen erstellt wird. Legen Sie für die horizontale Positionierung <xref:System.Windows.Controls.StackPanel.Orientation%2A> die- <xref:System.Windows.Controls.Orientation.Horizontal>Eigenschaft auf fest.  
  
 [!code-csharp[StackPanel_ovw2#1](~/samples/snippets/csharp/VS_Snippets_Wpf/StackPanel_ovw2/CSharp/StackPanel_Ovw_Sample2.cs#1)]
 [!code-vb[StackPanel_ovw2#1](~/samples/snippets/visualbasic/VS_Snippets_Wpf/StackPanel_ovw2/VisualBasic/StackPanelOvw.vb#1)]  
  
 Die kompilierte Anwendung gibt ein neues [!INCLUDE[TLA2#tla_ui](../../../../includes/tla2sharptla-ui-md.md)] aus, das folgendermaßen aussieht.  
  
 ![Ein typisches StackPanel-Element.](./media/panel-intro-stackpanel.PNG "panel_intro_stackpanel")  
  
<a name="Panels_overview_VirtualizingStackPanel_subsection"></a>   
#### <a name="virtualizingstackpanel"></a>VirtualizingStackPanel  
 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)]bietet auch eine Variation des <xref:System.Windows.Controls.StackPanel> Elements, das automatisch Daten gebundenen untergeordneten Inhalt "virtualisiert". In diesem Zusammenhang bezieht sich das Wort „virtualisieren“ auf eine Technik, mit der eine Teilmenge von Elementen aus einer größeren Menge von Datenelementen generiert wird, je nachdem, welche Elemente auf dem Bildschirm sichtbar sind. Es ist sowohl für den Arbeitsspeicher als auch für den Prozessor sehr aufwändig, eine große Menge an UI-Elementen zu generieren, wenn sich möglicherweise nur sehr wenige Elemente zu einer angegebenen Zeit auf einem Bildschirm befinden. <xref:System.Windows.Controls.VirtualizingStackPanel>( <xref:System.Windows.Controls.VirtualizingPanel>durch die von bereitgestellte Funktionalität) berechnet sichtbare Elemente und funktioniert mit dem <xref:System.Windows.Controls.ItemsControl> <xref:System.Windows.Controls.ItemContainerGenerator> <xref:System.Windows.Controls.ListBox> von einem (z <xref:System.Windows.Controls.ListView>. b. oder), um nur Elemente für sichtbare Elemente zu erstellen.  
  
 Das <xref:System.Windows.Controls.VirtualizingStackPanel> -Element wird automatisch als Element Host für Steuerelemente wie das <xref:System.Windows.Controls.ListBox>-Element festgelegt. Wenn eine Daten gebundene Auflistung gehostet wird, wird der Inhalt automatisch virtualisiert, solange sich der Inhalt innerhalb der Grenzen eines <xref:System.Windows.Controls.ScrollViewer>befindet. Dies verbessert erheblich die Leistung beim Hosten vieler untergeordneter Elemente.  
  
 Das folgende Markup zeigt, wie Sie einen <xref:System.Windows.Controls.VirtualizingStackPanel> als Element Host verwenden. Die <xref:System.Windows.Controls.VirtualizingStackPanel.IsVirtualizingProperty?displayProperty=nameWithType> angefügte-Eigenschaft muss auf `true` (Standard) festgelegt werden, damit die Virtualisierung stattfindet.  
  
 [!code-xaml[VirtualizingStackPanel_Intro#1](~/samples/snippets/csharp/VS_Snippets_Wpf/VirtualizingStackPanel_Intro/CS/default.xaml#1)]  
  
<a name="Panels_overview_WrapPanel"></a>   
### <a name="wrappanel"></a>WrapPanel  
 <xref:System.Windows.Controls.WrapPanel>wird verwendet, um untergeordnete Elemente in sequenzieller Position von links nach rechts zu positionieren, wobei der Inhalt in die nächste Zeile geht, wenn er den Rand seines übergeordneten Containers erreicht. Inhalt kann horizontal oder vertikal ausgerichtet werden. <xref:System.Windows.Controls.WrapPanel>ist für einfache Fluss [!INCLUDE[TLA#tla_ui](../../../../includes/tlasharptla-ui-md.md)] Szenarios nützlich. Es kann auch verwendet werden, um eine einheitliche Größe auf alle untergeordneten Elemente anzuwenden.  
  
 Im folgenden Beispiel wird veranschaulicht, wie ein <xref:System.Windows.Controls.WrapPanel> zum Anzeigen <xref:System.Windows.Controls.Button> von Steuerelementen erstellt wird, die beim Erreichen des edgeknotens des Containers eingebunden werden.  
  
 [!code-cpp[WrapPanel_Intro#1](~/samples/snippets/cpp/VS_Snippets_Wpf/WrapPanel_Intro/CPP/WrapPanel_Code.cpp#1)]
 [!code-csharp[WrapPanel_Intro#1](~/samples/snippets/csharp/VS_Snippets_Wpf/WrapPanel_Intro/CSharp/WrapPanel_Code.cs#1)]
 [!code-vb[WrapPanel_Intro#1](~/samples/snippets/visualbasic/VS_Snippets_Wpf/WrapPanel_Intro/VisualBasic/WrapPanel_vb.vb#1)]
 [!code-xaml[WrapPanel_Intro#1](~/samples/snippets/xaml/VS_Snippets_Wpf/WrapPanel_Intro/XAML/default.xaml#1)]  
  
 Die kompilierte Anwendung gibt ein neues [!INCLUDE[TLA2#tla_ui](../../../../includes/tla2sharptla-ui-md.md)] aus, das folgendermaßen aussieht.  
  
 ![Ein typisches WrapPanel-Element.](./media/wrappanel-element.PNG "WrapPanel_Element")  
  
<a name="Panels_nested_panel_elements"></a>   
## <a name="nested-panel-elements"></a>Geschachtelte Panel-Elemente  
 <xref:System.Windows.Controls.Panel>Elemente können ineinander geschachtelt werden, um komplexe Layouts zu schaffen. Dies kann sich als sehr nützlich erweisen <xref:System.Windows.Controls.Panel> [!INCLUDE[TLA2#tla_ui](../../../../includes/tla2sharptla-ui-md.md)], wenn eine für einen Teil von ideal ist, aber möglicherweise nicht den Anforderungen eines anderen Teils von [!INCLUDE[TLA2#tla_ui](../../../../includes/tla2sharptla-ui-md.md)]entspricht.  
  
 Es gibt praktisch keine Begrenzung hinsichtlich des Grads der Schachtelung, die Ihre Anwendung unterstützen kann; es wird jedoch im Allgemeinen empfohlen, Ihre Anwendung nur diese Bereichen verwenden zu lassen, die für das gewünschte Layout tatsächlich erforderlich sind. In vielen Fällen kann ein <xref:System.Windows.Controls.Grid> -Element anstelle von Netz Modulen verwendet werden, da es als Layoutcontainer flexibel ist. Dies kann die Leistung der Anwendung erhöhen, da sich keine unnötigen Elemente in Ihrer Struktur befinden.  
  
 Im folgenden Beispiel wird veranschaulicht, wie ein [!INCLUDE[TLA2#tla_ui](../../../../includes/tla2sharptla-ui-md.md)] erstellt wird, das die Vorteile <xref:System.Windows.Controls.Panel> von in der Struktur eingefügten Elemente nutzt, um ein bestimmtes Layout zu erzielen. In diesem speziellen Fall wird ein <xref:System.Windows.Controls.DockPanel> -Element verwendet, um [!INCLUDE[TLA2#tla_ui](../../../../includes/tla2sharptla-ui-md.md)] die <xref:System.Windows.Controls.StackPanel> Struktur und geschachtelte Elemente <xref:System.Windows.Controls.Grid>() bereitzustellen <xref:System.Windows.Controls.Canvas> , und eine wird verwendet, um untergeordnete Elemente <xref:System.Windows.Controls.DockPanel>genau innerhalb des übergeordneten Elements zu positionieren.  
  
 [!code-csharp[Nested_Panels#1](~/samples/snippets/csharp/VS_Snippets_Wpf/Nested_Panels/CSharp/nestedpanels.cs#1)]
 [!code-vb[Nested_Panels#1](~/samples/snippets/visualbasic/VS_Snippets_Wpf/Nested_Panels/VisualBasic/nestedpanels.vb#1)]  
  
 Die kompilierte Anwendung gibt ein neues [!INCLUDE[TLA2#tla_ui](../../../../includes/tla2sharptla-ui-md.md)] aus, das folgendermaßen aussieht.  
  
 ![Eine UI, die verschachtelte Bereiche nutzt.](./media/nested-panels.PNG "nested_panels")  
  
<a name="Panels_custom_panel_elements"></a>   
## <a name="custom-panel-elements"></a>Benutzerdefinierte Panel-Elemente  
 Während [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] ein Array flexibler Layoutsteuerelemente bietet, können benutzerdefinierte Layoutverhalten auch durch über <xref:System.Windows.FrameworkElement.ArrangeOverride%2A> schreiben <xref:System.Windows.FrameworkElement.MeasureOverride%2A> der-Methode und der-Methode erreicht werden. Sie können eine benutzerdefinierte Größe und Position erzielen, indem Sie innerhalb der Methode zum Außerkraftsetzen neues Postionierungsverhalten definieren.  
  
 Entsprechend können benutzerdefinierte Layoutverhalten, die auf abgeleiteten <xref:System.Windows.Controls.Canvas> Klassen <xref:System.Windows.Controls.Grid>basieren (z. b. oder <xref:System.Windows.FrameworkElement.ArrangeOverride%2A> ) <xref:System.Windows.FrameworkElement.MeasureOverride%2A> , durch Überschreiben der-und-Methoden definiert werden  
  
 Das folgende Markup zeigt, wie ein benutzerdefiniertes <xref:System.Windows.Controls.Panel> Element erstellt wird. Dieses neue <xref:System.Windows.Controls.Panel>, `PlotPanel`als definierte definiert, unterstützt die Positionierung von untergeordneten Elementen durch die Verwendung von hart codierten *x-* und *y-* Koordinaten. In diesem Beispiel wird ein <xref:System.Windows.Shapes.Rectangle> -Element (nicht angezeigt) am plotpunkt 50 (*x*) und 50 (*y*) positioniert.  
  
 [!code-cpp[PlotPanel#1](~/samples/snippets/cpp/VS_Snippets_Wpf/PlotPanel/CPP/PlotPanel.cpp#1)]
 [!code-csharp[PlotPanel#1](~/samples/snippets/csharp/VS_Snippets_Wpf/PlotPanel/CSharp/PlotPanel.cs#1)]
 [!code-vb[PlotPanel#1](~/samples/snippets/visualbasic/VS_Snippets_Wpf/PlotPanel/VisualBasic/PlotPanel.vb#1)]  
  
 Eine komplexere Implementierung von benutzerdefinierten Panel finden Sie unter [Create a Custom Content-Wrapping Panel Sample (Beispiel für das Erstellen eines Panels zum Umschließen von Inhalt)](https://go.microsoft.com/fwlink/?LinkID=159979).  
  
<a name="Panels_global_localization"></a>   
## <a name="localizationglobalization-support"></a>Unterstützung der Lokalisierung/Globalisierung  
 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] unterstützt eine Reihe von Funktionen, die Ihnen beim Erstellen einer lokalisierbaren [!INCLUDE[TLA2#tla_ui](../../../../includes/tla2sharptla-ui-md.md)] helfen.  
  
 Alle Panel-Elemente unterstützen die <xref:System.Windows.FrameworkElement.FlowDirection%2A> -Eigenschaft, die zum dynamischen erneuten fort leiten von Inhalten auf der Grundlage der Gebiets Schema-oder Spracheinstellungen eines Benutzers verwendet werden kann. Weitere Informationen finden Sie unter <xref:System.Windows.FrameworkElement.FlowDirection%2A>.  
  
 Die <xref:System.Windows.Window.SizeToContent%2A> -Eigenschaft stellt einen Mechanismus bereit, mit dem Anwendungsentwickler die Anforderungen von [!INCLUDE[TLA2#tla_ui](../../../../includes/tla2sharptla-ui-md.md)]lokalisiertem einschätzen können. Mit dem <xref:System.Windows.SizeToContent.WidthAndHeight> Wert dieser Eigenschaft wird ein übergeordnetes <xref:System.Windows.Window> Element immer dynamisch an den Inhalt angepasst und ist nicht durch künstliche Höhen-oder breiten Einschränkungen eingeschränkt.  
  
 <xref:System.Windows.Controls.DockPanel>, <xref:System.Windows.Controls.Grid> [!INCLUDE[TLA2#tla_ui](../../../../includes/tla2sharptla-ui-md.md)]und <xref:System.Windows.Controls.StackPanel> sind gut für lokalisierbare Optionen geeignet. <xref:System.Windows.Controls.Canvas>ist jedoch nicht gut geeignet, da Inhalte absolut positioniert werden, sodass die Lokalisierung schwierig ist.  
  
 Weitere Informationen zum Erstellen von [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)]-Anwendungen mit lokalisierbaren [!INCLUDE[TLA#tla_ui#plural](../../../../includes/tlasharptla-uisharpplural-md.md)]s finden Sie unter [Übersicht über die Verwendung eines automatischen Layouts](../advanced/use-automatic-layout-overview.md).  
  
## <a name="see-also"></a>Siehe auch

- [Exemplarische Vorgehensweise: Walkthrough: My first WPF desktop application (Exemplarische Vorgehensweise: Meine erste WPF-Desktopanwendung)](../getting-started/walkthrough-my-first-wpf-desktop-application.md)
- [Beispiel für einen WPF-Layoutkatalog](https://go.microsoft.com/fwlink/?LinkID=160054)
- [Layout](../advanced/layout.md)
- [Beispiel für WPF-Steuerelementsammlungen](https://go.microsoft.com/fwlink/?LinkID=160053)
- [Übersicht über Alignment, Margin und Padding](../advanced/alignment-margins-and-padding-overview.md)
- [Erstellen eines benutzerdefinierten Content-Wrapping Panel-Beispiels](https://go.microsoft.com/fwlink/?LinkID=159979)
- [Übersicht über angefügte Eigenschaften](../advanced/attached-properties-overview.md)
- [Übersicht über die Verwendung eines automatischen Layouts](../advanced/use-automatic-layout-overview.md)
- [Layout und Entwurf](../advanced/optimizing-performance-layout-and-design.md)
