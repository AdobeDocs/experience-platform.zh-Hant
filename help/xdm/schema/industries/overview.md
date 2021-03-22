---
solution: Experience Platform
title: 產業資料模型概觀
topic: 概述
description: 瞭解各種產業的標準化資料模型，這些模型可使用標準的體驗資料模型(XDM)元件來建立。
translation-type: tm+mt
source-git-commit: 6a7aebb64a533158f7ab17af0cd28243aeda0eca
workflow-type: tm+mt
source-wordcount: '512'
ht-degree: 0%

---


# 業界資料模型概觀

Experience Data Model(XDM)可讓您建立高度可自訂的結構描述，以擷取與您的業務相關的關鍵客戶體驗資料。 為協助簡化建立資料模型以符合XDM的程式，Adobe Experience Platform提供一套多功能的標準XDM元件，可擷取多個產業常用的概念。

>[!NOTE]
>
>新的標準XDM元件不斷推出，以滿足消費者的最佳需求。 如需最新元件的清單，您可以[探索UI](../../ui/explore.md)中的現有資源，或參考GitHub上的[官方XDM儲存庫](https://github.com/adobe/xdm/tree/master/components)。

根據您的業務所處的行業，某些XDM元件與您的需求的關聯性會高於其他元件。 此外，您在XDM架構之間建立的關係會因您的產業而異。

為了協助您根據特定產業制定資料模型策略，本指南提供數個受支援產業的實體關係圖(ERD)參考。

## 先決條件

要閱讀本指南中引用的ERD，您必須瞭解XDM元件如何進行交互以形成模式，以及XDM模式如何在整個Experience Platform中運行。 請確定您已閱讀下列概述檔案，然後再繼續：

* [XDM系統概述](../../home.md):瞭解XDM如何在平台生態系統中運作。
* [架構構成基礎](../../schema/composition.md):瞭解XDM元件（例如混合、類別和資料類型）對架構結構以及身分欄位角色的貢獻。

建議您檢閱[資料模型最佳實務指南](../../schema/best-practices.md)，以瞭解如何將資料對應至XDM的一般准則。

## 行業資料模型ERD {#erds}

以下ERD代表的業界垂直模型是以去標準化方式刻意建立的，並考量資料在平台中的儲存方式。

對於給定的ERD，中顯示的每個實體都基於基礎的XDM類。 對於給定實體，在&#x200B;**bold**&#x200B;中標籤的每一行代表混音或資料類型，其提供的相關欄位以未加粗文本列出。 指定實體的最重要欄位會以紅色反白顯示。

>[!NOTE]
>
>某些實體可能包含「_ID」欄位。 這代表平台在擷取事件或描述檔實體時自動指派給它們的唯一識別碼(`_id`)。 不過，如有需要，您可以選擇為此欄位使用您自己的唯一ID值。

所有可用於識別個別客戶的屬性都標示為「身分」，其中一個屬性標示為「主要身分」。

實體關係會標示為不相依，因為基於Cookie的事件通常無法判斷進行交易的人員或個人。

ERD適用於下列垂直產業：

* [[!UICONTROL Retail]](./retail.md)
* [[!UICONTROL Financial services]](./financial.md)
* [[!UICONTROL Travel and hospitality]](./travel-hospitality.md)
* [[!UICONTROL Telecommunications]](./telecom.md)

## 後續步驟

本檔案概述了行業資料模型ERD以及如何解釋它們。 要查看ERD，請從上面的清單中選擇一個。