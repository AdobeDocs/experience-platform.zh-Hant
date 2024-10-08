---
title: SQL深入分析
description: 瞭解使用案例、基本功能，以及使用Data Distiller開發SQL深入分析儀表板的必要步驟。 探索Data Distiller中的SQL深入分析功能如何增強透明度，並取得不同維度（例如設定檔、受眾、行銷活動、歷程、權益和同意）的營運深入分析。
exl-id: f807d0fd-c8ec-42d4-96a0-5ffc5681943b
source-git-commit: 4e78a7983fba492ded866a8f1fc6f98e20510b2b
workflow-type: tm+mt
source-wordcount: '941'
ht-degree: 0%

---

# SQL深入分析

使用Data Distiller的SQL Insights建立量身打造的報告資料模型，以擷取更深入的深入分析、最佳化策略，並調整分析以符合特定業務需求。 使用SQL Insights功能可增強透明度並從Adobe Experience Platform資料跨維度（例如設定檔、對象、行銷活動、歷程、權益和同意）取得營運深入分析。 此功能提供多功能、最適化解決方案，根據您的特定業務需求量身打造貴組織的報表資料模型。

若要[視覺化您的SQL深入分析](../../../dashboards/data-distiller/sql-insights/overview.md)，您可以使用[query pro mode](../../../dashboards/data-distiller/query-pro-mode/overview.md)以自訂SQL查詢進行複雜的分析，並將您的資料轉換為易於理解的圖表。 使用Query Pro模式可在您的控制面板上建立客製化的深入分析和視覺效果，並將您的深入分析下載為CSV檔案以迎合技術和非技術受眾。

本文介紹使用Data Distiller開發SQL深入分析控制面板的使用案例、基本功能和必要步驟。

## 先決條件

本教學課程使用使用者定義儀表板，在Platform UI中以視覺效果呈現自訂資料模型中的資料。 若要深入瞭解此功能，請參閱[使用者定義控制面板檔案](../../../dashboards/user-defined-dashboards.md)。

## 快速入門

您必須使用Data Distiller SKU來建立自訂資料模型，以利您的報表深入分析，並擴充內含豐富Platform資料的Real-Time CDP資料模型。 請參閱與資料Distiller SKU相關的[封裝](../../packaging.md)、[護欄](../../guardrails.md#query-accelerated-store)和[授權](../../data-distiller/license-usage.md)檔案。 如果您沒有Data Distiller SKU，請聯絡您的Adobe客戶服務代表以取得更多資訊。

## SQL深入分析使用案例 {#use-cases}

以下是透過Data Distiller中的SQL Insights可有效解決的常見使用案例。

### 設定檔與對象使用透明度 {#usage-transparency}

**挑戰：**&#x200B;如何依特定條件劃分關鍵績效指標(KPI)，例如業務單位、忠誠度狀態或客戶期限值(CLTV)。

**SQL Insights解決方案：** Data Distiller可擴充Adobe Experience Platform中的報表資料模型，協助您新增[自訂設定檔屬性，例如CLTV](../../use-cases/customer-lifetime-value.md)或忠誠度狀態。

### 同意異常追蹤 {#consent-anomaly-tracking}

**挑戰：**&#x200B;如何將對象重疊和大小趨勢線報告套用至電子郵件、簡訊和電話等管道的自訂同意屬性。

**SQL Insights解決方案：**&#x200B;報表資料模型可以延伸，以追蹤同意偏好設定在一段時間內的變更。 這涉及建立其他事實和維度資料表，以趨勢化同意偏好設定並排程[增量資料重新整理](../../key-concepts/incremental-load.md)。

### 最佳化對象細分策略 {#optimize-audience-segmentation-strategy}

**挑戰：**&#x200B;如何將機器學習(ML)模型產生的傾向分數整合到其對象KPI報表中。

**SQL深入分析解決方案：** Data Distiller允許包含自訂ML模型的[傾向分數](../../use-cases/propensity-score.md)，以方便在對象層級計算彙總分數。 然後可將此資料與標準KPI一起報告。

### 對象擴展 {#audience-expansion}

**挑戰：**&#x200B;如何在受眾重疊報表中取得個人資料計數以外的專案，並取得其他人口統計資料或偏好設定來指導受眾擴張策略。

**SQL Insights解決方案：**&#x200B;藉由擴充報表資料模型，使用者可以合併其他設定檔屬性，以相關人口統計資料和偏好設定豐富受眾重疊報表。

## 產生SQL Insights的主要功能 {#key-capabilities}

下圖著重說明產生SQL Insights的幾項基本功能。 這些功能包括：

1. **資料視覺效果：**&#x200B;結合趨勢和長條圖等視覺元素，以全面檢視資料趨勢。
1. **儀表板製作：**&#x200B;啟用建立根據特定使用案例量身打造的自訂儀表板，提供更個人化且目標更明確的分析體驗。
1. **彈性的SQL資料模型化：**&#x200B;使用通用的SQL資料模型化方法，讓使用者能夠順暢地結合併操控不同的資料集，增強適應性和分析深度。
1. **加速儲存：**&#x200B;實作加速儲存機制，以透過SQL有效率地提供彙總的深入分析，確保簡化並快速存取有價值的資訊。
1. **BI連線：**&#x200B;促進與熱門Business Intelligence(BI)工具(包括Power BI、Tableau、Looker和Apache Superset)的緊密整合。 此連線可確保與多種BI環境的相容性，讓使用者能夠靈活使用所選取的工具，進行深入分析和報告。

![資料Distiller SQL Insights主要功能的視覺化表示法。](../../images/data-distiller/sql-insights/key-capabilities-of-customizable-insights.png)

## 建立SQL深入分析的步驟 {#steps-to-create}

若要在資料Distiller中開發SQL深入分析控制面板，請遵循下列逐步指示。

1. **隨選查詢探索：**&#x200B;開始執行隨選`SELECT`查詢以探索資料湖上的原始資料。 這允許對實驗進行即時、探索性資料分析，並驗證未將查詢結果儲存在Data Lake中的資料。
1. **批次查詢使用率：**&#x200B;使用批次查詢來[建立排定的工作](../../api/scheduled-queries.md#create-a-new-scheduled-query)，以產生見解彙總表格，確保資料處理的系統化和自動化方法。 批次查詢執行`INSERT TABLE AS SELECT`和`CREATE TABLE AS SELECT`查詢以清理、塑形、操縱和擴充資料。 這些查詢的結果會儲存在Data Lake中。
1. **彙總見解載入：**&#x200B;將產生的彙總見解載入加速存放區，並使用SQL測試查詢，並確保資料擷取的正確性和效率。 若要瞭解如何[對加速存放區](../../api/accelerated-queries.md)進行無狀態查詢，請參閱檔案。
1. **存取與整合：**&#x200B;透過與Adobe Experience Platform [使用者定義儀表板](../../../dashboards/user-defined-dashboards.md)或其他偏好的Business Intelligence(BI)工具整合，可順暢地存取加速存放區中儲存的深入分析。 這些與協力廠商使用者端的整合讓使用者獲得有凝聚力的直覺式體驗。

![說明資料Distiller中SQL深入分析四個步驟的資訊圖表。](../../images/data-distiller/sql-insights/steps-to-customizable-insights.png)

## 後續步驟

閱讀本檔案後，您現在已能更妥善地瞭解使用案例、基本功能，以及使用Data Distiller開發SQL深入分析控制面板的必要步驟。 若要繼續瞭解如何建立自訂的報表資料模型，請參閱[報表見解資料模型指南](./reporting-insights-data-model.md)。
