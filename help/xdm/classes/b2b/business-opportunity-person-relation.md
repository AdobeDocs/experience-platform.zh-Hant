---
title: XDM業務機會人員關係類
description: 本文檔概述了「經驗資料模型」(XDM)中的XDM業務機會人員關係類。
exl-id: 7be193d2-52eb-4b28-953b-5e0fc21d8f93
source-git-commit: 34e0381d40f884cd92157d08385d889b1739845f
workflow-type: tm+mt
source-wordcount: '365'
ht-degree: 2%

---

# [!UICONTROL XDM業務機會人員關係] 類

>[!IMPORTANT]
>
>此類旨在供有權訪問 [Adobe Real-time Customer Data PlatformB2B版](../../../rtcdp/b2b-overview.md)。 您必須具有訪問Real-Time CDPB2B版的權限，才能讓此類參與 [即時客戶配置檔案](../../../profile/home.md)。

[!UICONTROL XDM業務機會人員關係] 是標準的體驗資料模型(XDM)類，它捕獲與業務機會關聯的人員的最低要求屬性。

![XDM Business Opportunity Person類的結構，如UI中所示](../../images/classes/b2b/business-opportunity-person-relation.png)

| 屬性 | 資料類型 | 說明 |
| --- | --- | --- |
| `extSourceSystemAudit` | [[!UICONTROL 外部源系統審核屬性]](../../data-types/external-source-system-audit-attributes.md) | 如果業務人員關係來自外部源系統，則此對象將捕獲該系統的審計屬性。 |
| `opportunityKey` | [[!UICONTROL B2B源]](../../data-types/b2b-source.md) | 業務機會 — 人員關係中業務機會的複合標識符。 |
| `opportunityPersonKey` | [[!UICONTROL B2B源]](../../data-types/b2b-source.md) | 機會 — 人員關係實體的組合標識符。 |
| `personKey` | [[!UICONTROL B2B源]](../../data-types/b2b-source.md) | 業務機會 — 人員關係中人員的複合標識符。 |
| `_id` | 字串 | 記錄的唯一標識符。 這是一個系統生成的值，它與類捕獲的其他ID欄位分開。 |
| `isDeleted` | 布林值 | 指示此市場營銷清單實體是否已在Marketo Engage中刪除。<br><br>使用 [Marketo源連接器](../../../sources/connectors/adobe-applications/marketo/marketo.md)，在Marketo刪除的任何記錄將自動反映在即時客戶配置檔案中。 但是，與這些檔案有關的記錄可能仍會在Data Lake中保留。 通過設定 `isDeleted` 至 `true`，可以使用該欄位在查詢資料湖時過濾已從源中刪除的記錄。 |
| `isPrimary` | 布林值 | 指示人員是否是此機會的主要聯繫人。 |
| `opportunityID` | 字串 | 業務機會 — 人員關係中業務機會的唯一標識符。 |
| `opportunityPersonID` | 字串 | 機會 — 人員關係實體的唯一標識符 |
| `personID` | 字串 | 機會 — 人員關係中人員的唯一標識符。 |
| `personRole` | 字串 | 人員在機會 — 人員關係中的角色。 |

{style="table-layout:auto"}

請參閱上的指南 [Real-Time CDPB2B版模式關係](../../tutorials/relationship-b2b.md) 瞭解此類在概念上如何與其他B2B類相關，以及如何在Adobe Experience PlatformUI中建立這些關係。
