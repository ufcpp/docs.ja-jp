---
title: "上の理由がリフト アンド シフトの既存のクラウド DevOps 対応アプリケーションへアプリ用 .NET"
description: "コンテナーの .NET アプリケーションの .NET Microservices アーキテクチャ |上の理由がリフト アンド シフトの既存のクラウド DevOps 対応アプリケーションへアプリ用 .NET"
author: CESARDELATORRE
ms.author: wiwagn
ms.date: 10/26/2017
ms.openlocfilehash: 941ca8d8fcb4d69f60282737851ab3e86b5782d4
ms.sourcegitcommit: 4f3fef493080a43e70e951223894768d36ce430a
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/21/2017
---
# <a name="reasons-to-lift-and-shift-existing-net-apps-to-cloud-devops-ready-applications"></a>上の理由がリフト アンド シフトの既存のクラウド DevOps 対応アプリケーションへアプリ用 .NET

クラウド DevOps 対応アプリケーションでは、短時間でおよび繰り返しを配信できますを顧客に信頼性の高いアプリケーション。 プラットフォーム、アプリの運用の複雑さの多くを遅らせることで重要な機敏性と信頼性を取得します。

アプリを出荷する時点で、すばやく市場にアプリケーションを取得できない場合が対象とする、市場が進化してきました。 アプリケーションを設計またはエンジニア リングどの程度に関係なく、遅すぎますする必要があります。 か可能性が失敗して、市場のニーズを持つアプリの配信を同期することはできませんので、最大限に到達しません。

ビジネスの継続的な技術革新の必要性は、制限を開発および運用チームをプッシュします。 ビジネスの継続的な技術革新に必要な機敏性を実現する唯一の方法では、コンテナーと特定のクラウド DevOps 対応アプリケーションの基本原則のようなテクノロジを使用してアプリケーションを刷新してです。

一番下の行はこと組織では、ビルドし、クラウド DevOps の準備完了であるアプリケーションを管理、顧客の手に先にソリューションを配置したりできます市場で、該当するときに新しいアイデアです。

## <a name="cloud-devops-ready-application-principles-and-tenets"></a>クラウド DevOps 対応アプリケーションの基本原則と基本思想 

クラウドの機能強化は次の 2 つの目標を達成に焦点を合わせた: コストの削減、および機敏性を向上させることによってビジネスの成長を改善します。 これらの目標は、プロセスを簡略化し、リリースのアプリケーションの出荷すると、摩擦を減らすことによって実現されます。

することで、アジャイル場合、で、アプリケーションはクラウド DevOps 対応方法-自律的に他の内部設置型アプリからのアプリケーションの開発しし、リリースは、展開、自動スケール、監視、およびクラウドでアプリをトラブルシューティングします。

キーが*アジリティ*です。 任意の展開の運用を最小限に減らす場合を除き、機敏性と出荷することはできませんの問題と開発/テスト環境の問題です。 コンテナー (具体的には、Docker、事実上の標準として) と管理サービスは、この目的のために設計されました。

機敏性を実現するためには、クラウドでのスケーラブルなプラットフォームにリリースされる CI/CD パイプラインに基づく自動の DevOps プロセスも必要です。 (Azure Service Fabric Kubernetes など) の拡張性の高い回復力のクラウド プラットフォームに展開する (Visual Studio Team Services や Jenkins) などの CI/CD プラットフォームは、クラウド内の機敏性を実現するためのキー テクノロジです。

次の一覧は、メインの基本思想またはクラウド DevOps 対応アプリケーションのプラクティスについて説明します。 これらの原則、プログレッシブまたは増分アプローチの一部のみまたはすべてを採用することができますに注意してください。

-   **コンテナー**です。 コンテナーでは、アプリケーション自体にアプリケーションの依存関係を含める機能を提供します。 コンテナリゼーションは、実稼働環境に展開またはステージング環境でテストするときに発生する可能性が問題の数を大幅に短縮します。 最終的には、コンテナーには、アプリケーションの配信の機敏性が向上します。

-   **復元力と拡張性の高いクラウド**です。 クラウドは、管理されている、弾力性、拡張性が高く、および回復力のあるであるプラットフォームを提供します。 これらの特性は、コストの機能強化を取得し、アプリケーションの出荷を高可用性と信頼性を継続的配信のための基本です。 管理サービスなどのマネージ データベース、管理サービス (CaaS)、および管理される記憶域は、アプリケーションのメンテナンス コストの軽減に根本的な部分をキャッシュします。

