---
keywords: Experience Platform；首頁；熱門主題；Marketo來源連接器；命名空間；結構；b2b;B2B
solution: Experience Platform
title: B2B命名空間和結構
description: 本檔案概述建立B2B來源連接器時所需的自訂命名空間。
exl-id: f1592be5-987e-41b8-9844-9dea5bd452b9
source-git-commit: 59dfa862388394a68630a7136dee8e8988d0368c
workflow-type: tm+mt
source-wordcount: '1707'
ht-degree: 4%

---

# B2B命名空間和結構

本檔案提供與B2B來源搭配使用之命名空間和結構之基礎設定的相關資訊。 本檔案也提供有關設定產生B2B命名空間和結構所需的Postman自動化公用程式的詳細資訊。

>[!IMPORTANT]
>
>您必須擁有 [Adobe Real-time Customer Data Platform B2B版](../../../../rtcdp/b2b-overview.md) 讓B2B架構參與 [即時客戶個人檔案](../../../../profile/home.md).

## 設定B2B命名空間和架構自動產生公用程式

使用B2B命名空間和架構自動產生公用程式的第一步，是設定您的平台開發人員主控台，以及 [!DNL Postman] 環境。

- 您可以從此下載命名空間和架構自動產生公用程式集合及環境 [GitHub存放庫](https://github.com/adobe/experience-platform-postman-samples/tree/master/Postman%20Collections/CDP%20Namespaces%20and%20Schemas%20Utility).
- 如需使用Platform API的詳細資訊，包括如何收集必要標題的值以及讀取範例API呼叫的詳細資訊，請參閱 [Platform API快速入門](../../../../landing/api-guide.md).
- 如需如何產生Platform API認證的詳細資訊，請參閱 [驗證和存取Experience PlatformAPI](../../../../landing/api-authentication.md).
- 有關如何設定的資訊 [!DNL Postman] 若為Platform API，請參閱以下的教學課程： [設定開發人員主控台和 [!DNL Postman]](../../../../landing/postman.md).

使用Platform開發人員主控台和 [!DNL Postman] 設定後，您現在可以開始將適當的環境值套用至 [!DNL Postman] 環境。

下表包含範例值，以及填入 [!DNL Postman] 環境：

| 變數 | 說明 | 範例 |
| --- | --- | --- |
| `CLIENT_SECRET` | 用來產生您 `{ACCESS_TOKEN}`. 請參閱 [驗證和存取Experience PlatformAPI](../../../../landing/api-authentication.md) 以了解如何擷取 `{CLIENT_SECRET}`. | `{CLIENT_SECRET}` |
| `JWT_TOKEN` | JSON Web Token(JWT)是用於生成{ACCESS_TOKEN}的驗證憑據。 請參閱 [驗證和存取Experience PlatformAPI](../../../../landing/api-authentication.md) 以了解如何產生 `{JWT_TOKEN}`. | `{JWT_TOKEN}` |
| `API_KEY` | 用來驗證對Experience PlatformAPI呼叫的唯一識別碼。 請參閱 [驗證和存取Experience PlatformAPI](../../../../landing/api-authentication.md) 以了解如何擷取 `{API_KEY}`. | `c8d9a2f5c1e03789bd22e8efdd1bdc1b` |
| `ACCESS_TOKEN` | 完成對Experience PlatformAPI的呼叫所需的授權Token。 請參閱 [驗證和存取Experience PlatformAPI](../../../../landing/api-authentication.md) 以了解如何擷取 `{ACCESS_TOKEN}`. | `Bearer {ACCESS_TOKEN}` |
| `META_SCOPE` | 關於 [!DNL Marketo]，此值已修正，且一律設為： `ent_dataservices_sdk`. | `ent_dataservices_sdk` |
| `CONTAINER_ID` | 此 `global` 容器包含所有標準Adobe和Experience Platform合作夥伴提供的類、架構欄位組、資料類型和架構。 關於 [!DNL Marketo]，此值會固定且一律設為 `global`. | `global` |
| `PRIVATE_KEY` | 用於驗證您的 [!DNL Postman] 例項來Experience PlatformAPI。 請參閱設定開發人員主控台的教學課程，以及 [設定開發人員主控台和 [!DNL Postman]](../../../../landing/postman.md) 有關如何檢索{PRIVATE_KEY}的說明。 | `{PRIVATE_KEY}` |
| `TECHNICAL_ACCOUNT_ID` | 用於整合到Adobe I/O的憑據。 | `D42AEVJZTTJC6LZADUBVPA15@techacct.adobe.com` |
| `IMS` | Identity Management系統(IMS)提供Adobe服務驗證的架構。 關於 [!DNL Marketo]，此值已修正，且一律設為： `ims-na1.adobelogin.com`. | `ims-na1.adobelogin.com` |
| `IMS_ORG` | 擁有或許可產品和服務並允許訪問其成員的公司實體。 請參閱 [設定開發人員主控台和 [!DNL Postman]](../../../../landing/postman.md) 有關如何檢索 `{ORG_ID}` 資訊。 | `ABCEH0D9KX6A7WA7ATQE0TE@adobeOrg` |
| `SANDBOX_NAME` | 您使用的虛擬沙箱分區的名稱。 | `prod` |
| `TENANT_ID` | 用來確保所建立資源與IMS組織中的ID命名方式正確，且內容也包含在您的IMS組織中。 | `b2bcdpproductiontest` |
| `PLATFORM_URL` | 您進行API呼叫的URL端點。 此值已修正，且一律設為： `http://platform.adobe.io/`. | `http://platform.adobe.io/` |

{style=&quot;table-layout:auto&quot;}

### 執行指令碼

使用 [!DNL Postman] 集合和環境設定後，您現在可以透過 [!DNL Postman] 介面。

在 [!DNL Postman] 介面，選擇自動生成器實用程式的根資料夾，然後選擇 **[!DNL Run]** 從頂端標題。

![根資料夾](../images/marketo/root-folder.png)

此 [!DNL Runner] 介面。 從此處，確保選中所有複選框，然後選中 **[!DNL Run Namespaces and Schemas Autogeneration Utility]**.

![運行生成器](../images/marketo/run-generator.png)

成功的要求會建立B2B所需的命名空間和結構。

## B2B命名空間

身分識別命名空間是 [[!DNL Identity Service]](../../../../identity-service/home.md) 用來區分身分的上下文或類型。 完全限定的身分包括ID值和命名空間。 請參閱 [命名空間概述](../../../../identity-service/namespaces.md) 以取得更多資訊。

B2B命名空間用於實體的主要身分識別中。

下表包含為B2B命名空間設定之基礎的相關資訊。

>[!NOTE]
>
>請向左/向右滾動以查看表的完整內容。

| 顯示名稱 | 身分符號 | 身分類型 |
| --- | --- | --- |
| B2B人員 | `b2b_person` | `CROSS_DEVICE` |
| B2B帳戶 | `b2b_account` | `B2B_ACCOUNT` |
| B2B機會 | `b2b_opportunity` | `B2B_OPPORTUNITY` |
| B2B機會人員關係 | `b2b_opportunity_person_relation` | `B2B_OPPORTUNITY_PERSON` |
| B2B行銷活動 | `b2b_campaign` | `B2B_CAMPAIGN` |
| B2B促銷活動成員 | `b2b_campaign_member` | `B2B_CAMPAIGN_MEMBER` |
| B2B行銷清單 | `b2b_marketing_list` | `B2B_MARKETING_LIST` |
| B2B行銷清單成員 | `b2b_marketing_list_member` | `B2B_MARKETING_LIST_MEMBER` |
| B2B帳戶人員關係 | `b2b_account_person_relation` | `B2B_ACCOUNT_PERSON` |

{style=&quot;table-layout:auto&quot;}

## B2B結構

Experience Platform 會使用結構，以一致且可重複使用的方式說明資料結構。藉由定義跨系統的一致資料，將可輕易保留意義，而發揮資料應有的價值。

在將資料擷取至Platform之前，必須先建立結構以說明資料的結構，並對每個欄位中可包含的資料類型提供限制。 結構由基類和零個或多個結構欄位組組成。

如需結構構成模型的詳細資訊，包括設計原則和最佳實務，請參閱 [綱要構成基本知識](../../../../xdm/schema/composition.md).

下表包含B2B架構的基礎設定資訊。

>[!NOTE]
>
>請向左/向右滾動以查看表的完整內容。

| 架構名稱 | 基類 | 欄位群組 | [!DNL Profile] 結構 | 主要身分 | 主要身分命名空間 | 次要身分 | 次要身分命名空間 | 關係 | 附註 |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| B2B帳戶 | [XDM商業帳戶](../../../../xdm/classes/b2b/business-account.md) | XDM業務帳戶詳細資訊 | 啟用 | `accountKey.sourceKey` 在基類中 | B2B帳戶 | `extSourceSystemAudit.externalKey.sourceKey` 在基類中 | B2B帳戶 | <ul><li>`accountParentKey.sourceKey` 在「 XDM業務帳戶詳細資訊」欄位組中</li><li>目標屬性： `/accountKey/sourceKey`</li><li>類型：一對一</li><li>參考結構：B2B帳戶</li><li>命名空間：B2B帳戶</li></ul> |
| B2B人員 | [XDM個別設定檔](../../../../xdm/classes/individual-profile.md) | <ul><li>XDM業務人員詳細資訊</li><li>XDM企業人員元件</li><li>IdentityMap</li><li>同意和偏好設定詳細資訊</li></ul> | 啟用 | `b2b.personKey.sourceKey` 「 XDM業務人員詳細資訊」欄位組 | B2B人員 | <ol><li>`extSourceSystemAudit.externalKey.sourceKey` XDM業務人員詳細資訊欄位組</li><li>`workEmail.address` XDM業務人員詳細資訊欄位組</ol></li> | <ol><li>B2B人員</li><li>電子郵件</li></ol> | <ul><li>`personComponents.sourceAccountKey.sourceKey` XDM業務人員元件欄位組</li><li>類型：多對一</li><li>參考結構：B2B帳戶</li><li>命名空間：B2B帳戶</li><li>目標屬性：accountKey.sourceKey</li><li>當前架構的關係名稱：帳戶</li><li>引用架構的關係名稱：人員</li></ul> |
| B2B機會 | [XDM業務機會](../../../../xdm/classes/b2b/business-opportunity.md) | XDM業務機會詳細資訊 | 啟用 | `opportunityKey.sourceKey` 在基類中 | B2B機會 | `extSourceSystemAudit.externalKey.sourceKey` 在基類中 | B2B機會 | <ul><li>`accountKey.sourceKey` 在基類中</li><li>類型：多對一</li><li>參考結構：B2B帳戶</li><li>命名空間：B2B帳戶</li><li>目標屬性： `accountKey.sourceKey`</li><li>當前架構的關係名稱：帳戶</li><li>引用架構的關係名稱：機會</li></ul> |
| B2B機會人員關係 | [XDM商機人員關係](../../../../xdm/classes/b2b/business-opportunity-person-relation.md) | None | 啟用 | `opportunityPersonKey.sourceKey` 在基類中 | B2B機會人員關係 | `extSourceSystemAudit.externalKey.sourceKey` 在基類中 | B2B機會人員關係 | **第一關係**<ul><li>`personKey.sourceKey` 在基類中</li><li>類型：多對一</li><li>參考結構：B2B人員</li><li>命名空間：B2B人員</li><li>目標屬性：b2b.personKey.sourceKey</li><li>當前架構的關係名稱：人員</li><li>引用架構的關係名稱：機會</li></ul>**第二關係**<ul><li>`opportunityKey.sourceKey` 在基類中</li><li>類型：多對一</li><li>參考結構：B2B機會 </li><li>命名空間：B2B機會 </li><li>目標屬性： `opportunityKey.sourceKey`</li><li>當前架構的關係名稱：機會</li><li>引用架構的關係名稱：人員</li></ul> |
| B2B行銷活動 | [XDM商業宣傳](../../../../xdm/classes/b2b/business-campaign.md) | XDM商業促銷活動詳細資訊 | 啟用 | `campaignKey.sourceKey` 在基類中 | B2B行銷活動 | `extSourceSystemAudit.externalKey.sourceKey` 在基類中 | B2B行銷活動 |
| B2B促銷活動成員 | [XDM Business Campaign成員](../../../../xdm/classes/b2b/business-campaign-members.md) | XDM Business Campaign成員詳細資訊 | 啟用 | `ccampaignMemberKey.sourceKey` 在基類中 | B2B促銷活動成員 | `extSourceSystemAudit.externalKey.sourceKey` 在基類中 | B2B促銷活動成員 | **第一關係**<ul><li>`personKey.sourceKey` 在基類中</li><li>類型：多對一</li><li>參考結構：B2B人員</li><li>命名空間：B2B人員</li><li>目標屬性： `b2b.personKey.sourceKey`</li><li>當前架構的關係名稱：人員</li><li>引用架構的關係名稱：行銷活動</li></ul>**第二關係**<ul><li>`campaignKey.sourceKey` 在基類中</li><li>類型：多對一</li><li>參考結構：B2B行銷活動</li><li>命名空間：B2B行銷活動</li><li>目標屬性： `campaignKey.sourceKey`</li><li>當前架構的關係名稱：行銷活動</li><li>引用架構的關係名稱：人員</li></ul> |
| B2B行銷清單 | [XDM商業行銷清單](../../../../xdm/classes/b2b/business-marketing-list.md) | None | 啟用 | `marketingListKey.sourceKey` 在基類中 | B2B行銷清單 | None | None | None | 靜態清單未從同步 [!DNL Salesforce] 因此沒有次要身分。 |
| B2B行銷清單成員 | [XDM商業行銷清單成員](../../../../xdm/classes/b2b/business-marketing-list-members.md) | None | 啟用 | `marketingListMemberKey.sourceKey` 在基類中 | B2B行銷清單成員 | None | None | **第一關係**<ul><li>`PersonKey.sourceKey` 在基類中</li><li>類型：多對一</li><li>參考結構：B2B人員</li><li>命名空間：B2B人員</li><li>目標屬性： `b2b.personKey.sourceKey`</li><li>當前架構的關係名稱：人員</li><li>引用架構的關係名稱：行銷清單</li></ul>**第二關係**<ul><li>`marketingListKey.sourceKey` 在基類中</li><li>類型：多對一</li><li>參考結構：B2B行銷清單</li><li>命名空間：B2B行銷清單</li><li>目標屬性： `marketingListKey.sourceKey`</li><li>當前架構的關係名稱：行銷清單</li><li>引用架構的關係名稱：人員</li></ul> | 靜態清單成員未從同步 [!DNL Salesforce] 因此沒有次要身分。 |
| B2B活動 | [XDM ExperienceEvent](../../../../xdm/classes/experienceevent.md) | <ul><li>造訪網頁</li><li>新銷售機會</li><li>轉換銷售機會</li><li>添加到清單</li><li>從清單中刪除</li><li>添加到機會</li><li>從銷售機會中刪除</li><li>已填寫表單</li><li>連結點按次數</li><li>電子郵件傳送</li><li>已開啟電子郵件</li><li>已點按電子郵件</li><li>電子郵件已退信</li><li>電子郵件已跳出軟體</li><li>取消訂閱電子郵件</li><li>分數已變更</li><li>已更新銷售機會</li><li>促銷活動進展中的狀態已變更</li><li>人員識別碼</li><li>Marketo Web URL</li><li>有趣的時刻</li><li>呼叫Webhook</li><li>變更促銷活動順序</li><li>收入階段已變更</li><li>合併銷售機會</li><li>已傳送電子郵件</li><li>變更促銷活動資料流</li><li>新增至Campaign</li></ul> | 啟用 | `personKey.sourceKey` 人員標識符欄位組 | B2B人員 | None | None | **第一關係**<ul><li>`listOperations.listKey.sourceKey` 欄位</li><li>類型：一對一</li><li>參考結構：B2B行銷清單</li><li>命名空間：B2B行銷清單</li></ul>**第二關係**<ul><li>`opportunityEvent.opportunityKey.sourceKey` 欄位</li><li>類型：一對一</li><li>參考結構：B2B機會</li><li>命名空間：B2B機會</li></ul>**第三種關係**<ul><li>`leadOperation.campaignProgression.campaignKey.sourceKey` 欄位</li><li>類型：一對一</li><li>參考結構：B2B行銷活動</li><li>命名空間：B2B行銷活動</li></ul> | `ExperienceEvent` 與實體不同。 體驗事件的身分是執行活動的人員。 |
| B2B帳戶人員關係 | [XDM企業帳戶人員關係](../../../../xdm/classes/b2b/business-account-person-relation.md) | 身分對應 | 啟用 | `accountPersonKey.sourceKey` 在基類中 | B2B帳戶人員關係 | None | None | **第一關係**<ul><li>`personKey.sourceKey` 在基類中</li><li>類型：多對一</li><li>參考結構：B2B人員</li><li>命名空間：B2B人員</li><li>目標屬性： `b2b.personKey.SourceKey`</li><li>當前架構的關係名稱：人員</li><li>引用架構的關係名稱：帳戶</li></ul>**第二關係**<ul><li>`accountKey.sourceKey` 在基類中</li><li>類型：多對一</li><li>參考結構：B2B帳戶</li><li>命名空間：B2B帳戶</li><li>目標屬性： `accountKey.sourceKey`</li><li>當前架構的關係名稱：帳戶</li><li>引用架構的關係名稱：人員</li></ul> |

{style=&quot;table-layout:auto&quot;}

## 後續步驟

了解如何連接 [!DNL Marketo] 若要將資料傳送至Platform，請參閱 [在UI中建立Marketo來源連接器](../../../tutorials/ui/create/adobe-applications/marketo.md).
