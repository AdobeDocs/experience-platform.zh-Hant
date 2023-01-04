---
title: Data Lake遷移到Gen2
description: 了解Adobe Experience Platform中將Data Lake移轉至Gen2所提供的新功能。
exl-id: 56d9c77a-d7eb-498d-994f-b15d150dedb7
source-git-commit: 34e0381d40f884cd92157d08385d889b1739845f
workflow-type: tm+mt
source-wordcount: '286'
ht-degree: 0%

---

# Adobe Experience Platform Data Lake遷移至Gen2

Adobe Experience Platform正在移轉至Gen2 Data Lake。 這是新一代的資料湖，為Platform使用者提供地理區域復寫、更精細的角色型存取控制(RBAC)和更佳的擴充功能等優勢。

## 使用者影響

當Adobe將資料湖從Gen1遷移到Gen2時，用戶將能夠 **讀取** 資料湖，但所有能力 **寫入** 進入Data Lake時會受到影響。 以下是受影響功能的清單：

- **來源**:來自來源和各種資料擷取工作流程的資料將會延遲。 移轉完成後，使用者就會看到其資料。
- **查詢服務**:使用者可以執行查詢，但無法將查詢的輸出寫入資料集。
- **即時客戶個人檔案**:透過 **批次** 移轉期間將無法使用擷取功能。 不過，透過 **串流** 移轉期間將可使用擷取功能。 此外，移轉期間將無法使用設定檔匯出。
- **Data Science Workspace**:來自Data Science Workspace的寫入作業將會失敗。
- **區段服務**:衍生自 **批次** 移轉期間無法啟動分段。 衍生自 **串流** 區段不受影響。
- **Customer Journey Analytics**:Customer Journey Analytics報表資料可能已過期，且在移轉期間不會重新整理，因為批次資料不會匯入Data Lake。

## 與Platform使用者的通訊

Adobe會聯絡系統管理員，詳細討論移轉的影響，並確認特定IMS組織的移轉日期和時間。
