---
title: "アセンブリを作成できません:&lt;エラー メッセージ&gt;|Microsoft ドキュメント"
ms.date: 2015-07-20
ms.prod: .net
ms.reviewer: 
ms.suite: 
ms.technology:
- devlang-visual-basic
ms.topic: article
f1_keywords:
- vbc30145
- bc30145
dev_langs:
- VB
helpviewer_keywords:
- BC30145
ms.assetid: 2e7eb2b9-eda6-4bdb-95cc-72c7f0be7528
caps.latest.revision: 11
author: dotnet-bot
ms.author: dotnetcontent
translation.priority.ht:
- cs-cz
- de-de
- es-es
- fr-fr
- it-it
- ja-jp
- ko-kr
- pl-pl
- pt-br
- ru-ru
- tr-tr
- zh-cn
- zh-tw
translationtype: Machine Translation
ms.sourcegitcommit: a06bd2a17f1d6c7308fa6337c866c1ca2e7281c0
ms.openlocfilehash: dac4b133882c043f9c84e936bad2e36f35fc4c33
ms.lasthandoff: 03/13/2017

---
# <a name="unable-to-emit-assembly-lterror-messagegt"></a>アセンブリを作成できません:&lt;エラー メッセージ&gt;
[!INCLUDE[vbprvb](../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)] コンパイラは、マニフェストを伴うアセンブリを生成するためにアセンブリ リンカー (Al.exe、Alink とも呼ばれます) を呼び出しますが、アセンブリを生成する出力段階でリンカーからエラーが報告されます。  
  
 **エラー ID:** BC30145  
  
## <a name="to-correct-this-error"></a>このエラーを解決するには  
  
1.  引用符で囲まれたエラー メッセージを調べ、トピックを参照してください。 [Al.exe ツールのエラーと警告](http://msdn.microsoft.com/en-us/7f125d49-0a03-47a6-9ba9-d61a679a7d4b)さらに詳しい説明とアドバイスします。  
  
2.  アセンブリを手動で署名を使用してください、 [Al.exe (アセンブリ リンカー)](https://msdn.microsoft.com/library/c405shex)または[Sn.exe (厳密名ツール)](https://msdn.microsoft.com/library/k5b5tt23)します。  
  
3.  エラーが続く場合は、状況に関する情報を収集し、マイクロソフト プロダクト サポート サービスに通知してください。  
  
### <a name="to-sign-the-assembly-manually"></a>アセンブリを手動で署名するには  
  
1.  使用して、 [Sn.exe (厳密名ツール)](https://msdn.microsoft.com/library/k5b5tt23)公開/秘密キー ペア ファイルを作成します。  
  
     このファイルは .snk の拡張子を持ちます。  
  
2.  エラーが発生している COM 参照をプロジェクトから削除します。  
  
3.  Windows の**開始** メニューをポイント**プログラム**、 をポイント**Microsoft Visual Studio 2008**、 をポイント**Visual Studio Tools**、 をクリックし、 **Visual Studio 2008 コマンド プロンプト**します。  
  
4.  アセンブリ ラッパーを格納するディレクトリに移動します。  
  
5.  次のコードを入力します。  
  
    ```  
    tlbimp <path to COM reference file> /out:<output assembly name> /keyfile:<path to .snk file>  
    ```  
  
     コードの一例として、次のように入力することができます。  
  
    ```  
    tlbimp c:\windows\system32\msi.dll /out:Interop.WindowsInstaller.dll /keyfile:"c:\documents and settings\mykey.snk"  
    ```  
  
     パスやファイルに空白が含まれている場合には、二重引用符 (") を使用します。  
  
6.  [!INCLUDE[vsprvs](../../../csharp/includes/vsprvs_md.md)] で、作成したファイルに .NET アセンブリへの参照を追加します。  
  
## <a name="see-also"></a>関連項目  
 [Al.exe (アセンブリ リンカー)](https://msdn.microsoft.com/library/c405shex)   
 [Al.exe ツールのエラーと警告](http://msdn.microsoft.com/en-us/7f125d49-0a03-47a6-9ba9-d61a679a7d4b)   
 [Sn.exe (厳密名ツール)](https://msdn.microsoft.com/library/k5b5tt23)   
 [方法 : 公開キーと秘密キーのキー ペアを作成する](http://msdn.microsoft.com/library/05026813-f3bd-4d7c-9e0b-fc588eb3d114)   
 [ご意見](https://docs.microsoft.com/visualstudio/ide/talk-to-us)
