---
title: "WordprocessingML ドキュメントの構造 (C#)"
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
ms.assetid: 3791b5e0-c502-469b-bb75-a7bf6fdd0a94
caps.latest.revision: 3
author: BillWagner
ms.author: wiwagn
ms.translationtype: HT
ms.sourcegitcommit: 306c608dc7f97594ef6f72ae0f5aaba596c936e1
ms.openlocfilehash: f5471b03c0bc5b96686f200318aacb71617805a3
ms.contentlocale: ja-jp
ms.lasthandoff: 07/28/2017

---
# <a name="shape-of-wordprocessingml-documents-c"></a>WordprocessingML ドキュメントの構造 (C#)
このトピックでは、WordprocessingML ドキュメントの XML 構造について説明します。  
  
## <a name="microsoft-office-formats"></a>Microsoft Office 形式  
 2007 Microsoft Office システムのネイティブ ファイル形式は Office Open XML (一般的な呼称は Open XML) です。 Open XML は Ecma 標準の XML ベースの形式であり、現在は ISO-IEC 標準としての検討が進められている段階です。 Open XML 内のワード プロセッシング ファイルのマークアップ言語は WordprocessingML と呼ばれます。 このチュートリアルの例では、WordprocessingML ソース ファイルを入力として使用します。  
  
 Microsoft Office 2003 を使用しており、Microsoft Office Compatibility Pack for Word, Excel, and PowerPoint 2007 File Formats をインストールしている場合は、Office Open XML Formats でドキュメントを保存できます。  
  
## <a name="the-shape-of-wordprocessingml-documents"></a>WordprocessingML ドキュメントの構造  
 最初に理解する必要があるのは WordprocessingML ドキュメントの構造です。 WordprocessingML ドキュメントには、ドキュメントの段落を含む本文要素 (名前は `w:body`) が 1 つあります。 各段落には、1 つ以上のテキスト ラン (名前は `w:r`) が含まれています。 各テキスト ランには、1 つ以上のテキスト片 (名前は `w:t`) が含まれています。  
  
 非常に単純な WordprocessingML ドキュメントを次に示します。  
  
```xml  
<?xml version="1.0" encoding="utf-8" standalone="yes"?>  
<w:document  
xmlns:ve="http://schemas.openxmlformats.org/markup-compatibility/2006"  
xmlns:o="urn:schemas-microsoft-com:office:office"  
xmlns:r="http://schemas.openxmlformats.org/officeDocument/2006/relationships"  
xmlns:m="http://schemas.openxmlformats.org/officeDocument/2006/math"  
xmlns:v="urn:schemas-microsoft-com:vml"  
xmlns:wp="http://schemas.openxmlformats.org/drawingml/2006/wordprocessingDrawing"  
xmlns:w10="urn:schemas-microsoft-com:office:word"  
xmlns:w="http://schemas.openxmlformats.org/wordprocessingml/2006/main"  
xmlns:wne="http://schemas.microsoft.com/office/word/2006/wordml">  
  <w:body>  
    <w:p w:rsidR="00E22EB6"  
         w:rsidRDefault="00E22EB6">  
      <w:r>  
        <w:t>This is a paragraph.</w:t>  
      </w:r>  
    </w:p>  
    <w:p w:rsidR="00E22EB6"  
         w:rsidRDefault="00E22EB6">  
      <w:r>  
        <w:t>This is another paragraph.</w:t>  
      </w:r>  
    </w:p>  
  </w:body>  
</w:document>  
```  
  
 このドキュメントには、2 つの段落が含まれています。 各段落には 1 つのテキスト ランが含まれており、各テキスト ランには 1 つのテキスト片が含まれています。  
  
 WordprocessingML ドキュメントの内容を XML 形式で表示する最も簡単な方法は、Microsoft Word を使用して WordprocessingML ドキュメントを作成および保存し、次のプログラムを実行してコンソールに XML を出力することです。  
  
 この例では、WindowsBase アセンブリに含まれるクラスを使用します。 また、<xref:System.IO.Packaging?displayProperty=fullName> 名前空間内の型を使用します。  
  
```csharp  
const string documentRelationshipType =  
  "http://schemas.openxmlformats.org/officeDocument/2006/relationships/officeDocument";  
const string wordmlNamespace =  
  "http://schemas.openxmlformats.org/wordprocessingml/2006/main";  
XNamespace w = wordmlNamespace;  
  
using (Package wdPackage = Package.Open("SampleDoc.docx", FileMode.Open, FileAccess.Read))  
{  
    PackageRelationship relationship =  
        wdPackage  
        .GetRelationshipsByType(documentRelationshipType)  
        .FirstOrDefault();  
    if (relationship != null)  
    {  
        Uri documentUri =  
            PackUriHelper.ResolvePartUri(  
                new Uri("/", UriKind.Relative),  
                relationship.TargetUri);  
        PackagePart documentPart = wdPackage.GetPart(documentUri);  
  
        //  Get the officeDocument part from the package.  
        //  Load the XML in the part into an XDocument instance.  
        XDocument xdoc =  
            XDocument.Load(XmlReader.Create(documentPart.GetStream()));  
        Console.WriteLine(xdoc.Root);  
    }  
}  
```  
  
## <a name="external-resources"></a>外部リソース  
 [Office (2007) Open XML ファイル形式の概要](http://go.microsoft.com/fwlink/?LinkId=98093)  
  
 [WordprocessingML の概要](http://go.microsoft.com/fwlink/?LinkId=98094)  
  
 [Office 2003: XML リファレンス スキーマのダウンロード ページ](http://go.microsoft.com/fwlink/?LinkId=98095)  
  
## <a name="see-also"></a>関連項目  
 [チュートリアル: WordprocessingML ドキュメント内のコンテンツの操作 (C#)](../../../../csharp/programming-guide/concepts/linq/tutorial-manipulating-content-in-a-wordprocessingml-document.md)

