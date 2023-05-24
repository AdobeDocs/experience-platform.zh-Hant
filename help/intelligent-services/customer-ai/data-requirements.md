---
keywords: Experience Platform；入門；客戶ai；熱門主題；客戶ai輸入；客戶ai輸出；資料要求
solution: Experience Platform, Real-time Customer Data Platform
feature: Customer AI
title: 客戶AI中的資料需求
topic-legacy: Getting started
description: 瞭解客戶AI使用的所需事件、輸入和輸出的詳細資訊。
exl-id: 9b21a89c-bf48-4c45-9eb3-ace38368481d
source-git-commit: 5f7b602b68f5cbf4b1f4b08603757b0956e36408
workflow-type: tm+mt
source-wordcount: '2484'
ht-degree: 2%

---


# 客戶AI中的輸入和輸出

下面的文檔概述了客戶AI中使用的不同必需事件、輸入和輸出。

## 快速入門 {#getting-started}

以下是在客戶AI中建立傾向模型並確定個性化營銷的目標受眾的步驟：

1. 大綱使用案例：傾向模型如何幫助確定個性化營銷的目標受眾？ 我的業務目標和相應的策略是什麼？ 傾向建模在這一過程中可以適應什麼？

2. 優先確定使用案例：哪些是企業最優先的任務？

