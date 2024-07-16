---
title: RainFocus來源概述
description: 瞭解如何將RainFocus帳戶中的事件管理和分析資料帶入Experience Platform
last-substantial-update: 2023-06-21T00:00:00Z
badge: Beta
exl-id: 88e333e3-2b93-4d66-8412-efadea58ac46
source-git-commit: b4334b4f73428f94f5a7e5088f98e2459afcaf3c
workflow-type: tm+mt
source-wordcount: '969'
ht-degree: 4%

---

# [!DNL RainFocus]

>[!NOTE]
>
>[!DNL RainFocus]來源是測試版。 如需使用Beta版標籤來源的相關資訊，請參閱[來源概觀](../../home.md#terms-and-conditions)。

[!DNL RainFocus]是一個平台，可用來推廣您的活動並建置您的對象。 您可以使用[!DNL RainFocus]來建立精美的促銷頁面、追蹤促銷活動成效並最佳化註冊轉換。

在Adobe Experience Platform和Real-time Customer Data Platform中使用[!DNL RainFocus]來源，透過出席者體驗事件即時自動擴充您的客戶資料設定檔。 在啟用後，體驗事件會自動串流到Real-Time CDP中，以便使用下游目的地和應用程式(例如Customer Journey Analytics和Adobe Journey Optimizer)進行強大的受眾細分、資料分析和啟用與會者歷程。

>[!IMPORTANT]
>
>此來源聯結器和檔案頁面是由[!DNL RainFocus]團隊建立和維護的。 若有任何查詢或更新要求，請直接透過clientcare<span>@rainfocus.com聯絡他們，或造訪[[!DNL RainFocus] 說明中心](https://help.rainfocus.com/hc/en-us)

## 先決條件

您必須先完成下列必要條件，才能在Experience Platform上啟用[!DNL RainFocus]整合：

[在Adobe Developer入口網站中建立Adobe服務帳戶(JWT)](https://developer.adobe.com/developer-console/docs/guides/authentication/ServiceAccountIntegration/)

>[!IMPORTANT]
>
>Adobe最近宣佈淘汰JWT權杖，改用OAuth。 為因應此變更，[!DNL RainFocus]來源不久將會移轉至OAuth。

### 收集必要的認證

為了連線[!DNL RainFocus]至Experience Platform，您必須在[!DNL RainFocus]中提供下列連線屬性的值：

| 認證 | 說明 | 範例 |
| --- | --- | --- |
| 用戶端 ID | 使用者端ID可從Adobe Developer入口網站的Adobe服務帳戶中取得。 | `b9c32a63e7d41a0f87d3e8b52a16e7a2` |
| 使用者端密碼 | 使用者端密碼可在Adobe Developer入口網站的Adobe服務帳戶中取得。 | `k1b-p-umplcjtg_arnw-R-Bx44bybu` |
| 技術帳戶ID | 技術帳戶ID可從Adobe Developer入口網站的Adobe服務帳戶中取得。 | `B3F9D2E8A64C573D21ABFE97@techacct.adobe.com` |
| 組織 ID | 組織ID可從Adobe Developer入口網站的Adobe服務帳戶中取得 | `D9A6F3BCE82FD147C50E3A19@techacct.adobe.com` |

### 建立XDM結構描述並定義身分欄位 {#create-an-xdm-schema-and-define-the-identity-field}

為了以Experience Platform儲存[!DNL RainFocus]中的體驗事件，您必須建立體驗資料模型(XDM)結構描述來說明可以儲存可能從[!DNL RainFocus]傳送的欄位和資料型別的資料集。

[!DNL RainFocus]建議下列欄位，涵蓋預設傳送的所有可能資料。

也建議使用下列欄位群組（以首碼表示）：

* 出席者
* 參展商
* 銷售機會
* Session
* 工作階段時間

**結構描述應包含下列欄位：**

| 欄位 | 類型 | 範例 | 說明 |
| --- | --- | --- | --- |
| `attendee.registered` | 字串 | 是 | 決定出席者是否被視為已註冊的旗標。 |
| `attendee.attendeeId` | 字串 | 1619119968857001fvLB | [!DNL RainFocus]中的出席者識別碼。 |
| `attendee.externalId` | 字串 | 1666809456617001wyPj | 組織指定的外部ID。 |
| `attendee.clientId` | 字串 | 8EFC1F57631CAFE70A495ECB@8f3f1f5c631caf3e495fd8.e | 出席者SSO使用者端ID。 |
| `attendee.email` | 字串 | user<span>@company.com | 出席者的電子郵件地址。 |
| `transmissionId` | 字串 | 1680309557133001YHhz | 用於資料推送的唯一識別碼。 |
| `eventType` | 字串 | 已排程工作階段 | 出席者體驗活動的名稱。 |
| `timestamp` | 日期時間 | 2023-04-01T00:41:57.000Z | 資料推送的時間戳記。 |
| `event.name` | 字串 | Adobe Summit2023 | 發生傳輸的事件的名稱。 |
| `exhibitor.exhibitorId` | 字串 | 1680309557133001YHhz | 參展商的[!DNL RainFocus]識別碼。 |
| `exhibitor.externalId` | 字串 | 1666809514105001lSJN | 使用者端系統中參展商的識別碼。 |
| `exhibitor.name` | 字串 | IBM | 參展商的名稱。 |
| `lead.leadId` | 字串 | 1666809456617001wyPj | 潛在客戶的[!DNL RainFocus]識別碼。 |
| `lead.note` | 字串 | | |
| `session.sessionId` | 字串 | 1666809373585001t4aV | 工作階段的[!DNL RainFocus]識別碼。 |
| `session.externalId` | 字串 | 1666809456617001wyPj | 使用者端系統中工作階段的識別碼。 |
| `session.code` | 字串 | GS3 | 工作階段的程式碼。 |
| `session.title` | 字串 | Inspiration主題演講 | 工作階段的標題。 |
| `session.length` | 整數 | 90 | 作業階段長度。 |
| `sessiontime.sessiontimeId` | 字串 | 1673033149739001OJLZ | 工作階段時間的[!DNL RainFocus]識別碼。 |
| `sessiontime.startTime` | 字串 | 2023-03-22 10:00:00 | 工作階段的開始時間。 |
| `sessiontime.endTime` | 字串 | 2023-03-22 10:00:00 | 工作階段的結束時間。 |
| `sessiontime.room` | 字串 | B32 | 用於工作階段的空間。 |

{style="table-layout:auto"}

若要為[!DNL RainFocus]資料建立結構描述，請閱讀以下檔案，以瞭解如何使用API或UI建立結構描述的步驟。

* [使用UI建立結構描述](../../../xdm/tutorials/create-schema-ui.md)
* [使用API建立結構描述](../../../xdm/tutorials/create-schema-api.md)

>[!IMPORTANT]
>
>* 結構描述必須擴充&#x200B;**XDM ExperienceEvent類別。**
>* 您必須確保結構描述包含&#x200B;**主要身分**，且已為設定檔&#x200B;**啟用**。 如需詳細資訊，請閱讀[在UI中定義身分欄位的指南](https://experienceleague.adobe.com/docs/experience-platform/xdm/ui/fields/identity.html)
>* 您可以將身分範例（電子郵件）取代為另一個適當的識別碼，例如sha256電子郵件或ECID。

### 在RainFocus中建立整合設定檔 {#create-an-integration-profile-in-rainfocus}

一旦您的服務帳戶和XDM結構描述準備就緒後，您現在可以透過[!DNL RainFocus]平台啟用[!DNL Integration Profile]。 [!DNL Integration Profile]負責將資料串流至Experience Platform。

登入[[!DNL RainFocus] 平台](https://app.rainfocus.com)。 在主要導覽區中選取&#x200B;**[!DNL Libraries]**，然後選取&#x200B;**[!DNL Integration Profiles]**

![已選取資料庫與整合設定檔的RainFocus UI。](/help/sources/images/tutorials/create/rainfocus/rainfocus_integration-profile.png)

若要建立新的設定檔，請選取&#x200B;**(`+`)**&#x200B;圖示。 接著，選取&#x200B;**Adobe Real-time Customer Data Platform**，然後選取&#x200B;**確定**。

![在RainFocus UI中建立整合設定檔視窗。](/help/sources/images/tutorials/create/rainfocus/rainfocus_integration-profile-select.png)

接下來，提供您在Adobe Developer入口網站專案中擷取的認證：

* **使用者端識別碼**
* **使用者端密碼**
* **技術帳戶ID**
* **組織 ID**

提供認證後，請選取「**[!DNL Save]**」。您現在應該會在[!DNL RainFocus]儀表板中看到新的[!DNL Integration Profile]列出。

選取您剛建立的[!DNL Integration Profile]，以檢視已設定的預先定義&#x200B;**推送型別**&#x200B;清單。 這些是將在發生時傳送給Experience Platform的[體驗事件](https://experienceleague.adobe.com/docs/experience-platform/xdm/classes/experienceevent.html)。

![ RainFocus儀表板中預先定義的推播型別清單。](/help/sources/images/tutorials/create/rainfocus/rainfocus_integration-profile-setup.png)

若要擷取範例JSON裝載的復本，請選取&#x200B;**[!DNL Sample JSON Payload]**。 接著，反白並複製範例JSON裝載，然後&#x200B;**將其儲存在副檔名為.json**&#x200B;的新檔案中。 這稍後將用於[對應組態](../../tutorials/ui/create/analytics/rainfocus.md#mapping)的Experience Platform。

![RainFocus儀表板中的JSON裝載範例。](/help/sources/images/tutorials/create/rainfocus/rainfocus_integration-profile-json.png)

>[!TIP]
>
>**安裝尚未完成**：建立資料流後，您必須提供您的&#x200B;**串流端點URL**&#x200B;和&#x200B;**資料流ID**，返回[!DNL RainFocus]儀表板以完成您的[!DNL Integration Profile]。

## 後續步驟

閱讀本檔案後，您已完成從[!DNL RainFocus]帳戶將資料串流到Experience Platform所需的先決條件設定。 您現在可以在[使用使用者介面](../../tutorials/ui/create/analytics/rainfocus.md)連線 [!DNL RainFocus] 以Experience Platform時繼續參閱指南。
