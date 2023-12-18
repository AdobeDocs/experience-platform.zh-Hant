---
title: XDM商業活動成員類別
description: 瞭解Experience Data Model (XDM)中的XDM商業活動會員類別。
exl-id: a39eac7d-46ee-4e9c-a1c0-4dbb63f2c813
source-git-commit: de8e944cfec3b52d25bb02bcfebe57d6a2a35e39
workflow-type: tm+mt
source-wordcount: '235'
ht-degree: 2%

---

# [!UICONTROL XDM商業活動會員] 類別

>[!IMPORTANT]
>
>此類別旨在由擁有存取權的組織使用 [Adobe Real-time Customer Data Platform B2B版本](../../../rtcdp/b2b-overview.md). 您必須擁有Real-Time CDP B2B Edition的存取權，此類別才能參與 [即時客戶個人檔案](../../../profile/home.md).

[!UICONTROL XDM商業活動會員] 是一個標準的體驗資料模型(XDM)類別，可描述與商業促銷活動相關聯的聯絡人或銷售機會。

![XDM商業活動成員類別在UI中的結構](../../images/classes/b2b/business-campaign-members.png)

| 屬性 | 資料類型 | 說明 |
| --- | --- | --- |
| `campaignKey` | [[!UICONTROL B2B來源]](../../data-types/b2b-source.md) | 相關行銷活動的複合識別碼。 |
| `campaignMemberKey` | [[!UICONTROL B2B來源]](../../data-types/b2b-source.md) | 行銷活動成員實體的複合識別碼。 |
| `extSourceSystemAudit` | [[!UICONTROL 外部來源系統稽核屬性]](../../data-types/external-source-system-audit-attributes.md) | 如果促銷活動會籍來自外部來源系統，此物件會擷取該系統的稽核屬性。 |
| `personKey` | [[!UICONTROL B2B來源]](../../data-types/b2b-source.md) | 關聯行銷活動成員的個人的複合識別碼。 |
| `_id` | 字串 | 紀錄的唯一識別碼。 這是系統產生的值，與 `campaignMemberID`. |

{style="table-layout:auto"}

若要瞭解此類別與其他B2B類別在概念上的關聯性，以及如何在Adobe Experience Platform UI中建立這些關聯性，請參閱以下指南： [Real-Time CDP B2B Edition中的結構描述關係](../../tutorials/relationship-b2b.md)

如需與此類別相容的其他欄位，請參閱 [[!UICONTROL XDM商業活動會員細節]](../../field-groups/b2b-campaign-members/details.md).
