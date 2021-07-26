---
solution: Experience Platform
title: 旅宿業資料模型ERD
topic-legacy: overview
description: 檢視實體關係圖(ERD)，此圖表說明旅行與旅宿業的標準化資料模型，與Adobe Experience Platform中使用的Experience Data Model(XDM)相容。
exl-id: 4d454160-9066-4702-815b-9509942f709e
source-git-commit: 38fa2345cb87e50bd4c8788996f03939fb199cf9
workflow-type: tm+mt
source-wordcount: '278'
ht-degree: 0%

---

# [!UICONTROL 旅行與住] 宿業資料模型ERD

以下實體關係圖(ERD)代表旅行和旅館業的標準化資料模型。 ERD是刻意以非標準化方式呈現，並考慮資料在Adobe Experience Platform中的儲存方式。

>[!NOTE]
>
>ERD是建議，您應如何為此行業使用案例建立資料模型。 若要在Platform中使用此資料模型，您必須自行建立建議的結構描述及其關係。 如需詳細資訊，請參閱UI中管理[結構](../../ui/resources/schemas.md)和[關係](../../tutorials/relationship-ui.md)的指南。

使用下列圖例來解釋此ERD:

* 中顯示的每個實體都以基礎的[Experience Data Model(XDM)類別](../composition.md#class)為基礎。
* 對於指定實體，在&#x200B;**bold**&#x200B;中標籤的每一行代表欄位組或資料類型，其下提供的相關欄位以未粗體文字列出。
* 指定實體的最重要欄位會以紅色突出顯示。
* 可用於識別個別客戶的所有屬性都會標示為「身分」，其中一個屬性會標示為「主要身分」。
* 實體關係會標示為不相依，因為以Cookie為基礎的事件通常無法判斷進行交易的人員或個人。

![](../../images/industries/travel-hospitality.png)

>[!NOTE]
>
>「體驗事件」實體包含「_ID」欄位，代表XDM ExperienceEvent類別所提供的唯一識別碼(`_id`)屬性。 如需此值預期內容的詳細資訊，請參閱[XDM ExperienceEvent](../../classes/experienceevent.md)上的參考檔案。