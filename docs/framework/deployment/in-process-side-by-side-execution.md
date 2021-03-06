---
title: "インプロセスの side-by-side 実行"
ms.custom: 
ms.date: 03/30/2017
ms.prod: .net-framework
ms.reviewer: 
ms.suite: 
ms.technology:
- dotnet-clr
ms.tgt_pltfrm: 
ms.topic: article
dev_langs:
- VB
- CSharp
- C++
- jsharp
helpviewer_keywords:
- in-process side-by-side execution
- side-by-side execution, in-process
ms.assetid: 18019342-a810-4986-8ec2-b933a17c2267
caps.latest.revision: 25
author: mairaw
ms.author: mairaw
manager: wpickett
ms.translationtype: HT
ms.sourcegitcommit: 306c608dc7f97594ef6f72ae0f5aaba596c936e1
ms.openlocfilehash: 5ad204e06868b21ac6f37bbdf02d29670a284496
ms.contentlocale: ja-jp
ms.lasthandoff: 07/28/2017

---
# <a name="in-process-side-by-side-execution"></a>インプロセスの side-by-side 実行
[!INCLUDE[net_v40_long](../../../includes/net-v40-long-md.md)] 以降では、インプロセスの side-by-side ホスティングを使用して、1 つのプロセスで複数のバージョンの共通言語ランタイム (CLR) を実行できます。 既定では、マネージ COM コンポーネントは、プロセスに読み込まれている .NET Framework のバージョンに関係なく、コンポーネントがビルドされた .NET Framework のバージョンで実行されます。  
  
## <a name="background"></a>背景  
 .NET Framework ではマネージ コード アプリケーションに対して常に side-by-side ホスティングが提供されてきましたが、[!INCLUDE[net_v40_short](../../../includes/net-v40-short-md.md)] より前のバージョンでは、マネージ COM コンポーネントについてはこの機能は提供されませんでした。 以前は、プロセスに読み込まれたマネージ COM コンポーネントは、既に読み込まれているランタイムのバージョン、またはインストールされている .NET Framework の最新バージョンで実行されました。 このバージョンが COM コンポーネントと互換性がない場合、コンポーネントは実行できませんでした。  
  
 [!INCLUDE[net_v40_short](../../../includes/net-v40-short-md.md)] が備える side-by-side ホスティングの新しいアプローチでは、次のことが保証されます。  
  
-   .NET Framework の新しいバージョンをインストールしても、既存のアプリケーションに影響はありません。  
  
-   アプリケーションは、それがビルドされたバージョンの .NET Framework に対して実行されます。 明示的に指示しない限り、新しいバージョンの .NET Framework は使われません。 ただし、新しいバージョンの .NET Framework を使うようにアプリケーションを移行する方が簡単です。  
  
## <a name="effects-on-users-and-developers"></a>ユーザーと開発者への影響  
  
-   **エンドユーザーとシステム管理者**。 これらのユーザーについては、単独で、またはアプリケーションと共に、ランタイムの新しいバージョンをインストールしても、コンピューターに影響がないことが、これまで以上に確実になっています。 既存のアプリケーションは引き続きこれまでと同じように動作します。  
  
