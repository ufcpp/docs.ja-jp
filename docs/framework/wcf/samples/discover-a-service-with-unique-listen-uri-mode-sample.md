---
title: "一意の ListenUri モードのサンプルを使用したサービスの探索 | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 9a6d35b2-0469-43c8-a0c9-63623e3d2733
caps.latest.revision: 8
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 8
---
# 一意の ListenUri モードのサンプルを使用したサービスの探索
このサンプルでは、<xref:System.ServiceModel.Channels.BindingContext.ListenUriMode%2A> プロパティが <xref:System.ServiceModel.Description.ListenUriMode> に設定されているサービスを探索する方法を示します。<xref:System.ServiceModel.Channels.BindingContext.ListenUriMode%2A> プロパティが <xref:System.ServiceModel.Description.ListenUriMode> に設定されている場合は、ポートを一意に設定するか、GUID を付加することによってパスを一意に設定して、ListenUri を一意にする必要があります。  
  
### サービスの機能  
 TCP エンドポイントの <xref:System.ServiceModel.Channels.BindingContext.ListenUriMode%2A> プロパティは、<xref:System.ServiceModel.Description.ListenUriMode> に設定されます。これにより、<xref:System.ServiceModel.Discovery.UdpDiscoveryEndpoint> エンドポイントを介してサービスを探索できるようになります。  
  
### クライアントの機能  
 このクライアントは、適切な `Via.Uri` を使用してサービスに接続します。この際、<xref:System.ServiceModel.Discovery.DiscoveryClient.Find%2A> メソッドが使用されます。このメソッドから返された <xref:System.ServiceModel.Discovery.FindResponse> は、有効な <xref:System.ServiceModel.Endpoint.ListenUri%2A> を含んでいるかどうか、および `Address.Uri` とは異なるかどうかについて照会されます。適切な情報は `InvokeCalculatorService` メソッドに渡されます。`InvokeCalculatorService` メソッドでは、呼び出し元から <xref:System.ServiceModel.Endpoint.ListenUri%2A> が渡され、適切な `Via.Uri` が設定された `ClientViaBehavior` がクライアントのエンドポイントに追加されます。  
  
##### このサンプルを使用するには  
  
1.  [!INCLUDE[vs_current_long](../../../../includes/vs-current-long-md.md)] で、UniqueListenUriMode.sln を開きます。  
  
2.  ソリューションをビルドするには、Ctrl キーと Shift キーを押しながら B キーを押します。  
  
3.  \[ソリューションの基本ディレクトリ\]\\service\\bin\\debug フォルダーに生成されたサービス アプリケーションを実行します。  
  
4.  \[ソリューションの基本ディレクトリ\]\\Client\\bin\\debug フォルダーに生成されたクライアント アプリケーションを実行します。  
  
     クライアントは実行中のサービスを検索し、サービスのエンドポイントで公開されているメタデータをコンソールに書き込みます。  
  
> [!IMPORTANT]
>  サンプルは、既にコンピューターにインストールされている場合があります。続行する前に、次の \(既定の\) ディレクトリを確認してください。  
>   
>  `<InstallDrive>:\WF_WCF_Samples`  
>   
>  このディレクトリが存在しない場合は、「[.NET Framework 4 向けの Windows Communication Foundation \(WCF\) および Windows Workflow Foundation \(WF\) のサンプル](http://go.microsoft.com/fwlink/?LinkId=150780)」にアクセスして、[!INCLUDE[indigo1](../../../../includes/indigo1-md.md)] および [!INCLUDE[wf1](../../../../includes/wf1-md.md)] のサンプルをすべてダウンロードしてください。このサンプルは、次のディレクトリに格納されます。  
>   
>  `<InstallDrive>:\WF_WCF_Samples\WCF\Basic\Discovery\UniqueListenUriMode`  
  
## 参照