---
keywords: Experience Platform;home；熱門主題；模式；模式；XDM;fields；模式；Schemas;Web交互；datatype；資料類型；
solution: Experience Platform
title: 網頁互動資料類型
topic: overview
description: 本檔案提供網路互動體驗資料模型(XDM)資料類型的概觀。
translation-type: tm+mt
source-git-commit: d282ea5526a05b28c6a82470eabf23e44d1fb420
workflow-type: tm+mt
source-wordcount: '187'
ht-degree: 2%

---


# [!UICONTROL 網頁互] 動資料類型

[!UICONTROL Web互] 動是標準的「體驗資料模型」(XDM)資料類型，可說明初次頁面載入完成後，網頁上發生的互動資訊。它可用來錄制不會觸發新頁面載入(例如單頁網頁應用程式(SPA))的豐富型網頁應用程式互動。

<img src="../images/data-types/web-interaction.PNG" width="500" /><br />

| 屬性 | 資料類型 | 說明 |
| --- | --- | --- |
| `linkClicks` | [[!UICONTROL 測量]](./measure.md) | 追蹤網頁連結點按的測量。 |
| `URL` | 字串 | 用於此Web互動的實際連結或URL。 |
| `name` | 字串 | 用於此Web連結的規範名稱。 這用於分類用途。 |
| `type` | 字串 | 連結類型。 此屬性必須等於下列其中一個列舉值： <li> `download` </li> <li> `exit` </li> <li> `other` </li> |

有關資料類型的詳細資訊，請參閱公共XDM儲存庫：

* [填入的範例](https://github.com/adobe/xdm/blob/master/components/datatypes/web/webinteraction.example.1.json)
* [完整架構](https://github.com/adobe/xdm/blob/master/components/datatypes/web/webinteraction.schema.json)