---
keywords: Experience Platform；首頁；熱門主題；對應csv；對應csv檔案；對應csv檔案至xdm；將csv對應至xdm;ui指南；對應程式；資料準備；資料準備；準備資料；
title: 資料準備UI指南
description: 本檔案提供如何使用Platform UI中的資料準備函式，將CSV檔案對應至XDM架構的指示。
exl-id: fafa4aca-fb64-47ff-a97d-c18e58ae4dae
source-git-commit: 34e0381d40f884cd92157d08385d889b1739845f
workflow-type: tm+mt
source-wordcount: '1845'
ht-degree: 1%

---

# 資料準備UI指南

本檔案提供如何使用Adobe Experience Platform使用者介面中的資料準備函式，將CSV檔案對應至XDM架構的指示。

## 快速入門

本教學課程需要妥善了解下列平台元件：

* [[!DNL Experience Data Model (XDM)] 系統](../../xdm/home.md):Platform用來組織客戶體驗資料的標準化架構。
   * [結構構成基本概念](../../xdm/schema/composition.md):了解XDM結構描述的基本建置組塊，包括結構描述的主要原則和最佳實務。
   * [結構編輯器教學課程](../../xdm/tutorials/create-schema-ui.md):了解如何使用結構編輯器UI建立自訂結構。
* [Identity服務](../../identity-service/home.md):跨裝置和系統橋接身分，以更全面了解個別客戶及其行為。
* [[!DNL Real-Time Customer Profile]](../../profile/home.md):根據來自多個來源的匯總資料，提供統一的即時消費者設定檔。
* [來源](../../sources/home.md):Experience Platform可讓您從各種來源擷取資料，同時使用Platform服務來建構、加標籤及增強傳入資料。

## 資料流詳細資訊

>[!TIP]
>
>您可以從源目錄中選擇任何源，以訪問資料流詳細資訊。 如需詳細資訊，請參閱 [來源概觀](../../sources/home.md).

您必須先建立資料流的詳細資訊，才能將CSV資料對應至XDM架構。

此 [!UICONTROL 資料流詳細資訊] 頁面可讓您選取要將CSV資料內嵌至現有目標資料集或新目標資料集。 現有資料集會隨預先建立的目標架構將您的資料對應至，而新資料集則需要您選取現有架構或建立新架構，才能將資料對應至。

### 使用現有目標資料集

若要將CSV資料內嵌至現有資料集，請選取 **[!UICONTROL 現有資料集]**. 您可以使用 [!UICONTROL 進階搜尋] 選項，或透過捲動下拉式選單中的現有資料集清單來執行。

選取資料集後，請提供資料流的名稱和可選說明。

在此程式中，您也可以啟用 [!UICONTROL 錯誤診斷] 和 [!UICONTROL 部分擷取]. [!UICONTROL 錯誤診斷] 為資料流中發生的任何錯誤記錄啟用詳細的錯誤消息生成，同時 [!UICONTROL 部分擷取] 可讓您內嵌包含錯誤的資料，最高可以是您手動定義的特定臨界值。 請參閱 [部分批次內嵌概觀](../../ingestion/batch-ingestion/partial.md) 以取得更多資訊。

![現有資料集](../images/ui/mapping/existing-dataset.png)

### 使用新目標資料集

若要將CSV資料內嵌至新資料集，請選取 **[!UICONTROL 新資料集]** 然後提供輸出資料集名稱和選用說明。 接下來，使用 [!UICONTROL 進階搜尋] 選項，或透過捲動下拉式選單中的現有結構清單來執行。

在選定架構後，為資料流提供名稱和可選說明，然後應用 [!UICONTROL 錯誤診斷] 和 [!UICONTROL 部分擷取] 資料流所需的設定。 完成後，請選取 **[!UICONTROL 下一個]**.

![新資料集](../images/ui/mapping/new-dataset.png)

## 選擇資料

此 [!UICONTROL 選擇資料] 步驟，提供您上傳本機檔案及預覽其結構和內容的介面。 選擇 **[!UICONTROL 選擇檔案]** 從本機系統上傳CSV檔案。 或者，您也可以將您要上傳的CSV檔案拖放至 [!UICONTROL 拖放檔案] 中。

>[!TIP]
>
>本機檔案上傳目前僅支援CSV檔案。 每個檔案的最大檔案大小為1 GB。

![選擇檔案](../images/ui/mapping/choose-files.png)

上傳檔案後，預覽介面會更新，以顯示檔案的內容和結構。

![preview-sample-data](../images/ui/mapping/preview-sample-data.png)

您可以根據您的檔案選擇列分隔符，如制表符、逗號、垂直號或自定義列分隔符。 選取 **[!UICONTROL 分隔字元]** 下拉式箭頭，然後從功能表中選取適當的分隔字元。

