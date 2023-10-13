---
title: 外部來源系統稽核屬性資料型別
description: 本檔案提供外部來源系統稽核屬性Experience Data Model (XDM)資料型別的概述。
exl-id: ebdd8707-9675-4232-a5b7-4e4a481d706a
source-git-commit: a7e6ebfe09566e6e027b13efc95dda97ff8f0315
workflow-type: tm+mt
source-wordcount: '192'
ht-degree: 15%

---

# [!UICONTROL 外部來源系統稽核屬性] 資料型別

[!UICONTROL 外部來源系統稽核屬性]是一種標準的體驗資料模式 (XDM) 資料類型，用於擷取外部來源系統的稽核詳細資料。

![](../images/data-types/external-source-system-audit-attributes.png)

| 屬性 | 資料類型 | 說明 |
| --- | --- | --- |
| `externalKey` | [[!UICONTROL B2B來源]](./b2b-source.md) | 用於稽核之來源的複合識別碼。 |
| `createdBy` | 字串 | 建立此記錄的使用者名稱。 |
| `createdDate` | 日期時間 | 建立此記錄的日期。 |
| `externalID` | 字串 | 來源的外部唯一識別碼。 如有需要，此值可用於協助識別和刪除重複專案。 |
| `lastActivityDate` | 日期時間 | 來源系統的上次活動日期。 |
| `lastReferencedDate` | 日期時間 | 來源系統的最後參考日期。 |
| `lastUpdatedBy` | 字串 | 上次更新此紀錄的人員名稱。 |
| `lastUpdatedDate` | 日期時間 | 來源系統的上次更新日期。 |
| `lastViewedDate` | 日期時間 | 來源系統的上次檢視日期。 |

{style="table-layout:auto"}

如需資料型別的詳細資訊，請參閱公用XDM存放庫：

* [填入範例](https://github.com/adobe/xdm/blob/master/components/datatypes/auditing/external-source-system-audit.example.1.json)
* [完整結構描述](https://github.com/adobe/xdm/blob/master/components/datatypes/auditing/external-source-system-audit.schema.json)
