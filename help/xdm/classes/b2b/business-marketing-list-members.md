---
title: XDM Business Marketing List Members類
description: 本檔案概述Experience Data Model(XDM)中的XDM Business Marketing List Members類別。
source-git-commit: 5fd82b02eb25f3d575de695c2f2b14a5e5b18400
workflow-type: tm+mt
source-wordcount: '226'
ht-degree: 2%

---

# [!UICONTROL XDM Business Marketing List ] Memberssclass

>[!NOTE]
>
>此類別僅適用於可存取即時客戶資料平台B2B版的組織。

[!UICONTROL XDM商業行銷清] 單會籍是標準的Experience Data Model(XDM)類別，可說明與行銷清單相關聯的成員、人員或聯絡人。

![](../../images/classes/b2b/business-marketing-list-members.png)

| 屬性 | 資料類型 | 說明 |
| --- | --- | --- |
| `extSourceSystemAudit` | [[!UICONTROL 外部源系統審核屬性]](../../data-types/external-source-system-audit-attributes.md) | 如果行銷清單成員資格來自外部來源系統，此物件會擷取該系統的稽核屬性。 |
| `marketingListKey` | [[!UICONTROL B2B源]](../../data-types/b2b-source.md) | 該人員所屬的行銷清單的複合標識符。 |
| `marketingListMemberKey` | [[!UICONTROL B2B源]](../../data-types/b2b-source.md) | 行銷清單成員資格實體的複合標識符。 |
| `personKey` | [[!UICONTROL B2B源]](../../data-types/b2b-source.md) | 行銷清單成員的人員的複合識別碼。 |
| `_id` | 字串 | 記錄的唯一標識符。 這是系統產生的值，與`marketingListMemberID`分開。 |
| `marketingListID` | 字串 | 行銷清單的唯一ID。 |
| `marketingListMemberID` | 字串 | 行銷清單成員資格實體的唯一ID。 |
| `personId` | 字串 | 人員的唯一ID。 |

請參閱即時CDP B2B版本](../../tutorials/relationship-b2b.md)中的[架構關係指南，了解此類別在概念上如何與其他B2B類別相關，以及如何在Adobe Experience Platform UI中建立這些關係。
