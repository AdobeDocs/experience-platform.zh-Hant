---
keywords: Experience Platform；首頁；熱門主題；查詢服務；查詢服務；查詢
solution: Experience Platform
title: 查詢服務總覽
description: 瞭解Experience Platform中查詢服務的角色。
exl-id: fdaefc12-a97d-4e4e-9aed-d3dbd0f43ea0
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '861'
ht-degree: 0%

---

# 查詢服務總覽

Adobe Experience Platform會擷取各種來源的資料。 行銷人員的主要挑戰是瞭解這些資料，以深入瞭解其客戶。 若要在Experience Platform中查詢資料，您可以使用標準SQL和Adobe Experience Platform查詢服務。 您可以使用查詢服務來聯結資料湖中的任何資料集，並將查詢結果擷取為新資料集，以用於報表、機器學習或內嵌至[!DNL Real-Time Customer Profile]。 本文概述了Experience Platform中查詢服務的角色。

您可以使用查詢服務來連線線上到離線客戶歷程，並瞭解您品牌的全頻道歸因。 以下影片說明體驗企業如何使用查詢服務來處理主要使用案例，以及查詢服務的運作方式。

>[!VIDEO](https://video.tv.adobe.com/v/29795?quality=12&learn=on)

## 使用查詢服務 {#usage}

若要分析資料，請使用Query Service使用者介面或RESTful API建立並執行SQL查詢。
使用Query Service UI，您可以撰寫、執行和排程查詢、檢視以前執行的查詢，以及存取組織內使用者儲存的查詢。 您也可以先測試查詢，再使用查詢編輯器在更廣泛的資料集上執行查詢。 請參閱[查詢服務UI指南](ui/overview.md)，瞭解UI功能的概觀。

RESTful API提供類似的體驗。 您可以使用查詢服務API以程式設計方式寫入和執行查詢、建立並儲存您要調整的查詢範本，或排程查詢以自動執行。 請參閱[Query Service開發人員指南](api/getting-started.md)，以取得使用Query Service API的詳細資訊。

若要快速開始使用查詢服務功能，建議您閱讀以下檔案：

- [查詢執行的一般指引](./best-practices/writing-queries.md)
- [查詢服務中的SQL語法](./sql/syntax.md)
- [使用SQL建立衍生資料集](./data-distiller/derived-datasets/create-derived-datasets-with-sql.md)

## 查詢服務與Experience Platform服務 {#experience-platform-services}

查詢服務會互動，並可與多個Experience Platform服務搭配使用。 若要充分利用Query Service的功能，您應該熟悉這些服務以及它們如何與Query Service互動。 [Experience Platform檔案登陸頁面](https://experienceleague.adobe.com/docs/experience-platform.html?lang=zh-Hant)提供平台的功能摘要和連結。

### [!DNL Data Science Workspace] {#data-science-workspace}

Adobe Experience Platform [!DNL Data Science Workspace]使用機器學習和人工智慧，從Experience Platform中儲存的資料取得深入分析。 資料科學家可以使用[!DNL Data Science Workspace]，根據有關客戶及其活動的記錄和時間序列資料來建置配方。 這些配方有助於進行預測，例如購買傾向和建議個人可能會讚賞和使用的選件。 您可以在[!DNL Data Science Workspace]內使用SQL，方法是將查詢服務整合至[!DNL JupyterLab]以探索、轉換及分析Adobe Analytics資料。 閱讀[[!DNL Data Science Workspace] 總覽](../data-science-workspace/home.md)和[Jupyter Notebook連線指南](./clients/jupyter-notebook.md)，瞭解[!DNL Data Science Workspace]如何與查詢服務互動的詳細資訊。

### [!DNL Segmentation Service] {#segmentation}

使用Adobe Experience Platform分段服務，將客戶劃分為具有類似特徵的較小群組。 接著，您就可以評估這些對象，針對即時客戶設定檔資料提供更佳的分析。 您可以使用查詢服務在資料湖中對此對象資料執行查詢並提供分析。 如需如何分析對象的詳細資訊，請參閱[分段服務總覽](../segmentation/home.md)和[[!DNL Profile Query Language] (PQL)指南](../segmentation/pql/overview.md)。

## 使用案例 {#use-cases}

查詢服務提供彈性的資料處理方式，有許多用途。 除了其他以外，這可減輕行銷人員劃分割槽段的負擔，並有助於產生可操作的受眾和有意義的業務深入分析。 下列使用案例提供更深入的查詢服務功能範例。

### Adobe Analytics瀏覽放棄 {#abandon-browse}

此[瀏覽放棄範例的中心為使用Adobe [!DNL Analytics]](./use-cases/abandoned-browse.md)資料來建立特定可操作的對象。 查詢服務採用複雜的分段邏輯，可計算各種個人化屬性以用於下游，或大幅簡化您建立受眾的方式。

## 使用自訂儀表板產生深入分析 {#custom-dashboards}

有了Adobe Experience Platform，您可以內嵌、儲存、建構及提取所有儲存的資料集，包括行為、CRM和銷售點資料。 使用[!DNL Experience Platform's Query Service]，您可以查詢這些資料集並回答有關業務的特定問題，然後開始產生有影響力的深入分析。 瞭解如何建立及管理自訂儀表板，您可於其中建立、新增及編輯自訂的Widget，以視覺化方式使用[使用者定義儀表板](../dashboards/standard-dashboards.md)的關鍵量度。 您甚至可以[搭配使用SQL查詢與Real-Time CDP見解資料模型，針對您的行銷和KPI使用案例自訂您自己的Real-Time Customer Data Platform報告](../dashboards/data-models/cdp-insights-data-model-b2c.md)。

## 後續步驟和其他資源

閱讀本檔案後，您將瞭解查詢服務及其在Experience Platform廣大範圍內的運作方式。 若要繼續瞭解查詢服務功能，建議您閱讀下列檔案：

- [Query Service開發人員指南](api/getting-started.md)：如需與Query Service API內各種端點互動的詳細資訊。
- [查詢服務使用者介面指南](ui/overview.md)：有關使用查詢編輯器和UI的詳細資訊。
- [查詢服務使用者端總覽](clients/overview.md)：如需與查詢服務連線的外部使用者端完整清單。

為了更能準備好執行查詢，請觀看以下影片。 此影片分享在查詢編輯器介面、PSQL使用者端、商業智慧(BI)解決方案和HTTP API中執行查詢的秘訣和最佳實務。

>[!VIDEO](https://video.tv.adobe.com/v/29811?quality=12&learn=on)
