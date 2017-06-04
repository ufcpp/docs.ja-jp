---
title: "方法: マネージ コード DCOM を WCF に移行する | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
dev_langs: 
  - "VB"
  - "CSharp"
  - "C++"
  - "jsharp"
ms.assetid: 52961ffc-d1c7-4f83-832c-786444b951ba
caps.latest.revision: 6
author: "mairaw"
ms.author: "mairaw"
manager: "wpickett"
caps.handback.revision: 6
---
# 方法: マネージ コード DCOM を WCF に移行する
Windows Communication Foundation \(WCF\) は、分散コンポーネント オブジェクト モデル \(DCOM\) と比較して、分散環境でサーバーとクライアントの間でマネージ コードを呼び出すための、推奨されているセキュリティで保護された選択肢です。  この記事では、以下のシナリオで、DCOM から WCF にコードを移行する方法を示します。  
  
-   リモート サービスからクライアントに値渡しでオブジェクトを返す  
  
-   クライアントからリモート サービスに値渡しでオブジェクトを送信する  
  
-   リモート サービスからクライアントに参照渡しでオブジェクトを返す  
  
 セキュリティ上の理由で、WCF では、クライアントからサービスに参照渡しでオブジェクトを送信することはできません。  クライアントとサーバーの間で対話を必要とするシナリオは、WCF で双方向サービスを使用することによって実現できます。  双方向サービスの詳細については、「[双方向サービス](../../../docs/framework/wcf/feature-details/duplex-services.md)」を参照してください。  
  
 WCF サービスの作成方法、およびそれらのサービスのクライアントの作成方法について詳しくは、「[基本的な WCF プログラミング](../../../docs/framework/wcf/basic-wcf-programming.md)」、「[サービスの設計と実装](../../../docs/framework/wcf/designing-and-implementing-services.md)」および「[クライアントを構築する](../../../docs/framework/wcf/building-clients.md)」を参照してください。  
  
## DCOM コード例  
 これらのシナリオでは、WCF を使用して示されている DCOM インターフェイスに、以下の構造があります。  
  
```  
[ComVisible(true)]  
[Guid("AA9C4CDB-55EA-4413-90D2-843F1A49E6E6")]  
public interface IRemoteService  
{  
   Customer GetObjectByValue();  
   IRemoteObject GetObjectByReference();  
   void SendObjectByValue(Customer customer);  
}  
  
[ComVisible(true)]  
[Guid("A12C98DE-B6A1-463D-8C24-81E4BBC4351B")]  
public interface IRemoteObject  
{  
}  
  
public class Customer  
{  
}  
  
```  
  
## サービスから値渡しでオブジェクトを返す  
 このシナリオでは、サービスを呼び出し、そのメソッドがオブジェクトを返します。オブジェクトはサーバーからクライアントに値で渡されます。  このシナリオは、次の COM 呼び出しを表しています。  
  
```  
public interface IRemoteService  
{  
    Customer GetObjectByValue();  
}  
```  
  
 このシナリオでは、クライアントは、リモート サービスからオブジェクトの逆シリアル化されたコピーを受け取ります。  クライアントは、サービスにコールバックしなくても、このローカル コピーと対話できます。  つまり、ローカル コピーのメソッドが呼び出されるときに、サービスはまったく関与しないことがクライアントに保証されています。  WCF は常にサービスから値渡しでオブジェクトを返すため、次の各手順では、通常の WCF サービスを作成する方法について説明します。  
  
### 手順 1: WCF サービスのインターフェイスを定義する  
 WCF サービスのパブリック インターフェイスを定義し、\[<xref:System.ServiceModel.ServiceContractAttribute>\] 属性でマークします。  クライアントに公開するメソッドを \[<xref:System.ServiceModel.OperationContractAttribute>\] 属性でマークします。  次の例は、これらの属性を使用して、サーバー側のインターフェイスと、クライアントが呼び出すことのできるインターフェイス メソッドとを識別する方法を示しています。  このシナリオで使用されるメソッドは、太字で示します。  
  
```  
using System.Runtime.Serialization;  
using System.ServiceModel;  
using System.ServiceModel.Web;   
. . .  
[ServiceContract]  
public interface ICustomerManager  
{  
    [OperationContract]  
    void StoreCustomer(Customer customer);  
  
    [OperationContract]     
    Customer GetCustomer(string firstName, string lastName);   
  
}  
  
```  
  
