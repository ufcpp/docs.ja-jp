---
title: "Deferred versus Immediate Loading | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-ado"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: d1d7247f-a3b7-460b-b342-5c1a2365aa1a
caps.latest.revision: 2
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 2
---
# Deferred versus Immediate Loading
オブジェクトに対してクエリを実行すると、要求したオブジェクトだけが実際に取得されます。  *関連*オブジェクトが自動で同時に取得されることはありません。  \(詳細については、「[Querying Across Relationships](../../../../../../docs/framework/data/adonet/sql/linq/querying-across-relationships.md)」を参照してください\)。ただし、関連オブジェクトにアクセスしようとすると、それらを取得する要求が生成されるため、関連オブジェクトがまだ読み込まれていない状態を識別することはできません。  
  
 たとえば、特定の注文のセットを取得するクエリを実行し、ときおり特定の顧客に電子メール通知を送信しようとしているとします。  最初から注文ごとにすべての顧客データを取得する必要はありません。  遅延読み込みを使用すると、関連情報が実際に必要になるまで、その情報の取得を遅らせることができます。  次に例を示します。  
  
 [!code-csharp[DLinqQueryConcepts#1](../../../../../../samples/snippets/csharp/VS_Snippets_Data/DLinqQueryConcepts/cs/Program.cs#1)]
 [!code-vb[DLinqQueryConcepts#1](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/DLinqQueryConcepts/vb/Module1.vb#1)]  
  
 その反対も同様です。  顧客データと注文データを同時に表示する必要のあるアプリケーションがあるとします。  両方のデータが必要であることがわかっています。  このアプリケーションでは、結果を取得するのと同時に、各顧客の注文情報が必要になります。  すべての顧客について注文を照会する個別のクエリを発行するのは適切ではありません。  ここで必要なのは、注文データと顧客データを同時に収集することです。  
  
 [!code-csharp[DLinqQueryConcepts#2](../../../../../../samples/snippets/csharp/VS_Snippets_Data/DLinqQueryConcepts/cs/Program.cs#2)]
 [!code-vb[DLinqQueryConcepts#2](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/DLinqQueryConcepts/vb/Module1.vb#2)]  
  
 1 つのクエリでクロス積によって顧客データと注文データを結合し、すべての関連データを大きな 1 つの投影として取得することもできます。  ただし、このような結果はエンティティではありません   \(詳細については、「[The LINQ to SQL Object Model](../../../../../../docs/framework/data/adonet/sql/linq/the-linq-to-sql-object-model.md)」を参照してください\)。  エンティティとは、識別子を持ち、変更が可能なオブジェクトですが、これらの結果は投影であり、変更や永続化はできません。  さらに、平坦な結合出力では、注文ごとに各顧客が繰り返し現れるため、余分なデータが大量に取得されることになります。  
  
 ここで必要なのは、関連オブジェクトのセットを同時に取得することです。  このセットは、目的の用途に必要十分なデータだけを取得できるように、グラフ上に線引きされた区画に相当します。  この目的から、[!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] では、オブジェクト モデルの特定の領域の即時読み込みを行う <xref:System.Data.Linq.DataLoadOptions> が用意されています。  次のメソッドがあります。  
  
-   <xref:System.Data.Linq.DataLoadOptions.LoadWith%2A> メソッド。メイン ターゲットに関連するデータを即時に読み込みます。  
  
-   <xref:System.Data.Linq.DataLoadOptions.AssociateWith%2A> メソッド。特定のリレーションシップに対して取得されるオブジェクトにフィルターを適用します。  
  
## 参照  
 [Query Concepts](../../../../../../docs/framework/data/adonet/sql/linq/query-concepts.md)