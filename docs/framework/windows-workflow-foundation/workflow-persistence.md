---
title: Workflowpersistenz
ms.date: 03/30/2017
helpviewer_keywords:
- programming [WF], persistence
ms.assetid: 39e69d1f-b771-4c16-9e18-696fa43b65b2
ms.openlocfilehash: afe47975a393db3074222ebf0461f5b73fb6442d
ms.sourcegitcommit: 2701302a99cafbe0d86d53d540eb0fa7e9b46b36
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/28/2019
ms.locfileid: "64655792"
---
# <a name="workflow-persistence"></a>Workflowpersistenz
Workflowpersistenz bezeichnet die dauerhafte Erfassung des Zustands einer Workflowinstanz unabhängig von Prozess- oder Computerinformationen. Sie wird durchgeführt, um einen bekannten Wiederherstellungspunkt für die Workflowinstanz im Fall eines Systemfehlers bereitzustellen oder um Arbeitsspeicher beizubehalten, indem Workflowinstanzen entladen werden, die gerade nicht aktiv sind, bzw. um den Zustand der Workflowinstanz von einem Knoten zu einem anderen Knoten in einer Serverfarm zu verschieben.  
  
 Die Persistenz aktiviert die Flexibilität, Skalierbarkeit und Wiederherstellung von Prozessen bei einem Fehler und bietet die Möglichkeit, den Arbeitsspeicher effizienter zu verwalten. Der Persistenzvorgang umfasst die Identifikation eines Persistenzpunkts, das Sammeln der zu speichernden Daten und schließlich die Delegierung des tatsächlichen Speichers der Daten an einen Persistenzanbieter.  
  
 Zum Aktivieren der Persistenz für einen Workflow müssen Sie einen Instanzspeicher Zuordnen der **WorkflowApplication** oder **WorkflowServiceHost** Siehe [Vorgehensweise: Aktivieren der Persistenz für Workflows und Workflowdienste](how-to-enable-persistence-for-workflows-and-workflow-services.md). Die **WorkflowApplication** und **WorkflowServiceHost** verwenden Sie den Instanzspeicher zugeordnet werden, um beibehalten von Workflowinstanzen in einem persistenten Speicher und das Laden von Workflowinstanzen in zu aktivieren. Arbeitsspeicher, die basierend auf Daten der Workflowinstanz im persistenten Speicher gespeichert werden.  
  
 Die [!INCLUDE[netfx_current_long](../../../includes/netfx-current-long-md.md)] im Lieferumfang der **SqlWorkflowInstanceStore** -Klasse, die Persistenz von Daten und Metadaten zu Workflowinstanzen in einer SQL Server 2005 oder SQL Server 2008-Datenbank ermöglicht. Finden Sie unter [SQL Workflow-Instanz Store](sql-workflow-instance-store.md) Weitere Details.  
  
 Zum Speichern und Laden Ihrer anwendungsspezifischen Daten zusammen mit den Informationen zur Workflowinstanz können Sie Persistenzteilnehmer erstellen, die die <xref:System.Activities.Persistence.PersistenceParticipant>-Klasse erweitern. Ein Persistenzteilnehmer nimmt am Persistenzvorgang teil, um benutzerdefinierte serialisierbare Daten in den persistenten Speicher zu speichern, die Daten aus dem Instanzspeicher in den Arbeitsspeicher zu laden und ggf. die zusätzliche Logik einer Persistenztransaktion auszuführen. Weitere Informationen finden Sie unter [Persistenzteilnehmer](persistence-participants.md).  
  
 Windows Server AppFabric vereinfacht die Konfiguration von Persistenz. Weitere Informationen finden Sie unter [Persistenzkonzepte mit Windows Server AppFabric](https://go.microsoft.com/fwlink/?LinkId=201200)  
  
## <a name="implicit-persistence-points"></a>Implizite Persistenzpunkte  
 Die folgende Liste enthält Beispiele der Bedingungen, zu denen ein Workflow beibehalten wird, wenn ein Instanzspeicher einem Workflow zugeordnet ist.  
  
- Wenn eine **TransactionScope** Aktivität abgeschlossen wird oder ein **TransactedReceiveScope** Aktivität abgeschlossen wird.  
  
- Wenn eine Workflowinstanz im Leerlauf wird und die **WorkflowIdleBehavior** auf den Workflowhost festgelegt ist. In diesem Fall z. B. Wenn Sie messagingaktivitäten verwenden oder eine **Verzögerung** Aktivität.  
  
- Wenn eine Workflowanwendung im Leerlauf wird und die **PersistableIdle** der Anwendung-Eigenschaftensatz auf **PersistableIdleAction.Persist**.  
  
- Wenn eine Hostanwendung angewiesen ist, eine Workflowinstanz beizubehalten oder zu entladen.  
  
- Wenn eine Workflowinstanz beendet oder fertig gestellt wird.  
  
- Wenn eine **Persist** Aktivität ausgeführt wird.  
  
- Wenn eine Instanz eines Workflows, die mit einer früheren Version von Windows Workflow Foundation entwickelt wurde, während einer interoperablen Ausführung auf einen Persistenzpunkt trifft.  
  
## <a name="in-this-section"></a>In diesem Abschnitt  
  
- [SQL-Workflowinstanzspeicher](sql-workflow-instance-store.md)  
  
- [Instanzspeicher](instance-stores.md)  
  
- [Persistenzteilnehmer](persistence-participants.md)  
  
- [Empfohlene Vorgehensweisen für die Persistenz](persistence-best-practices.md)  
  
- [Nicht beibehaltene Workflowinstanzen](non-persisted-workflow-instances.md)  
  
- [Anhalten und Fortsetzen eines Workflows](pausing-and-resuming-a-workflow.md)
