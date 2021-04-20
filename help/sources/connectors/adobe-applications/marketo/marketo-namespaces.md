---
keywords: Experience Platform;home；常用主題；Marketo源連接器；命名空間；方案
solution: Experience Platform
title: 'Marketo命名空間 '
topic: 概述
description: 本文檔概述了建立Marketo Engage源連接器時所需的自定義命名空間。
translation-type: tm+mt
source-git-commit: 2563b413ec35cb4c5f05a54bce6f7271917e51f3
workflow-type: tm+mt
source-wordcount: '1177'
ht-degree: 5%

---


# （測試版）[!DNL Marketo Engage]名稱空間和結構描述

>[!IMPORTANT]
>
>[!DNL Marketo Engage]來源目前處於測試階段。 功能和說明檔案會有所變更。

本文檔提供有關[!DNL Marketo Engage]（下稱&quot;[!DNL Marketo]&quot;）使用的B2B名稱空間和架構的基礎設定的資訊。 本文檔還提供有關設定生成[!DNL Marketo] B2B名稱空間和架構所需的郵遞員自動化實用程式的詳細資訊。

## 先決條件

您必須先設定平台開發人員主控台和[!DNL Postman]環境，才能產生B2B名稱空間和結構描述。 如需詳細資訊，請參閱[設定開發人員主控台和 [!DNL Postman]](../../../../landing/postman.md)的教學課程。

在設定平台開發人員主控台和[!DNL Postman]後，請將下列變數套用至您的[!DNL Marketo]環境：

