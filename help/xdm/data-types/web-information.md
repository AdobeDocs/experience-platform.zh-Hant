---
keywords: Experience Platform；首頁；熱門主題；方案；方案； XDM；欄位；方案；方案；網頁詳細資訊；資料類型；資料類型；網頁
solution: Experience Platform
title: Web資訊資料類型
topic-legacy: overview
description: 本檔案概述Experience Data Model(XDM)資料類型的網頁資訊。
source-git-commit: b22dce52563d5f3bbd1796c11d7c7b2a49fa6d5f
workflow-type: tm+mt
source-wordcount: '192'
ht-degree: 3%

---

# [!UICONTROL Web資] 訊資料類型

[!UICONTROL 網] 頁資訊是標準的體驗資料模型(XDM)資料類型，可說明透過特定於全球資訊網管道的體驗事件所記錄的資訊，包括網頁、反向連結及/或與頁面互動相關的連結。

![](../images/data-types/web-information.png)

| 屬性 | 資料類型 | 說明 |
| --- | --- | --- |
| `webInteraction` | [[!UICONTROL 網路互動]](./web-interaction.md) | 說明與互動對應之網頁連結或URL的詳細資訊。 |
| `webPageDetails` | [[!UICONTROL 網頁詳細資訊]](./webpage-details.md) | 說明發生Web互動的網頁的詳細資訊。 |
| `webReferrer` | [!UICONTROL 物件] | 說明網頁互動的反向連結，即訪客在記錄目前的網頁互動前所來的URL。 包含下列子屬性： <ul><li>`URL`:反向連結URL。</li><li>`type`:反向連結類型。</li></ul> |

{style=&quot;table-layout:auto&quot;}

如需資料類型的詳細資訊，請參閱公用XDM存放庫：

* [填入範例](https://github.com/adobe/xdm/blob/master/components/datatypes/web/webinfo.example.1.json)
* [完整結構](https://github.com/adobe/xdm/blob/master/components/datatypes/web/webinfo.schema.json)
