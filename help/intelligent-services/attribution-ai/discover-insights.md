---
keywords: Experience Platform；見解；歸因ai；熱門主題；歸因ai見解
solution: Intelligent Services, Experience Platform
title: 探索Attribution AI的見解
topic-legacy: Attribution AI insights
description: 本檔案可做為Adobe智慧型服務使用者介面中與服務例項深入資訊互動的指南。
exl-id: 6b8e51e7-1b56-4f4e-94cf-96672b426c88
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '1584'
ht-degree: 0%

---

# 探索Attribution AI的見解

Attribution AI服務例項可提供深入資訊，可協助您制定和衡量與行銷績效及投資報酬相關的行銷決策。 選擇服務例項可提供視覺化和篩選，協助您瞭解客戶歷程每個階段中每個客戶互動的影響。

本檔案可做為Adobe智慧型服務使用者介面中與服務例項深入資訊互動的指南。

## 快速入門

為了運用深入資訊進行Attribution AI，您需要有成功執行狀態的服務例項。 要建立新服務實例，請訪問[Attribution AI用戶介面指南](./user-guide.md)。 如果您最近建立了一個服務例項，但它仍在訓練和計分中，請允許24小時以完成執行。

## 服務實例見解總覽

在[!DNL Adobe Experience Platform] UI中，選擇左側導覽中的&#x200B;**[!UICONTROL Services]**。 出現&#x200B;**[!UICONTROL Services]**&#x200B;瀏覽器並顯示可用的Adobe智慧服務。 在Attribution AI容器中，選擇&#x200B;**[!UICONTROL Open]**。

![存取您的例項](./images/insights/open_Attribution_ai.png)

此時將顯示Attribution AI服務頁。 本頁列出了Attribution AI的服務實例，並顯示了相關資訊，包括實例的名稱、轉換事件、實例的運行頻率以及上次更新的狀態。 選擇要開始的服務實例名稱。

>[!NOTE]
>
>只能選擇已完成成功計分運行的服務實例。

![建立例項](./images/insights/select-service-instance.png)

接著，該服務例項的前瞻分析頁面隨即出現，您會在此處獲得視覺化資訊和許多篩選條件，以與資料互動。 本指南將詳細說明視覺化和濾鏡。

![設定頁面](./images/insights/landing-page.png)

### 服務實例詳細資訊

要查看服務實例的其他詳細資訊，請選擇右上角的&#x200B;**[!UICONTROL Show more]**。

![顯示更多](./images/insights/show-more.png)

此時將顯示詳細清單。 有關所列任何屬性的更多資訊，請訪問[Attribution AI使用手冊](./user-guide.md)。

![顯示詳細資訊](./images/insights/advanced-details.png)

### 編輯例項

要編輯實例，請在右上角的導航中選擇&#x200B;**[!UICONTROL Edit]**。
![按一下「編輯」按鈕](./images/insights/edit-button.png)

此時將出現編輯對話框，允許您編輯實例的名稱、說明和計分頻率。 如果實例狀態被禁用，則無法編輯計分頻率。 要確認更改並關閉對話框，請選擇右下角的&#x200B;**[!UICONTROL Save]**。

![編輯跨欄](./images/insights/edit-popover.png)

### 更多操作{#more-actions}

**[!UICONTROL More actions]**&#x200B;按鈕位於&#x200B;**[!UICONTROL Edit]**&#x200B;旁的右上導覽中。 選擇&#x200B;**[!UICONTROL More actions]**&#x200B;會開啟一個下拉菜單，允許您選擇以下操作之一：

- **[!UICONTROL Clone]**:克隆實例。
- **[!UICONTROL Delete]**:刪除實例。
- **[!UICONTROL Download summary data]**:下載包含摘要資料的CSV檔案。
- **[!UICONTROL Access scores]**:選取 **[!UICONTROL Access scores]** 會將您重新導向至 [存取分數，以進行Attribution AI教學](./download-scores.md)。
- **[!UICONTROL View run history]**:此時會出現一個快顯視窗，其中包含與服務例項相關聯的所有計分執行的清單。

![更多動作](./images/insights/more-actions.png)

