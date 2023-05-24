---
title: XDM業務帳戶人員關係分類
description: 本文檔概述了「經驗資料模型」(XDM)中的「XDM業務帳戶人員關係」類。
exl-id: d51abe9b-d936-4c84-96e2-35a81ca6b67f
source-git-commit: 34e0381d40f884cd92157d08385d889b1739845f
workflow-type: tm+mt
source-wordcount: '442'
ht-degree: 2%

---

# [!UICONTROL XDM業務帳戶人員關係] 類

>[!IMPORTANT]
>
>此類旨在供有權訪問 [Adobe Real-time Customer Data PlatformB2B版](../../../rtcdp/b2b-overview.md)。 您必須具有訪問Real-Time CDPB2B版的權限，才能讓此類參與 [即時客戶配置檔案](../../../profile/home.md)。

[!UICONTROL XDM業務帳戶人員關係] 是標準的體驗資料模型(XDM)類，它捕獲與業務帳戶關聯的人員的最低要求屬性。

![XDM業務帳戶人員關係類的結構（如UI中所示）](../../images/classes/b2b/business-account-person-relation.png)

| 屬性 | 資料類型 | 說明 |
| --- | --- | --- |
| `accountKey` | [[!UICONTROL B2B源]](../../data-types/b2b-source.md) | 帳戶 — 人員關係中帳戶的組合標識符。 |
| `accountPersonKey` | [[!UICONTROL B2B源]](../../data-types/b2b-source.md) | 帳戶 — 人員關係實體的組合標識符。 |
| `extSourceSystemAudit` | [[!UICONTROL 外部源系統審核屬性]](../../data-types/external-source-system-audit-attributes.md) | 如果帳戶 — 人員關係來自外部源系統，則此對象將捕獲該系統的審計屬性。 |
| `personKey` | [[!UICONTROL B2B源]](../../data-types/b2b-source.md) | 帳戶 — 人員關係中人員的組合標識符。 |
| `_id` | 字串 | 記錄的唯一標識符。 這是一個系統生成的值，它與類捕獲的其他ID欄位分開。 |
| `accountID` | 字串 | 帳戶 — 人員關係中帳戶的唯一標識符。 |
| `accountPersonID` | 字串 | 帳戶 — 人員關係實體的唯一標識符。 |
| `currencyCode` | 字串 | 用於帳戶與人員之間關係的ISO 4217幣種代碼。 |
| `isActive` | 布林值 | 指示帳戶與人員之間的關係是否處於活動狀態。 |
| `isDeleted` | 布林值 | 指示此帳戶 — 人員關係是否已在Marketo Engage中刪除。<br><br>使用 [Marketo源連接器](../../../sources/connectors/adobe-applications/marketo/marketo.md)，在Marketo刪除的任何記錄將自動反映在即時客戶配置檔案中。 但是，與這些檔案有關的記錄可能仍會在Data Lake中保留。 通過設定 `isDeleted` 至 `true`，可以使用該欄位在查詢資料湖時過濾已從源中刪除的記錄。 |
| `isDirect` | 布林值 | 指示這是否是帳戶與人員之間的直接關係。 |
| `isPrimary` | 布林值 | 指示此人是否是此帳戶上的主要聯繫人。 |
| `personID` | 字串 | 帳戶 — 人員關係中人員的唯一標識符。 |
| `personRoles` | 字串陣列 | 列出帳戶 — 人員關係中人員的角色。 |
| `relationEndDate` | 日期時間 | 帳戶與人員之間關係結束的日期。 |
| `relationStartDate` | 日期時間 | 帳戶與人員之間關係開始的日期。 |
| `relationshipSource` | 字串 | 帳戶 — 人員關係的源。 |

{style="table-layout:auto"}

請參閱上的指南 [Real-Time CDPB2B版模式關係](../../tutorials/relationship-b2b.md) 瞭解此類在概念上如何與其他B2B類相關，以及如何在Adobe Experience PlatformUI中建立這些關係。
