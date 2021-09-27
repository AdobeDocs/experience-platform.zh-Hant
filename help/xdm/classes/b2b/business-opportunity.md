---
title: XDM業務機會類
description: 本檔案概述Experience Data Model(XDM)中的XDM Business Opportunity類別。
source-git-commit: 19bb39b66f3a3eb93fd0138ac021568021d77b0f
workflow-type: tm+mt
source-wordcount: '176'
ht-degree: 5%

---

# [!UICONTROL XDM Business ] Popityclass

>[!NOTE]
>
>此類別僅適用於可存取B2B版即時客戶資料平台的組織。

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
