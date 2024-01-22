---
keywords: Experience Platform；首頁；熱門主題；查詢服務；查詢服務；查詢
solution: Experience Platform
title: 查詢服務總覽
description: 瞭解Experience Platform中查詢服務的角色。
exl-id: fdaefc12-a97d-4e4e-9aed-d3dbd0f43ea0
source-git-commit: ad1827284b7070f73421d10c49e1e86e282839eb
workflow-type: tm+mt
source-wordcount: '837'
ht-degree: 0%

---

# 查詢服務總覽

Adobe Experience Platform會擷取各種來源的資料。 行銷人員的主要挑戰是瞭解這些資料，以深入瞭解其客戶。 若要在Platform中查詢資料，您可以使用標準SQL和Adobe Experience Platform查詢服務。 您可以使用查詢服務來聯結資料湖中的任何資料集，並將查詢結果擷取為新資料集，以用於報表、機器學習或內嵌至 [!DNL Real-Time Customer Profile]. 本文概述了Experience Platform中查詢服務的角色。

您可以使用查詢服務來連線線上到離線客戶歷程，並瞭解您品牌的全頻道歸因。 以下影片說明體驗企業如何使用查詢服務來處理主要使用案例，以及查詢服務的運作方式。

>[!VIDEO](https://video.tv.adobe.com/v/29795?quality=12&learn=on)

## 使用查詢服務 {#usage}

若要分析資料，您可以使用查詢服務使用者介面和RESTful API，從中建立SQL查詢。 透過使用者介面，您可以編寫和執行查詢、檢視以前執行的查詢，以及存取由您組織內的使用者儲存的查詢。 您可以使用查詢編輯器（如沙箱），在將查詢執行到更廣的資料集之前先測試查詢。 請參閱 [查詢服務使用者介面指南](ui/overview.md) 以取得關於使用UI的詳細資訊。 RESTful API提供類似的體驗。 您可以使用查詢服務API以程式設計方式寫入和執行查詢、排程查詢以供未來使用和重複，以及建立您要寫入的查詢範本。 有關使用查詢服務API的更多資訊，請參閱 [Query Service開發人員指南](api/getting-started.md).

## 查詢服務和Experience Platform服務 {#experience-platform-services}

查詢服務會互動，並可與多個Experience Platform服務搭配使用。 若要充分利用Query Service的功能，您應該熟悉這些服務以及它們如何與Query Service互動。 此 [Experience Platform檔案登陸頁面](https://experienceleague.adobe.com/docs/experience-platform.html) 提供平台功能的摘要和連結。

### [!DNL Data Science Workspace] {#data-science-workspace}

Adobe Experience Platform [!DNL Data Science Workspace] 使用機器學習和人工智慧，從Experience Platform中儲存的資料獲得見解。 資料科學家可以使用 [!DNL Data Science Workspace] 根據有關客戶及其活動的記錄和時間序列資料來建立配方。 這些配方有助於進行預測，例如購買傾向和建議個人可能會讚賞和使用的選件。 您可以在以下位置使用SQL： [!DNL Data Science Workspace] 將查詢服務整合至 [!DNL JupyterLab] 探索、轉換及分析Adobe Analytics資料。 閱讀 [[!DNL Data Science Workspace] 概述](../data-science-workspace/home.md) 和 [Jupyter Notebook連線指南](./clients/jupyter-notebook.md) 如需如何操作的詳細資訊 [!DNL Data Science Workspace] 會與查詢服務互動。

### [!DNL Segmentation Service] {#segmentation}

使用Adobe Experience Platform分段服務，將客戶劃分為具有類似特徵的較小群組。 接著，您就可以評估這些對象，針對即時客戶設定檔資料提供更佳的分析。 您可以使用查詢服務在資料湖中對此對象資料執行查詢並提供分析。 閱讀 [Segmentation Service概述](../segmentation/home.md) 和 [[!DNL Profile Query Language] (PQL)指南](../segmentation/pql/overview.md) 以取得如何分析對象的詳細資訊。

## 使用案例 {#use-cases}

查詢服務提供彈性的資料處理方式，有許多用途。 除了其他以外，這可減輕行銷人員劃分割槽段的負擔，並有助於產生可操作的受眾和有意義的業務深入分析。 下列使用案例提供更深入的查詢服務功能範例。

### Adobe Analytics瀏覽放棄 {#abandon-browse}

這個 [瀏覽放棄範例的中心為使用Adobe [!DNL Analytics]](./use-cases/abandoned-browse.md) 建立可採取行動的特定受眾的資料。 查詢服務採用複雜的分段邏輯，可計算各種個人化屬性以用於下游，或大幅簡化您建立受眾的方式。

## 使用自訂儀表板產生深入分析 {#custom-dashboards}

有了Adobe Experience Platform，您可以內嵌、儲存、建構及提取所有儲存的資料集，包括行為、CRM和銷售點資料。 使用 [!DNL Experience Platform's Query Service]後，您就可以查詢這些資料集，並回答有關業務的特定問題，然後開始產生具影響力的深入分析。 瞭解如何建立及管理自訂儀表板，以便在其中建立、新增和編輯客製化介面工具集，以視覺化方式呈現關鍵量度 [使用者定義儀表板](../dashboards/user-defined-dashboards.md). 您甚至可以 [自訂您自己的Real-Time CDP報表](../dashboards/cdp-insights-data-model.md) SQL查詢搭配Real-time Customer Data Platform前瞻分析資料模型用於行銷和KPI使用案例。

## 後續步驟和其他資源

閱讀本檔案後，您將瞭解查詢服務及其在更大Experience Platform範圍內的運作方式。 若要繼續瞭解查詢服務功能，建議您閱讀下列檔案：

- 此 [Query Service開發人員指南](api/getting-started.md)：如需與查詢服務API內的各種端點互動的詳細資訊。
- 此 [查詢服務使用者介面指南](ui/overview.md)：如需使用查詢編輯器和UI的詳細資訊。
- 此 [查詢服務使用者端總覽](clients/overview.md)：如需與查詢服務連線的外部使用者端完整清單。

為了更能準備好執行查詢，請觀看以下影片。 此影片分享在查詢編輯器介面、PSQL使用者端、商業智慧(BI)解決方案和HTTP API中執行查詢的秘訣和最佳實務。

>[!VIDEO](https://video.tv.adobe.com/v/29811?quality=12&learn=on)
