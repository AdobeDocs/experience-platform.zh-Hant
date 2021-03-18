---
keywords: Experience Platform;home；熱門主題；更新資料流；編輯調度
description: 本教程介紹使用Sources工作區更新資料流調度的步驟，包括其接收頻率和間隔速率。
solution: Experience Platform
title: 在UI中更新源連接資料流計畫
topic: 概述
type: 教學課程
translation-type: tm+mt
source-git-commit: 31e4b15ad71a0d17278fbdb4d88ff42029cbe655
workflow-type: tm+mt
source-wordcount: '431'
ht-degree: 3%

---


# 在UI中更新資料流

本教程介紹使用[!UICONTROL Sources]工作區更新資料流調度的步驟，包括其接收頻率和間隔速率。

## 快速入門

本教學課程需要對Adobe Experience Platform的下列部分有正確的理解：

- [來源](../../home.md):Experience Platform可讓您從各種來源擷取資料，同時讓您能夠使用平台服務來建構、標示並增強傳入資料。
- [沙盒](../../../sandboxes/home.md):Experience Platform提供虛擬沙盒，可將單一平台實例分割為獨立的虛擬環境，以協助開發和發展數位體驗應用程式。

## 編輯排程

在平台UI中，從左側導覽器選擇&#x200B;**[!UICONTROL Sources]**&#x200B;以存取[!UICONTROL Sources]工作區。 從頂部標題中選擇&#x200B;**[!UICONTROL Dataflows]**&#x200B;以查看現有資料流清單。

![目錄](../../images/tutorials/update-dataflows/catalog.png)

[!UICONTROL Dataflows]頁包含所有現有資料流的清單，包括有關其運行狀態、上次運行日期和帳戶名的資訊。

選擇左上角的篩選器表徵圖![filter](../../images/tutorials/update/filter.png)以啟動排序面板。

![filter-dataflows](../../images/tutorials/update-dataflows/filter-dataflows.png)

排序面板提供所有可用來源的清單。 您可以從清單中選擇多個源以訪問屬於不同源的資料流的篩選選擇。

選擇要使用的源，以查看其現有資料流的清單。 在確定要重新計畫的資料流後，請選擇帳戶名稱旁邊的省略號(`...`)。

![重新排程](../../images/tutorials/update-dataflows/reschedule.png)

此時會出現下拉式功能表，提供您&#x200B;**[!UICONTROL Edit schedule]**、**[!UICONTROL Disable dataflow]**、**[!UICONTROL View in monitoring]**&#x200B;和&#x200B;**[!UICONTROL Delete]**&#x200B;的選項。 選取功能表中的 **[!UICONTROL Edit schedule]**。

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

通過本教程，您成功使用[!UICONTROL Sources]工作區更新了資料流的接收調度。

有關如何使用[!DNL Flow Service] API以寫程式方式執行這些操作的步驟，請參閱有關使用流服務API](../../tutorials/api/update-dataflows.md)更新資料流的[教程。