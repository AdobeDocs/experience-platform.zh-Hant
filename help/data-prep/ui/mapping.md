---
keywords: Experience Platform；首頁；熱門主題；映射csv；映射csv；映射csv；將csv檔案映射到xdm；將csv映射到xdm;ui指南；映射；資料準備；準備資料；
title: 資料準備UI指南
description: 本文檔提供有關如何在平台UI中使用資料準備函式將CSV檔案映射到XDM架構的說明。
exl-id: fafa4aca-fb64-47ff-a97d-c18e58ae4dae
source-git-commit: 34e0381d40f884cd92157d08385d889b1739845f
workflow-type: tm+mt
source-wordcount: '1845'
ht-degree: 1%

---

# 資料準備UI指南

本文檔提供了有關如何在Adobe Experience Platform用戶介面中使用資料準備函式將CSV檔案映射到XDM架構的說明。

## 快速入門

本教程需要瞭解以下平台元件：

* [[!DNL Experience Data Model (XDM)] 系統](../../xdm/home.md):平台組織客戶體驗資料的標準化框架。
   * [架構組合的基礎](../../xdm/schema/composition.md):瞭解XDM架構的基本構建基塊，包括架構組成中的關鍵原則和最佳做法。
   * [架構編輯器教程](../../xdm/tutorials/create-schema-ui.md):瞭解如何使用架構編輯器UI建立自定義架構。
* [身份服務](../../identity-service/home.md):通過跨設備和系統橋接身份，更好地瞭解單個客戶及其行為。
* [[!DNL Real-Time Customer Profile]](../../profile/home.md):基於來自多個源的聚合資料提供統一、即時的用戶配置檔案。
* [源](../../sources/home.md):Experience Platform允許從各種源接收資料，同時讓您能夠使用平台服務構建、標籤和增強傳入資料。

## 資料流詳細資訊

>[!TIP]
>
>通過從源目錄中選擇任何源，可以訪問資料流詳細資訊。 有關詳細資訊，請參見 [源概述](../../sources/home.md)。

在將CSV資料映射到XDM架構之前，必須先建立資料流的詳細資訊。

的 [!UICONTROL 資料流詳細資訊] 頁面允許您選擇是要將CSV資料插入現有目標資料集還是新目標資料集。 現有資料集附帶預構建的目標模式，用於將資料映射到，而新資料集要求您選擇現有模式或建立新模式，以將資料映射到。

### 使用現有目標資料集

要將CSV資料插入現有資料集，請選擇 **[!UICONTROL 現有資料集]**。 可以使用 [!UICONTROL 高級搜索] 選項，或通過在下拉菜單中滾動現有資料集清單來執行此操作。

選擇資料集後，請為資料流提供名稱和可選說明。

在此過程中，您還可以 [!UICONTROL 錯誤診斷] 和 [!UICONTROL 部分攝取]。 [!UICONTROL 錯誤診斷] 為資料流中出現的任何錯誤記錄啟用詳細的錯誤消息生成，同時 [!UICONTROL 部分攝取] 允許您接收包含錯誤的資料，最高可達您手動定義的特定閾值。 查看 [部分批處理接收概述](../../ingestion/batch-ingestion/partial.md) 的子菜單。

![現有資料集](../images/ui/mapping/existing-dataset.png)

### 使用新目標資料集

要將CSV資料插入新資料集，請選擇 **[!UICONTROL 新資料集]** 然後提供輸出資料集名稱和可選說明。 接下來，選擇要映射到的方案 [!UICONTROL 高級搜索] 選項，或通過在下拉菜單中滾動現有架構清單來執行。

選擇方案後，為資料流提供名稱和可選說明，然後應用 [!UICONTROL 錯誤診斷] 和 [!UICONTROL 部分攝取] 的子目錄。 完成後，選擇 **[!UICONTROL 下一個]**。

![新資料集](../images/ui/mapping/new-dataset.png)

## 選擇資料

的 [!UICONTROL 選擇資料] 步驟，提供一個介面以上載本地檔案並預覽其結構和內容。 選擇 **[!UICONTROL 選擇檔案]** 從本地系統上載CSV檔案。 或者，可以將要上載的CSV檔案拖放到 [!UICONTROL 拖放檔案] 的子菜單。

>[!TIP]
>
>本地檔案上載當前僅支援CSV檔案。 每個檔案的最大檔案大小為1 GB。

![選擇檔案](../images/ui/mapping/choose-files.png)

上載檔案後，預覽介面將更新以顯示檔案的內容和結構。

![預覽樣本資料](../images/ui/mapping/preview-sample-data.png)

