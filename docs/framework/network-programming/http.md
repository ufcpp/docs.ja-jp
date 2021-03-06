---
title: HTTP
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
- protocols, HTTP
- sending data, HTTP
- HttpWebResponse class, sending and receiving data
- HTTP
- receiving data, HTTP
- application protocols, HTTP
- Internet, HTTP
- network resources, HTTP
- HTTP, about HTTP
- HttpWebRequest class, sending and receiving data
ms.assetid: 985fe5d8-eb71-4024-b361-41fbdc1618d8
caps.latest.revision: 10
author: mcleblanc
ms.author: markl
manager: markl
ms.translationtype: HT
ms.sourcegitcommit: 306c608dc7f97594ef6f72ae0f5aaba596c936e1
ms.openlocfilehash: 124e383efbe6cf6bb459d013b9689bf5da287cf1
ms.contentlocale: ja-jp
ms.lasthandoff: 08/21/2017

---
# <a name="http"></a>HTTP
.NET Framework は、<xref:System.Net.HttpWebRequest> クラスと <xref:System.Net.HttpWebResponse> クラスを使用して、すべてのインターネット トラフィックの大部分を構成する HTTP プロトコルに対して包括的なサポートを提供します。 <xref:System.Net.WebRequest> と <xref:System.Net.WebResponse> から派生したこれらのクラスは、静的メソッド <xref:System.Net.WebRequest.Create%2A?displayProperty=fullName> が "http" または "https" で始まる URI に遭遇するたびに既定で返されます。 ほとんどの場合、**WebRequest** クラスと **WebResponse** クラスは、要求を行うために必要なすべてを提供しますが、プロパティとして公開されている HTTP 固有の機能にアクセスする必要がある場合は、これらのクラスを **HttpWebRequest** または **HttpWebResponse** に型キャストすることができますです。  
  
 **HttpWebRequest** と **HttpWebResponse** は、標準の HTTP 要求-応答のトランザクションをカプセル化し、一般的な HTTP ヘッダーへのアクセスを提供します。 これらのクラスは、パイプライン処理、チャック内データの送受信、認証、事前認証、暗号化、プロキシのサポート、サーバー証明書の検証、接続の管理を含むほとんどの HTTP 1.1 の機能もサポートします。 カスタム ヘッダー、およびプロパティを介して提供されていないヘッダーを格納し、**Headers** プロパティを介してアクセスすることができます。  
  
 **HttpWebRequest** は、**WebRequest** によって使用される既定のクラスであり、**WebRequest.Create** メソッドに URI を渡す前に登録する必要はありません。  
  
 <xref:System.Net.HttpWebRequest.AllowAutoRedirect%2A> プロパティを **true** (既定) に設定することで自動的に HTTP リダイレクトに従うアプリケーションを作成することができます。 アプリケーションが、要求をリダイレクトし、**HttpWebResponse** の <xref:System.Net.HttpWebResponse.ResponseUri%2A> プロパティに要求に応答した実際の Web リソースが含まれます。 **AllowAutoRedirect** を **false** に設定した場合、アプリケーションは、HTTP プロトコル エラーとしてリダイレクトを処理できる必要があります。  
  
 アプリケーションでは、<xref:System.Net.WebException.Status%2A> を <xref:System.Net.WebExceptionStatus> に設定し、<xref:System.Net.WebException> をキャッチすることによって HTTP プロトコル エラーを受信します。 <xref:System.Net.WebException.Response%2A> プロパティは、サーバーによって送信された **WebResponse** を含み、実際の HTTP エラーがに発生したことを示します。  
  
## <a name="see-also"></a>関連項目  
 [プロキシを介したインターネットへのアクセス](../../../docs/framework/network-programming/accessing-the-internet-through-a-proxy.md)   
 [アプリケーション プロトコルの使用](../../../docs/framework/network-programming/using-application-protocols.md)   
 [方法: HTTP 固有のプロパティにアクセスする](../../../docs/framework/network-programming/how-to-access-http-specific-properties.md)

