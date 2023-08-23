---
keywords: Experience Platform；首頁；熱門主題；日期範圍
title: 警報概觀
description: 了解 Adobe Experience Platform 中的警告，包括定義警告規則的結構。
feature: Alerts
exl-id: c38a93c6-1618-4ef9-8f94-41c7ab4af43c
source-git-commit: cb889a169aa42b761b0eeff5aa7fb771ad6ed4be
workflow-type: tm+mt
source-wordcount: '796'
ht-degree: 3%

---

# 警報概觀

>[!NOTE]
>
>警報在非生產沙箱中不受支援。 為了訂閱警報，您必須確保使用生產沙箱。 當沙箱重設時，所有訂閱警報都會重設。 刪除沙箱時，所有訂閱警報也會一併清除。

Adobe Experience Platform可讓您訂閱有關Adobe Experience Platform活動的事件型警報。 警示可減少或免除輪詢下列專案的需求： [[!DNL Observability Insights] API](../api/overview.md) 以檢查工作是否已完成、工作流程中是否已達到特定里程碑，或是否已發生任何錯誤。

當您的Platform作業達到特定條件集時（例如系統違反臨界值時會發生潛在問題），Platform可以向貴組織中訂閱警報訊息的任何使用者傳送警報訊息。 這些訊息可在預先定義的時間間隔內重複，直到警報解決為止。

本檔案提供Adobe Experience Platform中警報的概觀，包括定義警報規則的結構。

## 一次性警報與重複警報

Platform警報可以只傳送一次，也可以在預先定義的間隔內重複傳送，直到解決為止。 這些選項各自的使用案例旨在以下列方式不同：

| 一次性警報 | 重複警報 |
| --- | --- |
| 不一定表示有問題。 | 表示可能不想要的狀態。 |
| 不重複。 | 如果異常狀況持續存在，可以重複此步驟。 |
| 例如：<ul><li>資料擷取已成功完成。</li><li>查詢執行已完成。</li><li>已刪除資料。</li></ul> | 例如：<ul><li>擷取持續時間超過服務等級協定(SLA)。</li><li>在過去24小時內未發生每日內嵌。</li><li>串流處理器的錯誤率高於設定的臨界值。</li><li>設定檔總數超過軟體權利檔案。</li></ul> |

{style="table-layout:auto"}

## 警示剖析

警報可以劃分為下列元件：

| 元件 | 說明 |
| --- | --- |
| **量度** | 可觀察性 [量度](../api/metrics.md#available-metrics) 其值會觸發警報，例如失敗的批次擷取事件數(`timeseries.ingestion.dataset.batchfailed.count`)。 |
| **條件** | 如果解析為true （例如計數量度超過特定數字），會觸發警示的相關量度條件。 此條件可能與預先定義的時間範圍相關聯。 |
| **視窗** | （選擇性）警示的條件可能會限制在預先定義的時間範圍內。 例如，根據過去五分鐘失敗的批次數量，可能會觸發警報。 |
| **動作** | 觸發警報時，就會執行動作。 具體來說，訊息會透過傳遞通道(例如預先設定的webhook或Experience PlatformUI)傳送給適用的收件者。 |
| **頻率** | （選擇性）如果警示的條件仍為true或未解決，則可設定警示以定義的間隔重複其動作。 |

{style="table-layout:auto"}

## 接收和管理警示

可透過兩個通道接收及管理警報：

* [Adobe I/O事件](#events)
* [平台UI](#ui)

### I/O事件 {#events}

可將警報傳送至已設定的webhook，以有效自動化活動監控。 若要透過webhook接收警報，您必須在Adobe Developer主控台中為平台警報註冊webhook 。 請參閱以下指南： [訂閱Adobe I/O事件通知](./subscribe.md) 以取得特定步驟。

### 平台UI {#ui}

Platform UI可讓您檢視收到的警報並管理警報規則。 以下影片會介紹這些功能。

>[!VIDEO](https://video.tv.adobe.com/v/336218?quality=12&learn=on)

若要在Platform UI中處理警報，您必須透過Adobe Admin Console啟用下列存取控制許可權：

| 權限 | 說明 |
| --- | --- |
| 檢視警示 | 可讓您檢視已接收的警示訊息。 |
| 檢視警示歷史記錄* | 可讓您透過 [!UICONTROL 警報] 標籤。 |
| 管理警報* | 可讓您透過啟用和停用警示規則 [!UICONTROL 警報] 標籤。 |
| 解決警示* | 可讓您透過解決觸發的警報 [!UICONTROL 警報] 標籤。 |

{style="table-layout:auto"}

**若要存取 [!UICONTROL 警報] 索引標籤上，您還必須被授予「檢視警示」許可權，同時被授與其他其中一個許可權。*

>[!NOTE]
>
>如需如何在Platform中管理許可權的詳細資訊，請參閱 [存取控制檔案](../../access-control/ui/overview.md).

有了檢視警示許可權，可以透過選取鈴鐺圖示(![鈴鐺圖示](../images/alerts/overview/icon.png))。

![](../images/alerts/overview/ui.png)

>[!NOTE]
>
> 選取警示以導覽至相關儀表板，以取得觸發警示原因的詳細資訊。

此外， [!UICONTROL 警報] UI中的索引標籤可讓個別使用者訂閱特定的警報型別，並可讓管理員完全啟用或停用警報規則。 請參閱 [UI指南](./ui.md) 以取得管理警示的詳細資訊。

## 後續步驟

閱讀本檔案後，您將瞭解Platform警報及其在Platform生態系統中的角色。 請參閱本概述中連結至的流程檔案，以瞭解如何接收和管理警報。
