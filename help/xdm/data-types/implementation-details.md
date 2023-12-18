---
title: 實作詳細資料型別
description: 瞭解實作詳細資料Experience Data Model (XDM)資料型別。
exl-id: d3d16bae-196b-489d-8590-fd22150eedf1
source-git-commit: de8e944cfec3b52d25bb02bcfebe57d6a2a35e39
workflow-type: tm+mt
source-wordcount: '101'
ht-degree: 6%

---

# [!UICONTROL 實作詳細資料] 資料型別

[!UICONTROL 實作詳細資料] 是標準的體驗資料模型(XDM)資料型別，可描述技術實作，例如API或SDK。

![資料型別結構](../images/data-types/implementation-details.png)

| 屬性 | 資料類型 | 說明 |
| --- | --- | --- |
| `environment` | 字串 | 實作的環境。 |
| `name` | 字串 | SDK或端點的識別碼。 所有SDK或端點會透過URI識別，包括擴充功能。 |
| `version` | 字串 | API或SDK的版本。 |

{style="table-layout:auto"}

如需資料型別的詳細資訊，請參閱公用XDM存放庫：

* [填入範例](https://github.com/adobe/xdm/blob/master/components/datatypes/industry-verticals/implementationdetails.example.1.json)
* [完整結構描述](https://github.com/adobe/xdm/blob/master/components/datatypes/industry-verticals/implementationdetails.schema.json)
