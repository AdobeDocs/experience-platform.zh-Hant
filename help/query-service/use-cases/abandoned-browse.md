---
keywords: Experience Platform；查詢服務；查詢服務；查詢
title: Adobe Experience Platform查詢服務的範例使用案例
description: 以端對端範例示範Adobe Experience Platform查詢服務的多功能性和優點。
exl-id: 00bdae47-71b7-44ea-9365-a1d64c88d2bf
source-git-commit: 38689125a43ad0b1a12a00efe6800bb310d7557c
workflow-type: tm+mt
source-wordcount: '695'
ht-degree: 1%

---

# Adobe Experience Platform的範例使用案例 [!DNL Query Service]

本檔案及隨附的影片簡報會提供高階的端對端工作流程，展示Adobe Experience Platform如何運作 [!DNL Query Service] 有益於貴組織的策略性業務見解。 本指南以瀏覽放棄使用案例為例，說明下列重要概念：

* 資料處理對於Adobe Experience Platform潛力最大化的關鍵重要性。
* 根據您現有的資料架構建置查詢的方式。
* 確保資料品質符合您的需求，並設法彌補不足。
* 排程查詢以設定頻率執行，以用於下游的區段和個人化的目的地的程式。
* 行銷人員可輕鬆透過 [!DNL Query Service].

## 目標 {#objectives}

此工作流程示範仰賴多項Adobe Experience Platform服務。 如果您希望跟進，建議您充分瞭解下列功能和服務：

* 此 [Experience Data Model (XDM)結構描述組合的基本概念](../../xdm/schema/composition.md)
* 操作說明 [建立資料集並擷取資料](https://experienceleague.adobe.com/docs/platform-learn/tutorials/data-ingestion/create-datasets-and-ingest-data.html)
* 操作說明 [使用Adobe Analytics來源聯結器擷取資料](https://experienceleague.adobe.com/docs/platform-learn/tutorials/sources/ingest-data-from-adobe-analytics.html?lang=zh-Hant)
* [區段](../../segmentation/home.md)
* [目的地](../../destinations/home.md)

瀏覽放棄範例的中心為使用Adobe [!DNL Analytics] 建立可採取行動的特定受眾的資料。 對象經過改良，可包含過去四天瀏覽網站但未購買的每位客戶。 然後，對象中的每個設定檔都會以客戶行為模式所產生的最高價格SKU為目標。

查詢本身規範性很強，並且只包含符合區段定義的使用案例條件的資料。 如此一來，只要將 [!DNL Analytics] 正在處理的資料。 此外也會依價格從最高到最低排序資料，並選擇使用者瀏覽時價格最高的SKU。

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

## [!DNL Query Service] 使用adobe analytics瀏覽放棄範例 {#video-example}

下方所列的影片簡報，針對您的Experience Platform資料提供整體、真實的使用案例，並聚焦於 [!DNL Query Service] 和Adobe分析整合。

>[!VIDEO](https://video.tv.adobe.com/v/342533?quality=12&learn=on)

## 的優點 [!DNL Query Service] {#benefits}

所提供的功能 [!DNL Query Service] 有許多用途。 您可以使用它來適應分段的複雜邏輯、計算各種個人化屬性以用於下游，或大幅簡化建立受眾的方式。

[!DNL Query Service] 可讓您在查詢中加入限制，以簡化對象建立流程。 這可確保適合您對象的正確資料資格，進而改善資料品質。 維持查詢品質可讓對象正確無誤，並有助於提高資料可靠性。 您也可以根據從查詢衍生的屬性來建立結構描述和自訂表格，以儲存對象。 可以為設定檔啟用自訂表格，並且您可以使用這些資料點來進行細分和個人化。 此功能可協助想要建立明確受眾人群的行銷人員。

此外，將滿足任何循環或靜態條件的邏輯包含到查詢中， [!DNL Query Service] 提取複雜分段的重擔。

Adobe Experience Platform提供資料存放庫和必要工具，讓您以有效率且可靠的方式啟用資料。 透過將資料保留在Platform內，可讓您在執行其他程式時衍生屬性，並免除將資料匯出至協力廠商工具以進行操作和處理的需求。 處理數百個屬性或行銷活動時，這類處理間接成本可能會大幅影響專案時間表。 這可讓行銷人員透過單一位置存取其資料並建置行銷活動，以及非常動態的訊息分段和個人化方式。

## 後續步驟

閱讀本檔案後，您現在應該瞭解如何 [!DNL Query Service] 不只會影響資料品質和區段的便利性，也會影響資料架構在整個端對端工作流程中的重要性。 如需更多適用的SQL範例，瞭解如何搭配使用Adobe Analytics [!DNL Query Service]，請參閱 [Adobe Analytics銷售變數使用案例](./merchandising-variables.md).

其他說明下列專案優點的檔案： [!DNL Query Service] 對於貴組織的策略性業務見解，包括 [機器人篩選使用案例](./bot-filtering.md) 範例。

或者，這些檔案有助於您瞭解 [!DNL Query Service] 功能：

* [查詢執行指南](../best-practices/writing-queries.md)
* [資料資產組織指南](../best-practices/organize-data-assets.md).


