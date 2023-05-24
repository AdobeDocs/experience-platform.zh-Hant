---
title: XDM業務活動成員類
description: 本文檔概述了「經驗資料模型」(XDM)中的「XDM業務活動成員」類。
exl-id: a39eac7d-46ee-4e9c-a1c0-4dbb63f2c813
source-git-commit: 34e0381d40f884cd92157d08385d889b1739845f
workflow-type: tm+mt
source-wordcount: '246'
ht-degree: 1%

---

# [!UICONTROL XDM業務活動成員] 類

>[!IMPORTANT]
>
>此類旨在供有權訪問 [Adobe Real-time Customer Data PlatformB2B版](../../../rtcdp/b2b-overview.md)。 您必須具有訪問Real-Time CDPB2B版的權限，才能讓此類參與 [即時客戶配置檔案](../../../profile/home.md)。

[!UICONTROL XDM業務活動成員] 是一個標準的體驗資料模型(XDM)類，它描述與業務活動關聯的聯繫人或潛在顧客。

![XDM業務活動成員類的結構，如UI中所示](../../images/classes/b2b/business-campaign-members.png)

| 屬性 | 資料類型 | 說明 |
| --- | --- | --- |
| `campaignKey` | [[!UICONTROL B2B源]](../../data-types/b2b-source.md) | 關聯市場活動的組合標識符。 |
| `campaignMemberKey` | [[!UICONTROL B2B源]](../../data-types/b2b-source.md) | 市場活動成員身份實體的組合標識符。 |
| `extSourceSystemAudit` | [[!UICONTROL 外部源系統審核屬性]](../../data-types/external-source-system-audit-attributes.md) | 如果市場活動成員資格來自外部源系統，則此對象將捕獲該系統的審核屬性。 |
| `personKey` | [[!UICONTROL B2B源]](../../data-types/b2b-source.md) | 作為關聯市場活動成員的人員的組合標識符。 |
| `_id` | 字串 | 記錄的唯一標識符。 這是系統生成的值，它與 `campaignMemberID`。 |

{style="table-layout:auto"}

要瞭解此類在概念上如何與其他B2B類相關，以及如何在Adobe Experience PlatformUI中建立這些關係，請參閱上的指南 [Real-Time CDPB2B版模式關係](../../tutorials/relationship-b2b.md)

有關與此類相容的其他欄位，請參閱的欄位組引用 [[!UICONTROL XDM業務活動成員詳細資訊]](../../field-groups/b2b-campaign-members/details.md)。