-   **監視**です。 信頼性の高いアプリケーションは、しなくても検出および例外とアプリケーションのパフォーマンスの問題を診断することをお勧めはできません。 アプリケーション パフォーマンスの管理およびインスタント分析を使用して実用的な洞察を取得する必要があります。

-   **DevOps カルチャと継続的な配信**です。 クラウド DevOps の準備完了のプラクティスを採用するには、チームが不要になった独立サイロで作業するカルチャの変更が必要です。 CI/CD パイプラインが、開発チームと IT 運用チーム、コンテナーと CI/CD ツールでサポートされている間の向上の共同作業がある場合にのみ可能です。

図 4-2 は、クラウド DevOps 対応アプリケーションのメインの省略可能な柱を示しています。 以上柱を実装する、readier、アプリケーションは、顧客の期待を満たすで成功します。

> ![クラウド DevOps 対応アプリケーションのメインの柱](./media/image2.png)
>
> **図 4-2 です。** クラウド DevOps 対応アプリケーションのメインの柱

要約すると、クラウド DevOps 対応アプリケーションは、クラウド コンテナー、管理されたクラウド インフラストラクチャ、回復力のあるアプリケーション手法の組み合わせを使用しているときに、モデルをコンピューティングを活用したを構築し、アプリケーションを管理する方法監視、継続的な配信、および DevOps をすべて再構築し、既存のアプリケーションを書き直す必要はありません。

組織は、徐々 にこれらのテクノロジおよびアプローチ採用できます。 一度にすべての問題をすべてを採用する必要はありません。 導入できますにインクリメント方式でエンタープライズの優先度とユーザーのニーズによって異なります。

## <a name="benefits-of-a-cloud-devops-ready-application"></a>クラウド DevOps 対応アプリケーションの利点

(せずに再設計やコーディング) クラウド DevOps 対応アプリケーションに既存のアプリケーションを変換することで、次の利点を取得できます。

-   **管理されたインフラストラクチャはクラウド プロバイダーによって処理されるため、コストを削減**です。 DevOps の準備完了のクラウド アプリケーションでは、クラウドの既定の柔軟性、autoscale、および高可用性を使用して、クラウドの利点を取得します。 利点はコンピューティング機能 (Vm とコンテナー) するだけでなく関連しますが、クラウド内のリソースにも依存 DBaaS、CaaS、および任意のインフラストラクチャと同様に、アプリケーションがありますが必要です。

-   **回復力のあるアプリケーションとインフラストラクチャ**です。 クラウドに移行する場合は、; 一時的な障害を受け入れる必要があります。クラウド内の障害が発生します。 また、クラウド インフラストラクチャとハードウェアは、「置き換え可能な」が一時的なダウンタイムの営業案件の増加です。 同時に、内部クラウド機能と回復性を実装し、復旧を自動化する特定のアプリケーション開発の手法やすくはるか、クラウド内の予期しない障害から復旧します。

-   **アプリケーションのパフォーマンスがさらに深い洞察**です。 クラウドの監視ツールを Azure Application Insights の正常性の管理、ログ、および通知のビジュアル化を提供するようにします。 監査は、アプリケーションを簡単にデバッグおよび監査を記録します。 これは、信頼性の高いクラウド アプリケーションの基本的なです。

-   **アジャイルの展開でのアプリケーションの移植性**です。 コンテナー (Linux または Windows のいずれかのコンテナーが Docker エンジンに基づく) では、クラウドがロックされているアプリケーションを防ぐに最適なソリューションを提供します。 コンテナー、Docker ホスト、および複数のクラウド orchestrators を使用すると、簡単に 1 つの環境から移動したり、別のクラウドできます。 コンテナーは、通常のどの環境でも (ステージ/テスト/運用) への展開で発生する競合を排除します。

すべてこれらの利点の最終的なエンド ツー エンドのアプリケーションのライフ サイクルのキーのコストの削減を提供します。

次のセクションでは、これらの利点はさらに詳しく説明し、特定のテクノロジにリンクされています。

>[!div class="step-by-step"]
[前へ](index.md)
[次へ](microsoft-technologies-in-cloud-devops-ready-applications.md)