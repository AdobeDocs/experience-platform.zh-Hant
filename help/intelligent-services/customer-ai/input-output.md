---
keywords: Experience Platform；入門；客戶ai；熱門主題；客戶ai輸入；客戶ai輸出
solution: Experience Platform, Real-time Customer Data Platform
feature: Customer AI
title: 客戶AI中的輸入和輸出
topic-legacy: Getting started
description: 瞭解客戶AI使用的所需事件、輸入和輸出的詳細資訊。
exl-id: 9b21a89c-bf48-4c45-9eb3-ace38368481d
source-git-commit: b3c331821e2df17380edbc673066f6b10a06d65f
workflow-type: tm+mt
source-wordcount: '0'
ht-degree: 0%

---

# 客戶AI中的輸入和輸出

下面的文檔概述了客戶AI中使用的不同必需事件、輸入和輸出。

## 快速入門

客戶AI通過分析以下資料集之一來預測流失或轉換傾向得分：

- Adobe Analytics資料使用 [分析源連接器](../../sources/tutorials/ui/create/adobe-applications/analytics.md)
- Adobe Audience Manager資料使用 [Audience Manager源連接器](../../sources/tutorials/ui/create/adobe-applications/audience-manager.md)
- 體驗事件 (EE) 資料集
- 取用者體驗事件 (CEE) 資料集

