---
keywords: Experience Platform;home；熱門主題；更新資料流；編輯調度
description: 本教程介紹使用Sources工作區更新資料流調度的步驟，包括其接收頻率和間隔速率。
solution: Experience Platform
title: 在UI中更新源連接資料流
topic: overview
type: Tutorial
exl-id: 0499a2a3-5a22-47b1-ac0e-76a432bd26c0
translation-type: tm+mt
source-git-commit: 3a36996b43760bc9161b8d4750a1121e9ada8d30
workflow-type: tm+mt
source-wordcount: '718'
ht-degree: 1%

---

# 在UI中更新資料流

本教程提供了有關如何使用[!UICONTROL Sources]工作區更新現有源資料流的步驟，包括有關編輯資料流調度和映射的資訊。

## 快速入門

本教學課程需要對Adobe Experience Platform的下列部分有正確的理解：

- [來源](../../home.md):Experience Platform可讓您從各種來源擷取資料，同時讓您能夠使用平台服務來建構、標示並增強傳入資料。
- [沙盒](../../../sandboxes/home.md):Experience Platform提供虛擬沙盒，可將單一平台實例分割為獨立的虛擬環境，以協助開發和發展數位體驗應用程式。

## 編輯對應

>[!NOTE]
>
>下列來源目前不支援編輯對應功能：Adobe Analytics、Adobe Audience Manager、HTTP API和[!DNL Marketo Engage]。

在平台UI中，從左側導覽器選擇&#x200B;**[!UICONTROL Sources]**&#x200B;以存取[!UICONTROL Sources]工作區。 從頂部標題中選擇&#x200B;**[!UICONTROL Dataflows]**&#x200B;以查看現有資料流清單。

![目錄](../../images/tutorials/update-dataflows/catalog.png)

[!UICONTROL Dataflows]頁包含所有現有資料流的清單，包括有關其運行狀態、上次運行日期和帳戶名的資訊。

選擇左上角的篩選器表徵圖![filter](../../images/tutorials/update/filter.png)以啟動排序面板。

![filter-dataflows](../../images/tutorials/update-dataflows/filter-dataflows.png)

排序面板提供所有可用來源的清單。 您可以從清單中選擇多個源以訪問屬於不同源的資料流的篩選選擇。

選擇要使用的源，以查看其現有資料流的清單。 在確定要更新的資料流後，請選擇帳戶名稱旁邊的省略號(`...`)。

![edit-source](../../images/tutorials/update-dataflows/edit-source.png)

此時將出現一個下拉菜單，為您提供更新所選資料流的選項。 在此處，您可以選擇更新資料流的映射集和接收調度。 您也可以選擇選項，以在監視儀表板中檢查資料流，並禁用或刪除資料流。

選擇&#x200B;**[!UICONTROL Edit source]**&#x200B;以更新其映射。

![edit-dataflow](../../images/tutorials/update-dataflows/edit-dataflow.png)

出現[!UICONTROL Add data]步驟。 選擇適當的資料格式以查看所選資料的內容，然後選擇&#x200B;**[!UICONTROL Next]**&#x200B;繼續。

![添加資料](../../images/tutorials/update-dataflows/add-data.png)

[!UICONTROL Mapping]頁面提供了一個介面，您可以在其中添加和刪除與資料集關聯的映射集。

>[!TIP]
>
>映射更新僅應用於未來計畫的資料流運行。

選擇&#x200B;**[!UICONTROL Add new mapping]**&#x200B;以添加新映射集。

![新增對應](../../images/tutorials/update-dataflows/add-new-mapping.png)

接著，輸入適當的來源欄位屬性和目標XDM欄位值，以完成您的其他對應集。 選擇&#x200B;**[!UICONTROL Next]**&#x200B;繼續。

![新增對應——新增](../../images/tutorials/update-dataflows/new-mapping-added.png)

出現[!UICONTROL Scheduling]步驟，允許您更新資料流的接收計畫，並自動使用更新的映射來接收選定的源資料。

>[!NOTE]
>
>您無法更新已排程為一次性擷取且開始時間已過去的資料流的對應集。

![調度](../../images/tutorials/update-dataflows/scheduling.png)

在[!UICONTROL Dataflow detail]頁中，可以為資料流提供更新的名稱和說明，並重新配置資料流的錯誤閾值。

提供更新值後，請選擇&#x200B;**[!UICONTROL Next]**。

![dataflow-detail](../../images/tutorials/update-dataflows/dataflow-detail.png)

出現&#x200B;**[!UICONTROL Review]**&#x200B;步驟，允許您在更新資料流之前查看資料流。

複查資料流後，請選擇&#x200B;**[!UICONTROL Finish]**&#x200B;並為要建立新映射集的資料流留出一些時間。

![審查](../../images/tutorials/update-dataflows/review.png)

## 編輯排程

要編輯現有資料流的接收調度，請選擇資料流名稱旁邊的省略號(`...`)，然後從下拉菜單中選擇&#x200B;**[!UICONTROL Edit schedule]**。

![編輯——排程](../../images/tutorials/update-dataflows/edit-schedule.png)

**[!UICONTROL Edit schedule]**&#x200B;對話框提供了更新資料流接收頻率和間隔速率的選項。 設定更新的頻率和間隔值後，請選擇&#x200B;**[!UICONTROL Save]**。

>[!NOTE]
>
>無法重新計畫已計畫進行一次性提取的資料流。

![schedule-dialog-box](../../images/tutorials/update-dataflows/schedule-dialog-box.png)

| 排程 | 說明 |
| ---------- | ----------- |
| 頻率 | 資料流收集資料的頻率。 可接受的值包括：`minute`、`hour`、`day`或`week`。 |
| 間隔 | 該間隔用於指定兩個連續流運行之間的期間。 間隔的值應為非零整數，且必須大於或等於`15`。 |

片刻後，畫面底部會出現確認方塊，確認更新是否成功。

![schedule-confirm](../../images/tutorials/update-dataflows/schedule-confirm.png)

## 後續步驟

通過本教程，您成功使用[!UICONTROL Sources]工作區更新了資料流的接收時間表和映射集。

有關如何使用[!DNL Flow Service] API以寫程式方式執行這些操作的步驟，請參閱有關使用流服務API](../../tutorials/api/update-dataflows.md)更新資料流的[教程。
