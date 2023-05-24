---
title: Adobe Analytics報表套件資料源連接器
description: 此文檔概述了分析，並介紹了分析資料的使用案例。
exl-id: c4887784-be12-40d4-83bf-94b31eccdc2e
source-git-commit: 83ce7d46e4e64fbe961c964ed5a17ec12a7ec15f
workflow-type: tm+mt
source-wordcount: '1112'
ht-degree: 7%

---

# 用於報告套裝資料的 Adobe Analytics 來源連接器

Adobe Experience Platform允許您通過分析源連接器接收Adobe Analytics資料。 的 [!DNL Analytics] 源連接器流收集的資料 [!DNL Analytics] 即時轉換到平台，轉換SCDS格式 [!DNL Analytics] 資料 [!DNL Experience Data Model] (XDM)欄位，供平台使用。

此文檔提供 [!DNL Analytics] 並說明 [!DNL Analytics] 資料。

## Adobe Analytics和分析資料

[!DNL Analytics] 是一個功能強大的引擎，可幫助您瞭解更多有關客戶的資訊、客戶如何與您的Web屬性交互、查看您的數字營銷支出在哪裡有效，以及確定需要改進的領域。 [!DNL Analytics] 每年處理數萬億個Web事務 [!DNL Analytics] 源連接器允許您輕鬆地利用此豐富的行為資料並豐富 [!DNL Real-Time Customer Profile] 幾分鐘後。

![一個圖示，說明來自不同Adobe應用程式(包括Adobe Analytics)的資料的歷程。](./images/analytics-data-experience-platform.png)

在高層面， [!DNL Analytics] 收集來自世界各地各種數字通道和多個資料中心的資料。 一旦收集到資料，就會應用訪問者識別、分段和轉換體系結構(VISTA)規則和處理規則來塑造傳入資料。 在原始資料經過此輕量級處理後，它便被視為可供使用 [!DNL Real-Time Customer Profile]。 在與上述過程平行的過程中，將相同的處理資料進行微批處理並放入平台資料集中，以供 [!DNL Data Science Workspace]。 [!DNL Query Service]以及其他資料發現應用程式。

查看 [處理規則概述](https://experienceleague.adobe.com/docs/analytics/admin/admin-tools/processing-rules/processing-rules.html) 的子菜單。

## 體驗資料模型(XDM)

XDM是一種公開記錄的規範，它為應用程式提供了通用結構和定義，以用於與Experience Platform上的服務通信。

遵守XDM標準可以統一整合資料，使資料傳輸和資訊收集更加容易。

要瞭解有關XDM的詳細資訊，請參閱 [XDM系統概述](../../../xdm/home.md)。

## 如何將欄位從Adobe Analytics映射到XDM?

>[!IMPORTANT]
>
>資料準備轉換可能會增加整個資料流的延遲。 增加的附加延遲根據轉換邏輯的複雜性而改變。

當建立源連接時 [!DNL Analytics] 使用平台用戶介面將資料映射到Experience Platform中，資料欄位被自動映射和接收到 [!DNL Real-Time Customer Profile] 幾分鐘內。 有關建立源連接的說明 [!DNL Analytics] 使用平台UI，請參見 [分析源連接器教程](../../tutorials/ui/create/adobe-applications/analytics.md)。

有關在以下時間之間發生的欄位映射的詳細資訊 [!DNL Analytics] 和Experience Platform，看 [Adobe Analytics域映射](./mapping/analytics.md) 的子菜單。

## 平台上分析資料的預期延遲是什麼？

下表概述了平台上分析資料的預期延遲。 延遲因客戶配置、資料卷和用戶應用程式而異。 例如，如果Analytics實現配置了 `A4T` 到管道的延遲將增加到5-10分鐘。

| Analytics 資料 | 預期延遲 |
| -------------- | ---------------- |
| 新資料到 [!DNL Real-Time Customer Profile] (A4T) **不** 啟用) | &lt; 2 分鐘 |
| 新資料到 [!DNL Real-Time Customer Profile] (A4T) **是** 啟用) | 最多30分鐘 |
| 資料湖的新資料 | &lt; 90 分鐘 |
| 少於100億個事件的回填 | &lt; 4 週 |

生產沙箱的分析回填預設為13個月。 對於非生產沙箱中的分析資料，回填設定為三個月。 上表所列100億個事件的限額嚴格地與預期延遲有關。

在生產沙箱中建立分析源資料流時，將建立兩個資料流：

