---
title: XDM商業帳戶個人關係類別
description: 瞭解Experience Data Model (XDM)中的XDM商業帳戶個人關係類別。
exl-id: d51abe9b-d936-4c84-96e2-35a81ca6b67f
source-git-commit: de8e944cfec3b52d25bb02bcfebe57d6a2a35e39
workflow-type: tm+mt
source-wordcount: '432'
ht-degree: 3%

---

# [!UICONTROL XDM商業帳戶個人關係] 類別

>[!IMPORTANT]
>
>此類別旨在由擁有存取權的組織使用 [Adobe Real-time Customer Data Platform B2B版本](../../../rtcdp/b2b-overview.md). 您必須擁有Real-Time CDP B2B Edition的存取權，此類別才能參與 [即時客戶個人檔案](../../../profile/home.md).

[!UICONTROL XDM商業帳戶個人關係] 是一個標準的體驗資料模型(XDM)類別，可擷取與商業帳戶相關聯之個人的最低要求屬性。

![XDM商業帳戶個人關係類別在UI中的結構](../../images/classes/b2b/business-account-person-relation.png)

| 屬性 | 資料類型 | 說明 |
| --- | --- | --- |
| `accountKey` | [[!UICONTROL B2B來源]](../../data-types/b2b-source.md) | 帳戶 — 個人關係中帳戶的複合識別碼。 |
| `accountPersonKey` | [[!UICONTROL B2B來源]](../../data-types/b2b-source.md) | 帳戶 — 個人關係實體的複合識別碼。 |
| `extSourceSystemAudit` | [[!UICONTROL 外部來源系統稽核屬性]](../../data-types/external-source-system-audit-attributes.md) | 如果帳戶 — 人員關係來自外部來源系統，此物件會擷取該系統的稽核屬性。 |
| `personKey` | [[!UICONTROL B2B來源]](../../data-types/b2b-source.md) | 帳戶 — 個人關係中個人的複合識別碼。 |
| `_id` | 字串 | 紀錄的唯一識別碼。 這是系統產生的值，與類別擷取的其他ID欄位不同。 |
| `accountID` | 字串 | 帳戶 — 個人關係中帳戶的唯一識別碼。 |
| `accountPersonID` | 字串 | 帳戶 — 個人關係實體的唯一識別碼。 |
| `currencyCode` | 字串 | 用於帳戶和個人之間關係的ISO 4217貨幣代碼。 |
| `isActive` | 布林值 | 表示帳戶和個人之間的關係是否有效。 |
| `isDeleted` | 布林值 | 表示此帳戶 — 人員關係是否已在Marketo Engage中刪除。<br><br>使用時 [Marketo來源聯結器](../../../sources/connectors/adobe-applications/marketo/marketo.md)，在Marketo中刪除的任何記錄都會自動反映在即時客戶個人檔案中。 不過，與這些設定檔相關的記錄可能仍會保留在資料湖中。 透過設定 `isDeleted` 至 `true`，您可使用欄位來篩選在查詢資料湖時已從您的來源刪除哪些記錄。 |
| `isDirect` | 布林值 | 指示這是否為帳戶和個人之間的直接關係。 |
| `isPrimary` | 布林值 | 指出此人是否為此帳戶的主要聯絡人。 |
| `personID` | 字串 | 帳戶與個人關係中個人的唯一識別碼。 |
| `personRoles` | 字串陣列 | 列出客戶 — 個人關係中個人的角色。 |
| `relationEndDate` | 日期時間 | 帳戶和個人之間的關係結束的日期。 |
| `relationStartDate` | 日期時間 | 帳戶和個人之間的關係開始的日期。 |
| `relationshipSource` | 字串 | 帳戶 — 個人關係的來源。 |

{style="table-layout:auto"}

請參閱以下指南： [Real-Time CDP B2B Edition中的結構描述關係](../../tutorials/relationship-b2b.md) 瞭解此類別與其他B2B類別在概念上的關聯性，以及如何在Adobe Experience Platform UI中建立這些關聯性。