3. 在客戶AI中構建模型：看這個 [快速教程](https://experienceleague.adobe.com/docs/platform-learn/tutorials/intelligent-services/configure-customer-ai.html?lang=zh-Hant) 將我們 [UI指南](../customer-ai/user-guide/configure.md) 的下界。

4. [生成段](../customer-ai/user-guide/create-segment.md) 使用模型結果。

5. 根據這些領域採取有針對性的業務操作。 監視結果並迭代操作以改進。

下面是第一個型號的配置示例。  在本文檔中構建的示例模型使用客戶AI模型來預測未來30天內哪些人可能轉換為零售業務。 輸入資料集是Adobe Analytics資料集。

| 步驟 | 定義 | 範例 |
| ---- | ------ | ------- |
| 設定 | 指定有關模型的基本資訊。 | **名稱**:鉛筆購買傾向模型 <br> **模型類型**:轉換 |
| 選擇資料 | 指定用於構建模型的資料集。 | **資料集**:Adobe Analytics資料集 <br> **身份**:確保將每個資料集的標識列設定為公共標識。 |
| 定義目標 | 定義目標、合格填充、自定義事件和配置檔案屬性。 | **預測目標**:選擇 `commerce.purchases.value` 等於鉛筆 <br> **結果窗口**:30天。 |
| 設定選項 | 設定模型刷新的計畫並啟用配置檔案的分數 | **計畫**:每週 <br> **啟用配置檔案**:必須啟用此功能，以便模型輸出用於分段。 |

## 資料概述 {#data-overview}

以下各節概述了客戶AI中使用的不同必需事件、輸入和輸出。

客戶AI通過分析以下資料集來預測流失率（當客戶可能停止使用產品時）或轉換率（當客戶可能購買產品時）傾向得分：

- Adobe Analytics資料使用 [分析源連接器](../../sources/tutorials/ui/create/adobe-applications/analytics.md)
- Adobe Audience Manager資料使用 [Audience Manager源連接器](../../sources/tutorials/ui/create/adobe-applications/audience-manager.md)
- [體驗事件資料集](https://experienceleague.adobe.com/docs/experience-platform/xdm/classes/experienceevent.html)
- [消費者體驗事件資料集](https://experienceleague.adobe.com/docs/experience-platform/intelligent-services/data-preparation.html#cee-schema)

如果每個資料集共用相同的標識類型（命名空間）（如ECID），則可以從不同源添加多個資料集。 有關添加多個資料集的詳細資訊，請訪問 [客戶AI使用手冊](../customer-ai/user-guide/configure.md)。

>[!IMPORTANT]
>
>源連接器最多需要4週時間來回填資料。 如果您最近設定了連接器，則應驗證資料集是否具有客戶AI所需的最小資料長度。 請查看 [歷史資料](#data-requirements) 部分，以驗證您有足夠的資料實現預測目標。

下表概述了本文檔中使用的一些常用術語：

| 詞語 | 定義 |
| --- | --- |
| [體驗資料模型(XDM)](../../xdm/home.md) | XDM是一個基礎框架，它讓由Adobe Experience Platform牽頭的Adobe Experience Cloud能夠在正確的時間，在正確的渠道向正確的人傳遞正確的資訊。 平台使用XDM系統以一定的方式組織資料，使平台服務更易於使用。 |
| [XDM 結構](../../xdm/schema/composition.md) | Experience Platform 會使用結構，以一致且可重複使用的方式說明資料結構。藉由定義跨系統的一致資料，將可輕易保留意義，而發揮資料應有的價值。在將資料引入平台之前，必須構建一個架構來描述資料的結構，並對每個欄位中可以包含的資料類型提供約束。 架構由基本XDM類和零個或多個架構欄位組組成。 |
| [XDM類](../../xdm/schema/field-constraints.md) | 所有XDM架構都描述可分類為 `Experience Event`。 架構的資料行為由架構的類定義，該類在首次建立架構時分配給該架構。 XDM類描述模式必須包含的最小屬性數以表示特定資料行為。 |
| [欄位群組](../../xdm/schema/composition.md) | 定義架構中一個或多個欄位的元件。 欄位組強制實施其欄位在架構層次結構中的顯示方式，因此在每個架構中都顯示了與其包含的相同結構。 欄位組僅與由其標識的特定類相容 `meta:intendedToExtend` 屬性。 |
| [資料類型](../../xdm/schema/composition.md) | 還可以為架構提供一個或多個欄位的元件。 但是，與欄位組不同，資料類型不受特定類的限制。 這使得資料類型成為描述可跨具有潛在不同類的多個架構重複使用的通用資料結構的更靈活選項。 本文檔中概述的資料類型受CEE和Adobe Analytics架構的支援。 |
| [即時客戶個人檔案](../../profile/home.md) | 即時客戶概要資訊為有針對性的個性化體驗管理提供了集中的消費者概要資訊。 每個配置檔案都包含所有系統之間聚合的資料，以及可操作的時間戳事件帳戶，這些事件涉及您使用的任何系統中與Experience Platform一起發生的個人。 |

## 客戶AI輸入資料 {#customer-ai-input-data}

對於輸入資料集，如Adobe Analytics和Adobe Audience Manager，在連接過程中，預設情況下，各個源連接器會直接映射這些標準欄位組（Commerce、Web、Application和Search）中的事件。 下表顯示了客戶AI的預設標準欄位組中的事件欄位。

有關映射Adobe Analytics資料或Audience Manager資料的詳細資訊，請訪問分析欄位映射或Audience Manager [欄位映射指南](../../sources/connectors/adobe-applications/mapping/audience-manager.md)。

您可以將「體驗事件」或「消費者體驗事件XDM」架構用於未通過上述連接器之一填充的輸入資料集。 在模式建立過程中可以添加其他XDM欄位組。 欄位組可以通過Adobe（如標準欄位組或自定義欄位組）提供，這些欄位組與平台中的資料表示形式相匹配。

>[!IMPORTANT]
>
>必須確保資料正在填充到這些輸入資料集中。 如果在輸入資料集中找不到來自標準欄位組的事件，則必須在配置工作流期間添加自定義事件。 請參閱有關自定義事件的詳細資訊。

### 客戶AI使用的標準欄位組 {#standard-events}

體驗事件用於確定各種客戶行為。 根據資料的結構，下面列出的事件類型可能不包括客戶的所有行為。 您需要確定哪些欄位具有明確、明確地標識Web或其他特定於渠道的用戶活動所需的必要資料。 根據您的預測目標，所需的必填欄位可能會更改。

>[!NOTE]
>
>如果您使用Adobe Analytics或Adobe Audience Manager資料，則系統會自動建立模式，並使用捕獲資料所需的標準事件。 如果要建立自己的自定義EE架構來捕獲資料，則需要考慮捕獲資料所需的欄位組。

預設情況下，客戶AI使用以下四個標準欄位組中的事件：Commerce 、 Web 、 Application和Search。 在下面列出的標準欄位組中，不必為每個事件都提供資料，但某些情況需要某些事件。 如果您在標準欄位組中有任何可用事件，建議將其包含在您的架構中。 例如，如果要建立用於預測採購事件的客戶AI模型，則使用「商業」和「網頁詳細資訊」欄位組中的資料非常有用。

要在平台UI中查看欄位組，請選擇 **[!UICONTROL 架構]** 頁籤，然後選擇 **[!UICONTROL 欄位組]** 頁籤。

| 欄位群組 | 事件類型 | XDM欄位路徑 |
| --- | --- | --- |
| [!UICONTROL 商業詳細資訊] | 訂購 | <li> `commerce.order.purchaseID` </li> <li> `productListItems.SKU` </li> |
|  | productListViews | <li> `commerce.productListViews.value` </li> <li> `productListItems.SKU` </li> |
|  | 檢查 | <li> `commerce.checkouts.value` </li> <li> `productListItems.SKU` </li> |
|  | 購買 | <li> `commerce.purchases.value` </li> <li> `productListItems.SKU` </li> |
|  | productList刪除 | <li> `commerce.productListRemovals.value` </li> <li> `productListItems.SKU` </li> |
|  | 產品清單開啟 | <li> `commerce.productListOpens.value` </li> <li> `productListItems.SKU` </li> |
|  | 產品視圖 | <li> `commerce.productViews.value` </li> <li> `productListItems.SKU` </li> |
| [!UICONTROL Web詳細資訊] | web訪問 | `web.webPageDetails.name` |
|  | Web交互 | `web.webInteraction.linkClicks.value` |
| [!UICONTROL 應用程式詳細資訊] | 應用程式關閉 | <li> `application.applicationCloses.value` </li> <li> `application.name` </li> |
|  | 應用程式崩潰 | <li> `application.crashes.value` </li> <li> `application.name` </li> |
|  | 應用程式功能使用實例 | <li> `application.featureUsages.value` </li> <li> `application.name` </li> |
|  | applicationFirstLoants | <li> `application.firstLaunches.value` </li> <li> `application.name` </li> |
|  | 應用程式安裝 | <li> application.installs.value </li> <li> `application.name` </li> |
|  | 應用程式啟動 | <li> application.launches.value </li> <li> `application.name` </li> |
|  | 應用程式升級 | <li> application.upgrades.value </li> <li> `application.name` </li> |
| [!UICONTROL 搜索詳細資訊] | 搜尋 | `search.keywords` |

此外，客戶AI可以使用訂閱資料構建更好的流失模型。 使用 [[!UICONTROL 訂閱]](../../xdm/data-types/subscription.md) 資料類型格式。 但是，大多數欄位都是可選的，對於最佳的流失模型，強烈建議您為盡可能多的欄位提供資料，例如， `startDate`。 `endDate`，以及其他相關細節。 請聯繫您的客戶團隊，獲取有關此功能的其他支援。

### 添加自定義事件和配置檔案屬性 {#add-custom-events}

如果您有除預設值之外還要包括的資訊 [標準事件欄位](#standard-events) 由客戶AI使用，您可以 [自定義事件配置](./user-guide/configure.md#custom-events) 來增加模型使用的資料。

#### 何時使用自定義事件

在資料集選擇步驟中選擇的資料集包含以下內容時，需要自定義事件 *無* 客戶AI使用的預設事件欄位。 客戶AI需要有關結果以外的至少一個用戶行為事件的資訊。

自定義事件對以下項目有幫助：

- 將領域知識或先前的專業知識納入模型。

- 提高預測模型質量。

- 獲得更多的見解和解釋。

自定義事件的最佳候選者是包含可能預測結果的域知識的資料。 自定義事件的一些一般示例包括：

- 註冊帳戶

- 訂閱新聞稿

- 致電客戶服務

以下是一些特定於行業的自定義事件示例：

| 產業 | 自訂事件 |
| --- | --- |
| 零售 | 店內事務<br>註冊俱樂部卡<br>剪輯移動優惠券。 |
| 娛樂 | 採購季成員 <br> 流視頻。 |
| 招待 | 預訂餐廳 <br> 購買會員積分。 |
| 旅行 | 添加已知旅行者資訊購買英里數。 |
| 通訊 | 升級/降級/取消計畫。 |

自定義事件必須表示用戶啟動的操作才能被選擇。 例如，「電子郵件發送」是由營銷人員而不是用戶啟動的操作，因此不應將其用作自定義事件。

### 歷史資料

客戶AI需要歷史資料進行模型培訓。 資料在系統記憶體在所需的持續時間由兩個關鍵要素決定：結果窗口和合格人口。

預設情況下，如果在應用程式配置期間未提供符合條件的填充定義，則客戶AI會查找用戶在過去45天內有活動。 此外，客戶AI要求根據預測目標定義從歷史資料中最少500個合格事件和500個不合格事件（共1000個）。

以下示例演示了如何使用一個簡單的公式來幫助您確定所需的最小資料量。 如果資料超過最低要求，則模型可能提供更準確的結果。 如果小於所需的最小數量，則模型將失敗，因為沒有足夠的資料用於模型培訓。

**公式**:

要確定系統內現有資料的最小所需持續時間，請執行以下操作：

- 建立功能所需的最少資料為30天。 將資格回查窗口與30天進行比較：

   - 如果資格回望窗口大於30天，則資料要求=資格回望窗口+結果窗口。

   - 否則，資料需求= 30天+結果窗口。

**如果定義合格人口有多個條件，則資格回查窗口是最長的條件。

>[!NOTE]
>
>30是合格人口所需的最低天數。 如果未提供此選項，則預設值為45天。

**範例**:

- 您希望預測客戶是否可能在未來30天內為那些在過去60天內有Web活動的客戶購買手錶。

   - 資格回查窗口= 60天

   - 結果窗口= 30天

   - 所需資料= 60天+ 30天= 90天

- 您想預測用戶是否可能在接下來的7天內購買手錶 **無** 提供明確的合格人口。 在這種情況下，合格人口預設為「過去45天內有活動的人」，結果窗口為7天。

   - 資格回查窗口= 45天

   - 結果窗口= 7天

   - 所需資料= 45天+ 7天= 52天

- 您希望預測客戶是否可能在接下來的7天內為那些在過去7天內有某些Web活動的人購買手錶。

   - 資格回查窗口= 7天

   - 建立功能所需的最少資料= 30天

   - 結果窗口= 7天

   - 所需資料= 30天+ 7天= 37天

儘管客戶AI要求資料在系統記憶體在最短時間，但它對最新資料也最有效。 通過使用更新的行為資料，客戶AI可能能夠更準確地預測用戶的未來行為。

## 客戶AI輸出資料 {#customer-ai-output-data}

客戶AI為被視為合格的單個配置檔案生成多個屬性。 根據您已預配的內容，有兩種方法來使用分數（輸出）。 如果您有啟用即時客戶配置檔案的資料集，則可以使用中的「即時客戶配置檔案」中的洞見 [段生成器](../../segmentation/ui/segment-builder.md)。 如果沒有啟用配置檔案的資料集，則可以 [下載客戶AI輸出](./user-guide/download-scores.md) 資料集在資料湖上可用。

可以在平台中找到輸出資料集 **資料集** 工作區。 所有客戶AI輸出資料集都以名稱開頭 **客戶AI分數 — NAME_OF_APP**。 同樣，所有客戶AI輸出架構都以名稱開頭 **客戶AI架構 — 名稱_of_app**。

![客戶AI中輸出資料集的名稱](./images/user-guide/cai-schema-name-of-app.png)

下表介紹了在客戶AI輸出中找到的各種屬性：

| 屬性 | 說明 |
| ----- | ----------- |
| [!UICONTROL 分數] | 客戶在定義的時間範圍內實現預測目標的相對可能性。 這個值不應被視為概率百分比，而應被視為個人與總體人口相比的可能性。 此分數範圍為0到100。 |
| 概率 | 此屬性是在定義的時間範圍內實現預測目標的配置檔案的真實概率。 在比較不同目標之間的輸出時，建議您考慮概率超出百分點或分數。 在確定整個合格群體的平均概率時，應始終使用概率，因為對於不經常發生的事件，概率往往處於較低水準。 概率範圍在0和1之間的值。 |
| 百分點 | 此值提供有關配置檔案相對於其他類似得分的配置檔案的效能的資訊。 例如，一個百分位等級為99的流失檔案表明，與所有其他得分檔案中的99%相比，它有更高的翻譯風險。 百分位數範圍為1到100。 |
| 傾向類型 | 所選傾向類型。 |
| 分數日期 | 發生計分的日期。 |
| 影響因素 | 這些是預測的原因，說明為什麼一個檔案很可能轉換或篡改。 這些因素包括以下屬性：<ul><li>代碼：對配置檔案的預測得分產生積極影響的配置檔案或行為屬性。 </li><li>值：配置檔案或行為屬性的值。</li><li>重要性：指示配置檔案或行為屬性對預測分數（低、中、高）的權重</li></ul> |

## 後續步驟 {#next-steps}

準備資料並確保所有憑據和架構都到位後，請參閱 [配置客戶AI實例](./user-guide/configure.md) 指南，它指導您逐步完成建立客戶AI實例的教程。