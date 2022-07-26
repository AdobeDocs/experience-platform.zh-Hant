---
title: 實施詳細資訊資料類型
description: 本文檔概述了實施詳細資訊體驗資料模型(XDM)資料類型。
source-git-commit: 77fb3e348c2298fc5c325fcf2d3408da084b2b19
workflow-type: tm+mt
source-wordcount: '127'
ht-degree: 6%

---

# [!UICONTROL 實施詳細資訊] 資料類型

[!UICONTROL 實施詳細資訊] 是標準的體驗資料模型(XDM)資料類型，它描述技術實現，如API或SDK。

![資料類型結構](../images/data-types/implementation-details.png)

| 屬性 | 資料類型 | 說明 |
| --- | --- | --- |
| `environment` | 字串 | 實施環境。 |
| `name` | 字串 | SDK或終結點的標識符。 所有SDK或端點都通過URI標識，包括擴展。 |
| `version` | 字串 | API或SDK的版本。 |

{style=&quot;table-layout:auto&quot;}

有關資料類型的詳細資訊，請參閱公共XDM儲存庫：

* [填充示例](https://github.com/adobe/xdm/blob/master/components/datatypes/industry-verticals/implementationdetails.example.1.json)
* [完整架構](https://github.com/adobe/xdm/blob/master/components/datatypes/industry-verticals/implementationdetails.schema.json)
