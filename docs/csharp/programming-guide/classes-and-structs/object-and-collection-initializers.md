---
title: "オブジェクト初期化子とコレクション初期化子 (C# プログラミング ガイド)"
ms.date: 2015-07-20
ms.prod: .net
ms.technology:
- devlang-csharp
ms.topic: article
dev_langs:
- CSharp
helpviewer_keywords:
- object initializers [C#]
- collection initializers [C#]
ms.assetid: c58f3db5-d7d4-4651-bd2d-5a3a97357f61
caps.latest.revision: 27
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
ms.openlocfilehash: c4144f383d539129b4e03d5cad262e5a7b9e6b34
ms.contentlocale: ja-jp
ms.lasthandoff: 07/28/2017

---
# <a name="object-and-collection-initializers-c-programming-guide"></a>オブジェクト初期化子とコレクション初期化子 (C# プログラミング ガイド)
オブジェクト初期化子を使用すると、オブジェクトの作成時にアクセスできるフィールドまたはプロパティに、コンストラクターを呼び出して代入ステートメントを使用しなくても、値を割り当てることができます。 オブジェクト初期化子の構文では、コンストラクターの引数を指定することも、引数 (およびかっこ構文) を省略することもできます。  以下の例では、名前付きの型である `Cat` でオブジェクト初期化子を使用する方法と、既定のコンストラクターを呼び出す方法を示します。 `Cat` クラス内で自動実装プロパティが使用されています。 詳細については、「[自動実装プロパティ](../../../csharp/programming-guide/classes-and-structs/auto-implemented-properties.md)」を参照してください。  
  
 [!code-cs[csProgGuideLINQ#39](../../../csharp/programming-guide/arrays/codesnippet/CSharp/object-and-collection-initializers_1.cs)]  
  
 [!code-cs[csProgGuideLINQ#45](../../../csharp/programming-guide/arrays/codesnippet/CSharp/object-and-collection-initializers_2.cs)]  
  
## <a name="object-initializers-with-anonymous-types"></a>オブジェクト初期化子と匿名型  
 オブジェクト初期化子は、どのような場合にも使うことができますが、[!INCLUDE[vbteclinq](~/includes/vbteclinq-md.md)] クエリ式で使うと特に有用です。 クエリ式では、次の宣言に示すように、オブジェクト初期化子を使うことによってのみ初期化できる[匿名型](../../../csharp/programming-guide/classes-and-structs/anonymous-types.md)が頻繁に使われます。  
  
```csharp
var pet = new { Age = 10, Name = "Fluffy" };  
```  
  
 匿名型を使うと、[!INCLUDE[vbteclinq](~/includes/vbteclinq-md.md)] クエリ式の `select` 句によって元のシーケンスのオブジェクトを値と形状が元とは異なるオブジェクトに変換できます。 この方法は、シーケンス内の各オブジェクトの情報の一部のみを保存する場合に便利です。 次の例は、製品オブジェクト (`p`) に多くのフィールドおよびメソッドが含まれており、製品名および単価を含むオブジェクトのシーケンスを作成することにのみ関心があることを想定しています。  
  
 [!code-cs[csProgGuideLINQ#40](../../../csharp/programming-guide/arrays/codesnippet/CSharp/object-and-collection-initializers_3.cs)]  
  
 このクエリが実行されると、`productInfos` 変数には、次の例に示す `foreach` ステートメントでアクセスできるオブジェクトのシーケンスが格納されます。  
  
```csharp
foreach(var p in productInfos){...}  
```  
  
 作成される匿名型内の各オブジェクトには、2 つのパブリック プロパティがあります。これらのプロパティには、元のオブジェクトのプロパティまたはフィールドと同じ名前が付けられます。 匿名型を作成するときにフィールドの名前を変更することもできます。次の例では、フィールド `UnitPrice` の名前が `Price` に変更されます。  
  
```csharp
select new {p.ProductName, Price = p.UnitPrice};  
```  
  
## <a name="object-initializers-with-nullable-types"></a>オブジェクト初期化子と Null 許容型  
 オブジェクト初期化子を null 許容構造体と共に使用すると、コンパイル時にエラーになります。  
  
## <a name="collection-initializers"></a>コレクション初期化子  
 コレクション初期化子を使うと、<xref:System.Collections.IEnumerable> を実装するコレクション型を初期化するときに 1 つ以上の要素の初期化子を指定でき、適切なシグネチャの `Add` をインスタンス メソッドまたは拡張メソッドとして使用できます。 要素の初期化子は、単純な値、式またはオブジェクト初期化子です。 コレクション初期化子を使用すると、ソース コード内でクラスの `Add` メソッドの呼び出しを複数回指定する必要がなくなります。コンパイラによって呼び出しが追加されるためです。  
  
 2 つの単純なコレクション初期化子を次の例に示します。  
  
```csharp
List<int> digits = new List<int> { 0, 1, 2, 3, 4, 5, 6, 7, 8, 9 };  
List<int> digits2 = new List<int> { 0 + 1, 12 % 3, MakeInt() };  
```  
  
 次のコレクション初期化子は、前の例で定義されている `Cat` クラスのオブジェクトをオブジェクト初期化子を使用して初期化します。 個々のオブジェクト初期化子は、かっこで囲まれ、コンマで区切られています。  
  
 [!code-cs[csProgGuideLINQ#41](../../../csharp/programming-guide/arrays/codesnippet/CSharp/object-and-collection-initializers_4.cs)]  
  
 コレクションの `Add` メソッドで許容されている場合、コレクション初期化子の要素として [null](../../../csharp/language-reference/keywords/null.md) を指定できます。  
  
 [!code-cs[csProgGuideLINQ#42](../../../csharp/programming-guide/arrays/codesnippet/CSharp/object-and-collection-initializers_5.cs)]  
  
 コレクションがインデックス作成をサポートしている場合は、インデックス付きの要素を指定することができます。  
  
```csharp
var numbers = new Dictionary<int, string> {   
    [7] = "seven",   
    [9] = "nine",   
    [13] = "thirteen"   
};  
```  
  
## <a name="example"></a>例  
 [!code-cs[csProgGuideLINQ#46](../../../csharp/programming-guide/arrays/codesnippet/CSharp/object-and-collection-initializers_6.cs)]  
  
## <a name="see-also"></a>関連項目  
 [C# プログラミング ガイド](../../../csharp/programming-guide/index.md)   
 [LINQ クエリ式](../../../csharp/programming-guide/linq-query-expressions/index.md)   
 [匿名型](../../../csharp/programming-guide/classes-and-structs/anonymous-types.md)

