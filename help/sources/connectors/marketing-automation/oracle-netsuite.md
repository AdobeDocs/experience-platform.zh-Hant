---
title: oracleNetSuite Source概觀
description: 瞭解如何使用API或使用者介面將OracleNetSuite連線至Adobe Experience Platform。
last-substantial-update: 2024-01-30T00:00:00Z
badge: Beta
exl-id: 1dd30660-c990-4d3f-a64f-2a17e426f56d
source-git-commit: 8be502c9eea67119dc537a5d63a6c71e0bff1697
workflow-type: tm+mt
source-wordcount: '748'
ht-degree: 2%

---

# [!DNL Oracle NetSuite]

>[!NOTE]
>
>[!DNL Oracle NetSuite]來源是測試版。 如需使用Beta版標籤來源的相關資訊，請參閱[來源概觀](../../home.md#terms-and-conditions)。

Adobe Experience Platform可讓您從外部來源擷取資料，同時使用Platform服務來建構、加標籤及增強傳入資料。 您可以從多種來源(例如Adobe應用程式、雲端儲存、資料庫和許多其他來源)內嵌資料。

Experience Platform提供擷取資料協力廠商行銷自動化系統的支援。 對行銷自動化提供者的支援包括[!DNL Oracle NetSuite]。

[[!DNL Oracle NetSuite]](https://www.netsuite.com/)是以雲端為基礎的企業管理套件，包含ERP/財務、CRM及電子商務解決方案。

您可以使用兩個不同的來源從[!DNL Oracle NetSuite]擷取資料至Experience Platform：

* 使用[!DNL Oracle NetSuite Activities]來源來擷取事件資料。
* 使用[!DNL Oracle NetSuite Entities]來源來擷取客戶和連絡人資料。

檢視下表，以取得兩個[!DNL Oracle NetSuite]來源的詳細資訊。

| 來源 | 類型 | 說明 |
| --- | --- | --- |
| [[!DNL Oracle NetSuite Activities]](#oracle-netsuite-activities) | 活動 | 擷取新增到行事曆的排程活動。 |
| [[!DNL Oracle NetSuite Entities]](#oracle-netsuite-entities) | 客戶 | 擷取特定客戶資料，包括客戶名稱、地址和關鍵識別碼等詳細資訊。 |
| [[!DNL Oracle NetSuite Entities]](#oracle-netsuite-entities) | 連絡人 | 擷取聯絡人姓名、電子郵件、電話號碼，以及與客戶相關聯的任何自訂聯絡人相關欄位。 |

## IP位址允許清單 {#ip-allow-list}

使用來源聯結器之前，可能需要將IP位址清單新增至允許清單。 未能將您區域特定的IP位址新增到允許清單可能會導致使用來源時的錯誤或效能不佳。 如需詳細資訊，請參閱[IP位址允許清單](../../ip-address-allow-list.md)頁面。

## 先決條件 {#prerequisites}

在將[!DNL Oracle NetSuite]資料帶入Experience Platform之前，您必須先確定您有以下專案：

* **一個[!DNL Oracle NetSuite]帳戶**。
   * 如果您還沒有有效的帳戶，請連絡[[!DNL Oracle NetSuite]](https://www.NetSuite.com/portal/company/contactus.shtml)。
* 任何[!DNL Oracle NetSuite]產品的&#x200B;**使用中訂閱**。
* **帳戶識別碼**。
   * [!DNL Oracle NetSuite]來源使用OAuth 2.0與[!DNL Oracle NetSuite] API通訊。 如果您沒有帳戶ID，請瀏覽[上的[!DNL Oracle]檔案，瞭解如何擷取帳戶ID](https://docs.oracle.com/en/cloud/saas/netsuite/ns-online-help/section_1498754928.html#Finding-Your-NetSuite-Account-ID)。
* **使用者端識別碼**&#x200B;和&#x200B;**使用者端密碼**&#x200B;組合。
   * 需要使用者端識別碼和使用者端密碼才能存取[!DNL Oracle NetSuite] API。 在此步驟中，您也必須確保管理員具備：
      * 啟用OAuth 2.0功能並設定適當的OAuth 2.0角色。
      * 將使用者指派給OAuth 2.0角色並建立必要的整合記錄。
* **存取權杖**&#x200B;和&#x200B;**重新整理權杖**。
   * 請參閱[OAuth 2.0授權代碼授權流程](https://docs.oracle.com/en/cloud/saas/netsuite/ns-online-help/section_158074210415.html#OAuth-2.0-Authorization-Code-Grant-Flow)上的[!DNL Oracle]指南，瞭解如何產生存取和重新整理Token。

### 收集必要的認證 {#gather-credentials}

為了將[!DNL Oracle NetSuite]連線到Platform，您必須提供下列連線屬性的值：

| 認證 | 說明 | 範例 |
| --- | --- | --- |
| 用戶端 ID | 您在[!DNL Oracle NetSuite]中建立整合記錄時所產生的使用者端ID值。 如需詳細資訊，請參閱如何[建立整合記錄](https://docs.oracle.com/en/cloud/saas/netsuite/ns-online-help/section_157771733782.html#procedure_157838925981)的[!DNL Oracle]指南。 | `7fce.....b42f`<br>值是64個字元的字串。 |
| 用戶端密碼 | 建立整合記錄時產生的使用者端密碼值。 如需詳細資訊，請參閱如何[建立整合記錄](https://docs.oracle.com/en/cloud/saas/netsuite/ns-online-help/section_157771733782.html#procedure_157838925981)的[!DNL Oracle]指南。 | `5c98.....1b46`<br>值是64個字元的字串。 |
| 授權測試URL | （選用）您的[!DNL NetSuite]授權測試URL。 | `https://{ACCOUNT_ID}.app.netsuite.com<br>/app/login/oauth2/authorize.nl?response_type=code<br>&redirect_uri=https%3A%2F%2Fapi.github.com<br>&scope=rest_webservices<br>&state=ykv2XLx1BpT5Q0F3MRPHb94j<br>&client_id={CLIENT_ID}` |
| 存取權杖 | 存取權杖為JSON Web權杖(JWT)格式，僅有效60分鐘。 如需如何擷取存取權杖的詳細資訊，請參閱[NetSuite的OAuth 2.0授權](https://docs.oracle.com/en/cloud/saas/netsuite/ns-online-help/section_158081952044.html#Step-Two-POST-Request-to-the-Token-Endpoint)上的[!DNL Oracle]指南。 | `eyJr......f4V0`<br>值是1024個字元的字串，格式為JSON Web權杖(JWT)。 |
| 重新整理權杖 | 在存取權杖過期後，使用重新整理來產生新的存取權杖。 重新整理權杖的有效期為七天。 如需如何擷取存取權杖的詳細資訊，請參閱[NetSuite的OAuth 2.0授權](https://docs.oracle.com/en/cloud/saas/netsuite/ns-online-help/section_158081952044.html#Step-Two-POST-Request-to-the-Token-Endpoint)上的[!DNL Oracle]指南。 | `eyJr......dmxM`<br>值是1024個字元的字串，格式為JSON Web權杖(JWT)。 |
| 存取記號URL | 應用程式傳送POST要求的目的地權杖端點。 | `https://{ACCOUNT_ID}.suitetalk.api.netsuite.com<br>/services/rest/auth/oauth2/v1/token` |

>[!IMPORTANT]
>
>重新整理Token過期後，您必須使用更新的Token以Experience Platform方式建立新帳戶。

## 將[!DNL Oracle NetSuite Activities]連線至平台 {#oracle-netsuite-activities}

以下檔案提供如何使用API或使用者介面將[!DNL Oracle NetSuite Activities]連線到Platform的資訊：

* [使用API建立來源連線和資料流，將 [!DNL Oracle NetSuite Activities] 資料帶入Platform](../../tutorials/api/create/marketing-automation/oracle-netsuite-activities.md)。
* [使用UI](../../tutorials/ui/create/marketing-automation/oracle-netsuite-activities.md)連線您的 [!DNL Oracle NetSuite Activities] 帳戶以Experience Platform。
* [使用UI](../../tutorials/ui/dataflow/marketing-automation.md)為來源連線建立資料流。

## 將[!DNL Oracle NetSuite Entities]連線至平台 {#oracle-netsuite-entities}

以下檔案提供如何使用API或使用者介面將[!DNL Oracle NetSuite Entities]連線到Platform的資訊：

* [使用API建立來源連線和資料流，將 [!DNL Oracle NetSuite Entities] 資料帶入Platform](../../tutorials/api/create/marketing-automation/oracle-netsuite-entities.md)。
* [使用UI](../../tutorials/ui/create/marketing-automation/oracle-netsuite-entities.md)連線您的 [!DNL Oracle NetSuite Entities] 帳戶以Experience Platform。
* [使用UI](../../tutorials/ui/dataflow/marketing-automation.md)為來源連線建立資料流。
