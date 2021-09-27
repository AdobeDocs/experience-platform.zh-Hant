---
title: 即時客戶資料平台B2B版中的結構
description: 概略說明Experience Data Model(XDM)結構在即時客戶資料平台B2B版本中的角色。
source-git-commit: d83ad2870b6099d3c6359dcc7cd000ecad8a238f
workflow-type: tm+mt
source-wordcount: '218'
ht-degree: 0%

---

# 即時客戶資料平台B2B版（測試版）的結構描述

>[!IMPORTANT]
>
>即時客戶資料平台B2B版目前仍在測試中。 檔案和功能可能會有所變更。

即時客戶資料平台B2B版提供數種標準[體驗資料模型(XDM)類別](../../xdm/schema/composition.md#class)，可擷取關於基本B2B資料實體（例如帳戶、機會、促銷活動等）的詳細資訊。 此外，即時CDP B2B Edition還允許您定義這些結構之間的多對一關係，以便它們能夠參與高級細分使用案例。

Real-time CDP B2B Edition提供了以下標準類：

* [XDM商業帳戶](../../xdm/classes/b2b/business-account.md)
* [XDM企業帳戶人員關係](../../xdm/classes/b2b/business-account-person-relation.md)
* [XDM商業宣傳](../../xdm/classes/b2b/business-campaign.md)
* [XDM Business Campaign成員](../../xdm/classes/b2b/business-campaign-members.md)
* [XDM業務機會](../../xdm/classes/b2b/business-opportunity.md)
* [XDM商機人員關係](../../xdm/classes/b2b/business-opportunity-person-relation.md)
* [XDM商業行銷清單](../../xdm/classes/b2b/business-marketing-list.md)
* [XDM商業行銷清單成員](../../xdm/classes/b2b/business-marketing-list-members.md)

有關如何在兩個架構之間建立多對一關係的步驟，請參閱定義B2B架構關係](../../xdm/tutorials/relationship-b2b.md)的教學課程。[

如果您使用B2B來源連線，則可使用工具自動產生所需的結構及其之間的關係。 如需詳細資訊，請參閱來源檔案中[B2B命名空間](../../sources/connectors/adobe-applications/marketo/marketo-namespaces.md)的指南。
