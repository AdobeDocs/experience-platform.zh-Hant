---
keywords: Experience Platform；入門；客戶ai；熱門主題；客戶ai輸入；客戶ai輸出
solution: Experience Platform, Intelligent Services, Real-time Customer Data Platform
title: 客戶人工智慧的輸入與輸出
topic-legacy: Getting started
description: 進一步瞭解客戶人工智慧所使用的必要事件、輸入和輸出。
exl-id: 9b21a89c-bf48-4c45-9eb3-ace38368481d
translation-type: tm+mt
source-git-commit: ab0798851e5f2b174d9f4241ad64ac8afa20a938
workflow-type: tm+mt
source-wordcount: '2878'
ht-degree: 1%

---

# 客戶人工智慧中的輸入與輸出

以下檔案概述客戶人工智慧中使用的不同必要事件、輸入和輸出。

## 快速入門

客戶人工智慧可透過分析下列其中一個資料集來預測客戶流失或轉化傾向分數：

- 消費者體驗事件(CEE)資料集
- Adobe Analytics使用[Analytics來源連接器](../../sources/tutorials/ui/create/adobe-applications/analytics.md)的資料
- Adobe Audience Manager資料使用[Audience Manager源連接器](../../sources/tutorials/ui/create/adobe-applications/audience-manager.md)