根據檔案的不同，可以為源資料選擇列分隔符，如制表符、逗號、管道或自定義列分隔符。 選擇 **[!UICONTROL 分隔符]** 下拉箭頭，然後從菜單中選擇相應的分隔符。

完成後，選擇 **[!UICONTROL 下一個]**。

![分隔符](../images/ui/mapping/delimiter.png)

## 映射

的 **[!UICONTROL 映射]** 介面為您提供了一個綜合工具，用於將源欄位從源架構映射到目標架構中相應的目標XDM欄位。

![映射至xdm](../images/ui/mapping/map-csv-to-xdm.png)

### 瞭解映射介面 {#mapping-interface}

映射介面包括一個儀表板，該儀表板提供有關接收工作流上下文中映射欄位的運行狀況的資訊。 控制面板顯示有關映射欄位的以下詳細資訊：

| 屬性 | 說明 |
| --- | --- |
| [!UICONTROL 映射欄位] | 顯示已映射到目標XDM欄位的源欄位總數，而不考慮錯誤。 |
| [!UICONTROL 必填欄位] | 顯示必需的映射欄位數。 |
| [!UICONTROL 身分欄位] | 顯示定義為標識的映射欄位總數。 這些映射欄位由指紋表徵圖表示。 |
| [!UICONTROL 錯誤] | 顯示錯誤映射欄位的數量。 |

![頂面板](../images/ui/mapping/top-panel.png)

映射介面還提供一個選項面板，您可以從中選擇這些選項，以便通過映射欄位更好地進行交互或篩選。

![第二面板](../images/ui/mapping/second-panel.png)

要搜索特定映射集，請選擇 **[!UICONTROL 搜索源欄位]** 並輸入要隔離的源資料的名稱。

![搜尋](../images/ui/mapping/search.png)

選擇 **[!UICONTROL 所有源欄位]** 查看包含過濾選項的下拉菜單，以更好地縮小映射介面的視圖範圍。

篩選選項包括：

| 源欄位 | 說明 |
| --- | --- |
| [!UICONTROL 所有源欄位] | 此選項顯示源架構的所有源欄位。 預設情況下顯示此選項。 |
| [!UICONTROL 必填欄位] | 此選項篩選源方案，以僅顯示完成映射所需的欄位。 |
| [!UICONTROL 身分欄位] | 此選項篩選源架構，以僅顯示標籤為「標識」的欄位。 |
| [!UICONTROL 映射欄位] | 此選項篩選源架構以僅顯示已映射的欄位。 |
| [!UICONTROL 未映射的欄位] | 此選項篩選源架構以僅顯示尚未映射的欄位。 |
| [!UICONTROL 帶建議的欄位] | 此選項篩選源架構以僅顯示包含映射建議的欄位。 |

選擇 **[!UICONTROL 有錯誤的欄位]** 查看所有具有錯誤的映射欄位。

![篩選](../images/ui/mapping/filter.png)

此時將顯示錯誤映射欄位的孤立視圖，允許您通過智慧映射建議或手動映射樹解決錯誤。

![帶錯誤的欄位](../images/ui/mapping/fields-with-errors.png)

### 添加新欄位類型

通過選擇 **[!UICONTROL 新欄位類型]**。

#### 新建映射欄位

要添加新映射欄位，請選擇 **[!UICONTROL 新欄位類型]** ，然後選擇 **[!UICONTROL 添加新欄位]** 的下界。

![新增欄位](../images/ui/mapping/add-new-field.png)

接下來，從顯示的源架構樹中選擇要添加的源欄位，然後選擇 **[!UICONTROL 選擇]**。

![選擇 — 新域](../images/ui/mapping/select-new-field.png)

映射介面將使用您選擇的源欄位和空目標欄位進行更新。 選擇 **[!UICONTROL 映射目標欄位]** 開始將新源欄位映射到其相應的目標XDM欄位。

![地圖目標域](../images/ui/mapping/map-target-field.png)

此時將顯示互動式目標架構樹，允許您手動遍歷目標架構並為源欄位查找相應的目標XDM欄位。

![手動映射](../images/ui/mapping/manual-mapping.png)

完成後，選擇架構表徵圖以關閉目標架構介面。

![模式樹](../images/ui/mapping/schema-tree.png)

#### 計算欄位 {#calculated-fields}

計算欄位允許根據輸入方案中的屬性建立值。 然後，可以將這些值分配給目標架構中的屬性，並提供名稱和說明，以便更容易地引用。 計算欄位的最大長度為4096個字元。

要建立計算欄位，請選擇 **[!UICONTROL 新欄位類型]** ，然後選擇 **[!UICONTROL 添加計算欄位]**

![加法域](../images/ui/mapping/add-calculated-field.png)

