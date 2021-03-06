---
title: "ノード (Visual Basic) を使用したプログラミング |Microsoft ドキュメント"
ms.custom: 
ms.date: 2015-07-20
ms.prod: .net
ms.reviewer: 
ms.suite: 
ms.technology:
- devlang-visual-basic
ms.tgt_pltfrm: 
ms.topic: article
dev_langs:
- VB
ms.assetid: d8422a9b-dd37-44a3-8aac-2237ed9561e0
caps.latest.revision: 3
author: dotnet-bot
ms.author: dotnetcontent
translation.priority.mt:
- cs-cz
- pl-pl
- pt-br
- tr-tr
ms.translationtype: Machine Translation
ms.sourcegitcommit: a06bd2a17f1d6c7308fa6337c866c1ca2e7281c0
ms.openlocfilehash: 52fb60b95b869a79900f84c2a1a7a6151bb5b58f
ms.contentlocale: ja-jp
ms.lasthandoff: 03/13/2017

---
# <a name="programming-with-nodes-visual-basic"></a>ノード (Visual Basic) を使用したプログラミング
XML エディター、変換システム、レポート作成プログラムなどのプログラムを作成する [!INCLUDE[sqltecxlinq](../../../../csharp/programming-guide/concepts/linq/includes/sqltecxlinq_md.md)] の開発者は、要素や属性よりも細かい粒度レベルで動作するプログラムを作成しなければならないことがよくあります。 また場合によっては、ノード レベルで、テキスト ノード、処理命令、およびコメントを操作する必要があります。 このトピックでは、ノード レベルでのプログラミングについて詳しく説明します。  
  
## <a name="node-details"></a>ノードの詳細  
 ノード レベルで作業するプログラマが知っておく必要があるプログラミングの詳細事項がいくつかあります。  
  
### <a name="parent-property-of-children-nodes-of-xdocument-is-set-to-null"></a>XDocument の子ノードの Parent プロパティが Null に設定される  
 <xref:System.Xml.Linq.XObject.Parent%2A>プロパティには、親が含まれています<xref:System.Xml.Linq.XElement>、親ノードではなく。</xref:System.Xml.Linq.XElement> </xref:System.Xml.Linq.XObject.Parent%2A> 。 <xref:System.Xml.Linq.XDocument> <xref:System.Xml.Linq.XElement>。</xref:System.Xml.Linq.XElement>親</xref:System.Xml.Linq.XDocument>の子ノード 親は、ドキュメントのため、<xref:System.Xml.Linq.XObject.Parent%2A>それらのノードのプロパティの設定を null にします</xref:System.Xml.Linq.XObject.Parent%2A>。  
  
 この動作を次の例で示します。  
  
```vb  
Dim doc As XDocument = XDocument.Parse("<!-- a comment --><Root/>")  
Console.WriteLine(doc.Nodes().OfType(Of XComment).First().Parent Is Nothing)  
Console.WriteLine(doc.Root.Parent Is Nothing)  
```  
  
 この例を実行すると、次の出力が生成されます。  
  
```  
True  
True  
```  
  
### <a name="adjacent-text-nodes-are-possible"></a>隣接するテキスト ノードが存在する可能性がある  
 多くの XML プログラミング モデルでは、隣接するテキスト ノードが常に連結されます。 これは、テキスト ノードの正規化と呼ばれることがあります。 [!INCLUDE[sqltecxlinq](../../../../csharp/programming-guide/concepts/linq/includes/sqltecxlinq_md.md)] ではテキスト ノードは正規化されません。 同じ要素に&2; つのテキスト ノードを追加すると、隣接するテキスト ノードになります。 ただしではなく文字列として指定されたコンテンツを追加する場合、<xref:System.Xml.Linq.XText>ノード、[!INCLUDE[sqltecxlinq](../../../../csharp/programming-guide/concepts/linq/includes/sqltecxlinq_md.md)]を隣接するテキスト ノードに文字列を結合することがあります</xref:System.Xml.Linq.XText>。  
  
 この動作を次の例で示します。  
  
```vb  
Dim xmlTree As XElement = <Root>Content</Root>  
Console.WriteLine(xmlTree.Nodes().OfType(Of XText)().Count())  
  
' This does not add a new text node.  
xmlTree.Add("new content")  
Console.WriteLine(xmlTree.Nodes().OfType(Of XText)().Count())  
  
'// This does add a new, adjacent text node.  
xmlTree.Add(New XText("more text"))  
Console.WriteLine(xmlTree.Nodes().OfType(Of XText)().Count())  
```  
  
 この例を実行すると、次の出力が生成されます。  
  
```  
1  
1  
2  
```  
  
### <a name="empty-text-nodes-are-possible"></a>空のテキスト ノードが存在する可能性がある  
 一部の XML プログラミング モデルでは、テキスト ノードに空の文字列が含まれないことが保証されます。 その理由は、テキスト ノードに空の文字列が含まれていなければ、XML のシリアル化に対して影響が生じないためです。 ただし、隣接するテキスト ノードの場合と同じ理由で、テキスト ノードの値を空の文字列に設定することによってテキスト ノードからテキストを削除した場合、テキスト ノード自体は削除されません。  
  
```vb  
Dim xmlTree As XElement = <Root>Content</Root>  
Dim textNode As XText = xmlTree.Nodes().OfType(Of XText)().First()  
  
' The following line does not cause the removal of the text node.  
textNode.Value = ""  
  
Dim textNode2 As XText = xmlTree.Nodes().OfType(Of XText)().First()  
Console.WriteLine(">>{0}<<", textNode2)  
```  
  
 この例を実行すると、次の出力が生成されます。  
  
