---
title: "is (C# リファレンス)"
keywords: "is キーワード (C#), is (C#)"
ms.date: 02/17/2017
ms.prod: .net
ms.technology:
- devlang-csharp
ms.topic: article
f1_keywords:
- is_CSharpKeyword
- is
helpviewer_keywords:
- is keyword [C#]
ms.assetid: bc62316a-d41f-4f90-8300-c6f4f0556e43
caps.latest.revision: 
author: BillWagner
ms.author: wiwagn
ms.openlocfilehash: 9f0242439caa21268a6c314409f41587890c4126
ms.sourcegitcommit: 4f3fef493080a43e70e951223894768d36ce430a
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/21/2017
---
# <a name="is-c-reference"></a>is (C# リファレンス) #

オブジェクトに指定された型との互換性があるかどうかを確認するか、(C# 7 以降では) パターンとの比較によって式をテストします。

## <a name="testing-for-type-compatibility"></a>型の互換性に関するテスト ##

`is` キーワードを使用すると、実行時に型の互換性が評価されます。 これにより、オブジェクト インスタンスや式の結果を指定された型に変換できるかどうかが判定されます。 構文は次のとおりです

```csharp
   expr is type
```

ここで *expr* は何らかの型のインスタンスに評価される式、*type* は *expr* の結果が変換される型の名前です。 `is` ステートメントでは、*expr* が null 以外の値で、式の評価によって得られるオブジェクトが *type* に変換できる場合に `true`、それ以外の場合に `false` が返されます。

たとえば、次のコードでは `obj` を `Person` 型のインスタンスにキャストできるかどうかが判定されます。

[!code-csharp[is#1](../../../../samples/snippets/csharp/language-reference/keywords/is/is1.cs#1)]

`is` ステートメントは以下の場合に true となります。

- *expr* が *type* と同じ型のインスタンスである。

- *expr* が *type* から派生した型のインスタンスである。 つまり、*expr* の結果を *type* のインスタンスにアップキャストできる。

- *expr* のコンパイル時の型が *type* の基底クラスであり、*expr* の実行時の型が *type* または *type* から派生した型である。 変数の "*コンパイル時の型*" とは、その変数の宣言で定義されている型です。 変数の "*実行時の型*" とは、その変数に代入されているインスタンスの型です。

- *expr* が、*type* インターフェイスを実装する型のインスタンスである。

次の例は、変換ごとの `is` 式の評価が `true` となることを示しています。

[!code-csharp[is#3](../../../../samples/snippets/csharp/language-reference/keywords/is/is3.cs#3)]

式が常に `true` または `false` のいずれかになることが判明している場合は、`is` キーワードによってコンパイル時に警告が生成されます。 参照変換、ボックス変換、アンボックス変換のみが考慮され、ユーザー定義の変換や型の [implicit](implicit.md) および [explicit](explicit.md) 演算子によって定義された変換は無視されます。 次の例では、コンパイル時に変換結果が判明しているため、警告が生成されます。 `int` から `long` および `double` への変換の `is` 式では、変換が [implicit](implicit.md) 演算子によって処理されるため、false が返される点に注意してください。

[!code-csharp[is#2](../../../../samples/snippets/csharp/language-reference/keywords/is/is2.cs#2)]

`expr` には、匿名メソッドとラムダ式を除き、値を返すどのような式でも指定できます。 次の例では、`is` を使用してメソッド呼び出しの戻り値を評価しています。   
[!code-csharp[is#4](../../../../samples/snippets/csharp/language-reference/keywords/is/is4.cs#4)]

C# 7 以降では、[型パターン](#type)によるパターン マッチングを使用することで、`is` ステートメントを用いたより簡潔なコードを記述できます。

## <a name="pattern-matching-with-is"></a>`is` を使用したパターン マッチング ##

C# 7 以降では、`is` および [switch](../../../csharp/language-reference/keywords/switch.md) ステートメントでパターン マッチングがサポートされています。 `is` キーワードでは、以下のパターンがサポートされています。

- [型パターン](#type): 式を指定された型に変換できるかどうかをテストし、変換できる場合はその型の変数にキャストします。

- [定数パターン](#constant): 式の評価が指定された定数値になるかどうかをテストします。

- [var パターン](#var): 照合が常に成功し、式の値が新しいローカル変数にバインドされます。 

### <a name="type" />型パターン</a>

型パターンを使用してパターン マッチングを実行すると、式を指定された型に変換できるかどうかが `is` によってテストされ、変換できる場合はその型の変数にキャストされます。 `is` ステートメントのわかりやすい拡張機能であり、型の評価および変換を簡潔に記述できます。 `is` 型パターンの一般的な形式は次のとおりです。

```csharp
   expr is type varname 
```

ここで *expr* は何らかの型のインスタンスに評価される式、*type* は *expr* の結果が変換される型の名前、*varname* は `is` のテスト結果が `true` である場合に *expr* の結果が変換されるオブジェクトをそれぞれ表しています。 

以下のいずれかの条件が true である場合に `is` 式は `true` となります。

- *expr* が *type* と同じ型のインスタンスである。

- *expr* が *type* から派生した型のインスタンスである。 つまり、*expr* の結果を *type* のインスタンスにアップキャストできる。

- *expr* のコンパイル時の型が *type* の基底クラスであり、*expr* の実行時の型が *type* または *type* から派生した型である。 変数の "*コンパイル時の型*" とは、その変数の宣言で定義されている型です。 変数の "*実行時の型*" とは、その変数に代入されているインスタンスの型です。

- *expr* が、*type* インターフェイスを実装する型のインスタンスである。

*exp* が `true` で `is` が `if` ステートメントと共に使用されている場合は *varname* への代入が行われ、そのローカル スコープは `if` ステートメントを含むブロック内に限定されます。

次の例では、`is` 型のパターンを使用して、型 <xref:System.IComparable.CompareTo(System.Object)?displayProperty=nameWithType> のメソッドの実装を提供します。

[!code-csharp[is#5](../../../../samples/snippets/csharp/language-reference/keywords/is/is-type-pattern5.cs#5)]

パターン マッチングを使用しない場合、このコードは次のように記述できます。 型パターン マッチングを使用することにより、変換結果が `null` であるかどうかをテストする必要がなくなるため、コードがよりコンパクトで読みやすくなります。  

[!code-csharp[is#6](../../../../samples/snippets/csharp/language-reference/keywords/is/is-type-pattern6.cs#6)]

`is` 型パターンを使用すると、値の型の種類を判定する場合によりコンパクトなコードを記述できます。 次の例では、`is` 型パターンを使用し、オブジェクトが `Person` インスタンスか `Dog` インスタンスかを判定した後に適切なプロパティの値を表示しています。 

[!code-csharp[is#9](../../../../samples/snippets/csharp/language-reference/keywords/is/is-type-pattern9.cs#9)]

パターン マッチングを使用せずにこれと同等のコードを記述する場合は、明示的なキャストを含む代入処理を個別に行う必要があります。

[!code-csharp[is#10](../../../../samples/snippets/csharp/language-reference/keywords/is/is-type-pattern10.cs#10)]

### <a name="a-nameconstant--constant-pattern"></a><a name="constant" />定数パターン ###

定数パターンを使用してパターン マッチングを実行すると、式が指定された定数と等しいかどうかが `is` によってテストされます。 C# 6 以前のバージョンでの定数パターンは [switch](switch.md) ステートメントでサポートされています。 C# 7 以降では、`is` ステートメントでもサポートされています。 構文は次のとおりです。

```csharp
   expr is constant
```

ここで *expr* は評価する式、*constant* はテストする値を表しています。 *constant* には以下のいずれかの定数式を指定できます。 

- リテラル値。

- 宣言された `const` 変数の名前。

- 列挙定数。

定数式は以下のように評価されます。

- *expr* と *constant* が整数型の場合、式から `true` が返されるかどうか (つまり、`expr == constant` であるかどうか) が C# の等値演算子によって判定されます。

- それ以外の場合、式の値は静的 [Object.Equals(expr, constant)](xref:System.Object.Equals(System.Object,System.Object)) メソッドの呼び出しによって判定されます。  

次の例では、型パターンと定数パターンを組み合わせてオブジェクトが `Dice` インスタンスであるかどうかをテストし、そうである場合はサイコロ振り操作の値が 6 であるかどうかをテストします。

[!code-csharp[is#7](../../../../samples/snippets/csharp/language-reference/keywords/is/is-const-pattern7.cs#7)]
 
### <a name="var" /> var パターン</a>

var パターンによるパターン マッチは常に成功します。 構文は次のとおりです

```csharp 
   expr is var varname
```

ここで *expr* の値は常に *varname* というローカル変数に代入されます。 *varname* は *expr* と同じ型の静的変数です。 次の例では、var パターンを使用して式を `obj` という変数に代入しています。 その後、`obj` の値と型が表示されます。

[!code-csharp[is#8](../../../../samples/snippets/csharp/language-reference/keywords/is/is-var-pattern8.cs#8)]

*expr* が `null` である場合も `is` 式は true となり、`null` が *varname* に代入される点に注意してください。 

# <a name="c-language-specification"></a>C# 言語仕様
  
[!INCLUDE[CSharplangspec](~/includes/csharplangspec-md.md)]  
  
## <a name="see-also"></a>関連項目  
 [C# リファレンス](../../../csharp/language-reference/index.md)  
 [C# のキーワード](../../../csharp/language-reference/keywords/index.md)  
 [typeof](../../../csharp/language-reference/keywords/typeof.md)  
 [as](../../../csharp/language-reference/keywords/as.md)  
 [演算子のキーワード](../../../csharp/language-reference/keywords/operator-keywords.md)
