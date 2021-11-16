---
title: XDM Business Marketing List Members類
description: 本檔案概述Experience Data Model(XDM)中的XDM Business Marketing List Members類別。
exl-id: 069002c2-5583-4c59-84ee-c071e2acaaec
source-git-commit: 8718512a9768158183b9fb6b9e336081e47cd889
workflow-type: tm+mt
source-wordcount: '251'
ht-degree: 3%

---

# [!UICONTROL XDM商業行銷清單成員] 類

>[!IMPORTANT]
>
>此類別旨在供具有以下權限的組織使用： [Real-time Customer Data Platform B2B版](../../../rtcdp/b2b-overview.md). 您必須擁有Real-time CDP B2B Edition的訪問權限，才能讓此類參與 [即時客戶個人檔案](../../../profile/home.md).

[!UICONTROL XDM商業行銷清單成員] 是標準的Experience Data Model(XDM)類別，可說明與行銷清單相關聯的成員、人員或聯絡人。

![](../../images/classes/b2b/business-marketing-list-members.png)

| 屬性 | 資料類型 | 說明 |
| --- | --- | --- |
| `extSourceSystemAudit` | [[!UICONTROL 外部源系統審核屬性]](../../data-types/external-source-system-audit-attributes.md) | 如果行銷清單成員資格來自外部來源系統，此物件會擷取該系統的稽核屬性。 |
| `marketingListKey` | [[!UICONTROL B2B源]](../../data-types/b2b-source.md) | 該人員所屬的行銷清單的複合標識符。 |
| `marketingListMemberKey` | [[!UICONTROL B2B源]](../../data-types/b2b-source.md) | 行銷清單成員資格實體的複合標識符。 |
| `personKey` | [[!UICONTROL B2B源]](../../data-types/b2b-source.md) | 行銷清單成員的人員的複合識別碼。 |
| `_id` | 字串 | 記錄的唯一標識符。 這是系統產生的值，與 `marketingListMemberID`. |
| `marketingListID` | 字串 | 行銷清單的唯一ID。 |
| `marketingListMemberID` | 字串 | 行銷清單成員資格實體的唯一ID。 |
| `personId` | 字串 | 人員的唯一ID。 |

{style=&quot;table-layout:auto&quot;}

請參閱 [即時CDP B2B版中的架構關係](../../tutorials/relationship-b2b.md) 了解此類別在概念上如何與其他B2B類別相關，以及如何在Adobe Experience Platform UI中建立這些關係。
