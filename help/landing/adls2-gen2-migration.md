---
source-git-commit: b9816767556b9d50cf2ff5268816d1de6b85fc63
workflow-type: tm+mt
translation-type: tm+mt
source-wordcount: '262'
ht-degree: 0%

---
# Adobe Experience Platform Data Lake遷移至Gen2

Adobe Experience Platform正在移轉至Gen2 Data Lake。 這是新一代的資料庫，為平台使用者提供地理區域複製、更精細的角色存取控制(RBAC)和更佳的縮放等優點。

## 使用者影響

當Adobe將Data Lake從Gen1移轉至Gen 2時，使用者將能夠從 **Data** Lake讀取，但所有寫入 **** Data Lake的功能都將受到影響。 以下是受影響的功能清單：

- **來源**:來自來源的資料和各種資料擷取工作流程將會延遲。 移轉完成後，使用者將看到其資料。
- **查詢服務**:使用者可以執行查詢，但無法將查詢的輸出寫入資料集。
- **即時客戶個人檔案**:移轉期間，無法透過批次擷 **取** ，擷取至描述檔儲存的資料。 不過，在移轉期間， **透過串流** 擷取所擷取的資料將可供使用。 此外，在移轉期間，描述檔匯出將無法使用。
- **資料科學工作區**:來自Data Science Workspace的寫入操作將失敗。
- **區段服務**:移轉期間無 **法啟用** 「從批次分段衍生的觀眾」。 從串流區 **段衍生** 的觀眾不會受到影響。
- **客戶歷程分析**:「客戶歷程分析」報告資料可能已過時，且在移轉期間不會重新整理，因為批次未被收錄到Data Lake中。

## 與平台使用者的通訊

Adobe將聯絡系統管理員，詳細討論移轉的影響，並確認特定IMS組織的移轉日期和時間。