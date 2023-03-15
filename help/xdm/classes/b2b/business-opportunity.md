---
title: XDM業務機會類別
description: 本檔案概述Experience Data Model(XDM)中的XDM Business Opportunity類別。
exl-id: d816b0f9-fd37-45da-aa55-247f7f662da0
source-git-commit: 34e0381d40f884cd92157d08385d889b1739845f
workflow-type: tm+mt
source-wordcount: '319'
ht-degree: 3%

---

# [!UICONTROL XDM業務機會] 類

>[!IMPORTANT]
>
>此類別旨在供具有以下權限的組織使用： [Adobe Real-time Customer Data Platform B2B版](../../../rtcdp/b2b-overview.md). 您必須擁有Real-Time CDP B2B版的存取權，才能讓此類別參與 [即時客戶個人檔案](../../../profile/home.md).

[!UICONTROL XDM業務機會] 是標準的Experience Data Model(XDM)類別，可擷取業務機會的最低必要屬性。

![XDM Business Opportunity類別的結構，如UI中所示](../../images/classes/b2b/business-opportunity.png)

| 屬性 | 資料類型 | 說明 |
| --- | --- | --- |
| `accountKey` | [[!UICONTROL B2B源]](../../data-types/b2b-source.md) | 此機會關聯的帳戶的複合標識符。 |
| `extSourceSystemAudit` | [[!UICONTROL 外部源系統審核屬性]](../../data-types/external-source-system-audit-attributes.md) | 如果此機會來自外部源系統，則此對象將捕獲該系統的審核屬性。 |
| `opportunityKey` | [[!UICONTROL B2B源]](../../data-types/b2b-source.md) | 商機實體的複合標識符。 |
| `_id` | 字串 | 記錄的唯一標識符。 這是系統產生的值，與 `opportunityID`. |
| `accountID` | 字串 | 此機會關聯的帳戶的唯一ID。 |
| `isDeleted` | 布林值 | 指出此行銷清單實體是否已在Marketo Engage中刪除。<br><br>使用 [Marketo來源連接器](../../../sources/connectors/adobe-applications/marketo/marketo.md),Marketo中刪除的任何記錄都會自動反映在即時客戶個人檔案中。 不過，與這些設定檔相關的記錄仍可能會保留在Data Lake。 設定 `isDeleted` to `true`，您可以使用欄位來篩選已在查詢資料湖時從來源刪除的記錄。 |
| `opportunityDescription` | 字串 | 商機的說明。 |
| `opportunityID` | 字串 | 商機實體的唯一ID。 |
| `opportunityName` | 字串 | 商機的名稱。 |
| `opportunityStage` | 字串 | 銷售階段。 |
| `opportunityType` | 字串 | 機會的類型。 |

{style="table-layout:auto"}

請參閱 [Real-Time CDP B2B版中的結構關係](../../tutorials/relationship-b2b.md) 了解此類別在概念上如何與其他B2B類別相關，以及如何在Adobe Experience Platform UI中建立這些關係。
