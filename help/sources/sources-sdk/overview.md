---
keywords: Experience Platform；首頁；熱門主題；源；連接器；源連接器；源sdk;sdk;SDK
solution: Experience Platform
title: 自助源（批處理SDK）概述
topic-legacy: overview
description: Adobe Experience Platform自助源(Batch SDK)是一組配置API，允許您使用流服務API整合基於REST API的源，以將資料Experience Platform。
exl-id: 5d5449ad-a1ba-402b-a281-0b2d8b704f32
source-git-commit: 4d7799b01c34f4b9e4a33c130583eadcfdc3af69
workflow-type: tm+mt
source-wordcount: '596'
ht-degree: 0%

---

# 自助源（批SDK）概述

Adobe Experience Platform自助源(Batch SDK)是一個框架，它允許您使用以下元件將基於REST API的源整合到Experience Platform源目錄 [[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/)。 自助源（批處理SDK）提供了一組配置API來構建您自己的源並將批處理資料Experience Platform。

使用自助源（批處理SDK），您可以：

* 使用 [!DNL Flow Service] API。
* 定義源的規範，包括與支援的身份驗證類型和獲取資源資料的方式相關的資訊。
* 為新源建立面向用戶的文檔。

自助源文檔提供了配置、test和發佈基於REST API的源整合與Experience Platform的指導，並讓您的源成為不斷增長的源目錄的一部分。

![目錄](./assets/catalog.png)

## 瞭解來源

Experience Platform可以從外部源接收資料，同時允許您使用Experience Platform服務構造、標籤和增強該資料。 您可以從多種來源(如Adobe應用程式、基於雲的儲存、第三方軟體和您的CRM系統)接收資料。

有關源的詳細資訊，以及要查看Experience Platform當前支援的不同源的清單，請參見 [源概述](../home.md)。

## 建立源

通過自助源，您可以整合您自己的基於REST API的源，並將資料與 [!DNL Flow Service]。 通過建立、配置和提交新的連接規範，可以將源整合到Experience Platform源目錄 [!DNL Flow Service] API。

請參閱上的指南 [建立新連接規範](./api/api-overview.md) 有關如何將新源整合到Experience Platform的資訊。

## 記錄源

建立源後，請參閱 [文檔指南](./documentation/doc-overview.md) 有關如何通過 [!DNL GitHub] 或通過您自己的文本編輯器。

## 高級流程

以下概述了在Experience Platform中配置源的逐步過程：

* 閱讀 [自助源（批處理SDK）API指南](./api/api-overview.md)。
   * 閱讀 [入門指南](./api/getting-started.md)。
   * 按照本教程 [建立新連接規範](./api/create.md)。
   * 按照本教程 [更新連接規範](./api/update-connection-specs.md)。
   * 按照本教程 [將新連接規範ID添加到流規範](./api/update-flow-specs.md)
   * [提交新源](./api/submit.md)。
* 要更好地瞭解連接規範的結構和屬性，請閱讀上的指南 [自助源的配置選項（批SDK）](./config/config.md)。
   * 閱讀上的指南 [配置身份驗證規範](./config/authspec.md) 以便更好地瞭解可用於源的不同身份驗證類型。
   * 閱讀上的指南 [配置源規範](./config/sourcespec.md) 有關可為源配置的不同分頁類型、計畫格式和自定義架構的資訊。
   * 閱讀上的指南 [配置瀏覽規範](./config/explorespec.md) 有關如何定義瀏覽和檢查源中包含的對象所需的參數的資訊。
* 要開始記錄源，請閱讀 [建立自助源文檔概述](./documentation/doc-overview.md)
   * 你可以使用 [源API文檔模板](./documentation/template.md) 來構建API文檔。
   * 你可以使用 [源UI文檔模板](./documentation/ui-template.md) 來構建UI文檔。
   * 請參閱上的指南 [使用GitHub Web介面](./documentation/github.md) 有關如何使用GitHub建立文檔的步驟。
   * 請參閱上的指南 [使用文本編輯器](./documentation/text-editor.md) 有關如何使用本地電腦建立文檔的步驟。