* 一種資料流，將歷史報告套件資料13個月的回填到資料湖中。 當回填完成時，此資料流將結束。
* 向資料湖和資料湖發送即時資料的資料流 [!DNL Real-Time Customer Profile]。 此資料流會持續運行。

>[!NOTE]
>
>分析回填資料未被插入 [!DNL Profile] 因此未在許可證配置檔案中計算。

## 中的主標識符 [!DNL Analytics] 資料

每次從 [!DNL Analytics] 源連接器包含主標識符，該標識符取決於ECID或AAID是否存在。 如果存在ECID，則將ECID指定為主標識符。 如果存在AAID，則將AAID指定為主AID。

下表提供了有關您的 [!DNL Analytics] 資料。

| 標識欄位 | 說明 |
| --- | --- |
| AAID | AAID是Adobe Analytics的主要設備標識符，並保證在通過的每個事件上都存在 [!DNL Analytics] 源。 AAID有時稱為 *舊分析ID* 或 `s_vi` Cookie ID。 儘管如此，即使AAID `s_vi` cookie不存在。 AAID由 `post_visid_high` 和 `post_visid_low` 列 [[!DNL Analytics] 資料饋送](https://experienceleague.adobe.com/docs/analytics/export/analytics-data-feed/data-feed-contents/datafeeds-reference.html)。 在任何給定事件上，AAID欄位都包含單個標識，該標識可能是中所述的幾種不同類型之一 [操作順序 [!DNL Analytics] ID](https://experienceleague.adobe.com/docs/id-service/using/reference/analytics-reference/analytics-order-of-operations.html)。 **注釋**:在整個報告套件中，AAID可能包含各種事件的類型。 |
| ECID | ECID(Experience CloudID)是一個單獨的設備標識符欄位，在Adobe Analytics [!DNL Analytics] 使用Experience Cloud身份服務實現。 ECID有時也稱為MCID(Marketing CloudID)。 如果事件上存在ECID，則AAID可能基於ECID，具體取決於分析 [寬限期](https://experienceleague.adobe.com/docs/id-service/using/reference/analytics-reference/grace-period.html) 已配置。 ECID由 `mcvisid` 在分析資料源中。 有關ECID的詳細資訊，請參見 [ECID概述](../../../identity-service/ecid.md)。 有關ECID如何使用的資訊 [!DNL Analytics]，請參閱上的文檔 [分析和Experience CloudID請求](https://experienceleague.adobe.com/docs/id-service/using/reference/analytics-reference/legacy-analytics.html?lang=zh-Hant)。 |
| AACUSTOMID | AACUSTOMID是一個單獨的標識符欄位，它根據使用 `s.VisitorID` 變數 [!DNL Analytics] 執行。 AACUSTOMID由 `cust_visid` 列 [[!DNL Analytics] 資料饋送](https://experienceleague.adobe.com/docs/analytics/export/analytics-data-feed/data-feed-contents/datafeeds-reference.html)。 如果存在AACUSTOMID，則AAID將基於AACUSTOMID，因為AACUSTOMID比由 [操作順序 [!DNL Analytics] ID](https://experienceleague.adobe.com/docs/id-service/using/reference/analytics-reference/analytics-order-of-operations.html)。 |

### 如何 [!DNL Analytics] 源代理

的 [!DNL Analytics] 源將這些標識以XDM形式傳遞給Experience Platform，如：

* `endUserIDs._experience.aaid.id`
* `endUserIDs._experience.mcid.id`
* `endUserIDs._experience.aacustomid.id`

這些欄位不會標記為身分識別。 相反，相同的標識被複製到XDM `identityMap` 作為鍵值對：

* `{ "key": "AAID", "value": [ { "id": "<identity>", "primary": <true or false> } ] }`
* `{ "key": "ECID", "value": [ { "id": "<identity>", "primary": <true or false> } ] }`
* `{ "key": "AACUSTOMID", "value": [ { "id": "<identity>", "primary": false } ] }`

在標識映射中，如果存在ECID，則將其標籤為事件的主標識。 在這種情況下，AAID可能基於ECID，因為 [身份服務寬限期](https://experienceleague.adobe.com/docs/id-service/using/reference/analytics-reference/grace-period.html)。 否則，AAID 將標記為事件的主要身分識別。AACUSTOMID 永遠不會標記為事件的主要 ID。但是，如果存在AACUSTOMID，則AAID基於AACUSTOMID，因為操作的Experience Cloud順序。
