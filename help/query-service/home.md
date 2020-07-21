---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Adobe Experience Platform查詢服務
topic: overview
translation-type: tm+mt
source-git-commit: 3b710e7a20975880376f7e434ea4d79c01fa0ce5
workflow-type: tm+mt
source-wordcount: '613'
ht-degree: 0%

---


# [!DNL Query Service]概述

Adobe Experience Platform會從多種來源擷取資料。 行銷人員面臨的一大挑戰是，要瞭解這些資料，以獲得客戶的深入資訊。 Adobe Experience Platform可 [!DNL Query Service] 讓您使用標準SQL在中查詢資料，為您提供便利 [!DNL Platform]。 使用 [!DNL Query Service]時，您可以在中加入任何資料集，並 [!DNL Data Lake] 將查詢結果擷取為新資料集，以用於報告、機器學習或擷取 [!DNL Real-time Customer Profile]。 本文檔概述了Within的 [!DNL Query Service] 角色 [!DNL Experience Platform]。

[!DNL Query Service] 讓品牌能夠連接線上至線下的客戶歷程，並瞭解全通道歸因。 以下視訊說明體驗企業如何運用 [!DNL Query Service] 來解決關鍵使用案例及運作方式 [!DNL Query Service] 。

>[!VIDEO](https://video.tv.adobe.com/v/29795?quality=12&learn=on)

## Using [!DNL Query Service]

[!DNL Query Service] 提供了用戶介面和REST風格的API，您可以從中建立SQL查詢以更好地分析資料。 使用使用者介面，您可以編寫和執行查詢、檢視先前執行的查詢，以及存取IMS組織內的使用者儲存的查詢。 使用者介面可當成沙盒，在更廣泛的資料集上執行查詢之前先測試查詢。 有關在中使用互動式服務的詳 [!DNL Platform] 細資訊，請參閱查 [詢服務用戶介面指南](ui/overview.md)。 RESTful API提供類似的體驗，可讓您以程式設計方式編寫和執行查詢、排程查詢以供日後使用和重複，以及為想要編寫的查詢建立範本。 有關使用 [!DNL Query Service] API的詳細資訊，請參閱查詢服 [務開發人員指南](api/getting-started.md)。

## [!DNL Query Service] 和服 [!DNL Experience Platform] 務

[!DNL Query Service] 可與多個服務一起使 [!DNL Experience Platform] 用。 為了充份運用這些功 [!DNL Query Service's] 能，建議您熟悉這些服務及其互動方式 [!DNL Query Service]。

### [!DNL Data Science Workspace]

Adobe Experience Platform使用 [!DNL Data Science Workspace] 機器學習和人工智慧，從儲存在內部的資料獲得見解 [!DNL Experience Platform]。 [!DNL Data Science Workspace] 讓資料科學家根據客戶及其活動的記錄和時間序列資料來建立配方，以促進購買傾向等預測，並推薦個人可能喜歡和使用的優惠。 您可在中使用SQL [!DNL Data Science Workspace] ，方 [!DNL Query Service] 式 [!DNL JupyterLab]是整合至中，讓您探索、轉換和分析Adobe Analytics資料。 請閱讀概 [!DNL Data Science Workspace] 述以取得更多相關資訊， [!DNL Data Science Workspace]以及整合指南 [!DNL Query Service] ，以取得如何與之互動的 [!DNL Data Science Workspace] 詳細資訊 [!DNL Query Service]。

### [!DNL Segmentation Service]

Adobe Experience Platform可 [!DNL Segmentation Service] 讓使用者將客戶分成具有類似特徵的較小群組。 您隨後可評估這些區段，以便對您的資料提供更好的 [!DNL Real-time Customer Profile] 分析。 [!DNL Query Service] 可用來透過在中執行此區段資料的查詢來提供此分析 [!DNL Data Lake]。 請閱讀總 [!DNL Segmentation Service] 覽以取得區段的詳細資訊，以及 [!DNL Profile Query Language] (PQL)指南，以取得如何分析區段的詳細資訊。

### Looker BI使用案例

有了Adobe Experience Platform，您就可以收錄、儲存、建構及提取所有儲存的資料集— 包括行為、CRM和銷售點資料。 使用 [!DNL Experience Platform's Query Service]時，您可以查詢這些資料集並回答有關業務的特定問題，然後開始產生具影響力的見解。 以下視訊示範在商業智慧(BI)工具中使用建立控制面板的價值 [!DNL Query Service]。

>[!VIDEO](https://video.tv.adobe.com/v/28981?quality=12&learn=on)

## 後續步驟和其他資源

閱讀本檔案，您將瞭解它在更廣 [!DNL Query Service] 泛範圍內的運作方式及運作方式 [!DNL Experience Platform]。 如需有關在 [!DNL Query Service] API中與各種端點互動的詳細資訊，請閱讀查詢服 [務開發人員指南](api/getting-started.md)。 有關在中使用互動式服務的詳細 [!DNL Platform]資訊，請閱 [讀查詢服務使用者介面指南](ui/overview.md)。 有關連接外部客戶機的完整清單，請 [!DNL Query Service]閱讀查詢服務 [客戶機概述](clients/overview.md)。

若要讓您做好執行查詢的準備，請觀看下列影片。 此視訊分享在查詢編輯器介面、PSQL用戶端、商業智慧(BI)解決方案和HTTP API中執行查詢的秘訣與最佳實務。

>[!VIDEO](https://video.tv.adobe.com/v/29811?quality=12&learn=on)
