---
title: 'Aufgabe 2: Hosten des Workflow-Designers'
ms.date: 03/30/2017
ms.assetid: 0a29b138-270d-4846-b78e-2b875e34e501
ms.openlocfilehash: 15657ad79632812d3802e4da22b9ef297d08f932
ms.sourcegitcommit: dfd612ba454ce775a766bcc6fe93bc1d43dfda47
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 10/09/2019
ms.locfileid: "72180259"
---
# <a name="task-2-host-the-workflow-designer"></a>Aufgabe 2: Hosten des Workflow-Designers

In diesem Thema wird das Verfahren zum Hosting einer Instanz des [!INCLUDE[wfd1](../../../includes/wfd1-md.md)] in einer Windows Presentation Foundation (WPF)-Anwendung beschrieben.

Die Prozedur konfiguriert das **Raster** Steuerelement, das den Designer enthält, erstellt Programm gesteuert eine Instanz des <xref:System.Activities.Presentation.WorkflowDesigner>, das eine standardmäßige <xref:System.Activities.Statements.Sequence>-Aktivität enthält, registriert die Designer Metadaten, um Designer Unterstützung für alle integrierten Aktivitäten und hosten die [!INCLUDE[wfd2](../../../includes/wfd2-md.md)] in der WPF-Anwendung.

## <a name="to-host-the-workflow-designer"></a>So hosten Sie den Workflow-Designer

