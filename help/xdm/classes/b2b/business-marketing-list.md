---
title: XDM商業行銷清單類別
description: 本檔案概述Experience Data Model(XDM)中的XDM Business Marketing List類別。
source-git-commit: 19bb39b66f3a3eb93fd0138ac021568021d77b0f
workflow-type: tm+mt
source-wordcount: '164'
ht-degree: 3%

---

# [!UICONTROL XDM Business Marketing清] 單類

>[!NOTE]
>
>此類別僅適用於可存取B2B版即時客戶資料平台的組織。

[!UICONTROL XDM Business Marketing List] 是標準的Experience Data Model(XDM)類別，可擷取行銷清單的最低必要屬性。行銷清單可讓您針對最可能購買您產品的潛在客戶進行優先排序。

![](../../images/classes/b2b/business-marketing-list.png)

| 屬性 | 資料類型 | 說明 |
| --- | --- | --- |
| `extSourceSystemAudit` | [[!UICONTROL 外部源系統審核屬性]](../../data-types/external-source-system-audit-attributes.md) | 如果行銷清單來自外部來源系統，此物件會擷取該系統的稽核屬性。 |
| `marketingListKey` | [[!UICONTROL B2B源]](../../data-types/b2b-source.md) | 行銷清單實體的複合識別碼。 |
| `_id` | 字串 | 記錄的唯一標識符。 這是系統產生的值，與`marketingListID`分開。 |
| `marketingListDescription` | 字串 | 行銷清單的說明。 |
| `marketingListID` | 字串 | 行銷清單實體的唯一ID。 |
| `marketingListName` | 字串 | 行銷清單的名稱。 |
