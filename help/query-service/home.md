---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Adobe Experience Platform查詢服務
topic: overview
translation-type: tm+mt
source-git-commit: 45da024d45b5eebdfc393ee14890e24aed6021ce

---


# 查詢服務概述

Adobe Experience Platform會從多種來源擷取資料。 行銷人員面臨的一大挑戰是，要瞭解這些資料，以獲得客戶的深入資訊。 Adobe Experience Platform Query Service可讓您使用標準SQL在Platform中查詢資料，以方便您做到。 使用查詢服務，您可以加入資料湖中的任何資料集，並將查詢結果擷取為新資料集，以用於報告、機器學習或擷取至即時客戶個人檔案。 本檔案概述Experience Platform中查詢服務的角色。

## 使用查詢服務

Query Service提供使用者介面和REST風格的API，您可從中建立SQL查詢，以更好地分析資料。 使用使用者介面，您可以編寫和執行查詢、檢視先前執行的查詢，以及存取IMS組織內的使用者儲存的查詢。 使用者介面可當成沙盒，在更廣泛的資料集上執行查詢之前先測試查詢。 有關在平台中使用互動式服務的詳細資訊，請參閱查詢服務使 [用者介面指南](ui/overview.md)。 RESTful API提供類似的體驗，可讓您以程式設計方式編寫和執行查詢、排程查詢以供日後使用和重複，以及為想要編寫的查詢建立範本。 有關使用查詢服務API的詳細資訊，請參閱查詢服務開 [發人員指南](api/getting-started.md)。

## 查詢服務與體驗平台服務

查詢服務可與多個Experience Platform服務互動，並可搭配使用。 為了充分利用查詢服務的功能，建議您熟悉這些服務以及它們與查詢服務的交互方式。

### 資料科學工作區

Adobe Experience Platform Data Science Workspace使用機器學習和人工智慧，從Experience Platform中儲存的資料獲取見解。 Data Science Workspace讓資料科學家能夠根據客戶及其活動的記錄和時間序列資料來建立配方，以促進購買傾向和推薦個人可能喜歡和使用的優惠等預測。 您可以在Data Science Workspace中使用SQL，方法是將查詢服務整合到JupyterLab中，讓您探索、轉換和分析Adobe Analytics資料。 請閱讀Data Science Workspace概觀，以取得有關Data Science Workspace的詳細資訊，以及查詢服務整合指南，以取得有關Data Science Workspace如何與查詢服務互動的詳細資訊。

### 區段服務

Adobe Experience Platform Segmentation Service可讓使用者將客戶劃分為具有類似特徵的較小群組。 您隨後可評估這些區段，以便對即時客戶個人檔案資料提供更佳的分析。 查詢服務可用來在資料湖中執行此區段資料的查詢，以提供此分析。 請閱讀區段服務概觀以取得區段的詳細資訊，以及描述檔查詢語言(PQL)指南，以取得如何分析區段的詳細資訊。

## 後續步驟

閱讀本檔案後，您便瞭解了Query Service，以及它如何在更廣泛的Experience Platform中運作。 有關與查詢服務API中各個端點互動的詳細資訊，請參閱查詢服務開 [發人員指南](api/getting-started.md)。 有關在平台中使用互動式服務的更多資訊，請閱讀 [Query Service使用者介面指南](ui/overview.md)。 有關連接外部客戶機與查詢服務的完整清單，請閱讀查詢服 [務客戶機概述](clients/overview.md)。
