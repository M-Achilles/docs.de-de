---
title: EXISTS (Entity SQL)
ms.date: 03/30/2017
ms.assetid: d28ead43-4afb-4bdc-af64-efd2e05005d7
ms.openlocfilehash: 44f128a292b013fd3a3a80efdd2d10a63e3cfb07
ms.sourcegitcommit: 8a0fe8a2227af612f8b8941bdb8b19d6268748e7
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 10/03/2019
ms.locfileid: "71833838"
---
# <a name="exists-entity-sql"></a>EXISTS (Entity SQL)
Bestimmt, ob eine Auflistung leer ist.  
  
## <a name="syntax"></a>Syntax  
  
```sql  
[NOT] EXISTS ( expression )  
```  
  
## <a name="arguments"></a>Argumente  
 `expression`  
 Jeder gültige Ausdruck, der eine Auflistung zurückgibt.  
  
 NICHT  
 Gibt an, dass das Ergebnis von EXISTS negiert werden soll.  
  
## <a name="return-value"></a>Rückgabewert  
 `true`, wenn die Auflistung nicht leer ist, andernfalls `false`.  
  
## <a name="remarks"></a>Hinweise  
 EXISTS[!INCLUDE[esql](../../../../../../includes/esql-md.md)] ist einer der -Mengenoperatoren. Alle [!INCLUDE[esql](../../../../../../includes/esql-md.md)] -Mengenoperatoren werden von links nach rechts ausgewertet. Informationen zu Rang folgen Informationen für die [!INCLUDE[esql](../../../../../../includes/esql-md.md)]-Mengen Operatoren finden Sie unter [Ausnahme](except-entity-sql.md)von.  
  
## <a name="example"></a>Beispiel  
 Die folgende Entity SQL-Abfrage verwendet den EXISTS-Operator, um festzustellen, ob die Auflistung leer ist. Diese Abfrage beruht auf dem "AdventureWorks Sales"-Modell. Führen Sie folgende Schritte aus, um diese Abfrage zu kompilieren und auszuführen:  
  
1. Befolgen Sie das Verfahren in [gewusst wie: Führen Sie eine Abfrage aus, die die StructuralType-Ergebnisse @ no__t-0 zurückgibt.  
  
2. Übergeben Sie die folgende Abfrage als Argument an die `ExecuteStructuralTypeQuery` -Methode:  
  
 [!code-sql[DP EntityServices Concepts#EXISTS](~/samples/snippets/tsql/VS_Snippets_Data/dp entityservices concepts/tsql/entitysql.sql#exists)]  
  
## <a name="see-also"></a>Siehe auch

- [Entity SQL-Referenz](entity-sql-reference.md)
