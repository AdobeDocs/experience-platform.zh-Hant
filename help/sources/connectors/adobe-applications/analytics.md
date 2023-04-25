---
title: Adobe Analytics報表套裝資料的來源連接器
description: 本檔案概述Analytics並說明Analytics資料的使用案例。
exl-id: c4887784-be12-40d4-83bf-94b31eccdc2e
source-git-commit: 83ce7d46e4e64fbe961c964ed5a17ec12a7ec15f
workflow-type: tm+mt
source-wordcount: '1112'
ht-degree: 7%

---

# 用於報告套裝資料的 Adobe Analytics 來源連接器

Adobe Experience Platform可讓您透過Analytics來源連接器內嵌Adobe Analytics資料。 此 [!DNL Analytics] 源連接器流收集的資料 [!DNL Analytics] 即時轉換SCDS格式 [!DNL Analytics] 資料 [!DNL Experience Data Model] (XDM)欄位，供Platform使用。

本檔案提供 [!DNL Analytics] 並說明 [!DNL Analytics] 資料。

## Adobe Analytics與Analytics資料

[!DNL Analytics] 是一款功能強大的引擎，可協助您進一步了解客戶、客戶如何與您的Web屬性互動、了解您的數位行銷支出有何成效，以及找出需要改善的領域。 [!DNL Analytics] 每年處理數萬億個Web事務， [!DNL Analytics] 來源連接器可讓您輕鬆利用這項豐富的行為資料，並加以擴充 [!DNL Real-Time Customer Profile] 幾分鐘內。

![說明不同Adobe應用程式(包括Adobe Analytics)資料歷程的圖形。](./images/analytics-data-experience-platform.png)

從高層面講， [!DNL Analytics] 收集來自全球不同數位頻道和多個資料中心的資料。 收集資料後，會套用訪客身分識別、分段和轉換架構(VISTA)規則及處理規則，以塑造傳入資料。 原始資料經過此輕量化處理後，便會視為已可供使用 [!DNL Real-Time Customer Profile]. 在與上述程式平行的程式中，相同的處理資料會經過微批次處理並擷取至Platform資料集，以供使用 [!DNL Data Science Workspace], [!DNL Query Service]，以及其他資料發現應用程式。

請參閱 [處理規則概觀](https://experienceleague.adobe.com/docs/analytics/admin/admin-tools/processing-rules/processing-rules.html) 以取得處理規則的詳細資訊。

## Experience Data Model(XDM)

XDM是公開記錄的規範，為應用程式提供通用結構和定義，以便與Experience Platform上的服務進行通信。

遵循XDM標準，即可統一整合資料，更輕鬆傳送資料和收集資訊。

若要進一步了解XDM，請參閱 [XDM系統概觀](../../../xdm/home.md).

## 如何將欄位從Adobe Analytics對應至XDM?

>[!IMPORTANT]
>
>資料準備轉換可能會增加整體資料流的延遲。 增加的額外延遲會因轉換邏輯的複雜度而異。

當建立源連接以將 [!DNL Analytics] 使用Platform使用者介面將資料匯入Experience Platform時，資料欄位會自動對應並匯入 [!DNL Real-Time Customer Profile] 幾分鐘內。 有關建立源連接的說明 [!DNL Analytics] 使用Platform UI，請參閱 [Analytics來源連接器教學課程](../../tutorials/ui/create/adobe-applications/analytics.md).

有關在 [!DNL Analytics] 和Experience Platform，請參閱 [Adobe Analytics欄位對應](./mapping/analytics.md) 指南。

## 平台上Analytics資料的預期延遲為何？

下表列出Platform上Analytics資料的預期延遲。 延遲會因客戶配置、資料量和消費者應用程式而異。 例如，如果Analytics實施已設定 `A4T` 管道延遲會增加至5-10分鐘。

| Analytics 資料 | 預期延遲 |
| -------------- | ---------------- |
| 新資料 [!DNL Real-Time Customer Profile] (A4T) **not** 已啟用) | &lt; 2 分鐘 |
| 新資料 [!DNL Real-Time Customer Profile] (A4T) **is** 已啟用) | 最多30分鐘 |
| 資料湖的新資料 | &lt; 90 分鐘 |
| 回填少於100億個事件 | &lt; 4 週 |

生產沙箱的Analytics回填預設為13個月。 若為非生產沙箱中的Analytics資料，回填會設為三個月。 上表所述100億次事件的上限嚴格取決於預期的延遲。

