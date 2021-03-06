---
title: "ワークフロー ホスティングのオプション | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 37bcd668-9c5c-4e7c-81da-a1f1b3a16514
caps.latest.revision: 3
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 3
---
# ワークフロー ホスティングのオプション
[!INCLUDE[wf](../../../includes/wf-md.md)] のほとんどのサンプルでは、コンソール アプリケーションでホストされているワークフローが使用されていますが、これは実際のワークフローにとって現実的なシナリオではありません。実際のビジネス アプリケーションのワークフローは、開発者が作成した Windows サービス、[!INCLUDE[iisver](../../../includes/iisver-md.md)] や AppFabric などのサーバー アプリケーションのいずれかの永続的なプロセスでホストされます。これらの方法の違いを次に示します。  
  
## Windows AppFabric を使用した IIS でのワークフローのホスト  
 IIS と AppFabric は、ワークフローに推奨されるホストです。AppFabric を使用したワークフローのホスト アプリケーションは Windows プロセス アクティブ化サービスで、これは IIS を介した HTTP への依存関係のみを解消します。  
  
## IIS のみでのワークフローのホスト  
 [!INCLUDE[iisver](../../../includes/iisver-md.md)] のみを使用することは推奨されていません。AppFabric には、実行中のアプリケーションのメンテナンスを容易にする管理ツールと監視ツールがあるためです。ワークフローを [!INCLUDE[iisver](../../../includes/iisver-md.md)] のみでホストする必要があるのは、AppFabric への移行に関してインフラストラクチャ上の問題がある場合だけです。  
  
> [!WARNING]
>  さまざまな理由により、アプリケーション プールは [!INCLUDE[iisver](../../../includes/iisver-md.md)] によって定期的にリサイクルされます。アプリケーション プールがリサイクルされると、IIS は古いプールへのメッセージの受け取りを中止し、新しいアプリケーション プールをインスタンス化して新しい要求を受け取ります。ワークフローが応答の送信後も動作し続ける場合、[!INCLUDE[iisver](../../../includes/iisver-md.md)] は作業が完了したことを認識せず、ホスト アプリケーション プールをリサイクルする可能性があります。このような現象が発生した場合、ワークフローは中止され、追跡サービスは、\[理由\] フィールドが空になっている [1004 \- WorkflowInstanceAborted](../../../docs/framework/windows-workflow-foundation//1004-workflowinstanceaborted.md) メッセージを記録します。  
>   
>  永続化を使用する場合、ホストは、最後の永続性ポイントから、中止されたインスタンスを明示的に再開する必要があります。  
>   
>  AppFabric を使用する場合、永続化を使用すると、ワークフロー管理サービスは、最終的に、最後に成功した永続性ポイントからワークフローを再開します。永続化を使用せず、ワークフローが要求\/応答パターン以外の操作を実行している場合、ワークフローが中止されるとデータは失われます。  
  
## カスタム Windows サービスでのワークフローのホスト  
 カスタム ワークフロー サービスを作成してワークフローをホストする場合、開発者は AppFabric に標準搭載されている多くの機能を複製する必要がありますが、カスタム機能をより柔軟に使用できるようになります。このオプションは、AppFabric を選択できない場合にのみ検討してください。