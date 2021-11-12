---
title: XDM業務機會人員關係類
description: 本檔案概述Experience Data Model(XDM)中的XDM Business Opportunity Person Relation類別。
exl-id: 7be193d2-52eb-4b28-953b-5e0fc21d8f93
source-git-commit: edf7afc5db219430232a3226dc691570b50a32bd
workflow-type: tm+mt
source-wordcount: '242'
ht-degree: 4%

---

# [!UICONTROL XDM商機人員關係] 類

[!UICONTROL XDM商機人員關係] 是標準的Experience Data Model(XDM)類別，可擷取與業務機會相關聯之人員的最低必要屬性。

![](../../images/classes/b2b/business-opportunity-person-relation.png)

| 屬性 | 資料類型 | 說明 |
| --- | --- | --- |
| `extSourceSystemAudit` | [[!UICONTROL 外部源系統審核屬性]](../../data-types/external-source-system-audit-attributes.md) | 如果業務人員關係來自外部源系統，則此對象捕獲該系統的審計屬性。 |
| `opportunityKey` | [[!UICONTROL B2B源]](../../data-types/b2b-source.md) | 商機 — 人員關係中商機的複合標識符。 |
| `opportunityPersonKey` | [[!UICONTROL B2B源]](../../data-types/b2b-source.md) | 商機 — 人員關係實體的複合標識符。 |
| `personKey` | [[!UICONTROL B2B源]](../../data-types/b2b-source.md) | 機會 — 人員關係中人員的複合標識符。 |
| `_id` | 字串 | 記錄的唯一標識符。 這是系統產生的值，與類別擷取的其他ID欄位不同。 |
| `opportunityID` | 字串 | 業務機會 — 人員關係中業務機會的唯一標識符。 |
| `opportunityPersonID` | 字串 | 機會 — 人員關係實體的唯一標識符 |
| `isPrimary` | 布林值 | 指明此人是否是此機會的主要聯繫人。 |
| `personID` | 字串 | 業務機會 — 人員關係中人員的唯一標識符。 |
| `personRole` | 字串 | 人員在機會 — 人員關係中的角色。 |

{style=&quot;table-layout:auto&quot;}

請參閱 [即時CDP B2B版中的架構關係](../../tutorials/relationship-b2b.md) 了解此類別在概念上如何與其他B2B類別相關，以及如何在Adobe Experience Platform UI中建立這些關係。