1. Öffnen Sie das HostingApplication-Projekt, das Sie in [task 1 erstellt haben: Erstellen Sie eine neue Windows Presentation Foundation Anwendung @ no__t-0.

2. Passen Sie die Fenstergröße an, um die Verwendung des [!INCLUDE[wfd2](../../../includes/wfd2-md.md)] einfacher zu machen. Wählen Sie hierzu im Designer **MainWindow** , drücken Sie F4, um das **Eigenschaften** Fenster anzuzeigen, und legen Sie im Abschnitt **Layout** die **Breite** auf den Wert 600 und die **Höhe** auf 350 fest.

3. Legen Sie den Raster Namen fest, indem Sie im Designer den **Raster** Bereich auswählen (Klicken Sie auf das Feld im **MainWindow**), und legen Sie die **Name** -Eigenschaft oben im **Eigenschaften** Fenster auf "grid1" fest.

4. Klicken Sie im **Eigenschaften** Fenster auf die Auslassungs Punkte ( **...** ) neben der `ColumnDefinitions`-Eigenschaft, um das Dialogfeld Auflistungs- **Editor** zu öffnen.

5. Klicken Sie im Dialogfeld Auflistungs- **Editor** drei Mal auf die Schaltfläche **Hinzufügen** , um drei Spalten in das Layout einzufügen. Die erste Spalte enthält die **Toolbox**, in der zweiten Spalte wird die [!INCLUDE[wfd2](../../../includes/wfd2-md.md)] gehostet, und die dritte Spalte wird für die Eigenschaften Analyse verwendet.

6. Legen Sie die `Width`-Eigenschaft der mittleren Spalte auf den Wert "4 *" fest.

7. Klicken Sie auf **OK** , um die Änderungen zu speichern. Der folgenden XAML-Code wird der Datei " *MainWindow. XAML* " hinzugefügt:

    ```xaml
    <Grid Name="grid1">
        <Grid.ColumnDefinitions>
            <ColumnDefinition />
            <ColumnDefinition Width="4*" />
            <ColumnDefinition />
        </Grid.ColumnDefinitions>
    </Grid>
    ```

8. Klicken Sie in **Projektmappen-Explorer**mit der rechten Maustaste auf *MainWindow. XAML* , und wählen Sie **Code anzeigen**aus. Ändern Sie den Code, indem Sie folgende Schritte ausführen:

    1. Fügen Sie die folgenden Namespaces hinzu:

        ```csharp
        using System.Activities;
        using System.Activities.Core.Presentation;
        using System.Activities.Presentation;
        using System.Activities.Presentation.Metadata;
        using System.Activities.Presentation.Toolbox;
        using System.Activities.Statements;
        using System.ComponentModel;
        ```

    2. Fügen Sie der `MainWindow`-Klasse den folgenden Code hinzu, um ein privates Element Feld zu deklarieren, das eine Instanz von <xref:System.Activities.Presentation.WorkflowDesigner> enthalten soll:

        ```csharp
        public partial class MainWindow : Window
        {
            private WorkflowDesigner wd;

            public MainWindow()
            {
                InitializeComponent();
            }
        }
        ```

    3. Fügen Sie die folgende `AddDesigner`-Methode zu der `MainWindow`-Klasse hinzu. Die-Implementierung erstellt eine Instanz des-<xref:System.Activities.Presentation.WorkflowDesigner>, fügt ihr eine <xref:System.Activities.Statements.Sequence>-Aktivität hinzu und platziert Sie in der mittleren Spalte des grid1- **Rasters**.

        ```csharp
        private void AddDesigner()
        {
            // Create an instance of WorkflowDesigner class.
            this.wd = new WorkflowDesigner();

            // Place the designer canvas in the middle column of the grid.
            Grid.SetColumn(this.wd.View, 1);

            // Load a new Sequence as default.
            this.wd.Load(new Sequence());

            // Add the designer canvas to the grid.
            grid1.Children.Add(this.wd.View);
        }
        ```

    4. Registrieren Sie die Designer-Metadaten, um Designerunterstützung für alle integrierten Aktivitäten hinzuzufügen. Dies ermöglicht Ihnen, Aktivitäten aus der Toolbox auf der ursprünglichen <xref:System.Activities.Statements.Sequence>-Aktivität im [!INCLUDE[wfd2](../../../includes/wfd2-md.md)] abzulegen. Fügen Sie zu diesem Zweck der `MainWindow`-Klasse die `RegisterMetadata`-Methode hinzu:

        ```csharp
        private void RegisterMetadata()
        {
            var dm = new DesignerMetadata();
            dm.Register();
        }
        ```

        Weitere Informationen zum Registrieren von Aktivitäts Designern finden Sie unter [gewusst wie: Erstellen Sie einen benutzerdefinierten Aktivitäts Designer @ no__t-0.

    5. Fügen Sie im `MainWindow`-Klassenkonstruktor den zuvor deklarierten Methoden Aufrufe hinzu, um die Metadaten für die Designerunterstützung zu registrieren und das <xref:System.Activities.Presentation.WorkflowDesigner>-Objekt zu erstellen.

        ```csharp
        public MainWindow()
        {
            InitializeComponent();

            // Register the metadata.
            RegisterMetadata();

            // Add the WFF Designer.
            AddDesigner();
        }
        ```

        > [!NOTE]
        > Die `RegisterMetadata`-Methode registriert die Designer-Metadaten integrierter Aktivitäten, einschließlich der <xref:System.Activities.Statements.Sequence>-Aktivität. Da die `AddDesigner`-Methode die <xref:System.Activities.Statements.Sequence>-Aktivität verwendet, muss die `RegisterMetadata`-Methode zuerst aufgerufen werden.

9. Drücken Sie <kbd>F5</kbd> , um die Projekt Mappe zu erstellen und auszuführen.

10. Weitere Informationen finden Sie unter [task 3: Erstellen Sie die Toolbox-und PropertyGrid-Bereiche @ no__t-0, um zu erfahren, wie Sie den neu gehosteten Workflow-Designer Unterstützung für **Toolbox** und **PropertyGrid** hinzufügen.

## <a name="see-also"></a>Siehe auch

- [Erneutes Hosten des Workflow-Designers](rehosting-the-workflow-designer.md)
- [aufgabe 1: Erstellen einer neuen Windows Presentation Foundation Anwendung @ no__t-0
- [aufgabe 3: Erstellen der Toolbox-und PropertyGrid-Bereiche @ no__t-0