-   **アプリケーション開発者**。 Side-by-side ホスティングは、アプリケーション開発者に対する影響はほとんどありません。 既定では、アプリケーションはそれがビルドされた .NET Framework のバージョンで常に実行されます。これは変更されていません。 ただし、開発者はこの動作をオーバーライドし、新しいバージョンの .NET Framework で実行するようアプリケーションに指示できます ([シナリオ 2](#scenarios) をご覧ください)。  
  
-   **ライブラリ開発者とコンシューマー**。 ライブラリ開発者が直面する互換性の問題は、side-by-side ホスティングでは解決されません。 アプリケーションによって (直接参照または <xref:System.Reflection.Assembly.Load%2A?displayProperty=fullName> の呼び出しにより) 直接読み込まれるライブラリは、それが読み込まれる <xref:System.AppDomain> のランタイムを引き続き使います。 サポートする .NET Framework のすべてのバージョンについて、ライブラリをテストする必要があります。 [!INCLUDE[net_v40_short](../../../includes/net-v40-short-md.md)] ランタイムを使ってコンパイルされているアプリケーションに、それより前のランタイムを使ってビルドされたライブラリが含まれる場合は、そのライブラリも [!INCLUDE[net_v40_short](../../../includes/net-v40-short-md.md)] ランタイムを使います。 一方、ランタイムを使ってビルドされたアプリケーションに、[!INCLUDE[net_v40_short](../../../includes/net-v40-short-md.md)] を使ってビルドされたライブラリが含まれる場合は、アプリケーションも [!INCLUDE[net_v40_short](../../../includes/net-v40-short-md.md)] を使うように強制する必要があります ([シナリオ 3](#scenarios) をご覧ください)。  
  
-   **マネージ COM コンポーネントの開発者**。 以前は、マネージ COM コンポーネントはコンピューターにインストールされている最新バージョンのランタイムを使って自動的に実行しました。 現在は、ビルドされたバージョンのランタイムに対して COM コンポーネントを実行できるようになりました。  
  
     次の表で示すように、.NET Framework バージョン 1.1 でビルドされたコンポーネントは、バージョン 4 のコンポーネントとであれば side-by-side で実行できますが、バージョン 2.0、3.0、3.5 のコンポーネントとは、これらのバージョンでは side-by-side ホスティングを使用できないために side-by-side では実行できません。  
  
    |.NET Framework のバージョン|1.1|2.0 - 3.5|4|  
    |----------------------------|---------|----------------|-------|  
    |1.1|該当なし|いいえ|はい|  
    |2.0 - 3.5|いいえ|該当なし|はい|  
    |4|はい|はい|該当なし|  
  
> [!NOTE]
>  .NET Framework バージョン 3.0 および 3.5 はバージョン 2.0 に対して増分的にビルドされているため、side-by-side で実行する必要はありません。 これらは、本質的に同じバージョンです。  
  
<a name="scenarios"></a>   
## <a name="common-side-by-side-hosting-scenarios"></a>side-by-side ホスティングの一般的なシナリオ  
  
-   **シナリオ 1:** 以前のバージョンの .NET Framework でビルドされた COM コンポーネントを使うネイティブ アプリケーション。  
  
     インストールされている .NET Framework のバージョン: [!INCLUDE[net_v40_short](../../../includes/net-v40-short-md.md)] および COM コンポーネントによって使われている他のすべての .NET Framework のバージョンの場合。  
  
     対処方法: このシナリオの場合は、何も行いません。 COM コンポーネントは、登録された .NET Framework のバージョンで実行されます。  
  
-   **シナリオ 2**: [!INCLUDE[net_v20SP1_short](../../../includes/net-v20sp1-short-md.md)] でビルドされたマネージ アプリケーションを、できれば [!INCLUDE[dnprdnext](../../../includes/dnprdnext-md.md)] で実行したいが、バージョン 2.0 が存在しない場合は [!INCLUDE[net_v40_short](../../../includes/net-v40-short-md.md)] で実行したい場合。  
  
     インストールされている .NET Framework のバージョン: 以前のバージョンの .NET Framework と [!INCLUDE[net_v40_short](../../../includes/net-v40-short-md.md)]。  
  
     対処方法: アプリケーション ディレクトリの[アプリケーション構成ファイル](../../../docs/framework/configure-apps/index.md)で、次のように設定された [\<startup> 要素](../../../docs/framework/configure-apps/file-schema/startup/startup-element.md)と [\<supportedRuntime> 要素](../../../docs/framework/configure-apps/file-schema/startup/supportedruntime-element.md)を使います。  
  
    ```xml  
    <configuration>  
      <startup >  
        <supportedRuntime version="v2.0.50727" />  
        <supportedRuntime version="v4.0" />  
      </startup>  
    </configuration>  
    ```  
  
-   **シナリオ 3:** 以前のバージョンの .NET Framework でビルドされた COM コンポーネントを使うネイティブ アプリケーションを、[!INCLUDE[net_v40_short](../../../includes/net-v40-short-md.md)] で実行したい場合。  
  
     インストールされている .NET Framework のバージョン: [!INCLUDE[net_v40_short](../../../includes/net-v40-short-md.md)]。  
  
     対処方法: アプリケーション ディレクトリのアプリケーション構成ファイルで、`useLegacyV2RuntimeActivationPolicy` 属性と `true` に設定した `<startup>` 要素と、次のように設定された `<supportedRuntime>` 要素を使います。  
  
    ```xml  
    <configuration>  
      <startup useLegacyV2RuntimeActivationPolicy="true">  
        <supportedRuntime version="v4.0" />  
      </startup>  
    </configuration>  
    ```  
  
## <a name="example"></a>例  
 次の例では、コンポーネントがコンパイルされた .NET Framework のバージョンを使うことでマネージ COM コンポーネントを実行しているアンマネージ COM ホストを示します。  
  
 次の例を実行するには、[!INCLUDE[net_v35_long](../../../includes/net-v35-long-md.md)] を使って次のマネージ COM コンポーネントをコンパイルして登録します。 コンポーネントを登録するには、**[プロジェクト]** メニューの **[プロパティ]** をクリックし、**[ビルド]** タブをクリックして、**[COM の相互運用機能に登録]** チェック ボックスをオンにします。  
  
```  
using System;  
using System.Collections.Generic;  
using System.Linq;  
using System.Text;  
using System.Runtime.InteropServices;  
  
namespace BasicComObject  
{  
    [ComVisible(true), Guid("9C99C4B5-CA54-4c58-8988-49B6811BA53B")]  
    public class MyObject : SimpleObjectModel.IPrintInfo  
    {  
        public MyObject()  
        {  
        }  
        public void PrintInfo()  
        {  
            Console.WriteLine("MyObject was activated in {0} runtime in:\n\tAppDomain {1}:{2}", System.Runtime.InteropServices.RuntimeEnvironment.GetSystemVersion(), AppDomain.CurrentDomain.Id, AppDomain.CurrentDomain.FriendlyName);  
        }  
    }  
}  
```  
  
 次のアンマネージ C++ アプリケーションをコンパイルすると、前の例で作成した COM オブジェクトがアクティブ化すされます。  
  
```  
#include "stdafx.h"  
#include <string>  
#include <iostream>  
#include <objbase.h>  
#include <string.h>  
#include <process.h>  
  
using namespace std;  
  
int _tmain(int argc, _TCHAR* argv[])  
{  
    char input;  
    CoInitialize(NULL) ;  
    CLSID clsid;  
    HRESULT hr;  
    HRESULT clsidhr = CLSIDFromString(L"{9C99C4B5-CA54-4c58-8988-49B6811BA53B}",&clsid);  
    hr = -1;  
    if (FAILED(clsidhr))  
    {  
        printf("Failed to construct CLSID from String\n");  
    }  
    UUID id = __uuidof(IUnknown);  
    IUnknown * pUnk = NULL;  
    hr = ::CoCreateInstance(clsid,NULL,CLSCTX_INPROC_SERVER,id,(void **) &pUnk);  
    if (FAILED(hr))  
    {  
        printf("Failed CoCreateInstance\n");  
    }else  
    {  
        pUnk->AddRef();  
        printf("Succeeded\n");  
    }  
  
    DISPID dispid;  
    IDispatch* pPrintInfo;  
    pUnk->QueryInterface(IID_IDispatch, (void**)&pPrintInfo);  
    OLECHAR FAR* szMethod[1];  
    szMethod[0]=OLESTR("PrintInfo");   
    hr = pPrintInfo->GetIDsOfNames(IID_NULL,szMethod, 1, LOCALE_SYSTEM_DEFAULT, &dispid);  
    DISPPARAMS dispparams;  
    dispparams.cNamedArgs = 0;  
    dispparams.cArgs = 0;  
    VARIANTARG* pvarg = NULL;  
    EXCEPINFO * pexcepinfo = NULL;  
    WORD wFlags = DISPATCH_METHOD ;  
;  
    LPVARIANT pvRet = NULL;  
    UINT * pnArgErr = NULL;  
    hr = pPrintInfo->Invoke(dispid,IID_NULL, LOCALE_USER_DEFAULT, wFlags,  
        &dispparams, pvRet, pexcepinfo, pnArgErr);  
    printf("Press Enter to exit");  
    scanf_s("%c",&input);  
    CoUninitialize();  
    return 0;  
}  
```  
  
## <a name="see-also"></a>関連項目  
 [\<startup> 要素](../../../docs/framework/configure-apps/file-schema/startup/startup-element.md)   
 [\<<supportedRuntime> 要素](../../../docs/framework/configure-apps/file-schema/startup/supportedruntime-element.md)

