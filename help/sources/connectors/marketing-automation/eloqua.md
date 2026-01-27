---
title: Oracle Eloqua (V2) Source概觀
description: 瞭解如何將Oracle Eloqua連結至Adobe Experience Platform。
source-git-commit: 180754969d4ae8dbd1308dfc85dae73baf64f759
workflow-type: tm+mt
source-wordcount: '1824'
ht-degree: 2%

---

# [!DNL Oracle Eloqua] (V2)來源概觀

>[!IMPORTANT]
>
>自2026年1月起，已棄用原始[[!DNL Oracle Eloqua] (V1)](oracle-eloqua.md)來源。 這個已棄用的來源沒有可用的移轉，您必須使用新的[!DNL Oracle Eloqua] (V2)來源重新實作您的資料。

[!DNL Oracle Eloqua]是功能強大、企業級行銷自動化平台，主要在B2B領域協助組織，自動化並個人化管理銷售機會與協調購買者歷程的複雜流程。 它是行銷團隊可以跨多個數位頻道定義、部署和衡量複雜行銷活動的中央樞紐，確保潛在客戶在最參與的確切時刻收到正確的內容。 透過[!DNL Eloqua]擷取的支援物件為&#x200B;**連絡人**、**帳戶**、**行銷活動**&#x200B;和&#x200B;**活動**。 完成初始內嵌後，所有變更的資料都會使用排程的增量程式匯入。

您可以使用[!DNL Eloqua]來源將您的[!DNL Eloqua]帳戶連線至Adobe Experience Platform。 請閱讀以下檔案，瞭解如何開始使用。

## 使用案例範例 {#use-case-examples}

下表概述[!DNL Eloqua] (V2)與Adobe Experience Platform整合所支援的行銷物件。 對於每個物件，您將會找到說明以及範例使用案例，以說明將[!DNL Eloqua]資料與Real-Time CDP整合如何能夠提升行銷成效和促銷活動成果。

| 物件 | 說明 | 使用案例範例 |
| --- | --- | --- |
| 聯絡人 | 將連絡人資料（例如姓名、電子郵件、電話號碼、職稱）擷取至Real-Time CDP，建立詳細的統一客戶設定檔，以整合與每個個別連絡人的所有互動和參與。 | **行銷活動最佳化：**&#x200B;透過整合[!DNL Eloqua]的聯絡資料，您的行銷團隊可以根據最近的活動，例如電子郵件開啟、表單提交和事件註冊，來識別高優先順序的潛在客戶。 Real-Time CDP可全方位檢視每位連絡人在電子郵件、網站和其他行銷接觸點中的行為，讓行銷團隊量身打造行銷活動並最佳化訊息，以提高參與度和轉換率。 |
| 帳戶 | 內嵌帳戶層級資料（例如公司名稱、產業、公司規模、收入、位置）以在Real-Time CDP中建立以帳戶為基礎的行銷(ABM)策略，讓您的團隊透過相關訊息鎖定目標並與正確的組織互動。 | **ABM行銷活動：**&#x200B;整合來自[!DNL Eloqua]的帳戶資料有助於建置目標性ABM行銷活動。 例如，軟體公司可使用帳戶資料來細分並傳送自訂電子郵件促銷活動給金融領域公司的決策者，以促銷為其產業量身打造的新解決方案。 |
| 行銷活動 | 將行銷活動資料（例如行銷活動名稱、型別、目標、開啟率等績效量度、CTR）擷取至Real-Time CDP，以追蹤並最佳化多個管道中的行銷活動績效。 使用這些資料來評估投資報酬率，並調整您的策略。 | **跨管道歸因：**&#x200B;如果[!DNL Eloqua]將行銷活動資料傳送至Real-Time CDP，行銷團隊可以檢視跨不同管道（電子郵件、社群媒體、廣告等）的行銷活動績效、將轉換歸因到正確的接觸點，以及根據該insight調整未來策略。 |
| 活動 | 擷取活動資料（例如電子郵件開啟、點按、網站造訪、表單提交、網路研討會出席情況）以追蹤不同管道的即時行為和聯絡人，創造即時個人化參與的機會。 | **即時培養：**&#x200B;透過整合[!DNL Eloqua]中的活動資料，當連絡人參與內容（例如下載白皮書或按一下電子郵件連結）時，Real-Time CDP可以觸發個人化電子郵件或通知給銷售團隊，以便及時跟進及提供更好的轉換機會。 |

