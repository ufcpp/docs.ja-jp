---
title: "ホスティング サービス | Microsoft Docs"
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
helpviewer_keywords: 
  - "ホスティング サービス [WCF]"
ms.assetid: 192be927-6be2-4fda-98f0-e513c4881acc
caps.latest.revision: 31
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 31
---
# ホスティング サービス
アクティブにするには、サービスを作成してそのコンテキストと有効期間を制御するランタイム環境内で、サービスをホストする必要があります。[!INCLUDE[indigo1](../../../includes/indigo1-md.md)] サービスは、マネージ コードをサポートする任意の Windows プロセスで実行されるように設計されています。  
  
 [!INCLUDE[indigo2](../../../includes/indigo2-md.md)] は、サービス指向アプリケーションを構築するための統一されたプログラミング モデルを提供します。 このプログラミング モデルには一貫性があり、サービスが展開されるランタイム環境に影響されません。 これは実際には、ホスト オプションにかかわらず、サービスのコードがほぼ同じになることを意味しています。  
  
 これらのホスト オプションの範囲は、コンソール アプリケーション内部での実行から、Windows サービスのようなサーバー環境、インターネット インフォメーション サービス \(IIS\) または Windows プロセス アクティブ化サービス \(WAS\) で管理されるワーカー プロセス内での実行までさまざまです。 開発者は、サービスの展開要件を満たすホスト環境を選択します。 このような要件は、アプリケーションを展開するプラットフォーム、メッセージの送受信を行うトランスポート、適切な可用性を保証するために必要なプロセスのリサイクルや管理、その他、管理上または信頼性上の要件から導き出されます。 ホスト オプションの情報とガイドラインについて、次のセクションで説明します。  
  
## ホスト オプション  
  
#### マネージ アプリケーションにおける自己ホスト  
 [!INCLUDE[indigo2](../../../includes/indigo2-md.md)] サービスはすべてのマネージ アプリケーションでホストされます。 これは、展開に必要なインフラストラクチャが最小限になるため、最も柔軟なオプションです。 マネージ アプリケーション コード内にサービスのコードを埋め込み、続いて <xref:System.ServiceModel.ServiceHost> のインスタンスを作成して開き、サービスを有効にします。[!INCLUDE[crdefault](../../../includes/crdefault-md.md)] [方法 : マネージ アプリケーションで WCF サービスをホストする](../../../docs/framework/wcf/how-to-host-a-wcf-service-in-a-managed-application.md)。  
  
 このオプションで可能になる一般的なシナリオには、コンソール アプリケーション内部で実行される [!INCLUDE[indigo2](../../../includes/indigo2-md.md)] サービスと、[!INCLUDE[avalon1](../../../includes/avalon1-md.md)] または Windows フォーム \(WinForms\) に基づくリッチ クライアント アプリケーションの 2 つがあります。 コンソール アプリケーション内部の [!INCLUDE[indigo2](../../../includes/indigo2-md.md)] サービスをホストすることは、一般的にアプリケーションの開発フェーズで有用です。 コンソール アプリケーションにより、アプリケーション内部で起こっている状況を見極めるための情報のデバッグやトレースが容易になり、新しい場所にアプリケーションをコピーして移動することも簡単に行うことができます。 このホスト オプションを使用すると、[!INCLUDE[avalon2](../../../includes/avalon2-md.md)] や WinForms アプリケーションなど、外部と通信を行うリッチ クライアント アプリケーションの作成も容易になります。 たとえば、ユーザー インターフェイスに [!INCLUDE[avalon2](../../../includes/avalon2-md.md)] を使用しながら、他のクライアントからの接続を許容して情報を共有するために [!INCLUDE[indigo2](../../../includes/indigo2-md.md)] サービスをホストするピア ツー ピア コラボレーションのクライアントなどです。  
  
