---
title: XDM Business Campaign成員類別
description: 本檔案概述Experience Data Model(XDM)中的XDM Business Campaign Members類別。
exl-id: a39eac7d-46ee-4e9c-a1c0-4dbb63f2c813
source-git-commit: 14e3eff3ea2469023823a35ee1112568f5b5f4f7
workflow-type: tm+mt
source-wordcount: '249'
ht-degree: 2%

---

# [!UICONTROL XDM Business Campaign成員] 類

>[!IMPORTANT]
>
>此類別旨在供具有以下權限的組織使用： [Adobe Real-time Customer Data Platform B2B版](../../../rtcdp/b2b-overview.md). 您必須擁有Real-Time CDP B2B版的存取權，才能讓此類別參與 [即時客戶個人檔案](../../../profile/home.md).

[!UICONTROL XDM Business Campaign成員] 是標準的Experience Data Model(XDM)類別，可說明與業務促銷活動相關聯的聯絡人或潛在客戶。

![XDM業務促銷活動成員類別的結構，如同顯示在UI中](../../images/classes/b2b/business-campaign-members.png)

| 屬性 | 資料類型 | 說明 |
| --- | --- | --- |
| `campaignKey` | [[!UICONTROL B2B源]](../../data-types/b2b-source.md) | 關聯促銷活動的複合識別碼。 |
| `campaignMemberKey` | [[!UICONTROL B2B源]](../../data-types/b2b-source.md) | 促銷活動成員資格實體的複合標識符。 |
| `extSourceSystemAudit` | [[!UICONTROL 外部源系統審核屬性]](../../data-types/external-source-system-audit-attributes.md) | 如果促銷活動成員資格來自外部來源系統，此物件會擷取該系統的稽核屬性。 |
| `personKey` | [[!UICONTROL B2B源]](../../data-types/b2b-source.md) | 關聯促銷活動成員的人員的複合標識符。 |
| `_id` | 字串 | 記錄的唯一標識符。 這是系統產生的值，與 `campaignMemberID`. |

{style=&quot;table-layout:auto&quot;}

若要了解此類別在概念上如何與其他B2B類別相關，以及如何在Adobe Experience Platform UI中建立這些關係，請參閱 [Real-Time CDP B2B版中的結構關係](../../tutorials/relationship-b2b.md)

有關與此類相容的其他欄位，請參閱的欄位組引用 [[!UICONTROL XDM Business Campaign成員詳細資訊]](../../field-groups/b2b-campaign-members/details.md).
