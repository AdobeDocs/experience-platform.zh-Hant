---
title: XDM商業帳戶類別
description: 瞭解Experience Data Model (XDM)中的XDM商業帳戶類別。
exl-id: abe4c919-a680-4aad-918e-6e56cae8bd4d
source-git-commit: de8e944cfec3b52d25bb02bcfebe57d6a2a35e39
workflow-type: tm+mt
source-wordcount: '252'
ht-degree: 2%

---

# [!UICONTROL XDM商業帳戶] 類別

>[!IMPORTANT]
>
>此類別旨在由擁有存取權的組織使用 [Adobe Real-time Customer Data Platform B2B版本](../../../rtcdp/b2b-overview.md). 您必須擁有Real-Time CDP B2B Edition的存取權，此類別才能參與 [即時客戶個人檔案](../../../profile/home.md).

[!UICONTROL XDM商業帳戶] 是一個標準的體驗資料模型(XDM)類別，可擷取企業帳戶的最低要求屬性。

![XDM商業帳戶類別在UI中的結構](../../images/classes/b2b/business-account.png)

| 屬性 | 資料類型 | 說明 |
| --- | --- | --- |
| `accountKey` | [[!UICONTROL B2B來源]](../../data-types/b2b-source.md) | 帳戶實體的複合識別碼。 |
| `extSourceSystemAudit` | [[!UICONTROL 外部來源系統稽核屬性]](../../data-types/external-source-system-audit-attributes.md) | 如果帳戶來自外部來源系統，此物件會擷取該系統的稽核屬性。 |
| `_id` | 字串 | 紀錄的唯一識別碼。 這是系統產生的值，與 `accountKey` 識別碼。 |
| `isDeleted` | 布林值 | 指出是否已在Marketo Engage中刪除此帳戶實體。<br><br>使用時 [Marketo來源聯結器](../../../sources/connectors/adobe-applications/marketo/marketo.md)，在Marketo中刪除的任何記錄都會自動反映在即時客戶個人檔案中。 不過，與這些設定檔相關的記錄可能仍會保留在資料湖中。 透過設定 `isDeleted` 至 `true`，您可使用欄位來篩選在查詢資料湖時已從您的來源刪除哪些記錄。 |

{style="table-layout:auto"}

請參閱以下指南： [Real-Time CDP B2B Edition中的結構描述關係](../../tutorials/relationship-b2b.md) 瞭解此類別與其他B2B類別在概念上的關聯性，以及如何在Adobe Experience Platform UI中建立這些關聯性。
