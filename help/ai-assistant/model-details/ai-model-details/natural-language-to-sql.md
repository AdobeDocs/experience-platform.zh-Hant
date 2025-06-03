---
title: AI助理自然語言到SQL模型詳細資料
description: 瞭解AI Assistant Natural Language to SQL AI模型。
hide: true
hidefromtoc: true
exl-id: ca157945-5f74-45d0-9d40-c65d09a8e80d
source-git-commit: a8cc7c6f202cdd2786a69e548810b3957d69fdb3
workflow-type: tm+mt
source-wordcount: '632'
ht-degree: 0%

---

# AI助理作業分析自然語言到SQL模型詳細資料

## 模型概覽 {#model-overview}

* **模型名稱和版本**： Adobe Experience Platform AI Assistant Operational Insights Natural Language to SQL Model ([!DNL NL2SQL])。
* **模型發行日期**： 2025年2月
* **模型用途**：模型旨在將客戶有關營運見解的自然語言查詢轉譯為SQL查詢。 這些SQL查詢會在Adobe Experience Platform知識圖表上執行，該圖表包含有關客戶Experience Platform實體的中繼資料，例如結構描述、資料集、對象、目的地和歷程。 接著，SQL查詢的結果會用於產生客戶原始自然語言問題的回應。
* **目標使用者**：此模型的主要使用者是行銷專業人員、資料分析師或客戶歷程經理，他們想要使用自然語言瞭解Experience Platform中的營運分析並據以行動。 他們可能不是SQL或資料工程方面的專家，但需要有關其Experience Platform實體的快速、準確答案，以做出明智的決策並最佳化客戶體驗。
* **使用案例**：此模型可協助使用者存取其Experience Platform實體的中繼資料，例如對象、歷程、結構描述、屬性、資料集和目的地。 使用者可以使用自然語言提出問題，例如哪些對象已啟用或哪些對象正在使用特定架構，而模型會透過Experience Platform知識圖表將這些問題轉譯為SQL查詢。 這可讓使用者快速獲得運營可見度，並做出明智決策，而無需手動探索或查詢系統。
* **痛點**：此模型可解決使用Experience Platform的業務使用者和分析師所面臨的關鍵痛點，例如導覽大量相互連線中繼資料的複雜性、手動撰寫SQL查詢以擷取營運深入分析的需求，以及無法深入瞭解Experience Platform實體（如受眾、資料集和歷程）如何連線或執行。 藉由啟用對中繼資料的自然語言存取並自動化SQL產生，此模型減少對技術資源的依賴、縮短insight探索時間，並讓使用者能夠更快速作出資料導向式決策。

## 模型詳細資料 {#model-details}

* **模型型別**： LLM提示與動態內容內學習
* **輸入**：使用者自然語言查詢。
* **輸出**：模型會輸出[!DNL Snowflake]語法的SQL查詢，這些查詢將透過Experience Platform知識圖表執行。

**範例輸入**

```console
How many datasets were created within the last 10 days?
```

**範例輸出**

```SQL
SELECT
    COUNT(*) AS datasetCount 
FROM hkg_dim_dataset 
WHERE
    createdTime >= DATEADD(day, -10, CURRENT_DATE);
```

## 模型評估 {#model-evaluation}

* **評估量度和程式**：使用正確性評估模型。 例如，在所有[!DNL NL2SQL]個要求中，有多少要求會產生正確的SQL結果。 評估程式是以規則為基礎的比對（SQL標準化，然後是直接SQL字串比對）、以LLM為基礎的SQL求解器以及人力評估的組合。
* **評估資料與預先處理**：我們使用開放集進行回歸測試，而且我們也有每週的註解專案，透過抽樣的實際客戶流量來監視模型的效能。

## 模型部署 {#model-deployment}

* **模型監視**：基底模型由[!DNL Azure]代管。
* **模型更新**：模型會透過問題庫擴充每週定期更新。 模型也會視需要透過新的提示策略和指示更新。

## 公平性和偏差 {#fairness-and-bias}

* **模型公平性**：為了確保模型能一致地解譯和產生不同使用者意圖和語言差異的查詢，而不會引入偏見或強化成見，Adobe會使用立即的稽核、解釋功能，以及避免產生有偏見或不道德的輸出。
* **資料偏差**：模型輸出會受到In-Context Learning範例的影響，以及擷取器選取到提示中的內容。 問題庫的範例包含從「產品管理」的角度來看，被視為具有代表性的範例。 根據使用案例，客戶應考慮模型輸出中的潛在偏差如何與其預期應用程式相符或影響。

## 道德考量 {#ethical-considerations}

**與模型相關的道德考量**：為了避免公開PII或敏感屬性，模型已設計為避免強化現有的資料偏見並遵守存取控制邊界。 這包括篩選、標籤和稽核架構欄位，以負責地使用。