| 環境變數 | 範例值 | 附註 |
| --- | --- | --- |
| `PRIVATE_KEY` | `{PRIVATE_KEY}` |
| `SANDBOX_NAME` | `prod` |
| `TENANT_ID` | `b2bcdpproductiontest` |
| `munchkinId` | `123-ABC-456 ` | 如需詳細資訊，請參閱[驗證您的 [!DNL Marketo] instance](./marketo-auth.md)的教學課程。 |
| `sfdc_org_id` | `00D4W000000FgYJUA0` | 有關獲取組織ID的詳細資訊，請參閱以下[[!DNL Salesforce] 指南](https://help.salesforce.com/articleView?id=000325251&amp;type=1&amp;mode=1)。 |
| `msd_org_id` | `f6438fab-67e8-4814-a6b5-8c8dcdf7a98f` | 有關獲取組織ID的詳細資訊，請參閱以下[[!DNL Microsoft Dynamics] 指南](https://docs.microsoft.com/en-us/power-platform/admin/determine-org-id-name)。 |
| `has_abm` | `false` | 如果您訂閱帳戶型行銷，此值會設為`true`。 |
| `has_msi` | `false` | 如果您訂閱[!DNL Marketo Sales Insight]，此值會設為`true`。 |

{style=&quot;table-layout:auto&quot;}

## [!DNL Marketo] 命名空間

身分名稱空間是[[!DNL Identity Service]](../../../../identity-service/home.md)的一個元件，用作身份相關上下文的指示器。

完全限定身份包括ID值和命名空間。 每個新[!DNL Marketo]例項和資料集組合都需要新的自訂命名空間。 例如，[!DNL Marketo]來源連接器收錄`programs`資料集需要其自訂命名空間，而另一個Marketo來源連接器收錄相同資料集也需要其新的自訂命名空間。 如需詳細資訊，請參閱[名稱空間概述](../../../../identity-service/namespaces.md)。

[!DNL Marketo]命名空間用於實體的主要標識。

下表包含有關[!DNL Marketo]名稱空間的基礎設定的資訊。

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

| 顯示名稱 | 身分符號 | 身分類型 | 發行者類型 | 發行者實體類型 | [!DNL Salesforce] 訂閱組織ID範例 |
| --- | --- | --- | --- | --- | --- |
| `salesforce_person_{SALESFORCE_ORGANIZATION_ID}` | 自動產生 | `CROSS_DEVICE` | [!DNL Salesforce] | `person` | `00DA0000000Hz79` |
| `salesforce_account_{SALESFORCE_ORGANIZATION_ID}` | 自動產生 | `B2B_ACCOUNT` | [!DNL Salesforce] | `account` | `00DA0000000Hz79` |
| `salesforce_opportunity_{SALESFORCE_ORGANIZATION_ID}` | 自動產生 | `B2B_OPPORTUNITY` | [!DNL Salesforce] | `opportunity` | `00DA0000000Hz79` |
| `salesforce_opportunity_contact_role_{SALESFORCE_ORGANIZATION_ID}` | 自動產生 | `B2B_OPPORTUNITY_PERSON` | [!DNL Salesforce] | `opportunity contact role` | `00DA0000000Hz79` |
| `salesforce_campaign_{SALESFORCE_ORGANIZATION_ID}` | 自動產生 | `B2B_CAMPAIGN` | [!DNL Salesforce] | `campaign` | `00DA0000000Hz79` |
| `salesforce_campaign_member_{SALESFORCE_ORGANIZATION_ID}` | 自動產生 | `B2B_CAMPAIGN_MEMBER` | [!DNL Salesforce] | `campaign member` | `00DA0000000Hz79` |

{style=&quot;table-layout:auto&quot;}

### [!DNL Microsoft Dynamics] 命名空間

如果您訂閱[!DNL Dynamics]整合，則[!DNL Dynamics]命名空間會用作實體的次要身分識別。

下表包含有關[!DNL Dynamics]名稱空間的基礎設定的資訊。

| 顯示名稱 | 身分符號 | 身分類型 | 發行者類型 | 發行者實體類型 | [!DNL Salesforce] 訂閱組織ID範例 |
| --- | --- | --- | --- | --- | --- |
| `microsoft_person_{DYNAMICS_ID}` | 自動產生 | `CROSS_DEVICE` | [!DNL Microsoft] | `person` | `94cahe38-e51h-3d57-a9c6-2edklb7184mh` |
| `microsoft_account_{DYNAMICS_ID}` | 自動產生 | `B2B_ACCOUNT` | [!DNL Microsoft] | `account` | `94cahe38-e51h-3d57-a9c6-2edklb7184mh` |
| `microsoft_opportunity_{DYNAMICS_ID}` | 自動產生 | `B2B_OPPORTUNITY` | [!DNL Microsoft] | `opportunity` | `94cahe38-e51h-3d57-a9c6-2edklb7184mh` |
| `microsoft_opportunity_contact_connection_{DYNAMICS_ID}` | 自動產生 | `B2B_OPPORTUNITY_PERSON` | [!DNL Microsoft] | `opportunity relationship` | `94cahe38-e51h-3d57-a9c6-2edklb7184mh` |
| `microsoft_campaign_{DYNAMICS_ID}` | 自動產生 | `B2B_CAMPAIGN` | [!DNL Microsoft] | `campaign` | `94cahe38-e51h-3d57-a9c6-2edklb7184mh` |
| `microsoft_campaign_member_{DYNAMICS_ID}` | 自動產生 | `B2B_CAMPAIGN_MEMBER` | [!DNL Microsoft] | `campaign member` | `94cahe38-e51h-3d57-a9c6-2edklb7184mh` |

## [!DNL Marketo] 模式

Experience Platform 會使用結構，以一致且可重複使用的方式說明資料結構。藉由定義跨系統的一致資料，將可輕易保留意義，而發揮資料應有的價值。

在將資料引入平台之前，必須構建一個模式來描述資料的結構，並為每個欄位中可包含的資料類型提供約束。 結構描述由基類和零個或多個混合組成。

有關架構構成模型（包括設計原則和最佳實踐）的詳細資訊，請參閱[架構構成基礎](../../../../xdm/schema/composition.md)。

下表包含有關[!DNL Marketo]方案的基礎設定的資訊。

>[!NOTE]
>
>請向左／向右滾動以查看表的完整內容。

| 架構名稱 | 基本類 | Mixins | 主要身分 | 主要身分名稱空間 | 次要身份 | 次要身分名稱空間 | 關係 | 附註 |
| --- | --- | --- | --- | --- | --- | --- | --- | --- |
| [!DNL Marketo] 公司{MUNCHKIN_ID} | XDM業務帳戶 | XDM業務帳戶詳細資訊 | `accountID` 在基本類中 | `marketo_company_{MUNCHKIN_ID}` | `extSourceSystemAudit.externalID` 在基本類中 | `salesforce_account_{SALESFORCE_ORGANIZATION_ID}` | <ul><li>`accountParentID` 在XDM商業帳戶詳細資料混合中</li><li>類型：一對一</li><li>參考結構：Marketo公司{MUNCHKIN_ID}</li><li>命名空間: `marketo_company_{MUNCHKIN_ID}`</li></ul> |
| [!DNL Marketo] 人員{MUNCHKIN_ID} | XDM個人資料 | <ul><li>XDM業務人員詳細資訊</li><li>XDM業務人員元件</li></ul> | `personID` 在基本類中 | `marketo_person_{MUNCHKIN_ID}` | <ol><li>`extSourceSystemAudit.externalID` XDM企業人員詳細資料混合</li><li>`workEmail.address` XDM企業人員詳細資料混合</li><li>`identityMap` Identity Map混音</ol></li> | <ol><li>`salesforce_person_{SALESFORCE_ORGANIZATION_ID}`</li><li>電子郵件</li><li>ECID</li></ol> | <ul><li>`personComponents.sourceAccountID` XDM企業人員元件混合</li><li>類型：多對一</li><li>參考結構：Marketo公司{MUNCHKIN_ID}</li><li>命名空間: `marketo_company_{MUNCHKIN_ID}`</li><li>目標屬性：`accountID`</li><li>當前方案的關係名稱：帳戶</li><li>參考方案中的關係名稱：人物</li></ul> |
| [!DNL Marketo] 機會{MUNCHKIN_ID} | XDM業務機會 | XDM業務機會詳細資訊 | `opportunityID` 在基本類中 | `marketo_opportunity_{MUNCHKIN_ID}` | `extSourceSystemAudit.externalID` 在基本類中 | `salesforce_opportunity_{SALESFORCE_ORGANIZATION_ID}` | <ul><li>`accountID` 在基本類中</li><li>類型：多對一</li><li>參考結構：Marketo公司{MUNCHKIN_ID}</li><li>命名空間: `marketo_company_{MUNCHKIN_ID}`</li><li>目標屬性：`accountID`</li><li>當前方案的關係名稱：帳戶</li><li>參考方案中的關係名稱：機會</li></ul> |
| [!DNL Marketo] 業務機會聯繫人角色{MUNCHKIN_ID} | XDM業務機會人關係 | None | `opportunityPersonID` 在基本類中 | `marketo_opportunity_contact_role_{MUNCHKIN_ID}` | `extSourceSystemAudit.externalID` 在基本類中 | `salesforce_opportunity_contact_role_{SALESFORCE_ORGANIZATION_ID}` | 第一關係<ul><li>`personID` 在基本類中</li><li>類型：多對一</li><li>參考結構：Marketo人{MUNCHKIN_ID}</li><li>命名空間: `marketo_person_{MUNCHKIN_ID}`</li><li>目標屬性：`personID`</li><li>當前方案的關係名稱：人物</li><li>參考方案中的關係名稱：機會</li></ul>第二種關係<ul><li>`opportunityID` 在基本類中</li><li>類型：多對一</li><li>參考結構：Marketo機會{MUNCHKIN_ID}</li><li>命名空間: `marketo_opportunity_{MUNCHKIN_ID}`</li><li>目標屬性：`opportunityID`</li><li>當前方案的關係名稱：機會</li><li>參考方案中的關係名稱：人物</li></ul> |
| [!DNL Marketo] 方案{MUNCHKIN_ID} | XDM Business Campaign | XDM Business Campaign詳細資訊 | `campaignID` 在基本類中 | `marketo_program_{MUNCHKIN_ID}` | `extSourceSystemAudit.externalID` 在基本類中 | `salesforce_campaign_SALESFORCE_ORGANIZATION_ID}` |
| [!DNL Marketo] 方案成員{MUNCHKIN_ID} | XDM Business Campaign會員 | XDM Business Campaign成員詳細資訊 | `campaignMemberID` 在基本類中 | `marketo_program_member_{MUNCHKIN_ID}` | 無 | 無 | 第一關係<ul><li>`personID` 在基本類中</li><li>類型：多對一</li><li>參考結構：Marketo人{MUNCHKIN_ID}</li><li>命名空間: `marketo_person_{MUNCHKIN_ID}`</li><li>目標屬性：`personID`</li><li>當前方案的關係名稱：人物</li><li>參考方案中的關係名稱：計畫</li></ul>第二種關係<ul><li>`campaignID` 在基本類中</li><li>類型：多對一</li><li>參考結構：Marketo計畫{MUNCHKIN_ID}</li><li>命名空間: `marketo_program_{MUNCHKIN_ID}`</li><li>目標屬性：campaignID</li><li>當前方案的關係名稱：計畫</li><li>參考方案中的關係名稱：人物</li></ul> |
| [!DNL Marketo] 靜態清單{MUNCHKIN_ID} | XDM業務營銷清單 | 無 | `marketingListID` 在基本類中 | `marketo_static_list_{MUNCHKIN_ID}` | 無 | 無 | 無 | 靜態清單與[!DNL Salesforce]不同步，因此沒有輔助標識 |
| [!DNL Marketo] 靜態清單成員{MUNCHKIN_ID} | XDM Business Marketing List成員 | 無 | `marketingListMemberID` 在基本類中 | `marketo_static_list_member_{MUNCHKIN_ID}` | 無 | 無 | 第一關係<ul><li>`personID` 在基本類中</li><li>類型：多對一</li><li>參考結構：Marketo人{MUNCHKIN_ID}</li><li>命名空間: `marketo_person_{MUNCHKIN_ID}`</li><li>目標屬性：`personID`</li><li>當前方案的關係名稱：人物</li><li>參考方案中的關係名稱：清單</li></ul>第二種關係<ul><li>`marketingListID` 在基本類中</li><li>類型：多對一</li><li>參考結構：Marketo靜態清單{MUNCHKIN_ID}</li><li>命名空間: `marketo_static_list_{MUNCHKIN_ID}`</li><li>目標屬性：`marketingListID`</li><li>當前方案的關係名稱：清單</li><li>參考方案中的關係名稱：人物</li></ul> |
| [!DNL Marketo] 命名帳戶{MUNCHKIN_ID} | XDM業務帳戶 | XDM業務帳戶詳細資訊 | `accountID` 在基本類中 | `marketo_named_account_{MUNCHKIN_ID}` | `extSourceSystemAudit.externalID` 在基本類中 | `salesforce_account_{SALESFORCE_ORGANIZATION_ID}` | <ul><li>`accountParentID` 在XDM商業帳戶詳細資料混合中</li><li>類型：一對一</li><li>參考結構：Marketo命名帳戶{MUNCHKIN_ID}</li><li>命名空間: `marketo_named_account_{MUNCHKIN_ID}` |
| [!DNL Marketo] 活動{MUNCHKIN ID} | XDM體驗活動 | <ul><li>造訪網頁</li><li>新銷售線索</li><li>轉換銷售線索</li><li>新增至清單</li><li>從清單中移除</li><li>添加到業務機會</li><li>從銷售機會中刪除</li><li>填寫的表單</li><li>連結點按次數</li><li>電子郵件傳送</li><li>已開啟電子郵件</li><li>已點按電子郵件</li><li>電子郵件已退回</li><li>Email Roburced Soft</li><li>取消訂閱電子郵件</li><li>分數已變更</li><li>業務機會更新</li><li>促銷活動進展狀態已變更</li><li>人員識別碼</li><li>Marketo網址 | `personID` 人物識別碼混合 | marketo_person_{MUNCHKIN_ID} | 無 | 無 | 第一關係<ul><li>`listOperations.listID` 欄位</li><li>類型：一對一</li><li>參考結構：Marketo靜態清單{MUNCHKIN_ID}</li><li>命名空間: `marketo_static_list_{MUNCHKIN_ID}`</li></ul>第二種關係<ul><li>`opportunityEvent.opportunityID` 欄位</li><li>類型：一對一</li><li>參考結構：Marketo機會{MUNCHKIN_ID}</li><li>命名空間: `marketo_opportunity_{MUNCHKIN_ID}`</li></ul>第三種關係<ul><li>`leadOperation.campaignProgression.campaignID` 欄位</li><li>類型：一對一</li><li>參考結構：Marketo計畫{MUNCHKIN_ID}</li><li>命名空間: `marketo_program_{MUNCHKIN_ID}`</li></ul> |

{style=&quot;table-layout:auto&quot;}

>[!NOTE]
>
>[!DNL Real-time Customer Profile]的所有方案都已啟用

## 後續步驟

如要瞭解如何將[!DNL Marketo]資料連接至平台，請參閱UI](../../../tutorials/ui/create/adobe-applications/marketo.md)中有關建立Marketo源連接器的教學課程。[