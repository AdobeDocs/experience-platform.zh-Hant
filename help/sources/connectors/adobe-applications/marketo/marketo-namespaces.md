---
keywords: Experience Platform;home；常用主題；Marketo源連接器；命名空間；方案
solution: Experience Platform
title: Marketo命名空間
topic-legacy: overview
description: 本文檔概述了建立Marketo Engage源連接器時所需的自定義命名空間。
exl-id: f1592be5-987e-41b8-9844-9dea5bd452b9
source-git-commit: 609b951cbde880a9f354b343adb1796def0a812c
workflow-type: tm+mt
source-wordcount: '1677'
ht-degree: 4%

---

# （測試版）[!DNL Marketo Engage]名稱空間和結構描述

>[!IMPORTANT]
>
>[!DNL Marketo Engage]來源目前處於測試階段。 功能和說明檔案會有所變更。

本文檔提供有關[!DNL Marketo Engage]（下稱&quot;[!DNL Marketo]&quot;）使用的B2B名稱空間和架構的基礎設定的資訊。 本文檔還提供有關設定生成[!DNL Marketo] B2B名稱空間和架構所需的郵遞員自動化實用程式的詳細資訊。

## 設定[!DNL Marketo]命名空間和模式自動生成實用程式

使用[!DNL Marketo]命名空間和架構自動產生公用程式的第一步是設定您的平台開發人員主控台和[!DNL Postman]環境。

