---
title: 報告套裝資料的Adobe Analytics來源聯結器
description: 本檔案提供Analytics概觀及說明Analytics資料的使用案例。
exl-id: c4887784-be12-40d4-83bf-94b31eccdc2e
source-git-commit: 5ec22fcf0f4c48efc28a3abd343bb00a19756281
workflow-type: tm+mt
source-wordcount: '1110'
ht-degree: 2%

---

# 報告套裝資料的Adobe Analytics來源聯結器

Adobe Experience Platform可讓您透過Adobe Analytics來源聯結器擷取Analytics資料。 此 [!DNL Analytics] 來源聯結器串流資料收集者： [!DNL Analytics] 即時轉換至Platform，轉換SCD格式 [!DNL Analytics] 資料到 [!DNL Experience Data Model] (XDM)由平台使用的欄位。

本檔案提供以下專案的概觀： [!DNL Analytics] 並描述以下專案的使用案例： [!DNL Analytics] 資料。

## Adobe Analytics和Analytics資料

[!DNL Analytics] 是一個功能強大的引擎，可協助您進一步瞭解客戶、客戶如何與您的Web屬性互動、檢視您的數位行銷支出在何處有效，以及識別需要改善的領域。 [!DNL Analytics] 每年處理數萬億次的Web交易，以及 [!DNL Analytics] 來源聯結器可讓您輕鬆利用這項豐富的行為資料，並將 [!DNL Real-Time Customer Profile] 幾分鐘內。

![此圖形說明來自不同Adobe應用程式(包括Adobe Analytics)的資料歷程。](./images/analytics-data-experience-platform.png)

在高層面上， [!DNL Analytics] 從全球各地的各種數位頻道和多個資料中心收集資料。 收集到資料後，會套用訪客識別、細分和轉換架構(VISTA)規則和處理規則來塑造傳入的資料。 原始資料經過此輕量級處理之後，即可由以下人員使用 [!DNL Real-Time Customer Profile]. 在上述平行處理程式中，相同的已處理資料會經過微批次處理，並內嵌至Platform資料集，由以下人員消耗 [!DNL Query Service]和其他資料探索應用程式。