## 篩選資料

Attribution AI見解可讓您篩選資料，並根據您選取的篩選條件自動更新UI視覺效果。

### 轉換事件

當您在Attribution AI中建立新例項時，其中一個必填欄位是「轉換事件」。 轉換事件是可識別行銷活動（例如電子商務訂單、店內採購和網站造訪）影響的業務目標。

在實例中，**[!UICONTROL Conversion events]**&#x200B;下拉清單允許您選擇為實例定義的任何事件，以便篩選資料。 選取特定事件會變更UI視覺化，僅填入屬於這些事件的轉換。

![轉換事件](./images/insights/conversion-event.png)

### 歸因模型

選擇&#x200B;**[!UICONTROL Attribution Model]**&#x200B;會開啟一個下拉式清單，其中列出所有可用的不同歸因模型。 您可以選取多個模型來比較結果。 有關不同歸因模型及其運作方式的詳細資訊，請造訪[Attribution AI](./overview.md)概觀，其中包含各模型資訊的表格。

![歸因模型](./images/insights/attribution-model.png)

### 地區

>[!NOTE]
>
>只有在建立服務實例時執行了Attribution AI用戶介面指南中的可選步驟[區域型建模](./user-guide.md#region-based-modeling-optional)時，才會出現此篩選器。

此篩選器允許您選擇在實例建立過程中設定的任何區域。

### 新增篩選

您可以選擇&#x200B;**filter**&#x200B;圖示來開啟&#x200B;**[!UICONTROL Add filters]**&#x200B;快顯視窗，以新增其他篩選。 **[!UICONTROL Add filters]**&#x200B;快顯功能可讓您依「頻道」、「地理」、「媒體類型」和「產品」進行篩選。 只有服務實例的適用篩選器會由快顯欄位填入。 例如，如果您未提供地理資料或媒體類型，這些篩選屬性將無法用於您的例項。

![額外的濾鏡](./images/insights/additional-filters.png)

![篩選器快顯](./images/insights/filter-popover.png)

- **[!UICONTROL Channel]：選** 取渠道屬性可讓您篩選任何可用的行銷渠道。您可以選取多個渠道來比較。
- **[!UICONTROL Geography]：選** 擇地理屬性可讓您根據地區模型來篩選國家代碼。根據您的資料，此篩選器可能存在，也可能不存在。 國家／地區代碼有兩個字元長。 請參閱完整的國家／地區代碼清單[這裡](https://datahub.io/core/country-list)。
- **[!UICONTROL Media type]：選** 擇介質類型屬性可讓您過濾任何定義的介質類型。
- **[!UICONTROL Product]：選** 取產品屬性可讓您從建立執行個體時最初收錄的任何產品進行篩選。

### 日期範圍

選取日曆圖示以開啟日期範圍快顯視窗。 開始和結束轉換事件日期會決定在UI中填入的資料量。 您可以選擇縮小或擴大日期範圍，以集中或擴展填入的資料量。

![日期範圍](./images/insights/display-date-range.png)

## 資料概觀

**[!UICONTROL Overview]**&#x200B;卡片會依歸因模型顯示您的總轉換率。 總數會根據您使用本檔案先前概述的篩選器進行搜尋的特定程度而改變。 選取更多模型會將其他社交圈新增至「概述」，每個社交圈都有對應於圖例的色彩。

![概觀](./images/insights/Overview.png)

## 每週趨勢

**[!UICONTROL Weekly trends]**&#x200B;卡片會依您在篩選程式中設定的日期範圍來劃分轉換總數。

選擇&#x200B;**每週趨勢**&#x200B;卡右上角的省略號會顯示下拉式清單，讓您選取每日、每週或每月趨勢。

將滑鼠指標暫留在特定歸因模型的資料行上，會建立一個跨距，顯示該日期的轉換總數。

![趨勢](./images/insights/weekly-trends.png)

## 依頻道劃分

**[!UICONTROL Breakdown by channel]**&#x200B;卡用於確定與每個通道相關的轉換總數。 此資訊卡可協助您決定每個通道的成效和投資報酬率。

選取&#x200B;**[!UICONTROL Breakdown by channel]**&#x200B;卡片右上角的省略號會開啟下拉式清單，讓您根據觸點填入資料。

![劃分渠道](./images/insights/channel-breakdown.png)

## 熱門促銷活動

**[!UICONTROL Top campaigns]**&#x200B;卡片會顯示促銷活動的概述，以及促銷活動在每個頻道中的執行情形。 此資訊卡可協助您的團隊瞭解特定通道特定促銷活動的成效，並提供深入資訊，例如您應進一步投資的促銷活動。

![熱門促銷活動](./images/insights/top-campaigns.png)

## 依觸點位置劃分

選擇&#x200B;**[!UICONTROL Path Analysis]**&#x200B;頁籤會載入&#x200B;**[!UICONTROL Breakdown by touchpoint position]**&#x200B;和&#x200B;**[!UICONTROL Top conversion paths]**&#x200B;圖形。

**[!UICONTROL Breakdown by touchpoint position]**&#x200B;圖表是依觸點位置劃分的歸因轉換，並在所有轉換路徑上進行比較。 此圖表可協助您瞭解哪些觸點在轉換路徑的不同階段更有效。 階段包括入門、玩家和更近的階段。

- **起始點：** 表示接觸點是轉換路徑中的首次接觸。
- **播放器：** 指出接觸點不是導致轉換的首次或上次接觸。
- **詳細說** 明：指出接觸點是轉換前的上次接觸。

>!![NOTE]
所有觸點和位置的歸因模型貢獻百分比之和應等於100。

![使用者路徑劃分觸點](./images/insights/user-paths.png)

## 頂層轉換路徑

**[!UICONTROL Top conversion paths]**&#x200B;圖表顯示所選區域中頂端轉換路徑的受影響和演算法分數。 此圖表可讓您視覺化哪些觸點有助於轉換，以及每個觸點的歸因分數。 您可使用此資訊來檢視特定區域中最頻繁的路徑，並查看不同觸點組之間是否出現任何模式。

![最常見的使用者路徑](./images/insights/Touchpoint-paths.png)

## 觸點效能

選擇&#x200B;**[!UICONTROL Touchpoint Effectiveness]**&#x200B;頁籤會載入&#x200B;**[!UICONTROL Touchpoint effectiveness]**&#x200B;卡。 此卡片使用Attribution AI的資料分發來顯示每個觸點的資訊。 此表格的資料只會在特定時段產生，如卡片右上角的&#x200B;**[!UICONTROL As of]**&#x200B;日期所指示。

![觸點效果選擇](./images/insights/Touchpoint-effectiveness.png)

您可以使用&#x200B;**[!UICONTROL Touchpoint effectiveness]**&#x200B;卡片資訊來瞭解觸點對轉換的貢獻。 您也可以透過下列效能度量，瞭解每個觸點的有效性：

**接觸的路徑**:此度量會顯示達到／未達到接觸點轉換的路徑百分比。如果達到轉換的路徑與未達到轉換的路徑的比例較高，您會看到較高的歸因轉換。

![接觸度量的路徑](./images/insights/Touchpoint-metrics.png)

**效率衡量**:此量度以一到五的比例顯示星形。比例表示觸點對進行轉換的相對重要性。

>[!NOTE]
較高的接觸點體積並不保證較高的效率測量。

**總容量**:使用者觸點被觸碰的總次數。這包括路徑上出現的接觸點，可實現轉換，以及不導致轉換的路徑。

## 後續步驟

在您篩選完資料並能夠顯示適當資訊後，就可以選擇存取分數。 如需如何存取分數的深入指南，請造訪Attribution AI](./download-scores.md)教學課程中的[存取分數。 此外，您也可以下載摘要資料，如[more actions](#more-actions)所示。 選擇「下載摘要資料」會下載依日期匯總的摘要資料。

## 其他資源

以下視訊旨在協助您瞭解如何使用Attribution AI見解頁面來瞭解行銷通道和宣傳的投資報酬率。

>[!VIDEO](https://video.tv.adobe.com/v/32669?learn=on&quality=12)
