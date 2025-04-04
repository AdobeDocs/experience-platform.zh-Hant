---
title: Data Lake移轉至Gen2
description: 瞭解在Adobe Experience Platform中將Data Lake移轉至Gen2所提供的新功能。
exl-id: 56d9c77a-d7eb-498d-994f-b15d150dedb7
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '288'
ht-degree: 0%

---

# Adobe Experience Platform Data Lake移轉至Gen2

Adobe Experience Platform正在移轉至Gen2資料湖。 這是新一代的資料湖，可為Experience Platform使用者提供地理區域復寫、更精細的角色型存取控制(RBAC)和更好的擴充等優勢。

## 使用者影響

當Adobe將Data Lake從Gen1移轉至Gen 2時，使用者將能夠從Data Lake **讀取**，但&#x200B;**寫入**&#x200B;到Data Lake的所有功能都將受到影響。 以下是受影響的功能清單：

- **來源**：從來源及各種資料擷取工作流程傳入的資料將會延遲。 移轉完成後，使用者可以看到其資料。
- **查詢服務**：使用者可以執行查詢，但是無法將查詢的輸出寫入資料集。
- **即時客戶設定檔**：移轉期間將無法使用透過&#x200B;**批次**&#x200B;擷取而擷取到設定檔存放區的資料。 不過，透過&#x200B;**串流**&#x200B;擷取所擷取的資料將在移轉期間提供使用。 此外，在移轉期間將無法使用設定檔匯出。
- **資料科學Workspace**：從資料科學Workspace寫入將會失敗。
- **分段服務**：移轉期間無法啟用衍生自&#x200B;**批次**&#x200B;分段的對象。 從&#x200B;**串流**&#x200B;細分衍生的對象將不會受到影響。
- **Customer Journey Analytics**： Customer Journey Analytics報告資料可能已過期，移轉期間不會重新整理，因為批次未擷取至Data Lake。

## 與Experience Platform使用者通訊

Adobe將會連絡系統管理員，詳細討論移轉的影響，並確認特定組織的移轉日期和時間。
