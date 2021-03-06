---
title: "SchemaImporterExtension の技術サンプル"
ms.custom: 
ms.date: 03/30/2017
ms.prod: .net
ms.reviewer: 
ms.suite: 
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 3f5eb78f-0ef6-433a-b095-3a63b1ce0bc9
caps.latest.revision: 6
author: Erikre
ms.author: erikre
manager: erikre
ms.translationtype: HT
ms.sourcegitcommit: 717bcb6f9f72a728d77e2847096ea558a9c50902
ms.openlocfilehash: be04c759d53b74208ac4e9a9cf7a2ac4cf3f8cce
ms.contentlocale: ja-jp
ms.lasthandoff: 08/21/2017

---
# <a name="schemaimporterextension-technology-sample"></a>SchemaImporterExtension の技術サンプル
[サンプルのダウンロード](http://download.microsoft.com/download/4/7/B/47B2164C-E780-4B10-8DE4-2CB5B886E0A6/Technologies/Serialization/Xml%20Serialization/SchemaImporterExtension.zip.exe)  
  
 このサンプルでは、XML スキーマをインポートするときのコード生成を微調整する、<xref:System.Xml.Serialization.Advanced.SchemaImporterExtension> のカスタム化を示します。 このアプリケーションは、この拡張機能のビルド、登録および起動の方法を示しています。  
  
### <a name="to-build-the-sample-using-the-command-prompt"></a>コマンド プロンプトを使用してサンプルをビルドするには  
  
1.  コマンド プロンプト ウィンドウを開き、サンプルが格納されている、言語固有のサブディレクトリのいずれかに移動します。  
  
2.  コマンド ラインで「**msbuild.exe OrderSchemaImporterExtension.sln**」と入力します。  
  
### <a name="to-build-the-sample-using-visual-studio"></a>Visual Studio を使用してサンプルをビルドするには  
  
1.  [!INCLUDE[fileExplorer](../../../includes/fileexplorer-md.md)]を開き、サンプルが格納されている、言語固有のサブディレクトリのいずれかに移動します。  
  
2.  OrderSchemaImporterExtension.sln ファイルのアイコンをダブルクリックして、このファイルを Visual Studio で開きます。  
  
3.  **[ビルド]** メニューの **[ソリューションのビルド]**をクリックします。  
  
 アプリケーションは、既定の \bin ディレクトリまたは \bin\Debug ディレクトリにビルドされます。  
  
### <a name="to-run-the-sample"></a>サンプルを実行するには  
  
1.  コマンド プロンプトを使用して、新しい実行可能ファイルが格納されているディレクトリに移動します。  
  
2.  コマンド ラインで**実行ファイル名**を入力します。  
  
## <a name="remarks"></a>コメント  
 サンプルのバイナリ ファイルを作成する方法およびサンプルを登録する手順の詳細については、ソース コード ファイルおよび build.proj ファイル内のコメントを参照してください。  
  
## <a name="see-also"></a>関連項目  
 <xref:System.CodeDom.CodeCompileUnit>   
 <xref:System.CodeDom.CodeNamespace>   
 <xref:System.CodeDom.CodeNamespaceImport>   
 <xref:Microsoft.CSharp.CSharpCodeProvider>   
 <xref:System.Xml.Serialization.IXmlSerializable>   
 <xref:System.Xml.Serialization.Advanced.SchemaImporterExtension>   
 <xref:System.CodeDom>   
 <xref:System.CodeDom.Compiler>   
 <xref:System.Web.Services.Description>   
 <xref:System.Web.Services.Discovery>   
 <xref:System.Xml.Serialization>   
 <xref:System.Uri>   
 <xref:Microsoft.VisualBasic.VBCodeProvider>   
 <xref:System.Web.Services.Description.WebReference>   
 <xref:System.Xml.Serialization.XmlSchemaImporter>

