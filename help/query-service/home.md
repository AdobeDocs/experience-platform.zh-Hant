---
keywords: Experience Platform；首頁；熱門主題；查詢服務；查詢
solution: Experience Platform
title: 查詢服務總覽
description: 本文檔概述了Query Service在Experience Platform中的角色。
exl-id: fdaefc12-a97d-4e4e-9aed-d3dbd0f43ea0
source-git-commit: 58eadaaf461ecd9598f3f508fab0c192cf058916
workflow-type: tm+mt
source-wordcount: '722'
ht-degree: 0%

---

# [!DNL Query Service] 概覽

Adobe Experience Platform會從多種來源擷取資料。 行銷人員面臨的主要挑戰是要了解這些資料，以便深入了解其客戶。 Adobe Experience Platform [!DNL Query Service] 通過允許您使用標準SQL在中查詢資料，便於了 [!DNL Platform]. 使用 [!DNL Query Service]，您可以加入 [!DNL Data Lake] 並將查詢結果擷取為新資料集，以用於報表、機器學習或擷取至 [!DNL Real-Time Customer Profile]. 本檔案概述 [!DNL Query Service] with [!DNL Experience Platform].

[!DNL Query Service] 讓品牌能夠連線線上至離線客戶歷程並了解全管道歸因。 以下影片說明體驗業務如何運用 [!DNL Query Service] 解決關鍵使用案例及方式 [!DNL Query Service] 工作。

>[!VIDEO](https://video.tv.adobe.com/v/29795?quality=12&learn=on)

## 使用 [!DNL Query Service]

[!DNL Query Service] 提供了用戶介面和RESTful API，您可以從中建立SQL查詢，以便更好地分析資料。 透過使用者介面，您可以撰寫及執行查詢、檢視先前執行的查詢，以及存取由您IMS組織內的使用者儲存的查詢。 使用者介面可作為沙箱，在更廣泛的資料集上執行查詢前先測試查詢。 有關在中使用互動式服務的詳細資訊 [!DNL Platform] 可在 [查詢服務使用者介面指南](ui/overview.md). RESTful API提供類似的體驗，可讓您以程式設計方式撰寫和執行查詢、排程查詢以供日後使用和重複，以及為您想要撰寫的查詢建立範本。 有關使用 [!DNL Query Service] 您可以在 [Query Service開發人員指南](api/getting-started.md).

## [!DNL Query Service] 和 [!DNL Experience Platform] 服務

[!DNL Query Service] 可與多個 [!DNL Experience Platform] 服務。 為了充分利用 [!DNL Query Service's] 功能，建議您熟悉這些服務，以及它們與 [!DNL Query Service].

### [!DNL Data Science Workspace]

Adobe Experience Platform [!DNL Data Science Workspace] 使用機器學習和人工智慧，從儲存於 [!DNL Experience Platform]. [!DNL Data Science Workspace] 可讓資料科學家根據關於客戶及其活動的記錄和時間序列資料來建立配方，以促進購買傾向等預測，以及個人可能欣賞和使用的建議選件。 您可以在 [!DNL Data Science Workspace] 整合 [!DNL Query Service] into [!DNL JupyterLab]，可讓您探索、轉換和分析Adobe Analytics資料。 請閱讀 [!DNL Data Science Workspace] 概覽，以取得 [!DNL Data Science Workspace]，和 [!DNL Query Service] 整合指南，以了解如何 [!DNL Data Science Workspace] 與 [!DNL Query Service].

### [!DNL Segmentation Service]

Adobe Experience Platform [!DNL Segmentation Service] 可讓使用者將其客戶分割為具有類似特徵的較小群組。 之後可評估這些區段，以針對您的 [!DNL Real-Time Customer Profile] 資料。 [!DNL Query Service] 可透過在中對此區段資料執行查詢來提供此分析 [!DNL Data Lake]. 請閱讀 [!DNL Segmentation Service] 概述，以取得分段的詳細資訊，以及 [!DNL Profile Query Language] (PQL)指南，以取得如何分析區段的詳細資訊。

## 使用案例

[!DNL Query Service] 為您的資料處理提供彈性的方法，有多種用途。 其中之一，它可減輕行銷人員的細分負擔，並協助產生可操作的對象和有意義的業務分析。 下列使用案例提供更深入的範例，說明 [!DNL Query Service].

### Adobe Analytics瀏覽放棄

此 [瀏覽放棄範例以使用為中心Adobe [!DNL Analytics]](./use-cases/abandoned-browse.md) 資料，以建立特定可操作的對象。 [!DNL Query Service] 因應複雜的分段邏輯，可計算供下游使用的各種個人化屬性，或大幅簡化區段建立的方式。

### Looker BI控制面板

透過Adobe Experience Platform，您可以擷取、儲存、結構及提取所有儲存的資料集，包括行為、CRM和銷售點資料。 使用 [!DNL Experience Platform's Query Service]，您可以查詢這些資料集並回答有關業務的特定問題，然後開始產生具影響力的深入分析。 以下影片示範如何使用在商業智慧(BI)工具中建立控制面板的價值 [!DNL Query Service].

>[!VIDEO](https://video.tv.adobe.com/v/28981?quality=12&learn=on)

## 後續步驟和其他資源

閱讀本檔案，您便了解 [!DNL Query Service] 以及它在 [!DNL Experience Platform]. 如需與 [!DNL Query Service] API，請閱讀 [Query Service開發人員指南](api/getting-started.md). 有關在中使用互動式服務的詳細資訊 [!DNL Platform]，請閱讀 [查詢服務使用者介面指南](ui/overview.md). 有關連接外部客戶端與 [!DNL Query Service]，請閱讀 [查詢服務客戶端概述](clients/overview.md).

要更好地準備運行查詢，請觀看以下視頻。 此影片分享在查詢編輯器介面、PSQL用戶端、商業智慧(BI)解決方案和HTTP API中執行查詢的秘訣和最佳作法。

>[!VIDEO](https://video.tv.adobe.com/v/29811?quality=12&learn=on)
