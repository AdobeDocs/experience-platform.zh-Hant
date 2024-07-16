---
title: 曝光數資料型別
description: 瞭解曝光數XDM資料型別。
exl-id: 1e758043-a41e-45f7-ae8b-514990d0649e
source-git-commit: de8e944cfec3b52d25bb02bcfebe57d6a2a35e39
workflow-type: tm+mt
source-wordcount: '115'
ht-degree: 6%

---

# [!UICONTROL 曝光次數]資料型別

[!UICONTROL 曝光數]是描述行銷曝光數的標準XDM資料型別，這是用來量化廣告、數位貼文或網頁等內容數位檢視或參與次數的量度。

![](../images/data-types/impressions.png)

| 屬性 | 資料類型 | 說明 |
| --- | --- | --- |
| `ID` | 字串 | 閱聽的唯一ID。 |
| `displays` | 整數 | 閱聽專案已向客戶顯示的次數。 |
| `selected` | 整數 | 已選取或點選曝光專案的次數。 |
| `type` | 字串 | 閱聽型別。 |

{style="table-layout:auto"}

如需欄位群組的詳細資訊，請參閱公用XDM存放庫：

* [已填入範例](https://github.com/adobe/xdm/blob/master/components/datatypes/industry-verticals/impressions.example.1.json)
* [完整結構描述](https://github.com/adobe/xdm/blob/master/components/datatypes/industry-verticals/impressions.schema.json)
