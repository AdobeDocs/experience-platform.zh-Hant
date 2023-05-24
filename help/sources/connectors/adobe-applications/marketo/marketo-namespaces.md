---
title: B2B命名空間和架構
description: 本文檔概述了建立B2B源連接器時所需的自定義命名空間。
exl-id: f1592be5-987e-41b8-9844-9dea5bd452b9
source-git-commit: fcd44aef026c1049ccdfe5896e6199d32b4d1114
workflow-type: tm+mt
source-wordcount: '1717'
ht-degree: 4%

---

# B2B命名空間和架構

>[!NOTE]
>
>您可以使用Adobe Experience PlatformUI中的模板加快B2B和B2C資料的資產建立。 有關詳細資訊，請閱讀上的指南 [在平台UI中使用模板](../../../tutorials/ui/templates.md)。

本文檔提供有關要與B2B源一起使用的命名空間和架構的基礎設定的資訊。 本文檔還提供了有關設定生成B2B命名空間和架構所需的Postman自動化實用程式的詳細資訊。

>[!IMPORTANT]
>
>您必須有權訪問 [Adobe Real-time Customer Data PlatformB2B版](../../../../rtcdp/b2b-overview.md) 以便B2B模式參與 [即時客戶配置檔案](../../../../profile/home.md)。

## 設定B2B命名空間和模式自動生成實用程式

使用B2B命名空間和模式自動生成實用程式的第一步是設定平台開發人員控制台和 [!DNL Postman] 環境。

