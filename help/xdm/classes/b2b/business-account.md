---
title: XDM業務帳戶類別
description: 本檔案概述Experience Data Model(XDM)中的XDM商業帳戶類別。
source-git-commit: 19bb39b66f3a3eb93fd0138ac021568021d77b0f
workflow-type: tm+mt
source-wordcount: '126'
ht-degree: 3%

---

# [!UICONTROL XDM業務帳] 戶類

>[!NOTE]
>
>此類別僅適用於可存取B2B版即時客戶資料平台的組織。

[!UICONTROL XDM商業] 帳戶是標準的Experience Data Model(XDM)類別，可擷取商業帳戶的最低必要屬性。

![](../../images/classes/b2b/business-account.png)

| 屬性 | 資料類型 | 說明 |
| --- | --- | --- |
| `accountKey` | [[!UICONTROL B2B源]](../../data-types/b2b-source.md) | 帳戶實體的複合標識符。 |
| `extSourceSystemAudit` | [[!UICONTROL 外部源系統審核屬性]](../../data-types/external-source-system-audit-attributes.md) | 如果帳戶來自外部源系統，則此對象將捕獲該系統的審核屬性。 |
| `_id` | 字串 | 記錄的唯一標識符。 這是系統產生的值，與`accountID`分開。 |
| `accountID` | 字串 | 帳戶實體的唯一識別碼。 |
