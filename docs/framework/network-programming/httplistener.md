---
title: HttpListener
ms.date: 03/30/2017
helpviewer_keywords:
- HTTP
ms.assetid: 5b89d3fb-3c9a-49e2-af1f-c34c020c68ac
ms.openlocfilehash: d5b07617617ac28e4f7f72bc23a96b45a85dff75
ms.sourcegitcommit: 289e06e904b72f34ac717dbcc5074239b977e707
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 09/17/2019
ms.locfileid: "71047977"
---
# <a name="httplistener"></a>HttpListener
Die <xref:System.Net.HttpListener>-Klasse stellt einen programmgesteuerten HTTP-Protokolllistener bereit. Der Listener ist für die Lebensdauer des <xref:System.Net.HttpListener>-Objekts aktiv und wird in der Anwendung ausgeführt.  
  
## <a name="httpsys"></a>HTTP.SYS  
 Die <xref:System.Net.HttpListener>-Klasse basiert auf HTTP.sys; hierbei handelt es sich um den Kernelmoduslistener, der den gesamten HTTP-Verkehr für Windows verarbeitet. HTTP.sys bietet Verbindungsverwaltung, Bandbreiteneinschränkung und Webserverprotokollierung. Verwenden Sie das Tool "`HttpCfg.exe`", um SSL-Zertifikate hinzuzufügen. Weitere Informationen finden Sie in der Dokumentation zum Tool [HttpCfg.exe](https://go.microsoft.com/fwlink/?LinkID=178284) in der [Server](https://go.microsoft.com/fwlink/?LinkID=178285)-Dokumentation.  
  
## <a name="see-also"></a>Siehe auch

- <xref:System.Net.HttpListener>
- <xref:System.Net.HttpWebRequest>
- <xref:System.Net.HttpWebResponse>
- [HTTP-Server](https://go.microsoft.com/fwlink/?LinkID=178285)
- [Security Enhancements in Internet Information (Sicherheitsverbesserungen bei Internetinformationen)](https://go.microsoft.com/fwlink/?LinkID=178286)
- [Beispiel zur HttpListener ASPX-Hostanwendung](https://go.microsoft.com/fwlink/?LinkID=179560)
- [Beispiel zur HttpListener-Technologie](https://go.microsoft.com/fwlink/?LinkID=179558)
- [Beispiele zur Netzwerkprogrammierung](network-programming-samples.md)
