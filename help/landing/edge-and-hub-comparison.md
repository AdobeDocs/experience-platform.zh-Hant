---
solution: Experience Platform
title: Edge Network 與中心網路的比較
description: 瞭解可在Adobe Experience Platform上使用的不同處理路徑。
exl-id: 3e9c63d2-c798-44b4-870d-bf1551f29690
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '713'
ht-degree: 3%

---

# Edge Network 與中心網路的比較

Adobe Experience Platform是市面上功能最強大、最靈活、最開放的系統，可建置和管理可提升客戶體驗的完整解決方案。 您可以使用Experience Platform來集中和標準化來自任何系統的客戶資料和內容，並運用資料科學和機器學習來顯著改進豐富個人化體驗的設計和傳遞。 因此，Experience Platform提供多種資料處理方式，讓您以最佳方式評估資料。

## 伺服器型別

在Experience Platform上，可透過兩個不同的路徑處理資料：適用於批次和串流工作流程的Adobe Experience Platform中樞以及適用於即時體驗的Edge Network 。

### Adobe Experience Platform中心

中心是主要資料中心，位於中央位置，包含已在Adobe Experience Platform中收集的所有歷史資料及豐富設定檔內容。 這可讓您傳送和接收更強大且完整的資料給下游服務。 因此，在資料的&#x200B;**完整性**&#x200B;較重要的情況下，應該使用集線器。

集線器上的可用服務包括：

- 批次分段
- 串流區段
- 輪廓
- 目標
- 身分識別圖表
- 資料Distiller — 查詢服務
- Source聯結器

### Experience Platform Edge Network

Edge Network是一部伺服器，實際位置更接近不同的地理位置。 這些資料中心會處理透過SDK擴充功能和Edge Network API收集的所有資料。 Edge Network上存在的唯一資料是對象會籍、設定檔身分和個人化所需的屬性。

由於客戶與一般使用者較近，Edge Network可讓您更快速地傳送及接收資料給客戶。 此外，您可以使用Edge Network來處理事件轉送請求和標籤管理請求。 不過，Edge Network僅處理&#x200B;**行為**&#x200B;資料。 因此，Edge Network應該用於資料的&#x200B;**速度**&#x200B;較重要的情況。

Edge Network上的可用服務包括：

- 邊緣分段
- Edge設定檔
- Edge目的地
- 資料彙集
- SDK擴充功能

## 位置

下節列出中心和Edge Network的位置。

![列出集線器與Edge Network伺服器之不同位置的圖表。](./images/servers/platform-server-locations.png)

**中心**

- VA7 （美國維吉尼亞）
- NLD2 （荷蘭）
- AUS5 （澳洲）
- CAN2 （加拿大）
- GBR9 （英國）
- IND1 （印度）

**Edge Network**

- OR2 （美國奧勒岡州）
- VA6 （美國維吉尼亞州）
- IRL1 （愛爾蘭）
- IND1 （印度）
- SGP3 （新加坡）
- AUS3 （澳洲）
- JPN3 （日本）

有關可用伺服器位置的詳細資訊，請參閱[多雲端總覽](./multi-cloud.md#available-cloud-regions)。

## 後續步驟

閱讀本概述後，您現在瞭解在Adobe Experience Platform中心處理資料與Adobe Experience Platform Edge Network處理資料的差異。

## 附錄

下節列出有關在Adobe Experience Platform上處理資料的補充資訊。

### 常見問題

下節列出有關中心和Edge Network的常見問題：

#### 哪一種情況最適合集線器？

中心最適合資料的&#x200B;**完整性**&#x200B;較重要的情況。 例如，假設您想要建立行銷活動，以定位所有已放棄購物車的客戶。 在該使用案例中，您可以使用批次分段，建立符合捨棄購物車使用者的對象，並將其匯出至批次目的地。

#### 哪些案例最適合使用Edge Network？

Edge Network最適合使用&#x200B;**速度**&#x200B;資料較重要的情況。 例如，假設您需要建立有限的快閃銷售，將目標鎖定在購物車中有產品瀏覽您網站的客戶。 在該使用案例中，您可以使用邊緣細分，立即鎖定目標並傳送個人化通知給購物車中具有「閃購」產品的使用者。

#### 從中樞到Edge Network會傳送哪些資料？

只有在Edge上提供即時體驗所需的資料，才會從中心載入到Edge Network。 系統會自動將此資料從集線器傳送至Edge Network，以最終維持一致性，最多只會保留14天。 但是，這並&#x200B;**不**&#x200B;表示資料會與集線器中的資料保持完全同步。 因此，中樞和Edge Network之間的可用資料可能有所差異。
