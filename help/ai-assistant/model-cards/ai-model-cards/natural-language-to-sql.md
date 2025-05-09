---
title: AI助理自然語言到SQL模型卡
description: 瞭解AI Assistant Natural Language to SQL AI模型。
hide: true
hidefromtoc: true
source-git-commit: 70b705a7c6df24ad9549c46832ff4898253670ac
workflow-type: tm+mt
source-wordcount: '0'
ht-degree: 0%

---

# AI助理作業分析自然語言到SQL模型卡

## 模型概覽 {#model-overview}

* 模型的正式名稱為AI Assistant Operational Insights Natural Language to SQL Model ([!DNL NL2SQL])，並於2025年2月在其最新GA版本中發行。
* 此模型旨在將客戶有關營運見解的自然語言查詢轉譯為SQL查詢。 這些SQL查詢會在Adobe Experience Platform知識圖表上執行，該圖表包含有關客戶Experience Platform實體的中繼資料，例如結構描述、資料集、對象、目的地和歷程。 接著，SQL查詢的結果會用於產生客戶原始自然語言問題的回應。
* 此模型的主要使用者是行銷專業人員、資料分析師或客戶歷程經理，他們試圖使用自然語言在Experience Platform中瞭解營運見解並採取行動。 他們可能不是SQL或資料工程方面的專家，但需要有關其Experience Platform實體的快速、準確答案，以做出明智的決策並最佳化客戶體驗。
* 此模型是用於Operational Insights的AI助理的一部分，可幫助使用者存取其Experience Platform實體的中繼資料，例如受眾、歷程、結構描述、屬性、資料集和目的地。 使用者可以使用自然語言提出問題，例如哪些對象已啟用或哪些對象正在使用特定架構，而模型會透過Experience Platform知識圖表將這些問題轉譯為SQL查詢。 這可讓使用者快速獲得運營可見度，並做出明智決策，而無需手動探索或查詢系統。
* 此模型解決使用Experience Platform的業務使用者和分析師面臨的關鍵棘手問題，例如導覽大量相互連線中繼資料的複雜性、手動撰寫SQL查詢以擷取營運深入分析的需求，以及缺乏對Experience Platform實體（如受眾、資料集和歷程）如何連線或執行的透明度。 藉由啟用對中繼資料的自然語言存取並自動化SQL產生，此模型減少對技術資源的依賴、縮短insight探索時間，並讓使用者能夠更快速作出資料導向式決策。
* 模型不應用來存取或推斷個人識別資訊(PII)，例如客戶名稱、電子郵件地址或電話號碼，即使此類資料存在於平台中亦然。
* 此外，也不應依賴它來進行合規性或治理檢查，例如驗證資料保留原則、存取控制規則或同意狀態。 這些工作需要專門的系統和策略。

## 模型詳細資料 {#model-details}

* 模型型別為「LLM提示」及「動態內文學習」。
* 模型輸入是使用者自然語言查詢。
* 模型會輸出[!DNL Snowflake]語法的SQL查詢，這些查詢會透過Experience Platform知識圖形執行。

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

## 模型訓練 {#model-training}

* [!DNL NL2SQL]已使用[!DNL OpenAI]個GPT型模型用於內容學習。
* [!DNL NL2SQL]問題庫包含來自[!DNL Operational Insights]團隊的428個查詢以及來自Alpha使用案例的外部團隊的524個查詢。

## 模型評估 {#model-evaluation}

* 使用精確度來評估模型。 例如，在所有[!DNL NL2SQL]個要求中，有多少要求會產生正確的SQL結果。
* 評估程式是以規則為基礎的比對（SQL標準化，然後是直接SQL字串比對）、以LLM為基礎的SQL求解器以及人力評估的組合
* 開放集用於回歸測試，每週附註專案透過取樣的實際客戶流量監控模型的效能。
* 在對抗評估方面，有單獨的範圍內和範圍外模型，可作為[!DNL NL2SQL]的護欄。

## 模型部署 {#model-deployment}

* LLM模型是以GPT為基礎的模型，由[!DNL Azure OpenAI]個API代管。
* 基礎模型由[!DNL Azure]代管。
* 透過問題庫擴展，該模型每週定期更新。 模式也會視需要透過新的提示策略和指示更新。

## 說明 {#explainability}

模型會針對SQL使用個別的說明模型。

## 公平性和偏差 {#fairness-and-bias}

* 為確保模型能針對不同的使用者意圖和語言變體進行一致的解釋和產生查詢，而不會引入偏見或強化刻板印象，Adobe會使用立即稽核、解釋和防護措施，避免產生有偏見或不道德的輸出。
* 模型輸出會受內容感知學習範例的影響，以及擷取器選取到提示中的內容。 問題庫的範例包含了在執行總裁看來具有代表性的範例，而且我們根據真實的客戶流量擴充問題庫。

## 穩健性 {#robustness}

由於它收到的大部分查詢不在問題庫中涵蓋，因此生產流量的準確性反映了模型的穩健性。

## 隱私權與安全性考量事項 {#privacy-and-security-considerations}

此模型不會處理或保留任何個人識別資訊(PII)，而且這些資訊會隱藏起來，以產生SQL。 針對以屬性為基礎的存取控制許可權檢查，Experience Platform知識圖團隊將進一步處理產生的SQL，以確保治理品質。

## 道德考量 {#ethical-considerations}

為了避免公開PII或敏感屬性，此模型旨在支援隱私權、避免強化現有的資料偏見，並遵守存取控制邊界。 這包括篩選、標籤和稽核架構欄位，以負責地使用。

