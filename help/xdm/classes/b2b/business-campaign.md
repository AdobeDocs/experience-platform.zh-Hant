---
title: XDM商業活動類別
description: 瞭解Experience Data Model (XDM)中的XDM商業活動類別。
exl-id: 4e3228a1-74be-43af-b355-45d84afb1611
source-git-commit: de8e944cfec3b52d25bb02bcfebe57d6a2a35e39
workflow-type: tm+mt
source-wordcount: '228'
ht-degree: 3%

---

# [!UICONTROL XDM商業活動]類別

>[!IMPORTANT]
>
>此類別是供具有[Adobe Real-time Customer Data Platform B2B Edition](../../../rtcdp/b2b-overview.md)存取權的組織使用。 您必須擁有Real-Time CDP B2B Edition的存取權，此類別才能參與[即時客戶設定檔](../../../profile/home.md)。

[!UICONTROL XDM商業促銷活動]是一個標準的體驗資料模型(XDM)類別，可擷取商業促銷活動的最低要求屬性。

![ XDM商業促銷活動類別在UI中的結構](../../images/classes/b2b/business-campaign.png)

| 屬性 | 資料類型 | 說明 |
| --- | --- | --- |
| `campaignKey` | [[!UICONTROL B2B Source]](../../data-types/b2b-source.md) | 行銷活動實體的複合識別碼。 |
| `extSourceSystemAudit` | [[!UICONTROL 外部Source系統稽核屬性]](../../data-types/external-source-system-audit-attributes.md) | 如果促銷活動來自外部來源系統，此物件會擷取該系統的稽核屬性。 |
| `_id` | 字串 | 紀錄的唯一識別碼。 這是系統產生的值，與`campaignID`不同。 |
| `campaignDescription` | 字串 | 行銷活動的說明。 |
| `campaignID` | 字串 | 適用於行銷活動實體的唯一識別碼。 |
| `campaignName` | 字串 | 行銷活動的名稱。 |
| `campaignType` | 字串 | 行銷活動型別或目標對象。 |

{style="table-layout:auto"}

若要瞭解此類別與其他B2B類別在概念上的關聯性，以及如何在Adobe Experience Platform UI中建立這些關聯性，請參閱Real-Time CDP B2B Edition[結構描述關聯性指南](../../tutorials/relationship-b2b.md)

如需與此類別相容的其他欄位，請參閱[[!UICONTROL XDM商業促銷活動詳細資料]](../../field-groups/b2b-campaign/details.md)的欄位群組參考。
