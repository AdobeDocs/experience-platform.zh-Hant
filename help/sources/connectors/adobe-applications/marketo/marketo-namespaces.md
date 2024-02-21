---
title: B2B名稱空間和結構描述
description: 本檔案提供建立B2B來源聯結器時所需的自訂名稱空間概觀。
exl-id: f1592be5-987e-41b8-9844-9dea5bd452b9
source-git-commit: 5e8bb04ca18159eab98b2f7f0bba8cb1488a1f26
workflow-type: tm+mt
source-wordcount: '1620'
ht-degree: 3%

---

# B2B名稱空間和結構描述

>[!NOTE]
>
>您可以在Adobe Experience Platform UI中使用範本，快速建立B2B和B2C資料的資產。 如需詳細資訊，請閱讀以下指南： [在Platform UI中使用範本](../../../tutorials/ui/templates.md).

本檔案提供將用於與B2B來源搭配的名稱空間和結構描述的基礎設定資訊。 本檔案也提供設定Postman自動化公用程式（產生B2B名稱空間和結構描述所需）的相關詳細資訊。

>[!IMPORTANT]
>
>您必須有權存取 [Adobe Real-time Customer Data Platform B2B版本](../../../../rtcdp/b2b-overview.md) 以便B2B結構描述參與 [即時客戶個人檔案](../../../../profile/home.md).

## 設定B2B名稱空間和結構描述自動產生公用程式

使用B2B名稱空間和結構描述自動產生公用程式的第一個步驟，就是設定您的Platform開發人員主控台，以及 [!DNL Postman] 環境。