>[!IMPORTANT]
>
>來源連接器回填資料最多需要4週。 如果您最近設定了連接器，您應驗證資料集是否具有客戶AI所需的最小資料長度。 請檢閱[歷史資料](#data-requirements)區段，以確認您有足夠的資料可用於預測目標。

本文檔要求對CEE架構有基本的瞭解。 請先閱讀[智慧型服務資料準備](../data-preparation.md)檔案，再繼續。

下表概述本檔案中使用的一些常見術語：

| 詞語 | 定義 |
| --- | --- |
| [體驗資料模型(XDM)](../../xdm/home.md) | XDM是基礎性的架構，可讓Adobe Experience Platform的Adobe Experience Cloud在正確的時間，在正確的通道上向正確的人傳遞正確的訊息。 建立Experience Platform的方法XDM System可操作Experience Data Model架構，供平台服務使用。 |
| XDM 結構 | Experience Platform 會使用結構，以一致且可重複使用的方式說明資料結構。藉由定義跨系統的一致資料，將可輕易保留意義，而發揮資料應有的價值。在將資料匯入平台之前，必須先組合架構，以描述資料的結構，並為每個欄位中可包含的資料類型提供限制。 架構由基本XDM類和零個或多個架構欄位組組成。 |
| XDM類 | 所有XDM結構描述的資料可以分類為記錄或時間序列。 架構的資料行為由架構的類別定義，當初建立架構時，會指派給架構。 XDM類描述了模式必須包含的最小屬性數，以表示特定資料行為。 |
| [欄位群組](../../xdm/schema/composition.md) | 定義方案中一個或多個欄位的元件。 欄位群組強制其欄位在架構階層中的顯示方式，因此在每個架構中都會顯示與其所包含的相同結構。 欄位組僅與特定類相容，由其`meta:intendedToExtend`屬性標識。 |
| [資料類型](../../xdm/schema/composition.md) | 也可以為架構提供一個或多個欄位的元件。 但是，與欄位組不同，資料類型不限於特定類。 這使得資料類型成為更有彈性的選項，以說明可在具有潛在不同類別的多個結構中重複使用的常用資料結構。 CEE和Adobe Analytics模式都支援本文檔中概述的資料類型。 |
| 客戶流失 | 取消或選擇不續約其訂閱之帳戶百分比的測量。 高流失率可能會對月度經常性收入(MRR)產生負面影響，也可能表示對產品或服務的不滿。 |
| [即時客戶個人檔案](../../profile/home.md) | 即時客戶個人檔案提供集中化的消費者個人檔案，以進行針對性的個人化體驗管理。 每個描述檔都包含匯總至所有系統的資料，以及與您使用Experience Platform的任何系統中發生之個人相關之事件的可操作時間戳記帳戶。 |

## 客戶人工智慧輸入資料

>[!TIP]
>
> 客戶人工智慧會自動判斷哪些事件對預測有用，並在可用資料不足以產生品質預測時發出警告。

客戶AI支援CEE、Adobe Analytics和Adobe Audience Manager資料集。 CEE架構要求您在架構建立過程中添加欄位組。 如果您使用Adobe Analytics或Adobe Audience Manager資料集，來源連接器會在連線程式中直接對應下列的標準事件（商務、網頁詳細資訊、應用程式和搜尋）。

有關映射Adobe Analytics資料或Audience Manager資料的詳細資訊，請訪問[Analytics欄位映射](../../sources/connectors/adobe-applications/analytics.md)或[Audience Manager欄位映射](../../sources/connectors/adobe-applications/mapping/audience-manager.md)指南。

### 客戶AI {#standard-events}使用的標準事件

XDM體驗事件可用來判斷各種客戶行為。 根據您的資料結構，下列事件類型可能不包含客戶的所有行為。 您需要決定哪些欄位具備必要資料，才能清楚明確地識別Web使用者活動。 視您的預測目標而定，所需的必填欄位可能會變更。

客戶人工智慧依賴不同的事件類型來建立模型功能。 使用多個XDM欄位組，這些事件類型會自動添加到您的架構中。

>[!NOTE]
>
>如果您使用Adobe Analytics或Adobe Audience Manager資料，系統會自動建立結構，並包含擷取資料所需的標準事件。 如果您要建立自己的自訂CEE架構以擷取資料，則需要考慮擷取資料所需的欄位群組。

您不需要針對下列每個標準事件提供資料，但某些情況需要特定事件。 如果您有任何可用的標準事件資料，建議您將其納入架構中。 例如，如果您想要建立用於預測購買事件的Customer AI應用程式，請務必從`Commerce`和`Web page details`資料類型取得資料。

若要在平台UI中檢視欄位群組，請選取左側導軌上的&#x200B;**[!UICONTROL Schemas]**&#x200B;標籤，然後選取&#x200B;**[!UICONTROL Field groups]**&#x200B;標籤。

| 欄位群組 | 事件類型 | XDM欄位路徑 |
| --- | --- | --- |
| [!UICONTROL Commerce Details] | 訂單 | <li> commerce.order.purchaseID </li> <li> productListItems.SKU </li> |
|  | productListViews | <li> commerce.productListViews.value </li> <li> productListItems.SKU </li> |
|  | 結帳 | <li> commerce.checkouts.value </li> <li> productListItems.SKU </li> |
|  | 購買 | <li> commerce.purchases.value </li> <li> productListItems.SKU </li> |
|  | productListRemoves | <li> commerce.productListRemovals.value </li> <li> productListItems.SKU </li> |
|  | productListOpens | <li> commerce.productListOpens.value </li> <li> productListItems.SKU </li> |
|  | productViews | <li> commerce.productViews.value </li> <li> productListItems.SKU </li> |
| [!UICONTROL Web Details] | webVisit | web.webPageDetails.name |
|  | webInteraction | web.webInteraction.linkClicks.value |
| [!UICONTROL Application Details] | applicationCloses | <li> application.applicationCloses.value </li> <li> application.name </li> |
|  | applicationCrances | <li> application.crashes.value </li> <li> application.name </li> |
|  | applicationFeatureUsages | <li> application.featureUsages.value </li> <li> application.name </li> |
|  | applicationFirstLaunches | <li> application.firstLaunches.value </li> <li> application.name </li> |
|  | applicationInstalls | <li> application.installs.value </li> <li> application.name </li> |
|  | applicationLaunches | <li> application.launches.value </li> <li> application.name </li> |
|  | applicationUpgrades | <li> application.upgrades.value </li> <li> application.name </li> |
| [!UICONTROL Search Details] | 搜尋 | search.keywords |

此外，客戶人工智慧可以使用訂閱資料來建立更佳的客戶流失模型。 每個使用[[!UICONTROL Subscription]](../../xdm/data-types/subscription.md)資料類型格式的配置檔案都需要訂閱資料。 但是，大部分欄位都是選用的，對於最佳流失模型，強烈建議您盡可能多地提供資料，例如`startDate`、`endDate`和任何其他相關詳細資訊。

### 歷史資料 {#data-requirements}

客戶人工智慧需要模型訓練的歷史資料，但所需的資料量是根據兩個關鍵元素：結果窗口和合格人口。

根據預設，如果應用程式設定期間未提供符合資格的人口定義，客戶AI會尋找使用者在過去120天內有活動。 此外，客戶人工智慧根據預測的目標定義，至少需要500個符合資格的事件和500個非資格的事件（總計1000個）歷史資料。

提供的下列範例使用簡單的公式，協助您判斷所需資料的最小數量。 如果您有超過最低要求，則您的模型可能會提供更精確的結果。 如果您的數量少於所需的最小數量，則模型將失敗，因為模型培訓沒有足夠的資料量。

**公式**:

所需資料的最小長度=合格人口+結果視窗

>[!NOTE]
>
> 30是合格人口所需的最少天數。 如果未提供此選項，則預設值為120天。

範例：

- 您想要預測客戶是否可能在未來30天內購買手錶。 您也想對過去60天內有某些Web活動的使用者評分。 在此情況下，所需資料的最小長度= 60天+ 30天。 合格人口為60天，結果窗口為30天，總計90天。

- 您想要預測使用者是否可能在未來7天內購買手錶。 在此情況下，所需資料的最小長度= 120天+ 7天。 合格人口預設為120天，結果窗口為7天，總計為127天。

- 您想要預測客戶是否可能在未來7天內購買手錶。 您也想對過去7天內有某些Web活動的使用者評分。 在此情況下，所需資料的最小長度= 30天+ 7天。 合格人口至少需要30天，結果窗口為7天，總計37天。

除了所需的最低資料外，客戶人工智慧也能處理最新資料。 在此使用案例中，客戶AI會根據使用者最近的行為資料預測未來。 換言之，更新的資料可能會產生更準確的預測。

### 範例藍本

在本節中，說明客戶AI例項的不同藍本，以及所需和建議的事件類型。 有關欄位組及其欄位路徑的詳細資訊，請參閱上面的[標準事件表](#standard-events)。

>[!NOTE]
>
> 必要事件類型可用來明確識別Web使用者活動。 所需事件類型的數量將根據模式的預測目標和結構而改變。 如果您不確定需要某個特定事件類型，建議在建立CEE架構時加入該事件類型。 如果您使用Adobe Analytics或Adobe Audience Manager資料，則必須提供必要的標準事件，視您串流的資料而定。

### 方案1:電子商務零售網站上的購買轉換

**預測目標：** 預測合格設定檔的轉換傾向，以便在網站上購買特定的服裝文章。

**必要的標準事件類型：**

下列事件類型是最佳客戶人工智慧輸出與此特定預測目標的必要條件。 根據您的預測目標排除必要事件是可能的，但排除多個事件可能會導致結果不佳。

- 訂單
- 結帳
- 購買
- webVisit
- 搜尋

**其他建議的標準事件類型：**

在設定客戶AI例項時，可能會根據目標和合格人口的複雜性，要求剩餘的[事件類型](#standard-events)。 建議如果資料適用於特定資料類型，則此資料會包含在您的架構中。

### 方案2:媒體串流服務網站上的訂閱轉換

**預測目標：** 預測合格設定檔訂閱至特定訂閱層級（例如標準或優質計畫）的訂閱轉換傾向。

**必要的標準事件類型：**

下列事件類型是最佳客戶人工智慧輸出與此特定預測目標的必要條件。 根據您的預測目標排除必要事件是可能的，但排除多個事件可能會導致結果不佳。

- 訂單
- 結帳
- 購買
- webVisit
- 搜尋

在此範例中，`order`、`checkouts`和`purchases`用於指出已購買訂閱及其類型。

此外，對於精確的模型，建議您使用[訂閱資料類型](../../xdm/data-types/subscription.md)中的部分可用屬性。

**其他建議的標準事件類型：**

在設定客戶AI例項時，可能會根據目標和合格人口的複雜性，要求剩餘的[事件類型](#standard-events)。 建議如果資料適用於特定資料類型，則此資料會包含在您的架構中。

### 方案3:電子商務零售網站的流失率

**預測目** 標：預測購買事件不發生的可能性。

**必要的標準事件類型：**

下列事件類型是最佳客戶人工智慧輸出與此特定預測目標的必要條件。 根據您的預測目標排除必要事件是可能的，但排除多個事件可能會導致結果不佳。

- 訂單
- 結帳
- 購買
- webVisit
- 搜尋

**其他建議的標準事件類型：**

在設定客戶AI例項時，可能會根據目標和合格人口的複雜性，要求剩餘的[事件類型](#standard-events)。 建議如果資料適用於特定資料類型，則此資料會包含在您的架構中。

### 方案4:電子商務零售網站的向上銷售轉換

**預測目** 標：預測已購買特定產品以購買新相關產品之人口的購買傾向。

**必要的標準事件類型：**

下列事件類型是最佳客戶人工智慧輸出與此特定預測目標的必要條件。 根據您的預測目標排除必要事件是可能的，但排除多個事件可能會導致結果不佳。

- 訂單
- 結帳
- 購買
- webVisit
- 搜尋

**其他建議的標準事件類型：**

在設定客戶AI例項時，可能會根據目標和合格人口的複雜性，要求剩餘的[事件類型](#standard-events)。 建議如果資料適用於特定資料類型，則此資料會包含在您的架構中。

### 方案5:取消訂閱（流失）線上新聞出版社

**預測目標：** 預測合格人口下個月取消訂閱服務的傾向。

**必要的標準事件類型：**

下列事件類型是最佳客戶人工智慧輸出與此特定預測目標的必要條件。 根據您的預測目標排除必要事件是可能的，但排除多個事件可能會導致結果不佳。

- webVisit
- 搜尋

此外，對於精確的模型，建議您使用[訂閱資料類型](../../xdm/data-types/subscription.md)中的部分可用屬性。

**其他建議的標準事件類型：**

在設定客戶AI例項時，可能會根據目標和合格人口的複雜性，要求剩餘的[事件類型](#standard-events)。 建議如果資料適用於特定資料類型，則此資料會包含在您的架構中。

### 方案6:啟動行動應用程式

**預測目標：** 預測合格設定檔在未來X天內啟動付費行動應用程式的傾向。這類似於預測「每月活動使用者」的關鍵績效指標(KPI)。

**必要的標準事件類型：**

下列事件類型是最佳客戶人工智慧輸出與此特定預測目標的必要條件。 根據您的預測目標排除必要事件是可能的，但排除多個事件可能會導致結果不佳。

- 訂單
- 結帳
- 購買
- webVisit
- applicationCloses
- applicationCrances
- applicationFeatureUsages
- applicationFirstLaunches
- applicationInstalls
- applicationLaunches
- applicationUpgrades

在此範例中，當需要購買行動應用程式時，會使用`order`、`checkouts`和`purchases`。

**其他建議的標準事件類型：**

在設定客戶AI例項時，可能會根據目標和合格人口的複雜性，要求剩餘的[事件類型](#standard-events)。 建議如果資料適用於特定資料類型，則此資料會包含在您的架構中。

### 方案7:已實現特徵(Adobe Audience Manager)

**預測目** 標：預測某些特徵的傾向。

**必要的標準事件類型：**

為了使用來自Adobe Audience Manager的特性，您需要使用[Audience Manager源連接器](../../sources/tutorials/ui/create/adobe-applications/audience-manager.md)建立源連接。 源連接器自動建立具有正確欄位組的模式。 您不需要手動添加其他事件類型，方案才能與客戶AI一起使用。

當您設定新客戶AI例項時，`audienceName`和`audienceID`可用於在定義目標時選取要計分的特定特徵。

## 客戶人工智慧輸出資料

客戶AI會針對個別個人檔案產生數個屬性，這些屬性被認定為符合資格。 根據您已布建的內容，有兩種方式可以使用分數（輸出）。 如果您有啟用「即時客戶個人檔案」的資料集，您可以在[區段產生器](../../segmentation/ui/segment-builder.md)中使用來自「即時客戶個人檔案」的見解。 如果您沒有啟用設定檔的資料集，您可以[下載資料湖上可用的客戶AI輸出](./user-guide/download-scores.md)資料集。

>[!NOTE]
>
> 「即時客戶描述檔」會使用輸出值，可用來建立和定義區段。

下表說明在Customer AI輸出中找到的各種屬性：

| 屬性 | 說明 |
| ----- | ----------- |
| 分數 | 客戶在定義的時間範圍內達到預測目標的相對可能性。 此值不應視為概率百分比，而應視為個人與整體人口之比的可能性。 此分數的範圍為0到100。 |
| 概率 | 此屬性是描述檔在定義的時間範圍內達到預測目標的真實概率。 比較不同目標的輸出時，建議您考慮百分比或分數的概率。 在決定合格人口的平均概率時，應一律使用概率，因為不經常發生的事件的概率往往在較低端。 概率範圍0到1的值。 |
| 百分位數 | 此值提供描述檔相對於其他類似計分描述檔的效能資訊。 例如，若描述檔的流失百分位數排名為99，則表示其出現竄改的風險較高，而其他所有獲得分數的描述檔中，則有99%的風險。 百分位數範圍從1到100。 |
| 傾向類型 | 所選傾向類型。 |
| 分數日期 | 發生計分的日期。 |
| 影響因素 | 描述檔可能轉換或流失的預測原因。 因素包括以下屬性：<ul><li>程式碼：正面影響描述檔預測分數的描述檔或行為屬性。 </li><li>值：描述檔或行為屬性的值。</li><li>重要性：指出描述檔或行為屬性對預測分數的權重（低、中、高）</li></ul> |

## 下一步 {#next-steps}

準備好資料並準備好所有憑證和結構描述後，請從[設定客戶AI實例指南開始。 ](./user-guide/configure.md)本指南會逐步帶您建立客戶人工智慧的例項。
