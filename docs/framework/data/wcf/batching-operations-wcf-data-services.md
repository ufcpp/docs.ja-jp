---
title: "バッチ処理 (WCF Data Services) | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-oob"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "WCF Data Services, クライアント ライブラリ"
ms.assetid: 962a49d1-cc11-4b96-bc7d-071dd6607d6c
caps.latest.revision: 3
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 3
---
# バッチ処理 (WCF Data Services)
[!INCLUDE[ssODataFull](../../../../includes/ssodatafull-md.md)] は、[!INCLUDE[ssODataShort](../../../../includes/ssodatashort-md.md)] ベースのサービスに対する要求のバッチ処理をサポートしています。  詳細については、「[OData: バッチ処理](http://go.microsoft.com/fwlink/?LinkId=186075)」を参照してください。[!INCLUDE[ssAstoria](../../../../includes/ssastoria-md.md)] では、<xref:System.Data.Services.Client.DataServiceContext> を使用する各操作 \(クエリの実行や変更の保存など\) は、データ サービスに個別に送信される要求になります。  操作セットの論理スコープを維持するために、操作バッチを明示的に定義する必要があります。  この定義により、バッチ内のすべての操作が 1 つの HTTP 要求でデータ サービスに送信され、サーバーが操作を自動的に処理できるようになり、データ サービスへのラウンド トリップの数が減少します。  
  
## クエリ操作のバッチ処理  
 複数のクエリを 1 つのバッチで実行するには、バッチ内の各クエリを <xref:System.Data.Services.Client.DataServiceRequest%601> クラスの個別のインスタンスとして作成する必要があります。  この方法でクエリ要求を作成すると、クエリ自身が URI として定義されます。このクエリは、リソースのアドレス指定のルールに従います。  詳細については、「[データ サービス リソースへのアクセス](../../../../docs/framework/data/wcf/accessing-data-service-resources-wcf-data-services.md)」を参照してください。  バッチ化されたクエリ要求は、クエリ要求オブジェクトを含む <xref:System.Data.Services.Client.DataServiceContext.ExecuteBatch%2A> メソッドが呼び出されたときにデータ サービスに送信されます。  このメソッドは、<xref:System.Data.Services.Client.DataServiceResponse> オブジェクトを返します。このオブジェクトは、バッチ内の個々の要求への応答を表す <xref:System.Data.Services.Client.QueryOperationResponse%601> オブジェクトのコレクションです。個々のオブジェクトには、クエリによって返されるオブジェクトのコレクションまたはエラー情報が含まれます。  バッチ内のいずれかのクエリ操作が失敗した場合、<xref:System.Data.Services.Client.QueryOperationResponse%601> オブジェクトで失敗した操作のエラー情報が返され、残りの操作は引き続き実行されます。  詳細については、「[方法: クエリをバッチで実行する](../../../../docs/framework/data/wcf/how-to-execute-queries-in-a-batch-wcf-data-services.md)」を参照してください。  
  
 バッチ クエリは、非同期で実行することもできます。  詳細については、「[非同期操作](../../../../docs/framework/data/wcf/asynchronous-operations-wcf-data-services.md)」を参照してください。  
  
## 変更の保存操作のバッチ処理  
 <xref:System.Data.Services.Client.DataServiceContext.SaveChanges%2A> メソッドを呼び出すとき、コンテキストが追跡するすべての変更が REST ベースの操作に変換され、[!INCLUDE[ssODataShort](../../../../includes/ssodatashort-md.md)] サービスに対する要求として送信されます。  既定では、これらの変更は 1 つの要求メッセージで送信されません。  すべての変更を 1 つの要求で送信するには、<xref:System.Data.Services.Client.DataServiceContext.SaveChanges%28System.Data.Services.Client.SaveChangesOptions%29> メソッドを呼び出して、メソッドに指定する <xref:System.Data.Services.Client.SaveChangesOptions> 列挙体に <xref:System.Data.Services.Client.SaveChangesOptions> の値を含める必要があります。  
  
 バッチ処理された変更を非同期で保存することもできます。  詳細については、「[非同期操作](../../../../docs/framework/data/wcf/asynchronous-operations-wcf-data-services.md)」を参照してください。  
  
## 参照  
 [WCF Data Services クライアント ライブラリ](../../../../docs/framework/data/wcf/wcf-data-services-client-library.md)