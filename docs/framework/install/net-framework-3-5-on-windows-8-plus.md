---
title: "Windows 8、Windows 8.1、および Windows 10 への .NET Framework 3.5 のインストール"
ms.date: 05/26/2017
ms.prod: .net-framework
ms.technology:
- dotnet-clr
ms.topic: article
helpviewer_keywords:
- .NET Framework 3.5, installing on Windows 8
- Windows 8, installing .NET Framework 3.5
ms.assetid: 3eab3eb4-4573-42ac-98f8-36fb2c22c7d5
caps.latest.revision: 69
author: mairaw
ms.author: mairaw
ms.translationtype: HT
ms.sourcegitcommit: 93f77dd5c3ca61935ae98ddef15f9c5cf7644bbb
ms.openlocfilehash: e9c8dcfacff689761d9ec891db8a1a4756acece0
ms.contentlocale: ja-jp
ms.lasthandoff: 08/23/2017

---

# <a name="install-the-net-framework-35-on-windows-8-windows-81-and-windows-10"></a>Windows 8、Windows 8.1、および Windows 10 への .NET Framework 3.5 のインストール

.NET Framework は、Windows 上で実行されている多数のアプリケーションに不可欠な部分であり、それらのアプリケーションが稼働するための共通の機能を提供します。 開発者に対し、.NET Framework はアプリケーションを作成するための一貫したプログラミング モデルを提供します。 Windows オペレーティング システムを使用している場合は、.NET Framework がコンピューターに既にインストールされている場合があります。 具体的には、[!INCLUDE[net_v45](../../../includes/net-v45-md.md)] には [!INCLUDE[win8](../../../includes/win8-md.md)]が組み込まれており、[!INCLUDE[net_v451](../../../includes/net-v451-md.md)] には [!INCLUDE[win81](../../../includes/win81-md.md)] が組み込まれており、Windows 10 には [!INCLUDE[net_v46](../../../includes/net-v46-md.md)] が組み込まれています。  
  
ただし、.NET Framework 3.5 は [!INCLUDE[win8](../../../includes/win8-md.md)]、[!INCLUDE[win81](../../../includes/win81-md.md)]、または Windows 10 と一緒に自動的にインストールされません。これに依存するアプリケーションを実行するには、.NET Framework 3.5 を別途有効にする必要があります。 これは、3 つの方法のいずれかで呼び出される、Windows Update を使用して行われる必要があります。 以下の方法はすべて、インターネット接続が必要です。  
  
- [必要に応じて .NET Framework 3.5 をインストールする](#OnDemand)  
  
- [コントロール パネルで .NET Framework 3.5 を有効にする](#ControlPanel)  
  
- [.NET Framework 3.5 インストーラーをダウンロードする](http://www.microsoft.com/en-us/download/details.aspx?id=21) (注: これは .NET Framework を直接ダウンロードするのでなく、Windows Update を呼び出すインストーラーです)。  
  
インストール中にエラー 0x800f0906、0x800f0907、または 0x800f081f が発生することがあります。その場合は、「[.NET Framework 3.5 インストール エラー: 0x800f0906、0x800f0907、または 0x800f081f](https://support.microsoft.com/help/2734782/net-framework-3-5-installation-error-0x800f0906--0x800f081f--0x800f09)」を参照してください。 なお、これらのエラーは、 [セキュリティ更新プログラム 3005628](https://support.microsoft.com/kb/3005628)をインストールすれば解決することがあります。  
  
前述の方法がいずれも失敗した場合、またはインターネット接続がない場合は、Windows のインストール メディアを使用する必要があります。 詳細については、 [.NET Framework 3.5 のインストール エラーに関する記事](https://support.microsoft.com/en-us/kb/2734782)に記載されているエラー 0x800f0906 用の方法 3 を参照してください。 インストール メディアがいない場合は、「[Windows 8.1 用のインストール メディアを作成する](http://windows.microsoft.com/en-US/windows-8/create-reset-refresh-media?woldogcb=0)」を参照してください。  
  
**重要なメモ:**
  
- 通常は、コンピューターからすべてのバージョンの .NET Framework をアンインストールしないでください。 アプリごとに異なるバージョンのフレームワークに依存していることがあり、.NET Framework の複数のバージョンが 1 台のコンピューターに共存することができます。  
  
- .NET Framework 3.5 は、バージョン 2.0 および 3.0 用にビルドされたアプリでも使用されます。  
  
- .NET Framework 3.5 をインストールする前に Windows の言語パックをインストールすると、.NET Framework 3.5 のインストールが失敗することがあります。 Windows の言語パックをインストールする前に .NET Framework 3.5 をインストールしてください。  
  
- Windows CardSpace は [!INCLUDE[win8](../../../includes/win8-md.md)]の .NET Framework 3.5 では使用できません。  
  
- .NET Framework 3.5 のインストール方法については複雑であるため、残念ながら Windows Update とは独立して実行可能なスタンドアロン インストーラーを個別に提供することはできません。 その他の方法がすべて失敗した場合は、前述したインストール メディアを使用してください。  
  
<a name="OnDemand"></a>   
## <a name="install-the-net-framework-35-on-demand"></a>必要に応じて .NET Framework 3.5 をインストールする

アプリに .NET Framework 3.5 が必要でも、コンピューター上でこのバージョンが有効化されていることを検出できない場合、インストール中またはアプリの初回起動時に次のメッセージ ボックスが表示されます。 .NET Framework 3.5 を有効にするには、このメッセージ ボックスの **[Install this feature]** (この機能のインストール) を選択します。 このオプションを使用するには、インターネット接続が必要です。  
  
![Windows 8 に 3.5 をインストールするためのダイアログ ボックス](../../../docs/framework/deployment/media/installdialog.png "installdialog")  
  
<a name="ControlPanel"></a>   
## <a name="enable-the-net-framework-35-in-control-panel"></a>コントロール パネルで .NET Framework 3.5 を有効にする

コントロール パネルを使用して .NET Framework 3.5 を有効にできます。 このオプションを使用するには、インターネット接続が必要です。  
  
1. キーボードの Windows キー ![Windows ロゴ](../../../docs/framework/get-started/media/windowskeyboardlogo.png "Windowskeyboardlogo") を押します。 「Windows の機能」と入力して Enter キーを押します。 **[Windows の機能の有効化または無効化]** ダイアログ ボックスが表示されます。 あるいは、[コントロール パネル] を開き、**[プログラム]** の項目をクリックし、**[プログラムと機能]** で **[Windows の機能の有効化または無効化]** を選択します。  
  
2. **[.NET Framework 3.5 (.NET 2.0 および 3.0 を含む)]** チェック ボックスをオンにして **[OK]** を選択し、メッセージが表示された場合はコンピューターを再起動します。  
  
WCF スクリプトおよびハンドラー マッピングの機能を必要とする開発者でない限り、**Windows Communication Foundation (WCF) HTTP アクティブ化**用に子項目を選択する必要はありません。
  
## <a name="see-also"></a>関連項目

[インストール ガイド](../../../docs/framework/get-started/index.md)

