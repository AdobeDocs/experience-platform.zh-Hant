---
keywords: Experience Platform；首頁；熱門主題
solution: Experience Platform
title: XDM模式和描述符
topic-legacy: tutorial
type: Tutorial
description: 標準化和互操作性是Adobe Experience Platform背後的關鍵概念。 Experience Data Model(XDM)是由Adobe驅動，旨在標準化客戶體驗資料並定義客戶體驗管理的架構。 架構是描述Experience Platform中資料的標準方式，可讓符合架構的所有資料可重複使用，而不會在組織間產生衝突，甚至可在多個組織間共用。
exl-id: 1cdc45d7-57ca-4a2d-99a4-9a8cd885a511
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '478'
ht-degree: 0%

---

# 使用[!DNL Experience Data Model](XDM)模式和關係描述符

標準化和互操作性是Adobe Experience Platform背後的關鍵概念。 [!DNL Experience Data Model] (XDM)由Adobe驅動，旨在標準化客戶體驗資料並定義客戶體驗管理的架構。方案是描述[!DNL Experience Platform]中資料的標準方式，可讓符合方案的所有資料重複使用，而不會在組織間產生衝突，甚至可在多個組織間共用。 要瞭解有關XDM架構的更多資訊，請從閱讀[XDM系統概述](../xdm/home.md)開始。

## 使用方案註冊表建立方案

方案註冊表提供用戶介面和REST風格的API，您可以從中查看和管理Adobe Experience Platform方案庫中的所有資源。 方案庫包含由Adobe、[!DNL Experience Platform]合作夥伴和您使用的應用程式的供應商提供的資源，以及您定義並保存到方案註冊表的資源。 要瞭解如何為組織建立架構，請遵循使用架構註冊表API](../xdm/tutorials/create-schema-api.md)或[使用架構編輯器用戶介面](../xdm/tutorials/create-schema-ui.md)建立架構的教程。[

## 定義兩個方案之間的關係

瞭解客戶之間的關係以及客戶與品牌之間跨不同通道的互動是Adobe Experience Platform的重要組成部分。 在[!DNL Experience Data Model](XDM)結構中定義這些關係可讓您獲得客戶資料的複雜見解。 這些關係描述符可以使用方案註冊表API和方案編輯器UI來定義。 如需詳細資訊，請參閱使用API](../xdm/tutorials/relationship-api.md)或使用UI](../xdm/tutorials/relationship-ui.md)來定義兩個結構[之間關係的教學課程。[

## 建立臨機結構

在特定情況下，可能需要建立[!DNL Experience Data Model](XDM)架構，其中欄位的名稱僅限單一資料集使用。 這稱為「臨機」架構。 臨機結構描述用於[!DNL Experience Platform]的各種[資料擷取](../ingestion/home.md)工作流程，包括擷取CSV檔案並建立特定種類的[來源連線](../sources/home.md)。 建立臨機架構是使用「架構註冊表API」來完成的，其用途是與其他[!DNL Experience Platform]教學課程搭配使用，這些教學課程需要在工作流程中建立臨機架構。 若要開始建立臨機結構，請參閱使用API](../xdm/tutorials/ad-hoc.md)建立臨機結構的教學課程。[

## 後續步驟

在為組織定義結構描述後，您可以開始建立資料集，以便將資料收入其中。 若要開始，請參閱下列檔案：

* [資料集總覽](../catalog/datasets/overview.md)
* [資料擷取概觀](../ingestion/home.md)
