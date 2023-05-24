---
title: 資料湖遷移到Gen2
description: 瞭解將Data Lake遷移到Adobe Experience Platform的Gen2所提供的新功能。
exl-id: 56d9c77a-d7eb-498d-994f-b15d150dedb7
source-git-commit: 81f48de908b274d836f551bec5693de13c5edaf1
workflow-type: tm+mt
source-wordcount: '285'
ht-degree: 0%

---

# Adobe Experience Platform資料湖遷移到第2代

Adobe Experience Platform正在遷移到Gen2 Data Lake。 這是新一代資料湖，它為平台用戶提供了諸如地理區域複製、更精細的基於角色的訪問控制(RBAC)和更好的擴展等優勢。

## 用戶影響

當Adobe將Data Lake從Gen1遷移到Gen2時，用戶將能夠 **讀** 資料湖，但所有能力 **寫** 進入資料湖會受到影響。 以下是受影響功能的清單：

- **源**:來自源的資料和各種資料接收工作流將被延遲。 遷移完成後，用戶將看到其資料。
- **查詢服務**:用戶可以執行查詢，但無法將查詢的輸出寫入資料集。
- **即時客戶配置檔案**:通過接收到配置檔案儲存的資料 **批** 遷移期間將不提供攝取。 但是，通過 **流** 遷移期間將提供攝取。 此外，遷移期間將不提供配置檔案導出。
- **資料科學工作區**:來自Data Science Workspace的寫入操作將失敗。
- **分段服務**:源自 **批** 無法在遷移期間激活分段。 源自 **流** 分割不會受到影響。
- **Customer Journey Analytics**:Customer Journey Analytics報告資料可能已過期，在遷移期間不會刷新，因為未將批次插入資料湖。

## 與平台用戶的通信

Adobe將聯繫系統管理員，詳細討論遷移的影響，並確認特定組織的遷移日期和時間。
