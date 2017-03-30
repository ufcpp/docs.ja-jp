---
title: "呼び出し元情報 (Visual Basic) |Microsoft ドキュメント"
ms.custom: 
ms.date: 2015-07-20
ms.prod: .net
ms.reviewer: 
ms.suite: 
ms.technology:
- devlang-visual-basic
ms.topic: article
dev_langs:
- VB
ms.assetid: 15d556eb-4d0c-4497-98a3-7f60abb7d6a1
caps.latest.revision: 3
author: stevehoag
ms.author: shoag
translation.priority.mt:
- cs-cz
- pl-pl
- pt-br
- tr-tr
translationtype: Machine Translation
ms.sourcegitcommit: a06bd2a17f1d6c7308fa6337c866c1ca2e7281c0
ms.openlocfilehash: 9a4b63fb424ad6aef9d1bd56f43ccccd79f0b9b3
ms.lasthandoff: 03/13/2017

---
# <a name="caller-information-visual-basic"></a>呼び出し元情報 (Visual Basic)
呼び出し元情報の属性を使用すると、メソッドへの呼び出し元に関する情報を取得できます。 ソース コードのファイル パス、ソース コードの行番号、および呼び出し元のメンバー名を取得できます。 この情報は、トレース、デバッグ、および診断ツールの作成に役立ちます。  
  
 この情報を取得するには、省略可能なパラメーターに適用される属性を使用します。各パラメーターには既定値があります。 次の表に、呼び出し元情報属性で定義されている、<xref:System.Runtime.CompilerServices?displayProperty=fullName>名前空間:</xref:System.Runtime.CompilerServices?displayProperty=fullName>  
  
|属性|説明|型|  
|---|---|---|  
|<xref:System.Runtime.CompilerServices.CallerFilePathAttribute></xref:System.Runtime.CompilerServices.CallerFilePathAttribute>|呼び出し元を含むソース ファイルのフル パスです。 これは、コンパイル時のファイル パスです。|`String`|  
|<xref:System.Runtime.CompilerServices.CallerLineNumberAttribute></xref:System.Runtime.CompilerServices.CallerLineNumberAttribute>|メソッドが呼び出されたソース ファイルの行番号。|`Integer`|  
|<xref:System.Runtime.CompilerServices.CallerMemberNameAttribute></xref:System.Runtime.CompilerServices.CallerMemberNameAttribute>|呼び出し元のメソッド名またはプロパティ名。 参照してください[メンバー名](#MEMBERNAMES)このトピックで後述します。|`String`|  
  
## <a name="example"></a>例  
 呼び出し元情報の属性を使用する方法の例を次に示します。 `TraceMessage` メソッドを呼び出すたびに、呼び出し元情報は、省略可能なパラメーターの引数として設定されます。  
  
```vb  
Private Sub DoProcessing()  
    TraceMessage("Something happened.")  
End Sub  
  
Public Sub TraceMessage(message As String,  
        <System.Runtime.CompilerServices.CallerMemberName> Optional memberName As String = Nothing,  
        <System.Runtime.CompilerServices.CallerFilePath> Optional sourcefilePath As String = Nothing,  
        <System.Runtime.CompilerServices.CallerLineNumber()> Optional sourceLineNumber As Integer = 0)  
  
    System.Diagnostics.Trace.WriteLine("message: " & message)  
    System.Diagnostics.Trace.WriteLine("member name: " & memberName)  
    System.Diagnostics.Trace.WriteLine("source file path: " & sourcefilePath)  
    System.Diagnostics.Trace.WriteLine("source line number: " & sourceLineNumber)  
End Sub  
  
' Sample output:  
'   message: Something happened.  
'   member name: DoProcessing  
'   source file path: C:\Users\username\Documents\Visual Studio 2012\Projects\CallerInfoVB\CallerInfoVB\Form1.vb  
'   source line number: 15  
```  
  
## <a name="remarks"></a>解説  
 省略可能な各パラメーターには、明示的な既定値を指定する必要があります。 省略可能と指定されていないパラメーターには、呼び出し元情報の属性を適用できません。  
  
 呼び出し元情報の属性によってパラメーターが省略可能になるわけではありません。 この属性は、引数を省略したときに渡される既定値に影響します。  
  
 呼び出し元情報の値は、コンパイル時に中間言語 (IL) 内にリテラルとして出力されます。 結果とは異なり、<xref:System.Exception.StackTrace%2A>難読化によるプロパティは、結果の例外の影響を受けません</xref:System.Exception.StackTrace%2A>。  
  
 省略可能な引数を明示的に指定して、呼び出し元情報を制御したり、非表示にしたりできます。  
  
###  <a name="MEMBERNAMES"></a>メンバー名  
 `CallerMemberName` 属性を使用して、呼び出されたメソッドにメンバー名を `String` 引数として指定することを回避できます。 この手法を使用すると、問題を回避するを**名前の変更リファクタリング**変更されない、`String`値。 この利点は、次のタスクで役立ちます。  
  
-   トレース ルーチンと診断ルーチンの使用。  
  
-   実装する、<xref:System.ComponentModel.INotifyPropertyChanged>インターフェイスのデータをバインドする場合</xref:System.ComponentModel.INotifyPropertyChanged>。 このインターフェイスを使用すると、オブジェクトのプロパティが、プロパティが変更されたことをデータ バインド コントロールに通知できます。これによって、このコントロールは、更新された情報を表示できます。 `CallerMemberName` 属性がない場合は、リテラルとしてプロパティ名を指定する必要があります。  
  
 次のグラフは、`CallerMemberName` 属性の使用時に返されるメンバー名を示します。  
  
|呼び出しは、次のものの中で発生します。|メンバー名の結果|  
|-------------------------|------------------------|  
|メソッド、プロパティ、またはイベント|呼び出しが発生したメソッド、プロパティ、またはイベントの名前。|  
|コンストラクター|文字列「.ctor」|  
|静的コンストラクター|文字列「.cctor」|  
|デストラクターです。|文字列「Finalize」|  
|ユーザー定義の演算子または変換|生成されたメンバー名 (「op_Addition」など)。|  
|Attribute コンストラクター|属性が適用されるメンバーの名前。 属性がメンバー内の要素 (パラメーター、戻り値、ジェネリック型パラメーターなど) である場合、この結果は、その要素に関連付けられているメンバーの名前になります。|  
|含んでいないメンバー (型に適用されているアセンブリ レベルや属性など)|省略可能なパラメーターの既定値。|  
  
## <a name="see-also"></a>関連項目  
 [属性 (Visual Basic)](../../../visual-basic/language-reference/attributes.md)   
 [一般的な属性 (Visual Basic)](../../../visual-basic/programming-guide/concepts/attributes/common-attributes.md)   
 [省略可能なパラメーター](../../../visual-basic/programming-guide/language-features/procedures/optional-parameters.md)   
 [プログラミングの概念 (Visual Basic)](../../../visual-basic/programming-guide/concepts/index.md)