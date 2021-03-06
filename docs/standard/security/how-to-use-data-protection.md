---
title: "方法 : データ保護を使用する | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-standard"
ms.tgt_pltfrm: ""
ms.topic: "article"
dev_langs: 
  - "VB"
  - "CSharp"
  - "C++"
  - "jsharp"
helpviewer_keywords: 
  - "暗号化 [.NET Framework], データ保護 API"
  - "データ [.NET Framework], 復号化"
  - "データ [.NET Framework], 暗号化"
  - "データ保護 API [.NET Framework]"
  - "復号化"
  - "DPAPI"
  - "暗号化 [.NET Framework], データ保護 API"
  - "ProtectedData クラス, ProtectedData クラスの概要"
  - "ProtectedMemory クラス, ProtectedMemory クラスの概要"
ms.assetid: 606698b0-cb1a-42ca-beeb-0bea34205d20
caps.latest.revision: 11
author: "mairaw"
ms.author: "mairaw"
manager: "wpickett"
caps.handback.revision: 11
---
# 方法 : データ保護を使用する
.NET Framework では、データ保護 API \(DPAPI\) へのアクセスを提供しています。DPAPI を使用すると、現在のユーザー アカウントまたはコンピューターからの情報を使用してデータを暗号化できます。  DPAPI を使用すると、暗号化キーを明示的に生成および格納するという困難な問題を軽減できます。  
  
 <xref:System.Security.Cryptography.ProtectedMemory> クラスを使用すると、メモリ内のバイト配列を暗号化できます。  この機能は、Microsoft Windows XP 以降のオペレーティング システムで使用できます。  現在のプロセスによって暗号化されるメモリは、現在のプロセスのみ、すべてのプロセス、または同じユーザーのコンテキストによって復号化されることを指定できます。  <xref:System.Security.Cryptography.ProtectedMemory> オプションの詳しい説明については、「<xref:System.Security.Cryptography.MemoryProtectionScope> 列挙型」を参照してください。  
  
 バイト配列のコピーを暗号化するには、<xref:System.Security.Cryptography.ProtectedData> クラスを使用します。  この機能は、Microsoft Windows 2000 以降のオペレーティング システムで使用できます。  現在のユーザー アカウントによって暗号化されたデータは、同じユーザー アカウントによってのみ復号化できることを指定できます。あるいは、現在のユーザー アカウントによって暗号化されたデータは、コンピューター上の任意のアカウントによって復号化できることを指定できます。  <xref:System.Security.Cryptography.ProtectedData> オプションの詳しい説明については、「<xref:System.Security.Cryptography.DataProtectionScope> 列挙型」を参照してください。  
  
### データの保護を使用してメモリ内のデータを暗号化するには  
  
1.  暗号化するバイト配列、エントロピ、およびメモリ保護スコープを渡す際に、静的な <xref:System.Security.Cryptography.ProtectedMemory.Protect%2A> メソッドを呼び出します。  
  
### データ保護を使用してメモリ内のデータを復号化するには  
  
1.  復号化するバイト配列およびメモリ保護スコープを渡す際に、静的な <xref:System.Security.Cryptography.ProtectedMemory.Unprotect%2A> メソッドを呼び出します。  
  
### データ保護を使用してファイルやストリームのデータを暗号化するには  
  
1.  ランダム エントロピを作成します。  
  
2.  暗号化するバイト配列、エントロピ、およびデータ保護スコープを渡す際に、静的な <xref:System.Security.Cryptography.ProtectedData.Protect%2A> メソッドを呼び出します。  
  
3.  ファイルまたはストリームに暗号化されたデータを書き込みます。  
  
### データ保護を使用してファイルやストリームからデータを復号化するには  
  
1.  ファイルまたはストリームから暗号化されたデータを読み取ります。  
  
2.  復号化するバイト配列およびデータ保護スコープを渡す際に、静的な <xref:System.Security.Cryptography.ProtectedData.Unprotect%2A> メソッドを呼び出します。  
  
## 使用例  
 次のコード例は、暗号化と復号化の 2 つの形式を示しています。  最初に、コード例では、メモリ内のバイト配列を暗号化してから復号化します。  次に、コード例では、バイト配列のコピーを暗号化し、ファイルに保存して、そのファイルからデータを読み込み、その後データを復号化しています。  例では、元のデータ、暗号化されたデータ、および復号化されたデータが表示されます。  
  
 [!code-csharp[DPAPI-HowTO#1](../../../samples/snippets/csharp/VS_Snippets_CLR/DPAPI-HowTO/cs/sample.cs#1)]
 [!code-vb[DPAPI-HowTO#1](../../../samples/snippets/visualbasic/VS_Snippets_CLR/DPAPI-HowTO/vb/sample.vb#1)]  
  
## コードのコンパイル  
  
-   `System.Security.dll` への参照を含めます。  
  
-   <xref:System>、<xref:System.IO>、<xref:System.Security.Cryptography>、および <xref:System.Text> 名前空間を含めます。  
  
## 参照  
 <xref:System.Security.Cryptography.ProtectedMemory>   
 <xref:System.Security.Cryptography.ProtectedData>