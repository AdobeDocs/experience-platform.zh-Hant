---
title: Real-time Customer Data PlatformB2B版中的架構
description: Adobe Real-time Customer Data PlatformB2B版中體驗資料模型(XDM)架構的角色概述。
exl-id: 3b18d377-108f-443f-86ae-dc7537cf9013
source-git-commit: 34e0381d40f884cd92157d08385d889b1739845f
workflow-type: tm+mt
source-wordcount: '237'
ht-degree: 0%

---

# Real-time Customer Data PlatformB2B版中的架構

Adobe Real-time Customer Data PlatformB2B版提供 [體驗資料模型(XDM)類](../../xdm/schema/composition.md#class) 捕獲關於基本B2B資料實體的詳細資訊，如帳戶、機會、市場活動等。 此外，Real-Time CDPB2B版允許您定義這些架構之間的多對一關係，以便它們能夠參與高級細分使用案例。

>[!IMPORTANT]
>
>您必須具有訪問Real-Time CDPB2B版的權限，才能讓B2B架構參與 [即時客戶配置檔案](../../profile/home.md)。

Real-Time CDPB2B版提供以下標準類：

* [XDM業務客戶](../../xdm/classes/b2b/business-account.md)
* [XDM業務帳戶人員關係](../../xdm/classes/b2b/business-account-person-relation.md)
* [XDM業務活動](../../xdm/classes/b2b/business-campaign.md)
* [XDM業務活動成員](../../xdm/classes/b2b/business-campaign-members.md)
* [XDM業務機會](../../xdm/classes/b2b/business-opportunity.md)
* [XDM業務機會人員關係](../../xdm/classes/b2b/business-opportunity-person-relation.md)
* [XDM業務營銷清單](../../xdm/classes/b2b/business-marketing-list.md)
* [XDM業務營銷清單成員](../../xdm/classes/b2b/business-marketing-list-members.md)

要瞭解架構如何適用於您的B2B工作流，請參閱 [端到端教程](../b2b-tutorial.md)。

有關如何在兩個架構之間建立多對一關係的步驟，請參閱上的教程 [定義B2B架構關係](../../xdm/tutorials/relationship-b2b.md)。

如果使用的是B2B源連接，則可以使用工具自動生成所需的方案及其之間的關係。 請參閱上的指南 [B2B命名空間](../../sources/connectors/adobe-applications/marketo/marketo-namespaces.md) 的雙曲餘切值。
