---
solution: Experience Platform
title: 零售行業資料模型ERD
topic-legacy: overview
description: 檢視描述零售業標準化資料模型的實體關係圖(ERD)，該模型與Experience Data Model(XDM)相容，可在Adobe Experience Platform中使用。
exl-id: 40cbb243-668b-4280-815f-1f94a06b6b87
source-git-commit: 629f47b934c59fe875a54cb13962033122097538
workflow-type: tm+mt
source-wordcount: '218'
ht-degree: 0%

---

#  零售業資料模型ERD

以下實體關係圖(ERD)代表零售行業的標準化資料模型。 ERD是刻意以非標準化方式呈現，並考慮資料在Adobe Experience Platform中的儲存方式。

使用下列圖例來解釋此ERD:

* 中顯示的每個實體都以基礎的[Experience Data Model(XDM)類別](../composition.md#class)為基礎。
* 對於指定實體，在&#x200B;**bold**&#x200B;中標籤的每一行代表欄位組或資料類型，其下提供的相關欄位以未粗體文字列出。
* 指定實體的最重要欄位會以紅色突出顯示。
* 可用於識別個別客戶的所有屬性都會標示為「身分」，其中一個屬性會標示為「主要身分」。
* 實體關係會標示為不相依，因為以Cookie為基礎的事件通常無法判斷進行交易的人員或個人。

![](../../images/industries/retail.png)

>[!NOTE]
>
>「體驗事件」實體包含「_ID」欄位，代表XDM ExperienceEvent類別所提供的唯一識別碼(`_id`)屬性。 如需此值預期內容的詳細資訊，請參閱[XDM ExperienceEvent](../../classes/experienceevent.md)上的參考檔案。