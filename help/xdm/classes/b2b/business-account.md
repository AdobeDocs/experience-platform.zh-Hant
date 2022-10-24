---
title: XDM業務帳戶類別
description: 本檔案概述Experience Data Model(XDM)中的XDM商業帳戶類別。
exl-id: abe4c919-a680-4aad-918e-6e56cae8bd4d
source-git-commit: 14e3eff3ea2469023823a35ee1112568f5b5f4f7
workflow-type: tm+mt
source-wordcount: '264'
ht-degree: 2%

---

# [!UICONTROL XDM商業帳戶] 類

>[!IMPORTANT]
>
>此類別旨在供具有以下權限的組織使用： [Adobe Real-time Customer Data Platform B2B版](../../../rtcdp/b2b-overview.md). 您必須擁有Real-Time CDP B2B版的存取權，才能讓此類別參與 [即時客戶個人檔案](../../../profile/home.md).

[!UICONTROL XDM商業帳戶] 是標準的Experience Data Model(XDM)類別，可擷取商業帳戶的最低必要屬性。

![XDM商業帳戶類別的結構，如同顯示在UI中一樣](../../images/classes/b2b/business-account.png)

| 屬性 | 資料類型 | 說明 |
| --- | --- | --- |
| `accountKey` | [[!UICONTROL B2B源]](../../data-types/b2b-source.md) | 帳戶實體的複合標識符。 |
| `extSourceSystemAudit` | [[!UICONTROL 外部源系統審核屬性]](../../data-types/external-source-system-audit-attributes.md) | 如果帳戶來自外部源系統，則此對象將捕獲該系統的審核屬性。 |
| `_id` | 字串 | 記錄的唯一標識符。 這是系統產生的值，與 `accountKey` 識別碼。 |
| `isDeleted` | 布林值 | 指示是否已在Marketo Engage中刪除此帳戶實體。<br><br>使用 [Marketo來源連接器](../../../sources/connectors/adobe-applications/marketo/marketo.md),Marketo中刪除的任何記錄都會自動反映在即時客戶個人檔案中。 不過，與這些設定檔相關的記錄仍可能會保留在Data Lake。 設定 `isDeleted` to `true`，您可以使用欄位來篩選已在查詢資料湖時從來源刪除的記錄。 |

{style=&quot;table-layout:auto&quot;}

請參閱 [Real-Time CDP B2B版中的結構關係](../../tutorials/relationship-b2b.md) 了解此類別在概念上如何與其他B2B類別相關，以及如何在Adobe Experience Platform UI中建立這些關係。
