---
title: "方法: HTTP 固有のプロパティにアクセスする"
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
ms.assetid: f8848c7e-f5c5-4d42-b86d-9951ff8f4146
caps.latest.revision: 8
author: mcleblanc
ms.author: markl
manager: markl
ms.translationtype: HT
ms.sourcegitcommit: 306c608dc7f97594ef6f72ae0f5aaba596c936e1
ms.openlocfilehash: 6a0c5a2c3a159e4d10da03a584b29e4b77720534
ms.contentlocale: ja-jp
ms.lasthandoff: 08/21/2017

---
# <a name="how-to-access-http-specific-properties"></a>方法: HTTP 固有のプロパティにアクセスする
このサンプルでは、HTTP の **Keep-alive** 動作を無効にして、Web サーバーからプロトコル バージョン番号を取得する方法を示します。  
  
## <a name="example"></a>例  
  
```vb  
Dim HttpWReq As HttpWebRequest= _  
    CType(WebRequest.Create("http://www.contoso.com"), HttpWebRequest)  
' Turn off connection keep-alives.  
HttpWReq.KeepAlive = False  
  
Dim HttpWResp As HttpWebResponse = _  
    CType(HttpWReq.GetResponse(), HttpWebResponse)  
  
' Get the HTTP protocol version number returned by the server.  
Dim ver As String = HttpWResp.ProtocolVersion.ToString()  
HttpWResp.Close()  
```  
  
```csharp  
HttpWebRequest HttpWReq =   
    (HttpWebRequest)WebRequest.Create("http://www.contoso.com");  
// Turn off connection keep-alives.  
HttpWReq.KeepAlive = false;  
  
HttpWebResponse HttpWResp = (HttpWebResponse)HttpWReq.GetResponse();  
  
// Get the HTTP protocol version number returned by the server.  
String ver = HttpWResp.ProtocolVersion.ToString();  
HttpWResp.Close();  
```  
  
## <a name="compiling-the-code"></a>コードのコンパイル  
 この例で必要な要素は次のとおりです。  
  
-   **System.Net** 名前空間の参照。  
  
## <a name="see-also"></a>関連項目  
 [プロキシを介したインターネットへのアクセス](../../../docs/framework/network-programming/accessing-the-internet-through-a-proxy.md)   
 [アプリケーション プロトコルの使用](../../../docs/framework/network-programming/using-application-protocols.md)   
 [HTTP](../../../docs/framework/network-programming/http.md)

