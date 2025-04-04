---
title: 報告套裝資料的Adobe Analytics Source Connector
description: 本檔案提供Analytics概觀及說明Analytics資料的使用案例。
exl-id: c4887784-be12-40d4-83bf-94b31eccdc2e
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '1196'
ht-degree: 0%

---

# 報告套裝資料的Adobe Analytics來源聯結器

Adobe Experience Platform可讓您透過Adobe Analytics來源聯結器擷取Analytics資料。 [!DNL Analytics]來源聯結器會即時將[!DNL Analytics]所收集的資料串流到Experience Platform，將SCD格式的[!DNL Analytics]資料轉換為[!DNL Experience Data Model] (XDM)欄位以供Experience Platform使用。

本檔案提供[!DNL Analytics]的概觀，並說明[!DNL Analytics]資料的使用案例。

## Adobe Analytics和Analytics資料

[!DNL Analytics]是一款功能強大的引擎，可協助您進一步瞭解客戶、客戶如何與您的Web屬性互動、瞭解您的數位行銷支出在何處有效，以及找出需要改善的領域。 [!DNL Analytics]每年會處理數萬億個網頁交易，而[!DNL Analytics]來源聯結器可讓您輕鬆擷取此豐富的行為資料，並在幾分鐘內擴充[!DNL Real-Time Customer Profile]。

![說明不同Adobe應用程式(包括Adobe Analytics)之資料歷程的圖形。](./images/analytics-data-experience-platform.png)

基本上，[!DNL Analytics]會從全球各個數位頻道和多個資料中心收集資料。 收集到資料後，會套用訪客識別、細分和轉換架構(VISTA)規則和處理規則來塑造傳入的資料。 原始資料經過此輕量型處理之後，就會被視為[!DNL Real-Time Customer Profile]已可供使用。 在上述平行處理程式中，相同的已處理資料會經過微批次處理，並擷取至Experience Platform資料集，以供[!DNL Query Service]和其他資料探索應用程式使用。

