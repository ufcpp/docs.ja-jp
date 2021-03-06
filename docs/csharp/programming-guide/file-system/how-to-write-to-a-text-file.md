---
title: "方法: テキスト ファイルに書き込む (C# プログラミング ガイド)"
ms.date: 2015-07-20
ms.prod: .net
ms.technology:
- devlang-csharp
ms.topic: article
f1_keywords:
- TextWriter.WriteLine
- StreamWriter.Close
dev_langs:
- CSharp
helpviewer_keywords:
- files [C#], text files
- text, writing to files [C#]
ms.assetid: 2e99f184-d88b-4719-a7f1-d9ec482aa809
caps.latest.revision: 23
author: BillWagner
ms.author: wiwagn
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
ms.translationtype: HT
ms.sourcegitcommit: 306c608dc7f97594ef6f72ae0f5aaba596c936e1
ms.openlocfilehash: 12a74a5664a8f514c89d9de3ce470c98319f84d2
ms.contentlocale: ja-jp
ms.lasthandoff: 07/28/2017

---
# <a name="how-to-write-to-a-text-file-c-programming-guide"></a>方法: テキスト ファイルに書き込む (C# プログラミング ガイド)
テキストをファイルに書き込むさまざまな方法を次の例に示します。  最初の 2 つの例では、<xref:System.IO.File?displayProperty=fullName> クラスの静的なコンビニエンス メソッドを使用して、すべての IEnumerable\<string> の各要素と文字列をテキスト ファイルに記述しています。  例 3 は、ファイルに書き込むときに各行を個別に処理する必要がある場合にテキストをファイルに追加する方法を示します。  例 1 ～ 3 ではすべての既存の内容が上書きされます。例 4 に、既存のファイルにテキストを追加する方法を示します。  
  
 これらの例はいずれもファイルにリテラル文字列を書き込みますが、通常は、さまざまな型の値の書き込み、フィールド内での右揃えや左揃え、パディングの有無などに対応する多くのコントロールを持つ <xref:System.String.Format%2A> メソッドを使用します。  C# の[文字列補間](../../../csharp/language-reference/keywords/interpolated-strings.md)機能を使用することもできます。  
  
## <a name="example"></a>例  
 [!code-cs[csFilesandFolders#3](../../../csharp/programming-guide/file-system/codesnippet/CSharp/how-to-write-to-a-text-file_1.cs)]  
  
 これらの例はいずれもファイルにリテラル文字列を書き込みますが、通常は、さまざまな型の値の書き込み、フィールド内での右揃えや左揃え、パディングの有無などに対応する多くのコントロールを持つ <xref:System.String.Format%2A> メソッドを使用します。  C# の[文字列補間](../../../csharp/language-reference/keywords/interpolated-strings.md)機能を使用することもできます。  
  
## <a name="robust-programming"></a>信頼性の高いプログラミング  
 次の条件を満たす場合は、例外が発生する可能性があります。  
  
-   ファイルは存在するが、読み取り専用である。  
  
-   パス名が長すぎる。  
  
-   ディスクがいっぱいになっている。  
  
## <a name="see-also"></a>関連項目  
 [C# プログラミング ガイド](../../../csharp/programming-guide/index.md)   
 [ファイル システムとレジストリ (C# プログラミング ガイド)](../../../csharp/programming-guide/file-system/index.md)   
 [サンプル: コレクションをアプリケーション ストレージに保存する](http://code.msdn.microsoft.com/CSWinStoreAppSaveCollection-bed5d6e6)

