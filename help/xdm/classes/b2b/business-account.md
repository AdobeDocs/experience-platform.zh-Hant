---
title: XDM業務帳戶類別
description: 本檔案概述Experience Data Model(XDM)中的XDM商業帳戶類別。
exl-id: abe4c919-a680-4aad-918e-6e56cae8bd4d
source-git-commit: edf7afc5db219430232a3226dc691570b50a32bd
workflow-type: tm+mt
source-wordcount: '147'
ht-degree: 4%

---

# [!UICONTROL XDM商業帳戶] 類

[!UICONTROL XDM商業帳戶] 是標準的Experience Data Model(XDM)類別，可擷取商業帳戶的最低必要屬性。

![](../../images/classes/b2b/business-account.png)

| 屬性 | 資料類型 | 說明 |
| --- | --- | --- |
| `accountKey` | [[!UICONTROL B2B源]](../../data-types/b2b-source.md) | 帳戶實體的複合標識符。 |
| `extSourceSystemAudit` | [[!UICONTROL 外部源系統審核屬性]](../../data-types/external-source-system-audit-attributes.md) | 如果帳戶來自外部源系統，則此對象將捕獲該系統的審核屬性。 |
| `_id` | 字串 | 記錄的唯一標識符。 這是系統產生的值，與 `accountID`. |
| `accountID` | 字串 | 帳戶實體的唯一識別碼。 |

{style=&quot;table-layout:auto&quot;}

請參閱 [即時CDP B2B版中的架構關係](../../tutorials/relationship-b2b.md) 了解此類別在概念上如何與其他B2B類別相關，以及如何在Adobe Experience Platform UI中建立這些關係。
