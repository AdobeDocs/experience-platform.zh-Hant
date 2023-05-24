---
title: 印刷資料類型
description: 本文檔概述了Impress XDM資料類型。
exl-id: 1e758043-a41e-45f7-ae8b-514990d0649e
source-git-commit: afdac5ce2ed967b4688d456a586c946bc2cf4179
workflow-type: tm+mt
source-wordcount: '138'
ht-degree: 4%

---

# [!UICONTROL 印象] 資料類型

[!UICONTROL 印象] 是描述市場營銷印象的標準XDM資料類型，該資料類型是用於量化廣告、數字帖子或網頁等內容的數字視圖或預訂數量的度量。

![](../images/data-types/impressions.png)

| 屬性 | 資料類型 | 說明 |
| --- | --- | --- |
| `ID` | 字串 | 印象的唯一ID。 |
| `displays` | 整數 | 向客戶顯示印象項的次數。 |
| `selected` | 整數 | 選擇或按一下印象項的次數。 |
| `type` | 字串 | 印象類型。 |

{style="table-layout:auto"}

有關欄位組的詳細資訊，請參閱公共XDM儲存庫：

* [填充示例](https://github.com/adobe/xdm/blob/master/components/datatypes/industry-verticals/impressions.example.1.json)
* [完整架構](https://github.com/adobe/xdm/blob/master/components/datatypes/industry-verticals/impressions.schema.json)
