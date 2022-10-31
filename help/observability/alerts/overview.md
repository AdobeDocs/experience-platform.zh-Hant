---
keywords: Experience Platform；首頁；熱門主題；日期範圍
title: 警報概述
description: 了解 Adobe Experience Platform 中的警告，包括定義警告規則的結構。
feature: Alerts
exl-id: c38a93c6-1618-4ef9-8f94-41c7ab4af43c
source-git-commit: b1c82169056e66b9cdcf99f73daa7d37a3a01600
workflow-type: tm+mt
source-wordcount: '760'
ht-degree: 5%

---

# 警報概觀

Adobe Experience Platform可讓您訂閱Adobe Experience Platform活動的事件型警報。 警報減少或消除輪詢 [[!DNL Observability Insights] API](../api/overview.md) 為了檢查作業是否已完成、是否已到達工作流中的某個里程碑，或是否發生任何錯誤。

當您的Platform作業達到特定條件集時（例如，當系統違反臨界值時，可能會發生問題）,Platform會將警報訊息傳送給組織中已訂閱的任何使用者。 這些訊息可在預先定義的時間間隔內重複，直到解析警報為止。

本檔案概述Adobe Experience Platform中的警報，包括如何定義警報規則的結構。

## 一次性警報與重複警報

平台警報可以傳送一次，也可以在預先定義的間隔內重複，直到解決為止。 這些選項的使用案例會以下列方式有所不同：

| 一次性警報 | 重複警報 |
| --- | --- |
| 不一定表示有問題。 | 表示可能不需要的狀態。 |
| 不會重複。 | 如果異常狀況持續存在，則可重複。 |
| 例如：<ul><li>資料擷取已成功完成。</li><li>查詢執行已完成。</li><li>資料已刪除。</li></ul> | 例如：<ul><li>擷取持續時間超過服務層級合約(SLA)。</li><li>過去24小時內並未發生每日擷取。</li><li>流處理器的錯誤率高於配置的閾值。</li><li>設定檔總數超過權限。</li></ul> |

{style=&quot;table-layout:auto&quot;}

## 警報解剖

警報可劃分為下列元件：

| 元件 | 說明 |
| --- | --- |
| **量度** | 可觀察性 [量度](../api/metrics.md#available-metrics) 其值會觸發警報，例如失敗的批次擷取事件數(`timeseries.ingestion.dataset.batchfailed.count`)。 |
| **條件** | 與量度相關的條件，如果解析為true，就會觸發警報，例如計數量度超過特定數字。 此條件可與預先定義的時間視窗相關聯。 |
| **視窗** | （可選）警報的條件可限制為預先定義的時間窗口。 例如，根據過去五分鐘內失敗批次的數量，可能會觸發警報。 |
| **動作** | 觸發警報時，會執行動作。 具體而言，訊息會透過傳遞通道(例如預先設定的Webhook或Experience PlatformUI)傳送給適用的收件者。 |
| **頻率** | （選用）如果警報的條件維持為true或未解析，則可將警報設定為以定義的間隔重複其動作。 |

{style=&quot;table-layout:auto&quot;}

## 接收和管理警報

可以通過兩個通道接收和管理警報：

* [Adobe I/O事件](#events)
* [平台UI](#ui)

### I/O事件 {#events}

警報可傳送至已設定的WebHook，以有效自動化活動監控。 若要透過網頁連結接收警報，您必須在Adobe Developer Console中註冊您的網頁連結，以取得平台警報。 請參閱 [訂閱Adobe I/O事件通知](./subscribe.md) ，以了解特定步驟。

### 平台UI {#ui}

平台UI可讓您檢視收到的警報，並管理警報規則。 以下影片會介紹這些功能。

>[!VIDEO](https://video.tv.adobe.com/v/336218?quality=12&learn=on)

若要在Platform UI中處理警報，您必須透過Adobe Admin Console啟用下列存取控制權限：

| 權限 | 說明 |
| --- | --- |
| 檢視警報 | 允許您查看已接收的警報消息。 |
| 查看警報歷史記錄* | 可讓您透過 [!UICONTROL 警報] 標籤。 |
| 管理警報* | 可讓您透過 [!UICONTROL 警報] 標籤。 |
| 解決警報* | 可讓您透過 [!UICONTROL 警報] 標籤。 |

{style=&quot;table-layout:auto&quot;}

**若要存取 [!UICONTROL 警報] 標籤中，您還必須獲得「檢視警報」權限，並結合其他權限之一。*

>[!NOTE]
>
>如需如何在Platform中管理權限的詳細資訊，請參閱 [存取控制檔案](../../access-control/ui/overview.md).

透過「檢視警報」權限，您可以選取警鈴圖示(![鐘錶徵圖](../images/alerts/overview/icon.png))。

![](../images/alerts/overview/ui.png)

>[!NOTE]
>
> 選取警報以導覽至相關控制面板，以取得觸發警報的原因的詳細資訊。

此外， [!UICONTROL 警報] 「 」標籤可讓個別使用者訂閱特定警報類型，並讓管理員完全啟用或停用警報規則。 請參閱 [UI指南](./ui.md) 以了解有關管理警報的詳細資訊。

## 後續步驟

閱讀本檔案後，您便了解Platform警報及其在Platform生態系統中的角色。 請參閱本概述中連結至的程式檔案，了解如何接收及管理警報。
