---
title: 功能工程SQL擴充功能
description: 瞭解資料Distiller功能工程SQL擴充功能，以預先處理資料以供進階統計模型使用。 它涵蓋了可用的特徵擷取、轉換和選取技術。
role: Developer
source-git-commit: 1fcfb5c41750e853daaf036ceaae3527b805391c
workflow-type: tm+mt
source-wordcount: '717'
ht-degree: 1%

---

# 功能工程SQL擴充功能

>[!AVAILABILITY]
>
>已購買Data Distiller附加元件的客戶可使用此功能。 如需詳細資訊，請聯絡您的 Adobe 代表。

為了滿足您的功能工程需求，請使用SQL Transformer擴充功能來簡化和自動化資料前置處理。 使用此擴充功能來建立功能，並享受不同功能工程技術的無縫實驗，包括將它們與模型建立關聯。 專為分散式運算而設計，您可以平行且可擴充的方式執行大型資料集的功能工程，大幅減少使用Data Distiller功能工程SQL擴充功能進行資料前置處理所需的時間。

## 技術概覽 {#technique-overview}

特徵工程功能涵蓋三個主要領域：特徵擷取、特徵轉換和特徵選取。 每個區域都包含特定功能，專門用於擷取、轉換、聚焦及改善資料前置處理。

### 功能擷取 {#feature-extraction}

從您的資料中擷取相關資訊（尤其是文字資料），並將其轉換為支援的模型可加以使用或轉換並衍生資料集的數字格式。 使用下列函式來執行特徵擷取：

- **[文字轉換器](./feature-transformation.md#textual-transformations)**：將文字資料轉換為數值功能。
- **[計數向量器](./feature-transformation.md#countvectorizer)**：將文字檔案的集合轉換為權杖計數的向量。
- **[N格](./feature-transformation.md#ngram)**：從文字資料產生n格序列。
- **[停用字詞移除程式](./feature-transformation.md#stopwordsremover)**：篩選掉沒有重要意義的一般字詞。
- **[TF-IDF](./feature-transformation.md#tf-idf)**：測量檔案中字詞相對於語料庫的重要性。
- **[Tokenizer](./feature-transformation.md#tokenizer)**：將文字劃分為個別字詞（單字）。
- **[Word2Vec](./feature-transformation.md#word2vec)**：將文字對應至固定大小的向量，並建立文字內嵌。

### 特徵轉換 {#feature-transformation}

除了擷取特徵之外，請使用下列一般轉換器為進階統計模型和衍生資料集準備特徵。 套用縮放、正規化或編碼，以確保您的功能具有相同的比例並具有類似的分佈。

#### 一般轉換器

以下是處理各種資料型別的工具清單，以增強您的資料前置處理工作流程。

- **[數值輸入器](./feature-transformation.md#numeric-imputer)**：將數值欄中缺少的值填入
- **[字串輸入器](./feature-transformation.md#string-imputer)**：將遺漏的字串值取代為指定的值
- **[向量組合器](./feature-transformation.md#vector-assembler)**：將多個資料行合併為單一向量資料行。

#### 數值轉換器

應用這些技巧來有效地處理和縮放數值資料，以改善模型效能。

- **[二進位化程式](./feature-transformation.md#binarizer)**：根據臨界值將連續功能轉換為二進位值。
- **[分段器](./feature-transformation.md#bucketizer)**：將連續功能對應到獨立的分段。
- **[最小 — 最大縮放器](./feature-transformation.md#minmaxscaler)**：將功能重新縮放到指定的範圍，通常是[0、1]。
- **[最大Abs縮放器](./feature-transformation.md#maxabsscaler)**：將功能重新縮放到範圍[-1、1]，而不變更稀疏度。
- **[標準化程式](./feature-transformation.md#normalizer)**：標準化向量以擁有單位標準。
- **[Quantile Discretizer](./feature-transformation.md#quantilediscretizer)**：將連續特徵轉換為分類特徵，將其轉換為數量位數。
- **[標準縮放器](./feature-transformation.md#standardscaler)**：將功能標準化為具有單位標準差和/或零平均值。

#### 類別轉換器

使用這些轉換器將分類資料轉換並編碼為適合機器學習模型的格式。

- **[字串索引器](./feature-transformation.md#stringindexer)**：將類別字串資料轉換成數值索引。
- **[一個Hot Encoder](./feature-transformation.md#onehotencoder)**：將分類資料對應至二進位向量。

### 功能選取 {#feature-selection}

接下來，著重從原始集合中選取最重要特徵的子集。 此程式有助於降低資料的維度，讓您的模型更易於處理並改善整體模型效能。

<!-- Commented out as it 
## Supported machine learning algorithms {#supported-ml-algorithms}

Once you have preprocessed your data, use the feature engineering SQL extension to prepare your data for the following machine learning algorithms:

### Classification and regression {#classification-regression}

Use logical regression to predict categorical outcomes and linear regression to predict continuous values.

- **Logical Regression**: Use this for binary classification tasks.
- **Linear Regression**: Apply this algorithm for predicting continuous values.

### Clustering {#clustering}

Use a clustering algorithm to group data points into distinct clusters based on their similarities.

- **[`K-Means`](./feature-transformation.md#kmeans)**: Use `K-Means` for unsupervised learning tasks to partition data into a specified number of clusters, with each data point assigned to the cluster with the nearest mean. -->

## 實作OPTIONS子句 {#options-clause}

定義模型時，請使用`OPTIONS`子句指定演演算法及其引數。 首先，設定`type`引數以指出您正在使用的演演算法，例如`K-Means`。 然後，將`OPTIONS`子句中的相關引數定義為機碼值組，以微調您的模型。 瞭解有些引數可能是位置引數，如果提供自訂值，則需要指定所有先前的引數。 如果您選擇不自訂某些引數，系統會套用預設設定。 請參閱相關檔案，以瞭解每個引數的函式和預設值。

### 後續步驟

瞭解本檔案中概述的功能工程技術後，請繼續進行[模型](./models.md)檔案。 它會引導您使用您設計的功能，完成建立、訓練和管理可信賴模型的程式。 建立模型後，請繼續進行[實作進階統計模型檔案。](./implement-models/implement-models.md)。本檔案可做為概觀，連結至不同模型技術（包括叢集、分類和回歸）的深入指南。 透過遵循這些檔案，您可以瞭解如何在SQL工作流程中設定和實施各種信任的模型，並最佳化模型以進行進階資料分析。