如需處理規則的詳細資訊，請參閱[處理規則總覽](https://experienceleague.adobe.com/docs/analytics/admin/admin-tools/processing-rules/processing-rules.html)。

## 體驗資料模式 (XDM)

XDM是公開記錄的規格，為應用程式提供通用結構和定義，用於與Experience Platform上的服務通訊。

遵守XDM標準可讓資料統一整合，讓您更輕鬆地傳送資料及收集資訊。

若要深入瞭解XDM，請參閱[XDM系統總覽](../../../xdm/home.md)。

## 欄位如何從Adobe Analytics對應至XDM？

>[!IMPORTANT]
>
>「資料準備」轉換可能會增加整體資料流程的延遲。 新增的額外延遲因轉換邏輯的複雜度而異。

建立來源連線以使用Experience Platform使用者介面將[!DNL Analytics]資料帶入Experience Platform時，資料欄位會自動對應並在數分鐘內擷取到[!DNL Real-Time Customer Profile]。 如需使用Experience Platform UI建立與[!DNL Analytics]的來源連線的指示，請參閱[Analytics來源聯結器教學課程](../../tutorials/ui/create/adobe-applications/analytics.md)。

如需[!DNL Analytics]與Experience Platform之間發生之欄位對應的詳細資訊，請參閱[Adobe Analytics欄位對應](./mapping/analytics.md)指南。

## Experience Platform上的Analytics資料延遲時間預計會多久？

下表列出Experience Platform上Analytics資料的預期延遲。 延遲會依客戶組態、資料磁碟區和消費者應用程式而有所不同。 例如，如果Analytics實作設定為`A4T`，則管道的延遲將增加到5-10分鐘。

| Analytics資料 | 預期延遲 |
| -------------- | ---------------- |
| 新資料至[!DNL Real-Time Customer Profile] （A4T **未啟用**） | &lt; 2分鐘 |
| [!DNL Real-Time Customer Profile]的新資料（A4T **已啟用**） | 長達30分鐘 |
| 資料湖的新資料 | &lt; 2.25小時 |
| 新資料至Customer Journey Analytics而無需[拼接](https://experienceleague.adobe.com/docs/analytics-platform/using/stitching/overview.html?lang=en) | &lt; 3.75小時 |
| 使用拼接將資料新增至Customer Journey Analytics | &lt; 7小時 |
| 少於100億個事件的回填 | &lt; 4週 |

如需Customer Journey Analytics延遲的詳細資訊，請參閱： [Customer Journey Analytics護欄](https://experienceleague.adobe.com/docs/analytics-platform/using/cja-admin/guardrails.html?lang=en)。

生產沙箱的Analytics回填預設為13個月。 對於非生產沙箱中的Analytics資料，回填會設定為三個月。 上表提及的100億個事件上限嚴格與預期延遲有關。

在生產沙箱中建立Analytics來源資料流時，會建立兩個資料流：

* 此資料流會將13個月的歷史報表套裝資料回填至Data Lake。 此資料流會在回填完成時結束。
* 將即時資料傳送到資料湖和[!DNL Real-Time Customer Profile]的資料流流程。 此資料流會持續執行。

>[!NOTE]
>
>Analytics回填資料未擷取至[!DNL Profile]，因此不在授權設定檔中。

## [!DNL Analytics]資料中的主要識別碼

來自[!DNL Analytics]來源聯結器的每個點選都包含一個主要識別碼，此識別碼取決於ECID或AAID是否存在。 如果有ECID，則會將ECID指定為主要識別碼。 如果有AAID，則會將AAID指定為主要的。

下表提供您[!DNL Analytics]資料中識別欄位的詳細資訊。

| 身分欄位 | 說明 |
| --- | --- |
| AAID | AAID是Adobe Analytics中的主要裝置識別碼，並且保證存在於透過[!DNL Analytics]來源傳遞的每個事件中。 AAID有時稱為&#x200B;*舊版Analytics ID*&#x200B;或`s_vi` Cookie ID。 儘管如此，即使`s_vi` Cookie不存在，仍會建立AAID。 AAID由[[!DNL Analytics] 資料摘要](https://experienceleague.adobe.com/docs/analytics/export/analytics-data-feed/data-feed-contents/datafeeds-reference.html)中的`post_visid_high`和`post_visid_low`欄表示。 在任何特定事件上，AAID欄位都包含單一身分識別，該身分識別可能是 [!DNL Analytics] ID](https://experienceleague.adobe.com/docs/id-service/using/reference/analytics-reference/analytics-order-of-operations.html)的[作業順序中所述的幾種型別之一。 **注意**：在整個報告套裝中，AAID可能包含跨事件的多種型別。 |
| ECID | ECID (Experience Cloud ID)是單獨的裝置識別碼欄位，在使用Experience Cloud Identity Service實作[!DNL Analytics]時填入到Adobe Analytics中。 ECID有時也稱為MCID (Marketing Cloud ID)。 如果事件中存在ECID，則AAID可能會以ECID為基礎，具體取決於是否設定了Analytics [寬限期](https://experienceleague.adobe.com/docs/id-service/using/reference/analytics-reference/grace-period.html)。 ECID由Analytics資料摘要中的`mcvisid`表示。 如需有關ECID的詳細資訊，請參閱[ECID概觀](../../../identity-service/features/ecid.md)。 如需ECID如何搭配[!DNL Analytics]使用的詳細資訊，請參閱[Analytics與Experience Cloud ID要求](https://experienceleague.adobe.com/docs/id-service/using/reference/analytics-reference/legacy-analytics.html)的相關檔案。 |
| AACUSTOMID | AACUSTOMID是一個單獨的識別碼欄位，根據[!DNL Analytics]實作中`s.VisitorID`變數的使用情況在Adobe Analytics中填入。 AACUSTOMID由[[!DNL Analytics] 資料摘要](https://experienceleague.adobe.com/docs/analytics/export/analytics-data-feed/data-feed-contents/datafeeds-reference.html)中的`cust_visid`資料行表示。 如果AACUSTOMID存在，則AAID將會以AACUSTOMID為基礎，因為AACUSTOMID會勝過 [!DNL Analytics] ID](https://experienceleague.adobe.com/docs/id-service/using/reference/analytics-reference/analytics-order-of-operations.html)的[作業順序所定義的所有其他識別碼。 |

### [!DNL Analytics]來源如何處理身分

[!DNL Analytics]來源將這些身分識別以XDM形式傳遞給Experience Platform，如下所示：

* `endUserIDs._experience.aaid.id`
* `endUserIDs._experience.mcid.id`
* `endUserIDs._experience.aacustomid.id`

這些欄位不會標籤為身分。 相反地，相同的身分（如果存在於事件中）會作為索引鍵值配對複製到XDM的`identityMap`中：

* `{ "key": "AAID", "value": [ { "id": "<identity>", "primary": <true or false> } ] }`
* `{ "key": "ECID", "value": [ { "id": "<identity>", "primary": <true or false> } ] }`
* `{ "key": "AACUSTOMID", "value": [ { "id": "<identity>", "primary": false } ] }`

將身分或身分複製至`identityMap`時，`endUserIDs._experience.mcid.namespace.code`也會設定在相同事件上：

* 如果AAID存在，`endUserIDs._experience.aaid.namespace.code`會設為&quot;AAID&quot;。
* 如果ECID存在，`endUserIDs._experience.mcid.namespace.code`會設為&quot;ECID&quot;。
* 如果AACUSTOMID存在，`endUserIDs._experience.aacustomid.namespace.code`會設為「AACUSTOMID」。

在身分對應中，如果ECID存在，則會標示為事件的主要身分。 在這種情況下，由於[Identity服務寬限期](https://experienceleague.adobe.com/docs/id-service/using/reference/analytics-reference/grace-period.html)，AAID可能會以ECID為基礎。 否則，AAID會標示為事件的主要身分識別。 絕不會將AACUSTOMID標示為事件的主要ID。 不過，如果AACUSTOMID存在，則由於Experience Cloud的作業順序，AAID會以AACUSTOMID為基礎。

>[!NOTE]
>
>您可以使用「資料準備」來篩選掉來自Analytics的次要身分，例如AAID和AACUSTOMID。 如果篩選掉，這些身分如果可在傳入的Analytics資料中使用，就不會擷取到設定檔中。 未篩選的資料將繼續載入資料湖。
