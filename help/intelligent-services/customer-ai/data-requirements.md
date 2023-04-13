---
keywords: Experience Platform；快速入門；customer ai；熱門主題；customer ai輸入；customer ai輸出；資料需求
solution: Experience Platform, Real-time Customer Data Platform
feature: Customer AI
title: Customer AI的資料需求
topic-legacy: Getting started
description: 進一步了解Customer AI使用的必要事件、輸入和輸出。
exl-id: 9b21a89c-bf48-4c45-9eb3-ace38368481d
source-git-commit: 5f7b602b68f5cbf4b1f4b08603757b0956e36408
workflow-type: tm+mt
source-wordcount: '2484'
ht-degree: 2%

---


# Customer AI中的輸入和輸出

以下檔案概述Customer AI中使用的不同必要事件、輸入和輸出。

## 快速入門 {#getting-started}

以下是在Customer AI中建立傾向模型並識別個人化行銷目標對象的步驟：

1. 大綱使用案例：傾向模型如何協助識別個人化行銷的目標對象？ 實現目標的業務目標和相應策略是什麼？ 傾向模型在此程式中可適用於何處？

2. 優先處理使用案例：哪些是業務的最優先順序？

3. 在Customer AI中建立模型：看這個 [快速教學課程](https://experienceleague.adobe.com/docs/platform-learn/tutorials/intelligent-services/configure-customer-ai.html?lang=zh-Hant) 並將 [UI指南](../customer-ai/user-guide/configure.md) 來建立模型的逐步程式。

4. [建立區段](../customer-ai/user-guide/create-segment.md) 使用模型結果。

5. 根據這些區段採取有針對性的業務行動。 監控結果並反覆執行要改善的動作。

以下是第一個模型的組態範例。  此範例模型建置於本檔案中，使用客戶AI模型來預測未來30天內，哪些人可能會針對零售企業進行轉換。 輸入資料集是Adobe Analytics資料集。

| 步驟 | 定義 | 範例 |
| ---- | ------ | ------- |
| 設定 | 指定有關模型的基本資訊。 | **名稱**:鉛筆購買傾向模型 <br> **模型類型**:轉換 |
| 選擇資料 | 指定用於建立模型的資料集。 | **資料集**:Adobe Analytics資料集 <br> **身分**:請確定每個資料集的身分欄都設為共同身分。 |
| 定義目標 | 定義目標、合格母體、自訂事件和設定檔屬性。 | **預測目標**:選擇 `commerce.purchases.value` 等於鉛筆 <br> **結果窗口**:30天。 |
| 設定選項 | 設定模型重新整理的排程並啟用設定檔的分數 | **排程**:每週 <br> **啟用設定檔**:必須啟用此功能，才能在細分中使用模型輸出。 |

## 資料概觀 {#data-overview}

以下各節概述Customer AI中使用的不同必要事件、輸入和輸出。

Customer AI的運作方式是分析下列資料集，以預測流失率（客戶可能停止使用產品時）或轉換（客戶可能購買時）傾向分數：

- Adobe Analytics資料使用 [Analytics來源連接器](../../sources/tutorials/ui/create/adobe-applications/analytics.md)
- Adobe Audience Manager資料使用 [Audience Manager源連接器](../../sources/tutorials/ui/create/adobe-applications/audience-manager.md)
- [體驗事件資料集](https://experienceleague.adobe.com/docs/experience-platform/xdm/classes/experienceevent.html)
- [消費者體驗事件資料集](https://experienceleague.adobe.com/docs/experience-platform/intelligent-services/data-preparation.html#cee-schema)

如果每個資料集都共用相同的身分類型（命名空間）（例如ECID），您可以從不同來源新增多個資料集。 如需新增多個資料集的詳細資訊，請造訪 [Customer AI使用手冊](../customer-ai/user-guide/configure.md).

>[!IMPORTANT]
>
>來源連接器回填資料最多需要四周時間。 如果您最近設定了連接器，應確認資料集具有Customer AI所需的最小資料長度。 請查看 [歷史資料](#data-requirements) 區段來驗證您擁有足夠的資料用於預測目標。

下表概述本檔案中使用的一些常見術語：

| 詞語 | 定義 |
| --- | --- |
| [Experience Data Model(XDM)](../../xdm/home.md) | XDM是基本架構，可讓Adobe Experience Cloud(由Adobe Experience Platform提供技術支援)在適當的時間，透過適當的管道向適當的人員傳遞適當的訊息。 Platform使用XDM系統以特定方式組織資料，讓Platform服務的使用更輕鬆。 |
| [XDM 結構](../../xdm/schema/composition.md) | Experience Platform 會使用結構，以一致且可重複使用的方式說明資料結構。藉由定義跨系統的一致資料，將可輕易保留意義，而發揮資料應有的價值。在將資料擷取至Platform之前，必須先建立結構以說明資料的結構，並對每個欄位中可包含的資料類型提供限制。 結構包含基本XDM類別和零個或多個結構欄位群組。 |
| [XDM類別](../../xdm/schema/field-constraints.md) | 所有XDM結構都說明可分類為 `Experience Event`. 架構的資料行為由架構的類定義，該類在首次建立時分配給架構。 XDM類別說明結構必須包含的屬性數量最小，才能代表特定資料行為。 |
| [欄位群組](../../xdm/schema/composition.md) | 定義架構中一或多個欄位的元件。 欄位群組強制其欄位在架構階層中的顯示方式，因此在每個架構中呈現的結構都與其所包含的相同。 欄位組僅與特定類相容，由其標識 `meta:intendedToExtend` 屬性。 |
| [資料類型](../../xdm/schema/composition.md) | 也可為架構提供一或多個欄位的元件。 不過，與欄位群組不同，資料類型不會限制在特定類別。 這樣，資料類型就可更靈活地描述可跨具有潛在不同類別的多個架構重複使用的通用資料結構。 CEE和Adobe Analytics架構均支援本檔案中概述的資料類型。 |
| [即時客戶個人檔案](../../profile/home.md) | 即時客戶設定檔提供集中化的消費者設定檔，以便進行目標式和個人化的體驗管理。 每個設定檔都包含所有系統中匯總的資料，以及涉及個人事件的可操作的時間戳記帳戶，這些事件發生在您搭配Experience Platform使用的任何系統中。 |

## Customer AI輸入資料 {#customer-ai-input-data}

對於輸入資料集(如Adobe Analytics和Adobe Audience Manager)，各自的來源連接器依預設會在連線程式期間直接對應這些標準欄位群組（商務、網頁、應用程式和搜尋）中的事件。 下表顯示Customer AI預設標準欄位群組中的事件欄位。

如需對應Adobe Analytics資料或Audience Manager資料的詳細資訊，請造訪Analytics欄位對應或Audience Manager [欄位對應指南](../../sources/connectors/adobe-applications/mapping/audience-manager.md).

若是未透過上述其中一個連接器填入的輸入資料集，您可以使用體驗事件或消費者體驗事件XDM結構。 在架構建立程式期間，可新增其他XDM欄位群組。 欄位群組可由Adobe提供，例如標準欄位群組或自訂欄位群組，以符合Platform中的資料表示。

>[!IMPORTANT]
>
>您必須確保資料已填入這些輸入資料集。 如果在輸入資料集中找不到標準欄位群組的事件，則必須在設定工作流程期間新增自訂事件。 請參閱自訂事件的詳細資訊。

### Customer AI使用的標準欄位群組 {#standard-events}

體驗事件可用於判斷各種客戶行為。 根據您的資料結構，下列事件類型可能不包含客戶的所有行為。 您可自行決定哪些欄位具備必要資料，才能清楚、明確地識別Web或其他管道特定使用者活動。 需要的必要欄位可能會隨預測目標而改變。

>[!NOTE]
>
>如果您使用Adobe Analytics或Adobe Audience Manager資料，系統會自動建立結構並搭配擷取資料所需的標準事件。 如果您要建立自己的自定義EE架構以捕獲資料，則需要考慮捕獲資料所需的欄位組。

Customer AI依預設會使用這四個標準欄位群組中的事件：商務、Web、應用程式和搜索。 下列標準欄位群組中的每個事件不需要有資料，但某些案例需要特定事件。 如果標準欄位群組中有任何事件可供使用，建議您將其納入您的架構中。 例如，如果您想要建立用於預測購買事件的Customer AI模型，則有來自商務和網頁詳細資訊欄位群組的資料會很實用。

若要在Platform UI中檢視欄位群組，請選取 **[!UICONTROL 結構]** 標籤，然後選取 **[!UICONTROL 欄位群組]** 標籤。

| 欄位群組 | 事件類型 | XDM欄位路徑 |
| --- | --- | --- |
| [!UICONTROL 商務詳細資訊] | 訂購 | <li> `commerce.order.purchaseID` </li> <li> `productListItems.SKU` </li> |
|  | productListViews | <li> `commerce.productListViews.value` </li> <li> `productListItems.SKU` </li> |
|  | 結帳 | <li> `commerce.checkouts.value` </li> <li> `productListItems.SKU` </li> |
|  | 購買 | <li> `commerce.purchases.value` </li> <li> `productListItems.SKU` </li> |
|  | productListRemovements | <li> `commerce.productListRemovals.value` </li> <li> `productListItems.SKU` </li> |
|  | productListOpens | <li> `commerce.productListOpens.value` </li> <li> `productListItems.SKU` </li> |
|  | productViews | <li> `commerce.productViews.value` </li> <li> `productListItems.SKU` </li> |
| [!UICONTROL Web詳細資訊] | webVisit | `web.webPageDetails.name` |
|  | webInteraction | `web.webInteraction.linkClicks.value` |
| [!UICONTROL 應用程式詳細資訊] | applicationCloses | <li> `application.applicationCloses.value` </li> <li> `application.name` </li> |
|  | applicationCrashes | <li> `application.crashes.value` </li> <li> `application.name` </li> |
|  | applicationFeatureUsages | <li> `application.featureUsages.value` </li> <li> `application.name` </li> |
|  | applicationFirstLaunches | <li> `application.firstLaunches.value` </li> <li> `application.name` </li> |
|  | applicationInstalls | <li> application.installs.value </li> <li> `application.name` </li> |
|  | applicationLaunches | <li> application.launches.value </li> <li> `application.name` </li> |
|  | applicationUpgrades | <li> application.upgrades.value </li> <li> `application.name` </li> |
| [!UICONTROL 搜尋詳細資料] | 搜尋 | `search.keywords` |

此外，Customer AI可使用訂閱資料來建立更理想的流失模型。 每個設定檔都需要訂閱資料，使用 [[!UICONTROL 訂閱]](../../xdm/data-types/subscription.md) 資料類型格式。 不過，大部分欄位都是選用的，為了建立最佳的流失模型，強烈建議您盡可能提供多個欄位的資料，例如 `startDate`, `endDate`，以及任何其他相關詳細資訊。 請洽詢您的客戶團隊，以取得此功能的其他支援。

### 新增自訂事件和設定檔屬性 {#add-custom-events}

除了預設值，如果您還有您想要包含的資訊 [標準事件欄位](#standard-events) 由Customer AI使用，您可以使用 [自訂事件設定](./user-guide/configure.md#custom-events) 來增加模型所使用的資料。

#### 自訂事件的使用時機

在資料集選取步驟中選擇的資料集包含時，必須使用自訂事件 *無* Customer AI使用的預設事件欄位。 Customer AI需要除了結果以外至少一個使用者行為事件的相關資訊。

自訂事件有助於：

- 將領域知識或先前的專業知識納入模型。

- 改善預測模型品質。

- 獲得更多見解和解釋。

自訂事件的最佳候選項是包含可預測結果之領域知識的資料。 自訂事件的一些一般範例包括：

- 註冊帳戶

- 訂閱電子報

- 呼叫客戶服務

以下是一系列特定產業的自訂事件範例：

| 產業 | 自訂事件 |
| --- | --- |
| 零售 | 店內交易<br>註冊俱樂部卡<br>剪下行動抵用券。 |
| 娛樂 | 購買季會籍 <br> 串流視頻。 |
| 招待 | 預訂餐廳 <br> 購買忠誠度點數。 |
| 旅行 | 添加已知旅行者資訊購買里程。 |
| 通訊 | 升級/降級/取消計畫。 |

自訂事件必須代表使用者啟動的動作，才能加以選取。 例如，「電子郵件傳送」是由行銷人員而非使用者起始的動作，因此不應當用作自訂事件。

### 歷史資料

Customer AI需要歷史資料才能進行模型訓練。 資料在系統記憶體在的所需持續時間由兩個關鍵元素決定：結果窗口和合格人口。

如果在應用程式設定期間未提供符合條件的母體定義，依預設，Customer AI會尋找使用者在過去45天內有活動。 此外，根據預測目標定義，從歷史資料中至少需要500個合格事件和500個非合格事件（共1000個）。

下列範例示範如何使用簡單的公式，協助您判斷所需的最少資料量。 如果您的資料量超過最低需求，您的模型可能會提供更精確的結果。 如果您的數量少於所需的最小數量，則模型會失敗，因為沒有足夠的資料用於模型培訓。

**公式**:

要確定系統內現有資料的最短所需持續時間，請執行以下操作：

- 建立功能所需的最低資料為30天。 比較30天的資格回顧期間：

   - 如果資格回顧期間超過30天，資料需求=資格回顧期間+結果期間。

   - 否則，資料需求= 30天+結果視窗。

**如果定義合格母體有多個條件，資格回顧期間為最長的一個。

>[!NOTE]
>
>30是合格人口所需的最低天數。 若未提供，預設值為45天。

**範例**:

- 您想要預測過去60天內有某些網路活動的客戶，未來30天內是否可能購買手錶。

   - 資格回顧期間= 60天

   - 結果窗口= 30天

   - 所需資料= 60天+ 30天= 90天

- 您想要預測使用者是否可能在未來7天內購買手錶 **無** 提供明確的合格人口。 在這種情況下，合格人口預設為「過去45天內有活動的人」，結果窗口為7天。

   - 資格回顧期間= 45天

   - 結果窗口= 7天

   - 所需資料= 45天+ 7天= 52天

- 您想要預測過去7天內有網路活動的客戶，未來7天是否可能購買手錶。

   - 資格回顧期間= 7天

   - 建立功能所需的最低資料= 30天

   - 結果窗口= 7天

   - 所需資料= 30天+ 7天= 37天

雖然Customer AI需要最短的時間，才能讓資料存在於系統中，但它對最近的資料也有最佳的效用。 借由使用更新的行為資料，Customer AI可能會產生更精確的使用者未來行為預測。

## Customer AI輸出資料 {#customer-ai-output-data}

Customer AI會為個別設定檔產生數個屬性，這些設定檔被認為符合資格。 根據您已布建的項目，有兩種方式可以取用分數（輸出）。 如果您有已啟用「即時客戶設定檔」的資料集，您可以在 [區段產生器](../../segmentation/ui/segment-builder.md). 如果您沒有已啟用設定檔的資料集，您可以 [下載Customer AI輸出](./user-guide/download-scores.md) 資料湖上可用的資料集。

您可以在Platform中找到輸出資料集 **資料集** 工作區。 所有Customer AI輸出資料集的開頭皆為名稱 **Customer AI分數 — NAME_OF_APP**. 同樣地，所有Customer AI輸出結構都以名稱開頭 **Customer AI結構 — Name_of_app**.

![Customer AI中的輸出資料集名稱](./images/user-guide/cai-schema-name-of-app.png)

下表說明在Customer AI輸出中找到的各種屬性：

| 屬性 | 說明 |
| ----- | ----------- |
| [!UICONTROL 分數] | 客戶在定義的時間範圍內達到預測目標的相對可能性。 此值不會視為機率百分比，而是個人與整體人口比較的可能性。 此分數的範圍介於0到100之間。 |
| 機率 | 此屬性是設定檔在定義時間範圍內達到預測目標的真實機率。 比較不同目標的輸出時，建議您考量機率高於百分位數或分數。 在決定合格母體的平均機率時，應一律使用機率，因為不經常發生的事件的機率通常位於較低端。 機率範圍介於0和1之間的值。 |
| 百分位數 | 此值提供關於設定檔相對於其他類似計分設定檔之效能的資訊。 例如，流失率的百分位數排名為99的設定檔，表示其產生轉譯的風險較高，而分數的其他設定檔只有99%。 百分位數範圍從1到100。 |
| 傾向類型 | 選取的傾向類型。 |
| 分數日期 | 發生分數的日期。 |
| 影響因素 | 這些是設定檔可能轉換或流失的原因。 這些因素包括下列屬性：<ul><li>代碼：正面影響設定檔預測分數的設定檔或行為屬性。 </li><li>值：設定檔或行為屬性的值。</li><li>重要性：指出設定檔或行為屬性的權重對預測分數（低、中、高）</li></ul> |

## 後續步驟 {#next-steps}

準備資料並確定所有認證和結構就緒後，請參閱 [設定Customer AI例項](./user-guide/configure.md) 指南，逐步引導您建立Customer AI例項。