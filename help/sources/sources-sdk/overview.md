---
keywords: Experience Platform；首頁；熱門主題；來源；連接器；來源連接器；來源sdk;sdk; SDK
solution: Experience Platform
title: 來源SDK概述（測試版）
topic-legacy: overview
description: Adobe Experience Platform Sources SDK是一組設定API，可讓您使用流量服務API整合REST API型來源，將資料帶入Experience Platform。
hide: true
hidefromtoc: true
source-git-commit: 4ce9eac605fb7c801852cd0e109448d314092603
workflow-type: tm+mt
source-wordcount: '529'
ht-degree: 0%

---

# 來源SDK概述（測試版）

>[!IMPORTANT]
>
>Sources SDK目前仍在測試階段，而您的組織可能尚未取得存取權。 本檔案所述的功能可能會有所變更。

Adobe Experience Platform Sources SDK是一組設定API，可讓您使用 [[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/) 將資料帶入Experience Platform。

使用Sources SDK，您可以：

* 使用，將新來源設定為Platform目錄，並完成建立、讀取、更新和刪除功能 [!DNL Flow Service] API。
* 定義源的規範，包括與支援的驗證類型以及如何獲取資源資料相關的資訊。
* 為新來源建立面向使用者的檔案。

Sources SDK檔案提供的指示可供您使用Adobe Experience Platform Sources SDK來設定、測試及發行與Platform的REST API型來源整合，並讓您的來源成為不斷增長之來源目錄的一部分。

![目錄](./assets/catalog.png)

## 了解來源

Platform可內嵌來自外部來源的資料，同時允許您使用Platform服務來建構、加標籤及增強該資料。 您可以內嵌來自各種來源的資料，例如Adobe應用程式、雲端儲存、協力廠商軟體和您的CRM系統。

如需來源的詳細資訊，以及查看Platform上目前支援的不同來源的清單，請參閱 [來源概觀](../home.md).

## 建立來源

透過Sources SDK，您可以整合自己的REST API型來源，並將資料帶入Platform [!DNL Flow Service]. Sources SDK可讓您透過 [!DNL Flow Service] API。

請參閱 [建立新的連接規範](./api/overview.md) 以了解如何將新來源整合至Platform的資訊。

## 記錄您的來源

建立來源後，請參閱 [檔案指南](./documentation/overview.md) 有關如何通過以下方式記錄源的說明： [!DNL GitHub] 網頁介面或透過您自己的文字編輯器。

## 高級流程

在Experience Platform中配置源的逐步過程如下：

* 閱讀 [來源SDK API指南](./api/overview.md);
   * 閱讀 [快速入門手冊](./api/getting-started.md);
   * 請依照 [建立新的連接規範](./api/create.md);
   * 請依照 [更新連接規範](./api/update-connection-specs.md);
   * 請依照 [將新連接規範ID添加到流規範](./api/update-flow-specs.md)
   * [提交新源](./api/submit.md).
* 要更好地了解連接規範的結構和屬性，請參閱 [源SDK的配置選項](./config/config.md);
   * 請參閱 [配置驗證規範](./config/authspec.md);
   * 請參閱 [配置源規範](./config/sourcespec.md);
   * 請參閱 [配置瀏覽規範](./config/explorespec.md);
* 若要開始記錄來源，請參閱 [建立來源SDK檔案的概觀](./documentation/overview.md)
   * 您可以使用 [來源檔案範本](./documentation/template.md) 構造檔案；
   * 請參閱 [使用GitHub網頁介面](./documentation/github.md) 以取得使用GitHub建立檔案的步驟；
   * 請參閱 [使用文字編輯器](./documentation/text-editor.md) 以了解如何使用本機電腦建立檔案的步驟。

