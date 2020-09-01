---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: XDM模式和描述符
topic: tutorial
description: 標準化和互操作性是Adobe Experience Platform的主要概念。 Adobe推動的Experience Data Model(XDM)旨在標準化客戶體驗資料並定義客戶體驗管理的架構。 結構描述是Experience Platform中描述資料的標準方式，可讓符合結構的所有資料重複使用，而不會在組織間產生衝突，甚至可在多個組織間共用。
translation-type: tm+mt
source-git-commit: d3ece56d10b1940a5992906a65a50ffe2f7e4346
workflow-type: tm+mt
source-wordcount: '473'
ht-degree: 0%

---


# 使用( [!DNL Experience Data Model] XDM)模式和關係描述符

標準化和互操作性是Adobe Experience Platform的主要概念。 [!DNL Experience Data Model] (XDM)是由Adobe推動，旨在標準化客戶體驗資料並定義客戶體驗管理的架構。 結構描述是描述中資料的標準方法 [!DNL Experience Platform]，允許符合結構的所有資料可以重複使用，而不會在組織間發生衝突，甚至可以在多個組織之間共用。 若要進一步瞭解XDM架構，請先閱讀 [XDM系統概觀](../xdm/home.md)。

## 使用方案註冊表建立方案

架構註冊表提供使用者介面和REST風格的API，您可從中檢視和管理Adobe Experience Platform架構庫中的所有資源。 架構庫包含您所使用之應用程式的Adobe、合作夥伴 [!DNL Experience Platform] 、廠商所提供的資源，以及您定義並儲存至架構註冊表的資源。 要瞭解如何為組織建立方案，請遵循使用方案註冊表API [建立方案的教程](../xdm/tutorials/create-schema-api.md) ，或 [使用方案編輯器用戶介面建立方案的教程](../xdm/tutorials/create-schema-ui.md)。

## 定義兩個方案之間的關係

Adobe Experience Platform的重要部分，在於能夠跨不同通道瞭解客戶之間的關係以及客戶與品牌之間的互動。 在(XDM)結構中定義這 [!DNL Experience Data Model] 些關係，可讓您獲得客戶資料的複雜見解。 這些關係描述符可以使用模式註冊表API和模式編輯器UI來定義。 如需詳細資訊，請參閱使用API或使用UI定義兩個 [結構間關](../xdm/tutorials/relationship-api.md)[系的教學課程](../xdm/tutorials/relationship-ui.md)。

## 建立臨機結構

在特定情況下，可能需要建立(XDM)架構，其中欄位的名稱僅限單一資料集使用。 [!DNL Experience Data Model] 這稱為「臨機」架構。 臨機結構描述用於各種資料擷 [取工作流程](../ingestion/home.md) , [!DNL Experience Platform]包括擷取CSV檔案並建立特定類型的 [來源連線](../sources/home.md)。 建立臨機架構是使用「架構註冊表API」來完成的，其目的是與其他教學課程搭配使用，而教學課程需要在工作流程中建立臨機架構。 [!DNL Experience Platform] 若要開始建立臨機結構，請參閱使用API [建立臨機結構的教學課程](../xdm/tutorials/ad-hoc.md)。

## 後續步驟

在為組織定義結構描述後，您可以開始建立資料集，以便將資料收入其中。 若要開始，請參閱下列檔案：

* [資料集總覽](../catalog/datasets/overview.md)
* [資料擷取概觀](../ingestion/home.md)