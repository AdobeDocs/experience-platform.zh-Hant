---
title: Real-Time Customer Data Platform B2B edition中的結構描述
description: 概述Experience Data Model (XDM)結構描述在Adobe Real-Time Customer Data Platform B2B edition中的角色。
feature: Get Started, Data Management, Schemas
badgeB2B: label="B2B edition" type="Informative" url="https://helpx.adobe.com/tw/legal/product-descriptions/real-time-customer-data-platform-b2b-edition-prime-and-ultimate-packages.html newtab=true"
exl-id: 3b18d377-108f-443f-86ae-dc7537cf9013
source-git-commit: 0191fc8419c696d8cd114a5eb575b8cc0a815a72
workflow-type: tm+mt
source-wordcount: '844'
ht-degree: 8%

---

# Real-Time Customer Data Platform B2B edition中的結構描述

Adobe Real-Time Customer Data Platform B2B edition提供數個標準[體驗資料模型(XDM)類別](../../xdm/schema/composition.md#class)，可擷取基本B2B資料實體的詳細資訊，例如帳戶、商機、行銷活動等。 此外，Real-Time CDP B2B edition可讓您定義這些結構描述之間的多對一關係，讓這些結構描述可以參與進階細分使用案例。

>[!IMPORTANT]
>
>B2B結構描述可用於Experience Platform應用程式(例如，[Customer Journey Analytics B2B edition](https://experienceleague.adobe.com/zh-hant/docs/analytics-platform/using/cja-overview/cja-b2b/cja-b2b-edition))。 <br/>但是，您必須擁有Real-Time CDP B2B edition的存取權，才能讓（設定檔中的） B2B結構描述參與[即時客戶設定檔](../../profile/home.md)。

Real-Time CDP B2B edition提供下列標準類別：

* [XDM商業帳戶](../../xdm/classes/b2b/business-account.md)
* [XDM商業帳戶個人關係](../../xdm/classes/b2b/business-account-person-relation.md)
* [XDM商業活動](../../xdm/classes/b2b/business-campaign.md)
* [XDM商業活動會員](../../xdm/classes/b2b/business-campaign-members.md)
* [XDM商業機會](../../xdm/classes/b2b/business-opportunity.md)
* [XDM商業機會個人關係](../../xdm/classes/b2b/business-opportunity-person-relation.md)
* [XDM業務行銷清單](../../xdm/classes/b2b/business-marketing-list.md)
* [XDM業務行銷清單成員](../../xdm/classes/b2b/business-marketing-list-members.md)

若要瞭解結構描述如何適合您的B2B工作流程，請參閱[端對端教學課程](../b2b-tutorial.md)。

如需如何在兩個結構描述之間建立多對一關係的步驟，請參閱有關[定義B2B結構描述關係](../../xdm/tutorials/relationship-b2b.md)的教學課程。

如果您使用B2B來源連線，則可以使用工具來自動產生所需的結構描述以及它們之間的關係。 如需詳細資訊，請參閱來原始檔中的[B2B名稱空間](../../sources/connectors/adobe-applications/marketo/marketo-namespaces.md)指南。


下表包含有關B2B結構描述的基礎設定的資訊。

>[!NOTE]
>
>請向左/向右捲動以檢視表格的完整內容。

| 結構描述名稱 | 基底類別 | 欄位群組 | 結構描述中的[!DNL Profile] | 主要身分識別 | 主要身分識別命名空間 | 次要身分 | 次要身分名稱空間 | 關係 | 附註 |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| B2B 帳戶 | [XDM商業帳戶](../../xdm/classes/b2b/business-account.md) | XDM商業帳戶細節 | 啟用 | 基底類別中的`accountKey.sourceKey` | B2B 帳戶 | 基底類別中的`extSourceSystemAudit.externalKey.sourceKey` | B2B 帳戶 | <ul><li>XDM商業帳戶詳細資料欄位群組中的`accountParentKey.sourceKey`</li><li>目的地屬性： `/accountKey/sourceKey`</li><li>型別：一對一</li><li>參考結構描述：B2B帳戶</li><li>名稱空間： B2B帳戶</li></ul> |
| B2B人員 | [XDM 個別輪廓](../../xdm/classes/individual-profile.md) | <ul><li>XDM商業人士細節</li><li>XDM商業人士要素</li><li>身分對應</li><li>同意和偏好設定詳細資料</li></ul> | 啟用 | XDM商業人士詳細資料欄位群組中的`b2b.personKey.sourceKey` | B2B人員 | <ol><li>`extSourceSystemAudit.externalKey.sourceKey`個XDM商業人士詳細資料欄位群組</li><li>`workEmail.address`個XDM商業人士詳細資料欄位群組</ol></li> | <ol><li>B2B人員</li><li>電子郵件</li></ol> | <ul><li>`personComponents.sourceAccountKey.sourceKey`個XDM商業人士元件欄位群組</li><li>型別：多對一</li><li>參考結構描述：B2B帳戶</li><li>名稱空間： B2B帳戶</li><li>目的地屬性： accountKey.sourceKey</li><li>來自目前結構描述的關係名稱：帳戶</li><li>來自參照結構描述的關係名稱：人員</li></ul> |
| B2B 機會 | [XDM商機](../../xdm/classes/b2b/business-opportunity.md) | XDM商業機會詳細資料 | 啟用 | 基底類別中的`opportunityKey.sourceKey` | B2B 機會 | 基底類別中的`extSourceSystemAudit.externalKey.sourceKey` | B2B 機會 | <ul><li>基底類別中的`accountKey.sourceKey`</li><li>型別：多對一</li><li>參考結構描述：B2B帳戶</li><li>名稱空間： B2B帳戶</li><li>目的地屬性： `accountKey.sourceKey`</li><li>來自目前結構描述的關係名稱：帳戶</li><li>參考結構描述中的關係名稱：機會</li></ul> |
| B2B機會個人關係 | [XDM商業機會個人關係](../../xdm/classes/b2b/business-opportunity-person-relation.md) | None | 啟用 | 基底類別中的`opportunityPersonKey.sourceKey` | B2B機會個人關係 | | | **第一關聯性**<ul><li>基底類別中的`personKey.sourceKey`</li><li>型別：多對一</li><li>參考結構描述：B2B人員</li><li>名稱空間： B2B人員</li><li>目的地屬性： b2b.personKey.sourceKey</li><li>來自目前結構描述的關係名稱： Person</li><li>參考結構描述中的關係名稱：機會</li></ul>**第二個關聯性**<ul><li>基底類別中的`opportunityKey.sourceKey`</li><li>型別：多對一</li><li>參考結構描述：B2B機會 </li><li>名稱空間： B2B機會 </li><li>目的地屬性： `opportunityKey.sourceKey`</li><li>來自目前結構描述的關係名稱：機會</li><li>來自參照結構描述的關係名稱：人員</li></ul> |
| B2B 行銷活動 | [XDM商業活動](../../xdm/classes/b2b/business-campaign.md) | XDM商業活動細節 | 啟用 | 基底類別中的`campaignKey.sourceKey` | B2B 行銷活動 | | |
| B2B 行銷活動會員 | [XDM商業活動會員](../../xdm/classes/b2b/business-campaign-members.md) | XDM商業活動會員細節 | 啟用 | 基底類別中的`ccampaignMemberKey.sourceKey` | B2B 行銷活動會員 | | | **第一關聯性**<ul><li>基底類別中的`personKey.sourceKey`</li><li>型別：多對一</li><li>參考結構描述：B2B人員</li><li>名稱空間： B2B人員</li><li>目的地屬性： `b2b.personKey.sourceKey`</li><li>來自目前結構描述的關係名稱： Person</li><li>來自參考結構描述的關係名稱：行銷活動</li></ul>**第二個關聯性**<ul><li>基底類別中的`campaignKey.sourceKey`</li><li>型別：多對一</li><li>參考結構描述：B2B行銷活動</li><li>名稱空間： B2B行銷活動</li><li>目的地屬性： `campaignKey.sourceKey`</li><li>來自目前結構的關係名稱：行銷活動</li><li>來自參照結構描述的關係名稱：人員</li></ul> |
| B2B 行銷清單 | [XDM業務行銷清單](../../xdm/classes/b2b/business-marketing-list.md) | None | 啟用 | 基底類別中的`marketingListKey.sourceKey` | B2B 行銷清單 | None | None | None | 靜態清單未從[!DNL Salesforce]同步，因此沒有次要識別碼。 |
| B2B 行銷清單成員 | [XDM業務行銷清單成員](../../xdm/classes/b2b/business-marketing-list-members.md) | None | 啟用 | 基底類別中的`marketingListMemberKey.sourceKey` | B2B 行銷清單成員 | None | None | **第一關聯性**<ul><li>基底類別中的`PersonKey.sourceKey`</li><li>型別：多對一</li><li>參考結構描述：B2B人員</li><li>名稱空間： B2B人員</li><li>目的地屬性： `b2b.personKey.sourceKey`</li><li>來自目前結構描述的關係名稱： Person</li><li>來自參考結構描述的關係名稱：行銷清單</li></ul>**第二個關聯性**<ul><li>基底類別中的`marketingListKey.sourceKey`</li><li>型別：多對一</li><li>參考結構描述：B2B行銷清單</li><li>名稱空間： B2B行銷清單</li><li>目的地屬性： `marketingListKey.sourceKey`</li><li>來自目前結構的關係名稱：行銷清單</li><li>來自參照結構描述的關係名稱：人員</li></ul> | 靜態清單成員未從[!DNL Salesforce]同步，因此沒有次要身分。 |
| B2B帳戶個人關係 | [XDM商業帳戶個人關係](../../xdm/classes/b2b/business-account-person-relation.md) | 身分識別對應 | 啟用 | 基底類別中的`accountPersonKey.sourceKey` | B2B帳戶個人關係 | None | None | **第一關聯性**<ul><li>基底類別中的`personKey.sourceKey`</li><li>型別：多對一</li><li>參考結構描述：B2B人員</li><li>名稱空間： B2B人員</li><li>目的地屬性： `b2b.personKey.SourceKey`</li><li>來自目前結構描述的關係名稱：人員</li><li>來自參照結構描述的關係名稱：帳戶</li></ul>**第二個關聯性**<ul><li>基底類別中的`accountKey.sourceKey`</li><li>型別：多對一</li><li>參考結構描述：B2B帳戶</li><li>名稱空間： B2B帳戶</li><li>目的地屬性： `accountKey.sourceKey`</li><li>來自目前結構描述的關係名稱：帳戶</li><li>來自參照結構描述的關係名稱：人員</li></ul> |

{style="table-layout:auto"}

