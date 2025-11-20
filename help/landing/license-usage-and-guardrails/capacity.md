---
title: 授權使用量和容量
description: 瞭解您在Adobe Experience Platform中的授權使用量和容量限制。
exl-id: 38dad2f1-bd0f-4cc3-a3a6-5105ea866ea4
source-git-commit: ae0c626eaad66f663c9d97137087b2cca24d747e
workflow-type: tm+mt
source-wordcount: '1605'
ht-degree: 6%

---


# 授權使用和容量

>[!AVAILABILITY]
>
>若要使用此功能，您必須具備下列許可權：
>
>- **檢視授權使用量儀表板**
>   - 此許可權可讓您&#x200B;**檢視**&#x200B;容量首頁。
>- **管理沙箱**
>   - 此許可權可讓您&#x200B;**編輯**&#x200B;您的容量配置。
>   - 此外，您&#x200B;**必須**&#x200B;被指派存取您要編輯其容量分配的所有沙箱。
>
>在[存取控制總覽](/help/access-control/home.md#permissions)中可以找到Experience Platform內許可權的更多資訊
>
>此外，如果您已購買「高輸送量串流分段」，您將&#x200B;**無法**&#x200B;使用容量來配置您的容量。 若要更新容量，請聯絡Adobe客戶服務。

在Adobe Experience Platform中，容量可讓您知道您的組織是否已超過任何護欄，並提供有關如何解決這些問題的資訊。

如需Experience Platform中護欄的詳細資訊，請參閱[Real-Time CDP護欄概觀](../../rtcdp/guardrails/overview.md)。

## 容量行為 {#behavior}

>[!CONTEXTUALHELP]
>id="platform_capacity_streamingthroughput"
>title="串流輸送量"
>abstract="串流輸送量值用以測量在生產與開發沙箱中，將串流攝取傳入輪廓服務時，每秒最高的合併傳入事件數。"

>[!CONTEXTUALHELP]
>id="platform_capacity_streamingaudiences"
>title="串流客群計數"
>abstract="每個沙箱的串流客群數量上限。此數值包括沙箱中的邊緣客群數量。"

>[!CONTEXTUALHELP]
>id="platform_capacity_edgeaudiences"
>title="邊緣客群"
>abstract="每個沙箱的邊緣客群數量上限。"

目前，容量支援下列服務：

- 串流區段
- 串流擷取

在這些服務中，會追蹤以下護欄：

- 串流對象的最大數量為500個
   - 在這500個串流對象中，邊緣對象的最大數量為150個
- 串流擷取的初始合併輸送量為每秒1500筆記錄(rps)
   - 此合併的串流輸送量會測量每秒的合併尖峰傳入事件，以將擷取串流到您生產和開發沙箱中的即時客戶個人檔案。
   - 您可以購買額外的串流細分支援，最高可達每秒13,500筆記錄。 如需有關購買額外權益的詳細資訊，請參閱[Real-Time CDP產品說明](https://helpx.adobe.com/tw/legal/product-descriptions/real-time-customer-data-platform-b2c-edition-prime-and-ultimate-packages.html)。

對象容量處於&#x200B;**沙箱**&#x200B;層級。 這表示，對於您組織內的每個沙箱，您可以擁有500個串流對象，其中150個可以是Edge對象。

串流輸送量容量為&#x200B;**組織**&#x200B;層級，可分發到您的個別沙箱。 例如，使用串流擷取輸送量的1500 rps，您可以將生產沙箱設定為1300 rps，將開發沙箱設定為200 rps。

Experience Platform會以15分鐘滾動間隔計算沙箱的輸送量。 此輸送量以即時測量，每60秒會重新整理資料一次。

如果您的使用量達到授權容量的80%和90%，Experience Platform會發出警報，通知您達到指定容量上限。 您可以修改設定以自訂容量百分比，以接收警示或完全移除警示。

如果您的使用量超過授權容量的100%，則會視為違反您的容量。 此時，您將會遇到效能延遲，而且您的服務等級目標(SLT)將&#x200B;**無法**&#x200B;保證。

## 存取權 {#access}

若要存取容量概觀，請選取&#x200B;**[!UICONTROL License usage]**，然後選取&#x200B;**[!UICONTROL Capacity]**。

![已反白顯示存取[容量]區段的方法。](/help/landing/images/capacity/access-capacity.png)

此時會顯示「產能概觀」頁面，顯示包括警示歷史記錄以及組織產能詳細資訊的資訊。

![「容量概觀」頁面會完整顯示，並顯示警示歷程記錄和容量詳細資料區段。](/help/landing/images/capacity/capacity-overview.png) {zoomable="yes" width="80%"}

### 警報歷史記錄 {#alert-history}

**[!UICONTROL Alert history]**&#x200B;區段會顯示貴組織內最近的容量違規。

![顯示警示歷程記錄區段。](/help/landing/images/capacity/alert-history.png)

| 欄名稱 | 說明 |
| ----------- | ----------- |
| 沙箱 | 發生容量違規的沙箱名稱。 |
| 警報 | 沙箱中已破壞的容量。 |
| 時間戳記 | 發生違規的資料和時間。 |

若要檢視貴組織警示的完整歷程記錄，請選取![三點圖示](/help/images/icons/more.png)，接著選取&#x200B;**[!UICONTROL View all]**。

![顯示組織的完整警示歷史記錄。](/help/landing/images/capacity/full-alert-history.png)

### 容量詳細資料 {#capacity-details}

容量詳細資訊區段概述有關您組織容量的資訊。 在此區段中，您可以篩選每個沙箱並變更回顧期間。

![回顧期間的沙箱選擇器和日期選擇器會醒目提示。](/help/landing/images/capacity/filter-sandbox-and-date.png)

目前，這會顯示串流輸送量、串流對象和邊緣對象的容量資訊。

#### 串流輸送量 {#streaming-throughput}

串流輸送量區段會顯示有關您組織沙箱中的串流輸送量的資訊。 串流輸送量值會測量每秒將內嵌串流至設定檔服務的合併尖峰傳入事件。

![顯示容量詳細資訊頁面中的串流輸送量區段。](/help/landing/images/capacity/streaming-throughput-section.png)

| 欄名稱 | 說明 |
| ----------- | ----------- |
| 沙箱 | 沙箱的名稱。 |
| 服務 | 沙箱使用的服務。 目前，唯一支援的值是設定檔。 |
| 使用量（尖峰） | 在選取的回顧期間內，沙箱中資料的尖峰串流輸送量。 |
| 容量 | 沙箱的最大尖峰串流輸送量。 |
| 違規 | 如果發生違規，則為串流輸送量的違規型別。 |
| 建議的動作 | 說明緩解違規的建議動作的欄。 |

您可以選取個別沙箱，以檢視沙箱的串流輸送量的更詳細檢視。

![在串流處理量區段中反白顯示沙箱。](/help/landing/images/capacity/select-sandbox.png)

此時會顯示「串流輸送量詳細資訊」頁面。 您可以看到顯示與容量限制比較的請求輸送量的圖形、沙箱及其輸送量的清單，以及配置組織容量的按鈕。

![顯示串流處理量頁面，顯示所選沙箱的串流處理量的詳細資訊。](/help/landing/images/capacity/streaming-capacity-allocation.png)

若要更新組織的串流輸送量容量，請選取&#x200B;**[!UICONTROL Allocate capacities]**。

![串流輸送量詳細資訊頁面中會醒目顯示[配置容量]按鈕。](/help/landing/images/capacity/select-allocate.png)

配置頁面隨即顯示。 在此頁面中，您可以設定不同沙箱的容量。 所有容量的總和&#x200B;**必須**&#x200B;等於組織的容量總計。

![顯示容量配置頁面。](/help/landing/images/capacity/allocate-capacity.png)

>[!NOTE]
>
>您只能以&#x200B;**100**&#x200B;的順序設定新容量。 例如，您可以將沙箱的新容量值設為300或500，但您&#x200B;**無法**&#x200B;將此值設為450。
>
>如果值的順序不是100，則會相應地向上或向下舍入。

更新容量配置後，選取&#x200B;**[!UICONTROL Save]**&#x200B;以完成更新。 請注意，變更最多可能需要10分鐘的時間才會反映在您的組織上。

#### 客群計數 {#audience-count}

**[!UICONTROL Streaming audience count]**&#x200B;和&#x200B;**[!UICONTROL Edge audience count]**&#x200B;區段會顯示沙箱中的串流和邊緣對象數量，以及沙箱中允許的最大串流和邊緣對象數量。

![顯示[對象計數]區段。](/help/landing/images/capacity/audience-count.png)

| 欄名稱 | 說明 |
| ----------- | ----------- |
| 沙箱 | 沙箱的名稱。 |
| 服務 | 用於沙箱的服務。 |
| 使用方式 | 沙箱中列出型別的對象數。 |
| 容量 | 沙箱中允許之所列型別的對象最大數量。 |

## 串流輸送量最佳實務 {#suggestions}

您可以採用下列其中一種建議來解決串流輸送量違規：

1. 增加沙箱的已分配容量。
2. 識別[監視儀表板](/help/dataflows/ui/monitor-streaming-profile.md)中的高輸送量資料流，並視需要對這些資料流套用節流或篩選。
3. 透過使用批次擷取來減少延遲使用案例，讓您的擷取最佳化。

此外，您可以檢視資料流，瞭解是否能將資料策略最佳化。

| 貢獻因數 | 內容 | 對使用案例的影響 | 最佳做法 |
| --- | --- | --- | --- |
| 批次至串流轉換 | 批次工作負荷轉換為串流可大幅增加輸送量，進而影響效能和資源配置。 例如，在沒有速率限制的事件之後執行大量設定檔更新。 | 不需要低延遲處理時，批次使用案例就不需要串流策略。 | 評估使用案例需求。 針對批次傳出行銷，請考慮使用[批次擷取](/help/ingestion/batch-ingestion/overview.md)而非串流，以更有效率地管理資料擷取。 |
| 不必要的資料擷取 | 個人化不需要擷取資料可增加輸送量，而不會增加值，進而浪費資源。 例如，不論相關性為何，都將所有Analytics流量擷取至設定檔。 | 過多的不相關資料會產生雜訊，使得識別具影響力的資料點變得更困難。 在定義和管理對象和設定檔時，這也會造成摩擦。 | 僅擷取使用案例所需的資料。 請確定您篩選掉不必要的資料。<ul><li>**Adobe Analytics**：使用[資料列層級篩選](/help/sources/tutorials/ui/create/adobe-applications/analytics.md#filtering-for-real-time-customer-profile)來最佳化您的資料輸入。</li><li>**來源**：使用[[!DNL Flow Service] API來篩選所支援來源（如](/help/sources/tutorials/api/filter.md)和[!DNL Snowflake]）的資料列層級資料[!DNL Google BigQuery]。</li></li>**Edge資料流**：設定[動態資料流](/help/datastreams/configure-dynamic-datastream.md)，對來自WebSDK的流量執行列層級篩選。</li></ul> |

## 影片概觀 {#video}

下列影片提供容量概觀。

>[!VIDEO](https://video.tv.adobe.com/v/3475272/?learn=on&enablevpops)

## 常見問題 {#faq}

以下章節概述有關容量功能的常見問題。

### 我可以有總和小於目標最大值的合併輸送量上限嗎？

+++ 回答

不可以。 最大合併輸送量限制&#x200B;**必須**&#x200B;總計為您組織的護欄。

+++

### 如果超出最大容量，會發生什麼情況？

+++ 回答

這取決於超過的容量。

目前，如果您超過允許的最大受眾數量，您的過多受眾將不受影響。 不過，日後建立新對象的能力可能會受到限制。

如果超過串流輸送量，您會在擷取和分段中遇到效能延遲的問題。

+++

### 為何要遵循最大容量？

+++ 回答

在最大容量內工作，可確保資料保持一致，並保持資料的完整性。

您可在尖峰事件期間確保一致的效能，避免可能對系統效能造成負面影響，並影響下遊客戶體驗的技術問題，最終提升您的資料衛生和整體系統效能。

+++

### 管理串流擷取輸送量的最佳實務是什麼？

+++ 回答

為了最佳地管理您的串流擷取輸送量，您應該評估資料集，以確保它們為個人化所需的資料排定優先順序。


如果不需要即時處理，您應使用批次擷取，而非串流擷取。

+++
