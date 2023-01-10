---
keywords: Experience Platform；首頁；熱門主題；方案；方案； XDM；欄位；方案；方案；網頁詳細資訊；資料類型；資料類型；網頁
solution: Experience Platform
title: Web資訊資料類型
description: 本檔案概述Experience Data Model(XDM)資料類型的網頁資訊。
exl-id: bfb00835-5908-4baf-af2a-6d845710e340
source-git-commit: 60c0bd62b4effaa161c61ab304718ab8c20a06e1
workflow-type: tm+mt
source-wordcount: '190'
ht-degree: 3%

---

# [!UICONTROL 網路資訊] 資料類型

[!UICONTROL 網路資訊] 是標準的Experience Data Model(XDM)資料類型，可說明透過Experience Event（專屬於全球資訊網管道）所記錄的資訊，包括網頁、反向連結及/或與頁面互動相關的連結。

![](../images/data-types/web-information.png)

| 屬性 | 資料類型 | 說明 |
| --- | --- | --- |
| `webInteraction` | [[!UICONTROL 網路互動]](./web-interaction.md) | 說明與互動對應之網頁連結或URL的詳細資訊。 |
| `webPageDetails` | [[!UICONTROL 網頁詳細資訊]](./webpage-details.md) | 說明發生Web互動的網頁的詳細資訊。 |
| `webReferrer` | [!UICONTROL 物件] | 說明網頁互動的反向連結，即訪客在記錄目前的網頁互動前所來的URL。 包含下列子屬性： <ul><li>`URL`:反向連結URL。</li><li>`type`:反向連結類型。</li></ul> |

{style=&quot;table-layout:auto&quot;}

如需資料類型的詳細資訊，請參閱公用XDM存放庫：

* [填入範例](https://github.com/adobe/xdm/blob/master/components/datatypes/webinfo.example.1.json)
* [完整結構](https://github.com/adobe/xdm/blob/master/components/datatypes/webinfo.schema.json)
