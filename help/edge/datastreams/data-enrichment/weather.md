---
title: 使用DNL The Weather Channel的天氣資料
description: 使用DNL The Weather Channel中的天氣資料來增強通過資料流收集的資料。
exl-id: 548dfca7-2548-46ac-9c7e-8190d64dd0a4
source-git-commit: 05a7b73da610a30119b4719ae6b6d85f93cdc2ae
workflow-type: tm+mt
source-wordcount: '672'
ht-degree: 3%

---

# 使用來自 [!DNL The Weather Channel]

Adobe與 [!DNL [The Weather Company]](https://www.ibm.com/weather) 把美國天氣的附加背景帶到通過資料流收集的資料中。 您可以使用此資料進行分析、定位和在Experience Platform中建立段。

有3種類型的資料可從 [!DNL The Weather Channel]:

* **[!UICONTROL 當前天氣]**:根據用戶的位置確定用戶的當前天氣狀況。 這包括當前溫度、枕木、雲覆蓋等。
* **[!UICONTROL 預測天氣]**:預測包括用戶地點的1、2、3、5、7和10天預測。
* **[!UICONTROL 觸發器]**:觸發器是映射到不同語義天氣條件的特定組合。 有三種不同類型的天氣觸發器：

   * **[!UICONTROL 天氣觸發器]**:在語義上有意義的條件，例如寒冷或雨天。 不同氣候的定義可能不同。
   * **[!UICONTROL 產品觸發器]**:導致購買不同類型產品的條件。 例如：寒冷的天氣預報可能意味著購買雨衣的可能性更大。
   * **[!UICONTROL 惡劣天氣觸發]**:嚴重的天氣警告，比如冬季風暴或颶風警告。

## 先決條件 {#prerequisites}

在使用天氣資料之前，請確保滿足以下先決條件：

* 您必須授權您使用的天氣資料， [!DNL The Weather Channel]。 然後，他們將在您的帳戶中啟用它。
* 氣象資料只能通過資料流提供。 要使用天氣資料，必須使用 [!DNL Web SDK]。 [!DNL Mobile Edge Extension] 或 [伺服器API](../../../server-api/overview.md) 來利用這些資料。
* 您的資料流必須 [[!UICONTROL 地理位置]](../configure.md#advanced-options) 啟用。
* 添加 [氣象組](#schema-configuration) 到您使用的架構。

## 佈建 {#provisioning}

一旦您從 [!DNL The Weather Channel]，它們將允許您的帳戶訪問資料。 接下來，您必須聯繫Adobe客戶服務部門以在您的資料流上啟用資料。 啟用後，資料將自動追加。

您可以通過使用調試器運行邊緣跟蹤或使用「保證」跟蹤通過 [!DNL Edge Network]。

### 架構配置 {#schema-configuration}

必須將天氣欄位組添加到與您在資料流中使用的事件資料集對應的Experience Platform架構中。 有五個欄位組可用：

* [!UICONTROL 預測天氣]
* [!UICONTROL 當前天氣]
* [!UICONTROL 產品觸發器]
* [!UICONTROL 相對觸發器]
* [!UICONTROL 惡劣天氣觸發]

## 訪問天氣資料 {#access-weather-data}

一旦您的資料獲得許可並可用，您就可以在Adobe服務中以多種方式訪問它。

### Adobe Analytics {#analytics}

在 [!DNL Adobe Analytics]，天氣資料可通過處理規則以及其餘的 [!DNL XDM] 架構。

您可以在 [天氣參考](weather-reference.md) 的子菜單。 與所有 [!DNL XDM] 模式，鍵的前置詞為 `a.x`。 例如，名為 `weather.current.temperature.farenheit` 會出現 [!DNL Analytics] 如 `a.x.weather.current.temperature.farenheit`。

![處理規則介面](../../assets/datastreams/data-enrichment/weather/processing-rules.png)

### Adobe Customer Journey Analytics {#cja}

在 [!DNL Adobe Customer Journey Analytics]，在資料流中指定的資料集中提供了天氣資料。 只要天氣屬性 [添加到您的架構](#prerequisites-prerequisites)，它們將 [添加到資料視圖](https://experienceleague.adobe.com/docs/analytics-platform/using/cja-dataviews/create-dataview.html) 在 [!DNL Customer Journey Analytics]。

### Real-Time Customer Data Platform {#rtcdp}

天氣資料可在 [Real-time Customer Data Platform](../../../rtcdp/overview.md)，用於段。 天氣資料附於事件。

![顯示天氣事件的段生成器](../../assets/datastreams/data-enrichment/weather/schema-builder.png)

由於天氣條件經常變化，Adobe建議您設定段的時間約束，如上例所示。 與6個月前的寒日相比，在最後一兩天裡過一個寒冷的日子要影響得多。

查看 [天氣參考](weather-reference.md) 的子菜單。

### Adobe Target {#target}

在 [!DNL Adobe Target]，您可以使用天氣資料即時推動個性化。 天氣資料傳遞到 [!DNL Target] 如 [!UICONTROL 框] 參數，您可以通過自定義 [!UICONTROL 框] 的下界。

![目標受眾構建器](../../assets/datastreams/data-enrichment/weather/target-audience-builder.png)

參數是 [!DNL XDM] 指向特定欄位的路徑。 查看 [天氣參考](weather-reference.md) 的子菜單。

## 後續步驟 {#next-steps}

閱讀完本文檔後，您現在對如何跨各種Adobe解決方案使用天氣資料有了更好的瞭解。 要瞭解有關天氣資料欄位映射的更多資訊，請參見 [欄位映射引用](weather-reference.md)。
