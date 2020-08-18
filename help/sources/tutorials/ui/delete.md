---
keywords: Experience Platform;home;popular topics; delete dataflows
description: Adobe Experience Platform中的來源連接器可讓您依計畫吸收外部來源的資料。 本教程提供從Sources工作區刪除資料流的步驟。
solution: Experience Platform
title: 刪除資料流
topic: overview
translation-type: tm+mt
source-git-commit: 6bd5dc5a68fb2814ab99d43b34f90aa7e50aa463
workflow-type: tm+mt
source-wordcount: '449'
ht-degree: 1%

---


# 刪除資料流

Adobe Experience Platform中的來源連接器可讓您依計畫吸收外部來源的資料。 本教學課程提供從 [!UICONTROL Sources工作區刪除資料流] 的步驟。

## 快速入門

本教學課程需要對Adobe Experience Platform的下列元件有正確的認識：

- [[!DNL Experience Data Model] (XDM)系統](../../../xdm/home.md):組織客戶體驗資料 [!DNL Experience Platform] 的標準化架構。
   - [架構構成基礎](../../../xdm/schema/composition.md):瞭解XDM架構的基本建置區塊，包括架構組合的主要原則和最佳實務。
   - [架構編輯器教程](../../../xdm/tutorials/create-schema-ui.md):瞭解如何使用架構編輯器UI建立自訂架構。
- [[!DNL即時客戶基本資料]](../../../profile/home.md):根據來自多個來源的匯整資料，提供統一、即時的消費者個人檔案。

## 使用UI刪除資料流

登入 [Adobe Experience Platform](https://platform.adobe.com) ，然後從左側導覽列選取 **[!UICONTROL Sources]** ，以存取 **** Sources工作區。 「目 **[!UICONTROL 錄]** 」螢幕顯示了各種源，您可以用這些源建立帳戶和資料流。 每個源顯示與其關聯的現有帳戶和資料流的數量。

選擇 **[!UICONTROL Dataflows]** 以訪問 **[!UICONTROL Dataflows]** 頁。

![dataset-flow-activity](../../images/tutorials/delete/dataflows.png)

此時將顯示現有資料流清單。 此頁上是現有資料流的可排序資訊清單，如源、用戶名、運行狀態和上次運行日期。 選取左 **上角的** 「漏斗」圖示進行排序。

![dataflows-list](../../images/tutorials/delete/dataflows-list.png)

排序面板會出現在畫面的左側，其中包含可用來源的清單。
您可以使用排序函式選擇多個源。

選擇要訪問的源，並從主介面的資料流清單中找到要刪除的資料流。 在示例中，選擇的源為， **[!DNL Azure Blob Storage]** 資料流名為 **[!UICONTROL Customer Profiles資料流]**。 從排序面板中選擇多個源時，您最近建立的資料流將首先顯示，因為清單按建立日期排序。

選擇要刪除的資料流。

![dataflows-sort](../../images/tutorials/delete/dataflows-sort.png)

「屬 **[!UICONTROL 性]** 」面板出現在畫面的右側，其中包含有關所選資料流的資訊以及「編輯調 **[!UICONTROL 度」選項]**。

要刪除資料流，請選擇 **[!UICONTROL 刪除]**。

![dataflows-sort](../../images/tutorials/delete/dataflows-properties.png)

最後出現確認對話框，選擇「 **[!UICONTROL 刪除]** 」以完成該過程。

![刪除](../../images/tutorials/delete/delete.png)

片刻後，畫面底部會出現綠色的確認方塊，以確認刪除成功。

![確認](../../images/tutorials/delete/confirmed.png)

## 後續步驟

遵循本教學課程，您已成功存取 **[!UICONTROL Sources工作區的現有帳戶和]** 資料流。 現在，下游服務（例如和）可 [!DNL Platform] 以使用傳入 [!DNL Real-time Customer Profile] 的資料 [!DNL Data Science Workspace]。 如需詳細資訊，請參閱下列檔案：

- [[!DNL Real-time Customer Profile] 概述](../../../profile/home.md)
- [[!DNL Data Science Workspace] 概述](../../../data-science-workspace/home.md)