### 手順 2: データ コントラクトを定義する  
 次に、サービスとクライアントの間でデータが交換される方法を説明する、サービスのデータ コントラクトを作成する必要があります。  データ コントラクトで説明されたクラスは、\[<xref:System.Runtime.Serialization.DataContractAttribute>\] 属性でマークする必要があります。  クライアントとサーバーの両方に表示する個々のプロパティやフィールドは、\[<xref:System.Runtime.Serialization.DataMemberAttribute>\] 属性でマークする必要があります。データ コントラクト内のクラスから派生した型を許可する場合は、\[<xref:System.Runtime.Serialization.KnownTypeAttribute>\] 属性でそれらを指定する必要があります。  WCF は、サービス インターフェイス内の型と既知の型として識別される型だけを、シリアル化または逆シリアル化します。  既知の型ではない型を使用しようとすると、例外が発生します。  
  
 データ コントラクトの詳細については、「[データ コントラクト](../../../docs/framework/wcf/samples/data-contracts.md)」を参照してください。  
  
```  
[DataContract]  
[KnownType(typeof(PremiumCustomer))]  
public class Customer  
{  
    [DataMember]  
    public string Firstname;  
    [DataMember]  
    public string Lastname;  
    [DataMember]  
    public Address DefaultDeliveryAddress;  
    [DataMember]  
    public Address DefaultBillingAddress;  
}  
 [DataContract]  
public class PremiumCustomer : Customer  
{  
    [DataMember]  
    public int AccountID;  
}  
  
 [DataContract]  
public class Address  
{  
    [DataMember]  
    public string Street;  
    [DataMember]  
    public string Zipcode;  
    [DataMember]  
    public string City;  
    [DataMember]  
    public string State;  
    [DataMember]  
    public string Country;  
}  
  
```  
  
### 手順 3: WCF サービスを実装する  
 次に、前の手順で定義したインターフェイスを実装する、WCF サービス クラスを実装する必要があります。  
  
```  
public class CustomerService: ICustomerManager    
{  
    public void StoreCustomer(Customer customer)  
    {  
        // write to a database  
    }  
    public Customer GetCustomer(string firstName, string lastName)  
    {  
        // read from a database  
    }  
}  
```  
  
### 手順 4: サービスとクライアントを構成する  
 WCF サービスを実行するには、特定の WCF バインドを使用して特定の URL で上記のサービス インターフェイスを公開するエンドポイントを宣言する必要があります。  バインディングは、クライアントとサーバーが通信するための、トランスポート、エンコード、およびプロトコルの詳細を指定します。  通常、サービス プロジェクトの構成ファイル \(web.config\) にバインドを追加します。  サービス例のためのバインド エントリを以下に示します。  
  
```  
<configuration>  
  <system.serviceModel>  
    <services>  
      <service name="Server.CustomerService">  
        <endpoint address="http://localhost:8083/CustomerManager"   
                  binding="basicHttpBinding"  
                  contract="Shared.ICustomerManager" />  
      </service>  
    </services>  
  </system.serviceModel>  
</configuration>  
  
```  
  
 次に、サービスによって指定されたバインド情報と一致するように、クライアントを構成する必要があります。  そのためには、クライアントのアプリケーション構成 \(app.config\) ファイルに以下を追加します。  
  
```  
<configuration>  
  <system.serviceModel>  
    <client>  
      <endpoint name="customermanager"   
                address="http://localhost:8083/CustomerManager"   
                binding="basicHttpBinding"   
                contract="Shared.ICustomerManager"/>  
  </system.serviceModel>  
</configuration>  
  
```  
  
### 手順 5: サービスを実行する  
 最後に、サービス アプリに次の行を追加して、アプリを起動することにより、コンソール アプリケーション内で自己ホストすることができます。  WCF サービス アプリケーションをホストするその他の方法について詳しくは、「[ホスティング サービス](../../../docs/framework/wcf/hosting-services.md)」を参照してください。  
  
```  
ServiceHost customerServiceHost = new ServiceHost(typeof(CustomerService));  
customerServiceHost.Open();  
  
```  
  
### 手順 6: クライアントからサービスを呼び出す  
 クライアントからのサービスを呼び出すには、サービスのチャネル ファクトリを作成し、チャネルを要求する必要があります。これにより、クライアントから `GetCustomer` メソッドを直接呼び出すことができるようになります。  チャネルはサービスのインターフェイスを実装し、基になる要求\/応答のロジックを処理します。  このメソッドの呼び出しからの戻り値は、サービス応答の逆シリアル化されたコピーです。  
  
