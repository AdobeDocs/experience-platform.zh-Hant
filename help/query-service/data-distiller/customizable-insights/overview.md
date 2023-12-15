---
title: 可自訂的見解
description: 瞭解使用案例、基本功能，以及使用Data Distiller開發可自訂見解儀表板的必要步驟。 探索Data Distiller內的可自訂深入分析功能如何提升透明度，並取得不同維度（例如設定檔、受眾、行銷活動、歷程、權益和同意）的營運深入分析。
source-git-commit: 18c1d32bbc2732c38a9c37ee8fb9d36a23d4e515
workflow-type: tm+mt
source-wordcount: '886'
ht-degree: 0%

---

# 可自訂的見解

使用Data Distiller的可自訂深入分析，建立量身打造的報表資料模型以擷取更深入的深入分析、最佳化策略，並調整分析以符合特定業務需求。 使用可自訂深入分析功能來增強透明度，並從Adobe Experience Platform資料跨維度（例如設定檔、對象、行銷活動、歷程、權益和同意）取得營運深入分析。 此功能提供多功能、最適化解決方案，根據您的特定業務需求量身打造貴組織的報表資料模型。

本文介紹使用案例、基本功能，以及使用Data Distiller開發可自訂見解儀表板的必要步驟。

## 先決條件

本教學課程使用使用者定義儀表板，在Platform UI中以視覺效果呈現自訂資料模型中的資料。 請參閱 [使用者定義控制面板檔案](../../../dashboards/user-defined-dashboards.md) 以進一步瞭解此功能。

## 快速入門

您必須使用Data Distiller SKU來建立自訂資料模型，以利您的報表深入分析，並擴充內含豐富Platform資料的Real-Time CDP資料模型。 請參閱 [封裝](../../packaging.md)， [護欄](../../guardrails.md#query-accelerated-store)、和  [授權](../../data-distiller/license-usage.md) 與資料Distiller SKU相關的檔案。 如果您沒有Data Distiller SKU，請聯絡您的Adobe客戶服務代表以取得更多資訊。

## 可自訂的深入分析使用案例 {#use-cases}

以下是一些常見的使用案例，可透過Data Distiller中的可自訂深入分析有效解決。

### 設定檔與對象使用透明度 {#usage-transparency}

**挑戰：** 如何依特定條件劃分關鍵績效指標(KPI)，例如業務單位、忠誠度狀態或客戶期限值(CLTV)。

**可自訂的Insights解決方案：** Data Distiller可擴充Adobe Experience Platform中的報表資料模型，以便 [新增自訂設定檔屬性，例如CLTV](../../use-cases/customer-lifetime-value.md) 或忠誠度狀態。

### 同意異常追蹤 {#consent-anomaly-tracking}

**挑戰：** 如何將對象重疊和大小趨勢線報表套用至電子郵件、簡訊和電話等管道的自訂同意屬性。

**可自訂的Insights解決方案：** 報表資料模型可延伸以追蹤同意偏好設定在一段時間內的變更。 這涉及建立其他事實和維度表格，以分析同意偏好設定和排程的趨勢 [增量資料重新整理](../../key-concepts/incremental-load.md).

### 最佳化對象細分策略 {#optimize-audience-segmentation-strategy}

**挑戰：** 如何將機器學習(ML)模型產生的傾向分數整合到其對象KPI報表中。

**可自訂的Insights解決方案：** Data Distiller允許包含 [自訂ML模型的傾向分數](../../use-cases/propensity-score.md)，促進在對象層級計算彙總分數。 然後可將此資料與標準KPI一起報告。

### 對象擴展 {#audience-expansion}

**挑戰：** 如何在受眾重疊報表中取得不只是設定檔計數，以及取得其他人口統計資料或偏好設定來指導受眾擴張策略。

**可自訂的Insights解決方案：** 透過擴充報表資料模型，使用者可以合併其他設定檔屬性，利用相關的人口統計資料和偏好設定來豐富受眾重疊報表。

## 產生可自訂深入分析的重要功能 {#key-capabilities}

下圖著重說明產生可自訂深入分析的幾個基本功能。 這些功能包括：

1. **資料視覺效果：** 結合趨勢和長條圖等視覺元素，以全面檢視資料趨勢。
1. **控制面板製作：** 啟用建立根據特定使用案例量身打造的自訂控制面板，提供更個人化且更具針對性的分析體驗。
1. **彈性的SQL資料模型化：** 使用通用的SQL資料模型方法，讓使用者能夠順暢地組合及操控不同的資料集，進而增強適應性和分析深度。
1. **加速商店：** 實作加速的存放區機制，以透過SQL有效率地提供彙總的深入分析，確保簡化並快速存取有價值的資訊。
1. **BI連線：** 促進與熱門Business Intelligence(BI)工具(包括Power BI、Tableau、Looker和Apache Superset)的緊密整合。 此連線可確保與多種BI環境的相容性，讓使用者能夠靈活使用所選取的工具，進行深入分析和報告。

![資料Distiller可自訂深入分析主要功能的視覺表示。](../../images/data-distiller/customizable-insights/key-capabilities-of-customizable-insights.png)

## 建立可自訂深入分析的步驟 {#steps-to-create}

若要在Data Distiller中開發可自訂的深入分析控制面板，請遵循下列逐步指示。

1. **隨選查詢探索：** 從執行特定開始 `SELECT` 查詢，以探索data lake上的原始資料。 這允許對實驗進行即時、探索性資料分析，並驗證未將查詢結果儲存在Data Lake中的資料。
1. **批次查詢使用率：** 使用批次查詢來 [建立排程的工作](../../api/scheduled-queries.md#create-a-new-scheduled-query) 用於產生見解彙總表格，確保資料處理的系統和自動化方法。 批次查詢執行 `INSERT TABLE AS SELECT` 和 `CREATE TABLE AS SELECT` 進行查詢，以清除、塑形、操控及擴充資料。 這些查詢的結果會儲存在Data Lake中。
1. **正在載入彙總的深入分析：** 將產生的彙總見解載入加速存放區，並使用SQL來測試查詢，並確保資料擷取的準確性和效率。 若要瞭解如何 [對加速存放區進行無狀態查詢](../../api/accelerated-queries.md)，請參閱檔案。
1. **存取與整合：** 透過與Adobe Experience Platform整合，順暢地存取加速存放區中儲存的深入分析 [使用者定義儀表板](../../../dashboards/user-defined-dashboards.md) 或其他偏好的Business Intelligence(BI)工具。 這些與協力廠商使用者端的整合讓使用者獲得有凝聚力的直覺式體驗。

![此資訊圖表說明在Data Distiller中自訂前瞻分析的四個步驟。](../../images/data-distiller/customizable-insights/steps-to-customizable-insights.png)

## 後續步驟

閱讀本檔案後，您現在已能更妥善地瞭解使用案例、基本功能，以及使用Data Distiller開發可自訂見解儀表板的必要步驟。 若要繼續瞭解如何建立量身打造的報表資料模型，請參閱 [報表見解資料模型指南](./reporting-insights-data-model.md).
