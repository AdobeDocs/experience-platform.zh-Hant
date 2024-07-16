---
title: Real-time Customer Data Platform B2B版本中的結構描述
description: 概述Adobe Real-time Customer Data Platform B2B Edition中Experience Data Model (XDM)結構描述的作用。
feature: Get Started, Data Management, Schemas
badgeB2B: label="B2B版本" type="Informative" url="https://helpx.adobe.com/legal/product-descriptions/real-time-customer-data-platform-b2b-edition-prime-and-ultimate-packages.html newtab=true"
exl-id: 3b18d377-108f-443f-86ae-dc7537cf9013
source-git-commit: db57fa753a3980dca671d476521f9849147880f1
workflow-type: tm+mt
source-wordcount: '229'
ht-degree: 13%

---

# Real-time Customer Data Platform B2B版本中的結構描述

Adobe Real-time Customer Data Platform B2B Edition提供數個標準[體驗資料模型(XDM)類別](../../xdm/schema/composition.md#class)，可擷取基本B2B資料實體的詳細資訊，例如帳戶、商機、行銷活動等。 此外，Real-Time CDP B2B Edition可讓您定義這些結構描述之間的多對一關係，以便他們參與進階細分使用案例。

>[!IMPORTANT]
>
>您必須能存取Real-Time CDP B2B Edition，B2B結構描述才能參與[即時客戶設定檔](../../profile/home.md)。

Real-Time CDP B2B Edition提供下列標準類別：

* [XDM 企業帳戶](../../xdm/classes/b2b/business-account.md)
* [XDM 商業帳戶個人關係](../../xdm/classes/b2b/business-account-person-relation.md)
* [XDM 商業活動](../../xdm/classes/b2b/business-campaign.md)
* [XDM 商業活動會員](../../xdm/classes/b2b/business-campaign-members.md)
* [XDM 商業機會](../../xdm/classes/b2b/business-opportunity.md)
* [XDM 商業機會個人關係](../../xdm/classes/b2b/business-opportunity-person-relation.md)
* [XDM 業務行銷清單](../../xdm/classes/b2b/business-marketing-list.md)
* [XDM 業務行銷清單會員](../../xdm/classes/b2b/business-marketing-list-members.md)

若要瞭解結構描述如何適合您的B2B工作流程，請參閱[端對端教學課程](../b2b-tutorial.md)。

如需如何在兩個結構描述之間建立多對一關係的步驟，請參閱有關[定義B2B結構描述關係](../../xdm/tutorials/relationship-b2b.md)的教學課程。

如果您使用B2B來源連線，則可以使用工具來自動產生所需的結構描述以及它們之間的關係。 如需詳細資訊，請參閱來原始檔中的[B2B名稱空間](../../sources/connectors/adobe-applications/marketo/marketo-namespaces.md)指南。
