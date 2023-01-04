---
keywords: Experience Platform；首頁；熱門主題；監控；監控；資料流；監控擷取；資料擷取；資料擷取；檢視記錄；檢視批次；
solution: Experience Platform
title: 監控資料擷取
topic-legacy: overview
description: 本使用手冊提供如何在Adobe Experience Platform使用者介面中監控資料的步驟。 本指南要求您擁有Adobe ID和Adobe Experience Platform的存取權。
exl-id: 85711a06-2756-46f9-83ba-1568310c9f73
source-git-commit: 34e0381d40f884cd92157d08385d889b1739845f
workflow-type: tm+mt
source-wordcount: '654'
ht-degree: 0%

---

# 監控資料擷取

資料內嵌可讓您將資料內嵌至Adobe Experience Platform。 您可以使用批次內嵌(可讓您使用各種檔案類型（例如CSV）插入資料)或串流內嵌(可讓您將資料內嵌至 [!DNL Platform] 即時使用串流端點。

本使用手冊提供如何在Adobe Experience Platform使用者介面中監控資料的步驟。 本指南要求您擁有Adobe ID和Adobe Experience Platform的存取權。

## 監控串流端對端資料擷取 {#monitor-streaming-end-to-end-data-ingestion}

>[!CONTEXTUALHELP]
>id="platform_ingestion_streaming_ingestionrate"
>title="擷取率"
>abstract="每秒成功處理的事件數。"
>text="Learn more in the documentation"
>additional-url="http://www.adobe.com/go/monitor-dataflows-en" text="監視UI中源的資料流"

>[!TIP]
>
>若要計算特定日期的事件總數，請使用下列運算式： `total events / day = ingestion rate * 60 * 60 * 24`.

在 [Experience PlatformUI](https://platform.adobe.com)，選取 **[!UICONTROL 監控]** 在左側導覽功能表上，後面接著 **[!UICONTROL 端對端串流]**.

此 **[!UICONTROL 端對端串流]** 監視頁面。 此工作區提供一個圖表，顯示接收的串流事件的速率 [!DNL Platform]，此圖表顯示成功處理的串流事件的速率 [[!DNL Real-Time Customer Profile]](../../profile/home.md)，以及傳入資料的詳細清單。

![](../images/quality/monitor-data-flows/list-streams.png)

依預設，頂端圖表會顯示過去七天的擷取率。 您可以選取醒目提示的按鈕，調整此日期範圍以顯示不同的時段。

![](../images/quality/monitor-data-flows/events-received.png)

下圖顯示成功處理串流事件的比率，依 [!DNL Profile] 過去七天。 您可以選取醒目提示的按鈕，調整此日期範圍以顯示不同的時段。

>[!NOTE]
>
>若要讓資料顯示在此圖表上，資料必須 **顯式** 啟用 [!DNL Profile]. 了解如何為 [!DNL Profile]，請閱讀 [資料集使用指南](../../catalog/datasets/user-guide.md#enable-a-dataset-for-real-time-customer-profile).

![](../images/quality/monitor-data-flows/ingested-by-profile.png)

圖形下方是與上方顯示的日期範圍對應的所有串流獲取記錄清單。 列出的每個批次都會顯示其ID、資料集名稱、上次更新時的記錄數，以及錯誤數（如果有的話）。 您可以選取任何記錄，以取得有關該記錄的詳細資訊。

![](../images/quality/monitor-data-flows/streams.png)

### 檢視串流記錄

查看成功流式記錄的詳細資訊時，將顯示諸如已獲取記錄數、檔案大小、獲取開始和結束時間等資訊。

![](../images/quality/monitor-data-flows/successful-streaming.png)

失敗流記錄的詳細資訊顯示的資訊與成功記錄相同。

![](../images/quality/monitor-data-flows/failed-batch.png)

此外，失敗記錄提供了處理批時發生錯誤的詳細資訊。 在以下範例中，轉換或驗證資料時發生剖析錯誤。

>[!NOTE]
>
>如果擷取的列中發生錯誤，這些列將 **not** 會被刪除，除非產生的訊息導致XDM無效。

![](../images/quality/monitor-data-flows/failed-batch-error.png)

## 監控批次端對端資料內嵌

在 [[!DNL Experience Platform UI]](https://platform.adobe.com)，選取 **[!UICONTROL 監控]** 的上界。

此 **[!UICONTROL 批次端對端]** 監視」頁面，顯示先前擷取的批次清單。 您可以選擇任何批，以獲得有關該記錄的更詳細資訊。

![](../images/quality/monitor-data-flows/batch-monitoring.png)

### 查看批

查看成功批次的詳細資訊時，將顯示所獲取的記錄數、檔案大小以及所獲取的開始和結束時間等資訊。

![](../images/quality/monitor-data-flows/successful-batch.png)

失敗批次的詳細資訊顯示的資訊與成功批次的資訊相同，同時增加失敗記錄數。

![](../images/quality/monitor-data-flows/failed-batch.png)

此外，失敗的批提供了處理批時發生錯誤的詳細資訊。 在以下範例中，擷取的批次發生錯誤，因為該批次具有該人員的最大身分數量。

>[!NOTE]
>
>如果擷取的列中發生錯誤，這些列將 **not** 會被刪除，除非產生的訊息導致XDM無效。

![](../images/quality/monitor-data-flows/failed-streaming-error.png)
