---
keywords: Experience Platform;home;popular topics;query service；查詢服務；query
solution: Experience Platform
title: 查詢服務概述
topic-legacy: overview
description: 本文檔概述了查詢服務在Experience Platform中的角色。
exl-id: fdaefc12-a97d-4e4e-9aed-d3dbd0f43ea0
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '635'
ht-degree: 0%

---

# [!DNL Query Service] 概觀

Adobe Experience Platform收集來自各種來源的資料。 行銷人員面臨的一大挑戰是，要瞭解這些資料，以獲得客戶的深入資訊。 Adobe Experience Platform[!DNL Query Service]允許您使用標準SQL查詢[!DNL Platform]中的資料，從而方便了這一點。 使用[!DNL Query Service]，您可以在[!DNL Data Lake]中加入任何資料集，並將查詢結果擷取為新資料集，以用於報告、機器學習或擷取至[!DNL Real-time Customer Profile]。 本檔案概述[!DNL Experience Platform]中[!DNL Query Service]的角色。

[!DNL Query Service] 讓品牌能夠連接線上至線下的客戶歷程，並瞭解全通道歸因。以下視訊說明體驗企業如何運用[!DNL Query Service]解決關鍵使用案例，以及[!DNL Query Service]的運作方式。

>[!VIDEO](https://video.tv.adobe.com/v/29795?quality=12&learn=on)

## 使用[!DNL Query Service]

[!DNL Query Service] 提供了用戶介面和REST風格的API，您可以從中建立SQL查詢以更好地分析資料。使用使用者介面，您可以編寫和執行查詢、檢視先前執行的查詢，以及存取IMS組織內的使用者儲存的查詢。 使用者介面可當成沙盒，在更廣泛的資料集上執行查詢之前先測試查詢。 有關在[!DNL Platform]中使用互動式服務的更多資訊，請參見[查詢服務用戶介面指南](ui/overview.md)。 RESTful API提供類似的體驗，可讓您以程式設計方式編寫和執行查詢、排程查詢以供日後使用和重複，以及為想要編寫的查詢建立範本。 有關使用[!DNL Query Service] API的詳細資訊，請參閱[查詢服務開發人員指南](api/getting-started.md)。

## [!DNL Query Service] 和服 [!DNL Experience Platform] 務

[!DNL Query Service] 可與多個服務一起使 [!DNL Experience Platform] 用。為充份運用[!DNL Query Service's]功能，建議您熟悉這些服務，以及它們與[!DNL Query Service]的互動方式。

### [!DNL Data Science Workspace]

Adobe Experience Platform[!DNL Data Science Workspace]使用機器學習和人工智慧，從儲存在[!DNL Experience Platform]中的資料獲得見解。 [!DNL Data Science Workspace] 讓資料科學家根據客戶及其活動的記錄和時間序列資料來建立配方，以促進購買傾向等預測，並推薦個人可能喜歡和使用的優惠。通過將[!DNL Query Service]整合到[!DNL JupyterLab]中，可以在[!DNL Data Science Workspace]中使用SQL，從而允許您探索、轉換和分析Adobe Analytics資料。 請閱讀[!DNL Data Science Workspace]概觀以取得有關[!DNL Data Science Workspace]的詳細資訊，以及[!DNL Query Service]整合指南，以取得有關[!DNL Data Science Workspace]如何與[!DNL Query Service]互動的詳細資訊。

### [!DNL Segmentation Service]

Adobe Experience Platform[!DNL Segmentation Service]可讓使用者將客戶分成具有相似特徵的較小群組。 您隨後可評估這些區段，以便對[!DNL Real-time Customer Profile]資料提供更佳的分析。 [!DNL Query Service] 可用來透過在中執行此區段資料的查詢來提供此分析 [!DNL Data Lake]。請閱讀[!DNL Segmentation Service]概觀以取得區段的詳細資訊，以及[!DNL Profile Query Language](PQL)指南，以取得如何分析區段的詳細資訊。

### Looker BI使用案例

有了Adobe Experience Platform，您可以收集、儲存、構建和提取所有儲存的資料集— 包括行為、CRM和銷售點資料。 使用[!DNL Experience Platform's Query Service]，您可以查詢這些資料集並回答有關業務的特定問題，然後開始產生具影響力的見解。 以下視訊示範使用[!DNL Query Service]在商業智慧(BI)工具中建立控制面板的價值。

>[!VIDEO](https://video.tv.adobe.com/v/28981?quality=12&learn=on)

## 後續步驟和其他資源

閱讀本檔案後，您將瞭解[!DNL Query Service]以及它在[!DNL Experience Platform]的更大範圍內的運作方式。 有關與[!DNL Query Service] API中各種端點交互的詳細資訊，請閱讀[查詢服務開發人員指南](api/getting-started.md)。 有關在[!DNL Platform]中使用互動式服務的詳細資訊，請閱讀[查詢服務用戶介面指南](ui/overview.md)。 有關將外部客戶端與[!DNL Query Service]連接的完整清單，請閱讀[查詢服務客戶端概述](clients/overview.md)。

若要讓您做好執行查詢的準備，請觀看下列影片。 此視訊分享在查詢編輯器介面、PSQL用戶端、商業智慧(BI)解決方案和HTTP API中執行查詢的秘訣與最佳實務。

>[!VIDEO](https://video.tv.adobe.com/v/29811?quality=12&learn=on)
