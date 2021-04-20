---
keywords: Experience Platform；入門；歸因ai；熱門主題；歸因ai輸入；歸因ai輸出；
solution: Experience Platform, Intelligent Services
title: 輸入與輸出在Attribution AI
topic: Input and Output data for Attribution AI
description: 以下檔案概述了Attribution AI中使用的不同輸入和輸出。
exl-id: d6dbc9ee-0c1a-4a5f-b922-88c7a36a5380
translation-type: tm+mt
source-git-commit: 35b3994287d4f556fab8ee75c3bf242ff2690aef
workflow-type: tm+mt
source-wordcount: '2182'
ht-degree: 3%

---

# [!DNL Attribution AI]中的輸入和輸出

以下文檔概述了[!DNL Attribution AI]中使用的不同輸入和輸出。

## [!DNL Attribution AI] 輸入資料

Attribution AI的運作方式是分析下列其中一個資料集，以計算演算法分數：

- 消費者體驗事件(CEE)資料集
- Adobe Analytics使用[Analytics來源連接器](../../sources/tutorials/ui/create/adobe-applications/analytics.md)的資料集

>[!IMPORTANT]
>
>Adobe Analytics源連接器最多需要四周時間才能回填資料。 如果您最近設定了連接器，您應驗證資料集是否具有Attribution AI所需的最小資料長度。 請檢閱[歷史資料](#data-requirements)區段，以確認您有足夠的資料可計算精確的演算法分數。

有關設定[!DNL Consumer Experience Event](CEE)架構的詳細資訊，請參閱[智慧服務資料準備](../data-preparation.md)指南。 有關映射Adobe Analytics資料的詳細資訊，請訪問[Analytics欄位映射](../../sources/connectors/adobe-applications/analytics.md)文檔。

並非[!DNL Consumer Experience Event](CEE)架構中的所有列都是必需的。

>[!NOTE]
>
> 以下9欄是必填欄，其他欄是選用欄，但如果您想要將相同資料用於其他Adobe解決方案，例如[!DNL Customer AI]和[!DNL Journey AI]，則建議／必要欄。

| 必填欄 | 需要 |
| --- | --- |
| 主要身分欄位 | 觸點／轉換 |
| 時間戳記 | 觸點／轉換 |
| Channel._type | 觸點 |
| Channel.mediaAction | 觸點 |
| Channel.mediaType | 觸點 |
| Marketing.trackingCode | 觸點 |
| Marketing.campaignname | 觸點 |
| Marketing.campaigngroup | 觸點 |
| 商務 | 轉換 |

通常，歸因會在「商務」下的轉換欄（例如訂單、購買和結帳）上執行。 強烈建議使用「channel」和「marketing」欄來定義觸點，以獲得良好的見解。 不過，您可以隨附上述欄加入任何其他欄，以設定為轉換或接觸點定義。

以下列不是必需的，但如果您有可用資訊，建議您將這些列包括在CEE方案中。

**其他建議欄：**
- web.webReferer
- web.webInteraction
- web.webPageDetails
- xdm:productListItems

### 歷史資料 {#data-requirements}

>[!IMPORTANT]
>
> Attribution AI運作所需的最小資料量如下：
> - 您需要提供至少3個月（90天）的資料，才能建立良好的模型。
> - 您至少需要1000個轉換。


Attribution AI需要歷史資料作為模型訓練的輸入。 所需的資料持續時間主要由兩個關鍵因素決定：訓練窗口和回顧窗口。 縮短培訓視窗的輸入會更敏感於最新趨勢，而較長的培訓視窗有助於產生更穩定、更精確的模型。 以最能代表您業務目標的歷史資料來建立目標模型非常重要。

[訓練視窗設定](./user-guide.md#training-window)會根據發生時間篩選要包含於模型訓練的轉換事件。 目前，最低培訓時間為1個季度（90天）。 [回顧視窗](./user-guide.md#lookback-window)提供一個時間範圍，指出應包含多少天前的轉換事件接觸點與此轉換事件相關。 這兩個概念一起決定應用程式所需的輸入資料量（以天計）。

依預設，Attribution AI會將培訓視窗定義為最近2個季度（6個月），並將回顧視窗定義為56天。 換言之，模型將考慮過去2個季度中發生的所有已定義轉換事件，並尋找在相關轉換事件前56天內發生的所有觸點。

**公式**:

所需資料的最小長度=訓練視窗+回顧視窗

>[!TIP]
>
> 具有預設組態的應用程式所需的資料最小長度為：2個季度（180天）+ 56天= 236天。

範例：

- 您想要歸因過去90天（3個月）內發生的轉換事件，並追蹤轉換事件前4週內發生的所有觸點。 輸入資料的持續時間應跨越過去90天+ 28天（4週）。 培訓時間為90天，回顧時間為28天，總計為118天。

## Attribution AI輸出資料

Attribution AI輸出：

- [原始粒度分數](#raw-granular-scores)
- [匯總分數](#aggregated-attribution-scores)

**輸出模式示例：**

![](./images/input-output/schema_output.gif)

### 原始粒度分數{#raw-granular-scores}

Attribution AI會以最細微的層級輸出歸因分數，讓您可以依任何分數欄來切割分數。 若要在UI中檢視這些分數，請閱讀[檢視原始分數路徑](#raw-score-path)的章節。 若要使用API下載分數，請造訪[下載Attribution AI](./download-scores.md)檔案中的分數。

>[!NOTE]
>
> 只有在下列任一情況下，您才能從分數輸出資料集的輸入資料集中看到任何所需的報表欄：
> - 報表欄會包含在設定頁面中，做為觸點或轉換定義設定的一部分。
> - 報告欄會包含在其他分數資料集欄中。


下表概述原始分數範例輸出中的架構欄位：

| 欄名稱(DataType) | 可為空 | 說明 |
| --- | --- | --- |
| 時間戳記(DateTime) | False | 發生轉換事件或觀察的時間。<br> **範例：** 2020-06-09T00:01:51.000Z |
| identityMap(Map) | True | 與CEE XDM格式類似的用戶的identityMap。 |
| eventType（字串） | True | 此時間系列記錄的主要事件類型。<br> **範例：** 「訂購」、「購買」、「瀏覽」 |
| eventMergeId（字串） | True | 一個ID，可關聯或合併多個實質上是相同事件或應該合併的[!DNL Experience Events]。 這將由資料產生器在擷取之前填入。<br> **範例：** 575525617716-0-edc2ed37-1aab-4750-a820-1c2b3844b8c4 |
| _id（字串） | False | 時間序列事件的唯一識別碼。<br> **範例：** 4461-edc2ed37-1ab-4750-a820-1c2b3844b8c4 |
| _tenantId（物件） | False | 與您的保留ID對應的頂層物件容器。<br> **範例：** _atsdsnrmmsv2 |
| your_schema_name（對象） | False | 使用轉換事件對所有與其關聯的觸點事件及其元資料進行分數。<br> **範例：** Attribution AI分數——模型名稱__2020 |
| 區段（字串） | True | 轉換區段，例如模型所依據的地域劃分。 若沒有區段，則區段與conversionName相同。<br> **範例：** ORDER_US |
| conversionName（字串） | True | 設定期間設定的轉換名稱。<br> **範例：** 訂單、銷售線索、瀏覽 |
| 轉換（物件） | False | 轉換中繼資料欄。 |
| dataSource（字串） | True | 資料來源的全域唯一識別。<br> **示例：** Adobe Analytics |
| eventSource（字串） | True | 實際事件發生時的來源。<br> **範例：** Adobe.com |
| eventType（字串） | True | 此時間系列記錄的主要事件類型。<br> **範例：** Order |
| geo（字串） | True | 傳送轉換的地理位置`placeContext.geo.countryCode`。<br> **範例：** US |
| priceTotal(Double) | True | 透過轉換<br>取得的收入 **範例：** 99.9 |
| product（字串） | True | 產品本身的XDM識別碼。<br> **示例：** RX 1080 ti |
| productType（字串） | True | 產品的顯示名稱，如此顯示給此產品檢視的使用者。<br> **範例：** Gpus |
| 數量（整數） | True | 轉換期間購買的數量。<br> **示例：** 1 1080 ti |
| receivedTimestamp(DateTime) | True | 收到轉換的時間戳記。<br> **範例：** 2020-06-09T00:01:51.000Z |
| skuId（字串） | True | 庫存保留單位(SKU)，由廠商定義之產品的唯一識別碼。<br> **示例：** MJ-03-XS-Black |
| 時間戳記(DateTime) | True | 轉換的時間戳記。<br> **範例：** 2020-06-09T00:01:51.000Z |
| passThrough（物件） | True | 設定模型時，使用者指定的其他分數資料集欄。 |
| commerce_order_purchaseCity（字串） | True | 其他分數資料集欄。<br> **範例：** city:聖荷西 |
| customerProfile（對象） | False | 用於建立模型之使用者的身分詳細資料。 |
| identity（物件） | False | 包含用於構建模型的用戶的詳細資訊，如`id`和`namespace`。 |
| id（字串） | True | 使用者的身分識別碼，例如Cookie ID、AAID或MCID等。<br> **範例：** 1734876272540865634688320891369597404 |
| namespace（字串） | True | 用於建立路徑的身分名稱空間，進而建立模型。<br> **範例：** aaid |
| 接觸點詳細資料（物件陣列） | True | 觸點詳細資料清單，可導致依觸點發生次數或時間戳記排序的轉換。 |
| touchpointName（字串） | True | 設定期間設定的觸點名稱。<br> **範例：** PAID_SEARCH_CLICK |
| 分數（物件） | True | 此轉換的觸點貢獻為分數。 如需此物件中產生之分數的詳細資訊，請參閱[匯總歸因分數](#aggregated-attribution-scores)一節。 |
| touchPoint（物件） | True | 觸點中繼資料。 有關在此對象中生成的分數的詳細資訊，請參閱[聚合分數](#aggregated-scores)部分。 |

### 檢視原始分數路徑(UI){#raw-score-path}

您可以在UI中檢視原始分數的路徑。 首先，在「平台UI」中選擇&#x200B;**[!UICONTROL Schemas]**，然後從&#x200B;**[!UICONTROL Browse]**&#x200B;標籤中搜尋並選取您的歸因AI分數架構。

![選擇您的架構](./images/input-output/schemas_browse.png)

接著，在UI的&#x200B;**[!UICONTROL Structure]**&#x200B;視窗中選取欄位，**[!UICONTROL Field properties]**&#x200B;標籤隨即開啟。 在&#x200B;**[!UICONTROL Field properties]**&#x200B;中是對應至原始分數的路徑欄位。

![挑選結構](./images/input-output/field_properties.png)


### 匯總歸因分數{#aggregated-attribution-scores}

如果日期範圍少於30天，可從平台UI以CSV格式下載匯總的分數。

Attribution AI支援兩類歸因分數：演算法和規則型分數。

Attribution AI產生兩種不同的演算法分數，遞增和影響。 受影響的分數是每個行銷觸點所負責的轉換率的一部分。 遞增分數是行銷觸點直接造成的邊際影響量。 遞增分數與受影響分數的主要差異在於遞增分數會考慮基準效果。 不會假設轉換純粹是由先前的行銷觸點所造成。

以下是Adobe Experience PlatformUI的Attribution AI架構輸出範例：

![](./images/input-output/schema_screenshot.png)

請參閱下表，以取得這些歸因分數的詳細資訊：

| 歸因分數 | 說明 |
| ----- | ----------- |
| 影響（演算法） | 受影響的分數是每個行銷觸點所負責的轉換片段。 |
| 增量（演算法） | 遞增分數是行銷觸點直接造成的邊際影響量。 |
| 首次接觸 | 規則型歸因分數，可將所有評分指派給轉換路徑上的初始觸點。 |
| 上次接觸 | 以規則為基礎的歸因分數，可將所有評分指派給最接近轉換的觸點。 |
| 線性 | 規則型歸因分數，可為轉換路徑上的每個觸點指派相等的評分。 |
| U 形 | 以規則為基礎的歸因分數，將40%的評分指派給第一個觸點，40%的評分指派給最後一個觸點，而其他觸點將其餘20%平分。 |
| 時間耗損 | 規則型歸因分數，即離轉換較近的觸點獲得的評分高於離轉換較遠的觸點。 |

**原始分數參考（歸因分數）**

下表將歸因分數對應至原始分數。 如果您想要下載原始分數，請造訪[下載Attribution AI](./download-scores.md)檔案中的分數。

| 歸因分數 | 原始分數參考欄 |
| --- | --- |
| 影響（演算法） | _tenantID.your_schema_name.element.touchpoint.algorithmicEffected |
| 增量（演算法） | _tenantID.your_schema_name.touchpointsDetail.element.touchpoint.algorithmicEffected |
| 首次接觸 | _tenantID.your_schema_name.touchpointsDetail.element.touchpoint.firstTouch |
| 上次接觸 | _tenantID.your_schema_name.touchpointsDetail.element.touchpoint.lastTouch |
| 線性 | _tenantID.your_schema_name.touchpointsDetail.element.touchpoint.linear |
| U 形 | _tenantID.your_schema_name.touchpointsDetail.element.touchpoint.uShape |
| 時間耗損 | _tenantID.your_schema_name.touchpointsDetail.element.touchpoint.decayUnits |

### 匯總分數{#aggregated-scores}

如果日期範圍少於30天，可從平台UI以CSV格式下載匯總的分數。 有關這些聚合列的詳細資訊，請參見下表。

| 欄名稱 | 約束 | 可為空 | 說明 |
| --- | --- | --- | --- |
| customerevents_date(DateTime) | 用戶定義和固定格式 | False | YYYY-MM-DD格式的客戶事件日期。<br> **範例**:2016-05-02 |
| mediatouchpoints_date(DateTime) | 用戶定義和固定格式 | True | YYYY-MM-DD格式<br>的媒體接觸點日期 **範例**:2017-04-21 |
| segment（字串） | 計算 | False | 轉換區段，例如模型所依據的地域劃分。 若沒有區段，則區段會與conversion_scope相同。<br> **範例**:ORDER_AMER |
| conversion_scope（字串） | 用戶定義 | False | 使用者設定的轉換名稱。<br> **範例**:訂單 |
| touchpoint_scope（字串） | 用戶定義 | True | 使用者<br>所設定的Touchpoint名稱 **範例**:PAID_SEARCH_CLICK |
| product（字串） | 用戶定義 | True | 產品的XDM識別碼。<br> **範例**:CC |
| product_type（字串） | 用戶定義 | True | 產品的顯示名稱，如此顯示給此產品檢視的使用者。<br> **範例**:gpus，筆記型電腦 |
| geo（字串） | 用戶定義 | True | 傳送轉換的地理位置(placeContext.geo.countryCode)<br> **範例**:美國 |
| event_type（字串） | 用戶定義 | True | 此時間系列記錄的主要事件類型<br> **範例**:付費轉換 |
| media_type（字串） | ENUM | False | 說明媒體類型是付費、擁有還是免費。<br> **範例**:付費、擁有 |
| channel（字串） | ENUM | False | `channel._type`屬性，用於提供具有[!DNL Consumer Experience Event] XDM中相似屬性的渠道的粗略分類。<br> **範例**:搜尋 |
| action(String) | ENUM | False | `mediaAction`屬性用於提供體驗事件媒體動作類型。<br> **範例**:按一下 |
| campaign_group（字串） | 用戶定義 | True | 將多個促銷活動分組在一起的促銷活動群組名稱，例如&#39;50%_DISCOUNT&#39;。<br> **範例**:商業 |
| campaign_name（字串） | 用戶定義 | True | 用於識別行銷促銷活動的促銷活動名稱，例如&#39;50%_DISCOUNT_USA&#39;或&#39;50%_DISCOUNT_ASIA&#39;。<br> **範例**:感恩節大甩賣 |

**原始分數參考（匯總）**

下表將匯總的分數對應至原始分數。 如果您想要下載原始分數，請造訪[下載Attribution AI](./download-scores.md)檔案中的分數。 若要從UI中檢視原始分數路徑，請造訪本檔案中檢視原始分數路徑[的章節。](#raw-score-path)

| 欄名稱 | 原始分數參考欄 |
| --- | --- |
| customerevents_date | timestamp |
| mediatouchpoints_date | _tenantID.your_schema_name.touchpointsDetail.element.touchpoint.timestamp |
| 區段 | _tenantID.your_schema_name.segmentation |
| conversion_scope | _tenantID.your_schema_name.conversion.conversionName |
| 接觸點——範圍 | _tenantID.your_schema_name.touchpointsDetail.element.touchpointName |
| product | _tenantID.your_schema_name.conversion.product |
| product_type | _tenantID.your_schema_name.conversion.product_type |
| 地理 | _tenantID.your_schema_name.conversion.geo |
| event_type | eventType |
| media_type | _tenantID.your_schema_name.touchpointsDetail.element.touchpoint.mediaType |
| channel | _tenantID.your_schema_name.touchpointsDetail.element.touchpoint.mediaChannel |
| 動作 | _tenantID.your_schema_name.touchpointsDetail.element.touchpoint.mediaAction |
| campaign_group | _tenantID.your_schema_name.touchpointsDetail.element.touchpoint.campaignGroup |
| campaign_name | _tenantID.your_schema_name.touchpointsDetail.element.touchpoint.campaignName |


## 下一步 {#next-steps}

準備好資料並準備好所有憑據和方案後，請從[Attribution AI使用手冊](./user-guide.md)開始。 本指南會逐步帶您建立Attribution AI的例項。
