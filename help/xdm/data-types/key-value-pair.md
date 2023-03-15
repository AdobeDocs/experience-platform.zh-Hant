---
title: 鍵值對資料類型
description: 本檔案概略介紹Experience Data Model(XDM)資料類型。
exl-id: 2a1a7537-9019-4cf2-bfa1-9c760f9656dd
source-git-commit: 1d023ce6184e54693401eb68a04ceeb1464dcaa0
workflow-type: tm+mt
source-wordcount: '118'
ht-degree: 3%

---

# [!UICONTROL 索引鍵值組] 資料類型

[!UICONTROL 索引鍵值組] 是標準的Experience Data Model(XDM)資料類型，可擷取一般索引鍵值組的詳細資訊。 此資料類型用於 [[!UICONTROL Adobe Analytics ExperienceEvent完整擴充功能] 欄位群組](../field-groups/event/analytics-full-extension.md) 說明清單變數的陣列項目。

![鍵值對結構](../images/data-types/key-value-pair.png)

| 屬性 | 資料類型 | 說明 |
| --- | --- | --- |
| `key` | 字串 | 一般變數或值的索引鍵（名稱）。 |
| `value` | 字串 | 變數的值。 |

{style="table-layout:auto"}

如需資料類型的詳細資訊，請參閱 [公用XDM存放庫](https://github.com/adobe/xdm/blob/master/extensions/adobe/experience/analytics/keyvalue.schema.json).
