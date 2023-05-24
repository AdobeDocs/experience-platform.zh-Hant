---
title: 外部源系統審核屬性資料類型
description: 本文檔概述了外部源系統審核屬性體驗資料模型(XDM)資料類型。
exl-id: ebdd8707-9675-4232-a5b7-4e4a481d706a
source-git-commit: 14e3eff3ea2469023823a35ee1112568f5b5f4f7
workflow-type: tm+mt
source-wordcount: '214'
ht-degree: 2%

---

# [!UICONTROL 外部源系統審核屬性] 資料類型

>[!NOTE]
>
>此資料類型僅適用於有權訪問Adobe Real-time Customer Data PlatformB2B版的組織。

[!UICONTROL 外部源系統審核屬性] 是標準的體驗資料模型(XDM)資料類型，用於捕獲有關外部源系統的審核詳細資訊。

![](../images/data-types/external-source-system-audit-attributes.png)

| 屬性 | 資料類型 | 說明 |
| --- | --- | --- |
| `externalKey` | [[!UICONTROL B2B源]](./b2b-source.md) | 用於審計的源的組合標識符。 |
| `createdBy` | 字串 | 建立此記錄的用戶的名稱。 |
| `createdDate` | 日期時間 | 建立此記錄的日期。 |
| `externalID` | 字串 | 源的外部唯一標識符。 此值用於幫助識別和消除重複（如果需要）。 |
| `lastActivityDate` | 日期時間 | 源系統的上次活動日期。 |
| `lastReferencedDate` | 日期時間 | 源系統的上次引用日期。 |
| `lastUpdatedBy` | 字串 | 上次更新此記錄的人員的姓名。 |
| `lastUpdatedDate` | 日期時間 | 源系統的上次更新日期。 |
| `lastViewedDate` | 日期時間 | 源系統的上次查看日期。 |

{style="table-layout:auto"}

有關資料類型的詳細資訊，請參閱公共XDM儲存庫：

* [填充示例](https://github.com/adobe/xdm/blob/master/components/datatypes/auditing/external-source-system-audit.example.1.json)
* [完整架構](https://github.com/adobe/xdm/blob/master/components/datatypes/auditing/external-source-system-audit.schema.json)