```  
ChannelFactory<ICustomerManager> factory =   
     new ChannelFactory<ICustomerManager>("customermanager");  
ICustomerManager service = factory.CreateChannel();  
Customer customer = service.GetCustomer("Mary", "Smith");  
  
```  
  
## クライアントからサーバーに値渡しのオブジェクトを送信する  
 このシナリオでは、クライアントがサーバーに値渡しでオブジェクトを送信します。  つまり、サーバーは、オブジェクトの逆シリアル化されたコピーを受け取ります。  サーバーは、そのコピーのメソッドを呼び出すことができ、クライアント コードにコールバックがないことが保証されます。  前述のとおり、WCF での通常のデータ交換は、値渡しでなされます。  これにより、これらのいずれかのオブジェクトのメソッドの呼び出しはローカルでのみ実行され、クライアントではコードは呼び出されないことが保証されます。  
  
 このシナリオは、次の COM メソッドの呼び出しを表しています。  
  
```  
public interface IRemoteService  
{  
    void SendObjectByValue(Customer customer);  
}  
  
```  
  
 このシナリオでは、最初の例で示すものと同じサービス インターフェイスおよびデータ コントラクトを使用します。  さらに、クライアントとサービスが同じ方法で構成されます。  この例では、オブジェクトを送信するためにチャネルが作成されて、同じ方法で実行されます。  ただし、この例では、値渡しでオブジェクトを送信して、サービスを呼び出すクライアントを作成します。  クライアントがサービス コントラクトで呼び出すサービス メソッドは、太字で示されます。  
  
```  
[ServiceContract]  
public interface ICustomerManager  
{  
    [OperationContract]  
        void StoreCustomer(Customer customer);  
  
    [OperationContract]  
    Customer GetCustomer(string firstName, string lastName);  
}  
  
```  
  
### 値渡しのオブジェクトを送信するクライアントにコードを追加する  
 次のコードは、クライアントが値渡しの customer オブジェクトを新規に作成する方法、`ICustomerManager` サービスと通信するチャネルを作成する方法、およびそこに customer オブジェクトを送信する方法を示しています。  
  
 Customer オブジェクトはシリアル化され、サービスに送信されて、サービスによりそのオブジェクトの新しいコピーへと逆シリアル化されます。  サービスがこのオブジェクトで呼び出すメソッドは、サーバーにおいてローカルでのみ実行します。このコードは、派生型 \(`PremiumCustomer`\) の送信を例示していることに注意してください。  サービス コントラクトは `Customer` オブジェクトを想定していますが、サービス データ コントラクトは \[<xref:System.Runtime.Serialization.KnownTypeAttribute>\] 属性を使用して `PremiumCustomer` も許可されることを示しています。  このサービス インターフェイスを介して他の型をシリアル化または逆シリアル化しようとしても、WCF は失敗します。  
  
```  
PremiumCustomer customer = new PremiumCustomer();  
customer.Firstname = "John";  
customer.Lastname = "Doe";  
customer.DefaultBillingAddress = new Address();  
customer.DefaultBillingAddress.Street = "One Microsoft Way";  
customer.DefaultDeliveryAddress = customer.DefaultBillingAddress;  
customer.AccountID = 42;  
  
ChannelFactory<ICustomerManager> factory =  
   new ChannelFactory<ICustomerManager>("customermanager");  
ICustomerManager customerManager = factory.CreateChannel();  
customerManager.StoreCustomer(customer);  
```  
  
## サービスから参照渡しでオブジェクトを返す  
 このシナリオでは、クライアント アプリがリモート サービスを呼び出し、メソッドがオブジェクトを返します。オブジェクトはサービスからクライアントに参照によって渡されます。  
  
 前述のとおり、WCF サービスは常に値でオブジェクトを返します。  ただし、<xref:System.ServiceModel.EndpointAddress10> クラスを使用して同様の結果を得ることもできます。  <xref:System.ServiceModel.EndpointAddress10> は、サーバー上のセッションフルな参照渡しのオブジェクトを取得するためにクライアントが使用できる、シリアル化可能な値渡しのオブジェクトです。  
  
 このシナリオで示される WCF の参照渡しのオブジェクトの動作は、DCOM とは異なります。  DCOM では、サーバーが参照渡しのオブジェクトをクライアントに直接返すことができ、クライアントはそのオブジェクトのメソッドを呼び出して、サーバーで実行することができます。  しかし WCF では、オブジェクトが常に値渡しで返されます。  クライアントは、<xref:System.ServiceModel.EndpointAddress10> によって表されるその値渡しのオブジェクトを取得し、それを使用して独自の参照渡しのセッションフル オブジェクトを作成する必要があります。  セッションフル オブジェクトのクライアント メソッド呼び出しは、サーバーで実行されます。つまり、WCF でのこの参照渡しのオブジェクトは、セッションフルとなるように構成された通常の WCF サービスです。  
  
 WCF では、セッションは 2 つのエンドポイント間で送信される複数のメッセージを関連付ける方法です。  つまり、クライアントがこのサービスへの接続を確保すると、クライアントとサーバーの間でセッションが確立されます。  クライアントは、サーバー側オブジェクトの単一で一意のインスタンスを、この 1 つのセッション内でのすべてのやり取りに使用することになります。  セッションフル WCF コントラクトは、接続指向ネットワークの要求\/応答パターンに似ています。  
  
 このシナリオは、以下の DCOM メソッドによって表されます。  
  