完成後，請選取 **[!UICONTROL 下一個]**.

![分隔字元](../images/ui/mapping/delimiter.png)

## 映射

此 **[!UICONTROL 映射]** 介面提供全方位的工具，可將來源架構的來源欄位對應至目標架構中適當的目標XDM欄位。

![map-csv-to-xdm](../images/ui/mapping/map-csv-to-xdm.png)

### 了解對應介面 {#mapping-interface}

對應介麵包含控制面板，可提供擷取工作流程內容中對應欄位健全狀態的相關資訊。 控制面板會顯示有關您對應欄位的下列詳細資料：

| 屬性 | 說明 |
| --- | --- |
| [!UICONTROL 已映射欄位] | 顯示已對應至目標XDM欄位的來源欄位總數，而不考慮錯誤。 |
| [!UICONTROL 必填欄位] | 顯示所需的映射欄位數。 |
| [!UICONTROL 身分欄位] | 顯示定義為身分的映射欄位總數。 這些映射欄位由指紋表徵圖表示。 |
| [!UICONTROL 錯誤] | 顯示錯誤映射欄位數。 |

![頂端面板](../images/ui/mapping/top-panel.png)

對應介面也提供選項面板，供您選擇，以便在對應欄位中更妥善地互動或篩選。

![第二面板](../images/ui/mapping/second-panel.png)

要搜索特定映射集，請選擇 **[!UICONTROL 搜索源欄位]** 並輸入要隔離的源資料的名稱。

![搜尋](../images/ui/mapping/search.png)

選擇 **[!UICONTROL 所有源欄位]** ，查看篩選選項的下拉式功能表，以便更妥善縮小對應介面的檢視範圍。

篩選選項為：

| 來源欄位 | 說明 |
| --- | --- |
| [!UICONTROL 所有源欄位] | 此選項顯示源架構的所有源欄位。 預設會顯示此選項。 |
| [!UICONTROL 必填欄位] | 此選項篩選源架構，僅顯示完成映射所需的欄位。 |
| [!UICONTROL 身分欄位] | 此選項篩選源架構，以僅顯示為「標識」標籤的欄位。 |
| [!UICONTROL 已映射欄位] | 此選項將篩選源架構，以僅顯示已映射的欄位。 |
| [!UICONTROL 未映射的欄位] | 此選項會篩選源架構，以僅顯示尚未映射的欄位。 |
| [!UICONTROL 含建議的欄位] | 此選項會篩選來源結構，僅顯示包含對應建議的欄位。 |

選擇 **[!UICONTROL 有錯誤的欄位]** ，查看所有存在錯誤的映射欄位。

![篩選](../images/ui/mapping/filter.png)

錯誤對應欄位的隔離檢視隨即顯示，可讓您透過智慧型對應建議或手動對應樹狀結構來解決錯誤。

![帶錯誤的欄位](../images/ui/mapping/fields-with-errors.png)

### 新增欄位類型

您可以選取 **[!UICONTROL 新欄位類型]**.

#### 新映射欄位

要添加新的映射欄位，請選擇 **[!UICONTROL 新欄位類型]** 然後選取 **[!UICONTROL 新增欄位]** 從顯示的下拉式功能表。

![add-new-field](../images/ui/mapping/add-new-field.png)

接下來，從出現的源架構樹中選擇要添加的源欄位，然後選擇 **[!UICONTROL 選擇]**.

![select-new-field](../images/ui/mapping/select-new-field.png)

映射介面將使用您選擇的源欄位和空目標欄位進行更新。 選擇 **[!UICONTROL 映射目標欄位]** 開始將新源欄位映射到相應的目標XDM欄位。

![map-target-field](../images/ui/mapping/map-target-field.png)

隨即出現互動式目標架構樹狀結構，可讓您手動遍歷目標架構，並為來源欄位尋找適當的目標XDM欄位。

![手動映射](../images/ui/mapping/manual-mapping.png)

完成後，選擇架構表徵圖以關閉目標架構介面。

![綱要樹](../images/ui/mapping/schema-tree.png)

#### 計算欄位 {#calculated-fields}

計算欄位允許根據輸入架構中的屬性建立值。 然後，可將這些值指派給目標架構中的屬性，並提供名稱和說明，以便更輕鬆參考。 計算欄位的長度上限為4096個字元。

若要建立計算欄位，請選取 **[!UICONTROL 新欄位類型]** 然後選取 **[!UICONTROL 新增計算欄位]**

![add-calculated-field](../images/ui/mapping/add-calculated-field.png)

