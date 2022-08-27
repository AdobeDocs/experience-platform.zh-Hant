---
keywords: Experience Platform；入門；屬性；流行主題；屬性；輸入；屬性；輸出；
feature: Attribution AI
title: 輸入和輸出在Attribution AI
topic-legacy: Input and Output data for Attribution AI
description: 下面的檔案概述了在Attribution AI中使用的不同輸入和輸出。
exl-id: d6dbc9ee-0c1a-4a5f-b922-88c7a36a5380
source-git-commit: e0e96a52e30f5c34e0695c3e291bed9b6c085e00
workflow-type: tm+mt
source-wordcount: '2491'
ht-degree: 3%

---

# 輸入和輸出 [!DNL Attribution AI]

下文檔概述了在 [!DNL Attribution AI]。

## [!DNL Attribution AI] 輸入資料

Attribution AI通過分析以下資料集來計算算法得分：

- Adobe Analytics資料集 [分析源連接器](../../sources/tutorials/ui/create/adobe-applications/analytics.md)
- 一般來自Adobe Experience Platform架構的經驗事件(EE)資料集
- 消費者體驗事件(CEE)資料集

現在，您可以根據 **身份映射** （欄位），如果每個資料集共用相同的標識類型（命名空間），如ECID。 選擇標識和命名空間後，將顯示ID列完整性度量，該度量指示要縫合的資料量。 要瞭解有關添加多個資料集的詳細資訊，請訪問 [Attribution AI使用手冊](./user-guide.md#identity)。

預設情況下，通道資訊並不總是映射。 在某些情況下，如果mediaChannel(field)為空，則在將欄位映射到mediaChannel（因為它是必需的列）之前，將無法「繼續」。 如果在資料集中檢測到該通道，則預設情況下會將其映射到mediaChannel。 其他列，如 **媒體類型** 和 **媒體操作** 是可選的。

映射通道欄位後，繼續執行「定義事件」步驟，在該步驟中，您可以選擇轉換事件、觸點事件，並從單個資料集中選擇特定欄位。

>[!IMPORTANT]
>
>Adobe Analytics源連接器最多需要四周時間來回填資料。 如果最近設定了連接器，則應驗證資料集是否具有Attribution AI所需的最小資料長度。 請查看 [歷史資料](#data-requirements) 部分，以驗證您有足夠的資料來計算準確的算法得分。

有關設定的詳細資訊 [!DNL Consumer Experience Event] (CEE)架構，請參閱 [智慧服務資料準備](../data-preparation.md) 的子菜單。 有關映射Adobe Analytics資料的詳細資訊，請訪問 [分析欄位映射](../../sources/connectors/adobe-applications/analytics.md) 文檔。

不是 [!DNL Consumer Experience Event] (CEE)架構是必需的Attribution AI。

可以使用架構或所選資料集中下面建議的任何欄位配置觸摸點。

| 推薦列 | 需要 |
| --- | --- |
| 主標識欄位 | 觸點/轉換 |
| 時間戳記 | 觸點/轉換 |
| Channel._type | 觸點 |
| Channel.mediaAction | 觸點 |
| Channel.mediaType | 觸點 |
| Marketing.trackingCode | 觸點 |
| Marketing.campaignname | 觸點 |
| Marketing.campaigngroup | 觸點 |
| Commerce | 轉換 |

通常，屬性在「商務」下的訂單、採購和簽出等轉換列上運行。 「渠道」和「營銷」的列用於定義Attribution AI的觸點(例如， `channel._type = 'https://ns.adobe.com/xdm/channel-types/email'`)。 為獲得最佳結果和洞察力，強烈建議您盡可能多地包含轉換列和觸點列。 此外，您不僅限於上述列。 可以將任何其它建議或自定義列作為轉換或觸點定義。

體驗事件(EE)資料集只要與配置觸點相關的渠道或市場活動資訊存在於混合或傳遞欄位之一，就不需要明確地包含渠道和營銷混合。

>[!TIP]
>
>如果您在CEE架構中使用Adobe Analytics資料，則分析的觸點資訊通常儲存在 `channel.typeAtSource` (例如， `channel.typeAtSource = 'email'`)。

## 歷史資料 {#data-requirements}

>[!IMPORTANT]
>
> Attribution AI運行所需的最小資料量如下：
> - 您需要提供至少3個月（90天）的資料才能運行一個良好的模型。
> - 至少需要1000次轉換。


Attribution AI需要歷史資料作為模型訓練的輸入。 所需資料持續時間主要由兩個關鍵因素決定：訓練窗口和回顧窗口。 使用較短的培訓窗口進行輸入會更加敏感於最近的趨勢，而較長的培訓窗口有助於生成更穩定和準確的模型。 用最能代表您的業務目標的歷史資料來建模目標非常重要。

的 [培訓窗口配置](./user-guide.md#training-window) 根據發生時間篩選為模型訓練而設定的轉換事件。 目前，最低培訓窗口為1個季度（90天）。 的 [回望窗口](./user-guide.md#lookback-window) 提供一個時間框，指示應包括與此轉換事件相關的轉換事件觸點之前的天數。 這兩個概念一起確定應用程式所需的輸入資料量（以天計量）。

預設情況下，Attribution AI將培訓窗口定義為最近2個季度（6個月），回望窗口定義為56天。 換句話說，該模型將考慮過去2個季度中發生的所有已定義轉換事件，並查找在相關轉換事件之前56天內發生的所有觸點。

**公式**:

所需資料的最小長度=培訓窗口+回望窗口

>[!TIP]
>
> 具有預設配置的應用程式所需的最小資料長度為：2個季度（180天）+ 56天= 236天。

範例：

- 您要對過去90天（3個月）內發生的轉換事件進行屬性化，並跟蹤轉換事件發生前4週內發生的所有觸點。 輸入資料的持續時間應跨越過去90天+ 28天（4週）。 培訓窗口為90天，回望窗口為28天，總計為118天。

## Attribution AI輸出資料

Attribution AI輸出以下內容：

- [原始粒度分數](#raw-granular-scores)
- [聚合分數](#aggregated-attribution-scores)

**輸出架構示例：**

![](./images/input-output/schema_output.gif)

### 原始粒度分數 {#raw-granular-scores}

Attribution AI在盡可能細的級別輸出屬性得分，以便您可以按任何得分列對得分進行切片和分片。 要在UI中查看這些分數，請閱讀上 [查看原始記分路徑](#raw-score-path)。 要使用API下載分數，請訪問 [下載Attribution AI分數](./download-scores.md) 的子菜單。

>[!NOTE]
>
> 只有在以下任一情況下，才能從分數輸出資料集的輸入資料集中查看任何所需的報告列：
> - 報告列作為觸點或轉換定義配置的一部分包含在配置頁中。
> - 報告列包含在其他得分資料集列中。


下表概述了原始分數示例輸出中的架構欄位：

| 列名（資料類型） | 可為Null | 說明 |
| --- | --- | --- |
| 時間戳(DateTime) | False | 發生轉換事件或觀察的時間。 <br> **示例：** 2020-06-09T00:01:51.000Z |
| identityMap（映射） | True | identity與CEE XDM格式類似的用戶映射。 |
| eventType（字串） | 真 | 此時間系列記錄的主要事件類型。 <br> **示例：** &quot;訂單&quot;、&quot;採購&quot;、&quot;訪問&quot; |
| eventMergeId（字串） | 真 | 要關聯或合併多個 [!DNL Experience Events] 本質上是同一事件或應該合併的。 這將在接收之前由資料生成器填充。 <br> **示例：** 575525617716-0-edc2ed37-1ab-4750-a820-1c2b3844b8c4 |
| _id（字串） | 假 | 時間系列事件的唯一標識符。 <br> **示例：** 4461-edc2ed37-1ab-4750-a820-1c2b3844b8c4 |
| _tenantId（對象） | 假 | 與您的堅定ID對應的頂級對象容器。 <br> **示例：** _atsdsnrmmsv2 |
| your_schema_name（對象） | 假 | 使用轉換事件對與其關聯的所有觸點事件及其元資料進行分數行。 <br> **示例：** Attribution AI分數 — 型號名稱__2020 |
| 分段（字串） | 真 | 轉換段，例如建立模型所針對的地理分段。 如果沒有段，則段與conversionName相同。 <br> **示例：** 訂單(_U) |
| conversionName（字串） | 真 | 在安裝過程中配置的轉換的名稱。 <br> **示例：** 訂單、線索、訪問 |
| 轉換（對象） | 假 | 轉換元資料列。 |
| 資料源（字串） | 真 | 資料源的全局唯一標識。 <br> **示例：** Adobe Analytics |
| eventSource（字串） | 真 | 實際事件發生時的源。 <br> **示例：** Adobe |
| eventType（字串） | 真 | 此時間系列記錄的主要事件類型。 <br> **示例：** 訂單 |
| geo（字串） | 真 | 轉換所在的地理位置 `placeContext.geo.countryCode`。 <br> **示例：** 美國 |
| 價格合計（雙） | 真 | 透過轉換可換股債券 <br> **示例：** 九十九點九 |
| product（字串） | 真 | 產品本身的XDM標識符。 <br> **示例：** RX 1080ti |
| productType（字串） | 真 | 此產品視圖向用戶顯示的產品顯示名稱。 <br> **示例：** 格普斯 |
| 數量（整數） | 真 | 轉換期間採購的數量。 <br> **示例：** 小行星1080 |
| receivedTimestamp(DateTime) | 真 | 收到轉換的時間戳。 <br> **示例：** 2020-06-09T00:01:51.000Z |
| skuId（字串） | 真 | 庫存保管單位(SKU)，供應商定義的產品的唯一標識符。 <br> **示例：** MJ-03-XS — 黑色 |
| 時間戳(DateTime) | 真 | 轉換的時間戳。 <br> **示例：** 2020-06-09T00:01:51.000Z |
| 傳遞（對象） | 真 | 配置模型時用戶指定的其他分數資料集列。 |
| commerce_order_purchaseCity（字串） | 真 | 其他得分資料集列。 <br> **示例：** 城市：聖何塞 |
| customerProfile（對象） | 假 | 用於構建模型的用戶的標識詳細資訊。 |
| 標識（對象） | 假 | 包含用於構建模型的用戶的詳細資訊，如 `id` 和 `namespace`。 |
| id（字串） | 真 | 用戶的標識ID，如Cookie ID、AAID或MCID等。 <br> **示例：** 173487627254086563468320891369597404 |
| 命名空間（字串） | 真 | 用於生成路徑和模型的標識命名空間。 <br> **示例：** 救 |
| 觸點詳細資訊（對象陣列） | 真 | 導至轉換的觸點詳細資訊清單，按 | 觸點事件或時間戳。 |
| touchpointName（字串） | 真 | 在安裝過程中配置的觸點名稱。 <br> **示例：** 已付搜索按一下 |
| 分數（對象） | 真 | 此轉換的觸點貢獻為分數。 有關在此對象中生成的分數的詳細資訊，請參見 [聚合屬性分析](#aggregated-attribution-scores) 的子菜單。 |
| touchPoint（對象） | 真 | Touchpoint元資料。 有關在此對象中生成的分數的詳細資訊，請參見 [聚合分數](#aggregated-scores) 的子菜單。 |

### 查看原始分數路徑(UI) {#raw-score-path}

您可以在UI中查看原始分數的路徑。 通過選擇 **[!UICONTROL 架構]** 在平台UI中，然後從 **[!UICONTROL 瀏覽]** 頁籤。

![選擇您的架構](./images/input-output/schemas_browse.png)

接下來，在 **[!UICONTROL 結構]** 窗口， **[!UICONTROL 欄位屬性]** 的子菜單。 在 **[!UICONTROL 欄位屬性]** 是映射到原始分數的路徑欄位。

![選擇架構](./images/input-output/field_properties.png)

### 聚合的歸因分數 {#aggregated-attribution-scores}

如果日期範圍小於30天，可以從平台UI以CSV格式下載聚合分數。

Attribution AI支援兩類屬性得分，算法和基於規則的得分。

Attribution AI產生兩種不同的算法得分，增量和影響。 影響得分是每個市場營銷觸點所負責的轉換的一小部分。 增量分數是由市場營銷觸點直接引起的邊際影響量。 增量分數與影響分數的主要區別在於增量分數考慮了基線效果。 它並不認為轉換純粹是由前面的營銷觸點引起的。

下面是Adobe Experience PlatformUI的Attribution AI架構輸出示例：

![](./images/input-output/schema_screenshot.png)

有關這些屬性分數的詳細資訊，請參閱下表：

| 歸因分數 | 說明 |
| ----- | ----------- |
| 影響（算法） | 影響得分是每個市場營銷觸點所負責的轉換的一小部分。 |
| 增量（算法） | 增量得分是由市場營銷觸點直接引起的邊際影響量。 |
| 首次接觸 | 基於規則的屬性得分，將所有信用分配給轉換路徑上的初始觸點。 |
| 上次接觸 | 基於規則的歸因得分，將所有信用分配給最接近轉換的觸點。 |
| 線性 | 基於規則的屬性得分，為轉換路徑上的每個觸點分配等額信用。 |
| U 形 | 基於規則的歸因得分，將40%的信用分配給第一個觸點，40%的信用分配給最後一個觸點，其他觸點平分其餘20%。 |
| 時間耗損 | 基於規則的歸因得分，即距離轉換較近的觸點比距離轉換時間較遠的觸點獲得更多信用。 |

**原始分數引用（歸因分數）**

下表將屬性得分與原始得分進行映射。 如果您想下載原始分數，請訪問 [下載Attribution AI分數](./download-scores.md) 文檔。

| 歸因分數 | 原始分數引用列 |
| --- | --- |
| 影響（算法） | _tenantID.your_schema_name.element.touchpoint.algoritimEffected |
| 增量（算法） | _tenantID.your_schema_name.touchpointsDetail.element.touchpoint.algoriticEffected |
| 首次接觸 | _tenantID.your_schema_name.touchpointsDetail.element.touchpoint.firstTouch |
| 上次接觸 | _tenantID.your_schema_name.touchpointsDetail.element.touchpoint.lastTouch |
| 線性 | _tenantID.your_schema_name.touchpointsDetail.element.touchpoint.linear |
| U 形 | _tenantID.your_schema_name.touchpointsDetail.element.touchpoint.uShape |
| 時間耗損 | _tenantID.your_schema_name.touchpointsDetail.element.touchpoint.decayUnits |

### 聚合分數 {#aggregated-scores}

如果日期範圍小於30天，可以從平台UI以CSV格式下載聚合分數。 有關這些聚合列的詳細資訊，請參閱下表。

| 列名 | 約束 | 可為Null | 說明 |
| --- | --- | --- | --- |
| customerevents_date(DateTime) | 自定義格式和固定格式 | 假 | YYYY-MM-DD格式的客戶事件日期。 <br> **示例**:2016-05-02 |
| mediatouchpoints_date（日期時間） | 自定義格式和固定格式 | 真 | YYYY-MM-DD格式的媒體觸點日期 <br> **示例**:2017-04-21 |
| 段（字串） | 已計算 | 假 | 轉換段，例如建立模型時所依據的地理分段。 如果沒有段，則段與conversion_scope相同。 <br> **示例**:順序(_A) |
| conversion_scope（字串） | 用戶定義的 | 假 | 用戶配置的轉換的名稱。 <br> **示例**:訂單 |
| touchpoint_scope（字串） | 用戶定義的 | 真 | 用戶配置的Touchpoint的名稱 <br> **示例**:已付搜索按一下 |
| product（字串） | 用戶定義的 | 真 | 產品的XDM標識符。 <br> **示例**:抄送 |
| product_type（字串） | 用戶定義的 | 真 | 此產品視圖向用戶顯示的產品顯示名稱。 <br> **示例**:gpus，筆記型電腦 |
| geo（字串） | 用戶定義的 | 真 | 傳遞轉換的地理位置(placeContext.geo.countryCode) <br> **示例**:美國 |
| event_type（字串） | 用戶定義的 | 真 | 此時間系列記錄的主要事件類型 <br> **示例**:付款轉換 |
| media_type（字串） | 枚舉 | 假 | 描述介質類型是付費、擁有還是獲得。 <br> **示例**:已付、自有 |
| 通道（字串） | 枚舉 | 假 | 的 `channel._type` 屬性，用於提供具有相似屬性的通道的粗略分類 [!DNL Consumer Experience Event] XDM <br> **示例**:搜索 |
| 操作（字串） | 枚舉 | 假 | 的 `mediaAction` 屬性用於提供體驗事件媒體操作的類型。 <br> **示例**:按一下 |
| campaign_group（字串） | 用戶定義的 | 真 | 將多個市場活動組合在一起的市場活動組的名稱，如「50%_DISCOUNT」。 <br> **示例**:商業 |
| campaign_name（字串） | 用戶定義的 | 真 | 用於標識「50%_DISCOUNT_USA」或「50%_DISCOUNT_ASIA」等市場營銷活動的市場活動的名稱。 <br> **示例**:感恩節大促銷 |

**原始分數引用（聚合）**

下表將聚合得分映射到原始得分。 如果您想下載原始分數，請訪問 [下載Attribution AI分數](./download-scores.md) 文檔。 要從UI中查看原始分數路徑，請訪問 [查看原始記分路徑](#raw-score-path) 的下界。

| 列名 | 原始分數引用列 |
| --- | --- |
| customerevents_date | timestamp |
| 中間點_日期 | _tenantID.your_schema_name.touchpointsDetail.element.touchpoint.timestamp |
| 區段 | _tenantID.your_schema_name.segmentation |
| 轉換範圍 | _tenantID.your_schema_name.conversion.conversionName |
| 觸點範圍 | _tenantID.your_schema_name.touchpointsDetail.element.touchpointName |
| product | _tenantID.your_schema_name.conversion.product |
| 產品類型 | _tenantID.your_schema_name.conversion.product_type |
| 地質 | _tenantID.your_schema_name.conversion.geo |
| 事件類型 | 事件類型 |
| 媒體類型 | _tenantID.your_schema_name.touchpointsDetail.element.touchpoint.mediaType |
| channel | _tenantID.your_schema_name.touchpointsDetail.element.touchpoint.mediaChannel |
| 動作 | _tenantID.your_schema_name.touchpointsDetail.element.touchpoint.mediaAction |
| campay_group | _tenantID.your_schema_name.touchpointsDetail.element.touchpoint.campaignGroup |
| 戰役名稱 | _tenantID.your_schema_name.touchpointsDetail.element.touchpoint.campaignName |

>[!IMPORTANT]
>
> - Attribution AI僅使用更新的資料進行進一步的培訓和評分。 同樣，當您請求刪除資料時，客戶AI不會使用刪除的資料。
> - Attribution AI利用平台資料集。 為支援品牌可能收到的消費者權利請求，品牌應使用平台Privacy Service提交消費者訪問請求並刪除，以跨資料庫、身份服務和即時客戶配置檔案刪除其資料。
> - 我們用於模型輸入/輸出的所有資料集都將遵循平台指導原則。 平台資料加密適用於靜態和在途資料。 請參閱文檔以瞭解有關 [資料加密](../../../help/landing/governance-privacy-security/encryption.md)


## 後續步驟 {#next-steps}

準備好資料並準備好所有憑據和架構後，請按照 [Attribution AI使用手冊](./user-guide.md)。 本指南指導您建立Attribution AI實例。
