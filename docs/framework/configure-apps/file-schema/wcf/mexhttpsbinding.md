---
title: "&lt;mexHttpsBinding&gt; | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: f2ed3774-78b9-4a15-b79b-655f1ad68b86
caps.latest.revision: 8
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 8
---
# &lt;mexHttpsBinding&gt;
HTTPS 経由の WS\-MetadataExchange \(WS\-MEX\) メッセージ交換に使用されるバインディングの設定を指定します。  
  
## 構文  
  
```  
  
<mexHttpsBinding>  
   <binding   
       closeTimeout="TimeSpan"   
       name="string"   
       openTimeout="TimeSpan"   
       receiveTimeout="TimeSpan"  
       sendTimeout="TimeSpan">  
   </binding>  
</mexHttpsBinding>  
```  
  
## 属性および要素  
 以降のセクションでは、属性、子要素、および親要素について説明します。  
  
### 属性  
  
|属性|説明|  
|--------|--------|  
|`closeTimeout`|クローズ操作が完了するまでの期間を指定する <xref:System.TimeSpan> 値。  この値は必ず <xref:System.TimeSpan.Zero> 以上である必要があります。  既定値は 00:01:00 です。|  
|`name`|バインディングの構成名を格納する文字列です。  この値は、バインディングの ID として使用されるため、一意にする必要があります。  各バインドには、サービスのメタデータでこれをまとめて一意に識別する `name` および `namespace` 属性が含まれています。  また、この名前は、同じ種類のバインディング間で一意です。  [!INCLUDE[netfx40_short](../../../../../includes/netfx40-short-md.md)] 以降では、バインディングおよび動作に名前を付ける必要はありません。  既定の構成、および名前のないバインディングと動作の詳細については、「[簡略化された構成](../../../../../docs/framework/wcf/simplified-configuration.md)」および「[WCF サービスの簡略化された構成](../../../../../docs/framework/wcf/samples/simplified-configuration-for-wcf-services.md)」を参照してください。|  
|`openTimeout`|実行中の操作が完了するまでの時間間隔を指定する <xref:System.TimeSpan> 値です。  この値は必ず <xref:System.TimeSpan.Zero> 以上である必要があります。  既定値は 00:01:00 です。|  
|`receiveTimeout`|受信操作が完了するまでの時間間隔を指定する <xref:System.TimeSpan> 値です。  この値は必ず <xref:System.TimeSpan.Zero> 以上である必要があります。  既定値は 00:10:00 です。|  
|`sendTimeout`|送信操作が完了するまでの時間間隔を指定する <xref:System.TimeSpan> 値です。  この値は必ず <xref:System.TimeSpan.Zero> 以上である必要があります。  既定値は 00:01:00 です。|  
  
### 子要素  
 なし。  
  
### 親要素  
  
|要素|説明|  
|--------|--------|  
|[\<bindings\>](../../../../../docs/framework/configure-apps/file-schema/wcf/bindings.md)|この要素には、標準バインディングおよびカスタム バインディングのコレクションが保持されます。|  
  
## 解説  
 このバインディングは、基本的には証明書を使用してトランスポート レベルのセキュリティをサポートする `WSHttpBinding` バインディングです。  そのようなメタデータ エンドポイントの構成および使用の詳細については、「[方法 : カスタム WS\-Metadata Exchange バインディングを構成する](../../../../../docs/framework/wcf/extending/how-to-configure-a-custom-ws-metadata-exchange-binding.md)」、「[方法: MEX 以外のバインディングを介してメタデータを取得する](../../../../../docs/framework/wcf/extending/how-to-retrieve-metadata-over-a-non-mex-binding.md)」、および「[カスタム セキュア メタデータ エンドポイント](../../../../../docs/framework/wcf/samples/custom-secure-metadata-endpoint.md)」のサンプルを参照してください。  
  
## 参照  
 <xref:System.ServiceModel.Description.MetadataExchangeBindings.CreateMexHttpsBinding%2A>   
 <xref:System.ServiceModel.Configuration.MexHttpsBindingElement>   
 [方法 : 構成ファイルを使用してサービスのメタデータを公開する](../../../../../docs/framework/wcf/feature-details/how-to-publish-metadata-for-a-service-using-a-configuration-file.md)   
 [カスタム バインディングを介したメタデータの公開と取得](../../../../../docs/framework/wcf/extending/publishing-and-retrieving-metadata-over-a-custom-binding.md)   
 [方法 : カスタム WS\-Metadata Exchange バインディングを構成する](../../../../../docs/framework/wcf/extending/how-to-configure-a-custom-ws-metadata-exchange-binding.md)   
 [方法: MEX 以外のバインディングを介してメタデータを取得する](../../../../../docs/framework/wcf/extending/how-to-retrieve-metadata-over-a-non-mex-binding.md)   
 [カスタム セキュア メタデータ エンドポイント](../../../../../docs/framework/wcf/samples/custom-secure-metadata-endpoint.md)   
 [メタデータ](../../../../../docs/framework/wcf/feature-details/metadata.md)   
 [バインディング](../../../../../docs/framework/wcf/bindings.md)   
 [システムが提供するバインディングの構成](../../../../../docs/framework/wcf/feature-details/configuring-system-provided-bindings.md)   
 [Using Bindings to Configure Windows Communication Foundation Services and Clients](http://msdn.microsoft.com/ja-jp/bd8b277b-932f-472f-a42a-b02bb5257dfb)   
 [\<binding\>](../../../../../docs/framework/misc/binding.md)