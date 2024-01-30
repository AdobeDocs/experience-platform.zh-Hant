---
title: oracleNetSuite來源概觀
description: 瞭解如何使用API或使用者介面將OracleNetSuite連線至Adobe Experience Platform。
last-substantial-update: 2024-01-30T00:00:00Z
badge: Beta
source-git-commit: 632cff3ee4ca82d391e9a1df0cb38d903e8a5428
workflow-type: tm+mt
source-wordcount: '748'
ht-degree: 1%

---

# [!DNL Oracle NetSuite]

>[!NOTE]
>
>此 [!DNL Oracle NetSuite] 來源為測試版。 請閱讀 [來源概觀](../../home.md#terms-and-conditions) 以取得有關使用測試版標籤來源的詳細資訊。

Adobe Experience Platform可讓您從外部來源擷取資料，同時使用Platform服務來建構、加標籤及增強傳入資料。 您可以從多種來源(例如Adobe應用程式、雲端儲存、資料庫和許多其他來源)內嵌資料。

Experience Platform提供擷取資料協力廠商行銷自動化系統的支援。 對行銷自動化提供者的支援包括 [!DNL Oracle NetSuite].

[[!DNL Oracle NetSuite]](https://www.netsuite.com/) 是雲端型企業管理套件，包含ERP/財務、CRM及電子商務解決方案。

您可以使用兩個不同的來源來擷取資料 [!DNL Oracle NetSuite] 要Experience Platform：

* 使用 [!DNL Oracle NetSuite Activities] 擷取事件資料的來源。
* 使用 [!DNL Oracle NetSuite Entities] 擷取客戶和聯絡資料的來源。

檢視下表，瞭解兩者的詳細資訊 [!DNL Oracle NetSuite] 來源。

| 來源 | 類型 | 說明 |
| --- | --- | --- |
| [[!DNL Oracle NetSuite Activities]](#oracle-netsuite-activities) | 活動 | 擷取新增到行事曆的排程活動。 |
| [[!DNL Oracle NetSuite Entities]](#oracle-netsuite-entities) | 客戶 | 擷取特定客戶資料，包括客戶名稱、地址和關鍵識別碼等詳細資訊。 |
| [[!DNL Oracle NetSuite Entities]](#oracle-netsuite-entities) | 連絡人 | 擷取聯絡人姓名、電子郵件、電話號碼，以及與客戶相關聯的任何自訂聯絡人相關欄位。 |

## IP位址允許清單 {#ip-allow-list}

使用來源聯結器之前，可能需要將IP位址清單新增至允許清單。 未能將您區域特定的IP位址新增到允許清單可能會導致使用來源時的錯誤或效能不佳。 請參閱 [IP位址允許清單](../../ip-address-allow-list.md) 頁面以取得詳細資訊。

## 先決條件 {#prerequisites}

在帶上 [!DNL Oracle NetSuite] 要Experience Platform的資料，您必須先確保您擁有下列專案：

* **一個 [!DNL Oracle NetSuite] 帳戶**.
   * 連絡人 [[!DNL Oracle NetSuite]](https://www.NetSuite.com/portal/company/contactus.shtml) 如果您還沒有有效的帳戶。
* 一個 **使用中的訂閱** 至任何 [!DNL Oracle NetSuite] 產品。
* 一個 **帳戶ID**.
   * 此 [!DNL Oracle NetSuite] 來源使用OAuth 2.0與 [!DNL Oracle NetSuite] API。 如果您沒有帳戶ID，請造訪 [!DNL Oracle] 檔案： [如何擷取您的帳戶ID](https://docs.oracle.com/en/cloud/saas/netsuite/ns-online-help/section_1498754928.html#Finding-Your-NetSuite-Account-ID).
* A **使用者端ID** 和 **使用者端密碼** 組合。
   * 需要使用者端ID和使用者端密碼才能存取 [!DNL Oracle NetSuite] API。 在此步驟中，您也必須確保管理員具備：
      * 啟用OAuth 2.0功能並設定適當的OAuth 2.0角色。
      * 將使用者指派給OAuth 2.0角色並建立必要的整合記錄。
* 一個 **存取權杖** 和 **重新整理權杖**.
   * 請參閱 [!DNL Oracle] 指南： [OAuth 2.0授權代碼授予流程](https://docs.oracle.com/en/cloud/saas/netsuite/ns-online-help/section_158074210415.html#OAuth-2.0-Authorization-Code-Grant-Flow) 以取得有關如何產生存取權和重新整理Token的資訊。

### 收集必要的認證 {#gather-credentials}

為了連線 [!DNL Oracle NetSuite] 至Platform，您必須提供下列連線屬性的值：

| 認證 | 說明 | 範例 |
| --- | --- | --- |
| 使用者端ID | 當您在中建立整合記錄時產生的使用者端ID值 [!DNL Oracle NetSuite]. 閱讀 [!DNL Oracle] 操作方法指南 [建立整合記錄](https://docs.oracle.com/en/cloud/saas/netsuite/ns-online-help/section_157771733782.html#procedure_157838925981) 以取得詳細資訊。 | `7fce.....b42f`<br>值是64個字元的字串。 |
| 使用者端密碼 | 建立整合記錄時產生的使用者端密碼值。 閱讀 [!DNL Oracle] 操作方法指南 [建立整合記錄](https://docs.oracle.com/en/cloud/saas/netsuite/ns-online-help/section_157771733782.html#procedure_157838925981) 以取得詳細資訊。 | `5c98.....1b46`<br>值是64個字元的字串。 |
| 授權測試URL | （可選）您的 [!DNL NetSuite] 授權測試URL。 | `https://{ACCOUNT_ID}.app.netsuite.com<br>/app/login/oauth2/authorize.nl?response_type=code<br>&redirect_uri=https%3A%2F%2Fapi.github.com<br>&scope=rest_webservices<br>&state=ykv2XLx1BpT5Q0F3MRPHb94j<br>&client_id={CLIENT_ID}` |
| 存取權杖 | 存取權杖為JSON Web權杖(JWT)格式，僅有效60分鐘。 如需如何擷取存取Token的詳細資訊，請參閱 [!DNL Oracle] 指南： [NetSuite的OAuth 2.0授權](https://docs.oracle.com/en/cloud/saas/netsuite/ns-online-help/section_158081952044.html#Step-Two-POST-Request-to-the-Token-Endpoint). | `eyJr......f4V0`<br> 此值是格式為JSON Web權杖(JWT)的1024字元字串。 |
| 重新整理Token | 在存取權杖過期後，使用重新整理來產生新的存取權杖。 重新整理權杖的有效期為七天。 如需如何擷取存取Token的詳細資訊，請參閱 [!DNL Oracle] 指南： [NetSuite的OAuth 2.0授權](https://docs.oracle.com/en/cloud/saas/netsuite/ns-online-help/section_158081952044.html#Step-Two-POST-Request-to-the-Token-Endpoint). | `eyJr......dmxM`<br> 此值是格式為JSON Web權杖(JWT)的1024字元字串。 |
| 存取記號URL | 應用程式傳送POST要求的目的地權杖端點。 | `https://{ACCOUNT_ID}.suitetalk.api.netsuite.com<br>/services/rest/auth/oauth2/v1/token` |

>[!IMPORTANT]
>
>重新整理Token過期後，您必須使用更新的Token以Experience Platform方式建立新帳戶。

## 連線 [!DNL Oracle NetSuite Activities] 至平台 {#oracle-netsuite-activities}

以下檔案提供有關如何連線的資訊 [!DNL Oracle NetSuite Activities] 使用API或使用者介面至Platform：

* [建立來源連線和資料流以帶來 [!DNL Oracle NetSuite Activities] 使用API將資料匯入Platform](../../tutorials/api/create/marketing-automation/oracle-netsuite-activities.md).
* [連線您的 [!DNL Oracle NetSuite Activities] 要使用UIExperience Platform的帳戶](../../tutorials/ui/create/marketing-automation/oracle-netsuite-activities.md).
* [使用UI為來源連線建立資料流](../../tutorials/ui/dataflow/marketing-automation.md).

## 連線 [!DNL Oracle NetSuite Entities] 至平台 {#oracle-netsuite-entities}

以下檔案提供有關如何連線的資訊 [!DNL Oracle NetSuite Entities] 使用API或使用者介面至Platform：

* [建立來源連線和資料流以帶來 [!DNL Oracle NetSuite Entities] 使用API將資料匯入Platform](../../tutorials/api/create/marketing-automation/oracle-netsuite-entities.md).
* [連線您的 [!DNL Oracle NetSuite Entities] 要使用UIExperience Platform的帳戶](../../tutorials/ui/create/marketing-automation/oracle-netsuite-entities.md).
* [使用UI為來源連線建立資料流](../../tutorials/ui/dataflow/marketing-automation.md).