的 **[!UICONTROL 建立計算欄位]** 的子菜單。 左對話框包含計算欄位中支援的欄位、函式和運算子。 選擇一個頁籤，開始向表達式編輯器添加函式、欄位或運算子。

| 標記 | 說明 |
| --- | ----------- |
| [!UICONTROL 函數] | 「函式」頁籤列出了可用於轉換資料的函式。 要瞭解有關在計算欄位中可以使用的功能的詳細資訊，請閱讀上的指南 [使用資料準備（映射器）函式](../functions.md)。 |
| [!UICONTROL 欄位] | 「欄位」頁籤列出源架構中可用的欄位和屬性。 |
| [!UICONTROL 運算子] | 「運算子」(Operators)頁籤列出了可用於轉換資料的運算子。 |

![頁籤](../images/ui/mapping/tabs.png)

可以使用中心的表達式編輯器手動添加欄位、函式和運算子。 選擇編輯器以開始建立表達式。 完成後，選擇 **[!UICONTROL 保存]** 繼續。

![建立計算欄位](../images/ui/mapping/create-calculated-field.png)

### 導入映射 {#import}

您可以重新使用現有資料流的映射，以減少資料接收的手動配置時間並限制錯誤。 選擇 **[!UICONTROL 導入映射]** 重用現有映射。

![導入映射](../images/ui/mapping/import-mapping.png)

的 [!UICONTROL 導入映射] 的子菜單。

選擇預覽表徵圖以預覽所選資料流的映射。

![清單映射](../images/ui/mapping/list-mapping.png)

預覽窗口允許您在導入到資料流之前檢查現有映射。 驗證映射後，可以選擇 **[!UICONTROL 後退]** 返回資料流清單並檢查另一組映射，或者 **[!UICONTROL 選擇]** 繼續。

![預覽映射](../images/ui/mapping/preview-mapping.png)

或者，可以從資料流窗口清單中選擇要導入的映射。 選擇包含要導入的映射的資料流，然後選擇 **[!UICONTROL 選擇]** 繼續。

![選擇映射](../images/ui/mapping/select-mapping.png)

該介面將使用您導入的映射進行更新。

>[!NOTE]
>
>您建立的任何現有映射集或ML映射建議將替換為從現有資料流導入的映射。

![映射導入](../images/ui/mapping/mapping-imported.png)

選擇 **[!UICONTROL 預覽資料]** 查看所選資料集中最多100行示例資料的映射結果。

![預覽資料](../images/ui/mapping/preview-data.png)

在預覽期間，標識列作為第一個欄位按優先順序排列，因為它是驗證映射結果時所必需的關鍵資訊。 完成後，選擇 **[!UICONTROL 關閉]**。

![預覽螢幕](../images/ui/mapping/preview-screen.png)

要刪除所有映射欄位，請選擇 **[!UICONTROL 清除所有映射]**。

![全部清除](../images/ui/mapping/clear-all.png)

### 使用映射介面

平台根據您選擇的目標架構或資料集自動為自動映射欄位提供智慧建議。 您可以手動調整映射規則以適應您的使用情形，或修復任何重複的映射欄位以清除任何錯誤。

![映射介面](../images/ui/mapping/mapping-interface.png)

在要調整的目標欄位中選擇燈泡表徵圖。

![映射 — recc](../images/ui/mapping/mapping-recc.png)

的 [!UICONTROL 映射建議] 彈出式面板，顯示可映射到特定源欄位的建議目標欄位的清單。 預設情況下，將自動應用第一個建議。

有時，源架構有多個建議。 當出現這種情況時，映射卡將顯示最突出的建議，然後顯示一個表徵圖，其中包含可用的其他建議數。 選擇燈泡表徵圖將顯示其他建議的清單。 通過選中要映射到的建議案旁邊的複選框，可以選擇其中一個備選建議案。

在此處，您可以更改所選目標欄位以修復錯誤或匹配使用案例。

或者，可以選擇 **[!UICONTROL 手動選擇]** 手動使用互動式目標模式映射樹。

![重疊面板](../images/ui/mapping/recc-panel.png)

目標架構映射介面與映射欄位顯示在同一視圖中，允許您在同一螢幕中修改映射對。 選擇適合您的使用案例的目標欄位或修復錯誤。

![選擇目標域](../images/ui/mapping/select-target-field.png)

完成後，選擇 **[!UICONTROL 完成]** 繼續。

![完成](../images/ui/mapping/finish.png)

## 後續步驟

通過閱讀此文檔，您已使用平台UI中的映射介面成功將CSV檔案映射到目標XDM架構。 有關詳細資訊，請參閱以下文檔：

* [資料準備概述](../home.md)
* [源概述](../../sources/home.md)
* [監視UI中的源資料流](../../dataflows/ui/monitor-sources.md)
