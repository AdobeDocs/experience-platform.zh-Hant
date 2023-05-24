---
keywords: Experience Platform；首頁；熱門主題；源；連接器；源連接器；源sdk;sdk;SDK
title: 自助源（批處理SDK）API指南
description: 本文檔概述了建立新源的過程，包括有關如何使用流服務API檢索、寫入和提交新連接規範的步驟。
exl-id: 7e827989-207b-41e2-84d6-5ecb754bebb6
source-git-commit: fcd44aef026c1049ccdfe5896e6199d32b4d1114
workflow-type: tm+mt
source-wordcount: '487'
ht-degree: 0%

---

# 自助源（批處理SDK）API指南

本文檔概述了建立新源的過程，包括如何使用 [[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/)。

[!DNL Flow Service] 用於收集和集中平台內不同來源的客戶資料。 該服務提供用戶介面和REST風格的API，讓您能夠輕鬆地設定到各種資料提供程式的源連接。 通過這些源連接，您可以驗證第三方系統，設定接收運行時間，並管理資料接收吞吐量。

的 [!DNL Flow Service] API提供了多個端點，允許您以寫程式方式管理通過自助源（批處理SDK）整合的新源的連接和流規範。

## 建立新連接規範

配置新源的第一步是建立新連接規範。

連接規範返回源的連接器屬性。 它們包括與建立基本連接和源連接相關的驗證規範以及分配給特定源的固定連接規範ID。 連接規範與租戶和組織無關。 典型的連接規範包含有關給定源的基本資訊，以及三個不同的部分： `authSpec`。 `sourceSpec`, `exploreSpec`。

有關詳細說明，請參閱上的指南 [建立新連接規範](./create.md)。 有關用於連接規範的屬性和值的資訊，包括有關配置驗證、源和瀏覽規範的詳細資訊，請參見 [配置選項文檔](../config/config.md)。

## 更新流規格

成功建立連接規範後，必須追加 `RestStorageToAEP` 流規範，使源能夠建立資料流。

流規範包含定義流的資訊，包括它支援的源連接ID和目標連接ID、需要應用到資料的轉換規範以及生成流所需的調度參數。

有關詳細說明，請參閱上的指南 [更新流規範](./update-flow-specs.md)。

## 更新連接規範

您可以通過向以下站點發出PUT請求來更新連接規範 [!DNL Flow Service] API。 請參閱上的指南 [更新連接規範](./update-connection-specs.md) 的子菜單。

## 提交源

要將源提交到Experience Platform，必須先完成整個 [!DNL Flow Service] 源的API工作流，以確保源成功工作。 如果源運行成功，則您可以繼續並聯繫Adobe代表以進行驗證和升級。 請參閱上的指南 [測試和提交源](./submit.md) 的

## 後續步驟

開始使用 [!DNL Flow Service] API並通過自助源（批處理SDK）建立新源，請閱讀 [入門指南](./getting-started.md) 然後選擇其中一個端點參考線，以瞭解如何使用特定端點。
