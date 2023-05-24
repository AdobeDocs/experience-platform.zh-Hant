---
keywords: Experience Platform；首頁；熱門主題；更新資料流；編輯計畫
description: 本教程介紹了使用「源」工作區更新資料流調度的步驟，包括其接收頻率和間隔速率。
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

本教程提供了有關如何使用源工作區更新現有資料流（包括其調度和映射）的步驟。

## 快速入門

本教程需要對Adobe Experience Platform的以下部分進行有效的理解：

* [源](../../home.md):Experience Platform允許從各種源接收資料，同時讓您能夠使用平台服務構建、標籤和增強傳入資料。
* [沙箱](../../../sandboxes/home.md):Experience Platform提供虛擬沙箱，將單個平台實例分區為獨立的虛擬環境，以幫助開發和發展數字型驗應用程式。

## 更新資料流

在平台UI中，選擇 **[!UICONTROL 源]** 從左側導航 [!UICONTROL 源] 工作區。 選擇 **[!UICONTROL 資料流]** 查看現有資料流的清單。

![目錄](../../images/tutorials/update-dataflows/catalog.png)

的 [!UICONTROL 資料流] 頁包含所有現有資料流的清單，包括有關其相應目標資料集、源和帳戶名的資訊。

要對清單進行排序，請選擇篩選器表徵圖 ![濾波器](../../images/tutorials/update/filter.png) 框（左上角）中選擇相應的選項。

![篩選器資料流](../../images/tutorials/update-dataflows/filter-dataflows.png)

排序面板提供所有可用源的清單。 可以從清單中選擇多個源，以訪問屬於不同源的過濾資料流的選擇。

選擇要使用的源，以查看其現有資料流的清單。 確定要更新的資料流後，選擇橢圓(`...`)。

![編輯源](../../images/tutorials/update-dataflows/edit-source.png)

此時將出現下拉菜單，提供更新所選資料流的選項。 在此，您可以選擇更新資料流的映射集和接收計畫。 您還可以選擇選項來檢查監視儀表板中的資料流、訂閱警報以及禁用或刪除資料流。

要更新資料流的資訊，請選擇 **[!UICONTROL 更新資料流]**。

![更新資料流](../../images/tutorials/update-dataflows/update-dataflow.png)

### 添加資料

的 [!UICONTROL 添加資料] 的上界。 選擇適當的資料格式以查看所選資料的內容，然後選擇 **[!UICONTROL 下一個]** 繼續。

![添加資料](../../images/tutorials/update-dataflows/add-data.png)

### 資料流詳細資訊

在 [!UICONTROL 資料流詳細資訊] 頁中，您可以為資料流提供更新的名稱和說明，並重新配置資料流的錯誤閾值。 在此步驟中，您還可以配置或修改警報訂閱的設定。

提供更新值後，選擇 **[!UICONTROL 下一個]**。

![資料流詳細資訊](../../images/tutorials/update-dataflows/dataflow-detail.png)

### 映射

>[!NOTE]
>
>以下源當前不支援編輯映射功能：Adobe Analytics、Adobe Audience Manager、HTTP API和 [!DNL Marketo Engage]。

的 [!UICONTROL 映射] 頁為您提供了一個介面，您可以在其中添加和刪除與資料流關聯的映射集。

映射介面顯示資料流的現有映射集，而不顯示新的建議映射集。 映射更新僅應用於將來計畫的資料流運行。 為一次性接收計畫的資料流無法更新其映射集。

在此，可以使用映射介面修改應用於資料流的映射集。 有關如何使用映射介面的全面步驟，請參見 [資料準備UI指南](../../../data-prep/ui/mapping.md) 的子菜單。

![映射](../../images/tutorials/update-dataflows/mapping.png)

### 計畫

的 [!UICONTROL 計畫] 步驟，允許您更新資料流的接收計畫並自動使用更新的映射來接收選定的源資料。

>[!NOTE]
>
>無法重新計畫已安排一次性接收的資料流。

![新計畫](../../images/tutorials/update-dataflows/new-schedule.png)

您還可以使用「資料流」頁中提供的聯機更新選項更新資料流的接收計畫。

從資料流頁中，選擇橢圓(`...`)旁邊，然後選擇 **[!UICONTROL 編輯計畫]** 的下界。

![編輯計畫](../../images/tutorials/update-dataflows/edit-schedule.png)

的 **[!UICONTROL 編輯計畫]** 對話框為您提供了更新資料流的接收頻率和間隔速率的選項。 設定更新的頻率和間隔值後，選擇 **[!UICONTROL 保存]**。

![時間表彈出](../../images/tutorials/update-dataflows/schedule-pop-up.png)

### 請檢閱

的 **[!UICONTROL 審閱]** 步驟，允許您在更新資料流之前查看資料流。

查看資料流後，選擇 **[!UICONTROL 完成]** 並為要建立新映射集的資料流留出一些時間。

![審查](../../images/tutorials/update-dataflows/review.png)

## 後續步驟

按照本教程，您已成功使用 [!UICONTROL 源] 工作區，以更新資料流的接收計畫和映射集。

有關如何使用 [!DNL Flow Service] API，請參閱有關 [使用流服務API更新資料流](../../tutorials/api/update-dataflows.md)。
