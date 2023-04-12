---
keywords: Experience Platform；首頁；熱門主題；來源；連接器；來源連接器；來源sdk;sdk; SDK
title: 自助來源（批次SDK）API指南
description: 本文檔概述了建立新源的過程，包括如何使用流服務API檢索、寫入和提交新連接規範的步驟。
exl-id: 7e827989-207b-41e2-84d6-5ecb754bebb6
source-git-commit: fcd44aef026c1049ccdfe5896e6199d32b4d1114
workflow-type: tm+mt
source-wordcount: '487'
ht-degree: 0%

---

# 自助來源（批次SDK）API指南

本文檔概述了建立新源的過程，包括如何使用 [[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/).

[!DNL Flow Service] 用於收集和集中Platform內各種不同來源的客戶資料。 此服務提供使用者介面和RESTful API，讓您輕鬆設定與各種資料提供者的來源連線。 這些來源連線可讓您驗證您的協力廠商系統、設定擷取執行的時間，以及管理資料擷取吞吐量。

此 [!DNL Flow Service] API提供數個端點，可讓您以程式設計方式管理要透過自助來源(Batch SDK)整合之新來源的連線和流程規格。

## 建立新的連接規範

配置新源的第一步是建立新的連接規範。

連接規範返回源的連接器屬性。 它們包括與建立基本連接和源連接相關的驗證規範，以及分配給特定源的固定連接規範ID。 連線規格不受租用戶和組織限制。 典型的連接規範包含有關給定源的基本資訊以及三個不同的部分： `authSpec`, `sourceSpec`，和 `exploreSpec`.

如需詳細指示，請參閱 [建立新的連接規範](./create.md). 有關用於連接規範的屬性和值的資訊，包括有關配置身份驗證、源和瀏覽規範的詳細資訊，請參閱 [配置選項文檔](../config/config.md).

## 更新流量規格

成功建立連接規範後，必須附加 `RestStorageToAEP` 流規範，使源能夠建立資料流。

流規範包含定義流的資訊，包括它支援的源和目標連接ID、需要應用於資料的轉換規範，以及生成流所需的調度參數。

如需詳細指示，請參閱 [更新流規範](./update-flow-specs.md).

## 更新連接規範

您可以向 [!DNL Flow Service] API。 請參閱 [更新連接規範](./update-connection-specs.md) 以取得更多資訊。

## 提交您的來源

若要提交整合的來源至Experience Platform，您必須先完成整個 [!DNL Flow Service] 來源的API工作流程，以確保您的來源成功運作。 如果源運行成功，則可以繼續，並聯繫Adobe代表以進行驗證和升級。 請參閱 [測試和提交您的源](./submit.md) 詳細資訊

## 後續步驟

若要開始使用 [!DNL Flow Service] API並透過自助來源（批次SDK）建立新來源，請閱讀 [快速入門手冊](./getting-started.md) 然後，選取其中一個端點指南，以了解如何使用特定端點。