- 您可以從此[GitHub儲存庫](https://github.com/adobe/experience-platform-postman-samples/tree/master/Postman%20Collections/CDP%20Namespaces%20and%20Schemas%20Utility)下載命名空間和架構自動生成實用程式集和環境。
- 如需有關使用平台API的詳細資訊，包括如何收集必要標題值和讀取範例API呼叫的詳細資訊，請參閱[開始使用平台API](../../../../landing/api-guide.md)的指南。
- 如需如何產生平台API認證的詳細資訊，請參閱[驗證及存取Experience PlatformAPI的教學課程](../../../../landing/api-authentication.md)。
- 如需如何為平台API設定[!DNL Postman]的詳細資訊，請參閱[設定開發人員主控台和 [!DNL Postman]](../../../../landing/postman.md)的教學課程。

透過設定平台開發人員主控台和[!DNL Postman]，您現在可以開始將適當的環境值套用至您的[!DNL Postman]環境。

下表包含範例值以及填入[!DNL Postman]環境的其他資訊：

| 變數 | 說明 | 範例 |
| --- | --- | --- |
| `CLIENT_SECRET` | 用於生成`{ACCESS_TOKEN}`的唯一標識符。 有關如何檢索`{CLIENT_SECRET}`的資訊，請參閱[驗證和訪問Experience PlatformAPI](../../../../landing/api-authentication.md)的教程。 | `{CLIENT_SECRET}` |
| `JWT_TOKEN` | JSON Web Token(JWT)是用來產生{ACCESS_TOKEN}的驗證憑證。 有關如何生成`{JWT_TOKEN}`的資訊，請參閱[驗證和訪問Experience PlatformAPI](../../../../landing/api-authentication.md)的教程。 | `{JWT_TOKEN}` |
| `API_KEY` | 用於驗證對Experience PlatformAPI的呼叫的唯一識別碼。 有關如何檢索`{API_KEY}`的資訊，請參閱[驗證和訪問Experience PlatformAPI](../../../../landing/api-authentication.md)的教程。 | `c8d9a2f5c1e03789bd22e8efdd1bdc1b` |
| `ACCESS_TOKEN` | 完成對Experience PlatformAPI的呼叫所需的授權Token。 有關如何檢索`{ACCESS_TOKEN}`的資訊，請參閱[驗證和訪問Experience PlatformAPI](../../../../landing/api-authentication.md)的教程。 | `Bearer {ACCESS_TOKEN}` |
| `META_SCOPE` | 對於[!DNL Marketo]，此值是固定的，一直設定為：`ent_dataservices_sdk`。 | `ent_dataservices_sdk` |
| `CONTAINER_ID` | `global`容器包含所有標準Adobe和Experience Platform夥伴提供的類、方案欄位組、資料類型和方案。 對於[!DNL Marketo]，此值是固定的，且始終設定為`global`。 | `global` |
| `PRIVATE_KEY` | 用於驗證[!DNL Postman]實例以Experience PlatformAPI的憑據。 如需如何擷取{PRIVATE_KEY}的指示，請參閱有關設定開發人員主控台和[設定開發人員主控台和 [!DNL Postman]](../../../../landing/postman.md)的教學課程。 | `{PRIVATE_KEY}` |
| `TECHNICAL_ACCOUNT_ID` | 用於與Adobe I/O整合的憑據。 | `D42AEVJZTTJC6LZADUBVPA15@techacct.adobe.com` |
| `IMS` | Identity Management系統(IMS)為Adobe服務提供認證框架。 對於[!DNL Marketo]，此值是固定的，始終設定為：`ims-na1.adobelogin.com`。 | `ims-na1.adobelogin.com` |
| `IMS_ORG` | 可擁有或授權產品與服務並允許存取其成員的公司實體。 有關如何檢索`{IMS_ORG}`資訊的說明，請參閱[設定開發人員控制台和 [!DNL Postman]](../../../../landing/postman.md)上的教程。 | `ABCEH0D9KX6A7WA7ATQE0TE@adobeOrg` |
| `SANDBOX_NAME` | 您使用的虛擬沙盒分區的名稱。 | `prod` |
| `TENANT_ID` | 用於確保您建立的資源正確命名並包含在IMS組織中的ID。 | `b2bcdpproductiontest` |
| `PLATFORM_URL` | 您對其進行API呼叫的URL端點。 此值是固定的，且始終設定為：`http://platform.adobe.io/`。 | `http://platform.adobe.io/` |
| `munchkinId` | [!DNL Marketo]帳戶的唯一ID。 有關如何檢索`munchkinId`的資訊，請參閱[驗證 [!DNL Marketo] 實例](./marketo-auth.md)的教程。 | `123-ABC-456` |
| `sfdc_org_id` | [!DNL Salesforce]帳戶的組織ID。 有關獲取[!DNL Salesforce]組織ID的詳細資訊，請參閱以下[[!DNL Salesforce] 指南](https://help.salesforce.com/articleView?id=000325251&amp;type=1&amp;mode=1)。 | `00D4W000000FgYJUA0` |
| `msd_org_id` | [!DNL Dynamics]帳戶的組織ID。 有關獲取[!DNL Dynamics]組織ID的詳細資訊，請參閱以下[[!DNL Microsoft Dynamics] 指南](https://docs.microsoft.com/en-us/power-platform/admin/determine-org-id-name)。 | `f6438fab-67e8-4814-a6b5-8c8dcdf7a98f` |
| `has_abm` | 一個布爾值，指示您是否預訂[!DNL Marketo Account-Based Marketing]。 | `false` |
| `has_msi` | 一個布爾值，指示您是否被切換到[!DNL Marketo Sales Insight]。 | `false` |

{style=&quot;table-layout:auto&quot;}

### 運行指令碼

在設定[!DNL Postman]系列和環境後，您現在可以透過[!DNL Postman]介面執行指令碼。

在[!DNL Postman]介面中，選擇自動生成器實用程式的根資料夾，然後從頂部標題中選擇&#x200B;**[!DNL Run]**。

![根資料夾](../images/marketo/root-folder.png)

出現[!DNL Runner]介面。 在此處，確保選中所有複選框，然後選擇&#x200B;**[!DNL Run Adobe I/O Access Token Generation + Automate Namespace creation]**。

![運行生成器](../images/marketo/run-generator.png)

成功的請求會根據測試版規格建立B2B命名空間和結構。

## [!DNL Marketo] 命名空間

身分名稱空間是[[!DNL Identity Service]](../../../../identity-service/home.md)的一個元件，用作身份相關上下文的指示器。

完全限定身份包括ID值和命名空間。 每個新[!DNL Marketo]例項和資料集組合都需要新的自訂命名空間。 例如，[!DNL Marketo]來源連接器收錄`programs`資料集需要其自訂命名空間，而另一個Marketo來源連接器收錄相同資料集也需要其新的自訂命名空間。 如需詳細資訊，請參閱[名稱空間概述](../../../../identity-service/namespaces.md)。

[!DNL Marketo]命名空間用於實體的主要標識。

下表包含有關[!DNL Marketo]名稱空間的基礎設定的資訊。

>[!NOTE]
>
>請向左／向右滾動以查看表的完整內容。

| 顯示名稱 | 身分符號 | 身分類型 | 發行者類型 | 發行者實體類型 | Munchkin ID範例 |
| --- | --- | --- | --- | --- | --- |
| `marketo_person_{MUNCHKIN_ID}` | 自動產生 | `CROSS_DEVICE` | [!DNL Marketo] | `person` | `123-ABC-789` |
| `marketo_company_{MUNCHKIN_ID}` | 自動產生 | `B2B_ACCOUNT` | [!DNL Marketo] | `company` | `123-ABC-789` |
| `marketo_opportunity_{MUNCHKIN_ID}` | 自動產生 | `B2B_OPPORTUNITY` | [!DNL Marketo] | `opportunity` | `123-ABC-789` |
| `marketo_opportunity_contact_role_{MUNCHKIN_ID}` | 自動產生 | `B2B_OPPORTUNITY_PERSON` | [!DNL Marketo] | `opportunity contact role` | `123-ABC-789` |
| `marketo_program_{MUNCHKIN_ID}` | 自動產生 | `B2B_CAMPAIGN` | [!DNL Marketo] | `program` | `123-ABC-789` |
| `marketo_program_member_{MUNCHKIN_ID}` | 自動產生 | `B2B_CAMPAIGN_MEMBER` | [!DNL Marketo] | `program member` | `123-ABC-789` |
| `marketo_static_list_{MUNCHKIN_ID}` | 自動產生 | `B2B_MARKETING_LIST` | [!DNL Marketo] | `static list` | `123-ABC-789` |
| `marketo_static_list_member_{MUNCHKIN_ID}` | 自動產生 | `B2B_MARKETING_LIST_MEMBER` | [!DNL Marketo] | `static list member` | `123-ABC-789` |
| `marketo_named_account_{MUNCHKIN_ID}` | 自動產生 | `B2B_ACCOUNT` | [!DNL Marketo] | `named account` | `123-ABC-789` |

{style=&quot;table-layout:auto&quot;}

### [!DNL Salesforce] 命名空間

如果您訂閱[!DNL Salesforce]整合，則會在實體的次要識別中使用[!DNL Salesforce]命名空間。

下表包含有關[!DNL Salesforce]名稱空間的基礎設定的資訊。

>[!NOTE]
>
>請向左／向右滾動以查看表的完整內容。

| 顯示名稱 | 身分符號 | 身分類型 | 發行者類型 | 發行者實體類型 | [!DNL Salesforce] 訂閱組織ID範例 |
| --- | --- | --- | --- | --- | --- |
| `salesforce_lead_{SALESFORCE_ORGANIZATION_ID}` | 自動產生 | `CROSS_DEVICE` | [!DNL Salesforce] | `lead` | `00DA0000000Hz79` |
| `salesforce_account_{SALESFORCE_ORGANIZATION_ID}` | 自動產生 | `B2B_ACCOUNT` | [!DNL Salesforce] | `account` | `00DA0000000Hz79` |
| `salesforce_opportunity_{SALESFORCE_ORGANIZATION_ID}` | 自動產生 | `B2B_OPPORTUNITY` | [!DNL Salesforce] | `opportunity` | `00DA0000000Hz79` |
| `salesforce_opportunity_contact_role_{SALESFORCE_ORGANIZATION_ID}` | 自動產生 | `B2B_OPPORTUNITY_PERSON` | [!DNL Salesforce] | `opportunity contact role` | `00DA0000000Hz79` |
| `salesforce_campaign_{SALESFORCE_ORGANIZATION_ID}` | 自動產生 | `B2B_CAMPAIGN` | [!DNL Salesforce] | `campaign` | `00DA0000000Hz79` |
| `salesforce_campaign_member_{SALESFORCE_ORGANIZATION_ID}` | 自動產生 | `B2B_CAMPAIGN_MEMBER` | [!DNL Salesforce] | `campaign member` | `00DA0000000Hz79` |

{style=&quot;table-layout:auto&quot;}

### [!DNL Microsoft Dynamics] 命名空間

如果您訂閱[!DNL Dynamics]整合，則[!DNL Dynamics]命名空間會用作實體的次要身分識別。

下表包含有關[!DNL Dynamics]名稱空間的基礎設定的資訊。

>[!NOTE]
>
>請向左／向右滾動以查看表的完整內容。

| 顯示名稱 | 身分符號 | 身分類型 | 發行者類型 | 發行者實體類型 | [!DNL Dynamics] 訂閱組織ID範例 |
| --- | --- | --- | --- | --- | --- |
| `microsoft_person_{DYNAMICS_ID}` | 自動產生 | `CROSS_DEVICE` | [!DNL Microsoft] | `person` | `94cahe38-e51h-3d57-a9c6-2edklb7184mh` |
| `microsoft_account_{DYNAMICS_ID}` | 自動產生 | `B2B_ACCOUNT` | [!DNL Microsoft] | `account` | `94cahe38-e51h-3d57-a9c6-2edklb7184mh` |
| `microsoft_opportunity_{DYNAMICS_ID}` | 自動產生 | `B2B_OPPORTUNITY` | [!DNL Microsoft] | `opportunity` | `94cahe38-e51h-3d57-a9c6-2edklb7184mh` |
| `microsoft_opportunity_contact_connection_{DYNAMICS_ID}` | 自動產生 | `B2B_OPPORTUNITY_PERSON` | [!DNL Microsoft] | `opportunity relationship` | `94cahe38-e51h-3d57-a9c6-2edklb7184mh` |
| `microsoft_campaign_{DYNAMICS_ID}` | 自動產生 | `B2B_CAMPAIGN` | [!DNL Microsoft] | `campaign` | `94cahe38-e51h-3d57-a9c6-2edklb7184mh` |
| `microsoft_campaign_member_{DYNAMICS_ID}` | 自動產生 | `B2B_CAMPAIGN_MEMBER` | [!DNL Microsoft] | `campaign member` | `94cahe38-e51h-3d57-a9c6-2edklb7184mh` |

{style=&quot;table-layout:auto&quot;}

## [!DNL Marketo] 模式

Experience Platform 會使用結構，以一致且可重複使用的方式說明資料結構。藉由定義跨系統的一致資料，將可輕易保留意義，而發揮資料應有的價值。

在將資料引入平台之前，必須構建一個模式來描述資料的結構，並為每個欄位中可包含的資料類型提供約束。 方案由基本類和零個或多個方案欄位組組成。

有關架構構成模型（包括設計原則和最佳實踐）的詳細資訊，請參閱[架構構成基礎](../../../../xdm/schema/composition.md)。

下表包含有關[!DNL Marketo]方案的基礎設定的資訊。

>[!NOTE]
>
>請向左／向右滾動以查看表的完整內容。

| 架構名稱 | 基本類 | 欄位群組 | [!DNL Profile] 在架構中 | 主要身分 | 主要身分名稱空間 | 次要身份 | 次要身分名稱空間 | 關係 | 附註 |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| `[!DNL Marketo] Company {MUNCHKIN_ID}` | XDM業務帳戶 | XDM業務帳戶詳細資訊 | 啟用 | `accountID` 在基本類中 | `marketo_company_{MUNCHKIN_ID}` | `extSourceSystemAudit.externalID` 在基本類中 | `salesforce_account_{SALESFORCE_ORGANIZATION_ID}` | <ul><li>`accountParentID` 在「XDM業務帳戶詳細資訊」欄位組中</li><li>類型：一對一</li><li>參考結構：`[!DNL Marketo] Company {MUNCHKIN_ID}`</li><li>命名空間: `marketo_company_{MUNCHKIN_ID}`</li></ul> |
| `[!DNL Marketo] Person {MUNCHKIN_ID}` | XDM個人資料 | <ul><li>XDM業務人員詳細資訊</li><li>XDM業務人員元件</li><li>IdentityMap</li></ul> | 啟用 | `personID` 在基本類中 | `marketo_person_{MUNCHKIN_ID}` | <ol><li>`extSourceSystemAudit.externalID` XDM業務人員詳細資訊欄位組</li><li>`workEmail.address` XDM業務人員詳細資訊欄位組</li><li>`identityMap` Identity Map欄位群組</ol></li> | <ol><li>`salesforce_lead_{SALESFORCE_ORGANIZATION_ID}`</li><li>電子郵件</li><li>ECID</li></ol> | <ul><li>`personComponents.sourceAccountID` XDM業務人員元件欄位組</li><li>類型：多對一</li><li>參考結構：`[!DNL Marketo] Company {MUNCHKIN_ID}`</li><li>命名空間: `marketo_company_{MUNCHKIN_ID}`</li><li>目標屬性：`accountID`</li><li>當前方案的關係名稱：帳戶</li><li>參考方案中的關係名稱：人物</li></ul> |
| `[!DNL Marketo] Opportunity {MUNCHKIN_ID}` | XDM業務機會 | XDM業務機會詳細資訊 | 啟用 | `opportunityID` 在基本類中 | `marketo_opportunity_{MUNCHKIN_ID}` | `extSourceSystemAudit.externalID` 在基本類中 | `salesforce_opportunity_{SALESFORCE_ORGANIZATION_ID}` | <ul><li>`accountID` 在基本類中</li><li>類型：多對一</li><li>參考結構：`[!DNL Marketo] Company {MUNCHKIN_ID}`</li><li>命名空間: `marketo_company_{MUNCHKIN_ID}`</li><li>目標屬性：`accountID`</li><li>當前方案的關係名稱：帳戶</li><li>參考方案中的關係名稱：機會</li></ul> |
| `[!DNL Marketo] Opportunity Contact Role {MUNCHKIN_ID}` | XDM業務機會人關係 | None | 啟用 | `opportunityPersonID` 在基本類中 | `marketo_opportunity_contact_role_{MUNCHKIN_ID}` | `extSourceSystemAudit.externalID` 在基本類中 | `salesforce_opportunity_contact_role_{SALESFORCE_ORGANIZATION_ID}` | 第一關係<ul><li>`personID` 在基本類中</li><li>類型：多對一</li><li>參考結構：`[!DNL Marketo] Person {MUNCHKIN_ID}`</li><li>命名空間: `marketo_person_{MUNCHKIN_ID}`</li><li>目標屬性：`personID`</li><li>當前方案的關係名稱：人物</li><li>參考方案中的關係名稱：機會</li></ul>第二種關係<ul><li>`opportunityID` 在基本類中</li><li>類型：多對一</li><li>參考結構：`[!DNL Marketo] Opportunity {MUNCHKIN_ID}`</li><li>命名空間: `marketo_opportunity_{MUNCHKIN_ID}`</li><li>目標屬性：`opportunityID`</li><li>當前方案的關係名稱：機會</li><li>參考方案中的關係名稱：人物</li></ul> |
| `[!DNL Marketo] Program {MUNCHKIN_ID}` | XDM Business Campaign | XDM Business Campaign詳細資訊 | 啟用 | `campaignID` 在基本類中 | `marketo_program_{MUNCHKIN_ID}` | `extSourceSystemAudit.externalID` 在基本類中 | `salesforce_campaign_{SALESFORCE_ORGANIZATION_ID}` |
| `[!DNL Marketo] Program Member {MUNCHKIN_ID}` | XDM Business Campaign會員 | XDM Business Campaign成員詳細資訊 | 啟用 | `campaignMemberID` 在基本類中 | `marketo_program_member_{MUNCHKIN_ID}` | 無 | 無 | 第一關係<ul><li>`personID` 在基本類中</li><li>類型：多對一</li><li>參考結構：Marketo人{MUNCHKIN_ID}</li><li>命名空間: `marketo_person_{MUNCHKIN_ID}`</li><li>目標屬性：`personID`</li><li>當前方案的關係名稱：人物</li><li>參考方案中的關係名稱：計畫</li></ul>第二種關係<ul><li>`campaignID` 在基本類中</li><li>類型：多對一</li><li>參考結構：`[!DNL Marketo] Program {MUNCHKIN_ID}`</li><li>命名空間: `marketo_program_{MUNCHKIN_ID}`</li><li>目標屬性：`campaignID`</li><li>當前方案的關係名稱：計畫</li><li>參考方案中的關係名稱：人物</li></ul> |
| `[!DNL Marketo] Static List {MUNCHKIN_ID}` | XDM業務營銷清單 | 無 | 啟用 | `marketingListID` 在基本類中 | `marketo_static_list_{MUNCHKIN_ID}` | 無 | 無 | 無 | 靜態清單與[!DNL Salesforce]不同步，因此沒有次標識。 |
| `[!DNL Marketo] Static List Member {MUNCHKIN_ID}` | XDM Business Marketing List成員 | 無 | 啟用 | `marketingListMemberID` 在基本類中 | `marketo_static_list_member_{MUNCHKIN_ID}` | 無 | 無 | 第一關係<ul><li>`personID` 在基本類中</li><li>類型：多對一</li><li>參考結構：`[!DNL Marketo] Person {MUNCHKIN_ID}`</li><li>命名空間: `marketo_person_{MUNCHKIN_ID}`</li><li>目標屬性：`personID`</li><li>當前方案的關係名稱：人物</li><li>參考方案中的關係名稱：清單</li></ul>第二種關係<ul><li>`marketingListID` 在基本類中</li><li>類型：多對一</li><li>參考結構：`[!DNL Marketo] Static List {MUNCHKIN_ID}`</li><li>命名空間: `marketo_static_list_{MUNCHKIN_ID}`</li><li>目標屬性：`marketingListID`</li><li>當前方案的關係名稱：清單</li><li>參考方案中的關係名稱：人物</li></ul> | 靜態清單成員與[!DNL Salesforce]不同步，因此沒有次標識。 |
| `[!DNL Marketo] Named Account {MUNCHKIN_ID}` | XDM業務帳戶 | XDM業務帳戶詳細資訊 | 啟用 | `accountID` 在基本類中 | `marketo_named_account_{MUNCHKIN_ID}` | `extSourceSystemAudit.externalID` 在基本類中 | `salesforce_account_{SALESFORCE_ORGANIZATION_ID}` | <ul><li>`accountParentID` 在「XDM業務帳戶詳細資訊」欄位組中</li><li>類型：一對一</li><li>參考結構：`[!DNL Marketo] Named Account {MUNCHKIN_ID}`</li><li>命名空間: `marketo_named_account_{MUNCHKIN_ID}` |
| [!DNL Marketo] 活動 `{MUNCHKIN ID}` | XDM ExperienceEvent | <ul><li>造訪網頁</li><li>新銷售線索</li><li>轉換銷售線索</li><li>新增至清單</li><li>從清單中移除</li><li>添加到業務機會</li><li>從銷售機會中刪除</li><li>填寫的表單</li><li>連結點按次數</li><li>電子郵件傳送</li><li>已開啟電子郵件</li><li>已點按電子郵件</li><li>電子郵件已退回</li><li>Email Roburced Soft</li><li>取消訂閱電子郵件</li><li>分數已變更</li><li>業務機會更新</li><li>促銷活動進展狀態已變更</li><li>人員識別碼</li><li>Marketo網址 | 啟用 | `personID` 人員識別碼欄位群組 | `marketo_person_{MUNCHKIN_ID}` | 無 | 無 | 第一關係<ul><li>`listOperations.listID` 欄位</li><li>類型：一對一</li><li>參考結構：`[!DNL Marketo] Static List {MUNCHKIN_ID}`</li><li>命名空間: `marketo_static_list_{MUNCHKIN_ID}`</li></ul>第二種關係<ul><li>`opportunityEvent.opportunityID` 欄位</li><li>類型：一對一</li><li>參考結構：`[!DNL Marketo] Opportunity {MUNCHKIN_ID}`</li><li>命名空間: `marketo_opportunity_{MUNCHKIN_ID}`</li></ul>第三種關係<ul><li>`leadOperation.campaignProgression.campaignID` 欄位</li><li>類型：一對一</li><li>參考結構：`[!DNL Marketo] Program {MUNCHKIN_ID}`</li><li>命名空間: `marketo_program_{MUNCHKIN_ID}`</li></ul> | `[!DNL Marketo] Activity {MUNCHKIN_ID}`架構的主要身份是`personID`，與`[!DNL Marketo] Person {MUNCHKIN_ID}`架構的主要身份相同。 |

{style=&quot;table-layout:auto&quot;}

## 後續步驟

如要瞭解如何將[!DNL Marketo]資料連接至平台，請參閱UI](../../../tutorials/ui/create/adobe-applications/marketo.md)中有關建立Marketo源連接器的教學課程。[
