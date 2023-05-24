---
keywords: Experience Platform；首頁；熱門主題；模式；模式；XDM；欄位；模式；模式；網頁詳細資訊；資料類型；資料類型；網頁
solution: Experience Platform
title: 體驗通道資料類型
description: 本文檔概述了「體驗渠道體驗資料模型」(XDM)資料類型。
exl-id: 209654f7-0bde-439a-989c-ce2e41599105
source-git-commit: 60c0bd62b4effaa161c61ab304718ab8c20a06e1
workflow-type: tm+mt
source-wordcount: '268'
ht-degree: 2%

---

# [!UICONTROL 體驗渠道] 資料類型

[!UICONTROL 體驗渠道] 是描述體驗通道的標準體驗資料模型(XDM)資料類型。 體驗通道表示如何使用數字型驗的方法或路徑。

有多種體驗渠道，每種渠道在內容的傳遞方式、客戶互動的觀察方式以及資料的收集方式等方面都受到不同的限制。 在渠道中，經驗可以提供到特定的位置。 通道中存在的位置和類型不同於通道。

![](../images/data-types/experience-channel.png)

| 屬性 | 資料類型 | 說明 |
| --- | --- | --- |
| `_id` | 字串 | 唯一標識通道的ID。 每個特定的體驗渠道都定義一個常數 `@id`。 |
| `_type` | 字串 | 為具有相似屬性的通道提供粗分類標籤。 |
| `contentTypes` | 字串陣列 | 此渠道可提供的內容類型。 |
| `locationTypes` | 字串陣列 | 此渠道包括和可向其傳送內容的位置（虛擬位置）類型。 |
| `mediaAction` | 字串 | 描述「體驗事件」介質操作（如果適用）。 |
| `mediaType` | 字串 | 描述介質類型是付費、擁有還是獲得。 |
| `metricTypes` | 字串陣列 | 可以在此渠道中收集的度量。 |
| `mode` | 字串 | 在此渠道中如何提供體驗。 |
| `typeAtSource` | 字串 | 通道的自定義名稱。 |

{style="table-layout:auto"}

有關資料類型的詳細資訊，請參閱公共XDM儲存庫：

* [填充示例](https://github.com/adobe/xdm/blob/master/components/datatypes/channels/channel.example.1.json)
* [完整架構](https://github.com/adobe/xdm/blob/master/components/datatypes/channels/channel.schema.json)
