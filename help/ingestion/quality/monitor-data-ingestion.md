---
keywords: Experience Platform；首頁；熱門主題；監視；監視；資料流；監視；接收；資料接收；資料接收；查看記錄；查看批；
solution: Experience Platform
title: 監視資料接收
description: 本使用手冊提供了如何在Adobe Experience Platform用戶介面中監視資料的步驟。 本指南要求您擁有Adobe ID和訪問Adobe Experience Platform。
exl-id: 85711a06-2756-46f9-83ba-1568310c9f73
source-git-commit: e802932dea38ebbca8de012a4d285eab691231be
workflow-type: tm+mt
source-wordcount: '654'
ht-degree: 3%

---

# 監視資料攝取

資料接收允許您將資料接收到Adobe Experience Platform。 您可以使用批處理接收(允許您使用各種檔案類型（如CSV）插入資料)，也可以使用流式處理接收(允許您將資料接收到 [!DNL Platform] 即時使用流端點。

本使用手冊提供了如何在Adobe Experience Platform用戶介面中監視資料的步驟。 本指南要求您擁有Adobe ID和訪問Adobe Experience Platform。

## 監視流式端到端資料接收 {#monitor-streaming-end-to-end-data-ingestion}

>[!CONTEXTUALHELP]
>id="platform_ingestion_streaming_ingestionrate"
>title="擷取率"
>abstract="每秒成功處理的事件數。"
>text="Learn more in the documentation"
>additional-url="http://www.adobe.com/go/monitor-dataflows-en" text="監視 UI 中來源的資料流"

>[!TIP]
>
>要計算特定日期上的事件總數，請使用的表達式： `total events / day = ingestion rate * 60 * 60 * 24`。

在 [Experience PlatformUI](https://platform.adobe.com)選中 **[!UICONTROL 監視]** 在左導航菜單上，然後 **[!UICONTROL 流式端到端]**。

的 **[!UICONTROL 流式端到端]** 顯示監視頁面。 此工作區提供一個圖表，顯示接收流式事件的速率 [!DNL Platform]，一個圖表，顯示已成功處理的流式事件的速率 [[!DNL Real-Time Customer Profile]](../../profile/home.md)，以及傳入資料的詳細清單。

![](../images/quality/monitor-data-flows/list-streams.png)

預設情況下，頂部圖表顯示過去七天的攝取率。 通過選擇突出顯示的按鈕，可以調整此日期範圍以顯示不同的時間段。

![](../images/quality/monitor-data-flows/events-received.png)

下圖顯示成功處理流式處理事件的速率 [!DNL Profile] 過去七天。 通過選擇突出顯示的按鈕，可以調整此日期範圍以顯示不同的時間段。

>[!NOTE]
>
>要使資料顯示在此圖表上，資料必須 **明確** 啟用 [!DNL Profile]。 瞭解如何為 [!DNL Profile]，閱讀 [資料集使用手冊](../../catalog/datasets/user-guide.md#enable-a-dataset-for-real-time-customer-profile)。

![](../images/quality/monitor-data-flows/ingested-by-profile.png)

圖表下面是與上面顯示的日期範圍對應的所有流式接收記錄的清單。 每個列出的批顯示其ID、資料集名稱、上次更新時的批記錄數以及錯誤數（如果有）。 您可以選擇任何記錄以瞭解有關該記錄的詳細資訊。

![](../images/quality/monitor-data-flows/streams.png)

### 查看流記錄

當查看成功流式傳輸記錄的詳細資訊時，將顯示資訊，如所攝取的記錄數、檔案大小以及接收開始和結束時間。

![](../images/quality/monitor-data-flows/successful-streaming.png)

失敗的流記錄的詳細資訊顯示與成功記錄相同的資訊。

![](../images/quality/monitor-data-flows/failed-batch.png)

此外，失敗的記錄提供了處理批時發生的錯誤的詳細資訊。 在下面的示例中，轉換或驗證資料時出現分析錯誤。

>[!NOTE]
>
>如果接收的行中存在錯誤，這些行將 **不** 刪除，除非生成的消息導致XDM無效。

![](../images/quality/monitor-data-flows/failed-batch-error.png)

## 監視批處理端到端資料接收

在 [[!DNL Experience Platform UI]](https://platform.adobe.com)選中 **[!UICONTROL 監視]** 按鈕。

的 **[!UICONTROL 批端到端]** 顯示「監視」頁，其中顯示先前接收的批的清單。 您可以選擇任何批以瞭解有關該記錄的詳細資訊。

![](../images/quality/monitor-data-flows/batch-monitoring.png)

### 查看批

查看成功批的詳細資訊時，會顯示接收的記錄數、檔案大小以及接收開始和結束時間等資訊。

![](../images/quality/monitor-data-flows/successful-batch.png)

失敗批的詳細資訊顯示與成功批相同的資訊，添加失敗的記錄數。

![](../images/quality/monitor-data-flows/failed-batch.png)

此外，失敗的批提供了處理批時發生的錯誤的詳細資訊。 在下面的示例中，所攝取的批出錯，因為它具有該人的最大標識數。

>[!NOTE]
>
>如果接收的行中存在錯誤，這些行將 **不** 刪除，除非生成的消息導致XDM無效。

![](../images/quality/monitor-data-flows/failed-streaming-error.png)
