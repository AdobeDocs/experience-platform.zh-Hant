---
title: XDM Business Marketing List Members類
description: 本檔案概述Experience Data Model(XDM)中的XDM Business Marketing List Members類別。
exl-id: 069002c2-5583-4c59-84ee-c071e2acaaec
source-git-commit: 14e3eff3ea2469023823a35ee1112568f5b5f4f7
workflow-type: tm+mt
source-wordcount: '339'
ht-degree: 2%

---

# [!UICONTROL XDM商業行銷清單成員] 類

>[!IMPORTANT]
>
>此類別旨在供具有以下權限的組織使用： [Adobe Real-time Customer Data Platform B2B版](../../../rtcdp/b2b-overview.md). 您必須擁有Real-Time CDP B2B版的存取權，才能讓此類別參與 [即時客戶個人檔案](../../../profile/home.md).

[!UICONTROL XDM商業行銷清單成員] 是標準的Experience Data Model(XDM)類別，可說明與行銷清單相關聯的成員、人員或聯絡人。

![XDM Business Marketing List Members類的結構，如同它顯示在UI中一樣](../../images/classes/b2b/business-marketing-list-members.png)

| 屬性 | 資料類型 | 說明 |
| --- | --- | --- |
| `extSourceSystemAudit` | [[!UICONTROL 外部源系統審核屬性]](../../data-types/external-source-system-audit-attributes.md) | 如果行銷清單成員資格來自外部來源系統，此物件會擷取該系統的稽核屬性。 |
| `marketingListKey` | [[!UICONTROL B2B源]](../../data-types/b2b-source.md) | 該人員所屬的行銷清單的複合標識符。 |
| `marketingListMemberKey` | [[!UICONTROL B2B源]](../../data-types/b2b-source.md) | 行銷清單成員資格實體的複合標識符。 |
| `personKey` | [[!UICONTROL B2B源]](../../data-types/b2b-source.md) | 行銷清單成員的人員的複合識別碼。 |
| `_id` | 字串 | 記錄的唯一標識符。 這是系統產生的值，與 `marketingListMemberID`. |
| `isDeleted` | 布林值 | 指示此市場營銷清單成員實體是否已在Marketo Engage中刪除。<br><br>使用 [Marketo來源連接器](../../../sources/connectors/adobe-applications/marketo/marketo.md),Marketo中刪除的任何記錄都會自動反映在即時客戶個人檔案中。 不過，與這些設定檔相關的記錄仍可能會保留在Data Lake。 設定 `isDeleted` to `true`，您可以使用欄位來篩選已在查詢資料湖時從來源刪除的記錄。 |
| `marketingListID` | 字串 | 行銷清單的唯一ID。 |
| `marketingListMemberID` | 字串 | 行銷清單成員資格實體的唯一ID。 |
| `personId` | 字串 | 人員的唯一ID。 |

{style=&quot;table-layout:auto&quot;}

請參閱 [Real-Time CDP B2B版中的結構關係](../../tutorials/relationship-b2b.md) 了解此類別在概念上如何與其他B2B類別相關，以及如何在Adobe Experience Platform UI中建立這些關係。
