---
keywords: Experience Platform；首頁；熱門主題；監控；監視；資料流程；監視擷取；資料擷取；資料擷取；檢視記錄；檢視批次；
solution: Experience Platform
title: 監控資料擷取
description: 本使用手冊提供如何在Adobe Experience Platform使用者介面中監視資料的步驟。 本指南會要求您擁有Adobe ID並存取Adobe Experience Platform。
exl-id: 85711a06-2756-46f9-83ba-1568310c9f73
source-git-commit: b48c24ac032cbf785a26a86b50a669d7fcae5d97
workflow-type: tm+mt
source-wordcount: '649'
ht-degree: 4%

---

# 監視資料攝取

資料內嵌可讓您將資料內嵌至Adobe Experience Platform。 您可以使用批次擷取，這可讓您使用各種檔案型別（例如CSV）插入資料，或是使用串流擷取，可讓您使用串流端點即時擷取您的資料到[!DNL Experience Platform]。

本使用手冊提供如何在Adobe Experience Platform使用者介面中監視資料的步驟。 本指南會要求您擁有Adobe ID並存取Adobe Experience Platform。

## 監視串流端對端資料擷取 {#monitor-streaming-end-to-end-data-ingestion}

>[!CONTEXTUALHELP]
>id="platform_ingestion_streaming_ingestionrate"
>title="擷取率"
>abstract="每秒成功處理的事件數。"
>text="Learn more in the documentation"
>additional-url="https://experienceleague.adobe.com/docs/experience-platform/dataflows/ui/monitor-sources.html?lang=zh-Hant" text="監視 UI 中來源的資料流"

>[!TIP]
>
>若要計算特定日期的總事件數，請使用下列運算式： `total events / day = ingestion rate * 60 * 60 * 24`。

在[Experience Platform UI](https://platform.adobe.com)中，選取左側導覽功能表上的&#x200B;**[!UICONTROL 監視]**，然後選取&#x200B;**[!UICONTROL 串流處理端對端]**。

顯示&#x200B;**[!UICONTROL 串流端對端]**&#x200B;監視頁面。 此工作區提供顯示[!DNL Experience Platform]接收串流事件的速率的圖表、顯示[[!DNL Real-Time Customer Profile]](../../profile/home.md)成功處理串流事件的速率的圖表，以及傳入資料的詳細清單。

![](../images/quality/monitor-data-flows/list-streams.png)

根據預設，頂端圖表會顯示過去七天的擷取率。 您可以選取醒目提示的按鈕，調整此日期範圍以顯示不同的時段。

![](../images/quality/monitor-data-flows/events-received.png)

下方圖表顯示過去7天內[!DNL Profile]成功處理串流事件的速率。 您可以選取醒目提示的按鈕，調整此日期範圍以顯示不同的時段。

>[!NOTE]
>
>資料必須明確為[!DNL Profile]啟用&#x200B;**&#x200B;**，資料才能顯示在此圖表上。 若要瞭解如何啟用[!DNL Profile]的串流資料，請閱讀[資料集使用手冊](../../catalog/datasets/user-guide.md#enable-a-dataset-for-real-time-customer-profile)。

![](../images/quality/monitor-data-flows/ingested-by-profile.png)

圖形下方是與上方顯示之日期範圍相對應的所有串流擷取記錄清單。 每個列出的批次都會顯示其ID、資料集名稱、上次更新時間、批次中的記錄數以及錯誤數（如果存在）。 您可以選取任何記錄，以取得有關該記錄的詳細資訊。

![](../images/quality/monitor-data-flows/streams.png)

### 檢視串流記錄

檢視成功串流記錄的詳細資訊時，會顯示所擷取的記錄數、檔案大小以及擷取開始和結束時間等資訊。

![](../images/quality/monitor-data-flows/successful-streaming.png)

失敗的串流記錄的詳細資訊會顯示與成功記錄相同的資訊。

![](../images/quality/monitor-data-flows/failed-batch.png)

此外，失敗的記錄會提供處理批次時發生之錯誤的詳細資料。 在以下範例中，轉換或驗證資料時出現剖析錯誤。

>[!NOTE]
>
>如果擷取的資料列發生錯誤，這些資料列&#x200B;**不會**&#x200B;被捨棄，除非產生的訊息導致無效的XDM。

![](../images/quality/monitor-data-flows/failed-batch-error.png)

## 監視批次端對端資料擷取

在[[!DNL Experience Platform UI]](https://platform.adobe.com)中，選取左側導覽功能表上的&#x200B;**[!UICONTROL 監視]**。

**[!UICONTROL 批次端對端]**&#x200B;監視頁面出現，顯示先前擷取的批次清單。 您可以選取任何批次，以取得該記錄的詳細資訊。

![](../images/quality/monitor-data-flows/batch-monitoring.png)

### 檢視批次

檢視成功批次的詳細資訊時，會顯示擷取的記錄數、檔案大小以及擷取的開始和結束時間等資訊。

![](../images/quality/monitor-data-flows/successful-batch.png)

失敗批次的詳細資訊會顯示與成功批次相同的資訊，以及失敗記錄數的增加。

![](../images/quality/monitor-data-flows/failed-batch.png)

此外，失敗的批次會提供處理批次時發生之錯誤的詳細資料。 在以下範例中，擷取的批次發生錯誤，因為它有人員的最大身分數量。

>[!NOTE]
>
>如果擷取的資料列發生錯誤，這些資料列&#x200B;**不會**&#x200B;被捨棄，除非產生的訊息導致無效的XDM。

![](../images/quality/monitor-data-flows/failed-streaming-error.png)
