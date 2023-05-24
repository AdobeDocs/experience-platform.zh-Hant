---
title: XDM業務活動類
description: 本文檔概述了「經驗資料模型」(XDM)中的「XDM業務活動」類。
exl-id: 4e3228a1-74be-43af-b355-45d84afb1611
source-git-commit: 34e0381d40f884cd92157d08385d889b1739845f
workflow-type: tm+mt
source-wordcount: '237'
ht-degree: 2%

---

# [!UICONTROL XDM業務活動] 類

>[!IMPORTANT]
>
>此類旨在供有權訪問 [Adobe Real-time Customer Data PlatformB2B版](../../../rtcdp/b2b-overview.md)。 您必須具有訪問Real-Time CDPB2B版的權限，才能讓此類參與 [即時客戶配置檔案](../../../profile/home.md)。

[!UICONTROL XDM業務活動] 是標準的體驗資料模型(XDM)類，它捕獲業務活動所需的最小屬性。

![XDM業務活動類在UI中顯示的結構](../../images/classes/b2b/business-campaign.png)

| 屬性 | 資料類型 | 說明 |
| --- | --- | --- |
| `campaignKey` | [[!UICONTROL B2B源]](../../data-types/b2b-source.md) | 市場活動實體的組合標識符。 |
| `extSourceSystemAudit` | [[!UICONTROL 外部源系統審核屬性]](../../data-types/external-source-system-audit-attributes.md) | 如果市場活動來自外部源系統，則此對象將捕獲該系統的審核屬性。 |
| `_id` | 字串 | 記錄的唯一標識符。 這是系統生成的值，它與 `campaignID`。 |
| `campaignDescription` | 字串 | 市場活動的說明。 |
| `campaignID` | 字串 | 市場活動實體的唯一標識符。 |
| `campaignName` | 字串 | 活動的名稱。 |
| `campaignType` | 字串 | 市場活動類型或目標受眾。 |

{style="table-layout:auto"}

要瞭解此類在概念上如何與其他B2B類相關，以及如何在Adobe Experience PlatformUI中建立這些關係，請參閱上的指南 [Real-Time CDPB2B版模式關係](../../tutorials/relationship-b2b.md)

有關與此類相容的其他欄位，請參閱的欄位組引用 [[!UICONTROL XDM業務活動詳細資訊]](../../field-groups/b2b-campaign/details.md)。
