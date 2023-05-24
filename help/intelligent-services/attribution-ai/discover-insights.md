---
keywords: Experience Platform；真知灼見；屬性；熱門主題；屬性真知灼見
feature: Attribution AI
title: 在Attribution AI中發現洞察力
description: 本文檔用作與Adobe智慧服務用戶介面中的服務實例透視交互的指南。
exl-id: 6b8e51e7-1b56-4f4e-94cf-96672b426c88
source-git-commit: e4e30fb80be43d811921214094cf94331cbc0d38
workflow-type: tm+mt
source-wordcount: '1656'
ht-degree: 0%

---

# 在Attribution AI中發現洞見

Attribution AI服務實例提供可用於幫助制定和衡量與營銷業績和投資回報相關的營銷決策的洞見。 選擇服務實例可提供可視化效果和篩選器，幫助您瞭解客戶旅程的每個階段中每個客戶交互的影響。

本文檔用作與Adobe智慧服務用戶介面中的服務實例透視交互的指南。

## 快速入門

為了利用洞察力進行Attribution AI，您需要有一個運行狀態成功的服務實例。 要建立新服務實例，請訪問 [Attribution AI用戶介面指南](./user-guide.md)。 如果您最近建立了一個服務實例，但該實例仍在訓練和評分，請允許它24小時才能完成運行。

## 服務實例透視概述

在 [!DNL Adobe Experience Platform] UI，選擇 **[!UICONTROL 服務]** 的子菜單。 的 **[!UICONTROL 服務]** 瀏覽器出現並顯示可用Adobe智慧服務。 在Attribution AI容器中，選擇 **[!UICONTROL 開啟]**。

![訪問實例](./images/insights/open_Attribution_ai.png)

將顯示Attribution AI服務頁面。 此頁列出Attribution AI的服務實例並顯示有關這些實例的資訊，包括實例名稱、轉換事件、實例的運行頻率以及上次更新的狀態。 選擇要開始的服務實例名稱。

>[!NOTE]
>
>只能選擇已完成成功計分運行的服務實例。

![建立實例](./images/insights/select-service-instance.png)

接下來，將顯示該服務實例的透視頁面，其中為您提供了可視化效果和多個篩選器以與資料交互。 在本指南中，將對可視化效果和濾鏡進行更詳細的說明。

![設定頁面](./images/insights/landing-page.png)

### 服務實例詳細資訊

要查看服務實例的附加詳細資訊，請選擇 **[!UICONTROL 顯示更多]** 右上角。

![顯示更多](./images/insights/show-more.png)

將顯示詳細清單。 有關所列任何屬性的詳細資訊，請訪問 [Attribution AI使用手冊](./user-guide.md)。

![顯示詳細資訊](./images/insights/advanced-details.png)

### 編輯實例

要編輯實例，請選擇 **[!UICONTROL 編輯]** 的上界。
![按一下「編輯」按鈕](./images/insights/edit-button.png)

此時將出現「編輯」對話框，允許您編輯實例的名稱、說明和記分頻率。 如果實例狀態被禁用，則無法編輯計分頻率。 要確認更改並關閉對話框，請選擇 **[!UICONTROL 保存]** 在右下角。

![編輯跨距](./images/insights/edit-popover.png)

### 更多操作 {#more-actions}

的 **[!UICONTROL 更多操作]** 按鈕位於右上角的導航中 **[!UICONTROL 編輯]**。 選擇 **[!UICONTROL 更多操作]** 開啟一個下拉清單，您可以選擇以下操作之一：

- **[!UICONTROL 克隆]**:克隆實例。
- **[!UICONTROL 刪除]**:刪除實例。
- **[!UICONTROL 下載摘要資料]**:下載包含摘要資料的CSV檔案。
- **[!UICONTROL 訪問分數]**:選擇 **[!UICONTROL 訪問分數]** 將你引向 [訪問分數教程](./download-scores.md)。
- **[!UICONTROL 查看運行歷史記錄]**:此時將顯示一個跨距，其中包含與服務實例關聯的所有計分運行的清單。