#### マネージ Windows サービス  
 このホスト オプションは、[!INCLUDE[indigo2](../../../includes/indigo2-md.md)] サービスをマネージ Windows サービス \(従来 NT サービスと呼ばれていたもの\) としてホストするアプリケーション ドメイン \(AppDomain\) の登録から構成されているため、サービスのプロセス有効期間は Windows サービスのサービス コントロール マネージャー \(SCM\) によって制御されます。 自己ホスト オプションと同様、この種類のホスト環境では、ホスト コードをアプリケーションの一部として記述する必要があります。 サービスは、Windows サービスと [!INCLUDE[indigo2](../../../includes/indigo2-md.md)] サービスの両方として実装します。そのためには、<xref:System.ServiceProcess.ServiceBase> クラスから継承すると同時に、[!INCLUDE[indigo2](../../../includes/indigo2-md.md)] サービス コントラクト インターフェイスからも継承します。 次に <xref:System.ServiceModel.ServiceHost> を作成し、オーバーライドされた [OnStart\(String\<xref:System.ServiceProcess.ServiceBase.OnStart%28System.String%5B%5D%29> メソッドで開き、オーバーライドされた <xref:System.ServiceProcess.ServiceBase.OnStop> メソッドで閉じます。 また、<xref:System.Configuration.Install.Installer> から継承されるインストーラー クラスも実装し、プログラムが Installutil.exe ツールによって Windows サービスとしてインストールされるようにする必要があります。[!INCLUDE[crdefault](../../../includes/crdefault-md.md)] [方法 : マネージ Windows サービスで WCF サービスをホストする](../../../docs/framework/wcf/feature-details/how-to-host-a-wcf-service-in-a-managed-windows-service.md)。 マネージ Windows サービスのホスト オプションによって有効になるシナリオは、メッセージがアクティブ化されていない、セキュリティ保護された環境において、IIS の外部でホストされ、長時間実行される [!INCLUDE[indigo2](../../../includes/indigo2-md.md)] サービスです。 サービスの有効期限は代わりにオペレーティング システムによって制御されます。 このホスト オプションは Windows のすべてのバージョンで使用できます。  
  
#### インターネット インフォメーション サービス \(IIS\)  
 IIS ホスト オプションは [!INCLUDE[vstecasp](../../../includes/vstecasp-md.md)] と統合され、プロセスのリサイクル、アイドル シャットダウン、処理状況の監視、メッセージに基づくアクティベーションなど、このテクノロジによって提供される機能を使用します。[!INCLUDE[wxp](../../../includes/wxp-md.md)] および [!INCLUDE[ws2003](../../../includes/ws2003-md.md)] オペレーティング システムでは、高可用性と高スケーラビリティが求められる Web サービス アプリケーションのホストには、このオプションが適切なソリューションとなります。 IIS では、顧客がエンタープライズ クラスのサーバー製品に求める統合された管理性も提供されます。 このホスト オプションでは、IIS が正しく構成されている必要がありますが、アプリケーションの一部としてホスト コードを書く必要はありません。[!INCLUDE[indigo2](../../../includes/indigo2-md.md)] サービス用に IIS ホストを構成する方法の[!INCLUDE[crabout](../../../includes/crabout-md.md)]については、「[方法 : IIS で WCF サービスをホストする](../../../docs/framework/wcf/feature-details/how-to-host-a-wcf-service-in-iis.md)」を参照してください。  
  
 IIS でホストされるサービスは HTTP トランスポートしか使用できません。 IIS 5.1 の実装では、[!INCLUDE[wxp](../../../includes/wxp-md.md)] にいくつかの制限がありました。[!INCLUDE[indigo2](../../../includes/indigo2-md.md)] 上で IIS 5.1 によって提供される、[!INCLUDE[wxp](../../../includes/wxp-md.md)] サービス用のメッセージ ベースのアクティベーションでは、同じコンピューター上にあるそれ以外の自己ホスト型 [!INCLUDE[indigo2](../../../includes/indigo2-md.md)] サービスによる、ポート 80 を使用した通信が妨げられます。[!INCLUDE[indigo2](../../../includes/indigo2-md.md)] 上で [!INCLUDE[iis601](../../../includes/iis601-md.md)] によってホストした場合は、[!INCLUDE[ws2003](../../../includes/ws2003-md.md)] サービスは他のアプリケーションと同じ AppDomain\/アプリケーション プール\/ワーカー プロセスで実行できます。 ただし、[!INCLUDE[indigo2](../../../includes/indigo2-md.md)] と [!INCLUDE[iis601](../../../includes/iis601-md.md)] のどちらもカーネル モードの HTTP スタック \(HTTP.sys\) を使用するため、IIS 5.1 とは異なり、[!INCLUDE[iis601](../../../includes/iis601-md.md)] ではポート 80 を同じコンピューター上で実行される他の自己ホスト型 [!INCLUDE[indigo2](../../../includes/indigo2-md.md)] サービスと共有できます。  
  
#### Windows プロセス アクティブ化サービス \(WAS\)  
 Windows プロセス アクティブ化サービス \(WAS\) とは、[!INCLUDE[lserver](../../../includes/lserver-md.md)] でも使用できる [!INCLUDE[wv](../../../includes/wv-md.md)] 用の新しいプロセス アクティブ化機構です。 よく知られている [!INCLUDE[iis601](../../../includes/iis601-md.md)] のプロセス モデル \(アプリケーション プールとメッセージ ベースのプロセス アクティベーション\) とホスト機能 \(迅速な障害保護、状態の監視、プロセスのリサイクルなど\) はそのままですが、HTTP に対する依存性がアクティベーション アーキテクチャから解消されています。[!INCLUDE[iisver](../../../includes/iisver-md.md)] では、WAS を使用して HTTP 経由でのメッセージ ベースのアクティベーションを実現しています。 ただし、[!INCLUDE[indigo2](../../../includes/indigo2-md.md)] がサポートする他のプロトコル \(TCP、MSMQ、名前付きパイプなど\) を介してメッセージ ベースのアクティベーションを実現するために、WAS には追加の [!INCLUDE[indigo2](../../../includes/indigo2-md.md)] コンポーネントもプラグインされています。 これにより、IIS のプロセスのリサイクル、迅速な障害保護、一般的な構成システムなど、これまで HTTP ベースのアプリケーションのみで利用可能だった IIS 機能を、通信プロトコルを使用するアプリケーションでも使用できるようになりました。  
  
 このホスト オプションでは、WAS が正しく構成されている必要がありますが、アプリケーションの一部としてホスト コードを書く必要はありません。 WAS ホストを構成する方法の[!INCLUDE[crabout](../../../includes/crabout-md.md)]については、「[方法 : WAS で WCF サービスをホストする](../../../docs/framework/wcf/feature-details/how-to-host-a-wcf-service-in-was.md)」を参照してください。  
  
## ホスト環境の選択  
 次の表に、各ホスト オプションに関連する主な利点とシナリオの要点をまとめます。  
  
|ホスト環境|一般的なシナリオ|主な利点と制限|  
|-----------|--------------|-------------|  
|マネージ アプリケーション \("自己ホスト"\)|-   開発時に使用されるコンソール アプリケーション。<br />-   サービスにアクセスするリッチな Winform と [!INCLUDE[avalon2](../../../includes/avalon2-md.md)] クライアント アプリケーション。|-   柔軟性。<br />-   展開の容易さ。<br />-   サービスのエンタープライズ ソリューションではない。|  
|Windows サービス \(従来 NT サービスと呼ばれていたもの\)|-   IIS 外でホストされ長時間実行される [!INCLUDE[indigo2](../../../includes/indigo2-md.md)] サービス。|-   サービス プロセスの有効期間は、メッセージ ベースのアクティベーションではなくオペレーティング システムにより制御される。<br />-   すべてのバージョンの Windows でサポートされる。<br />-   セキュリティで保護された環境。|  
|IIS 5.1、[!INCLUDE[iis601](../../../includes/iis601-md.md)]|-   HTTP プロトコルを使い、インターネット上で [!INCLUDE[indigo2](../../../includes/indigo2-md.md)] サービスを [!INCLUDE[vstecasp](../../../includes/vstecasp-md.md)] コンテンツと共に同時に実行する。|-   プロセスのリサイクル。<br />-   アイドル シャットダウン。<br />-   処理状況の監視。<br />-   メッセージ ベースのアクティベーション。<br />-   HTTP のみ。|  
|Windows プロセス アクティブ化サービス \(WAS\)|-   インターネット上で IIS をインストールせずに、さまざまなトランスポート プロトコルを使用して [!INCLUDE[indigo2](../../../includes/indigo2-md.md)] サービスを実行する。|-   IIS は不要。<br />-   プロセスのリサイクル。<br />-   アイドル シャットダウン。<br />-   処理状況の監視。<br />-   メッセージ ベースのアクティベーション。<br />-   HTTP、TCP、名前付きパイプ、および MSMQ で動作する。|  
|IIS 7.0|-   [!INCLUDE[indigo2](../../../includes/indigo2-md.md)] コンテンツと共に [!INCLUDE[vstecasp](../../../includes/vstecasp-md.md)] サービスを実行する。<br />-   インターネット上で、さまざまなトランスポート プロトコルを使用して [!INCLUDE[indigo2](../../../includes/indigo2-md.md)] サービスを実行する。|-   WAS の利点。<br />-   [!INCLUDE[vstecasp](../../../includes/vstecasp-md.md)] および IIS コンテンツと統合される。|  
  
 ホスト環境の選択は、その展開先の Windows のバージョン、メッセージの送信に必要なトランスポート、および必要となるプロセスとアプリケーション ドメインのリサイクルの種類に依存します。 次の表に、これらの要件に関連するデータをまとめます。  
  
|ホスト環境|プラットフォームの可用性|サポートされるトランスポート|プロセスと AppDomain のリサイクル|  
|-----------|------------------|--------------------|----------------------------|  
|マネージ アプリケーション \("自己ホスト"\)|[!INCLUDE[wxp](../../../includes/wxp-md.md)], [!INCLUDE[ws2003](../../../includes/ws2003-md.md)], [!INCLUDE[wv](../../../includes/wv-md.md)],<br /><br /> [!INCLUDE[lserver](../../../includes/lserver-md.md)]|HTTP、<br /><br /> net.tcp、<br /><br /> net.pipe、<br /><br /> net.msmq|いいえ|  
|Windows サービス \(従来 NT サービスと呼ばれていたもの\)|[!INCLUDE[wxp](../../../includes/wxp-md.md)], [!INCLUDE[ws2003](../../../includes/ws2003-md.md)], [!INCLUDE[wv](../../../includes/wv-md.md)],<br /><br /> [!INCLUDE[lserver](../../../includes/lserver-md.md)]|HTTP、<br /><br /> net.tcp、<br /><br /> net.pipe、<br /><br /> net.msmq|いいえ|  
|IIS 5.1|[!INCLUDE[wxp](../../../includes/wxp-md.md)]|HTTP|はい|  
|[!INCLUDE[iis601](../../../includes/iis601-md.md)]|[!INCLUDE[ws2003](../../../includes/ws2003-md.md)]|HTTP|はい|  
|Windows プロセス アクティブ化サービス \(WAS\)|[!INCLUDE[wv](../../../includes/wv-md.md)], [!INCLUDE[lserver](../../../includes/lserver-md.md)]|HTTP、<br /><br /> net.tcp、<br /><br /> net.pipe、<br /><br /> net.msmq|はい|  
  
 信頼されていないホストからサービスや拡張機能を実行すると、セキュリティが損なわれるので注意してください。 また、偽装して <xref:System.ServiceModel.ServiceHost> を開くと、アプリケーションは、ユーザーの <xref:System.Security.Principal.WindowsIdentity> をキャッシュするなどして、ユーザーがログオフしていないことを確認する必要があります。  
  
## 参照  
 [システム要件](../../../docs/framework/wcf/wcf-system-requirements.md)   
 [基本的なプログラミング ライフサイクル](../../../docs/framework/wcf/basic-programming-lifecycle.md)   
 [サービス コントラクトの実装](../../../docs/framework/wcf/implementing-service-contracts.md)   
 [方法 : IIS で WCF サービスをホストする](../../../docs/framework/wcf/feature-details/how-to-host-a-wcf-service-in-iis.md)   
 [方法 : WAS で WCF サービスをホストする](../../../docs/framework/wcf/feature-details/how-to-host-a-wcf-service-in-was.md)   
 [方法 : マネージ Windows サービスで WCF サービスをホストする](../../../docs/framework/wcf/feature-details/how-to-host-a-wcf-service-in-a-managed-windows-service.md)   
 [方法 : マネージ アプリケーションで WCF サービスをホストする](../../../docs/framework/wcf/how-to-host-a-wcf-service-in-a-managed-application.md)