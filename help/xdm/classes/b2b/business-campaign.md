---
title: XDM Business Campaign類別
description: 本檔案概述Experience Data Model(XDM)中的XDM Business Campaign類別。
exl-id: 4e3228a1-74be-43af-b355-45d84afb1611
source-git-commit: b5cdd72238f7b4519de1c789f4294b9698415327
workflow-type: tm+mt
source-wordcount: '194'
ht-degree: 5%

---

# [!UICONTROL XDM業務] 促銷活動類別（測試版）

>[!IMPORTANT]
>
>此類別屬於目前測試版的即時客戶資料平台B2B版。 檔案和功能可能會有所變更。

[!UICONTROL XDM Business Campaign] 是標準的Experience Data Model(XDM)類別，可擷取業務促銷活動的最低必要屬性。

![](../../images/classes/b2b/business-campaign.png)

| 屬性 | 資料類型 | 說明 |
| --- | --- | --- |
| `campaignKey` | [[!UICONTROL B2B源]](../../data-types/b2b-source.md) | 促銷活動實體的複合識別碼。 |
| `extSourceSystemAudit` | [[!UICONTROL 外部源系統審核屬性]](../../data-types/external-source-system-audit-attributes.md) | 如果促銷活動來自外部來源系統，此物件會擷取該系統的稽核屬性。 |
| `_id` | 字串 | 記錄的唯一標識符。 這是系統產生的值，與`campaignID`分開。 |
| `campaignDescription` | 字串 | 促銷活動的說明。 |
| `campaignID` | 字串 | 促銷活動實體的唯一識別碼。 |
| `campaignName` | 字串 | 促銷活動的名稱。 |
| `campaignType` | 字串 | 促銷活動類型或目標對象。 |

{style=&quot;table-layout:auto&quot;}

請參閱即時CDP B2B版本](../../tutorials/relationship-b2b.md)中的[架構關係指南，了解此類別在概念上如何與其他B2B類別相關，以及如何在Adobe Experience Platform UI中建立這些關係。
