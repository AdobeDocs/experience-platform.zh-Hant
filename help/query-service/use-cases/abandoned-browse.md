---
keywords: Experience Platform；查詢服務；查詢服務；查詢
title: Adobe Experience Platform查詢服務的範例使用案例
description: 以端對端範例示範Adobe Experience Platform查詢服務的多功能性和優點。
exl-id: 00bdae47-71b7-44ea-9365-a1d64c88d2bf
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '696'
ht-degree: 0%

---

# Adobe Experience Platform [!DNL Query Service]的使用案例範例

本檔案及隨附的影片簡報提供高階的端對端工作流程，展示Adobe Experience Platform [!DNL Query Service]如何讓貴組織的策略業務見解受益。 本指南以瀏覽放棄使用案例為例，說明下列重要概念：

* 資料處理對於Adobe Experience Platform潛力最大化的關鍵重要性。
* 根據您現有的資料架構建置查詢的方式。
* 確保資料品質符合您的需求，並設法彌補不足。
* 排程查詢以設定頻率執行，以用於下游的區段和個人化的目的地的程式。
* 行銷人員可輕鬆透過[!DNL Query Service]的強大功能，將衍生資料集納入其對象。

## 目標 {#objectives}

此工作流程示範仰賴多項Adobe Experience Platform服務。 如果您希望跟進，建議您充分瞭解下列功能和服務：

* Experience Data Model (XDM)結構描述組合的[基本概念](../../xdm/schema/composition.md)
* 如何[建立資料集並擷取資料](https://experienceleague.adobe.com/docs/platform-learn/tutorials/data-ingestion/create-datasets-and-ingest-data.html)
* 如何使用Adobe Analytics來源聯結器[內嵌資料](https://experienceleague.adobe.com/docs/platform-learn/tutorials/sources/ingest-data-from-adobe-analytics.html?lang=zh-Hant)
* [區段](../../segmentation/home.md)
* [目標](../../destinations/home.md)

瀏覽放棄範例的中心為使用Adobe [!DNL Analytics]資料來建立特定可操作的對象。 對象經過改良，可包含過去四天瀏覽網站但未購買的每位客戶。 然後，對象中的每個設定檔都會以客戶行為模式所產生的最高價格SKU為目標。

查詢本身規範性很強，並且只包含符合區段定義的使用案例條件的資料。 這會減少正在處理的[!DNL Analytics]資料量，進而改善效能。 此外也會依價格從最高到最低排序資料，並選擇使用者瀏覽時價格最高的SKU。

簡報中使用的查詢如下所示：

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

## 使用adobe analytics的[!DNL Query Service]瀏覽放棄範例 {#video-example}

下方所呈現的影片提供您的Experience Platform資料，並著重於[!DNL Query Service]和Adobe分析整合的整體真實使用案例。

>[!VIDEO](https://video.tv.adobe.com/v/342533?quality=12&learn=on)

## [!DNL Query Service]的優點 {#benefits}

[!DNL Query Service]提供的功能有許多用途。 您可以使用它來適應分段的複雜邏輯、計算各種個人化屬性以用於下游，或大幅簡化建立受眾的方式。

[!DNL Query Service]可讓您在查詢中包含限制，以簡化您的對象建立流程。 這可確保適合您對象的正確資料資格，進而改善資料品質。 維持查詢品質可讓對象正確無誤，並有助於提高資料可靠性。 您也可以根據從查詢衍生的屬性來建立結構描述和自訂表格，以儲存對象。 可以為設定檔啟用自訂表格，並且您可以使用這些資料點來進行細分和個人化。 此功能可協助想要建立明確受眾人群的行銷人員。

此外，將滿足任何循環或靜態條件的邏輯納入查詢中，[!DNL Query Service]會提取複雜分段的負擔。

Adobe Experience Platform提供資料存放庫和必要工具，讓您以有效率且可靠的方式啟用資料。 透過將資料保留在Experience Platform中，它可讓您在執行其他程式時衍生屬性，並免除將資料匯出至第三方工具以進行操作和處理的需求。 處理數百個屬性或行銷活動時，這類處理間接成本可能會大幅影響專案時間表。 這可讓行銷人員透過單一位置存取其資料並建置行銷活動，以及非常動態的訊息分段和個人化方式。

## 後續步驟

閱讀本檔案後，您現在應該瞭解[!DNL Query Service]不僅影響資料品質和區段的容易程度，還影響其在資料架構中對於整個端對端工作流程的重要性。 如需使用Adobe Analytics搭配[!DNL Query Service]的更適用SQL範例，請參閱[Adobe Analytics銷售變數使用案例](./merchandising-variables.md)。

顯示[!DNL Query Service]對貴組織策略性業務深入分析之優點的其他檔案為[機器人篩選使用案例](./bot-filtering.md)範例。

或者，這些檔案有助於您瞭解[!DNL Query Service]功能：

* [查詢執行指南](../best-practices/writing-queries.md)
* [資料資產組織的指南](../best-practices/organize-data-assets.md)。