![更多操作](./images/insights/more-actions.png)

## 篩選資料

Attribution AI透視允許您過濾資料並根據選定的過濾器自動更新用戶介面視覺對象。

### 轉換事件

在Attribution AI中建立新實例時，其中一個必填欄位是「轉換事件」。 轉換事件是確定營銷活動影響的業務目標，如電子商務訂單、店內採購和網站訪問。

在實例內， **[!UICONTROL 轉換事件]** 下拉菜單允許您選擇為實例定義的任何事件以篩選資料。 選擇特定事件將UI可視化內容更改為僅填充屬於這些事件的轉換。

![轉換事件](./images/insights/conversion-event.png)

### 歸因模型

選擇 **[!UICONTROL 屬性模型]** 開啟一個下拉清單，其中所有不同的屬性模型都可用。 可以選擇多個模型來比較結果。 有關不同的屬性模型及其工作原理的詳細資訊，請訪問 [Attribution AI](./overview.md) 概述，其中包含包含每個模型資訊的表。

![屬性模型](./images/insights/attribution-model.png)

### 區域

>[!NOTE]
>
>僅當您執行了可選步驟時，此篩選器才存在 [區域建模](./user-guide.md#region-based-modeling-optional) 建立服務實例時的「Attribution AI」用戶介面指南。

此過濾器允許您選擇在實例建立過程中設定的任何區域。

### 添加篩選器

通過選擇 **濾波器** 表徵圖以開啟 **[!UICONTROL 添加篩選器]** 沿面。 的 **[!UICONTROL 添加篩選器]** popover允許您按通道、地理位置、媒體類型和產品進行篩選。 只有服務實例的適用過濾器由跨距填充。 例如，如果您未提供地理資料或媒體類型，則這些篩選器屬性將不可用於您的實例。

![額外篩選](./images/insights/additional-filters.png)

![過濾](./images/insights/filter-popover.png)

- **[!UICONTROL 頻道]:** 選擇渠道屬性允許您篩選任何可用的市場營銷渠道。 可以選擇多個通道來比較它們。
- **[!UICONTROL 地理]:** 選擇地理位置屬性允許您根據基於區域的模型篩選國家代碼。 根據您的資料，此篩選器可能存在，也可能不存在。 國家/地區代碼為兩個字元長。 請參閱完整的國家/地區代碼清單 [這裡](https://datahub.io/core/country-list)。
- **[!UICONTROL 媒體類型]:** 選擇媒體類型屬性允許您過濾任何定義的媒體類型。
- **[!UICONTROL 產品]:** 選擇product屬性允許您從建立實例時最初攝取的任何產品中篩選。

### 日期範圍

選擇日曆表徵圖以開啟日期範圍跨距。 開始和結束轉換事件日期確定在UI中填充的資料量。 您可以選擇縮小或擴大日期範圍，以集中或擴展填充的資料量。

![日期範圍](./images/insights/display-date-range.png)

## 資料概述

的 **[!UICONTROL 概述]** card按屬性模型顯示總轉換。 總數根據您使用本文檔前面概述的篩選器進行搜索的具體程度而更改。 選擇更多模型會向「概述」(Overview)添加其他圓，每個圓的顏色與圖例對應。

![概覽](./images/insights/Overview.png)

## 每週趨勢

的 **[!UICONTROL 每週趨勢]** card按您在篩選過程中設定的日期範圍分解您的總轉換。

在右上角選取橢圓 **每週趨勢** 卡顯示一個下拉清單，允許您選擇每日、每週或每月趨勢。

懸停在特定屬性模型的資料行上會建立一個跨距，顯示該日期的轉換總數。

![趨勢](./images/insights/weekly-trends.png)

## 按渠道細分

的 **[!UICONTROL 按渠道細分]** 卡用於確定與每個通道相關的轉換總數。 此卡可用於幫助就每個渠道的有效性和投資回報做出決策。

在右上角選取橢圓 **[!UICONTROL 按渠道細分]** 卡將開啟一個下拉清單，允許您根據觸點填充資料。

![擊穿通道](./images/insights/channel-breakdown.png)

## 頂級市場活動

的 **[!UICONTROL 頂級市場活動]** card顯示市場活動概覽以及市場活動在每個渠道中的表現。 此卡可以幫助您的團隊瞭解特定渠道的特定活動的有效性，並提供深入的見解，例如您應進一步投資的活動。

![頂級活動](./images/insights/top-campaigns.png)

## 按觸地位置分列的故障

選擇 **[!UICONTROL 路徑分析]** 頁籤載入 **[!UICONTROL 按觸地位置分列的故障]** 和 **[!UICONTROL 頂部轉換路徑]** 圖形。

的 **[!UICONTROL 按觸地位置分列的故障]** graph是按所有轉換路徑上比較的觸點位置劃分的屬性轉換細分。 此圖表有助於您瞭解哪些點在轉換路徑的不同階段更有效。 舞台是開場、玩家和更近的。

- **入門：** 指示觸點是轉換路徑中的第一次觸點。
- **玩家：** 指示觸點不是導致轉換的第一次或最後一次觸摸。
- **近點：** 指示觸點是轉換前的最後一次觸摸。

>!![NOTE]
所有觸地點和位置的歸屬模型所佔百分比之和應等於100。

![用戶路徑故障觸點](./images/insights/user-paths.png)

## 頂部轉換路徑

的 **[!UICONTROL 頂部轉換路徑]** 圖形顯示所選區域中頂部轉換路徑上的影響和算法得分。 此圖表允許您直觀地顯示哪些觸點有助於轉換，以及每個觸點的歸因得分。 您可以使用此資訊查看特定區域中最頻繁的路徑，並查看不同點集之間是否出現任何模式。

![最常見的用戶路徑](./images/insights/Touchpoint-paths.png)

## 觸點效能

選擇 **[!UICONTROL 觸地點有效性]** 頁籤載入 **[!UICONTROL 觸點效能]** 卡。 此卡使用Attribution AI的資料分發來顯示每個觸點的資訊。 此表的資料僅生成特定時間段(如 **[!UICONTROL 截至]** 卡右上角的日期。

![觸點效能選擇](./images/insights/Touchpoint-effectiveness.png)

您可以使用 **[!UICONTROL 觸點效能]** 卡資訊，以瞭解觸點如何促成轉換。 您還可以通過以下效能指標瞭解每個觸點的有效性：

**接觸的路徑**:此度量顯示達到/未達到觸點轉換的路徑的百分比。 如果實現轉換的路徑與未實現轉換的路徑的比率（百分比）較高，則將看到更高的屬性轉換。

![接觸的路徑度量](./images/insights/Touchpoint-metrics.png)

**效率度量**:此度量以1到5的比例顯示星體。 比例表示點在進行轉換時的相對重要性。

>[!NOTE]
接觸點體積越大，效率越高。

**總卷**:用戶觸碰觸點的總次數。 這包括在實現轉換的路徑上出現的觸點，以及不導致轉換的路徑。

## 後續步驟

一旦您完成了對資料的篩選並能夠顯示適當的資訊，您就可以選擇訪問分數。 有關如何訪問分數的深入指南，請訪問 [訪問分數在Attribution AI](./download-scores.md) 教程。 此外，您還可以下載摘要資料，如中所示 [更多操作](#more-actions)。 選擇「下載摘要資料」將下載按日期聚合的摘要資料。

## 其他資源

以下視頻旨在幫助學習如何使用Attribution AI洞察力頁面瞭解營銷渠道和活動的ROI。

>[!VIDEO](https://video.tv.adobe.com/v/32669?learn=on&quality=12)