此 **[!UICONTROL 建立計算欄位]** 框。 左側對話方塊包含計算欄位中支援的欄位、函式和運算子。 選取其中一個索引標籤，以開始將函式、欄位或運算子新增至運算式編輯器。

| 標記 | 說明 |
| --- | ----------- |
| [!UICONTROL 函數] | 函式索引標籤列出可用於轉換資料的函式。 若要進一步了解可在計算欄位中使用的函式，請參閱 [使用資料準備（映射器）函式](../functions.md). |
| [!UICONTROL 欄位] | 「欄位」頁簽列出源架構中可用的欄位和屬性。 |
| [!UICONTROL 運算子] | 運算子索引標籤會列出可用於轉換資料的運算子。 |

![標籤](../images/ui/mapping/tabs.png)

您可以使用中心的運算式編輯器手動新增欄位、函式和運算子。 選取要開始建立運算式的編輯器。 完成後，請選取 **[!UICONTROL 儲存]** 繼續。

![create-calculated-field](../images/ui/mapping/create-calculated-field.png)

### 匯入對應 {#import}

您可以重複使用現有資料流的映射，以減少手動配置資料獲取的時間並限制錯誤。 選擇 **[!UICONTROL 匯入對應]** 重複使用現有映射。

![導入映射](../images/ui/mapping/import-mapping.png)

此 [!UICONTROL 匯入對應] 窗口，提供要選擇的資料流清單。

選擇預覽表徵圖以預覽所選資料流的映射。

![清單對應](../images/ui/mapping/list-mapping.png)

預覽窗口允許您在導入到資料流之前檢查現有映射。 驗證對應後，您可以選取 **[!UICONTROL 返回]** 要返回資料流清單並檢查另一組映射，或者可以選擇 **[!UICONTROL 選擇]** 繼續。

![預覽對應](../images/ui/mapping/preview-mapping.png)

或者，您可以從資料流清單窗口中選擇要導入的映射。 選擇包含要導入的映射的資料流，然後選擇 **[!UICONTROL 選擇]** 繼續。

![選擇映射](../images/ui/mapping/select-mapping.png)

介面會隨您匯入的對應而更新。

>[!NOTE]
>
>您建立的任何現有映射集或ML映射建議將替換為從現有資料流導入的映射。

![映射導入](../images/ui/mapping/mapping-imported.png)

選擇 **[!UICONTROL 預覽資料]** ，查看所選資料集最多100列範例資料的對應結果。

![預覽資料](../images/ui/mapping/preview-data.png)

在預覽期間，身分欄會優先順序排列為第一個欄位，因為這是驗證對應結果時所需的關鍵資訊。 完成後，請選取 **[!UICONTROL 關閉]**.

![預覽畫面](../images/ui/mapping/preview-screen.png)

要刪除所有映射欄位，請選擇 **[!UICONTROL 清除所有映射]**.

![全部清除](../images/ui/mapping/clear-all.png)

### 使用對應介面

Platform會根據您選取的目標結構或資料集，自動為自動對應欄位提供智慧型建議。 您可以手動調整對應規則以符合您的使用案例，或修正任何重複的對應欄位以清除任何錯誤。

![映射介面](../images/ui/mapping/mapping-interface.png)

在要調整的目標欄位中選取燈泡表徵圖。

![mapping-recc](../images/ui/mapping/mapping-recc.png)

此 [!UICONTROL 對應建議] 彈出式面板隨即出現，顯示可映射到特定源欄位的建議目標欄位清單。 依預設，會自動套用第一個建議。

有時，來源結構有多個建議可供使用。 發生此情況時，對應卡片會顯示最顯著的建議，後面接著包含可用其他建議數量的圖示。 選取燈泡圖示會顯示其他建議的清單。 您可以選取您要對應至之建議旁的核取方塊，以選擇其中一個替代建議。

從這裡，您可以變更選取的目標欄位以修正錯誤或符合您的使用案例。

或者，您也可以選取 **[!UICONTROL 手動選取]** 來手動使用互動式目標架構對應樹。

![recc-panel](../images/ui/mapping/recc-panel.png)

目標架構映射介面與映射欄位顯示在同一視圖中，允許您在同一螢幕中修改映射對。 選取適合您的使用案例或修正錯誤的目標欄位。

![select-target-field](../images/ui/mapping/select-target-field.png)

完成後，請選取 **[!UICONTROL 完成]** 繼續。

![完成](../images/ui/mapping/finish.png)

## 後續步驟

閱讀本檔案後，您就使用Platform UI的對應介面，成功將CSV檔案對應至目標XDM架構。 如需詳細資訊，請參閱下列檔案：

* [資料準備概述](../home.md)
* [來源概觀](../../sources/home.md)
* [在UI中監視源資料流](../../dataflows/ui/monitor-sources.md)
