---
keywords: Experience Platform；查詢服務；查詢服務；查詢
title: Adobe Experience Platform查詢服務的範例使用案例
description: 此端對端範例可示範Adobe Experience Platform Query Service的多功能性和優點。
exl-id: 00bdae47-71b7-44ea-9365-a1d64c88d2bf
source-git-commit: 668b2624b7a23b570a3869f87245009379e8257c
workflow-type: tm+mt
source-wordcount: '712'
ht-degree: 2%

---

# Adobe Experience Platform的範例使用案例 [!DNL Query Service]

本檔案及隨附的影片簡報提供高階的端對端工作流程，說明Adobe Experience Platform [!DNL Query Service] 可讓您組織的策略性業務分析受益。 本指南以瀏覽放棄使用案例為例，說明下列重要概念：

* 資料處理對發揮Adobe Experience Platform潛力的重要性。
* 根據您現有的資料架構建立查詢的方式。
* 確保符合您需求的資料品質，以及緩解任何短缺的方法。
* 排程查詢以在設定頻率執行，以用於細分和個人化目的地的下遊程式。
* 行銷人員可透過 [!DNL Query Service].

## 目標 {#objectives}

此工作流程示範仰賴數個Adobe Experience Platform服務。 若您想繼續，建議您充分了解下列功能和服務：

* 此 [Experience Data Model(XDM)結構組合基本概念](../../xdm/schema/composition.md)
* 如何 [建立資料集和內嵌資料](https://experienceleague.adobe.com/docs/platform-learn/tutorials/data-ingestion/create-datasets-and-ingest-data.html)
* 如何 [使用Adobe Analytics來源連接器擷取資料](https://experienceleague.adobe.com/docs/platform-learn/tutorials/sources/ingest-data-from-adobe-analytics.html?lang=zh-Hant)
* [區段](../../segmentation/home.md)
* [目的地](../../destinations/home.md)

瀏覽放棄範例以使用Adobe為中心 [!DNL Analytics] 資料，以建立特定可操作的對象。 對象經過調整，以包含過去四天內瀏覽過網站但未購買的每個客戶。 接著，會以客戶行為模式所產生的最高價格SKU來鎖定對象中的每個設定檔。

查詢本身規範性很強，且僅包含符合區段定義之使用案例標準的資料。 這可以將 [!DNL Analytics] 正在處理的資料。 它也會依從最高到最低的價格訂購資料，並選擇使用者瀏覽的最高價格SKU。

演示文稿中使用的查詢如下所示：

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

以下提供的影片簡報提供全方位的真實案例，供您著重於的Experience Platform資料使用 [!DNL Query Service] 和Adobe分析整合。

>[!VIDEO](https://video.tv.adobe.com/v/342533?quality=12&learn=on)

## 優點 [!DNL Query Service] {#benefits}

提供的功能 [!DNL Query Service] 有許多用途。 您可以使用它來容納複雜的邏輯以用於細分、計算各種個人化屬性以供下游使用，或大幅簡化區段的建立方式。

[!DNL Query Service] 可讓您在查詢中加入限制，以簡化區段建立程式。 這可確保正確的資料符合區段的資格，並建立更精確的受眾，進而改善資料品質。 維護查詢品質，可提供準確的受眾，並有助於提升資料可靠性。 您也可以根據從查詢衍生的屬性建立結構和自訂表格，以儲存您的對象。 可為「設定檔」啟用自訂表格，且您可以將這些資料點用於細分和個人化。 此功能可協助行銷人員建立清晰的人員受眾。

此外，在查詢中加入滿足任何循環或靜態條件的邏輯， [!DNL Query Service] 提取複雜細分的負擔。

Adobe Experience Platform提供資料存放庫和必要的工具，讓您以有效且可靠的方式啟用資料。 將資料保留在Platform內，可讓您在執行其他程式時衍生屬性，而無須將資料匯出至協力廠商工具以進行操作和處理。 處理數百個屬性或行銷活動時，這類處理間接費用可能會對專案時間軸造成重大影響。 這可讓行銷人員在單一位置存取其資料並建置行銷活動，同時也提供將訊息分段及個人化的非常動態方式。

## 後續步驟

閱讀本檔案後，您現在應了解 [!DNL Query Service] 不僅會影響資料的品質和區段的便利性，也會影響資料架構對整個端對端工作流程的重要性。 如需更適用的SQL範例，請使用Adobe Analytics搭配 [!DNL Query Service]，請參閱 [Adobe Analytics銷售變數使用案例](./merchandising-variables.md).

說明 [!DNL Query Service] 對貴組織的策略性業務洞察 [機器人篩選使用案例](./bot-filtering.md) 範例。

或者，這些文檔有助於您了解 [!DNL Query Service] 功能：

* [查詢執行指南](../best-practices/writing-queries.md)
* [資料資產組織指南](../best-practices/organize-data-assets.md).