```  
public interface IRemoteService  
{  
    IRemoteObject GetObjectByReference();  
}  
```  
  
### 手順 1: セッションフル WCF サービスのインターフェイスと実装を定義する  
 最初に、セッションフル オブジェクトを含む WCF サービスのインターフェイスを定義します。  
  
 このコードでは、セッションフル オブジェクトが `ServiceContract` 属性でマークされ、通常の WCF サービスのインターフェイスとして示されています。  さらに、<xref:System.ServiceModel.ServiceContractAttribute.SessionMode%2A> プロパティが設定されて、セッションフル サービスとなることが示されています。  
  
```  
  
[ServiceContract(SessionMode = SessionMode.Allowed)]  
public interface ISessionBoundObject  
{  
    [OperationContract]  
    string GetCurrentValue();  
  
    [OperationContract]  
    void SetCurrentValue(string value);  
}  
```  
  
 サービスの実装を次のコードに示します。  
  
 サービスは \[ServiceBehavior\] 属性でマークされ、InstanceContextMode プロパティが InstanceContextMode.PerSessions に設定されて、セッションごとにこの型の一意のインスタンスを作成する必要があることを示しています。  
  
```  
[ServiceBehavior(InstanceContextMode = InstanceContextMode.PerSession)]  
    public class MySessionBoundObject : ISessionBoundObject  
    {  
        private string _value;  
  
        public string GetCurrentValue()  
        {  
            return _value;  
        }  
  
        public void SetCurrentValue(string val)  
        {  
            _value = val;  
        }  
  
    }  
  
```  
  
### 手順 2: セッションフル オブジェクトの WCF ファクトリ サービスを定義する  
 セッションフル オブジェクトを作成するサービスを定義して実装する必要があります。  この方法を次のコードに示します。  このコードは、<xref:System.ServiceModel.EndpointAddress10> オブジェクトとして返される別の WCF サービスを作成します。  これはセッションフル オブジェクトの作成に使用できる、エンドポイントのシリアル化可能な形式です。  
  
```  
[ServiceContract]  
    public interface ISessionBoundFactory  
    {  
        [OperationContract]  
        EndpointAddress10 GetInstanceAddress();  
    }  
  
```  
  
 このサービスの実装を次に示します。  この実装では、セッションフル オブジェクトを作成するためにシングルトン チャネル ファクトリを保持しています。  チャネル ファクトリは、`GetInstanceAddress` が呼び出されるとチャネルを作成し、このチャネルに関連付けられているリモート アドレスをポイントする <xref:System.ServiceModel.EndpointAddress10> オブジェクトを作成します。  <xref:System.ServiceModel.EndpointAddress10> は、値渡しでクライアントに返すことのできるデータ型です。  
  
```  
public class SessionBoundFactory : ISessionBoundFactory  
    {  
        public static ChannelFactory<ISessionBoundObject> _factory =   
            new ChannelFactory<ISessionBoundObject>("sessionbound");  
  
        public SessionBoundFactory()  
        {  
        }  
  
        public EndpointAddress10 GetInstanceAddress()  
        {  
            IClientChannel channel = (IClientChannel)_factory.CreateChannel();  
            return EndpointAddress10.FromEndpointAddress(channel.RemoteAddress);  
        }  
    }  
  
```  
  
### 手順 3: WCF サービスを構成して開始する  
 これらのサービスをホストするには、サーバーの構成ファイル \(web.config\) に以下を追加する必要があります。  
  
