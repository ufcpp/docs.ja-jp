---
title: "const (C# リファレンス) | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.technology: 
  - "devlang-csharp"
ms.topic: "article"
f1_keywords: 
  - "const_CSharpKeyword"
  - "const"
dev_langs: 
  - "CSharp"
helpviewer_keywords: 
  - "const キーワード [C#]"
ms.assetid: 79eb447c-117b-4418-933f-97c50aa472db
caps.latest.revision: 28
author: "BillWagner"
ms.author: "wiwagn"
caps.handback.revision: 28
---
# const (C# リファレンス)
定数フィールドまたはローカル定数を宣言するには、`const` キーワードを使用します。  定数フィールドとローカルは変数でないため、変更できません。  定数には、数字、ブール値、文字列、または null 参照が含まれます。  いずれかの時点で変わることが予想される情報を表すために定数を作成してはなりません。  たとえば、サービスの価格、製品バージョン番号、会社のブランド名などを格納するためには定数フィールドを使用しないでください。  これらの値は時間の経過とともに変更される場合があります。コンパイラは定数を伝達するため、ライブラリでコンパイルされた他のコードを再コンパイルして、変更点を反映することが必要になってしまいます。  [readonly](../../../csharp/language-reference/keywords/readonly.md) キーワードも参照してください。  次に例を示します。  
  
```  
  
      const int x = 0;  
public const double gravitationalConstant = 6.673e-11;  
private const string productName = "Visual C#";  
```  
  
## 解説  
 定数宣言の型は、宣言で導入されるメンバーの型を指定します。  ローカル定数または定数フィールドの初期化子は、ターゲット型に暗黙に変換できる定数式であることが必要です。  
  
 定数式は、コンパイル時にすべて評価されます。  このため、参照型の定数になりうる値は、`string` と null 参照に限られます。  
  
 定数宣言は、複数の定数を宣言できます。たとえば、次のように宣言できます。  
  
```  
public const double x = 1.0, y = 2.0, z = 3.0;  
```  
  
 `static` 修飾子は、定数宣言では使用できません。  
  
 定数は、次に示すように、定数式の一部になることができます。  
  
```  
public const int c1 = 5;  
public const int c2 = c1 + 100;  
```  
  
> [!NOTE]
>  [readonly](../../../csharp/language-reference/keywords/readonly.md) キーワードは、`const` キーワードとは異なります。  `const` フィールドは、フィールドの宣言でしか初期化できません。  `readonly` フィールドは、宣言またはコンストラクターのどちらかで初期化できます。  このため、`readonly` フィールドは、使用するコンストラクターに応じて異なる値を持つことができます。  また、`const` フィールドがコンパイル時定数であるのに対し、`readonly` フィールドは実行時定数として使用できます。たとえば、`public static readonly uint l1 = (uint)DateTime.Now.Ticks;` のように使用します。  
  
## 使用例  
 [!code-cs[csrefKeywordsModifiers#5](../../../csharp/language-reference/keywords/codesnippet/CSharp/const_1.cs)]  
  
## 使用例  
 この例では、定数をローカル変数として使用する方法を示しています。  
  
 [!code-cs[csrefKeywordsModifiers#6](../../../csharp/language-reference/keywords/codesnippet/CSharp/const_2.cs)]  
  
## C\# 言語仕様  
 [!INCLUDE[CSharplangspec](../../../csharp/language-reference/keywords/includes/csharplangspec-md.md)]  
  
## 参照  
 [C\# リファレンス](../../../csharp/language-reference/index.md)   
 [C\# プログラミング ガイド](../../../csharp/programming-guide/index.md)   
 [C\# のキーワード](../../../csharp/language-reference/keywords/index.md)   
 [修飾子](../../../csharp/language-reference/keywords/modifiers.md)   
 [readonly](../../../csharp/language-reference/keywords/readonly.md)