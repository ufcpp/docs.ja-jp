---
title: "方法 : ASP.NET AJAX エンドポイントのために HTTP POST または HTTP GET を選択する | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: b47de82a-4c92-4af6-bceb-a5cb8bb8ede9
caps.latest.revision: 17
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 17
---
# 方法 : ASP.NET AJAX エンドポイントのために HTTP POST または HTTP GET を選択する
[!INCLUDE[indigo1](../../../../includes/indigo1-md.md)] では、クライアント Web サイトの JavaScript から呼び出される ASP.NET AJAX 対応のエンドポイントを公開するサービスを作成できます。  このようなサービスを構築するための基本的な手順については、「[方法 : 構成を使用して ASP.NET AJAX エンドポイントを追加する](../../../../docs/framework/wcf/feature-details/how-to-use-configuration-to-add-an-aspnet-ajax-endpoint.md)」および「[方法 : 構成を使用せずに ASP.NET AJAX エンドポイントを追加する](../../../../docs/framework/wcf/feature-details/how-to-add-an-aspnet-ajax-endpoint-without-using-configuration.md)」を参照してください。  
  
 ASP.NET AJAX では、HTTP POST 動詞および HTTP GET 動詞を使用する操作をサポートしており、HTTP POST が既定となっています。  副作用がなく、返されるデータがほとんど、またはまったく変更されない操作を作成する場合は、代わりに HTTP GET を使用します。  GET 操作の結果はキャッシュされます。つまり、同じ操作についての複数の呼び出し結果がサービスに対する 1 回だけの要求で済むことになります。  このキャッシュ動作は、[!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] によってではなく、任意のレベル \(ユーザーのブラウザーやプロキシ サーバー、その他のレベル\) で実行できます。キャッシュはサービス パフォーマンスの向上が望まれる場合には有効ですが、データの変更が頻繁であったり、操作によって何かのアクションが実行される場合は適していません。  
  
 たとえば、ユーザーの音楽ライブラリを管理するサービスをデザインする場合、アルバムのタイトルに基づいてアーティストを検索する操作では GET の使用は役に立ちますが、ユーザーの個人コレクションにアルバムを追加する操作では POST を使用する必要があります。  
  
 キャッシュの有効期間を制御するには、<xref:System.ServiceModel.Web.OutgoingWebResponseContext> 型を使用します。  たとえば、1 時間ごとに更新される天気予報を返すサービスをデザインする場合、GET を使用することが考えられますが、サービスを使用するユーザーが古いデータにアクセスすることを防止するために、キャッシュの有効期間を 1 時間以内に制限します。  
  
 Script Manager コントロールを使用する ASP.NET AJAX ページからサービスを使用する場合は、Script Manager のメカニズムにより適切な要求の種類が発行されることが保証されているため、操作で GET と POST のどちらを使用しても違いはありません。  
  
 HTTP GET 操作では、複合型データ コントラクト型も含めて、POST 操作でサポートされるすべての入力パラメーターを使用できます。  ただし、多くの場合、キャッシュの効率が低下するため、多数のパラメーター、または複雑すぎるパラメーターを GET 操作で使用しないことをお勧めします。  
  
 このトピックでは、<xref:System.ServiceModel.Web.WebGetAttribute> または <xref:System.ServiceModel.Web.WebInvokeAttribute> 属性を追加することで、サービス コントラクトに適切な操作を GET と POST から選択する方法について説明します。  サービスの実行に必要な他の手順 \(サービスの実装、構成、およびホスト\) は、[!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] の ASP.NET AJAX サービスで使用される手順と同様になります。  
  
 <xref:System.ServiceModel.Web.WebGetAttribute> でマークされた操作では、常に GET 要求が使用されます。  <xref:System.ServiceModel.Web.WebInvokeAttribute> でマークされた操作と、これらの 2 つの属性のどちらでもマークされていない操作では、POST 要求が使用されます。  <xref:System.ServiceModel.Web.WebInvokeAttribute> は、<xref:System.ServiceModel.Web.WebInvokeAttribute.Method%2A> プロパティを介して、GET と POST 以外の HTTP 動詞 \(PUT や DELETE など\) の使用を許可します。  ただし、これらの動詞は ASP.NET AJAX ではサポートされていません。  Script Manager コントロールを使用して ASP.NET ページからサービスを使用する場合は、<xref:System.ServiceModel.Web.WebInvokeAttribute.Method%2A> プロパティは使用しないでください。  
  
 GET に切り替える実施例については、「[基本的な AJAX サービス](../../../../docs/framework/wcf/samples/basic-ajax-service.md)」のサンプルを参照してください。  
  
 POST の使用例については、「[HTTP POST を使用する AJAX サービス](../../../../docs/framework/wcf/samples/ajax-service-using-http-post.md)」のサンプルを参照してください。  
  
