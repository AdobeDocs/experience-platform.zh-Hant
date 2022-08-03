---
keywords: Experience Platform；首頁；熱門主題；日期範圍
title: 警報概述
description: 了解 Adobe Experience Platform 中的警告，包括定義警告規則的結構。
feature: Alerts
exl-id: c38a93c6-1618-4ef9-8f94-41c7ab4af43c
source-git-commit: d82487f34c0879ed27ac55e42d70346f45806131
workflow-type: tm+mt
source-wordcount: '740'
ht-degree: 5%

---

# 警報概述

Adobe Experience Platform允許您訂閱有關Adobe Experience Platform活動的基於事件的警報。 警報減少或消除輪詢 [[!DNL Observability Insights] API](../api/overview.md) 以檢查作業是否已完成、是否已達到工作流中的某個里程碑，或是否發生任何錯誤。

當平台操作中達到某組條件時（例如當系統超過閾值時可能出現的問題），平台可以向組織中已訂閱這些條件的任何用戶發送警報消息。 這些消息可以在預定義的時間間隔內重複，直到警報解決。

本文檔概述了Adobe Experience Platform州的警報，包括如何定義警報規則的結構。

## 一次性警報與重複警報

平台警報可以發送一次，也可以在預定義的時間間隔內重複，直到解決。 這些選項的使用情形可有以下不同：

| 一次性警報 | 重複警報 |
| --- | --- |
| 不一定表示有問題。 | 指示可能不需要的狀態。 |
| 不會重複。 | 如果異常情況持續存在，可以重複。 |
| 例如：<ul><li>資料接收已成功完成。</li><li>查詢執行已完成。</li><li>資料已刪除。</li></ul> | 例如：<ul><li>接收持續時間超過服務級別協定(SLA)。</li><li>過去24小時里沒有每天攝取食物。</li><li>流處理器的錯誤率高於配置的閾值。</li><li>配置檔案總數超過權利。</li></ul> |

{style=&quot;table-layout:auto&quot;}

## 警報解剖

警報可分為以下元件：

| 元件 | 說明 |
| --- | --- |
| **量度** | 可觀性 [度量](../api/metrics.md#available-metrics) 其值觸發警報，如失敗的批處理接收事件數(`timeseries.ingestion.dataset.batchfailed.count`)。 |
| **條件** | 與度量相關的條件，如果該度量解析為true，則觸發警報，例如計數度量超過特定數。 此條件可與預定義的時間窗口相關聯。 |
| **窗口** | （可選）警報的條件可限制為預定義的時間窗口。 例如，根據過去五分鐘內失敗的批次數，可能觸發警報。 |
| **動作** | 觸發警報時，將執行操作。 具體地，通過諸如預配置的網鈎或Experience PlatformUI的傳遞渠道將消息發送到適用的接收者。 |
| **頻率** | （可選）如果警報的條件仍為true或未解析，則可以將其配置為在定義的時間間隔內重複其操作。 |

{style=&quot;table-layout:auto&quot;&quot;

## 接收和管理警報

可以通過兩個通道接收和管理警報：

* [Adobe I/O事件](#events)
* [平台UI](#ui)

### I/O事件 {#events}

警報可以發送到已配置的Webhook，以便有效自動化活動監視。 要通過webhook接收警報，必須在Adobe Developer控制台中註冊webhook以獲取平台警報。 請參閱上的指南 [訂閱Adobe I/O事件通知](./subscribe.md) 的子菜單。

### 平台UI {#ui}

平台UI允許您查看已接收的警報和管理警報規則。 以下視頻介紹了這些功能。

>[!VIDEO](https://video.tv.adobe.com/v/336218?quality=12&learn=on)

要在平台UI中處理警報，您必須通過Adobe Admin Console啟用以下訪問控制權限：

| 權限 | 說明 |
| --- | --- |
| 查看警報 | 允許您查看已接收的警報消息。 |
| 查看警報歷史記錄* | 允許您通過 [!UICONTROL 警報] 頁籤。 |
| 管理警報* | 允許您通過 [!UICONTROL 警報] 頁籤。 |
| 解決警報* | 允許您通過 [!UICONTROL 警報] 頁籤。 |

{style=&quot;table-layout:auto&quot;&quot;

**為了訪問 [!UICONTROL 警報] 頁籤中，您還必須將「查看警報」權限與其他權限之一組合。*

>[!NOTE]
>
>有關如何管理平台中權限的詳細資訊，請參閱 [訪問控制文檔](../../access-control/ui/overview.md)。

使用「查看警報」權限，可以通過選擇鈴形表徵圖(![鐘形表徵圖](../images/alerts/overview/icon.png))。

![](../images/alerts/overview/ui.png)

另外， [!UICONTROL 警報] 頁籤允許單個用戶訂閱特定警報類型，並允許管理員完全啟用或禁用警報規則。 查看 [UI指南](./ui.md) 的子菜單。

## 後續步驟

通過閱讀本文檔，您已瞭解平台警報及其在平台生態系統中的角色。 請參閱本概述中連結到的流程文檔，瞭解如何接收和管理警報。
