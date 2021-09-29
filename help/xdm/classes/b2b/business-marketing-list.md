---
title: XDM商業行銷清單類別
description: 本檔案概述Experience Data Model(XDM)中的XDM Business Marketing List類別。
exl-id: 510c5608-054d-4bed-91eb-22d84b5dc625
source-git-commit: b5cdd72238f7b4519de1c789f4294b9698415327
workflow-type: tm+mt
source-wordcount: '213'
ht-degree: 4%

---

# [!UICONTROL XDM Business Marketing ] Listclass（測試版）

>[!IMPORTANT]
>
>此類別屬於目前測試版的即時客戶資料平台B2B版。 檔案和功能可能會有所變更。

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

{style=&quot;table-layout:auto&quot;}

請參閱即時CDP B2B版本](../../tutorials/relationship-b2b.md)中的[架構關係指南，了解此類別在概念上如何與其他B2B類別相關，以及如何在Adobe Experience Platform UI中建立這些關係。
