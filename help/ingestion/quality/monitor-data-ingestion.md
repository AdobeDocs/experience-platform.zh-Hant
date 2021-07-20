---
keywords: Experience Platform；首頁；熱門主題；監控；監控；資料流；監控擷取；資料擷取；資料擷取；檢視記錄；檢視批次；
solution: Experience Platform
title: 監控資料擷取
topic-legacy: overview
description: 本使用手冊提供如何在Adobe Experience Platform使用者介面中監控資料的步驟。 本指南要求您擁有Adobe ID和Adobe Experience Platform的存取權。
exl-id: 85711a06-2756-46f9-83ba-1568310c9f73
source-git-commit: 3fadf7006c8ea058e469067b61950ed2d2d12e3f
workflow-type: tm+mt
source-wordcount: '618'
ht-degree: 0%

---

# 監控資料擷取

資料內嵌可讓您將資料內嵌至Adobe Experience Platform。 您可以使用批次內嵌(可讓您使用各種檔案類型（例如CSV）插入資料)或串流內嵌（可讓您使用串流端點即時將資料內嵌至[!DNL Platform]）。

本使用手冊提供如何在Adobe Experience Platform使用者介面中監控資料的步驟。 本指南要求您擁有Adobe ID和Adobe Experience Platform的存取權。

## 監控串流端對端資料擷取

在[Experience PlatformUI](https://platform.adobe.com)中，在左側導覽功能表中選取&#x200B;**[!UICONTROL 監控]**，然後選取&#x200B;**[!UICONTROL 串流端對端]**。

此時將顯示&#x200B;**[!UICONTROL 流端到端]**&#x200B;監視頁。 此工作區提供顯示[!DNL Platform]接收的流式事件的速率的圖形、顯示[[!DNL Real-time Customer Profile]](../../profile/home.md)成功處理的流式事件的速率的圖形，以及傳入資料的詳細清單。

![](../images/quality/monitor-data-flows/list-streams.png)

依預設，頂端圖表會顯示過去七天的擷取率。 您可以選取醒目提示的按鈕，調整此日期範圍以顯示不同的時段。

![](../images/quality/monitor-data-flows/events-received.png)

下圖顯示過去七天內[!DNL Profile]成功處理串流事件的比率。 您可以選取醒目提示的按鈕，調整此日期範圍以顯示不同的時段。

>[!NOTE]
>
>若要在此圖表上顯示資料，資料必須為&#x200B;**deplicy**&#x200B;啟用[!DNL Profile]。 若要了解如何為[!DNL Profile]啟用串流資料，請參閱[資料集使用手冊](../../catalog/datasets/user-guide.md#enable-a-dataset-for-real-time-customer-profile)。

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
>如果擷取的列中發生錯誤，除非產生的訊息導致無效的XDM，否則會捨棄這些列&#x200B;**not**。

![](../images/quality/monitor-data-flows/failed-batch-error.png)

## 監控批次端對端資料內嵌

在[[!DNL Experience Platform UI]](https://platform.adobe.com)中，選擇左側導航菜單上的&#x200B;**[!UICONTROL 監視]**。

此時將顯示「**[!UICONTROL 批次端到端]**&#x200B;監視」頁，其中顯示先前導入的批的清單。 您可以選擇任何批，以獲得有關該記錄的更詳細資訊。

![](../images/quality/monitor-data-flows/batch-monitoring.png)

### 查看批

查看成功批次的詳細資訊時，將顯示所獲取的記錄數、檔案大小以及所獲取的開始和結束時間等資訊。

![](../images/quality/monitor-data-flows/successful-batch.png)

失敗批次的詳細資訊顯示的資訊與成功批次的資訊相同，同時增加失敗記錄數。

![](../images/quality/monitor-data-flows/failed-batch.png)

此外，失敗的批提供了處理批時發生錯誤的詳細資訊。 在以下範例中，擷取的批次發生錯誤，因為該批次具有該人員的最大身分數量。

>[!NOTE]
>
>如果擷取的列中發生錯誤，除非產生的訊息導致無效的XDM，否則會捨棄這些列&#x200B;**not**。

![](../images/quality/monitor-data-flows/failed-streaming-error.png)
