---
title: XDM業務機會人員關係類
description: 本檔案概述Experience Data Model(XDM)中的XDM Business Opportunity Person Relation類別。
source-git-commit: 5fd82b02eb25f3d575de695c2f2b14a5e5b18400
workflow-type: tm+mt
source-wordcount: '257'
ht-degree: 2%

---

# [!UICONTROL XDM Business Opportunity Person關] 系類

>[!NOTE]
>
>此類別僅適用於可存取即時客戶資料平台B2B版的組織。

[!UICONTROL XDM Business Opportunity Person Relationship] 是一種標準的Experience Data Model(XDM)類，它捕獲與業務機會關聯的人員的最低必需屬性。

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

請參閱即時CDP B2B版本](../../tutorials/relationship-b2b.md)中的[架構關係指南，了解此類別在概念上如何與其他B2B類別相關，以及如何在Adobe Experience Platform UI中建立這些關係。
