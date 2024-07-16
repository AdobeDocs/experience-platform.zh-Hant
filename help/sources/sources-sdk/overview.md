---
keywords: Experience Platform；首頁；熱門主題；來源；聯結器；來源聯結器；來源SDK；SDK
solution: Experience Platform
title: 自助來源（批次SDK）概觀
description: Adobe Experience Platform自助來源（批次SDK）是一組設定API，可讓您使用流程服務API整合REST API型來源，以將您的資料帶到Experience Platform。
exl-id: 5d5449ad-a1ba-402b-a281-0b2d8b704f32
source-git-commit: 59dfa862388394a68630a7136dee8e8988d0368c
workflow-type: tm+mt
source-wordcount: '592'
ht-degree: 3%

---

# 自助來源（批次SDK）概觀

Adobe Experience Platform自助來源（批次SDK）是一種架構，可讓您使用[[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/)將REST API型來源整合至Experience Platform來源目錄。 自助來源（批次SDK）提供一組設定API，用於建置您自己的來源並將您的批次資料帶入Experience Platform。

使用自助式來源（批次SDK），您可以：

* 使用[!DNL Flow Service] API設定新來源並整合至Experience Platform目錄。
* 為您的來源定義規格，包括與支援的驗證型別相關的資訊，以及如何擷取資源資料。
* 為您的新來源建立面向使用者的檔案。

自助來原始檔提供設定、測試和發行REST API型來源與Experience Platform整合的指示，並讓您的來源成為不斷成長的來源目錄的一部分。

![目錄](./assets/catalog.png)

## 瞭解來源

Experience Platform可從外部來源內嵌資料，同時允許您使用Experience Platform服務來建構、加標籤及增強這些資料。 您可以從各種來源擷取資料，例如 Adob&#x200B;&#x200B;e 應用程式、雲端型儲存空間、協力廠商軟體和 CRM 系統。

如需有關來源的詳細資訊，以及檢視Experience Platform目前支援的不同來源的清單，請參閱[來源概觀](../home.md)。

## 建立來源

透過自助來源，您可以整合您自己的REST API型來源，並將您的資料與[!DNL Flow Service]Experience Platform。 您可以透過[!DNL Flow Service] API建立、設定和提交新的連線規格，將來源整合至Experience Platform來源目錄。

請參閱[建立新連線規格](./api/api-overview.md)的指南，瞭解如何整合新來源以進行Experience Platform。

## 記錄您的來源

建立您的來源後，請參閱[檔案指南](./documentation/doc-overview.md)，瞭解如何透過[!DNL GitHub]網頁介面或您自己的文字編輯器來記錄來源的說明。

## 高階流程

以Experience Platform設定來源的逐步流程概述如下：

* 閱讀[自助式來源（批次SDK） API指南](./api/api-overview.md)。
   * 閱讀[快速入門手冊](./api/getting-started.md)。
   * 請依照有關[建立新連線規格](./api/create.md)的教學課程進行。
   * 請依照有關[更新您的連線規格](./api/update-connection-specs.md)的教學課程進行。
   * 請依照教學課程中的指示[將新的連線規格ID新增至流程規格](./api/update-flow-specs.md)
   * [送出您的新來源](./api/submit.md)。
* 若要更深入瞭解連線規格的結構和屬性，請閱讀自助來源（批次SDK）](./config/config.md)的[組態選項指南。
   * 請閱讀[設定驗證規格](./config/authspec.md)的指南，以更清楚瞭解您可以用於來源的不同驗證型別。
   * 請閱讀[設定來源規格](./config/sourcespec.md)的指南，以瞭解可針對來源設定的不同分頁型別、排程格式和自訂結構描述的相關資訊。
   * 請閱讀[設定瀏覽規格](./config/explorespec.md)的指南，瞭解如何定義瀏覽和檢查來源中所含物件所需的引數。
* 若要開始記錄您的來源，請閱讀建立自助來原始檔的[總覽](./documentation/doc-overview.md)
   * 您可以使用此[來源API檔案範本](./documentation/template.md)來建構您的API檔案。
   * 您可以使用此[來源UI檔案範本](./documentation/ui-template.md)來建構您的UI檔案。
   * 如需如何使用GitHub建立檔案的步驟，請參閱[使用GitHub網頁介面](./documentation/github.md)的指南。
   * 請參閱[使用文字編輯器](./documentation/text-editor.md)的指南，以瞭解如何使用本機電腦建立檔案的步驟。