在生產沙箱中建立Analytics來源資料流時，會建立兩個資料流：

* 將13個月的歷史報表套裝資料回填至資料湖的資料流。 此資料流在回填完成時結束。
* 將即時資料發送到資料湖和的資料流 [!DNL Real-Time Customer Profile]. 此資料流持續運行。

>[!NOTE]
>
>Analytics回填資料不會擷取至 [!DNL Profile] 因此，不會計入授權設定檔中。

## 中的主要識別碼 [!DNL Analytics] 資料

來自 [!DNL Analytics] 來源連接器包含主要識別碼，視ECID或AAID是否存在而定。 如果有ECID，系統會將ECID指定為主要識別碼。 如果有AAID，則將AAID指定為主要。

下表提供您 [!DNL Analytics] 資料。

| 身分欄位 | 說明 |
| --- | --- |
| AAID | AAID是Adobe Analytics中的主要裝置識別碼，且必定會存在於通過 [!DNL Analytics] 來源。 AAID有時稱為 *舊版Analytics ID* 或 `s_vi` cookie ID。 儘管如此，系統仍會建立AAID，即使 `s_vi` cookie不存在。 AAID由 `post_visid_high` 和 `post_visid_low` 欄 [[!DNL Analytics] 資料摘要](https://experienceleague.adobe.com/docs/analytics/export/analytics-data-feed/data-feed-contents/datafeeds-reference.html). 在任何指定事件上，AAID欄位包含單一身分，該身分可能是 [操作順序 [!DNL Analytics] ID](https://experienceleague.adobe.com/docs/id-service/using/reference/analytics-reference/analytics-order-of-operations.html). **附註**:在整個報表套裝中，AAID可能包含不同事件的多種類型。 |
| ECID | ECID(Experience CloudID)是個別的裝置識別碼欄位，在 [!DNL Analytics] 是使用Experience Cloud身分服務實作。 ECID有時也稱為MCID(Marketing CloudID)。 如果事件上有ECID,AAID可能會以ECID為基礎，端視Analytics [寬限期](https://experienceleague.adobe.com/docs/id-service/using/reference/analytics-reference/grace-period.html) 已設定。 ECID由 `mcvisid` 在Analytics資料摘要中。 如需ECID的詳細資訊，請參閱 [ECID概觀](../../../identity-service/ecid.md). 如需ECID如何運作的相關資訊 [!DNL Analytics]，請參閱 [Analytics與Experience CloudID請求](https://experienceleague.adobe.com/docs/id-service/using/reference/analytics-reference/legacy-analytics.html?lang=zh-Hant). |
| AACUSTOMID | AACUSTOMID是個別的識別碼欄位，會根據使用 `s.VisitorID` 變數 [!DNL Analytics] 實作。 AACUSTOMID由 `cust_visid` 欄 [[!DNL Analytics] 資料摘要](https://experienceleague.adobe.com/docs/analytics/export/analytics-data-feed/data-feed-contents/datafeeds-reference.html). 如果AACUSTOMID存在，則AAID將以AACUSTOMID為基礎，因為AACUSTOMID會壓倒由 [操作順序 [!DNL Analytics] ID](https://experienceleague.adobe.com/docs/id-service/using/reference/analytics-reference/analytics-order-of-operations.html). |

### 如何 [!DNL Analytics] 來源識別

此 [!DNL Analytics] 來源會以XDM形式將這些身分傳遞至Experience Platform:

* `endUserIDs._experience.aaid.id`
* `endUserIDs._experience.mcid.id`
* `endUserIDs._experience.aacustomid.id`

這些欄位不會標記為身分識別。 相反地，相同的身分會複製到XDM的 `identityMap` 作為機碼值組：

* `{ "key": "AAID", "value": [ { "id": "<identity>", "primary": <true or false> } ] }`
* `{ "key": "ECID", "value": [ { "id": "<identity>", "primary": <true or false> } ] }`
* `{ "key": "AACUSTOMID", "value": [ { "id": "<identity>", "primary": false } ] }`

在身分對應中，如果ECID存在，則會標示為事件的主要身分。 在此情況下，AAID可能會以ECID為基礎，因為 [Identity服務寬限期](https://experienceleague.adobe.com/docs/id-service/using/reference/analytics-reference/grace-period.html). 否則，AAID 將標記為事件的主要身分識別。AACUSTOMID 永遠不會標記為事件的主要 ID。不過，如果存在AACUSTOMID，則AAID會根據AACUSTOMID，因為Experience Cloud的操作順序。
