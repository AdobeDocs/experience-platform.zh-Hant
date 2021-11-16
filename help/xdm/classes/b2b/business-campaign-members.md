---
title: XDM Business Campaign成員類別
description: 本檔案概述Experience Data Model(XDM)中的XDM Business Campaign Members類別。
exl-id: a39eac7d-46ee-4e9c-a1c0-4dbb63f2c813
source-git-commit: 8718512a9768158183b9fb6b9e336081e47cd889
workflow-type: tm+mt
source-wordcount: '245'
ht-degree: 3%

---

# [!UICONTROL XDM Business Campaign成員] 類

>[!IMPORTANT]
>
>此類別旨在供具有以下權限的組織使用： [Real-time Customer Data Platform B2B版](../../../rtcdp/b2b-overview.md). 您必須擁有Real-time CDP B2B Edition的訪問權限，才能讓此類參與 [即時客戶個人檔案](../../../profile/home.md).

[!UICONTROL XDM Business Campaign成員] 是標準的Experience Data Model(XDM)類別，可說明與業務促銷活動相關聯的聯絡人或潛在客戶。

![](../../images/classes/b2b/business-campaign-members.png)

| 屬性 | 資料類型 | 說明 |
| --- | --- | --- |
| `campaignKey` | [[!UICONTROL B2B源]](../../data-types/b2b-source.md) | 關聯促銷活動的複合識別碼。 |
| `campaignMemberKey` | [[!UICONTROL B2B源]](../../data-types/b2b-source.md) | 促銷活動成員資格實體的複合標識符。 |
| `extSourceSystemAudit` | [[!UICONTROL 外部源系統審核屬性]](../../data-types/external-source-system-audit-attributes.md) | 如果促銷活動成員資格來自外部來源系統，此物件會擷取該系統的稽核屬性。 |
| `personKey` | [[!UICONTROL B2B源]](../../data-types/b2b-source.md) | 關聯促銷活動成員的人員的複合標識符。 |
| `_id` | 字串 | 記錄的唯一標識符。 這是系統產生的值，與 `campaignMemberID`. |
| `campaignID` | 字串 | 相關促銷活動的唯一ID。 |
| `campaignMemberID` | 字串 | 促銷活動成員資格實體的唯一ID。 |
| `personId` | 字串 | 屬於相關促銷活動成員之人員的唯一ID。 |

{style=&quot;table-layout:auto&quot;}

請參閱 [即時CDP B2B版中的架構關係](../../tutorials/relationship-b2b.md) 了解此類別在概念上如何與其他B2B類別相關，以及如何在Adobe Experience Platform UI中建立這些關係。
