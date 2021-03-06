---
title: 'Vorgehensweise: Verarbeiten von Ereignissen in einer Web Forms-Anwendung'
ms.date: 03/30/2017
ms.technology: dotnet-standard
dev_langs:
- csharp
- vb
helpviewer_keywords:
- events [.NET Framework], Web Forms
- Web Forms controls, and events
- event handlers [.NET Framework], Web Forms
- events [.NET Framework], consuming
- Web Forms, event handling
ms.assetid: 73bf8638-c4ec-4069-b0bb-a1dc79b92e32
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: dc1dee9377200e4c9fd575b8dcd00982db45f249
ms.sourcegitcommit: 0be8a279af6d8a43e03141e349d3efd5d35f8767
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/18/2019
ms.locfileid: "59317810"
---
# <a name="how-to-consume-events-in-a-web-forms-application"></a>Vorgehensweise: Verarbeiten von Ereignissen in einer Web Forms-Anwendung
Ein häufiges Szenario in ASP.NET Web Forms-Anwendungen ist das Auffüllen einer Webseite mit Steuerelementen und das anschließende Durchführen einer bestimmten Aktion, auf deren Steuerelement der Benutzer klickt. Beispielsweise löst ein <xref:System.Web.UI.WebControls.Button?displayProperty=nameWithType>-Steuerelement ein Ereignis aus, wenn der Benutzer auf der Webseite darauf klickt. Durch die Verarbeitung des Ereignisses kann Ihre Anwendung die zugehörige Anwendungslogik für diesen Schaltflächenklick ausführen.  
  
### <a name="to-handle-a-button-click-event-on-a-webpage"></a>So behandeln Sie ein Click-Ereignis auf einer Webseite  
  
1. Erstellen Sie eine ASP.NET Web Forms-Seite (Webseite), bei der der `OnClick`-Wert des <xref:System.Web.UI.WebControls.Button>-Steuerelements auf den Namen der Methode festgelegt ist, die Sie im nächsten Schritt definieren.  
  
    ```xml  
    <asp:Button ID="Button1" runat="server" Text="Click Me" OnClick="Button1_Click" />  
    ```  
  
2. Definieren Sie einen Ereignishandler, der der Delegatsignatur des <xref:System.Web.UI.WebControls.Button.Click>-Ereignisses entspricht und den von Ihnen für den `OnClick`-Wert definierten Namen trägt.  
  
    ```csharp  
    protected void Button1_Click(object sender, EventArgs e)  
    {  
        // perform action  
    }  
    ```  
  
    ```vb  
    Protected Sub Button1_Click(sender As Object, e As EventArgs) Handles Button1.Click  
        ' perform action  
    End Sub  
    ```  
  
     Das <xref:System.Web.UI.WebControls.Button.Click>-Ereignis verwendet die <xref:System.EventHandler>-Klasse für den Delegattyp und die <xref:System.EventArgs>-Klasse für die Ereignisdaten. Das Framework für ASP.NET-Seiten generiert automatisch Code, der eine <xref:System.EventHandler>-Instanz erstellt und diese Delegatinstanz dem <xref:System.Web.UI.WebControls.Button.Click>-Ereignis der <xref:System.Web.UI.WebControls.Button>-Instanz hinzufügt.  
  
3. Fügen Sie in der in Schritt 2 definierten Ereignishandlermethode Code hinzu, um die beim Auftreten des Ereignisses erforderlichen Aktionen auszuführen.  
  
## <a name="see-also"></a>Siehe auch

- [Ereignisse](../../../docs/standard/events/index.md)