{style="table-layout:auto"}

## 先決條件 {#prerequisites}

請閱讀以下章節，瞭解在將來源連線至Experience Platform之前，必須完成的先決條件設定。

### 設定驗證的應用程式

請依照下列步驟，瞭解如何設定您的[!DNL Eloqua]帳戶，並使用基本驗證連線至Experience Platform。

若要開始使用，請以管理員（或有權建立使用者、安全性群組和應用程式的使用者）身分登入您的[!DNL Eloqua]執行個體。

![我的Eloqua儀表板。](../../images/tutorials/create/eloqua/admin.png)

瀏覽至&#x200B;**設定** > **平台擴充功能** > **應用程式雲端開發人員** > **建立應用程式**。 提供您應用程式的詳細資料，包括其名稱、說明、圖示和OAuth回呼URL。 完成時選取&#x200B;**儲存**。

![&#x200B; Eloqua儀表板中的「應用程式開發人員」面板和「建立應用程式」按鈕。](../../images/tutorials/create/eloqua/create-app.png)

| 屬性 | 說明 |
| --- | --- |
| 名稱 | 應用程式的名稱。 |
| 說明 | 應用程式的簡短說明。 |
| 圖示 | 圖示的URL。 |
| OAuth回呼URL | 安裝應用程式並透過[!DNL Eloqua]驗證後，使用者應該重新導向的URL。 |

![在Eloqua中建立應用程式視窗。](../../images/tutorials/create/eloqua/new-app.png)

建立您的應用程式後，瀏覽至[!DNL Authentication to Eloqua]，並從新建立的應用程式中擷取&#x200B;**使用者端識別碼**&#x200B;和&#x200B;**使用者端密碼**。 這些值將在稍後連線到Experience Platform時使用。

![Eloqua中的使用者端識別碼與使用者端密碼。](../../images/tutorials/create/eloqua/credentials.png)

安全性群組可讓管理員控制使用者對資產、功能、介面等擁有的存取層級。 若要建立安全性群組，請瀏覽至&#x200B;**設定** > **使用者**。 接著，選取左側面板上的&#x200B;**群組**&#x200B;索引標籤，然後選取&#x200B;**建立新的安全性群組**。

![Eloqua中的使用者管理儀表板。](../../images/tutorials/create/eloqua/user-management.png)

使用&#x200B;**[!DNL Security Group Overview]**&#x200B;視窗提供安全性群組的名稱和縮寫。 建立後，瀏覽至[!DNL Action Permissions]並從清單中新增[!DNL Consume] API許可權，然後選取&#x200B;**儲存**。

![Eloqua中的安全性群組概觀視窗。](../../images/tutorials/create/eloqua/security-group-overview.png)

![使用API的選擇視窗](../../images/tutorials/create/eloqua/consume-api.png)

>[!NOTE]
>
>[!DNL Consume] API為必要許可權，但您可以根據應用程式的使用情況新增更多許可權。

若要擷取行銷活動資料，請導覽至&#x200B;**編輯使用者**&#x200B;介面，並將[!DNL Guided Campaigns]新增至您選取的安全性群組。

![已新增具有引導式行銷活動的安全性群組。](../../images/tutorials/create/eloqua/add-guided-campaigns.png)

您可以選擇建立其他使用者，並將該使用者新增至安全性群組。 如需詳細步驟，請閱讀有關[!DNL Eloqua]建立使用者[和](https://docs.oracle.com/en/cloud/saas/marketing/eloqua-user/Help/UserManagement/Tasks/CreatingIndividualUsers.htm)將使用者指派給安全性群組[的](https://docs.oracle.com/en/cloud/saas/marketing/eloqua-user/Help/SecurityGroups/Tasks/AddingUsersToSecurityGroups.htm)檔案。

### 收集必要的認證

您必須提供下列認證的值，才能將[!DNL Eloqua]連線至Experience Platform。

| 認證 | 說明 |
| --- | --- |
| 用戶端 ID | 授權Experience Platform時，[!DNL Eloqua]用來識別您帳戶的公開識別碼。 |
| 用戶端密碼 | 只有使用者端應用程式和授權伺服器才知道的機密金鑰。 使用者端ID需要搭配此金鑰才能驗證您的帳戶。 |
| 使用者名稱 | 與您的[!DNL Eloqua]帳戶相關聯的使用者名稱。 這可用來驗證及授權您的存取權。 使用者名稱格式為`CompanyName\Username`。 |
| 密碼 | 與您的[!DNL Eloqua]帳戶關聯的密碼。 除了您的使用者名稱之外，它還會授予您Eloqua環境的存取權。 |
| 基底端點 | [!DNL Eloqua]的驗證基底URI的前置詞。 驗證時，基底端點不應該包含`http://`或`https://`。 |

## [!DNL Eloqua]對應指南

>[!NOTE]
>
>以下是內部用於增量資料載入的差異欄位：
>
>- **連絡人：** `C_DateModified`
>- **帳戶：** `M_DateModified`
>- **活動：** `CreatedAt`
>- **自訂物件：** `UpdatedAt`
>- **行銷活動：** `updatedAt`

下表提供[!DNL Eloqua]來源欄位與Experience Platform中其對應的Experience Data Model (XDM)目的地欄位之間的詳細對應。 每一列概述轉換邏輯、欄位是否不可變，並提供其他附註以幫助您瞭解如何在Experience Platform中擷取和建構您的[!DNL Eloqua]資料。

### 帳戶

| Eloqua Source欄 | XDM目的地路徑 | 附註 |
| --- | --- | --- |
| `"Eloqua"` | accountKey.sourceType | 此欄位一律設定為固定值「Eloqua」。 |
| `"${SOURCE_INSTANCE_ID}"` | accountKey.sourceInstanceID | `SOURCE_INSTANCE_ID`將自動由聯結器取代。 |
| `Id` | accountKey.sourceID | |
| `concat(Id, "\\@${SOURCE_INSTANCE_ID}.Eloqua")` | accountKey.sourceKey | `SOURCE_INSTANCE_ID`將自動由聯結器取代。 |
| `M_CompanyName` | 帳戶名稱 | |
| `M_Country` | accountPhysicalAddress.country | |
| `M_Address1` | accountPhysicalAddress.street1 | |
| `M_City` | accountPhysicalAddress.city | |
| `M_State_Prov` | accountPhysicalAddress.stateProvince | |
| `M_Zip_Postal` | accountPhysicalAddress.postalCode | |
| `M_BusPhone` | accountPhone.number | |
| `M_Fax1` | accountFax.number | |
| `M_Account_Engagement_Score` | accountscore | |
| `M_Account_Type1` | 帳戶型別 | |
| `M_Wesbsite1` | accountOrganization.website | |
| `M_Employees1` | accountOrganization.numberOfEmployees | |
| `to_decimal(M_Annual_Revenue1)` | accountOrganization.annualRevenue.amount | |
| `M_DateModified` | extSourceSystemAudit.lastUpdatedDate | |
| `M_DateCreated` | extSourceSystemAudit.createdDate | |
| `M_Industry1` | accountOrganization.industry | |
| `iif(M_SFDCAccountID != null && M_SFDCAccountID != "", to_object("sourceType", "Salesforce", "sourceInstanceID", "${CRM_INSTANCE_ID}", "sourceID", M_SFDCAccountID, "sourceKey", concat(M_SFDCAccountID, "\\@${CRM_INSTANCE_ID}.Salesforce")), iif(M_MSCRMAccountID != null && M_MSCRMAccountID != "", to_object("sourceType", "Dynamics", "sourceInstanceID", "${CRM_INSTANCE_ID}", "sourceID", M_MSCRMAccountID, "sourceKey", concat(M_MSCRMAccountID, "\\@${CRM_INSTANCE_ID}.Dynamics")), null))` | extSourceSystemAudit.externalKey | 聯結器無法自動偵測您的CRM執行個體ID。 您必須手動將`${CRM_INSTANCE_ID}`取代為您的實際CRM執行個體ID (您的Salesforce或Dynamics執行個體ID)。 在內嵌期間，如果存在`M_SFDCAccountID`，聯結器將使用該值產生外部金鑰並附加`\@CRM_INSTANCE_ID.Salesforce`。 如果該欄位為空，聯結器將使用`M_MSCRMAccountID`並改為附加`\@CRM_INSTANCE_ID.Dynamics`。 如果兩個欄位都為空，此欄位將設定為Null。 |

{style="table-layout:auto"}

### 活動

| Eloqua Source欄 | XDM目的地路徑 | 附註 |
| --- | --- | --- |
| `"Eloqua"` | personKey.sourceType | 此欄位一律設定為固定值「Eloqua」。 |
| `"${SOURCE_INSTANCE_ID}"` | personKey.sourceInstanceID | `SOURCE_INSTANCE_ID`將自動由聯結器取代。 |
| `ContactId` | personKey.sourceID |  |
| `concat(ContactId, "\\@${SOURCE_INSTANCE_ID}.Eloqua")` | personKey.sourceKey | `SOURCE_INSTANCE_ID`將自動由聯結器取代。 |
| `ExternalId` | _id |  |
| `iif(ActivityType!=null && ActivityType!="", iif(ActivityType=="EmailSend", "directMarketing.emailSent", iif(ActivityType=="EmailOpen", "directMarketing.emailOpened", iif(ActivityType=="EmailClickthrough", "directMarketing.emailClicked", iif(ActivityType=="Unsubscribe", "directMarketing.emailUnsubscribed", iif(ActivityType=="Bounceback", "directMarketing.emailBounced", iif(ActivityType=="FormSubmit", "web.formFilledOut", iif(ActivityType=="PageView", "web.webpagedetails.pageViews", ActivityType))))))), null)` | eventType | 系統會根據ActivityType填入對應的Experience Platform eventType值。 對於ExternalActivities，Experience Platform中沒有eventType。 您可以修改此對應以處理更多型別。 |
| `ActivityDate` | 時間戳記 | |
| `iif(AssetType == "Email", AssetName, null)` | directMarketing.mailingName | |
| `iif(AssetType == "Email", to_object("sourceType", "Eloqua", "sourceInstanceID", "${SOURCE_INSTANCE_ID}","sourceID",${AssetId}, "sourceKey", concat(${AssetId},"\\@${SOURCE_INSTANCE_ID}.Eloqua")), null)` | directMarketing.mailingKey | `SOURCE_INSTANCE_ID`將自動由聯結器取代。 |
| `iif(AssetType == "Email", EmailAddress, null)` | directMarketing.email | |
| `iif(ActivityType == "Bounceback", SmtpStatusCode, null)` | directMarketing.emailBouncedCode | |
| `iif(AssetType == "Email", SmtpMessage, null)` | directMarketing.emailBouncedDetails | |
| `iif(AssetType == "Email", EmailWebLink, null)` | directMarketing.linkURL | |
| `iif(ActivityType == "FormSubmit", AssetName, null)` | web.fillOutForm.webFormName | |
| `iif(ActivityType == "FormSubmit", to_object("sourceType", "Eloqua", "sourceInstanceID", "${SOURCE_INSTANCE_ID}","sourceID",${AssetId}, "sourceKey", concat(${AssetId},"\\@${SOURCE_INSTANCE_ID}.Eloqua")), null)` | web.fillOutForm.webFormKey | `SOURCE_INSTANCE_ID`將自動由聯結器取代。 |
| `iif(ActivityType == "PageView", AssetName, null)` | web.webPageDetails.name | |
| `iif(ActivityType == "PageView", to_object("sourceType", "Eloqua", "sourceInstanceID", "${SOURCE_INSTANCE_ID}","sourceID",${AssetId}, "sourceKey", concat(${AssetId},"\\@${SOURCE_INSTANCE_ID}.Eloqua")), null)` | web.webPageDetails.webPageKey | `SOURCE_INSTANCE_ID`將自動由聯結器取代。 |
| `iif(ActivityType == "PageView", Url, null)` | web.webPageDetails.URL | |

{style="table-layout:auto"}

### 行銷活動

| Eloqua Source欄 | XDM目的地路徑 | 附註 |
| --- | --- | --- |
| `"Eloqua"` | campaignKey.sourceType | 此欄位一律設定為固定值「Eloqua」。 |
| `"${SOURCE_INSTANCE_ID}"` | campaignKey.sourceInstanceID | `SOURCE_INSTANCE_ID`將自動由聯結器取代。 |
| `id` | campaignKey.sourceID | |
| `concat(id, "\\@${SOURCE_INSTANCE_ID}.Eloqua")` | campaignKey.sourceKey | `SOURCE_INSTANCE_ID`將自動由聯結器取代。 |
| `name` | campaignName | |
| `endAt` | campaignEndDate | |
| `startAt` | campaignStartDate | |
| `actualCost` | actualCost.amount | |
| `budgetedCost` | budgetedCost.amount | |
| `description` | campaignDescription | |
| `currentStatus` | campaignStates | |
| `campaignType` | campaignType | |
| `createdAt` | extSourceSystemAudit.createdDate | |
| `updatedAt` | extSourceSystemAudit.lastUpdatedDate | |

{style="table-layout:auto"}

### 聯絡人

| Eloqua Source欄 | XDM目的地路徑 | 附註 |
| --- | --- | --- |
| `"Eloqua"` | b2b.personKey.sourceType | 此欄位一律設定為固定值「Eloqua」。 |
| `"${SOURCE_INSTANCE_ID}"` | b2b.personKey.sourceInstanceID | `SOURCE_INSTANCE_ID`將自動由聯結器取代。 |
| `Id` | b2b.personKey.sourceID |  |
| `concat(Id, "\\@${SOURCE_INSTANCE_ID}.Eloqua"` | b2b.personKey.sourceKey | `SOURCE_INSTANCE_ID`將自動由聯結器取代。 |
| `C_Company` | b2b.companyName |  |
| `C_Website1` | b2b.companyWebsite |  |
| `C_Job_Title1` | extendedWorkDetails.jobTitle |  |
| `C_Fax` | faxPhone.number |  |
| `C_MobilePhone` | mobilePhone.number |  |
| `iif(C_SFDCLeadID != null && C_SFDCLeadID != "\\", to_object("sourceType", "Salesforce", "sourceInstanceID", "${CRM_INSTANCE_ID}", "sourceID", C_SFDCLeadID, "sourceKey", concat(C_SFDCLeadID, "\\@${CRM_INSTANCE_ID}.Salesforce")), iif(C_SFDCContactID != null && C_SFDCContactID != "\\", to_object("sourceType", "Salesforce", "sourceInstanceID", "${CRM_INSTANCE_ID}", "sourceID", C_SFDCContactID, "sourceKey", concat(C_SFDCContactID, "\\@${CRM_INSTANCE_ID}.Salesforce")), null))` | personComponents.sourceExternalKey | 如果[!DNL Eloqua]執行個體已與Salesforce同步，則請保留此對應。 否則，請將其移除。 聯結器無法判斷CRM_INSTANCE_ID，因此您必須使用同步的Salesforce執行個體識別碼取代${CRM_INSTANCE_ID}。 相同的對應適用於personComponents和extSourceSystemAudit，因此請保留兩者。 |
| `iif(C_MSCRMLeadID != null && C_MSCRMLeadID != "\\", to_object("sourceType", "Dynamics", "sourceInstanceID", "${CRM_INSTANCE_ID}", "sourceID", C_MSCRMLeadID, "sourceKey", concat(C_MSCRMLeadID, "\\@${CRM_INSTANCE_ID}.Dynamics")), iif(C_MSCRMContactID != null && C_MSCRMContactID != "\\", to_object("sourceType", "Dynamics", "sourceInstanceID", "${CRM_INSTANCE_ID}", "sourceID", C_MSCRMContactID, "sourceKey", concat(C_MSCRMContactID, "\\@${CRM_INSTANCE_ID}.Dynamics")), null))"` | personComponents.sourceExternalKey | 如果[!DNL Eloqua]執行個體已與Dynamics同步，則請保留此對應。 否則，請將其移除。 聯結器無法判斷CRM_INSTANCE_ID，因此您必須將${CRM_INSTANCE_ID}取代為您同步的Dynamics執行個體識別碼。 相同的對應適用於personComponents和extSourceSystemAudit，因此請保留兩者。 |
| `iif(C_SFDCLeadID != null && C_SFDCLeadID != "\\", to_object("sourceType", "Salesforce", "sourceInstanceID", "${CRM_INSTANCE_ID}", "sourceID", C_SFDCLeadID, "sourceKey", concat(C_SFDCLeadID, "\\@${CRM_INSTANCE_ID}.Salesforce")), iif(C_SFDCContactID != null && C_SFDCContactID != "\\", to_object("sourceType", "Salesforce", "sourceInstanceID", "${CRM_INSTANCE_ID}", "sourceID", C_SFDCContactID, "sourceKey", concat(C_SFDCContactID, "\\@${CRM_INSTANCE_ID}.Salesforce")), null))"` | extSourceSystemAudit.externalKey | 如果[!DNL Eloqua]執行個體已與Salesforce同步，則請保留此對應。 否則，請將其移除。 聯結器無法判斷CRM_INSTANCE_ID，因此您必須使用同步的Salesforce執行個體識別碼取代${CRM_INSTANCE_ID}。 相同的對應適用於personComponents和extSourceSystemAudit，因此請保留兩者。 |
| `iif(C_MSCRMLeadID != null && C_MSCRMLeadID != "\\", to_object("sourceType", "Dynamics", "sourceInstanceID", "${CRM_INSTANCE_ID}", "sourceID", C_MSCRMLeadID, "sourceKey", concat(C_MSCRMLeadID, "\\@${CRM_INSTANCE_ID}.Dynamics")), iif(C_MSCRMContactID != null && C_MSCRMContactID != "\\", to_object("sourceType", "Dynamics", "sourceInstanceID", "${CRM_INSTANCE_ID}", "sourceID", C_MSCRMContactID, "sourceKey", concat(C_MSCRMContactID, "\\@${CRM_INSTANCE_ID}.Dynamics")), null))` | extSourceSystemAudit.externalKey | 如果[!DNL Eloqua]執行個體已與Dynamics同步，則請保留此對應。 否則，請將其移除。 聯結器無法判斷CRM_INSTANCE_ID，因此您必須將${CRM_INSTANCE_ID}取代為您同步的Dynamics執行個體識別碼。 相同的對應適用於personComponents和extSourceSystemAudit，因此請保留兩者。 |
| `C_DateCreated` | extSourceSystemAudit.createdDate |  |
| `C_DateModified` | extSourceSystemAudit.lastUpdatedDate |  |
| `iif(C_SFDCAccountID != null && C_SFDCAccountID != "\\", to_object("sourceType", "Salesforce", "sourceInstanceID", "${CRM_INSTANCE_ID}", "sourceID", C_SFDCAccountID, "sourceKey", concat(C_SFDCAccountID, "\\@${CRM_INSTANCE_ID}.Salesforce")), iif(C_MSCRMAccountID != null && C_MSCRMAccountID != "\\", to_object("sourceType", "Dynamics", "sourceInstanceID", "${CRM_INSTANCE_ID}", "sourceID", C_MSCRMAccountID, "sourceKey", concat(C_MSCRMAccountID, "\\@${CRM_INSTANCE_ID}.Dynamics")), null))` | b2b.accountKey | 聯結器無法判斷CRM_INSTANCE_ID，因此您必須將${CRM_INSTANCE_ID}取代為您同步的CRM執行個體ID (Salesforce執行個體ID或Dynamics執行個體ID)。 相同的對應同時適用於b2b.accountKey和personComponents.sourceAccountKey，因此請保留兩者。 |
| `iif(C_SFDCAccountID != null && C_SFDCAccountID != "\\", to_object("sourceType", "Salesforce", "sourceInstanceID", "${CRM_INSTANCE_ID}", "sourceID", C_SFDCAccountID, "sourceKey", concat(C_SFDCAccountID, "\\@${CRM_INSTANCE_ID}.Salesforce")), iif(C_MSCRMAccountID != null && C_MSCRMAccountID != "\\", to_object("sourceType", "Dynamics", "sourceInstanceID", "${CRM_INSTANCE_ID}", "sourceID", C_MSCRMAccountID, "sourceKey", concat(C_MSCRMAccountID, "\\@${CRM_INSTANCE_ID}.Dynamics")), null))` | personComponents.sourceAccountKey | 聯結器無法判斷CRM_INSTANCE_ID，因此您必須將${CRM_INSTANCE_ID}取代為您同步的CRM執行個體ID (Salesforce執行個體ID或Dynamics執行個體ID)。 相同的對應同時適用於b2b.accountKey和personComponents.sourceAccountKey，因此請保留兩者。 |
| `C_Lead_Source___Original1` | b2b.personSource | |
| `C_Lead_Source___Original1` | personComponents.personSource | |
| `C_Lead_Status1` | b2b.personStatus | |
| `C_Lead_Status1` | personComponents.personStatus | |
| `C_FirstName` | person.name.firstName | |
| `C_LastName` | person.name.lastName | |
| `C_Middle_Name1` | person.name.middleName | |
| `C_Salutation` | person.name.courtesyTitle | |
| `C_City` | workAddress.city | |
| `C_Country` | workAddress.country | |
| `C_Zip_Postal` | workAddress.postalCode | |
| `C_State_Prov` | workAddress.state | |

{style="table-layout:auto"}

### 活動型別對應參考

| Eloqua ActivityType | XDM eventType |
| -------------------- | --------------- |
| `EmailSend` | directMarketing.emailSent |
| `EmailOpen` | directMarketing.emailOpened |
| `EmailClickthrough` | directMarketing.emailClicked |
| `Unsubscribe` | directMarketing.emailUnsubscribed |
| `Bounceback` | directMarketing.emailBounced |
| `FormSubmit` | web.formFilledOut |
| `PageView` | web.webpagedetails.pageViews |
| `Other` | 按原樣傳遞 |

{style="table-layout:auto"}

### 變數預留位置

對應範本使用下列變數預留位置，這些預留位置在資料流執行後會被取代：

| 預留位置 | 說明 | 使用方式 |
| ----------- | ----------- | ----- |
| `${SOURCE_INSTANCE_ID}` | Eloqua來源例項的唯一ID | 用於來源索引鍵 |
| `${CRM_INSTANCE_ID}` | CRM系統(Salesforce/Dynamics)的唯一ID | 用於外部金鑰 |

## 將[!DNL Eloqua]連線至Experience Platform

繼續在Experience Platform中設定您的[!DNL Eloqua]來源連線。 如需透過UI設定連線的逐步指南，請參閱這裡的[教學課程](../../tutorials/ui/create/marketing-automation/eloqua.md)。 閱讀本教學課程，瞭解如何連線您的[!DNL Eloqua]帳戶、選取資料、對應欄位、排程內嵌及監視資料流程。

