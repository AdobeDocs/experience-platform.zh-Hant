---
title: 外部源系統審核屬性資料類型
description: 本檔案概述外部來源系統稽核屬性Experience Data Model(XDM)資料類型。
exl-id: ebdd8707-9675-4232-a5b7-4e4a481d706a
source-git-commit: 14e3eff3ea2469023823a35ee1112568f5b5f4f7
workflow-type: tm+mt
source-wordcount: '214'
ht-degree: 2%

---

# [!UICONTROL 外部源系統審核屬性] 資料類型

>[!NOTE]
>
>此資料類型僅適用於可存取Adobe Real-time Customer Data Platform B2B版本的組織。

[!UICONTROL 外部源系統審核屬性] 是標準的Experience Data Model(XDM)資料類型，可擷取外部來源系統的稽核詳細資料。

![](../images/data-types/external-source-system-audit-attributes.png)

| 屬性 | 資料類型 | 說明 |
| --- | --- | --- |
| `externalKey` | [[!UICONTROL B2B源]](./b2b-source.md) | 用於審核的源的複合標識符。 |
| `createdBy` | 字串 | 建立此記錄的用戶的名稱。 |
| `createdDate` | DateTime | 建立此記錄的日期。 |
| `externalID` | 字串 | 源的外部唯一標識符。 此值可協助您視需要識別及去重複化。 |
| `lastActivityDate` | DateTime | 源系統的最後活動日期。 |
| `lastReferencedDate` | DateTime | 源系統的最後引用日期。 |
| `lastUpdatedBy` | 字串 | 上次更新此記錄的人員的名稱。 |
| `lastUpdatedDate` | DateTime | 源系統的上次更新日期。 |
| `lastViewedDate` | DateTime | 源系統的上次查看日期。 |

{style="table-layout:auto"}

如需資料類型的詳細資訊，請參閱公用XDM存放庫：

* [填入範例](https://github.com/adobe/xdm/blob/master/components/datatypes/auditing/external-source-system-audit.example.1.json)
* [完整結構](https://github.com/adobe/xdm/blob/master/components/datatypes/auditing/external-source-system-audit.schema.json)
