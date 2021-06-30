---
title: Data Lake遷移到Gen2
description: 了解Adobe Experience Platform中將Data Lake移轉至Gen2所提供的新功能。
exl-id: 56d9c77a-d7eb-498d-994f-b15d150dedb7
source-git-commit: 97f803f649b2c42b0449a2f8f0cff370ed1aba93
workflow-type: tm+mt
source-wordcount: '286'
ht-degree: 0%

---

# Adobe Experience Platform Data Lake遷移至Gen2

Adobe Experience Platform正在移轉至Gen2 Data Lake。 這是新一代的資料湖，為Platform使用者提供地理區域復寫、更精細的角色型存取控制(RBAC)和更佳的擴充功能等優勢。

## 使用者影響

當Adobe將資料湖從Gen1遷移到Gen2時，用戶將能夠從資料湖&#x200B;**讀取**，但&#x200B;**寫入**&#x200B;到資料湖的所有功能都將受到影響。 以下是受影響功能的清單：

- **來源**:來自來源和各種資料擷取工作流程的資料將會延遲。移轉完成後，使用者就會看到其資料。
- **查詢服務**:使用者可以執行查詢，但無法將查詢的輸出寫入資料集。
- **即時客戶個人檔案**:透過批次擷取擷取擷取至設 **** 定檔存放區的資料在移轉期間將無法使用。不過，透過&#x200B;**串流**&#x200B;擷取擷取的資料，將可在移轉期間使用。 此外，移轉期間將無法使用設定檔匯出。
- **Data Science Workspace**:來自Data Science Workspace的寫入作業將會失敗。
- **區段服務**:從批次分段 **** 衍生的對象無法在移轉期間啟用。衍生自&#x200B;**串流**&#x200B;區段的對象將不受影響。
- **Customer Journey Analytics**:Customer Journey Analytics報表資料可能已過期，且在移轉期間不會重新整理，因為批次資料不會匯入Data Lake。

## 與Platform使用者的通訊

Adobe會聯絡系統管理員，詳細討論移轉的影響，並確認特定IMS組織的移轉日期和時間。
