---
keywords: Experience Platform；首頁；熱門主題；源；連接器；源連接器；源sdk;sdk;SDK
solution: Experience Platform
title: 源SDK概述(Beta)
topic-legacy: overview
description: Adobe Experience Platform源SDK是一組配置API，它允許您使用流服務API整合基於REST API的源，以將資料Experience Platform。
hide: true
hidefromtoc: true
exl-id: 5d5449ad-a1ba-402b-a281-0b2d8b704f32
source-git-commit: ce902e461c748e30e0307558da894a4dbdd212a4
workflow-type: tm+mt
source-wordcount: '544'
ht-degree: 0%

---

# 源SDK概述(Beta)

>[!IMPORTANT]
>
>源SDK當前處於測試版中，您的組織可能尚未訪問它。 本文檔中描述的功能可能會發生更改。

Adobe Experience Platform源SDK是一組配置API，允許您使用 [[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/) 將您的資料Experience Platform。

使用Sources SDK，您可以：

* 將新源配置到平台目錄，並使用 [!DNL Flow Service] API。
* 定義源的規範，包括與支援的身份驗證類型和獲取資源資料的方式相關的資訊。
* 為新源建立面向用戶的文檔。

Sources SDK文檔提供了使用Adobe Experience Platform源SDK配置、test和發佈與平台基於REST API的源整合的說明，並使您的源成為不斷增長的源目錄的一部分。

![目錄](./assets/catalog.png)

## 瞭解來源

平台可以從外部源接收資料，同時允許您使用平台服務來構建、標籤和增強資料。 您可以從多種來源(如Adobe應用程式、基於雲的儲存、第三方軟體和您的CRM系統)接收資料。

有關源的詳細資訊，以及要查看平台上當前支援的不同源的清單，請參見 [源概述](../home.md)。

## 建立源

通過源SDK，您可以整合您自己的基於REST API的源，並將資料帶到平台 [!DNL Flow Service]。 Sources SDK允許您通過以下方式將新源與平台整合：通過 [!DNL Flow Service] API。

請參閱上的指南 [建立新連接規範](./api/api-overview.md) 有關如何將新源整合到平台的資訊。

## 記錄源

建立源後，請參閱 [文檔指南](./documentation/doc-overview.md) 有關如何通過 [!DNL GitHub] 或通過您自己的文本編輯器。

## 高級流程

以下概述了在Experience Platform中配置源的逐步過程：

* 閱讀 [源SDK API指南](./api/api-overview.md);
   * 閱讀 [入門指南](./api/getting-started.md);
   * 按照本教程 [建立新連接規範](./api/create.md);
   * 按照本教程 [更新連接規範](./api/update-connection-specs.md);
   * 按照本教程 [將新連接規範ID添加到流規範](./api/update-flow-specs.md)
   * [提交新源](./api/submit.md)。
* 要更好地瞭解連接規範的結構和屬性，請參閱上的指南 [源SDK的配置選項](./config/config.md);
   * 請參閱上的指南 [配置身份驗證規範](./config/authspec.md);
   * 請參閱上的指南 [配置源規範](./config/sourcespec.md);
   * 請參閱上的指南 [配置瀏覽規範](./config/explorespec.md);
* 要開始記錄源，請參閱 [建立源SDK文檔概述](./documentation/doc-overview.md)
   * 你可以使用 [源API文檔模板](./documentation/template.md) 構建API文檔；
   * 你可以使用 [源UI文檔模板](./documentation/ui-template.md) 構建UI文檔；
   * 請參閱上的指南 [使用GitHub Web介面](./documentation/github.md) 有關如何使用GitHub建立文檔的步驟；
   * 請參閱上的指南 [使用文本編輯器](./documentation/text-editor.md) 有關如何使用本地電腦建立文檔的步驟。
