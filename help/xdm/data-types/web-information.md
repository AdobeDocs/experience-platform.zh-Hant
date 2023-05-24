---
keywords: Experience Platform；首頁；熱門主題；模式；模式；XDM；欄位；模式；模式；網頁詳細資訊；資料類型；資料類型；網頁
solution: Experience Platform
title: Web資訊資料類型
description: 本文檔概述了Web資訊體驗資料模型(XDM)資料類型。
exl-id: bfb00835-5908-4baf-af2a-6d845710e340
source-git-commit: 60c0bd62b4effaa161c61ab304718ab8c20a06e1
workflow-type: tm+mt
source-wordcount: '187'
ht-degree: 1%

---

# [!UICONTROL Web資訊] 資料類型

[!UICONTROL Web資訊] 是標準體驗資料模型(XDM)資料類型，它描述通過特定於萬維網渠道的體驗事件記錄的資訊，包括與頁面交互相關的網頁、引用者和/或連結。

![](../images/data-types/web-information.png)

| 屬性 | 資料類型 | 說明 |
| --- | --- | --- |
| `webInteraction` | [[!UICONTROL Web交互]](./web-interaction.md) | 描述有關與交互對應的Web連結或URL的詳細資訊。 |
| `webPageDetails` | [[!UICONTROL 網頁詳細資訊]](./webpage-details.md) | 描述有關發生Web交互的網頁的詳細資訊。 |
| `webReferrer` | [!UICONTROL 物件] | 描述Web交互的引用者，該引用者是訪問者在記錄當前Web交互之前的URL。 包含以下子屬性： <ul><li>`URL`:引用者URL。</li><li>`type`:參考型別。</li></ul> |

{style="table-layout:auto"}

有關資料類型的詳細資訊，請參閱公共XDM儲存庫：

* [填充示例](https://github.com/adobe/xdm/blob/master/components/datatypes/webinfo.example.1.json)
* [完整架構](https://github.com/adobe/xdm/blob/master/components/datatypes/webinfo.schema.json)
