---
keywords: Experience Platform；快速入門；Attributionai；熱門主題；Attributionai輸入；Attributionai輸出；
feature: Attribution AI
title: 輸入和輸出(在Attribution AI中)
description: 以下文檔概述了Attribution AI中使用的不同輸入和輸出。
exl-id: d6dbc9ee-0c1a-4a5f-b922-88c7a36a5380
source-git-commit: e4e30fb80be43d811921214094cf94331cbc0d38
workflow-type: tm+mt
source-wordcount: '2504'
ht-degree: 3%

---

# 輸入和輸出 [!DNL Attribution AI]

以下檔案概述 [!DNL Attribution AI].

## [!DNL Attribution AI] 輸入資料

Attribution AI的運作方式是分析下列資料集，據以計算演算法分數：

- Adobe Analytics資料集使用 [Analytics來源連接器](../../sources/tutorials/ui/create/adobe-applications/analytics.md)
- 一般來自Adobe Experience Platform結構的體驗事件(EE)資料集
- 消費者體驗事件(CEE)資料集

您現在可以根據 **身分圖** （欄位），如果每個資料集都有相同的身分類型（命名空間），例如ECID。 選取身分和命名空間後，ID欄完整性量度就會顯示，指出要匯整的資料量。 若要進一步了解新增多個資料集，請造訪 [Attribution AI使用指南](./user-guide.md#identity).

預設不會一律對應通道資訊。 在某些情況下，如果mediaChannel（欄位）空白，在將欄位映射到mediaChannel之前，您將無法「繼續」，因為它是必填欄位。 如果在資料集中偵測到管道，則預設會對應至mediaChannel 。 其他欄，例如 **媒體類型** 和 **媒體動作** 仍為選用。

對應管道欄位後，請繼續「定義事件」步驟，您可在此選取轉換事件、接觸點事件，以及從個別資料集選擇特定欄位。

>[!IMPORTANT]
>
>Adobe Analytics來源連接器最多可能需要四周時間來回填資料。 如果您最近設定了連接器，應確認資料集的資料長度是Attribution AI所需的最小值。 請查看 [歷史資料](#data-requirements) 區段來驗證您有足夠的資料來計算精確的演算法分數。

如需設定 [!DNL Consumer Experience Event] (CEE)架構，請參閱 [Intelligent Services資料準備](../data-preparation.md) 指南。 如需對應Adobe Analytics資料的詳細資訊，請造訪 [Analytics欄位對應](../../sources/connectors/adobe-applications/analytics.md) 檔案。

並非 [!DNL Consumer Experience Event] (CEE)結構是Attribution AI的必要結構。

您可以使用架構或所選資料集中下方建議的任何欄位來設定接觸點。

| 建議的欄 | 需要 |
| --- | --- |
| 主要身分欄位 | 接觸點/轉換 |
| 時間戳記 | 接觸點/轉換 |
| Channel._type | 接觸點 |
| Channel.mediaAction | 接觸點 |
| Channel.mediaType | 接觸點 |
| Marketing.trackingCode | 接觸點 |
| Marketing.campaignname | 接觸點 |
| Marketing.campaigngroup | 接觸點 |
| Commerce | 轉換 |

歸因通常會在「商務」下的「訂購」、「購買」和「結帳」等轉換欄上執行。 「管道」和「行銷」的欄可用來定義Attribution AI的接觸點(例如 `channel._type = 'https://ns.adobe.com/xdm/channel-types/email'`)。 為獲得最佳結果和深入分析，強烈建議您納入盡可能多的轉換和接觸點欄。 此外，您也不限於上述欄。 您可以將任何其他建議或自訂欄加入為轉換或接觸點定義。

只要與設定接觸點相關的管道或行銷活動資訊存在於mixin或傳遞欄位之一，資料集就不需要明確具有管道和行銷混合。

>[!TIP]
>
>如果您在CEE架構中使用Adobe Analytics資料，Analytics的接觸點資訊通常會儲存在 `channel.typeAtSource` (例如， `channel.typeAtSource = 'email'`)。

## 歷史資料 {#data-requirements}

>[!IMPORTANT]
>
> Attribution AI運作所需的最小資料量如下：
> - 您需要提供至少3個月（90天）的資料，才能執行良好的模型。
> - 您至少需要1000次轉換。


Attribution AI需要歷史資料作為模型訓練的輸入。 所需的資料持續時間主要取決於兩個關鍵因素：訓練窗口和回顧窗口。 較短的培訓窗口對最新趨勢更敏感，而較長的培訓窗口有助於生成更穩定、更準確的模型。 以最能代表您業務目標的歷史資料來建立目標模型非常重要。

此 [培訓窗口配置](./user-guide.md#training-window) 根據發生時間篩選要納入模型訓練的轉換事件。 目前，最低培訓期間為1個季度（90天）。 此 [回顧期間](./user-guide.md#lookback-window) 提供一個時間範圍，指出應包含多少天前的轉換事件接觸點與此轉換事件相關。 這兩個概念共同決定應用程式所需的輸入資料量（以天計量）。

預設情況下，Attribution AI將培訓期間定義為最近的2個季度（6個月），將回顧期間定義為56天。 換言之，模型會考慮過去2個季度發生的所有已定義轉換事件，並尋找在相關轉換事件前56天內發生的所有接觸點。

**公式**:

所需資料的最小長度=訓練期間+回顧期間

>[!TIP]
>
> 具有預設配置的應用程式所需的資料的最小長度為：2個季度（180天）+ 56天= 236天。

範例：

- 您想要歸因過去90天（3個月）內發生的轉換事件，並追蹤轉換事件前4週內發生的所有接觸點。 輸入資料的持續時間應會跨越過去90天+ 28天（4週）。 培訓期間為90天，回顧期間為28天，總計為118天。

## Attribution AI輸出資料

Attribution AI會輸出下列項目：

- [原始粒度分數](#raw-granular-scores)
- [匯總分數](#aggregated-attribution-scores)

**輸出架構示例：**

![](./images/input-output/schema_output.gif)

### 原始粒度分數 {#raw-granular-scores}

Attribution AI會輸出盡可能精細的歸因分數，以便您可以依任何分數欄來分割分數。 若要在UI中檢視這些分數，請閱讀 [檢視原始分數路徑](#raw-score-path). 若要使用API下載分數，請造訪 [下載分數Attribution AI](./download-scores.md) 檔案。

>[!NOTE]
>
> 只有在下列其中一項為真時，您才能從分數輸出資料集的輸入資料集中看到任何所需的報表欄：
> - 報表欄包含在設定頁面中，作為接觸點或轉換定義設定的一部分。
> - 報表欄會包含在其他分數資料集欄中。


下表概述原始分數範例輸出中的架構欄位：

| 欄名稱(DataType) | 可空 | 說明 |
| --- | --- | --- |
| timestamp(DateTime) | False | 轉換事件或觀察發生的時間。 <br> **範例：** 2020-06-09T00:01:51.000Z |
| identityMap(Map) | True | 與CEE XDM格式類似的使用者身分對應。 |
| eventType（字串） | True | 此時間序列記錄的主要事件類型。 <br> **範例：** &quot;Order&quot;、&quot;Purchase&quot;、&quot;Visit&quot; |
| eventMergeId（字串） | True | 關聯或合併多個 [!DNL Experience Events] 本質上是相同事件或應合併的事件。 這會先由資料產生器填入，再擷取。 <br> **範例：** 575525617716-0-edc2ed37-1aab-4750-a820-1c2b3844b8c4 |
| _id（字串） | False | 時間序列事件的唯一識別碼。 <br> **範例：** 4461-edc2ed37-1aab-4750-a820-1c2b3844b8c4 |
| _tenantId（物件） | False | 與您的保留ID對應的頂層物件容器。 <br> **範例：** _atsdsnrmsv2 |
| your_schema_name（對象） | False | 對轉換事件的所有與其相關聯的接觸點事件及其元資料進行分數列。 <br> **範例：** Attribution AI分數 — 型號__2020 |
| 分段（字串） | True | 轉換區段，例如建立模型時所依據的地域劃分。 若缺少區段，則區段與conversionName相同。 <br> **範例：** ORDER_US |
| conversionName（字串） | True | 設定期間所設定的轉換名稱。 <br> **範例：** 訂購、銷售機會、訪問 |
| 轉換（物件） | False | 轉換中繼資料欄。 |
| dataSource（字串） | True | 資料源的全局唯一標識。 <br> **範例：** Adobe Analytics |
| eventSource（字串） | True | 實際事件發生時的來源。 <br> **範例：** Adobe.com |
| eventType（字串） | True | 此時間序列記錄的主要事件類型。 <br> **範例：** 順序 |
| geo（字串） | True | 傳送轉換的地理位置 `placeContext.geo.countryCode`. <br> **範例：** US |
| priceTotal(Double) | True | 透過轉換取得之收入 <br> **範例：** 99.9 |
| product（字串） | True | 產品本身的XDM識別碼。 <br> **範例：** RX 1080 ti |
| productType（字串） | True | 產品的顯示名稱，如此產品檢視向使用者顯示。 <br> **範例：** Gpus |
| 數量（整數） | True | 轉換期間購買的數量。 <br> **範例：** 1 1080鈦 |
| receivedTimestamp(DateTime) | True | 收到轉換的時間戳記。 <br> **範例：** 2020-06-09T00:01:51.000Z |
| skuId（字串） | True | 保存單位(SKU)，由供應商定義之產品的唯一識別碼。 <br> **範例：** MJ-03-XS — 黑 |
| timestamp(DateTime) | True | 轉換的時間戳記。 <br> **範例：** 2020-06-09T00:01:51.000Z |
| passThrough（物件） | True | 設定模型時，使用者指定的其他分數資料集欄。 |
| commerce_order_purchaseCity（字串） | True | 其他分數資料集欄。 <br> **範例：** 城市：聖荷西 |
| customerProfile(Object) | False | 用於建立模型之使用者的身分詳細資料。 |
| 標識（對象） | False | 包含用於建立模型的使用者的詳細資訊，例如 `id` 和 `namespace`. |
| id（字串） | True | 使用者的身分ID，例如Cookie ID、Adobe Analytics ID(AAID)或Experience CloudID（ECID，又稱為MCID或訪客ID）等。 <br> **範例：** 17348762725408656344688320891369597404 |
| 命名空間（字串） | True | 用於建立路徑的身分命名空間，進而建立模型。 <br> **範例：** aaid |
| 接觸點詳細資料（物件陣列） | True | 導致轉換的接觸點詳細資訊清單，依 | 接觸點發生次數或時間戳記。 |
| touchpointName（字串） | True | 設定期間設定的接觸點名稱。 <br> **範例：** PAID_SEARCH_CLICK |
| 分數（物件） | True | 以分數形式貢獻此轉換的接觸點。 如需此物件中產生分數的詳細資訊，請參閱 [匯總歸因分數](#aggregated-attribution-scores) 區段。 |
| touchPoint（物件） | True | 接觸點中繼資料。 如需此物件中產生分數的詳細資訊，請參閱 [匯總分數](#aggregated-scores) 區段。 |

### 檢視原始分數路徑(UI) {#raw-score-path}

您可以在UI中檢視原始分數的路徑。 從選擇開始 **[!UICONTROL 結構]** 然後，在Platform UI中，從 **[!UICONTROL 瀏覽]** 標籤。

![選擇您的架構](./images/input-output/schemas_browse.png)

接下來，在 **[!UICONTROL 結構]** UI的視窗， **[!UICONTROL 欄位屬性]** 標籤。 內 **[!UICONTROL 欄位屬性]** 是映射至原始分數的路徑欄位。

![選擇結構](./images/input-output/field_properties.png)

### 匯總歸因分數 {#aggregated-attribution-scores}

如果日期範圍少於30天，可從Platform UI下載匯總的分數為CSV格式。

Attribution AI支援兩類歸因分數：演算法分數和規則型分數。

Attribution AI會產生兩種不同的演算法分數，分數為增量和受影響。 受影響的分數是每個行銷接觸點所負責轉換的一小部分。 增量分數是行銷接觸點直接造成的邊際影響量。 增量分數與受影響分數之間的主要差異在於，增量分數會將基線效果納入考量。 不會假設轉換純粹是由先前的行銷接觸點造成。

以下是Adobe Experience Platform UI的Attribution AI結構輸出範例：

![](./images/input-output/schema_screenshot.png)

請參閱下表，以取得這些歸因分數的詳細資訊：

| 歸因分數 | 說明 |
| ----- | ----------- |
| 影響（演算法） | 受影響的分數是每個行銷接觸點負責的轉換部分。 |
| 增量（演算法） | 增量分數是行銷接觸點直接造成的邊際影響量。 |
| 首次接觸 | 規則型歸因分數，可將所有評分指派給轉換路徑上的初始接觸點。 |
| 上次接觸 | 規則型歸因分數，會將所有評分指派給最接近轉換的接觸點。 |
| 線性 | 規則型歸因分數，可為轉換路徑上的每個接觸點指派相等的評分。 |
| U 形 | 以規則為基礎的歸因分數，將40%的評分指派給第一個接觸點，並將40%的評分指派給最後一個接觸點，而其他接觸點平分其餘20%。 |
| 時間耗損 | 規則型歸因分數，靠近轉換的接觸點會獲得比離轉換更遠的接觸點更多的評分。 |

**原始分數參考（歸因分數）**

下表將歸因分數對應至原始分數。 如果您想要下載原始分數，請造訪 [下載分數Attribution AI](./download-scores.md) 檔案。

| 歸因分數 | 原始分數參考欄 |
| --- | --- |
| 影響（演算法） | _tenantID.your_schema_name.element.touchpoint.algorithmicAffected |
| 增量（演算法） | _tenantID.your_schema_name.touchpointsDetail.element.touchpoint.algorithmAffected |
| 首次接觸 | _tenantID.your_schema_name.touchpointsDetail.element.touchpoint.firstTouch |
| 上次接觸 | _tenantID.your_schema_name.touchpointsDetail.element.touchpoint.lastTouch |
| 線性 | _tenantID.your_schema_name.touchpointsDetail.element.touchpoint.linear |
| U 形 | _tenantID.your_schema_name.touchpointsDetail.element.touchpoint.uShape |
| 時間耗損 | _tenantID.your_schema_name.touchpointsDetail.element.touchpoint.decayUnits |

### 匯總分數 {#aggregated-scores}

如果日期範圍少於30天，可從Platform UI下載匯總的分數為CSV格式。 請參閱下表，以取得這些匯總欄的詳細資訊。

| 欄名稱 | 限制 | 可空 | 說明 |
| --- | --- | --- | --- |
| customerevents_date(DateTime) | 用戶定義和固定格式 | False | 客戶事件日期（YYYY-MM-DD格式）。 <br> **範例**:2016-05-02 |
| mediatouchpoints_date(DateTime) | 用戶定義和固定格式 | True | YYYY-MM-DD格式的媒體接觸點日期 <br> **範例**:2017-04-21 |
| 區段（字串） | 計算 | False | 轉換區段，例如建立模型時所依據的地域劃分。 若缺少區段，則區段與conversion_scope相同。 <br> **範例**:ORDER_AMER |
| conversion_scope（字串） | 用戶定義 | False | 轉換的名稱，如使用者所設定。 <br> **範例**:訂購 |
| touchpoint_scope（字串） | 用戶定義 | True | 使用者設定的接觸點名稱 <br> **範例**:PAID_SEARCH_CLICK |
| product（字串） | 用戶定義 | True | 產品的XDM識別碼。 <br> **範例**:CC |
| product_type（字串） | 用戶定義 | True | 產品的顯示名稱，如此產品檢視向使用者顯示。 <br> **範例**:gpus，筆記型電腦 |
| geo（字串） | 用戶定義 | True | 傳送轉換的地理位置(placeContext.geo.countryCode) <br> **範例**:US |
| event_type（字串） | 用戶定義 | True | 此時間序列記錄的主要事件類型 <br> **範例**:付費轉換 |
| media_type（字串） | 列舉 | False | 說明媒體類型是付費、擁有還是獲得。 <br> **範例**:付費、擁有 |
| channel（字串） | 列舉 | False | 此 `channel._type` 屬性，用於提供具有類似屬性之管道的粗略分類 [!DNL Consumer Experience Event] XDM. <br> **範例**:搜尋 |
| 動作（字串） | 列舉 | False | 此 `mediaAction` 屬性可用來提供體驗事件媒體動作的類型。 <br> **範例**:按一下 |
| campaign_group（字串） | 用戶定義 | True | 促銷活動群組的名稱，其中多個促銷活動會分組在一起，如&#39;50%_DISCOUNT&#39;。 <br> **範例**:商業 |
| campaign_name（字串） | 用戶定義 | True | 用於識別行銷活動的促銷活動名稱，例如&#39;50%_DISCOUNT_USA&#39;或&#39;50%_DISCOUNT_ASIA&#39;。 <br> **範例**:感恩節大賣 |

**原始分數參考（匯總）**

下表將匯總的分數對應至原始分數。 如果您想要下載原始分數，請造訪 [下載分數Attribution AI](./download-scores.md) 檔案。 若要從UI內檢視原始分數路徑，請造訪 [檢視原始分數路徑](#raw-score-path) 。

| 欄名稱 | 原始分數參考欄 |
| --- | --- |
| customrevents_date | timestamp |
| mediatouchpoints_date | _tenantID.your_schema_name.touchpointsDetail.element.touchpoint.timestamp |
| 區段 | _tenantID.your_schema_name.segmentation |
| conversion_scope | _tenantID.your_schema_name.conversion.conversionName |
| touchpoint_scope | _tenantID.your_schema_name.touchpointsDetail.element.touchpointName |
| product | _tenantID.your_schema_name.conversion.product |
| product_type | _tenantID.your_schema_name.conversion.product_type |
| 地理 | _tenantID.your_schema_name.conversion.geo |
| event_type | eventType |
| media_type | _tenantID.your_schema_name.touchpointsDetail.element.touchpoint.mediaType |
| channel | _tenantID.your_schema_name.touchpointsDetail.element.touchpoint.mediaChannel |
| 動作 | _tenantID.your_schema_name.touchpointsDetail.element.touchpoint.mediaAction |
| campaign_group | _tenantID.your_schema_name.touchpointsDetail.element.touchpoint.campaignGroup |
| campaign_name | _tenantID.your_schema_name.touchpointsDetail.element.touchpoint.campaignName |

>[!IMPORTANT]
>
> - Attribution AI僅使用更新的資料以進一步訓練和評分。 同樣地，當您請求刪除資料時，Customer AI不會使用已刪除的資料。
> - Attribution AI可運用Platform資料集。 為支援品牌可能收到的消費者權利請求，品牌應使用PlatformPrivacy Service來提交消費者存取和刪除請求，以在資料湖、Identity Service和即時客戶設定檔中移除其資料。
> - 我們用於輸入/輸出模型的所有資料集都將遵循Platform准則。 平台資料加密適用於閒置和傳輸中的資料。 請參閱本檔案以深入了解 [資料加密](../../../help/landing/governance-privacy-security/encryption.md)


## 後續步驟 {#next-steps}

準備好資料並部署所有憑證和結構後，請先遵循 [Attribution AI使用指南](./user-guide.md). 本指南會逐步引導您建立Attribution AI的例項。
