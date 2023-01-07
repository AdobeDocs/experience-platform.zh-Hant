---
keywords: Experience Platform；快速入門；customer ai；熱門主題；customer ai輸入；customer ai輸出
solution: Experience Platform, Real-time Customer Data Platform
feature: Customer AI
title: Customer AI中的輸入和輸出
description: 進一步了解Customer AI使用的必要事件、輸入和輸出。
exl-id: 9b21a89c-bf48-4c45-9eb3-ace38368481d
source-git-commit: e4e30fb80be43d811921214094cf94331cbc0d38
workflow-type: tm+mt
source-wordcount: '3195'
ht-degree: 3%

---

# Customer AI中的輸入和輸出

以下檔案概述Customer AI中使用的不同必要事件、輸入和輸出。

## 快速入門

Customer AI的運作方式是分析下列其中一個資料集，以預測流失率或轉換傾向分數：

- Adobe Analytics資料使用 [Analytics來源連接器](../../sources/tutorials/ui/create/adobe-applications/analytics.md)
- Adobe Audience Manager資料使用 [Audience Manager源連接器](../../sources/tutorials/ui/create/adobe-applications/audience-manager.md)
- 體驗事件 (EE) 資料集
- 取用者體驗事件 (CEE) 資料集

如果每個資料集共用相同的身分類型（命名空間）（例如ECID），您可以從不同來源新增多個資料集。 如需新增多個資料集的詳細資訊，請造訪 [Customer AI使用手冊](./user-guide/configure.md#select-data)

>[!IMPORTANT]
>
>來源連接器回填資料最多需要四周時間。 如果您最近設定了連接器，應確認資料集具有Customer AI所需的最小資料長度。 請查看 [歷史資料](#data-requirements) 區段來驗證您擁有足夠的資料用於預測目標。

本文檔需要對CEE架構有基本的了解。 請查看 [Intelligent Services資料準備](../data-preparation.md) 檔案，再繼續。

下表概述本檔案中使用的一些常見術語：

| 詞語 | 定義 |
| --- | --- |
| [Experience Data Model(XDM)](../../xdm/home.md) | XDM是基本架構，可讓Adobe Experience Cloud(由Adobe Experience Platform提供技術支援)在適當的時間，透過適當的管道向適當的人員傳遞適當的訊息。 建置Experience Platform的方法 — XDM系統可操作Experience Data Model結構，以供Platform服務使用。 |
| XDM 結構 | Experience Platform 會使用結構，以一致且可重複使用的方式說明資料結構。藉由定義跨系統的一致資料，將可輕易保留意義，而發揮資料應有的價值。在將資料擷取至Platform之前，必須先建立結構以說明資料的結構，並對每個欄位中可包含的資料類型提供限制。 結構包含基本XDM類別和零個或多個結構欄位群組。 |
| XDM類別 | 所有XDM結構都說明可分類為記錄或時間序列的資料。 架構的資料行為由架構的類定義，該類在首次建立時分配給架構。 XDM類別說明結構必須包含的屬性數量最小，才能代表特定資料行為。 |
| [欄位群組](../../xdm/schema/composition.md) | 定義架構中一或多個欄位的元件。 欄位群組強制其欄位在架構階層中的顯示方式，因此在每個架構中呈現的結構都與其所包含的相同。 欄位組僅與特定類相容，由其標識 `meta:intendedToExtend` 屬性。 |
| [資料類型](../../xdm/schema/composition.md) | 也可為架構提供一或多個欄位的元件。 不過，與欄位群組不同，資料類型不會限制在特定類別。 這樣，資料類型就可更靈活地描述可跨具有潛在不同類別的多個架構重複使用的通用資料結構。 CEE和Adobe Analytics架構均支援本檔案中概述的資料類型。 |
| 流失率 | 取消或選擇不續訂其訂閱的帳戶百分比的測量。 高流失率可能對每月經常性收入(MRR)造成負面影響，也可能表示對產品或服務的不滿。 |
| [即時客戶個人檔案](../../profile/home.md) | 「即時客戶設定檔」提供集中的消費者設定檔，以便進行目標式和個人化的體驗管理。 每個設定檔都包含所有系統中匯總的資料，以及涉及個人事件的可操作的時間戳記帳戶，這些事件發生在您搭配Experience Platform使用的任何系統中。 |

## Customer AI輸入資料

>[!TIP]
>
> Customer AI會自動判斷哪些事件對預測有用，並在可用資料不足以產生品質預測時發出警告。

Customer AI支援Adobe Analytics、Adobe Audience Manager、Experience Event(EE)和Cunsomer Experience Event(CEE)資料集。 CEE架構要求您在架構建立過程中添加欄位組。 如果您使用Adobe Analytics或Adobe Audience Manager資料集，來源連接器會在連線程式期間直接對應下列的標準事件（商務、網頁詳細資料、應用程式和搜尋）。 如果每個資料集共用相同的身分類型（命名空間）（例如ECID），您可以從不同來源新增多個資料集。

如需對應Adobe Analytics資料或Audience Manager資料的詳細資訊，請造訪 [Analytics欄位對應](../../sources/connectors/adobe-applications/analytics.md) 或 [Audience Manager欄位對應](../../sources/connectors/adobe-applications/mapping/audience-manager.md) 指南。

### Customer AI使用的標準事件 {#standard-events}

XDM體驗事件可用來判斷各種客戶行為。 根據您的資料結構，下列事件類型可能不包含客戶的所有行為。 您可自行決定哪些欄位具有清楚、明確地識別Web使用者活動所需的必要資料。 需要的必要欄位可能會隨預測目標而改變。

Customer AI仰賴不同的事件類型來建立模型功能。 使用多個XDM欄位群組時，這些事件類型會自動新增至您的架構。

>[!NOTE]
>
>如果您使用Adobe Analytics或Adobe Audience Manager資料，系統會自動建立結構並搭配擷取資料所需的標準事件。 如果要建立自己的自定義CEE架構來捕獲資料，則需要考慮捕獲資料所需的欄位組。

不需要為下列每個標準事件提供資料，但某些情況下需要特定事件。 如果您有任何可用的標準事件資料，建議您將其納入您的結構中。 例如，如果您想要建立用於預測購買事件的Customer AI應用程式，最好使用 `Commerce` 和 `Web page details` 資料類型。

若要在Platform UI中檢視欄位群組，請選取 **[!UICONTROL 結構]** 標籤，然後選取 **[!UICONTROL 欄位群組]** 標籤。

| 欄位群組 | 事件類型 | XDM欄位路徑 |
| --- | --- | --- |
| [!UICONTROL 商務詳細資訊] | 訂購 | <li> commerce.order.purchaseID </li> <li> productListItems.SKU </li> |
|  | productListViews | <li> commerce.productListViews.value </li> <li> productListItems.SKU </li> |
|  | 結帳 | <li> commerce.checkouts.value </li> <li> productListItems.SKU </li> |
|  | 購買 | <li> commerce.purchases.value </li> <li> productListItems.SKU </li> |
|  | productListRemovements | <li> commerce.productListRemovals.value </li> <li> productListItems.SKU </li> |
|  | productListOpens | <li> commerce.productListOpens.value </li> <li> productListItems.SKU </li> |
|  | productViews | <li> commerce.productViews.value </li> <li> productListItems.SKU </li> |
| [!UICONTROL Web詳細資訊] | webVisit | web.webPageDetails.name |
|  | webInteraction | web.webInteraction.linkClicks.value |
| [!UICONTROL 應用程式詳細資訊] | applicationCloses | <li> application.applicationCloses.value </li> <li> application.name </li> |
|  | applicationCrashes | <li> application.crashes.value </li> <li> application.name </li> |
|  | applicationFeatureUsages | <li> application.featureUsages.value </li> <li> application.name </li> |
|  | applicationFirstLaunches | <li> application.firstLaunches.value </li> <li> application.name </li> |
|  | applicationInstalls | <li> application.installs.value </li> <li> application.name </li> |
|  | applicationLaunches | <li> application.launches.value </li> <li> application.name </li> |
|  | applicationUpgrades | <li> application.upgrades.value </li> <li> application.name </li> |
| [!UICONTROL 搜尋詳細資料] | 搜尋 | search.keywords |

此外，Customer AI可使用訂閱資料來建立更理想的流失模型。 每個設定檔都需要訂閱資料，使用 [[!UICONTROL 訂閱]](../../xdm/data-types/subscription.md) 資料類型格式。 不過，大部分欄位都是選用的，為了建立最佳的流失模型，強烈建議您盡可能提供多個欄位的資料，例如 `startDate`, `endDate`，以及任何其他相關詳細資訊。

### 新增自訂事件和設定檔屬性

如果您有除了 [標準事件欄位](#standard-events) 由Customer AI使用，在您的 [執行個體配置](./user-guide/configure.md#custom-events).

如果您選取的資料集包含自訂事件或設定檔屬性，例如您的結構中定義的「飯店訂房」或「X公司的員工」，您可以將它們新增至執行個體。 Customer AI會使用這些額外的自訂事件和設定檔屬性來改善模型品質，並提供更精確的結果。

### 歷史資料 {#data-requirements}

Customer AI需要模型訓練的歷史資料，但所需資料量是根據兩個關鍵元素：結果窗口和合格人口。

如果在應用程式設定期間未提供符合條件的母體定義，依預設，Customer AI會尋找使用者在過去120天內有活動。 此外，根據預測目標定義，Customer AI至少需要500個合格事件和500個非合格事件（共1000個）的歷史資料。

提供的下列範例使用簡單的公式來協助您判斷所需的最少資料量。 如果您的需求超過最低要求，您的模型可能會提供更精確的結果。 如果您的資料量小於所需的最小數量，則模型會失敗，因為沒有足夠的資料量用於模型訓練。

**公式**:

所需資料的最小長度=合格人口+結果窗口

>[!NOTE]
>
> 30是合格人口所需的最低天數。 若未提供，則預設為120天。

範例：

- 您想要預測客戶是否可能在未來30天內購買手錶。 您也想對過去60天內有某些Web活動的使用者評分。 在此情況下，所需資料的最小長度= 60天+ 30天。 合格人口為60天，結果期為30天，總共90天。

- 您想要預測使用者是否可能在未來7天內購買手錶。 在此情況下，所需資料的最小長度= 120天+ 7天。 合格人口預設為120天，結果窗口為7天，總計為127天。

- 您想要預測客戶是否可能在未來7天內購買手錶。 您也想對過去7天內有某些Web活動的使用者評分。 在此情況下，所需資料的最小長度= 30天+ 7天。 合格人口至少需要30天，結果期為7天，總共37天。

除了所需的最低資料， Customer AI對最新資料的運作也最佳。 在此使用案例中，Customer AI會根據使用者最近的行為資料預測未來。 換句話說，更新的資料可能會產生更準確的預測。

### 範例案例

本節會說明Customer AI例項的不同案例，以及必要和建議的事件類型。 請參閱 [標準事件表](#standard-events) 以取得欄位群組及其欄位路徑的詳細資訊。

>[!NOTE]
>
> 必要的事件類型可用來清楚且明確地識別網頁使用者活動。 所需事件類型的數量會根據您結構的預測目標和結構而改變。 如果您不確定需要某個特定事件類型，建議在建置CEE架構時包含該事件類型。 如果您使用Adobe Analytics或Adobe Audience Manager資料，則視您串流的資料而定，應提供必要的標準事件。

### 方案1:電子商務零售網站上的購買轉換

**預測目標：** 預測合格設定檔在網站上購買特定服裝文章的轉換傾向。

**必要的標準事件類型：**

以下列出的事件類型是最佳Customer AI輸出與此特定預測目標的必要項目。 視您的預測目標而定，可能會排除必要事件，但排除多個事件可能會導致結果不佳。

- 訂購
- 結帳
- 購買
- webVisit
- 搜尋

**其他建議的標準事件類型：**

其餘任何 [事件類型](#standard-events) 設定Customer AI例項時，可能需要依目標和合格母體的複雜度而定。 如果資料可用於特定資料類型，建議將此資料包含在您的架構中。

### 方案2:媒體串流服務網站上的訂閱轉換

**預測目標：** 預測合格設定檔提交至特定訂閱層級（例如標準或付費計畫）的訂閱轉換傾向。

**必要的標準事件類型：**

以下列出的事件類型是最佳Customer AI輸出與此特定預測目標的必要項目。 視您的預測目標而定，可能會排除必要事件，但排除多個事件可能會導致結果不佳。

- 訂購
- 結帳
- 購買
- webVisit
- 搜尋

在此範例中， `order`, `checkouts`，和 `purchases` 可用來指出已購買訂閱及其類型。

此外，為了精確模型，建議您使用 [訂閱資料類型](../../xdm/data-types/subscription.md).

**其他建議的標準事件類型：**

其餘任何 [事件類型](#standard-events) 設定Customer AI例項時，可能需要依目標和合格母體的複雜度而定。 如果資料可用於特定資料類型，建議將此資料包含在您的架構中。

### 方案3:電子商務零售網站的流失率

**預測目標：** 預測購買事件不會發生的機率。

**必要的標準事件類型：**

以下列出的事件類型是最佳Customer AI輸出與此特定預測目標的必要項目。 視您的預測目標而定，可能會排除必要事件，但排除多個事件可能會導致結果不佳。

- 訂購
- 結帳
- 購買
- webVisit
- 搜尋

**其他建議的標準事件類型：**

其餘任何 [事件類型](#standard-events) 設定Customer AI例項時，可能需要依目標和合格母體的複雜度而定。 如果資料可用於特定資料類型，建議將此資料包含在您的架構中。

### 方案4:電子商務零售網站上的向上銷售轉換

**預測目標：** 預測已購買特定產品以購買新相關產品的人口的購買傾向。

**必要的標準事件類型：**

以下列出的事件類型是最佳Customer AI輸出與此特定預測目標的必要項目。 視您的預測目標而定，可能會排除必要事件，但排除多個事件可能會導致結果不佳。

- 訂購
- 結帳
- 購買
- webVisit
- 搜尋

**其他建議的標準事件類型：**

其餘任何 [事件類型](#standard-events) 設定Customer AI例項時，可能需要依目標和合格母體的複雜度而定。 如果資料可用於特定資料類型，建議將此資料包含在您的架構中。

### 方案5:取消訂閱（流失率）

**預測目標：** 預測合格人口下月取消訂閱服務的傾向。

**必要的標準事件類型：**

以下列出的事件類型是最佳Customer AI輸出與此特定預測目標的必要項目。 視您的預測目標而定，可能會排除必要事件，但排除多個事件可能會導致結果不佳。

- webVisit
- 搜尋

此外，為了精確模型，建議您使用 [訂閱資料類型](../../xdm/data-types/subscription.md).

**其他建議的標準事件類型：**

其餘任何 [事件類型](#standard-events) 設定Customer AI例項時，可能需要依目標和合格母體的複雜度而定。 如果資料可用於特定資料類型，建議將此資料包含在您的架構中。

### 方案6:啟動行動應用程式

**預測目標：** 預測合格設定檔在未來X天內啟動付費行動應用程式的傾向。 這類似於預測「每月作用中使用者」的關鍵績效指標(KPI)。

**必要的標準事件類型：**

以下列出的事件類型是最佳Customer AI輸出與此特定預測目標的必要項目。 視您的預測目標而定，可能會排除必要事件，但排除多個事件可能會導致結果不佳。

- 訂購
- 結帳
- 購買
- webVisit
- applicationCloses
- applicationCrashes
- applicationFeatureUsages
- applicationFirstLaunches
- applicationInstalls
- applicationLaunches
- applicationUpgrades

在此範例中， `order`, `checkouts`，和 `purchases` 是在需要購買行動應用程式時使用。

**其他建議的標準事件類型：**

其餘任何 [事件類型](#standard-events) 設定Customer AI例項時，可能需要依目標和合格母體的複雜度而定。 如果資料可用於特定資料類型，建議將此資料包含在您的架構中。

### 方案7:已實現的特徵(Adobe Audience Manager)

**預測目標：** 預測某些特徵要實現的傾向。

**必要的標準事件類型：**

若要使用Adobe Audience Manager的特徵，您必須使用 [Audience Manager源連接器](../../sources/tutorials/ui/create/adobe-applications/audience-manager.md). 源連接器會自動建立具有正確欄位組的架構。 您不需要手動新增其他事件類型，便能讓結構與Customer AI搭配使用。

當您設定新的客戶AI例項時， `audienceName` 和 `audienceID` 可用來在定義目標時選取特定特徵以進行計分。

## Customer AI輸出資料

Customer AI會為個別設定檔產生數個屬性，這些設定檔被認為符合資格。 根據您已布建的項目，有兩種方式可以取用分數（輸出）。 如果您有已啟用「即時客戶設定檔」的資料集，您可以在 [區段產生器](../../segmentation/ui/segment-builder.md). 如果您沒有已啟用設定檔的資料集，您可以 [下載Customer AI輸出](./user-guide/download-scores.md) 資料湖上可用的資料集。

您可以在下方找到輸出資料集 **資料集** 在平台中。 所有Customer AI輸出資料集的開頭皆為名稱 **Customer AI分數 — Name_of_app**. 同樣地，所有Customer AI輸出結構都以名稱開頭 **Customer AI結構 — Name_of_app**.

![cai-schema-name-of-app](./images/user-guide/cai-schema-name-of-app.png)

>[!NOTE]
>
> 輸出值由即時客戶設定檔使用，可用來建立和定義區段。

下表說明在Customer AI輸出中找到的各種屬性：

| 屬性 | 說明 |
| ----- | ----------- |
| 分數 | 客戶在定義的時間範圍內達到預測目標的相對可能性。 此值不會視為機率百分比，而是個人與整體人口比較的可能性。 此分數的範圍介於0到100之間。 |
| 機率 | 此屬性是設定檔在定義時間範圍內達到預測目標的真實機率。 比較不同目標的輸出時，建議您考量機率高於百分位數或分數。 在決定合格母體的平均機率時，應一律使用機率，因為不經常發生的事件的機率通常位於較低端。 機率範圍介於0和1之間的值。 |
| 百分位數 | 此值提供關於設定檔相對於其他類似計分設定檔之效能的資訊。 例如，流失率的百分位數排名為99的設定檔，表示其產生轉譯的風險較高，而分數的其他設定檔只有99%。 百分位數範圍從1到100。 |
| 傾向類型 | 選取的傾向類型。 |
| 分數日期 | 發生分數的日期。 |
| 影響因素 | 設定檔可能轉換或流失的預測原因。 因素包括下列屬性：<ul><li>代碼：正面影響設定檔預測分數的設定檔或行為屬性。 </li><li>值：設定檔或行為屬性的值。</li><li>重要性：指出設定檔或行為屬性的權重對預測分數（低、中、高）</li></ul> |

>[!NOTE]
>
> - Customer AI僅使用更新的資料進行進一步訓練和計分。 同樣地，當您請求刪除資料時，Customer AI不會使用已刪除的資料。
> - Customer AI運用Platform資料集。 為支援品牌可能收到的消費者權利請求，品牌應使用PlatformPrivacy Service來提交消費者存取和刪除請求，以在資料湖、Identity Service和即時客戶設定檔中移除其資料。
> - 我們用於輸入/輸出模型的所有資料集都將遵循Platform准則。 平台資料加密適用於閒置和傳輸中的資料。 請參閱本檔案以深入了解 [資料加密](../../../help/landing/governance-privacy-security/encryption.md)


## 後續步驟 {#next-steps}

當您準備好資料及所有認證和結構描述後，請依照[設定 Customer AI 執行個體](./user-guide/configure.md)指南中的指示開始進行。本指南會逐步引導您建立Customer AI的例項。




