---
title: "XML ツリーの変更 (LINQ to XML) (C#)"
ms.custom: 
ms.date: 2015-07-20
ms.prod: .net
ms.reviewer: 
ms.suite: 
ms.technology:
- devlang-csharp
ms.topic: article
dev_langs:
- CSharp
ms.assetid: 8ec47e6d-2363-4694-be46-8d5ca4d15fc9
caps.latest.revision: 3
author: BillWagner
ms.author: wiwagn
ms.translationtype: HT
ms.sourcegitcommit: 306c608dc7f97594ef6f72ae0f5aaba596c936e1
ms.openlocfilehash: 0cb4ff851dbea97f254d5290ce021d560849e3d9
ms.contentlocale: ja-jp
ms.lasthandoff: 07/28/2017

---
# <a name="modifying-xml-trees-linq-to-xml-c"></a>XML ツリーの変更 (LINQ to XML) (C#)
[!INCLUDE[sqltecxlinq](~/includes/sqltecxlinq-md.md)] は、XML ツリーのメモリ内ストアです。 ソースから XML ツリーを読み込んだり解析したりした後に、[!INCLUDE[sqltecxlinq](~/includes/sqltecxlinq-md.md)] を使用してツリーを直接変更することができます。その後、ツリーをシリアル化して、ファイルに保存したり、リモート サーバーに送信したりできます。  
  
 ツリーを直接変更する際には、<xref:System.Xml.Linq.XContainer.Add%2A> などの特定のメソッドを使用します。  
  
 ただし、これには別の方法もあります。それは、関数型構築を使用して、別の新しいツリーを生成する方法です。 XML ツリーに対する変更の種類やツリーのサイズによっては、この方法の方が堅牢で、開発も容易になります。 このセクションの最初のトピックでは、この 2 つの方法を比較します。  
  
## <a name="in-this-section"></a>このセクションの内容  
  
|トピック|説明|  
|-----------|-----------------|  
|[メモリ内の XML ツリーの変更と関数型構築の比較 (LINQ to XML) (C#)](../../../../csharp/programming-guide/concepts/linq/in-memory-xml-tree-modification-vs-functional-construction-linq-to-xml.md)|XML ツリーのメモリ内での変更と関数型構築とを比較します。|  
|[XML ツリーへの要素、属性、およびノードの追加](../../../../csharp/programming-guide/concepts/linq/adding-elements-attributes-and-nodes-to-an-xml-tree.md)|XML ツリーへの要素、属性、またはノードの追加に関する情報について説明します。|  
|[XML ツリー内の要素、属性、およびノードの変更](../../../../csharp/programming-guide/concepts/linq/modifying-elements-attributes-and-nodes-in-an-xml-tree.md)|既存の要素、属性、またはノードの変更に関する情報について説明します。|  
|[XML ツリーからの要素、属性、およびノードの削除 (C#)](../../../../csharp/programming-guide/concepts/linq/removing-elements-attributes-and-nodes-from-an-xml-tree.md)|XML ツリーからの要素、属性、またはノードの削除に関する情報について説明します。|  
|[名前と値のペアの保持 (C#)](../../../../csharp/programming-guide/concepts/linq/maintaining-name-value-pairs.md)|アプリケーションの情報を名前/値のペアとして保持する方法について説明します。このような情報には、構成情報やグローバル設定があります。|  
|[方法: XML ツリー全体の名前空間を変更する (C#)](../../../../csharp/programming-guide/concepts/linq/how-to-change-the-namespace-for-an-entire-xml-tree.md)|XML ツリーを名前空間の間で移動する方法について説明します。|  
  
## <a name="see-also"></a>関連項目  
 [プログラミング ガイド (LINQ to XML) (C#)](../../../../csharp/programming-guide/concepts/linq/programming-guide-linq-to-xml.md)

