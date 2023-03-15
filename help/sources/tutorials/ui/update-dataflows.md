---
keywords: Experience Platform；首頁；熱門主題；更新資料流；編輯排程
description: 本教學課程涵蓋使用Sources工作區更新資料流排程的步驟，包括其擷取頻率和間隔速率。
solution: Experience Platform
title: 在UI中更新源連接資料流
type: Tutorial
exl-id: 0499a2a3-5a22-47b1-ac0e-76a432bd26c0
source-git-commit: ed92bdcd965dc13ab83649aad87eddf53f7afd60
workflow-type: tm+mt
source-wordcount: '724'
ht-degree: 1%

---

# 更新UI中的資料流

本教學課程提供如何使用來源工作區更新現有資料流的步驟，包括其排程和對應。

## 快速入門

本教學課程需要妥善了解下列Adobe Experience Platform元件：

* [來源](../../home.md):Experience Platform可讓您從各種來源擷取資料，同時使用Platform服務來建構、加標籤及增強傳入資料。
* [沙箱](../../../sandboxes/home.md):Experience Platform提供可將單一Platform執行個體分割成個別虛擬環境的虛擬沙箱，以協助開發及改進數位體驗應用程式。

## 更新資料流

在平台UI中，選取 **[!UICONTROL 來源]** 從左側導覽器存取 [!UICONTROL 來源] 工作區。 選擇 **[!UICONTROL 資料流]** 從頂部標題查看現有資料流清單。

![目錄](../../images/tutorials/update-dataflows/catalog.png)

此 [!UICONTROL 資料流] 頁面包含所有現有資料流的清單，包括其對應目標資料集、源和帳戶名稱的相關資訊。

若要排序清單，請選取篩選圖示 ![篩選](../../images/tutorials/update/filter.png) 左上角以使用排序面板。

![篩選資料流](../../images/tutorials/update-dataflows/filter-dataflows.png)

排序面板提供所有可用來源的清單。 您可以從清單中選擇多個源以訪問屬於不同源的資料流的篩選選擇。

選擇要使用的源，以查看其現有資料流的清單。 確定要更新的資料流後，請選取點(`...`)。

![編輯來源](../../images/tutorials/update-dataflows/edit-source.png)

此時將顯示一個下拉菜單，提供更新所選資料流的選項。 在此，您可以選擇更新資料流的映射集和獲取計畫。 您還可以選擇選項以檢查監視儀表板中的資料流、訂閱警報以及禁用或刪除資料流。

要更新資料流的資訊，請選擇 **[!UICONTROL 更新資料流]**.

![update-dataflow](../../images/tutorials/update-dataflows/update-dataflow.png)

### 新增資料

此 [!UICONTROL 新增資料] 步驟。 選取適當的資料格式以檢閱所選資料的內容，然後選取 **[!UICONTROL 下一個]** 繼續。

![新增資料](../../images/tutorials/update-dataflows/add-data.png)

### 資料流詳細資訊

在 [!UICONTROL 資料流詳細資訊] 頁，您可以為資料流提供更新的名稱和說明，並重新配置資料流的錯誤閾值。 在此步驟中，您也可以配置或修改警報訂閱的設定。

提供更新的值後，請選取 **[!UICONTROL 下一個]**.

![dataflow detail](../../images/tutorials/update-dataflows/dataflow-detail.png)

### 映射

>[!NOTE]
>
>下列來源目前不支援編輯對應功能：Adobe Analytics、Adobe Audience Manager、HTTP API和 [!DNL Marketo Engage].

此 [!UICONTROL 對應] 「 」頁提供了一個介面，您可以在其中添加和刪除與資料流關聯的映射集。

映射介面顯示資料流的現有映射集，而不是新建議的映射集。 映射更新只應用於將來計畫的資料流運行。 計畫進行一次性獲取的資料流的映射集無法更新。

在此，可以使用映射介面修改應用到資料流的映射集。 如需如何使用對應介面的完整步驟，請參閱 [資料準備UI指南](../../../data-prep/ui/mapping.md) 以取得更多資訊。

![映射](../../images/tutorials/update-dataflows/mapping.png)

### 排程

此 [!UICONTROL 排程] 步驟，允許您更新資料流的獲取計畫，並自動使用更新的映射內嵌選定源資料。

>[!NOTE]
>
>無法重新計畫計劃一次性獲取的資料流。

![新排程](../../images/tutorials/update-dataflows/new-schedule.png)

您也可以使用資料流頁面中提供的行內更新選項來更新資料流的獲取計畫。

從資料流頁中，選擇點(`...`)，然後選取 **[!UICONTROL 編輯排程]** 從顯示的下拉式功能表。

![編輯排程](../../images/tutorials/update-dataflows/edit-schedule.png)

此 **[!UICONTROL 編輯排程]** 對話框提供了更新資料流的接收頻率和間隔速率的選項。 設定更新的頻率和間隔值後，請選取 **[!UICONTROL 儲存]**.

![排程快顯視窗](../../images/tutorials/update-dataflows/schedule-pop-up.png)

### 請檢閱

此 **[!UICONTROL 檢閱]** 步驟，允許您在更新資料流之前先對其進行查看。

審核資料流後，請選擇 **[!UICONTROL 完成]** 並為建立具有新映射集的資料流留出一些時間。

![審查](../../images/tutorials/update-dataflows/review.png)

## 後續步驟

依照本教學課程，您已成功使用 [!UICONTROL 來源] 工作區來更新資料流的擷取排程和對應集。

有關如何以程式設計方式使用 [!DNL Flow Service] API，請參閱 [使用流服務API更新資料流](../../tutorials/api/update-dataflows.md).
