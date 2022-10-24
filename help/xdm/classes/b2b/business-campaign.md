---
title: XDM Business Campaign類別
description: 本檔案概述Experience Data Model(XDM)中的XDM Business Campaign類別。
exl-id: 4e3228a1-74be-43af-b355-45d84afb1611
source-git-commit: 14e3eff3ea2469023823a35ee1112568f5b5f4f7
workflow-type: tm+mt
source-wordcount: '240'
ht-degree: 4%

---

# [!UICONTROL XDM商業宣傳] 類

>[!IMPORTANT]
>
>此類別旨在供具有以下權限的組織使用： [Adobe Real-time Customer Data Platform B2B版](../../../rtcdp/b2b-overview.md). 您必須擁有Real-Time CDP B2B版的存取權，才能讓此類別參與 [即時客戶個人檔案](../../../profile/home.md).

[!UICONTROL XDM商業宣傳] 是標準的Experience Data Model(XDM)類別，可擷取商業促銷活動的最低必要屬性。

![XDM Business Campaign類別的結構，如同顯示在UI中一樣](../../images/classes/b2b/business-campaign.png)

| 屬性 | 資料類型 | 說明 |
| --- | --- | --- |
| `campaignKey` | [[!UICONTROL B2B源]](../../data-types/b2b-source.md) | 促銷活動實體的複合識別碼。 |
| `extSourceSystemAudit` | [[!UICONTROL 外部源系統審核屬性]](../../data-types/external-source-system-audit-attributes.md) | 如果促銷活動來自外部來源系統，此物件會擷取該系統的稽核屬性。 |
| `_id` | 字串 | 記錄的唯一標識符。 這是系統產生的值，與 `campaignID`. |
| `campaignDescription` | 字串 | 促銷活動的說明。 |
| `campaignID` | 字串 | 促銷活動實體的唯一識別碼。 |
| `campaignName` | 字串 | 促銷活動的名稱。 |
| `campaignType` | 字串 | 促銷活動類型或目標對象。 |

{style=&quot;table-layout:auto&quot;}

若要了解此類別在概念上如何與其他B2B類別相關，以及如何在Adobe Experience Platform UI中建立這些關係，請參閱 [Real-Time CDP B2B版中的結構關係](../../tutorials/relationship-b2b.md)

有關與此類相容的其他欄位，請參閱的欄位組引用 [[!UICONTROL XDM商業促銷活動詳細資訊]](../../field-groups/b2b-campaign/details.md).