1.  セッションフル オブジェクトのエンドポイントを示す `<client>` セクションを追加します。  このシナリオでは、サーバーもクライアントとして機能するので、それが有効となるように構成する必要があります。  
  
2.  `<services>` セクションで、ファクトリおよびセッションフル オブジェクトのサービス エンドポイントを宣言します。  これにより、クライアントは、サービス エンドポイントと通信すること、<xref:System.ServiceModel.EndpointAddress10> を取得すること、およびセッションフル チャネルを作成することが可能になります。  
  
 これらの設定のある構成ファイルの例を次に示します。  
  
```  
<configuration>  
  <system.serviceModel>  
    <client>  
      <endpoint name="sessionbound"  
                address="net.tcp://localhost:8081/SessionBoundObject"  
                binding="netTcpBinding"  
                contract="Shared.ISessionBoundObject"/>  
    </client>  
  
    <services>  
      <service name="Server.MySessionBoundObject">  
        <endpoint address="net.tcp://localhost:8081/SessionBoundObject"  
                  binding="netTcpBinding"   
                  contract="Shared.ISessionBoundObject" />  
      </service>  
      <service name="Server.SessionBoundFactory">  
        <endpoint address="net.tcp://localhost:8081/SessionBoundFactory"  
                  binding="netTcpBinding"   
                  contract="Shared.ISessionBoundFactory" />  
      </service>  
    </services>  
  </system.serviceModel>  
</configuration>  
  
```  
  
 以下の行をコンソール アプリケーションに追加し、サービスを自己ホストして、アプリを開始します。  
  
```  
ServiceHost factoryHost = new ServiceHost(typeof(SessionBoundFactory));  
factoryHost.Open();  
  
ServiceHost sessionBoundServiceHost = new ServiceHost(  
typeof(MySessionBoundObject));  
sessionBoundServiceHost.Open();  
```  
  
### 手順 4: クライアントを構成してサービスを呼び出す  
 プロジェクトのアプリケーション構成ファイル \(app.config\) に以下のエントリを作成して、クライアントが WCF サービスと通信するように構成します。  
  
```  
<configuration>  
  <system.serviceModel>  
    <client>  
      <endpoint name="sessionbound"   
                address="net.tcp://localhost:8081/SessionBoundObject"   
                binding="netTcpBinding"   
                contract="Shared.ISessionBoundObject"/>  
      <endpoint name="factory"   
                address="net.tcp://localhost:8081/SessionBoundFactory"   
                binding="netTcpBinding"   
                contract="Shared.ISessionBoundFactory"/>  
    </client>    
  </system.serviceModel>  
</configuration>  
  
```  
  
 サービスを呼び出すには、クライアントにコードを追加して、以下を実行するようにします。  
  
1.  `ISessionBoundFactory` サービスへのチャネルを作成します。  
  
2.  チャネルを使用して `ISessionBoundFactory` サービスを呼び出し、<xref:System.ServiceModel.EndpointAddress10> オブジェクトを取得します。  
  
3.  <xref:System.ServiceModel.EndpointAddress10> を使用してチャネルを作成し、セッションフル オブジェクトを取得します。  
  
4.  `SetCurrentValue` および `GetCurrentValue` メソッドを呼び出して、複数の呼び出しの間で同じオブジェクト インスタンスが使用されることを示します。  
  
```  
ChannelFactory<ISessionBoundFactory> factory =  
        new ChannelFactory<ISessionBoundFactory>("factory");  
  
ISessionBoundFactory sessionBoundFactory = factory.CreateChannel();  
  
EndpointAddress10 address = sessionBoundFactory.GetInstanceAddress();  
  
ChannelFactory<ISessionBoundObject> sessionBoundObjectFactory =  
    new ChannelFactory<ISessionBoundObject>(  
        new NetTcpBinding(),  
        address.ToEndpointAddress());  
  
ISessionBoundObject sessionBoundObject =  
        sessionBoundObjectFactory.CreateChannel();  
  
sessionBoundObject.SetCurrentValue("Hello");  
if (sessionBoundObject.GetCurrentValue() == "Hello")  
{  
    Console.WriteLine("Session-full instance management works as expected");  
}  
```  
  
## 参照  
 [基本的な WCF プログラミング](../../../docs/framework/wcf/basic-wcf-programming.md)   
 [サービスの設計と実装](../../../docs/framework/wcf/designing-and-implementing-services.md)   
 [クライアントを構築する](../../../docs/framework/wcf/building-clients.md)   
 [双方向サービス](../../../docs/framework/wcf/feature-details/duplex-services.md)