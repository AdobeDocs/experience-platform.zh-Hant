---
title: XDM業務帳戶人員關係類
description: 本檔案概述Experience Data Model(XDM)中的XDM商業帳戶人員關係類別。
exl-id: d51abe9b-d936-4c84-96e2-35a81ca6b67f
source-git-commit: 8718512a9768158183b9fb6b9e336081e47cd889
workflow-type: tm+mt
source-wordcount: '349'
ht-degree: 3%

---

# [!UICONTROL XDM企業帳戶人員關係] 類

>[!IMPORTANT]
>
>此類別旨在供具有以下權限的組織使用： [Real-time Customer Data Platform B2B版](../../../rtcdp/b2b-overview.md). 您必須擁有Real-time CDP B2B Edition的訪問權限，才能讓此類參與 [即時客戶個人檔案](../../../profile/home.md).

[!UICONTROL XDM企業帳戶人員關係] 是標準的Experience Data Model(XDM)類別，可擷取與商業帳戶相關聯之人員的最低必要屬性。

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

{style=&quot;table-layout:auto&quot;}

請參閱 [即時CDP B2B版中的架構關係](../../tutorials/relationship-b2b.md) 了解此類別在概念上如何與其他B2B類別相關，以及如何在Adobe Experience Platform UI中建立這些關係。
