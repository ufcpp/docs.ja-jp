---
title: "基本認証とダイジェスト認証"
ms.custom: 
ms.date: 03/30/2017
ms.prod: .net-framework
ms.reviewer: 
ms.suite: 
ms.tgt_pltfrm: 
ms.topic: article
dev_langs:
- VB
- CSharp
- C++
- jsharp
helpviewer_keywords:
- authentication [.NET Framework], classes
- Basic authentication
- authentication [.NET Framework], basic
- client authentication, basic
- user authentication, basic
- authentication [.NET Framework], digest
- receiving data, authentication
- client authentication, digest
- Internet, authentication
- digest authentication
- sending data, authentication
- network resources, authentication
- user authentication, digest
ms.assetid: 8cce2742-8d52-4643-9dd2-64ddf38aa878
caps.latest.revision: 11
author: mcleblanc
ms.author: markl
manager: markl
ms.translationtype: HT
ms.sourcegitcommit: 306c608dc7f97594ef6f72ae0f5aaba596c936e1
ms.openlocfilehash: 369a473b2e9172abe10d263bb066b253500f9502
ms.contentlocale: ja-jp
ms.lasthandoff: 08/21/2017

---
# <a name="basic-and-digest-authentication"></a>基本認証とダイジェスト認証
基本認証とダイジェスト認証の <xref:System.Net> 実装では、RFC2617 – HTTP 認証: 基本認証とダイジェスト認証 (www.w3.org の World Wide Web コンソーシアム Web サイトで使用可能) に従います。  
  
 基本認証とダイジェスト認証を使用するには、次の例に示すように、アプリケーションはインターネットからデータを要求するために使用される <xref:System.Net.WebRequest> オブジェクトの <xref:System.Net.WebRequest.Credentials%2A> プロパティでユーザー名とパスワードを指定する必要があります。  
  
```vb  
Dim MyURI As String = "http://www.contoso.com/"  
Dim WReq As WebRequest = WebRequest.Create(MyURI)  
WReq.Credentials = New NetworkCredential(UserName, SecurelyStoredPassword)  
```  
  
```csharp  
String MyURI = "http://www.contoso.com/";  
WebRequest WReq = WebRequest.Create(MyURI);  
WReq.Credentials = new NetworkCredential(UserName, SecurelyStoredPassword);  
```  
  
> [!CAUTION]
>  基本認証およびダイジェスト認証で送信されるデータは暗号化されないため、敵対者がデータを見ることができます。 また、基本認証の資格情報 (ユーザー名とパスワード) はクリア テキストで送信されるので、傍受される可能性があります。  
  
## <a name="see-also"></a>関連項目  
 [NTLM 認証および Kerberos 認証](../../../docs/framework/network-programming/ntlm-and-kerberos-authentication.md)   
 [インターネット認証](../../../docs/framework/network-programming/internet-authentication.md)

