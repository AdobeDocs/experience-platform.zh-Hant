---
title: Real-time Customer Data Platform B2B版（測試版）的結構描述
description: 概略說明Real-time Customer Data Platform B2B版本中Experience Data Model(XDM)結構之角色。
exl-id: 3b18d377-108f-443f-86ae-dc7537cf9013
source-git-commit: 6f421a8ae77318ca2598d640cf7e27ea485ec9db
workflow-type: tm+mt
source-wordcount: '219'
ht-degree: 0%

---

# Real-time Customer Data Platform B2B版（測試版）的結構描述

>[!IMPORTANT]
>
>Real-time Customer Data Platform B2B版目前仍在測試中。 檔案和功能可能會有所變更。

Real-time Customer Data Platform B2B版提供數種標準 [Experience Data Model(XDM)類別](../../xdm/schema/composition.md#class) 擷取關於基本B2B資料實體的詳細資訊，例如帳戶、機會、促銷活動等。 此外，即時CDP B2B Edition還允許您定義這些結構之間的多對一關係，以便它們能夠參與高級細分使用案例。

Real-time CDP B2B Edition提供了以下標準類：

* [XDM商業帳戶](../../xdm/classes/b2b/business-account.md)
* [XDM企業帳戶人員關係](../../xdm/classes/b2b/business-account-person-relation.md)
* [XDM商業宣傳](../../xdm/classes/b2b/business-campaign.md)
* [XDM Business Campaign成員](../../xdm/classes/b2b/business-campaign-members.md)
* [XDM業務機會](../../xdm/classes/b2b/business-opportunity.md)
* [XDM商機人員關係](../../xdm/classes/b2b/business-opportunity-person-relation.md)
* [XDM商業行銷清單](../../xdm/classes/b2b/business-marketing-list.md)
* [XDM商業行銷清單成員](../../xdm/classes/b2b/business-marketing-list-members.md)

如需如何在兩個結構之間建立多對一關係的步驟，請參閱以下的教學課程： [定義B2B架構關係](../../xdm/tutorials/relationship-b2b.md).

如果您使用B2B來源連線，則可使用工具自動產生所需的結構及其之間的關係。 請參閱 [B2B命名空間](../../sources/connectors/adobe-applications/marketo/marketo-namespaces.md) ，以取得詳細資訊。
