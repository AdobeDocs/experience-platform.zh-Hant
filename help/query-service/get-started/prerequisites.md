---
keywords: Experience Platform；查詢服務；查詢服務；查詢
title: Adobe Experience Platform查詢服務快速入門
description: 完整利用Adobe Experience Platform查詢服務的必要步驟劃分
exl-id: 36ab9354-23f9-4cb8-bcd4-00fe076386ab
source-git-commit: fa22a0ca0c79d5d62fd39de3a808f84a11a80c4d
workflow-type: tm+mt
source-wordcount: '363'
ht-degree: 1%

---

# 開始使用Adobe Experience Platform [!DNL Query Service] {#getting-started}

使用Adobe Experience Platform查詢服務針對擷取的資料集執行SQL查詢、聯結來自多個來源的資料，並產生用於分析、機器學習工作流程或即時客戶個人檔案的衍生資料集。 擷取資料後，請透過UI存取查詢服務以進行互動式分析和共同作業，或透過API存取以自動執行程式化查詢。

## 先決條件 {#prerequisites}

開始查詢資料之前，請確定您擁有：

- **必要的許可權**：您的使用者帳戶可以存取Experience Platform中的查詢服務。 如果UI中沒有此服務，請檢閱[許可權檔案](../../access-control/home.md#permissions)並連絡您的系統管理員。
- **資料擷取**：您已將資料擷取到Experience Platform。

如果您需要擷取資料，請觀看[資料擷取教學課程影片](https://experienceleague.adobe.com/docs/platform-learn/tutorials/data-ingestion/create-datasets-and-ingest-data.html)，以瞭解資料集建立、結構描述對應、擷取和驗證的概觀。 如需更深入的資訊和其他學習資源的連結，請參閱[擷取概觀檔案](../../ingestion/home.md)。

## 快速入門路徑

將資料內嵌至Experience Platform後，您就可以在Experience Platform中使用[!DNL Query Editor]或查詢服務API，開始使用查詢服務。

### [!DNL Query Editor]

使用[!DNL Query Editor]進行分析、資料探索和合作查詢開發。 如需UI功能的概述，請參閱[查詢服務UI檔案](../ui/overview.md)。 若要瞭解如何在UI中撰寫和執行查詢，請閱讀[[!DNL Query Editor user guide]](../ui/user-guide.md)。

### 查詢服務API

使用查詢服務API進行自動化工作流程、查詢範本管理和程式化整合。 請參閱[Query Service開發人員指南](../api/getting-started.md)，以取得使用Query Service API的詳細說明。

## 後續步驟

本檔案說明在Experience Platform中使用[!DNL Query Service]功能所需的先決條件。 若要快速開始使用查詢服務功能，建議您閱讀以下檔案：

- [查詢執行的一般指引](../best-practices/writing-queries.md)
- [查詢服務中的SQL語法](../sql/syntax.md)
- [使用SQL建立衍生資料集](../data-distiller/derived-datasets/create-derived-datasets-with-sql.md)

或者，若要進一步瞭解查詢服務如何在Experience Platform中改善資料處理，請觀看[放棄的瀏覽使用案例簡報](../use-cases/abandoned-browse.md#video-example)。

下列資源有助於增進您對[!DNL Query Service]的瞭解：

- [[!DNL Query Service] UI 概觀](../ui/overview.md)
- [[!DNL Query Service]認證](../ui/credentials.md)
- [使用者端連線概觀](../clients/overview.md)
