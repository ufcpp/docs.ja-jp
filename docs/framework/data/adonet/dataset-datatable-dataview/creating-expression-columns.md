---
title: "式列の作成 | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-ado"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 0af3bd64-92a2-4b47-ae62-f5df35f131a6
caps.latest.revision: 4
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 4
---
# 式列の作成
列の式を定義すると、同じ行の他の列値またはテーブル内の複数の行の列値に基づいて計算した値を、その列に格納できます。  評価する式を定義するには、対象の列の <xref:System.Data.DataColumn.Expression%2A> プロパティを使用し、その式で <xref:System.Data.DataColumn.ColumnName%2A> プロパティを使用して他の列を参照します。  式列の <xref:System.Data.DataColumn.DataType%2A> は、その式が返す値に適した型であることが必要です。  
  
 テーブル内の式列で使用できるいくつかの式の種類を次の表に示します。  
  
|式の種類|例|  
|----------|-------|  
|比較|"Total \>\= 500"|  
|計算|"UnitPrice \* Quantity"|  
|集約|Sum\(Price\)|  
  
 次の例に示すように、既存の **DataColumn** オブジェクトの **Expression** プロパティを設定したり、このプロパティを <xref:System.Data.DataColumn> コンストラクターに渡す 3 番目の引数として使用したりできます。  
  
```vb  
workTable.Columns.Add("Total",Type.GetType("System.Double"))  
workTable.Columns.Add("SalesTax", Type.GetType("System.Double"), _  
  "Total * 0.086")  
  
```  
  
```csharp  
workTable.Columns.Add("Total", typeof(Double));  
workTable.Columns.Add("SalesTax", typeof(Double), "Total * 0.086");  
```  
  
 式は他の式列を参照できます。ただし、2 つの式が相互に参照し合う循環参照の場合は、例外が生成されます。  式の記述の規則については、**DataColumn** クラスの <xref:System.Data.DataColumn.Expression%2A> プロパティのトピックを参照してください。  
  
## 参照  
 <xref:System.Data.DataColumn>   
 <xref:System.Data.DataSet>   
 <xref:System.Data.DataTable>   
 [DataTable スキーマの定義](../../../../../docs/framework/data/adonet/dataset-datatable-dataview/datatable-schema-definition.md)   
 [DataTable](../../../../../docs/framework/data/adonet/dataset-datatable-dataview/datatables.md)   
 [ADO.NET Managed Providers and DataSet Developer Center \(ADO.NET マネージ プロバイダーと DataSet デベロッパー センター\)](http://go.microsoft.com/fwlink/?LinkId=217917)