- 您可以從這裡下載名稱空間和結構描述自動產生公用程式集合和環境 [GitHub存放庫](https://github.com/adobe/experience-platform-postman-samples/tree/master/Postman%20Collections/CDP%20Namespaces%20and%20Schemas%20Utility).
- 如需有關使用Platform API的資訊，包括如何收集所需標題的值以及讀取範例API呼叫的詳細資訊，請參閱以下指南： [Platform API快速入門](../../../../landing/api-guide.md).
- 如需如何產生Platform API認證的詳細資訊，請參閱以下教學課程： [驗證及存取Experience PlatformAPI](../../../../landing/api-authentication.md).
- 如需如何設定的詳細資訊 [!DNL Postman] 若為Platform API，請參閱以下教學課程： [設定開發人員控制檯和 [!DNL Postman]](../../../../landing/postman.md).

使用平台開發人員主控台及 [!DNL Postman] 設定，您現在可以開始將適當的環境值套用至 [!DNL Postman] 環境。

下表包含範例值，以及有關填入 [!DNL Postman] 環境：

| 變數 | 說明 | 範例 |
| --- | --- | --- |
| `CLIENT_SECRET` | 用於產生 `{ACCESS_TOKEN}`. 請參閱上的教學課程 [驗證及存取Experience PlatformAPI](../../../../landing/api-authentication.md) 以取得如何擷取您的 `{CLIENT_SECRET}`. | `{CLIENT_SECRET}` |
| `JWT_TOKEN` | JSON Web權杖(JWT)是驗證認證，用於產生您的 {ACCESS_TOKEN}. 請參閱上的教學課程 [驗證及存取Experience PlatformAPI](../../../../landing/api-authentication.md) 以取得如何產生 `{JWT_TOKEN}`. | `{JWT_TOKEN}` |
| `API_KEY` | 用於驗證對Experience Platform API的呼叫的唯一識別碼。 請參閱上的教學課程 [驗證及存取Experience PlatformAPI](../../../../landing/api-authentication.md) 以取得如何擷取您的 `{API_KEY}`. | `c8d9a2f5c1e03789bd22e8efdd1bdc1b` |
| `ACCESS_TOKEN` | 完成對Experience Platform API的呼叫所需的授權權杖。 請參閱上的教學課程 [驗證及存取Experience PlatformAPI](../../../../landing/api-authentication.md) 以取得如何擷取您的 `{ACCESS_TOKEN}`. | `Bearer {ACCESS_TOKEN}` |
| `META_SCOPE` | 關於 [!DNL Marketo]，此值為固定值，一律設為： `ent_dataservices_sdk`. | `ent_dataservices_sdk` |
| `CONTAINER_ID` | 此 `global` container保有所有標準Adobe和Experience Platform合作夥伴提供的類別、結構描述欄位群組、資料型別和結構描述。 關於 [!DNL Marketo]，此值為固定值，一律設為 `global`. | `global` |
| `PRIVATE_KEY` | 用來驗證您的身分的認證 [!DNL Postman] 執行個體以Experience PlatformAPI。 請參閱有關設定開發人員控制檯的教學課程，並且 [設定開發人員控制檯和 [!DNL Postman]](../../../../landing/postman.md) 以取得如何擷取您的 {PRIVATE_KEY}. | `{PRIVATE_KEY}` |
| `TECHNICAL_ACCOUNT_ID` | 用來整合至Adobe I/O的認證。 | `D42AEVJZTTJC6LZADUBVPA15@techacct.adobe.com` |
| `IMS` | Identity Management系統(IMS)提供驗證Adobe服務的架構。 關於 [!DNL Marketo]，此值為固定值，且一律設為： `ims-na1.adobelogin.com`. | `ims-na1.adobelogin.com` |
| `IMS_ORG` | 企業實體，可以擁有或授權產品及服務並允許存取其成員。 請參閱上的教學課程 [設定開發人員控制檯和 [!DNL Postman]](../../../../landing/postman.md) 以取得如何擷取您的 `{ORG_ID}` 資訊。 | `ABCEH0D9KX6A7WA7ATQE0TE@adobeOrg` |
| `SANDBOX_NAME` | 您正在使用的虛擬沙箱分割的名稱。 | `prod` |
| `TENANT_ID` | ID，用來確保您建立的資源已正確命名且包含在您的組織內。 | `b2bcdpproductiontest` |
| `PLATFORM_URL` | 您對其進行API呼叫的URL端點。 此值為固定值，且一律設為： `http://platform.adobe.io/`. | `http://platform.adobe.io/` |

{style="table-layout:auto"}

### 執行指令碼

使用您的 [!DNL Postman] 收集和環境設定，您現在可以透過以下執行指令碼： [!DNL Postman] 介面。

在 [!DNL Postman] 介面，選取自動產生器公用程式的根資料夾，然後選取 **[!DNL Run]** 從頂端標題。

![root-folder](../images/marketo/root-folder.png)

此 [!DNL Runner] 介面出現。 從這裡，確定已選取所有核取方塊，然後選取 **[!DNL Run Namespaces and Schemas Autogeneration Utility]**.

![執行產生器](../images/marketo/run-generator.png)

成功的請求會建立B2B所需的名稱空間和結構描述。

## B2B名稱空間

身分名稱空間是的元件 [[!DNL Identity Service]](../../../../identity-service/home.md) 這有助於區分身分的上下文。 完整身分包含身分值和名稱空間。 閱讀 [名稱空間概觀](../../../../identity-service/features/namespaces.md) 以取得詳細資訊。

B2B名稱空間會用於實體的主要身分識別中。

下表包含有關B2B名稱空間的基礎設定的資訊。

>[!NOTE]
>
>請向左/向右捲動以檢視表格的完整內容。

| 顯示名稱 | 身分識別符號 | 身分類型 |
| --- | --- | --- |
| B2B人員 | `b2b_person` | `CROSS_DEVICE` |
| B2B帳戶 | `b2b_account` | `B2B_ACCOUNT` |
| B2B機會 | `b2b_opportunity` | `B2B_OPPORTUNITY` |
| B2B機會個人關係 | `b2b_opportunity_person_relation` | `B2B_OPPORTUNITY_PERSON` |
| B2B行銷活動 | `b2b_campaign` | `B2B_CAMPAIGN` |
| B2B行銷活動會員 | `b2b_campaign_member` | `B2B_CAMPAIGN_MEMBER` |
| B2B行銷清單 | `b2b_marketing_list` | `B2B_MARKETING_LIST` |
| B2B行銷清單成員 | `b2b_marketing_list_member` | `B2B_MARKETING_LIST_MEMBER` |
| B2B帳戶個人關係 | `b2b_account_person_relation` | `B2B_ACCOUNT_PERSON` |

{style="table-layout:auto"}

## B2B結構描述

Experience Platform 會使用結構，以一致且可重複使用的方式說明資料結構。藉由定義跨系統的一致資料，將更容易保留意義，進而從資料中獲得價值。

在將資料擷取到Platform之前，必須組成結構描述資料的結構並對可包含在每個欄位中的資料型別提供限制。 結構描述包含一個基底類別和零個或多個結構描述欄位群組。

如需結構描述組合模型的詳細資訊，包括設計原則和最佳實務，請參閱 [結構描述組合的基本面](../../../../xdm/schema/composition.md).

下表包含有關B2B結構描述的基礎設定的資訊。

>[!NOTE]
>
>請向左/向右捲動以檢視表格的完整內容。

| 方案名稱 | 基底類別 | 欄位群組 | [!DNL Profile] 在結構描述中 | 主要身分識別 | 主要身分名稱空間 | 次要身分 | 次要身分名稱空間 | 關係 | 附註 |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| B2B帳戶 | [XDM商業帳戶](../../../../xdm/classes/b2b/business-account.md) | XDM商業帳戶細節 | 啟用 | `accountKey.sourceKey` 在基底類別中 | B2B帳戶 | `extSourceSystemAudit.externalKey.sourceKey` 在基底類別中 | B2B帳戶 | <ul><li>`accountParentKey.sourceKey` 在XDM商業帳戶詳細資訊欄位群組中</li><li>目的地屬性： `/accountKey/sourceKey`</li><li>型別：一對一</li><li>參考結構描述：B2B帳戶</li><li>名稱空間： B2B帳戶</li></ul> |
| B2B人員 | [XDM 個別設定檔](../../../../xdm/classes/individual-profile.md) | <ul><li>XDM商業人士細節</li><li>XDM商業人士要素</li><li>身分對應</li><li>同意和偏好設定詳細資料</li></ul> | 啟用 | `b2b.personKey.sourceKey` 在XDM商業人士詳細資料欄位群組中 | B2B人員 | <ol><li>`extSourceSystemAudit.externalKey.sourceKey` 「XDM商業人士詳細資訊」欄位群組的</li><li>`workEmail.address` 「XDM商業人士詳細資訊」欄位群組的</ol></li> | <ol><li>B2B人員</li><li>電子郵件</li></ol> | <ul><li>`personComponents.sourceAccountKey.sourceKey` 「XDM商業人士要素」欄位群組</li><li>型別：多對一</li><li>參考結構描述：B2B帳戶</li><li>名稱空間： B2B帳戶</li><li>目的地屬性： accountKey.sourceKey</li><li>來自目前結構描述的關係名稱：帳戶</li><li>來自參照結構描述的關係名稱：人員</li></ul> |
| B2B機會 | [XDM商業機會](../../../../xdm/classes/b2b/business-opportunity.md) | XDM商業機會詳細資料 | 啟用 | `opportunityKey.sourceKey` 在基底類別中 | B2B機會 | `extSourceSystemAudit.externalKey.sourceKey` 在基底類別中 | B2B機會 | <ul><li>`accountKey.sourceKey` 在基底類別中</li><li>型別：多對一</li><li>參考結構描述：B2B帳戶</li><li>名稱空間： B2B帳戶</li><li>目的地屬性： `accountKey.sourceKey`</li><li>來自目前結構描述的關係名稱：帳戶</li><li>參考結構描述中的關係名稱：機會</li></ul> |
| B2B機會個人關係 | [XDM商業機會個人關係](../../../../xdm/classes/b2b/business-opportunity-person-relation.md) | None | 啟用 | `opportunityPersonKey.sourceKey` 在基底類別中 | B2B機會個人關係 | `extSourceSystemAudit.externalKey.sourceKey` 在基底類別中 | B2B機會個人關係 | **第一個關係**<ul><li>`personKey.sourceKey` 在基底類別中</li><li>型別：多對一</li><li>參考結構描述：B2B人員</li><li>名稱空間： B2B人員</li><li>目的地屬性： b2b.personKey.sourceKey</li><li>來自目前結構描述的關係名稱： Person</li><li>參考結構描述中的關係名稱：機會</li></ul>**第二個關係**<ul><li>`opportunityKey.sourceKey` 在基底類別中</li><li>型別：多對一</li><li>參考結構描述：B2B機會 </li><li>名稱空間： B2B機會 </li><li>目的地屬性： `opportunityKey.sourceKey`</li><li>來自目前結構描述的關係名稱：機會</li><li>來自參照結構描述的關係名稱：人員</li></ul> |
| B2B行銷活動 | [XDM商業活動](../../../../xdm/classes/b2b/business-campaign.md) | XDM商業活動細節 | 啟用 | `campaignKey.sourceKey` 在基底類別中 | B2B行銷活動 | `extSourceSystemAudit.externalKey.sourceKey` 在基底類別中 | B2B行銷活動 |
| B2B行銷活動會員 | [XDM商業活動會員](../../../../xdm/classes/b2b/business-campaign-members.md) | XDM商業活動會員細節 | 啟用 | `ccampaignMemberKey.sourceKey` 在基底類別中 | B2B行銷活動會員 | `extSourceSystemAudit.externalKey.sourceKey` 在基底類別中 | B2B行銷活動會員 | **第一個關係**<ul><li>`personKey.sourceKey` 在基底類別中</li><li>型別：多對一</li><li>參考結構描述：B2B人員</li><li>名稱空間： B2B人員</li><li>目的地屬性： `b2b.personKey.sourceKey`</li><li>來自目前結構描述的關係名稱： Person</li><li>來自參考結構描述的關係名稱：行銷活動</li></ul>**第二個關係**<ul><li>`campaignKey.sourceKey` 在基底類別中</li><li>型別：多對一</li><li>參考結構描述：B2B行銷活動</li><li>名稱空間： B2B行銷活動</li><li>目的地屬性： `campaignKey.sourceKey`</li><li>來自目前結構的關係名稱：行銷活動</li><li>來自參照結構描述的關係名稱：人員</li></ul> |
| B2B行銷清單 | [XDM業務行銷清單](../../../../xdm/classes/b2b/business-marketing-list.md) | None | 啟用 | `marketingListKey.sourceKey` 在基底類別中 | B2B行銷清單 | None | None | None | 靜態清單未同步自 [!DNL Salesforce] 因此沒有次要身分。 |
| B2B行銷清單成員 | [XDM業務行銷清單成員](../../../../xdm/classes/b2b/business-marketing-list-members.md) | None | 啟用 | `marketingListMemberKey.sourceKey` 在基底類別中 | B2B行銷清單成員 | None | None | **第一個關係**<ul><li>`PersonKey.sourceKey` 在基底類別中</li><li>型別：多對一</li><li>參考結構描述：B2B人員</li><li>名稱空間： B2B人員</li><li>目的地屬性： `b2b.personKey.sourceKey`</li><li>來自目前結構描述的關係名稱： Person</li><li>來自參考結構描述的關係名稱：行銷清單</li></ul>**第二個關係**<ul><li>`marketingListKey.sourceKey` 在基底類別中</li><li>型別：多對一</li><li>參考結構描述：B2B行銷清單</li><li>名稱空間： B2B行銷清單</li><li>目的地屬性： `marketingListKey.sourceKey`</li><li>來自目前結構的關係名稱：行銷清單</li><li>來自參照結構描述的關係名稱：人員</li></ul> | 靜態清單成員未同步自 [!DNL Salesforce] 因此沒有次要身分。 |
| B2B活動 | [XDM ExperienceEvent](../../../../xdm/classes/experienceevent.md) | <ul><li>造訪網頁</li><li>新銷售機會</li><li>轉換潛在客戶</li><li>新增至清單</li><li>從清單移除</li><li>新增至商機</li><li>從機會移除</li><li>表單已填寫</li><li>連結點按次數</li><li>電子郵件已傳遞</li><li>電子郵件已開啟</li><li>電子郵件已點按</li><li>電子郵件已退回</li><li>電子郵件已軟退回</li><li>電子郵件已取消訂閱</li><li>分數已變更</li><li>機會已更新</li><li>促銷活動進度變更中的狀態</li><li>個人識別碼</li><li>Marketo網頁URL</li><li>有趣的時刻</li><li>呼叫Webhook</li><li>變更促銷活動步調</li><li>收入階段已變更</li><li>合併銷售機會</li><li>已傳送電子郵件</li><li>變更促銷活動資料流</li><li>新增至行銷活動</li></ul> | 啟用 | `personKey.sourceKey` 個人識別碼欄位群組 | B2B人員 | None | None | **第一個關係**<ul><li>`listOperations.listKey.sourceKey` 欄位</li><li>型別：一對一</li><li>參考結構描述：B2B行銷清單</li><li>名稱空間： B2B行銷清單</li></ul>**第二個關係**<ul><li>`opportunityEvent.opportunityKey.sourceKey` 欄位</li><li>型別：一對一</li><li>參考結構描述：B2B機會</li><li>名稱空間： B2B機會</li></ul>**第三個關係**<ul><li>`leadOperation.campaignProgression.campaignKey.sourceKey` 欄位</li><li>型別：一對一</li><li>參考結構描述：B2B行銷活動</li><li>名稱空間： B2B行銷活動</li></ul> | `ExperienceEvent` 與實體不同。 體驗事件的身分識別是執行活動的人員。 |
| B2B帳戶個人關係 | [XDM商業帳戶個人關係](../../../../xdm/classes/b2b/business-account-person-relation.md) | 身分對應 | 啟用 | `accountPersonKey.sourceKey` 在基底類別中 | B2B帳戶個人關係 | None | None | **第一個關係**<ul><li>`personKey.sourceKey` 在基底類別中</li><li>型別：多對一</li><li>參考結構描述：B2B人員</li><li>名稱空間： B2B人員</li><li>目的地屬性： `b2b.personKey.SourceKey`</li><li>來自目前結構描述的關係名稱：人員</li><li>來自參照結構描述的關係名稱：帳戶</li></ul>**第二個關係**<ul><li>`accountKey.sourceKey` 在基底類別中</li><li>型別：多對一</li><li>參考結構描述：B2B帳戶</li><li>名稱空間： B2B帳戶</li><li>目的地屬性： `accountKey.sourceKey`</li><li>來自目前結構描述的關係名稱：帳戶</li><li>來自參照結構描述的關係名稱：人員</li></ul> |

{style="table-layout:auto"}

## 後續步驟

若要瞭解如何連結 [!DNL Marketo] 資料到Platform，請參閱上的教學課程 [在UI中建立Marketo來源聯結器](../../../tutorials/ui/create/adobe-applications/marketo.md).
