---
keywords: Experience Platform；首頁；熱門主題；警報
description: 建立資料流時，您可以訂閱警報，接收有關流運行狀態、成功或失敗的警報消息。
title: 在UI中訂閱內容內警報
hide: true
hidefromtoc: true
source-git-commit: a81d21f615206e644044c2f0f546a458d1aebbf3
workflow-type: tm+mt
source-wordcount: '282'
ht-degree: 0%

---

# 訂閱警報消息，以監視UI中的源資料流

Adobe Experience Platform可讓您訂閱Adobe Experience Platform活動的事件型警報。 警報減少或消除輪詢 [[!DNL Observability Insights] API](../../../observability/api/overview.md) 為了檢查作業是否已完成、是否已到達工作流中的某個里程碑，或是否發生任何錯誤。

建立資料流時，您可以訂閱警報，接收有關流運行狀態、成功或失敗的警報消息。

本檔案提供如何訂閱警報及接收流程執行之警報訊息的步驟。

## 快速入門

本檔案需要妥善了解下列Adobe Experience Platform元件：

* [來源](../../home.md): [!DNL Experience Platform] 可讓您從各種來源擷取資料，同時使用來建構、加標籤及增強傳入資料 [!DNL Platform] 服務。
* [可觀察性](../../../observability/home.md): [!DNL Observability Insights] 可讓您透過使用統計量度和事件通知來監控Platform活動。
   * [警報](../../../observability/alerts/overview.md):當您的Platform作業達到特定條件集時（例如，當系統違反臨界值時，可能會發生問題）,Platform會將警報訊息傳送給組織中已訂閱的任何使用者。

## 在UI中訂閱警報 {#subscribe-sources-alerts}

>[!CONTEXTUALHELP]
>id="platform_sources_alerts_subscribe"
>title="訂閱源警報"
>abstract="警報允許您根據源資料流的狀態接收通知。 如果資料流已啟動、成功、失敗或未內嵌任何資料，則可以設定警報通知來獲取更新。"
>text="Learn more in documentation"