請參閱 [處理規則概觀](https://experienceleague.adobe.com/docs/analytics/admin/admin-tools/processing-rules/processing-rules.html) 以取得處理規則的詳細資訊。

## 體驗資料模式 (XDM)

XDM是公開記錄的規格，為應用程式提供通用結構和定義，用於與Experience Platform上的服務通訊。

遵守XDM標準可讓資料統一整合，讓您更輕鬆地傳送資料及收集資訊。

若要進一步瞭解XDM，請參閱 [XDM系統概覽](../../../xdm/home.md).

## 欄位如何從Adobe Analytics對應至XDM？

>[!IMPORTANT]
>
>「資料準備」轉換可能會增加整體資料流程的延遲。 新增的額外延遲因轉換邏輯的複雜度而異。

建立來源連線以帶來 [!DNL Analytics] 資料使用Platform使用者介面進入Experience Platform，資料欄位會自動對應並擷取到 [!DNL Real-Time Customer Profile] 幾分鐘內。 有關使用建立來源連線的指示 [!DNL Analytics] 使用Platform UI，請參閱 [Analytics來源聯結器教學課程](../../tutorials/ui/create/adobe-applications/analytics.md).

有關期間發生的欄位對應的詳細資訊 [!DNL Analytics] 和Experience Platform，請參閱 [Adobe Analytics欄位對映](./mapping/analytics.md) 指南。

## Platform上Analytics資料的預期延遲為何？

下表列出Platform上Analytics資料的預期延遲。 延遲會依客戶組態、資料磁碟區和消費者應用程式而有所不同。 例如，如果Analytics實作設定為 `A4T` 管道的延遲將增加到5至10分鐘。

| Analytics 資料 | 預期延遲 |
| -------------- | ---------------- |
| 將新資料新增至 [!DNL Real-Time Customer Profile] (A4T **非** 已啟用) | &lt; 2分鐘 |
| 將新資料新增至 [!DNL Real-Time Customer Profile] (A4T **是** 已啟用) | 長達30分鐘 |
| 資料湖的新資料 | &lt; 2.25小時 |
| 少於100億個事件的回填 | &lt; 4週 |

生產沙箱的Analytics回填預設為13個月。 對於非生產沙箱中的Analytics資料，回填會設定為三個月。 上表提及的100億個事件上限嚴格與預期延遲有關。

在生產沙箱中建立Analytics來源資料流時，會建立兩個資料流：

* 此資料流會將13個月的歷史報表套裝資料回填至Data Lake。 此資料流會在回填完成時結束。
* 將即時資料傳送至資料湖和的資料流流程。 [!DNL Real-Time Customer Profile]. 此資料流會持續執行。

>[!NOTE]
>
>Analytics回填資料未擷取至 [!DNL Profile] 因此，授權設定檔中不會計入此專案。

## 中的主要識別碼 [!DNL Analytics] 資料

來自的每次點選 [!DNL Analytics] 來源聯結器包含取決於ECID或AAID存在與否的主要識別碼。 如果有ECID，則會將ECID指定為主要識別碼。 如果有AAID，則會將AAID指定為主要的。

下表提供中身分欄位的詳細資訊 [!DNL Analytics] 資料。

| 身分欄位 | 說明 |
| --- | --- |
| AAID | AAID是Adobe Analytics中的主要裝置識別碼，並且保證存在於透過傳遞的每個事件中， [!DNL Analytics] 來源。 AAID有時稱為 *舊版Analytics ID* 或作為 `s_vi` Cookie ID。 儘管如此，系統仍會建立AAID，即使 `s_vi` Cookie不存在。 AAID由 `post_visid_high` 和 `post_visid_low` 欄於 [[!DNL Analytics] 資料摘要](https://experienceleague.adobe.com/docs/analytics/export/analytics-data-feed/data-feed-contents/datafeeds-reference.html). 在任何特定事件中，AAID欄位都包含單一身分識別，該身分識別可能是 [的作業順序 [!DNL Analytics] ID](https://experienceleague.adobe.com/docs/id-service/using/reference/analytics-reference/analytics-order-of-operations.html). **注意**：在整個報表套裝中，AAID可能包含跨事件的多種型別。 |
| ECID | ECID (Experience CloudAdobe Analytics ID)是獨立的裝置識別碼欄位，此欄位會在 [!DNL Analytics] 是使用Experience CloudIdentity Service實作。 ECID有時也稱為MCID (Marketing CloudID)。 如果事件中存在ECID，則AAID可能會以ECID為基礎，具體取決於Analytics是否 [寬限期](https://experienceleague.adobe.com/docs/id-service/using/reference/analytics-reference/grace-period.html) 已設定。 ECID由 `mcvisid` 在Analytics資料摘要中。 如需ECID的詳細資訊，請參閱 [ECID概觀](../../../identity-service/ecid.md). 如需ECID如何與搭配使用的詳細資訊 [!DNL Analytics]，請參閱上的檔案 [Analytics與Experience CloudID請求](https://experienceleague.adobe.com/docs/id-service/using/reference/analytics-reference/legacy-analytics.html). |
| AACUSTOMID | Adobe Analytics AACUSTOMID是一個單獨的識別碼欄位，根據 `s.VisitorID` 中的變數 [!DNL Analytics] 實作。 AACUSTOMID由 `cust_visid` 中的欄 [[!DNL Analytics] 資料摘要](https://experienceleague.adobe.com/docs/analytics/export/analytics-data-feed/data-feed-contents/datafeeds-reference.html). 如果AACUSTOMID存在，則AAID將會以AACUSTOMID為基礎，因為AACUSTOMID會勝過 [的作業順序 [!DNL Analytics] ID](https://experienceleague.adobe.com/docs/id-service/using/reference/analytics-reference/analytics-order-of-operations.html). |

### 如何 [!DNL Analytics] 來源處理身分

此 [!DNL Analytics] 來源將這些身分識別以XDM形式傳遞給Experience Platform，如下所示：

* `endUserIDs._experience.aaid.id`
* `endUserIDs._experience.mcid.id`
* `endUserIDs._experience.aacustomid.id`

這些欄位不會標記為身分識別。 而是將相同的身分識別複製到XDM的 `identityMap` 做為機碼值組：

* `{ "key": "AAID", "value": [ { "id": "<identity>", "primary": <true or false> } ] }`
* `{ "key": "ECID", "value": [ { "id": "<identity>", "primary": <true or false> } ] }`
* `{ "key": "AACUSTOMID", "value": [ { "id": "<identity>", "primary": false } ] }`

在身分對應中，如果ECID存在，則會標示為事件的主要身分。 在此情況下，AAID可能以ECID為基礎，因為 [Identity Service寬限期](https://experienceleague.adobe.com/docs/id-service/using/reference/analytics-reference/grace-period.html). 否則，AAID會標示為事件的主要身分識別。 AACUSTOMID 永遠不會標記為事件的主要 ID。不過，如果AACUSTOMID存在，則AAID會因為作業順序Experience Cloud而以AACUSTOMID為基礎。

>[!NOTE]
>
>您可以使用「資料準備」來篩選掉來自Analytics的次要身分，例如AAID和AACUSTOMID。 如果篩選掉，這些身分如果可在傳入的Analytics資料中使用，就不會擷取到設定檔中。 未篩選的資料將繼續載入資料湖。
