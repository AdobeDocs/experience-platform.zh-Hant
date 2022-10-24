---
title: XDM業務帳戶人員關係類
description: 本檔案概述Experience Data Model(XDM)中的XDM商業帳戶人員關係類別。
exl-id: d51abe9b-d936-4c84-96e2-35a81ca6b67f
source-git-commit: 14e3eff3ea2469023823a35ee1112568f5b5f4f7
workflow-type: tm+mt
source-wordcount: '445'
ht-degree: 3%

---

# [!UICONTROL XDM企業帳戶人員關係] 類

>[!IMPORTANT]
>
>此類別旨在供具有以下權限的組織使用： [Adobe Real-time Customer Data Platform B2B版](../../../rtcdp/b2b-overview.md). 您必須擁有Real-Time CDP B2B版的存取權，才能讓此類別參與 [即時客戶個人檔案](../../../profile/home.md).

[!UICONTROL XDM企業帳戶人員關係] 是標準的Experience Data Model(XDM)類別，可擷取與商業帳戶相關聯之人員的最低必要屬性。

![XDM業務帳戶人員關係類別的結構，如同顯示在UI中](../../images/classes/b2b/business-account-person-relation.png)

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
| `isDeleted` | 布林值 | 指出此帳戶與人員關係是否已在Marketo Engage中刪除。<br><br>使用 [Marketo來源連接器](../../../sources/connectors/adobe-applications/marketo/marketo.md),Marketo中刪除的任何記錄都會自動反映在即時客戶個人檔案中。 不過，與這些設定檔相關的記錄仍可能會保留在Data Lake。 設定 `isDeleted` to `true`，您可以使用欄位來篩選已在查詢資料湖時從來源刪除的記錄。 |
| `isDirect` | 布林值 | 指出這是否為帳戶與人員之間的直接關係。 |
| `isPrimary` | 布林值 | 指出該人員是否為此帳戶的主要聯絡人。 |
| `personID` | 字串 | 帳戶 — 人員關係中人員的唯一標識符。 |
| `personRoles` | 字串陣列 | 列出帳戶 — 人員關係中人員的角色。 |
| `relationEndDate` | DateTime | 帳戶與人員之間的關係結束的日期。 |
| `relationStartDate` | DateTime | 帳戶與人員之間的關係開始的日期。 |
| `relationshipSource` | 字串 | 帳戶 — 人員關係的來源。 |

{style=&quot;table-layout:auto&quot;}

請參閱 [Real-Time CDP B2B版中的結構關係](../../tutorials/relationship-b2b.md) 了解此類別在概念上如何與其他B2B類別相關，以及如何在Adobe Experience Platform UI中建立這些關係。
