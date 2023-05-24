---
title: XDM業務營銷清單成員類
description: 本文檔概述了「體驗資料模型」(XDM)中的「XDM業務營銷清單成員」類。
exl-id: 069002c2-5583-4c59-84ee-c071e2acaaec
source-git-commit: 34e0381d40f884cd92157d08385d889b1739845f
workflow-type: tm+mt
source-wordcount: '336'
ht-degree: 2%

---

# [!UICONTROL XDM業務營銷清單成員] 類

>[!IMPORTANT]
>
>此類旨在供有權訪問 [Adobe Real-time Customer Data PlatformB2B版](../../../rtcdp/b2b-overview.md)。 您必須具有訪問Real-Time CDPB2B版的權限，才能讓此類參與 [即時客戶配置檔案](../../../profile/home.md)。

[!UICONTROL XDM業務營銷清單成員] 是一個標準體驗資料模型(XDM)類，它描述與市場營銷清單關聯的成員、人員或聯繫人。

![XDM業務營銷清單成員類的結構，如在UI中顯示的那樣](../../images/classes/b2b/business-marketing-list-members.png)

| 屬性 | 資料類型 | 說明 |
| --- | --- | --- |
| `extSourceSystemAudit` | [[!UICONTROL 外部源系統審核屬性]](../../data-types/external-source-system-audit-attributes.md) | 如果市場營銷清單成員資格來自外部源系統，則此對象將捕獲該系統的審計屬性。 |
| `marketingListKey` | [[!UICONTROL B2B源]](../../data-types/b2b-source.md) | 該人員所屬的市場營銷清單的組合標識符。 |
| `marketingListMemberKey` | [[!UICONTROL B2B源]](../../data-types/b2b-source.md) | 市場營銷清單成員身份實體的組合標識符。 |
| `personKey` | [[!UICONTROL B2B源]](../../data-types/b2b-source.md) | 作為市場營銷清單成員的人員的組合標識符。 |
| `_id` | 字串 | 記錄的唯一標識符。 這是系統生成的值，它與 `marketingListMemberID`。 |
| `isDeleted` | 布林值 | 指示此市場營銷清單成員實體是否已在Marketo Engage中刪除。<br><br>使用 [Marketo源連接器](../../../sources/connectors/adobe-applications/marketo/marketo.md)，在Marketo刪除的任何記錄將自動反映在即時客戶配置檔案中。 但是，與這些檔案有關的記錄可能仍會在Data Lake中保留。 通過設定 `isDeleted` 至 `true`，可以使用該欄位在查詢資料湖時過濾已從源中刪除的記錄。 |
| `marketingListID` | 字串 | 市場營銷清單的唯一ID。 |
| `marketingListMemberID` | 字串 | 市場營銷清單成員身份實體的唯一ID。 |
| `personId` | 字串 | 人員的唯一ID。 |

{style="table-layout:auto"}

請參閱上的指南 [Real-Time CDPB2B版模式關係](../../tutorials/relationship-b2b.md) 瞭解此類在概念上如何與其他B2B類相關，以及如何在Adobe Experience PlatformUI中建立這些關係。
