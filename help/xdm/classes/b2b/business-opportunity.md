---
title: XDM商業機會類別
description: 瞭解Experience Data Model (XDM)中的XDM商業機會類別。
exl-id: d816b0f9-fd37-45da-aa55-247f7f662da0
source-git-commit: de8e944cfec3b52d25bb02bcfebe57d6a2a35e39
workflow-type: tm+mt
source-wordcount: '309'
ht-degree: 3%

---

# [!UICONTROL XDM商業機會]類別

>[!IMPORTANT]
>
>此類別是供具有[Adobe Real-time Customer Data Platform B2B Edition](../../../rtcdp/b2b-overview.md)存取權的組織使用。 您必須擁有Real-Time CDP B2B Edition的存取權，此類別才能參與[即時客戶設定檔](../../../profile/home.md)。

[!UICONTROL XDM商業機會]是一個標準的體驗資料模型(XDM)類別，可擷取商業機會的最低要求屬性。

![ XDM商業機會類別在UI中的結構](../../images/classes/b2b/business-opportunity.png)

| 屬性 | 資料類型 | 說明 |
| --- | --- | --- |
| `accountKey` | [[!UICONTROL B2B Source]](../../data-types/b2b-source.md) | 與此機會相關聯的帳戶的複合識別碼。 |
| `extSourceSystemAudit` | [[!UICONTROL 外部Source系統稽核屬性]](../../data-types/external-source-system-audit-attributes.md) | 如果機會來自外部來源系統，此物件會擷取該系統的稽核屬性。 |
| `opportunityKey` | [[!UICONTROL B2B Source]](../../data-types/b2b-source.md) | 機會實體的複合識別碼。 |
| `_id` | 字串 | 紀錄的唯一識別碼。 這是系統產生的值，與`opportunityID`不同。 |
| `accountID` | 字串 | 與此機會相關聯的帳戶的唯一ID。 |
| `isDeleted` | 布林值 | 表示此行銷清單實體是否已在Marketo Engage中刪除。<br><br>使用[Marketo來源聯結器](../../../sources/connectors/adobe-applications/marketo/marketo.md)時，在Marketo中刪除的任何記錄都會自動反映在即時客戶個人檔案中。 不過，與這些設定檔相關的記錄可能仍會保留在資料湖中。 透過將`isDeleted`設定為`true`，您可以在查詢資料湖時使用該欄位來篩選出已從您的來源中刪除的記錄。 |
| `opportunityDescription` | 字串 | 機會的說明。 |
| `opportunityID` | 字串 | 機會實體的唯一ID。 |
| `opportunityName` | 字串 | 機會的名稱。 |
| `opportunityStage` | 字串 | 機會的銷售階段。 |
| `opportunityType` | 字串 | 機會型別。 |

{style="table-layout:auto"}

請參閱Real-Time CDP B2B Edition[&#128279;](../../tutorials/relationship-b2b.md)中結構描述關聯性的指南，瞭解此類別與其他B2B類別在概念上的關聯性，以及如何在Adobe Experience Platform UI中建立這些關聯性。