- 可以從此下載命名空間和架構自動生成實用程式集合及環境 [GitHub儲存庫](https://github.com/adobe/experience-platform-postman-samples/tree/master/Postman%20Collections/CDP%20Namespaces%20and%20Schemas%20Utility)。
- 有關使用平台API的資訊，包括有關如何收集所需標頭值和讀取示例API調用的詳細資訊，請參閱上的指南 [平台API入門](../../../../landing/api-guide.md)。
- 有關如何為平台API生成憑據的資訊，請參見上的教程 [驗證和訪問Experience PlatformAPI](../../../../landing/api-authentication.md)。
- 有關如何設定的資訊 [!DNL Postman] 有關平台API，請參見上的教程 [設定開發人員控制台和 [!DNL Postman]](../../../../landing/postman.md)。

使用平台開發人員控制台和 [!DNL Postman] 設定後，您現在可以開始將適當的環境值應用到 [!DNL Postman] 環境。

下表包含示例值以及有關填充 [!DNL Postman] 環境：

| 變數 | 說明 | 範例 |
| --- | --- | --- |
| `CLIENT_SECRET` | 用於生成您的 `{ACCESS_TOKEN}`。 請參閱上的教程 [驗證和訪問Experience PlatformAPI](../../../../landing/api-authentication.md) 有關如何檢索 `{CLIENT_SECRET}`。 | `{CLIENT_SECRET}` |
| `JWT_TOKEN` | JSON Web令牌(JWT)是用於生成{ACCESS_TOKEN}的身份驗證憑據。 請參閱上的教程 [驗證和訪問Experience PlatformAPI](../../../../landing/api-authentication.md) 有關如何生成 `{JWT_TOKEN}`。 | `{JWT_TOKEN}` |
| `API_KEY` | 用於驗證對Experience PlatformAPI的調用的唯一標識符。 請參閱上的教程 [驗證和訪問Experience PlatformAPI](../../../../landing/api-authentication.md) 有關如何檢索 `{API_KEY}`。 | `c8d9a2f5c1e03789bd22e8efdd1bdc1b` |
| `ACCESS_TOKEN` | 完成對Experience PlatformAPI的調用所需的授權令牌。 請參閱上的教程 [驗證和訪問Experience PlatformAPI](../../../../landing/api-authentication.md) 有關如何檢索 `{ACCESS_TOKEN}`。 | `Bearer {ACCESS_TOKEN}` |
| `META_SCOPE` | 關於 [!DNL Marketo]，此值是固定的，並且始終設定為： `ent_dataservices_sdk`。 | `ent_dataservices_sdk` |
| `CONTAINER_ID` | 的 `global` 容器包含所有標準Adobe和Experience Platform夥伴提供的類、架構欄位組、資料類型和架構。 關於 [!DNL Marketo]，此值是固定的，始終設定為 `global`。 | `global` |
| `PRIVATE_KEY` | 用於驗證您的 [!DNL Postman] 實例到Experience PlatformAPI。 請參閱有關設定開發人員控制台和 [設定開發人員控制台和 [!DNL Postman]](../../../../landing/postman.md) 有關如何檢索{PRIVATE_KEY}的說明。 | `{PRIVATE_KEY}` |
| `TECHNICAL_ACCOUNT_ID` | 用於整合到Adobe I/O的憑據。 | `D42AEVJZTTJC6LZADUBVPA15@techacct.adobe.com` |
| `IMS` | Identity Management系統(IMS)為Adobe服務提供了驗證框架。 關於 [!DNL Marketo]，此值是固定的，並且始終設定為： `ims-na1.adobelogin.com`。 | `ims-na1.adobelogin.com` |
| `IMS_ORG` | 擁有或許可產品和服務並允許訪問其成員的公司實體。 請參閱上的教程 [設定開發人員控制台和 [!DNL Postman]](../../../../landing/postman.md) 有關如何檢索 `{ORG_ID}` 的下界。 | `ABCEH0D9KX6A7WA7ATQE0TE@adobeOrg` |
| `SANDBOX_NAME` | 您正在使用的虛擬沙盒分區的名稱。 | `prod` |
| `TENANT_ID` | 用於確保建立的資源名稱正確且包含在組織中的ID。 | `b2bcdpproductiontest` |
| `PLATFORM_URL` | 要對其進行API調用的URL終結點。 此值是固定的，始終設定為： `http://platform.adobe.io/`。 | `http://platform.adobe.io/` |

{style="table-layout:auto"}

### 運行指令碼

與 [!DNL Postman] 設定集合和環境，您現在可以通過 [!DNL Postman] 。

在 [!DNL Postman] 介面，選擇自動生成器實用程式的根資料夾，然後選擇 **[!DNL Run]** 的下界。

![根資料夾](../images/marketo/root-folder.png)

的 [!DNL Runner] 對話框。 在此處，確保選中所有複選框，然後選擇 **[!DNL Run Namespaces and Schemas Autogeneration Utility]**。

![運行發電機](../images/marketo/run-generator.png)

成功的請求會建立B2B所需的命名空間和架構。

## B2B命名空間

標識命名空間是 [[!DNL Identity Service]](../../../../identity-service/home.md) 用來區分身份的上下文或類型。 完全限定的標識包括ID值和命名空間。 查看 [命名空間概述](../../../../identity-service/namespaces.md) 的子菜單。

B2B命名空間用於實體的主標識。

下表包含有關為B2B命名空間設定的基礎設定的資訊。

>[!NOTE]
>
>請向左/向右滾動以查看表的完整內容。

| 顯示名稱 | 身分識別符號 | 身分類型 |
| --- | --- | --- |
| B2B人員 | `b2b_person` | `CROSS_DEVICE` |
| B2B帳戶 | `b2b_account` | `B2B_ACCOUNT` |
| B2B機會 | `b2b_opportunity` | `B2B_OPPORTUNITY` |
| B2B機會人員關係 | `b2b_opportunity_person_relation` | `B2B_OPPORTUNITY_PERSON` |
| B2B活動 | `b2b_campaign` | `B2B_CAMPAIGN` |
| B2B市場活動成員 | `b2b_campaign_member` | `B2B_CAMPAIGN_MEMBER` |
| B2B市場營銷清單 | `b2b_marketing_list` | `B2B_MARKETING_LIST` |
| B2B市場營銷清單成員 | `b2b_marketing_list_member` | `B2B_MARKETING_LIST_MEMBER` |
| B2B帳戶人員關係 | `b2b_account_person_relation` | `B2B_ACCOUNT_PERSON` |

{style="table-layout:auto"}

## B2B模式

Experience Platform 會使用結構，以一致且可重複使用的方式說明資料結構。藉由定義跨系統的一致資料，將可輕易保留意義，而發揮資料應有的價值。

在將資料引入平台之前，必須構建一個架構來描述資料的結構，並對每個欄位中可以包含的資料類型提供約束。 架構由基類和零個或多個架構欄位組組成。

有關架構組成模型（包括設計原則和最佳做法）的詳細資訊，請參見 [架構組合基礎](../../../../xdm/schema/composition.md)。

下表包含有關B2B架構的基礎設定的資訊。

>[!NOTE]
>
>請向左/向右滾動以查看表的完整內容。

| 方案名稱 | 基類 | 欄位群組 | [!DNL Profile] 在架構中 | 主要身分識別 | 主標識命名空間 | 次標識 | 輔助標識命名空間 | 關係 | 附註 |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| B2B帳戶 | [XDM業務客戶](../../../../xdm/classes/b2b/business-account.md) | XDM業務帳戶詳細資訊 | 啟用 | `accountKey.sourceKey` 在基類中 | B2B帳戶 | `extSourceSystemAudit.externalKey.sourceKey` 在基類中 | B2B帳戶 | <ul><li>`accountParentKey.sourceKey` 在「XDM業務帳戶詳細資訊」欄位組中</li><li>目標屬性： `/accountKey/sourceKey`</li><li>類型：一對一</li><li>引用架構：B2B帳戶</li><li>命名空間：B2B帳戶</li></ul> |
| B2B人員 | [XDM 個別設定檔](../../../../xdm/classes/individual-profile.md) | <ul><li>XDM業務人員詳細資訊</li><li>XDM業務人員元件</li><li>標識映射</li><li>同意和首選項詳細資訊</li></ul> | 啟用 | `b2b.personKey.sourceKey` 在「XDM業務人員詳細資訊」欄位組中 | B2B人員 | <ol><li>`extSourceSystemAudit.externalKey.sourceKey` XDM業務人員詳細資訊欄位組</li><li>`workEmail.address` XDM業務人員詳細資訊欄位組</ol></li> | <ol><li>B2B人員</li><li>電子郵件</li></ol> | <ul><li>`personComponents.sourceAccountKey.sourceKey` XDM業務人員元件欄位組</li><li>類型：多對一</li><li>引用架構：B2B帳戶</li><li>命名空間：B2B帳戶</li><li>目標屬性：accountKey.sourceKey</li><li>當前架構的關係名稱：帳戶</li><li>來自引用架構的關係名稱：人物</li></ul> |
| B2B機會 | [XDM業務機會](../../../../xdm/classes/b2b/business-opportunity.md) | XDM業務機會詳細資訊 | 啟用 | `opportunityKey.sourceKey` 在基類中 | B2B機會 | `extSourceSystemAudit.externalKey.sourceKey` 在基類中 | B2B機會 | <ul><li>`accountKey.sourceKey` 在基類中</li><li>類型：多對一</li><li>引用架構：B2B帳戶</li><li>命名空間：B2B帳戶</li><li>目標屬性： `accountKey.sourceKey`</li><li>當前架構的關係名稱：帳戶</li><li>來自引用架構的關係名稱：機會</li></ul> |
| B2B機會人員關係 | [XDM業務機會人員關係](../../../../xdm/classes/b2b/business-opportunity-person-relation.md) | None | 啟用 | `opportunityPersonKey.sourceKey` 在基類中 | B2B機會人員關係 | `extSourceSystemAudit.externalKey.sourceKey` 在基類中 | B2B機會人員關係 | **第一段關係**<ul><li>`personKey.sourceKey` 在基類中</li><li>類型：多對一</li><li>引用架構：B2B人員</li><li>命名空間：B2B人員</li><li>目標屬性：b2b.personKey.sourceKey</li><li>當前架構的關係名稱：人員</li><li>來自引用架構的關係名稱：機會</li></ul>**第二關係**<ul><li>`opportunityKey.sourceKey` 在基類中</li><li>類型：多對一</li><li>引用架構：B2B機會 </li><li>命名空間：B2B機會 </li><li>目標屬性： `opportunityKey.sourceKey`</li><li>當前架構的關係名稱：機會</li><li>來自引用架構的關係名稱：人物</li></ul> |
| B2B活動 | [XDM業務活動](../../../../xdm/classes/b2b/business-campaign.md) | XDM業務活動詳細資訊 | 啟用 | `campaignKey.sourceKey` 在基類中 | B2B活動 | `extSourceSystemAudit.externalKey.sourceKey` 在基類中 | B2B活動 |
| B2B市場活動成員 | [XDM業務活動成員](../../../../xdm/classes/b2b/business-campaign-members.md) | XDM業務活動成員詳細資訊 | 啟用 | `ccampaignMemberKey.sourceKey` 在基類中 | B2B市場活動成員 | `extSourceSystemAudit.externalKey.sourceKey` 在基類中 | B2B市場活動成員 | **第一段關係**<ul><li>`personKey.sourceKey` 在基類中</li><li>類型：多對一</li><li>引用架構：B2B人員</li><li>命名空間：B2B人員</li><li>目標屬性： `b2b.personKey.sourceKey`</li><li>當前架構的關係名稱：人員</li><li>來自引用架構的關係名稱：市場活動</li></ul>**第二關係**<ul><li>`campaignKey.sourceKey` 在基類中</li><li>類型：多對一</li><li>引用架構：B2B活動</li><li>命名空間：B2B活動</li><li>目標屬性： `campaignKey.sourceKey`</li><li>當前架構的關係名稱：活動</li><li>來自引用架構的關係名稱：人物</li></ul> |
| B2B市場營銷清單 | [XDM業務營銷清單](../../../../xdm/classes/b2b/business-marketing-list.md) | None | 啟用 | `marketingListKey.sourceKey` 在基類中 | B2B市場營銷清單 | None | None | None | 靜態清單未從同步 [!DNL Salesforce] 因此沒有第二身份。 |
| B2B市場營銷清單成員 | [XDM業務營銷清單成員](../../../../xdm/classes/b2b/business-marketing-list-members.md) | None | 啟用 | `marketingListMemberKey.sourceKey` 在基類中 | B2B市場營銷清單成員 | None | None | **第一段關係**<ul><li>`PersonKey.sourceKey` 在基類中</li><li>類型：多對一</li><li>引用架構：B2B人員</li><li>命名空間：B2B人員</li><li>目標屬性： `b2b.personKey.sourceKey`</li><li>當前架構的關係名稱：人員</li><li>來自引用架構的關係名稱：市場營銷清單</li></ul>**第二關係**<ul><li>`marketingListKey.sourceKey` 在基類中</li><li>類型：多對一</li><li>引用架構：B2B市場營銷清單</li><li>命名空間：B2B市場營銷清單</li><li>目標屬性： `marketingListKey.sourceKey`</li><li>當前架構的關係名稱：市場營銷清單</li><li>來自引用架構的關係名稱：人物</li></ul> | 靜態清單成員未從同步 [!DNL Salesforce] 因此沒有第二身份。 |
| B2B活動 | [XDM體驗事件](../../../../xdm/classes/experienceevent.md) | <ul><li>訪問Web頁</li><li>新潛在客戶</li><li>轉換潛在顧客</li><li>添加到清單</li><li>從清單中刪除</li><li>添加到機會</li><li>從機會中刪除</li><li>已填寫窗體</li><li>連結按一下</li><li>電子郵件已發送</li><li>已開啟電子郵件</li><li>已按一下電子郵件</li><li>電子郵件已退回</li><li>電子郵件已跳過軟</li><li>取消訂閱電子郵件</li><li>分數已更改</li><li>業務機會已更新</li><li>市場活動進展狀態已更改</li><li>人員標識符</li><li>Marketo網站URL</li><li>有趣的時刻</li><li>呼叫Webhook</li><li>更改市場活動指南</li><li>收入階段已更改</li><li>合併銷售線索</li><li>已傳送電子郵件</li><li>更改市場活動流</li><li>添加到市場活動</li></ul> | 啟用 | `personKey.sourceKey` 人員標識符欄位組 | B2B人員 | None | None | **第一段關係**<ul><li>`listOperations.listKey.sourceKey` 場</li><li>類型：一對一</li><li>引用架構：B2B市場營銷清單</li><li>命名空間：B2B市場營銷清單</li></ul>**第二關係**<ul><li>`opportunityEvent.opportunityKey.sourceKey` 場</li><li>類型：一對一</li><li>引用架構：B2B機會</li><li>命名空間：B2B機會</li></ul>**第三種關係**<ul><li>`leadOperation.campaignProgression.campaignKey.sourceKey` 場</li><li>類型：一對一</li><li>引用架構：B2B活動</li><li>命名空間：B2B活動</li></ul> | `ExperienceEvent` 與實體不同。 體驗事件的身份是執行該活動的人。 |
| B2B帳戶人員關係 | [XDM業務帳戶人員關係](../../../../xdm/classes/b2b/business-account-person-relation.md) | 身分對應 | 啟用 | `accountPersonKey.sourceKey` 在基類中 | B2B帳戶人員關係 | None | None | **第一段關係**<ul><li>`personKey.sourceKey` 在基類中</li><li>類型：多對一</li><li>引用架構：B2B人員</li><li>命名空間：B2B人員</li><li>目標屬性： `b2b.personKey.SourceKey`</li><li>當前架構的關係名稱：人物</li><li>來自引用架構的關係名稱：帳戶</li></ul>**第二關係**<ul><li>`accountKey.sourceKey` 在基類中</li><li>類型：多對一</li><li>引用架構：B2B帳戶</li><li>命名空間：B2B帳戶</li><li>目標屬性： `accountKey.sourceKey`</li><li>當前架構的關係名稱：帳戶</li><li>來自引用架構的關係名稱：人物</li></ul> |

{style="table-layout:auto"}

## 後續步驟

瞭解如何連接 [!DNL Marketo] 資料到平台，請參閱上的教程 [在UI中建立Marketo源連接器](../../../tutorials/ui/create/adobe-applications/marketo.md)。
