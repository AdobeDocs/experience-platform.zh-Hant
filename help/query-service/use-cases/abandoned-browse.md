---
keywords: Experience Platform；查詢服務；查詢服務；查詢
title: Adobe Experience Platform查詢服務的示例用例
description: 一個端到端示例，演示Adobe Experience Platform查詢服務的多用性和優點。
exl-id: 00bdae47-71b7-44ea-9365-a1d64c88d2bf
source-git-commit: 668b2624b7a23b570a3869f87245009379e8257c
workflow-type: tm+mt
source-wordcount: '712'
ht-degree: 2%

---

# Adobe Experience Platform示例用例 [!DNL Query Service]

本文檔及隨附的視頻演示提供了高端端到端工作流程，演示了Adobe Experience Platform [!DNL Query Service] 有利於您組織的戰略性業務洞察力。 本指南以瀏覽放棄使用案例為例說明以下主要概念：

* 資料處理對最大限度地發揮Adobe Experience Platform的潛力至關重要。
* 基於現有資料體系結構構建查詢的方法。
* 確保滿足您需要的資料質量，以及緩解任何不足的方法。
* 調度查詢以在設定頻率下運行以便在分段和用於個性化的目的地中下游使用的過程。
* 通過以下功能，營銷人員可以輕鬆地將派生屬性包括在其細分市場中 [!DNL Query Service]。

## 目標 {#objectives}

此工作流演示依賴於多個Adobe Experience Platform服務。 如果您想繼續，建議您充分瞭解以下功能和服務：

* 的 [經驗資料模型(XDM)架構組合基礎](../../xdm/schema/composition.md)
* 如何 [建立資料集和攝取資料](https://experienceleague.adobe.com/docs/platform-learn/tutorials/data-ingestion/create-datasets-and-ingest-data.html)
* 如何 [使用Adobe Analytics源連接器接收資料](https://experienceleague.adobe.com/docs/platform-learn/tutorials/sources/ingest-data-from-adobe-analytics.html?lang=zh-Hant)
* [區段](../../segmentation/home.md)
* [目的地](../../destinations/home.md)

瀏覽放棄示例以使用Adobe [!DNL Analytics] 建立特定可操作受眾的資料。 觀眾經過細化，包括了過去四天瀏覽網站但沒有購買的所有客戶。 然後，受眾中的每個配置檔案都以客戶行為模式所產生的最高價格SKU為目標。

查詢本身是非常規範的，只包括滿足段定義的使用案例標準的資料。 這通過最小化 [!DNL Analytics] 正在處理的資料。 它還按價格從最高到最低訂購資料，並選擇用戶瀏覽的最高價格SKU。

在演示中使用的查詢可以在下面看到：

```sql
INSERT INTO summit_adv_data_prep_dataset
SELECT STRUCT(
    customerId AS crmCustomerId, struct(sku AS sku, price AS sku_price, abandonTS AS abandonTS) AS abandonBrowse) AS _pfreportingonprod
FROM
(SELECT
B.personKey.sourceId,
A.productListItems[0].SKU AS sku,
max(A.timestamp) AS abandonTS,
max(c._pfreportingonprod.price) AS price
FROM summit_adobe_analytics_dataset A,profile_attribute_14adf268_2a20_4dee_bee6_a6b0e34616a9 B,summit_product_dataset c
WHERE A._experience.analytics.customDimension.evars.evar1 = B.personKey.sourceID
AND productListItems[0].SKU = C._pfreportingonprod.sku
AND A.web.webpagedetails.URL NOT LIKE '%orderconfirmation%'
AND timestamp > current_date - interval '4 day'
GROUP BY customerId,sku
order by price desc)D;
```

## [!DNL Query Service] 使用adobe analytics瀏覽放棄示例 {#video-example}

下面看到的視頻演示為您重點關注的Experience Platform資料提供了一個全面、真實的使用案例 [!DNL Query Service] 和Adobe分析整合。

>[!VIDEO](https://video.tv.adobe.com/v/342533?quality=12&learn=on)

## 優勢 [!DNL Query Service] {#benefits}

提供的功能 [!DNL Query Service] 有很多用處。 您可以使用它來適應複雜的邏輯進行分割、計算各種個性化屬性以便下游使用，或者極大地簡化構建段的方式。

[!DNL Query Service] 使您能夠在查詢中包含約束以簡化段構建過程。 這通過確保適當的資料符合您的資料段的要求並建立更準確的受眾來提高資料質量。 維護查詢質量將使讀者獲得準確的資訊，並有助於提高資料可靠性。 您還可以根據從查詢派生的屬性建立架構和自定義表來保存受眾。 可以為配置檔案啟用自定義表，並且可以使用這些資料點進行分段和個性化。 此功能可幫助那些希望建立清晰受眾的營銷人員。

此外，通過在查詢中包含滿足任何循環或靜態條件的邏輯， [!DNL Query Service] 提取精細分割的負擔。

Adobe Experience Platform提供了一個資料儲存庫和必要的工具，以高效、可靠的方式激活資料。 通過將資料保留在平台內，它允許您在運行其他進程時導出屬性，並消除了將資料導出到第三方工具以進行操作和處理的需要。 在處理數百個屬性或市場活動時，此類處理間接費用會對項目時間表產生很大影響。 這為營銷人員提供了訪問其資料和構建市場活動的單一位置，以及一種非常動態的消息分段和個性化方法。

## 後續步驟

通過閱讀此文檔，您現在應瞭解 [!DNL Query Service] 不僅會影響資料的質量和易於分割，而且會影響資料體系結構對整個端到端工作流的重要性。 有關使用Adobe Analytics與 [!DNL Query Service]，請參見 [Adobe Analytics商品化變數使用案例](./merchandising-variables.md)。

其他顯示 [!DNL Query Service] 對您組織的戰略性業務洞見是 [bot過濾用例](./bot-filtering.md) 示例。

或者，這些文檔有助於您瞭解 [!DNL Query Service] 功能：

* [查詢執行指南](../best-practices/writing-queries.md)
* [資料資產組織指南](../best-practices/organize-data-assets.md)。