```  
>><<  
```  
  
### <a name="an-empty-text-node-impacts-serialization"></a>空のテキスト ノードがシリアル化に影響する  
 要素に空の子テキスト ノードのみが含まれている場合、その要素は長いタグ構文 `<Child></Child>` でシリアル化されます。 子ノードがまったく含まれていない要素は、短いタグ構文 `<Child />` でシリアル化されます。  
  
```vb  
Dim child1 As XElement = New XElement("Child1", _  
    New XText("") _  
)  
Dim child2 As XElement = New XElement("Child2")  
Console.WriteLine(child1)  
Console.WriteLine(child2)  
```  
  
 この例を実行すると、次の出力が生成されます。  
  
```  
<Child1></Child1>  
<Child2 />  
```  
  
### <a name="namespaces-are-attributes-in-the-linq-to-xml-tree"></a>LINQ to XML ツリーでは名前空間が属性になる  
 名前空間宣言の構文は属性と同じですが、XSLT や XPath などの一部のプログラミング インターフェイスでは、名前空間宣言が属性と見なされません。 ただし、 [!INCLUDE[sqltecxlinq](../../../../csharp/programming-guide/concepts/linq/includes/sqltecxlinq_md.md)]、として名前空間が格納されている<xref:System.Xml.Linq.XAttribute>XML ツリー内のオブジェクト</xref:System.Xml.Linq.XAttribute>。 名前空間宣言を含んでいる要素の属性を反復処理すると、名前空間宣言が、返されるコレクションの項目の&1; つになります。  
  
 <xref:System.Xml.Linq.XAttribute.IsNamespaceDeclaration%2A>プロパティは、属性は名前空間の宣言であるかどうかを示します</xref:System.Xml.Linq.XAttribute.IsNamespaceDeclaration%2A>。  
  
```vb  
Dim root As XElement = _   
<Root  
    xmlns='http://www.adventure-works.com'  
    xmlns:fc='www.fourthcoffee.com'  
    AnAttribute='abc'/>  
For Each att As XAttribute In root.Attributes()  
    Console.WriteLine("{0}  IsNamespaceDeclaration:{1}", att, _  
                      att.IsNamespaceDeclaration)  
Next  
```  
  
 この例を実行すると、次の出力が生成されます。  
  
```  
xmlns="http://www.adventure-works.com"  IsNamespaceDeclaration:True  
xmlns:fc="www.fourthcoffee.com"  IsNamespaceDeclaration:True  
AnAttribute="abc"  IsNamespaceDeclaration:False  
```  
  
### <a name="xpath-axis-methods-do-not-return-child-white-space-of-xdocument"></a>XPath 軸メソッドからは XDocument の空白の子ノードが返されない  
 [!INCLUDE[sqltecxlinq](../../../../csharp/programming-guide/concepts/linq/includes/sqltecxlinq_md.md)]子テキスト ノードでは、<xref:System.Xml.Linq.XDocument>テキスト ノードには、空白だけが含まれている限り、</xref:System.Xml.Linq.XDocument> 。 ただし、XPath オブジェクト モデルは含まれません空白文字、ドキュメントの子ノードとしてための子を反復処理すると、<xref:System.Xml.Linq.XDocument>を使用して、<xref:System.Xml.Linq.XContainer.Nodes%2A>軸、空白のテキスト ノードが返されます</xref:System.Xml.Linq.XContainer.Nodes%2A></xref:System.Xml.Linq.XDocument>。 子を反復処理するときに、 <xref:System.Xml.Linq.XDocument>XPath 軸メソッドを使用して、空白のテキスト ノードは返されません</xref:System.Xml.Linq.XDocument>。  
  
```vb  
' Create a document with some white space child nodes of the document.  
Dim root As XDocument = XDocument.Parse( _  
"<?xml version='1.0' encoding='utf-8' standalone='yes'?>" & _  
vbNewLine & "<Root/>" & vbNewLine & "<!--a comment-->" & vbNewLine, _  
LoadOptions.PreserveWhitespace)  
  
' Count the white space child nodes using LINQ to XML.  
Console.WriteLine(root.Nodes().OfType(Of XText)().Count())  
  
' Count the white space child nodes using XPathEvaluate.  
Dim nodes As IEnumerable = CType(root.XPathEvaluate("text()"), IEnumerable)  
Console.WriteLine(nodes.OfType(Of XText)().Count())  
```  
  
 この例を実行すると、次の出力が生成されます。  
  
```  
3  
0  
```  
  
### <a name="xdeclaration-objects-are-not-nodes"></a>XDeclaration オブジェクトはノードではない  
 子ノードを反復処理すると、 <xref:System.Xml.Linq.XDocument>、XML 宣言オブジェクトは表示されません</xref:System.Xml.Linq.XDocument>。 これはドキュメントのプロパティであって、ドキュメントの子ノードではありません。  
  
```vb  
Dim doc As XDocument = _  
<?xml version='1.0' encoding='utf-8' standalone='yes'?>  
<Root/>  
  
doc.Save("Temp.xml")  
Console.WriteLine(File.ReadAllText("Temp.xml"))  
  
' This shows that there is only one child node of the document.  
Console.WriteLine(doc.Nodes().Count())  
```  
  
 この例を実行すると、次の出力が生成されます。  
  
```  
<?xml version="1.0" encoding="utf-8" standalone="yes"?>  
<Root />  
1  
```  
  
## <a name="see-also"></a>関連項目  
 [高度な LINQ to XML のプログラミング (Visual Basic)](../../../../visual-basic/programming-guide/concepts/linq/advanced-linq-to-xml-programming.md)

