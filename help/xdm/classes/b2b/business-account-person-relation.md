---
title: XDM業務帳戶人員關係類
description: 本檔案概述Experience Data Model(XDM)中的XDM商業帳戶人員關係類別。
source-git-commit: d83ad2870b6099d3c6359dcc7cd000ecad8a238f
workflow-type: tm+mt
source-wordcount: '334'
ht-degree: 2%

---

# [!UICONTROL XDM業務客戶人] 員關係類別（測試版）

>[!IMPORTANT]
>
>此類別屬於目前測試版的即時客戶資料平台B2B版。 檔案和功能可能會有所變更。

[!UICONTROL XDM企業帳戶人] 員關係是標準的體驗資料模型(XDM)類別，可擷取與企業帳戶相關聯的人員所需的最低屬性。

![](../../images/classes/b2b/business-account-person-relation.png)

| 屬性 | 資料類型 | 說明 |
| --- | --- | --- |
| `accountKey` | [[!UICONTROL B2B源]](../../data-types/b2b-source.md) | 帳戶 — 人員關係中帳戶的複合識別碼。 |
| `accountPersonKey` | [[!UICONTROL B2B源]](../../data-types/b2b-source.md) | 帳戶 — 人員關係實體的複合標識符。 |
| `extSourceSystemAudit` | [[!UICONTROL 外部源系統審核屬性]](../../data-types/external-source-system-audit-attributes.md) | 如果帳戶 — 人員關係來自外部源系統，則此對象將捕獲該系統的審核屬性。 |
| `personKey` | [[!UICONTROL B2B源]](../../data-types/b2b-source.md) | 帳戶 — 人員關係中人員的複合標識符。 |
| `_id` | 字串 | 記錄的唯一標識符。 這是系統產生的值，與類別擷取的其他ID欄位不同。 |
| `accountID` | 字串 | 帳戶 — 人員關係中帳戶的唯一識別碼。 |
| `accountPersonID` | 字串 | 帳戶 — 人員關係實體的唯一標識符。 |
| `currencyCode` | 字串 | 用於帳戶與人員之間關係的ISO 4217貨幣代碼。 |
| `isActive` | 布林值 | 指示帳戶與人員之間的關係是否有效。 |
| `isDirect` | 布林值 | 指出這是否為帳戶與人員之間的直接關係。 |
| `isPrimary` | 布林值 | 指出該人員是否為此帳戶的主要聯絡人。 |
| `personID` | 字串 | 帳戶 — 人員關係中人員的唯一標識符。 |
| `personRole` | 字串 | 人員在帳戶 — 人員關係中的角色。 |
| `relationEndDate` | DateTime | 帳戶與人員之間的關係結束的日期。 |
| `relationStartDate` | DateTime | 帳戶與人員之間的關係開始的日期。 |

請參閱即時CDP B2B版本](../../tutorials/relationship-b2b.md)中的[架構關係指南，了解此類別在概念上如何與其他B2B類別相關，以及如何在Adobe Experience Platform UI中建立這些關係。
