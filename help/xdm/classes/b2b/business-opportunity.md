---
title: XDM業務機會類
description: 本檔案概述Experience Data Model(XDM)中的XDM Business Opportunity類別。
exl-id: d816b0f9-fd37-45da-aa55-247f7f662da0
source-git-commit: b5cdd72238f7b4519de1c789f4294b9698415327
workflow-type: tm+mt
source-wordcount: '225'
ht-degree: 5%

---

# [!UICONTROL XDM Business ] Popityclass（測試版）

>[!IMPORTANT]
>
>此類別屬於目前測試版的即時客戶資料平台B2B版。 檔案和功能可能會有所變更。

[!UICONTROL XDM Business Optimity是] 標準的Experience Data Model(XDM)類別，可擷取業務機會的最低必要屬性。

![](../../images/classes/b2b/business-opportunity.png)

| 屬性 | 資料類型 | 說明 |
| --- | --- | --- |
| `accountKey` | [[!UICONTROL B2B源]](../../data-types/b2b-source.md) | 此機會關聯的帳戶的複合標識符。 |
| `extSourceSystemAudit` | [[!UICONTROL 外部源系統審核屬性]](../../data-types/external-source-system-audit-attributes.md) | 如果此機會來自外部源系統，則此對象將捕獲該系統的審核屬性。 |
| `opportunityKey` | [[!UICONTROL B2B源]](../../data-types/b2b-source.md) | 商機實體的複合標識符。 |
| `_id` | 字串 | 記錄的唯一標識符。 這是系統產生的值，與`opportunityID`分開。 |
| `accountID` | 字串 | 此機會關聯的帳戶的唯一ID。 |
| `opportunityDescription` | 字串 | 商機的說明。 |
| `opportunityID` | 字串 | 商機實體的唯一ID。 |
| `opportunityName` | 字串 | 商機的名稱。 |
| `opportunityStage` | 字串 | 銷售階段。 |
| `opportunityType` | 字串 | 機會的類型。 |

{style=&quot;table-layout:auto&quot;}

請參閱即時CDP B2B版本](../../tutorials/relationship-b2b.md)中的[架構關係指南，了解此類別在概念上如何與其他B2B類別相關，以及如何在Adobe Experience Platform UI中建立這些關係。
