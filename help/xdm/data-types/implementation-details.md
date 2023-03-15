---
title: 實作詳細資料資料類型
description: 本檔案概略說明實作詳細資料Experience Data Model(XDM)資料類型。
exl-id: d3d16bae-196b-489d-8590-fd22150eedf1
source-git-commit: 2fd35c4ac29f43391f9dc03c636d20558b701be7
workflow-type: tm+mt
source-wordcount: '124'
ht-degree: 4%

---

# [!UICONTROL 實作詳細資料] 資料類型

[!UICONTROL 實作詳細資料] 是標準的Experience Data Model(XDM)資料類型，可說明技術實作，例如API或SDK。

![資料類型結構](../images/data-types/implementation-details.png)

| 屬性 | 資料類型 | 說明 |
| --- | --- | --- |
| `environment` | 字串 | 實作的環境。 |
| `name` | 字串 | SDK或端點的識別碼。 所有SDK或端點都透過URI來識別，包括擴充功能。 |
| `version` | 字串 | API或SDK的版本。 |

{style="table-layout:auto"}

如需資料類型的詳細資訊，請參閱公用XDM存放庫：

* [填入範例](https://github.com/adobe/xdm/blob/master/components/datatypes/industry-verticals/implementationdetails.example.1.json)
* [完整結構](https://github.com/adobe/xdm/blob/master/components/datatypes/industry-verticals/implementationdetails.schema.json)
