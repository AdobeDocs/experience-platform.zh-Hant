---
keywords: Experience Platform;home;popular topics; delete dataflows
description: 來源工作區可讓您刪除包含錯誤或已過時的現有批處理和流資料流。
solution: Experience Platform
title: 刪除資料流
topic: overview
type: Tutorial
translation-type: tm+mt
source-git-commit: 7cb5862112c80e386e697aa2bd503abe49f11a3f
workflow-type: tm+mt
source-wordcount: '358'
ht-degree: 1%

---


# 刪除UI中的資料流

Sources工 [!UICONTROL 作區] ，可讓您刪除現有的批次和串流資料流，這些資料流包含錯誤或已過時。

本教學課程提供使用 [!UICONTROL Sources工作區刪除資料流] 的步驟。

## 快速入門

本教學課程需要對Adobe Experience Platform的下列元件有正確的認識：

- [來源](../../home.md): [!DNL Experience Platform] 允許從各種來源接收資料，同時提供使用服務構建、標籤和增強傳入資料的 [!DNL Platform] 能力。
- [沙盒](../../../sandboxes/home.md): [!DNL Experience Platform] 提供虛擬沙盒，可將單一執行個體分 [!DNL Platform] 割為不同的虛擬環境，以協助開發和發展數位體驗應用程式。

## 刪除資料流

在 [Experience Platform UI中](https://platform.adobe.com)，從左側導覽器中選取 **[!UICONTROL Sources]** ，以存取 [!UICONTROL Sources] 工作區，然後從頂端標題 **** 選取DataflowsTraflows。

![目錄](../../images/tutorials/delete/catalog.png)

此時將 **[!UICONTROL 顯示]** 「資料流」頁。 本頁列出了可查看的資料流，包括其目標資料集、源、帳戶名和建立日期的相關資訊。

選取左上角的篩![選器圖示](../../images/tutorials/delete/filter.png)（篩選器圖示）以啟動排序面板。

![資料流](../../images/tutorials/delete/dataflows.png)

排序面板提供所有來源的清單。 您可以從清單中選擇多個源，以訪問與所選特定源關聯的資料流的篩選選擇。

選擇要使用的源，以查看其現有資料流的清單。 確定要刪除的資料流後，請選擇資料流名稱旁邊的省略號(`...`)。

![資料流過濾器](../../images/tutorials/delete/dataflows-filter.png)

此時將顯示一個下拉菜單，為您提供了編輯資料流時間表、禁用資料流或完全刪除資料流的選項。

選擇 **[!UICONTROL 刪除]** ，刪除資料流。

![刪除](../../images/tutorials/delete/delete.png)

將出現最終確認對話框。 選擇 **[!UICONTROL 刪除]** ，以完成流程。

![confirm](../../images/tutorials/delete/confirm.png)

片刻後，畫面底部會顯示確認方塊，以確認刪除成功。

![確認](../../images/tutorials/delete/confirmed.png)

## 後續步驟

按照本教程，您已成功使用 [!UICONTROL Sources] 工作區刪除現有資料流。

有關如何使用 [API調用以寫程式方式執行這些操作的步驟](../../tutorials/api/delete-dataflows.md) ，請參閱使用Flow Service API刪除資料流的教程。