### HTTP GET または HTTP POST 要求に応答する WCF サービスを作成するには  
  
1.  <xref:System.ServiceModel.ServiceContractAttribute> 属性でマークされたインターフェイスを使用して、基本的な [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] サービス コントラクトを定義します。  各操作を <xref:System.ServiceModel.OperationContractAttribute> でマークします。  <xref:System.ServiceModel.Web.WebGetAttribute> 属性を追加して、操作が HTTP GET 要求に応答するように指定します。  HTTP POST を明示的に指定するために <xref:System.ServiceModel.Web.WebInvokeAttribute> 属性を追加することもできます。また、属性を指定しなければ、既定で HTTP POST となります。  
  
    ```  
    [ServiceContract]  
    public interface IMusicService  
    {  
        //This operation uses a GET method.  
        [OperationContract]  
        [WebGet]  
        string LookUpArtist(string album);  
  
        //This operation will use a POST method.  
        [OperationContract]  
        [WebInvoke]  
        void AddAlbum(string user, string album);  
  
        //This operation will use POST method by default  
        //since nothing else is explicitly specified.  
        [OperationContract]  
        string[] GetAlbums(string user);  
  
        //Other operations omitted…  
  
    }  
    ```  
  
2.  `MusicService` を使用して、`IMusicService` サービス コントラクトを実装します。  
  
    ```  
    public class MusicService : IMusicService  
    {  
        public void AddAlbum(string user, string album)  
        {  
            //Add implementation here.  
        }  
  
         //Other operations omitted…  
    }  
    ```  
  
3.  アプリケーションで、.svc という拡張子を付けて新しい service ファイルを作成します。  サービスに該当する [@ServiceHost](../../../../docs/framework/configure-apps/file-schema/wcf-directive/servicehost.md) ディレクティブ情報を追加して、このファイルを編集します。  ASP.NET AJAX エンドポイントが自動的に構成されるように、[@ServiceHost](../../../../docs/framework/configure-apps/file-schema/wcf-directive/servicehost.md) ディレクティブで <xref:System.ServiceModel.Activation.WebScriptServiceHostFactory> を使用することを指定します。  
  
    ```  
    <%@ServiceHost   
        language=c#   
        Debug="true"   
        Service="Microsoft.Ajax.Samples.MusicService"  
        Factory=System.ServiceModel.Activation.WebScriptServiceHostFactory  
    %>  
    ```  
  
### サービスを呼び出すには  
  
1.  ブラウザーを使用すると、クライアントのコードなしでサービスの GET 操作をテストできます。  たとえば、サービスがアドレス "http:\/\/example.com\/service.svc" で構成されている場合、ブラウザーのアドレス バーに「http:\/\/example.com\/service.svc\/LookUpArtist?album\=SomeAlbum」と入力するとサービスが呼び出され、応答がダウンロードまたは表示されます。  
  
2.  GET 操作によるサービスは、他の ASP.NET AJAX サービスと同様に、サービス URL を ASP.NET AJAX Script Manager コントロールのスクリプト コレクションに入力することで使用できます。  例については、「[基本的な AJAX サービス](../../../../docs/framework/wcf/samples/basic-ajax-service.md)」を参照してください。  
  
## 参照  
 [ASP.NET AJAX 用の WCF サービスの作成](../../../../docs/framework/wcf/feature-details/creating-wcf-services-for-aspnet-ajax.md)   
 [方法 : AJAX 対応 ASP.NET Web サービスを WCF に移行する](../../../../docs/framework/wcf/feature-details/how-to-migrate-ajax-enabled-aspnet-web-services-to-wcf.md)