如果每個資料集共用相同的標識類型（命名空間）（如ECID），則可以從不同源添加多個資料集。 有關添加多個資料集的詳細資訊，請訪問 [客戶AI使用手冊](./user-guide/configure.md#select-data)

>[!IMPORTANT]
>
>源連接器最多需要4週時間來回填資料。 如果您最近設定了連接器，則應驗證資料集是否具有客戶AI所需的最小資料長度。 請查看 [歷史資料](#data-requirements) 部分，以驗證您有足夠的資料實現預測目標。

本文檔要求對CEE架構有基本的瞭解。 請查看 [智慧服務資料準備](../data-preparation.md) 文檔，然後繼續。

下表概述了本文檔中使用的一些常用術語：

| 詞語 | 定義 |
| --- | --- |
| [體驗資料模型(XDM)](../../xdm/home.md) | XDM是一個基礎框架，它讓由Adobe Experience Platform牽頭的Adobe Experience Cloud能夠在正確的時間，在正確的渠道向正確的人傳遞正確的資訊。 構建Experience Platform的方法體系XDM系統可操作經驗資料模型模式供平台服務使用。 |
| XDM 結構 | Experience Platform 會使用結構，以一致且可重複使用的方式說明資料結構。藉由定義跨系統的一致資料，將可輕易保留意義，而發揮資料應有的價值。在將資料引入平台之前，必須構建一個架構來描述資料的結構，並對每個欄位中可以包含的資料類型提供約束。 架構由基本XDM類和零個或多個架構欄位組組成。 |
| XDM類 | 所有XDM架構都描述可以分類為記錄或時間序列的資料。 架構的資料行為由架構的類定義，該類在首次建立架構時分配給該架構。 XDM類描述模式必須包含的最小屬性數以表示特定資料行為。 |
| [欄位群組](../../xdm/schema/composition.md) | 在架構中定義一個或多個欄位的元件。 欄位組強制實施其欄位在架構層次結構中的顯示方式，因此在每個架構中都顯示了與其包含的相同結構。 欄位組僅與由其標識的特定類相容 `meta:intendedToExtend` 屬性。 |
| [資料類型](../../xdm/schema/composition.md) | 還可以為架構提供一個或多個欄位的元件。 但是，與欄位組不同，資料類型不受特定類的限制。 這使得資料類型成為描述可跨具有潛在不同類的多個架構重複使用的通用資料結構的更靈活選項。 本文檔中概述的資料類型受CEE和Adobe Analytics架構的支援。 |
| 衝 | 取消或選擇不續訂其訂閱的帳戶百分比的度量。 較高的流失率會對月度經常性收入(MRR)產生負面影響，也可能表明對產品或服務的不滿。 |
| [即時客戶個人檔案](../../profile/home.md) | 即時客戶概要資訊為有針對性的個性化體驗管理提供了集中的消費者概要資訊。 每個配置檔案都包含所有系統之間聚合的資料，以及可操作的時間戳事件帳戶，這些事件涉及您使用的任何系統中與Experience Platform一起發生的個人。 |

## 客戶AI輸入資料

>[!TIP]
>
> 客戶AI自動確定哪些事件對預測有用，如果可用資料不足以生成質量預測，則會發出警告。

客戶AI支援Adobe Analytics、Adobe Audience Manager、體驗事件(EE)和消費者體驗事件(CEE)資料集。 CEE架構要求您在架構建立過程中添加欄位組。 如果您使用Adobe Analytics或Adobe Audience Manager資料集，源連接器將在連接過程中直接映射下面列出的標準事件（Commerce、Web頁詳細資訊、應用程式和搜索）。 如果每個資料集共用相同的標識類型（命名空間）（如ECID），則可以從不同源添加多個資料集。

有關映射Adobe Analytics資料或Audience Manager資料的詳細資訊，請訪問 [分析欄位映射](../../sources/connectors/adobe-applications/analytics.md) 或 [Audience Manager欄位映射](../../sources/connectors/adobe-applications/mapping/audience-manager.md) 的子菜單。

### 客戶AI使用的標準事件 {#standard-events}

XDM體驗事件用於確定各種客戶行為。 根據資料的結構，下面列出的事件類型可能不包括客戶的所有行為。 您需要確定哪些欄位具有明確、明確地標識Web用戶活動所需的必要資料。 根據您的預測目標，所需的必填欄位可能會更改。

客戶AI依賴不同事件類型來構建模型功能。 使用多個XDM欄位組將這些事件類型自動添加到您的架構中。

>[!NOTE]
>
>如果您使用Adobe Analytics或Adobe Audience Manager資料，則系統會自動建立模式，並使用捕獲資料所需的標準事件。 如果要建立自己的自定義CEE架構來捕獲資料，則需要考慮捕獲資料所需的欄位組。

不必為下面列出的每個標準事件都提供資料，但某些情況需要某些事件。 如果您有任何可用的標準事件資料，建議將其納入您的架構。 例如，如果您想建立用於預測採購事件的客戶AI應用程式，則使用 `Commerce` 和 `Web page details` 資料類型。

要在平台UI中查看欄位組，請選擇 **[!UICONTROL 架構]** 頁籤，然後選擇 **[!UICONTROL 欄位組]** 頁籤。

| 欄位群組 | 事件類型 | XDM欄位路徑 |
| --- | --- | --- |
| [!UICONTROL 商業詳細資訊] | 訂單 | <li> commerce.order.purchaseID </li> <li> productListItems.SKU </li> |
|  | productListViews | <li> commerce.productListViews.value </li> <li> productListItems.SKU </li> |
|  | 檢查 | <li> commerce.checkouts.value </li> <li> productListItems.SKU </li> |
|  | 購買 | <li> commerce.purchases.value </li> <li> productListItems.SKU </li> |
|  | productList刪除 | <li> commerce.productListRemovals.value </li> <li> productListItems.SKU </li> |
|  | 產品清單開啟 | <li> commerce.productListOpens.value </li> <li> productListItems.SKU </li> |
|  | 產品視圖 | <li> commerce.productViews.value </li> <li> productListItems.SKU </li> |
| [!UICONTROL Web詳細資訊] | web訪問 | web.webPageDetails.name |
|  | Web交互 | web.webInteraction.linkClicks.value |
| [!UICONTROL 應用程式詳細資訊] | 應用程式關閉 | <li> application.applicationCloses.value </li> <li> application.name </li> |
|  | 應用程式崩潰 | <li> application.crashes.value </li> <li> application.name </li> |
|  | 應用程式功能使用實例 | <li> application.featureUsages.value </li> <li> application.name </li> |
|  | applicationFirstLoants | <li> application.firstLaunches.value </li> <li> application.name </li> |
|  | 應用程式安裝 | <li> application.installs.value </li> <li> application.name </li> |
|  | 應用程式啟動 | <li> application.launches.value </li> <li> application.name </li> |
|  | 應用程式升級 | <li> application.upgrades.value </li> <li> application.name </li> |
| [!UICONTROL 搜索詳細資訊] | 搜尋 | search.keywords |

此外，客戶AI可以使用訂閱資料構建更好的流失模型。 使用 [[!UICONTROL 訂閱]](../../xdm/data-types/subscription.md) 資料類型格式。 但是，大多數欄位都是可選的，對於最佳的流失模型，強烈建議您為盡可能多的欄位提供資料，例如， `startDate`。 `endDate`，以及其他相關細節。

### 添加自定義事件和配置檔案屬性

如果您有除 [標準事件欄位](#standard-events) 客戶AI使用的自定義事件和自定義配置檔案屬性選項 [實例配置](./user-guide/configure.md#custom-events)。

如果您選擇的資料集包含在您的架構中定義的自定義事件或配置檔案屬性，如「hotel reservation」或「X company的僱員」，則可以將它們添加到實例中。 客戶AI使用這些附加的自定義事件和配置檔案屬性來改進模型質量並提供更準確的結果。

### 歷史資料 {#data-requirements}

客戶AI要求模型培訓的歷史資料，但所需資料量基於兩個關鍵要素：結果窗口和合格人口。

預設情況下，如果在應用程式配置期間未提供符合條件的填充定義，則客戶AI會查找用戶在過去120天中有活動。 此外，客戶AI要求基於預測目標定義的至少500個合格事件和500個不合格事件（總計1000個）的歷史資料。

以下示例使用簡單的公式幫助您確定所需的最小資料量。 如果您的要求超過最低要求，則模型可能會提供更準確的結果。 如果小於所需的最小數量，則模型將失敗，因為沒有足夠的資料來進行模型培訓。

**公式**:

所需資料的最小長度=合格人口+結果窗口

>[!NOTE]
>
> 30是合格人口所需的最低天數。 如果未提供此選項，則預設值為120天。

範例：

- 您希望預測客戶是否可能在未來30天內購買手錶。 您還希望對過去60天內有某些Web活動的用戶進行評分。 在這種情況下，所需資料的最小長度= 60天+ 30天。 合格人口為60天，結果窗口為30天，共90天。

- 您希望預測用戶是否可能在接下來的7天內購買手錶。 在這種情況下，所需資料的最小長度= 120天+ 7天。 合格人口預設為120天，結果窗口為7天，總計127天。

- 您希望預測客戶是否可能在接下來的7天內購買手錶。 您還希望對過去7天中有某些Web活動的用戶進行評分。 在這種情況下，所需資料的最小長度= 30天+ 7天。 合格人口至少需要30天，結果窗口為7天，共37天。

除了所需的最低資料外，客戶AI還能最好地處理最新資料。 在此使用案例中，客戶AI正在根據用戶最近的行為資料對未來進行預測。 換句話說，更新的資料可能會產生更準確的預測。

### 示例方案

在本節中，將介紹客戶AI實例的不同方案以及所需和建議的事件類型。 請參閱 [標準事件表](#standard-events) 的子菜單。

>[!NOTE]
>
> 必需的事件類型用於明確和明確地標識Web用戶活動。 所需事件類型的數量將根據您的架構的預測目標和結構而變化。 如果您不確定是否需要特定事件類型，建議在構建CEE架構時包括該事件類型。 如果您使用Adobe Analytics或Adobe Audience Manager資料，則所需的標準事件應根據您正在流式傳輸的資料可用。

### 方案1:在電子商務零售網站上的採購轉換

**預測目標：** 預測合格配置檔案在網站上購買某件服裝的轉換傾向。

**必需的標準事件類型：**

下面列出的事件類型是具有此特定預測目標的最佳客戶AI輸出所必需的。 根據預測目標，可以排除所需事件，但排除多個事件可能會導致結果不佳。

- 訂單
- 檢查
- 購買
- web訪問
- 搜尋

**其他建議的標準事件類型：**

其餘任何 [事件類型](#standard-events) 在配置客戶AI實例時，可能需要根據目標的複雜性和合格人數。 如果資料可用於特定資料類型，則建議將此資料包含在您的架構中。

### 方案2:媒體流服務網站上的訂閱轉換

**預測目標：** 預測合格配置檔案提交到特定訂閱級別的訂閱轉換傾向，如標準或溢價計畫。

**必需的標準事件類型：**

下面列出的事件類型是具有此特定預測目標的最佳客戶AI輸出所必需的。 根據預測目標，可以排除所需事件，但排除多個事件可能會導致結果不佳。

- 訂單
- 檢查
- 購買
- web訪問
- 搜尋

在本例中， `order`。 `checkouts`, `purchases` 用於指示已購買訂閱及其類型。

此外，對於精確的模型，建議使用 [訂閱資料類型](../../xdm/data-types/subscription.md)。

**其他建議的標準事件類型：**

其餘任何 [事件類型](#standard-events) 在配置客戶AI實例時，可能需要根據目標的複雜性和合格人數。 如果資料可用於特定資料類型，則建議將此資料包含在您的架構中。

### 方案3:瀏覽電子商務零售網站

**預測目標：** 預測不會發生購買事件的可能性。

**必需的標準事件類型：**

下面列出的事件類型是具有此特定預測目標的最佳客戶AI輸出所必需的。 根據預測目標，可以排除所需事件，但排除多個事件可能會導致結果不佳。

- 訂單
- 檢查
- 購買
- web訪問
- 搜尋

**其他建議的標準事件類型：**

其餘任何 [事件類型](#standard-events) 在配置客戶AI實例時，可能需要根據目標的複雜性和合格人數。 如果資料可用於特定資料類型，則建議將此資料包含在您的架構中。

### 方案4:電子商務零售網站上的追加銷售轉換

**預測目標：** 預測購買特定產品以購買新相關產品的人口的購買傾向。

**必需的標準事件類型：**

下面列出的事件類型是具有此特定預測目標的最佳客戶AI輸出所必需的。 根據預測目標，可以排除所需事件，但排除多個事件可能會導致結果不佳。

- 訂單
- 檢查
- 購買
- web訪問
- 搜尋

**其他建議的標準事件類型：**

其餘任何 [事件類型](#standard-events) 在配置客戶AI實例時，可能需要根據目標的複雜性和合格人數。 如果資料可用於特定資料類型，則建議將此資料包含在您的架構中。

### 方案5:取消訂閱（流失）線上新聞發佈

**預測目標：** 預測合格人口下月退訂服務的傾向。

**必需的標準事件類型：**

下面列出的事件類型是具有此特定預測目標的最佳客戶AI輸出所必需的。 根據預測目標，可以排除所需事件，但排除多個事件可能會導致結果不佳。

- web訪問
- 搜尋

此外，對於精確的模型，建議使用 [訂閱資料類型](../../xdm/data-types/subscription.md)。

**其他建議的標準事件類型：**

其餘任何 [事件類型](#standard-events) 在配置客戶AI實例時，可能需要根據目標的複雜性和合格人數。 如果資料可用於特定資料類型，則建議將此資料包含在您的架構中。

### 方案6:啟動移動應用程式

**預測目標：** 預測合格配置檔案在未來X天內啟動付費移動應用程式的傾向。 這類似於預測「每月活動用戶」的關鍵績效指標(KPI)。

**必需的標準事件類型：**

下面列出的事件類型是具有此特定預測目標的最佳客戶AI輸出所必需的。 根據預測目標，可以排除所需事件，但排除多個事件可能會導致結果不佳。

- 訂單
- 檢查
- 購買
- web訪問
- 應用程式關閉
- 應用程式崩潰
- 應用程式功能使用實例
- applicationFirstLoants
- 應用程式安裝
- 應用程式啟動
- 應用程式升級

在本例中， `order`。 `checkouts`, `purchases` 在需要購買移動應用程式時使用。

**其他建議的標準事件類型：**

其餘任何 [事件類型](#standard-events) 在配置客戶AI實例時，可能需要根據目標的複雜性和合格人數。 如果資料可用於特定資料類型，則建議將此資料包含在您的架構中。

### 方案7:實現的特徵(Adobe Audience Manager)

**預測目標：** 預測某些性狀的可實現性。

**必需的標準事件類型：**

要使用Adobe Audience Manager的特徵，您需要使用 [Audience Manager源連接器](../../sources/tutorials/ui/create/adobe-applications/audience-manager.md)。 源連接器自動建立具有正確欄位組的架構。 您無需手動添加其他事件類型，方案即可與客戶AI配合使用。

配置新客戶AI實例時， `audienceName` 和 `audienceID` 可用於在定義目標時為評分選擇特定特徵。

## 客戶AI輸出資料

客戶AI為被視為合格的單個配置檔案生成多個屬性。 根據您已預配的內容，有兩種方法來使用分數（輸出）。 如果您有啟用即時客戶配置檔案的資料集，則可以使用中的「即時客戶配置檔案」中的洞見 [段生成器](../../segmentation/ui/segment-builder.md)。 如果沒有啟用配置檔案的資料集，則可以 [下載客戶AI輸出](./user-guide/download-scores.md) 資料集在資料湖上可用。

可以在以下位置找到輸出資料集 **資料集** 在平台中。 所有客戶AI輸出資料集都以名稱開頭 **客戶AI分數 — 名稱_of_app**。 同樣，所有客戶AI輸出架構都以名稱開頭 **客戶AI架構 — 名稱_of_app**。

![cai-schema-of-app](./images/user-guide/cai-schema-name-of-app.png)

>[!NOTE]
>
> 輸出值由即時客戶配置檔案使用，該配置檔案可用於建立和定義段。

下表介紹了在客戶AI輸出中找到的各種屬性：

| 屬性 | 說明 |
| ----- | ----------- |
| 分數 | 客戶在定義的時間範圍內實現預測目標的相對可能性。 這個值不應被視為概率百分比，而應被視為個人與總體人口相比的可能性。 此分數範圍為0到100。 |
| 概率 | 此屬性是在定義的時間範圍內實現預測目標的配置檔案的真實概率。 在比較不同目標的輸出時，建議您考慮概率超出百分點或分數。 在確定整個合格群體的平均概率時，應始終使用概率，因為對於不經常發生的事件，概率往往處於較低水準。 概率範圍在0和1之間的值。 |
| 百分點 | 此值提供有關配置檔案相對於其他類似得分的配置檔案的效能的資訊。 例如，一個百分位等級為99的流失檔案表明，與所有其他得分檔案中的99%相比，它有更高的翻譯風險。 百分位數範圍從1到100。 |
| 傾向類型 | 所選傾向類型。 |
| 分數日期 | 發生計分的日期。 |
| 影響因素 | 關於配置檔案可能轉換或更改的原因的預測。 因素包括以下屬性：<ul><li>代碼：對配置檔案的預測得分產生積極影響的配置檔案或行為屬性。 </li><li>值：配置檔案或行為屬性的值。</li><li>重要性：指示配置檔案或行為屬性對預測分數（低、中、高）的權重</li></ul> |

>[!NOTE]
>
> - 客戶AI僅使用更新的資料進行進一步培訓和評分。 同樣，當您請求刪除資料時，客戶AI不會使用刪除的資料。
> - 為幫助促進客戶AI中的GDPR法規遵從性，您可以使用Adobe Experience Platform Privacy Service設定協定來滿足客戶請求，以便跨資料庫、身份服務和即時客戶配置檔案訪問和刪除其資料。
> - 所有資料都在傳輸和靜止時被加密。 請參閱文檔以瞭解有關 [資料加密](../../../help/landing/governance-privacy-security/encryption.md)


## 後續步驟 {#next-steps}

當您準備好資料及所有認證和結構描述後，請依照[設定 Customer AI 執行個體](./user-guide/configure.md)指南中的指示開始進行。本指南指導您建立客戶AI實例。
