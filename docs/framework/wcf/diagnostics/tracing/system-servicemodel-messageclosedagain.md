---
title: "System.ServiceModel.MessageClosedAgain | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 24c274d4-65cd-4c91-9869-bc6eb34ef979
caps.latest.revision: 6
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 6
---
# System.ServiceModel.MessageClosedAgain
System.ServiceModel.MessageClosedAgain  
  
## 説明  
 メッセージがもう一度閉じられました。  
  
 メッセージを閉じることができるのは一度だけです。このトレースがユーザー拡張コード内で出力されている場合は、ユーザー拡張コードは既に閉じられているメッセージをさらに閉じようとしていることが示されています。このトレースが製品のコード内で出力されている場合は、ユーザー拡張コードがメッセージを閉じるのが早すぎる可能性があることが示されています。  
  
## 参照  
 [トレース](../../../../../docs/framework/wcf/diagnostics/tracing/index.md)   
 [トレースを使用したアプリケーションのトラブルシューティング](../../../../../docs/framework/wcf/diagnostics/tracing/using-tracing-to-troubleshoot-your-application.md)   
 [管理と診断](../../../../../docs/framework/wcf/diagnostics/index.md)