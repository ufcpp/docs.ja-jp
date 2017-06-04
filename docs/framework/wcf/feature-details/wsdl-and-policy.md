---
title: "WSDL とポリシー | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: cea87440-3519-4640-8494-b8a2b0e88c84
caps.latest.revision: 10
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 10
---
# WSDL とポリシー
ここでは、[!INCLUDE[indigo1](../../../../includes/indigo1-md.md)] WSDL 1.1、WS\-Policy、および WS\-PolicyAttachment の実装の詳細、および [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] によって導入される追加の WS\-Policy アサーションと WSDL 1.1 拡張について説明します。  
  
 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] では、ここで説明する制約と説明に基づいて、W3C に提出された WS\-Policy 仕様と WS\-PolicyAttachment 仕様を実装しています。  
  
 このドキュメントでは、次の表に示すプレフィックスと名前空間を使用します。  
  
|プレフィックス|Namespace|  
|-------------|---------------|  
|wsp \(WS\-Policy 1.2\)|http:\/\/schemas.xmlsoap.org\/ws\/2004\/09\/policy|  
|wsp \(WS\-Policy 1.5\)|http:\/\/www.w3.org\/ns\/ws\-policy|  
|http|http:\/\/schemas.microsoft.com\/ws\/06\/2004\/policy\/http|  
|msmq|http:\/\/schemas.microsoft.com\/ws\/06\/2004\/mspolicy\/msmq|  
|msf|http:\/\/schemas.microsoft.com\/ws\/2006\/05\/framing\/policy|  
|mssp|http:\/\/schemas.microsoft.com\/ws\/2005\/07\/securitypolicy|  
|msc|http:\/\/schemas.microsoft.com\/ws\/2005\/12\/wsdl\/contract|  
|cdp|http:\/\/schemas.microsoft.com\/net\/2006\/06\/duplex|  
  
## WCF WSDL1.1 の拡張  
 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] では、次の WSDL1.1 拡張を使用して、コントラクト セッションの要件を表します。  
  
 wsdl:portType\/wsdl:operation\/@msc:isInitiating  
 xs:boolean は、この操作が [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] セッションを開始するかどうかを示します。既定値は `false` です。  
  
 wsdl:portType\/wsdl:operation\/@msc:isTerminating  
 xs:boolean は、この操作が [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] セッションを終了するかどうかを示します。既定値は `false` です。  
  
 wsdl:portType\/wsdl:operation\/@msc:usingSession  
 xs:boolean は、このコントラクトでセッションを確立する必要があるかどうかを示します。  
  
### SOAP 1.x HTTP バインディング トランスポートの URI  
 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] では、次の URI を使用して、WSDL 1.1、SOAP 1.1 および 1.2 のバインディング拡張要素に使用するトランスポートを示します。  
  
|Transport|URI|  
|---------------|---------|  
|HTTP|http:\/\/schemas.xmlsoap.org\/soap\/http|  
|TCP|http:\/\/schemas.microsoft.com\/soap\/tcp|  
|MSMQ|http:\/\/schemas.microsoft.com\/soap\/msmq|  
|名前付きパイプ|http:\/\/schemas.microsoft.com\/soap\/named\-pipe|  
  
## WCF で実装されるポリシー アサーション  
 Web サービス仕様 \(WS\-\*\) で導入されたポリシー アサーションとこのドキュメントの他のセクションに記載しているポリシー アサーションに加えて、[!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] では次のポリシー アサーションを実装します。  
  
|ポリシー アサーション|ポリシー サブジェクト|説明|  
|-----------------|-----------------|--------|  
|http:HttpBasicAuthentication|エンドポイント|エンドポイントは、HTTP 基本認証を使用します。|  
|http:HttpDigestAuthentication|エンドポイント|エンドポイントは、HTTP ダイジェスト認証を使用します。|  
|http:HttpNegotiateAuthentication|エンドポイント|エンドポイントは、HTTP ネゴシエート認証を使用します。|  
|http:HttpNtlmAuthentication|エンドポイント|エンドポイントは、HTTP NTLM 認証を使用します。|  
|msf:Streamed|エンドポイント|エンドポイントは、ストリーミングされたメッセージ フレームを使用します。  このアサーションは、TCP、名前付きパイプのようなトランスポートに提供されるメッセージ フレーム プロトコルと共に使用されます。|  
|msf:SslTransportSecurity|エンドポイント|エンドポイントは、トランスポート層セキュリティ \(TLS\) をメッセージ フレームと共に使用します。|  
|msf:WindowsTransportSecurity|エンドポイント|エンドポイントは、Security Provider Negotiation \(SPNEGO\) をメッセージ フレームと共に使用します。|  
|msmq:MsmqBestEffort|エンドポイント|MSMQ はベストエフォート保証を使用します。|  
|msmq:MsmqSession|エンドポイント|MSMQ はセッション保証を使用します。|  
|msmq:MsmqVolatile|エンドポイント|MSMQ は揮発性です。|  
|msmq:Authenticated|エンドポイント|認証が、MSMQ トランスポートと共に使用されます。|  
|msmq:WindowsDomain|エンドポイント|MSMQ は Windows ドメイン認証を使用します。|  
|cdp:CompositeDuplex|エンドポイント|エンドポイントは、メッセージの送受信に 2 つの個別の逆方向トランスポート接続を使用します。|  
|mssp:RsaToken|入れ子|RSA キー トークンのアサーションです。  通常、この要件を満たすのは、保証する署名内でキー情報の一部として直接シリアル化される RSA キーです。|  
|mssp:SslContextToken|入れ子|WS\-Trust を使用するバイナリ TLS ハンドシェイクによって取得される SecurityContextToken の使用を要求します。  入れ子になったアサーションには、sp:RequireDerivedKeys、mssp:MustNotSendCancel、mssp:RequireClientCertificate があります。|  
|mssp:MustNotSendCancel|入れ子|Cancel バインディング \[WS\-Trust、WS\-SC\] を使用するセキュリティ トークン要求 \(RST\) の要求メッセージ \[WS\-Trust\] を特定の SecurityContextToken の発行者に送信しないという要件を指定します。  このアサーションが存在する場合、このような要求メッセージを発行者に送信することはできません。  このアサーションが存在しない場合、このような要求メッセージを発行者に送信できます。|  
|mssp:RequireClientCertificate|入れ子|このオプション要素では、TLSNEGO プロトコルの一部としてクライアント証明書を提供するという要件を指定します。  このアサーションが存在する場合、クライアント証明書を提供する必要があります。  このアサーションが存在しない場合、クライアント証明書を提供しないでください。  このアサーションは、mssp:SslContextToken の外側で使用することはできません。|  
  
## 参照  
 [カスタム WSDL パブリケーション](../../../../docs/framework/wcf/samples/custom-wsdl-publication.md)   
 [方法 : カスタム WSDL をエクスポートする](../../../../docs/framework/wcf/extending/how-to-export-custom-wsdl.md)   
 [方法 : カスタム WSDL をインポートする](../../../../docs/framework/wcf/extending/how-to-import-custom-wsdl.md)