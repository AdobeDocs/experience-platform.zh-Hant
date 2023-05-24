---
keywords: Experience Platform；首頁；熱門主題；查詢服務；查詢服務；查詢服務；查詢
solution: Experience Platform
title: 查詢服務總覽
description: 此文檔概述了Experience Platform中查詢服務的角色。
exl-id: fdaefc12-a97d-4e4e-9aed-d3dbd0f43ea0
source-git-commit: fcd44aef026c1049ccdfe5896e6199d32b4d1114
workflow-type: tm+mt
source-wordcount: '721'
ht-degree: 0%

---

# [!DNL Query Service] 概覽

Adobe Experience Platform從各種來源收集資料。 營銷人員面臨的一個主要挑戰是，如何理解這些資料，以便瞭解客戶的真知灼見。 Adobe Experience Platform [!DNL Query Service] 通過允許您使用標準SQL在 [!DNL Platform]。 使用 [!DNL Query Service]，可以加入任何資料集 [!DNL Data Lake] 並將查詢結果捕獲為新資料集，用於報告、機器學習或接收到 [!DNL Real-Time Customer Profile]。 本文檔概述了 [!DNL Query Service] 內 [!DNL Experience Platform]。

[!DNL Query Service] 使品牌能夠將線上到線下的顧客之旅聯繫起來，並瞭解全方位渠道的歸屬。 以下視頻顯示了體驗企業如何利用 [!DNL Query Service] 解決關鍵使用案例以及如何 [!DNL Query Service] 工作。

>[!VIDEO](https://video.tv.adobe.com/v/29795?quality=12&learn=on)

## 使用 [!DNL Query Service]

[!DNL Query Service] 提供了用戶介面和REST風格的API，您可以從中建立SQL查詢以更好地分析資料。 使用用戶介面，您可以編寫和執行查詢、查看以前執行的查詢以及訪問組織中用戶保存的查詢。 用戶介面將用作沙箱，用於在更寬的資料集上執行查詢之前test查詢。 有關在中使用互動式服務的詳細資訊 [!DNL Platform] 在 [查詢服務用戶介面指南](ui/overview.md)。 REST風格的API提供了類似的體驗，允許您以寫程式方式編寫和執行查詢、計畫查詢以供將來使用和重複，以及為要編寫的查詢建立模板。 有關使用 [!DNL Query Service] 可在 [查詢服務開發人員指南](api/getting-started.md)。

## [!DNL Query Service] 和 [!DNL Experience Platform] 服務

[!DNL Query Service] 可與多個設備交互，並可與多個設備結合使用 [!DNL Experience Platform] 服務。 為了讓 [!DNL Query Service's] 功能，建議您熟悉這些服務及其與 [!DNL Query Service]。

### [!DNL Data Science Workspace]

Adobe Experience Platform [!DNL Data Science Workspace] 使用機器學習和人工智慧從儲存在 [!DNL Experience Platform]。 [!DNL Data Science Workspace] 使資料科學家能夠根據記錄和有關客戶及其活動的時間序列資料來構建配方，從而促進購買傾向和個人可能喜歡和使用的推薦產品等預測。 可在 [!DNL Data Science Workspace] 通過 [!DNL Query Service] 入 [!DNL JupyterLab]允許您瀏覽、轉換和分析Adobe Analytics資料。 請閱讀 [!DNL Data Science Workspace] 概述有關 [!DNL Data Science Workspace]的 [!DNL Query Service] 整合指南，瞭解有關如何 [!DNL Data Science Workspace] 交互 [!DNL Query Service]。

### [!DNL Segmentation Service]

Adobe Experience Platform [!DNL Segmentation Service] 允許用戶將客戶分成具有相似特徵的小組。 隨後可以評估這些段，以便對 [!DNL Real-Time Customer Profile] 資料。 [!DNL Query Service] 可通過運行此段資料中的查詢來提供此分析 [!DNL Data Lake]。 請閱讀 [!DNL Segmentation Service] 概述，瞭解有關分段的詳細資訊，以及 [!DNL Profile Query Language] (PQL)指南，瞭解有關如何分析段的詳細資訊。

## 使用案例

[!DNL Query Service] 為您的資料處理提供了靈活的方法，可滿足多種目的。 除其他外，它可減輕營銷人員細分的負擔，並幫助產生可操作的受眾和有意義的商業洞見。 以下使用案例提供了更深入的示例，說明 [!DNL Query Service]。

### Adobe Analytics瀏覽放棄

此 [瀏覽放棄示例以使用Adobe [!DNL Analytics]](./use-cases/abandoned-browse.md) 建立特定可操作受眾的資料。 [!DNL Query Service] 適應複雜的分段邏輯，以計算各種個性化屬性以便下游使用，或大大簡化您構建段的方式。

### 查找器BI儀表板

使用Adobe Experience Platform，您可以攝取、儲存、構建和拉取所有儲存的資料集 — 包括行為、 CRM和銷售點資料。 使用 [!DNL Experience Platform's Query Service]，您可以在這些資料集上查詢並回答有關業務的特定問題，然後開始產生影響性的見解。 以下視頻演示了在業務智慧(BI)工具中使用 [!DNL Query Service]。

>[!VIDEO](https://video.tv.adobe.com/v/28981?quality=12&learn=on)

## 後續步驟和其他資源

通過閱讀此文檔，您已 [!DNL Query Service] 以及它在更大範圍內的作用 [!DNL Experience Platform]。 有關與&lt;客戶名稱>內各端點交互的詳細資訊 [!DNL Query Service] API，請閱讀 [查詢服務開發人員指南](api/getting-started.md)。 有關在中使用互動式服務的詳細資訊 [!DNL Platform]，請閱讀 [查詢服務用戶介面指南](ui/overview.md)。 有關將外部客戶端與 [!DNL Query Service]，請閱讀 [查詢服務客戶端概述](clients/overview.md)。

要更好地準備運行查詢，請觀看以下視頻。 此視頻共用在查詢編輯器介面、PSQL客戶端、業務智慧(BI)解決方案和HTTP API中運行查詢的提示和最佳做法。

>[!VIDEO](https://video.tv.adobe.com/v/29811?quality=12&learn=on)
