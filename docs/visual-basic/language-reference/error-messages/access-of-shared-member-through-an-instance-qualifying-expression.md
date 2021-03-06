---
title: "インスタンスを通じて共有メンバーへのアクセス正規の式は評価されません。Microsoft ドキュメント"
ms.date: 2015-07-20
ms.prod: .net
ms.suite: 
ms.technology:
- devlang-visual-basic
ms.topic: article
f1_keywords:
- vbc42025
- BC42025
dev_langs:
- VB
helpviewer_keywords:
- BC42025
ms.assetid: db3337e5-c349-42bf-86df-d9c1e00952a5
caps.latest.revision: 23
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
ms.openlocfilehash: 39be3c95d5acc20afe3a33be9d4db48c09f99a9c
ms.lasthandoff: 03/13/2017

---
# <a name="access-of-shared-member-through-an-instance-qualifying-expression-will-not-be-evaluated"></a>インスタンスを経由する共有メンバーへのアクセスです。正規の式は評価されません。
クラスまたは構造体のインスタンス変数の使用にアクセスする、`Shared`変数、プロパティ、プロシージャ、またはそのクラスまたは構造体で定義されたイベント。 この警告は、インスタンス変数を使用して、クラスまたは構造体、定数または列挙型、または入れ子になったクラスや構造体などの暗黙的な共有メンバーにアクセスする場合にも発生することができます。  
  
 メンバーの共有の目的は、そのメンバーの&1; つのコピーのみを作成し、その&1; つのコピーのクラスまたは構造体の宣言されているすべてのインスタンスを使用できるようにです。 アクセスするには、この目的で一貫性が、`Shared`メンバーがそのクラスまたは構造体の個々 のインスタンスを保持する変数ではなく、クラスまたは構造の名前を使用します。  
  
 アクセス、`Shared`インスタンス変数を使用してメンバー コードも容易に、メンバーであるという事実を隠すことで理解しづらい`Shared`します。 さらに、このようなアクセスが式の一部である場合などに、他のアクションを実行するには`Function`共有メンバーのインスタンスを返すプロシージャ[!INCLUDE[vbprvb](../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)]式とそれ以外の場合、その他の操作をバイパスします。  
  
 詳細と例では、次を参照してください。 [Shared](../../../visual-basic/language-reference/modifiers/shared.md)します。  
  
 既定では、このメッセージは警告です。 警告を非表示や警告をエラーとして扱う方法の詳細については、次を参照してください。 [Visual Basic での警告の構成](https://docs.microsoft.com/visualstudio/ide/configuring-warnings-in-visual-basic)します。  
  
 **エラー ID:** BC42025  
  
## <a name="to-correct-this-error"></a>このエラーを解決するには  
  
-   クラスまたは定義する構造体の名前を使用して、`Shared`メンバーへのアクセスに、次の例に示すようにします。  
  
```vb  
Public Class testClass  
    Public Shared Sub sayHello()  
        MsgBox("Hello")  
    End Sub  
End Class  
  
Module testModule  
    Public Sub Main()  
        ' Access a shared method through an instance variable.  
        ' This generates a warning.  
        Dim tc As New testClass  
        tc.sayHello()  
  
        ' Access a shared method by using the class name.  
        ' This does not generate a warning.  
        testClass.sayHello()  
    End Sub  
End Module  
```  
  
> [!NOTE]
>  スコープの影響に関する警告は、2 つのプログラミング要素は、同じ名前を付けるときにあります。 使用してインスタンスを宣言する場合、前の例で`Dim testClass as testClass = Nothing`、コンパイラは、処理の呼び出し`testClass.sayHello()`クラス名、および警告は表示されず、メソッドのアクセスが発生するとします。  
  
## <a name="see-also"></a>関連項目  
 [共有](../../../visual-basic/language-reference/modifiers/shared.md)   
 [Visual Basic におけるスコープ](../../../visual-basic/programming-guide/language-features/declared-elements/scope.md)
