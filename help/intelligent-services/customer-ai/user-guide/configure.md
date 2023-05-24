---
keywords: Experience Platform；使用手冊；客戶；熱門主題；配置實例；建立實例；
solution: Experience Platform, Real-time Customer Data Platform
feature: Customer AI
title: 配置客戶AI實例
description: AI/ML服務將客戶AI作為一種易於使用的Adobe Sensei服務提供，可針對不同的使用情形進行配置。 以下各節提供了配置客戶AI實例的步驟。
exl-id: 78353dab-ccb5-4692-81f6-3fb3f6eca886
source-git-commit: 3bc750b5e1cf47cbca6b037d099936c80c926cf8
workflow-type: tm+mt
source-wordcount: '2828'
ht-degree: 0%

---


# 配置客戶AI實例

客戶AI作為AI/ML服務的一部分，使您能夠生成自定義傾向分數，而不必擔心機器學習。

AI/ML服務將客戶AI作為一種易於使用的Adobe Sensei服務提供，可針對不同的使用情形進行配置。 以下各節提供了配置客戶AI實例的步驟。

## 建立實例 {#set-up-your-instance}

在平台UI中，選擇 **[!UICONTROL 服務]** 的子菜單。 的 **[!UICONTROL 服務]** 瀏覽器顯示並顯示您可以使用的所有可用服務。 在客戶AI的容器中，選擇 **[!UICONTROL 開啟]**。

![](../images/user-guide/navigate-to-service.png)

的 **客戶AI** UI顯示並顯示您的所有服務實例。

- 您可以找到 **[!UICONTROL 已分配配置檔案總數]** 位於 **[!UICONTROL 建立實例]** 容器。 此度量跟蹤客戶AI在當前日曆年（包括所有沙盒環境和任何已刪除的服務實例）評分的配置檔案總數。

![](../images/user-guide/total-profiles.png)

可以使用UI右側的控制項編輯、克隆和刪除服務實例。 要顯示這些控制項，請從現有控制項中選擇一個實例 **[!UICONTROL 服務實例]**。 控制項包含以下內容：

- **[!UICONTROL 編輯]**:選擇 **[!UICONTROL 編輯]** 允許您修改現有服務實例。 您可以編輯實例的名稱、說明和記分頻率。
- **[!UICONTROL 克隆]**:選擇 **[!UICONTROL 克隆]** 複製當前選定的服務實例安裝程式。 然後，您可以修改工作流以進行小微調整，並將其更名為新實例。
- **[!UICONTROL 刪除]**:您可以刪除包含任何歷史運行的服務實例。 將從平台中刪除相應的輸出資料集。 但是，與Real-Time Customer Profile同步的分數不會刪除。
- **[!UICONTROL 資料源]**:此實例使用的資料集的連結。 如果正在使用多個資料集，則選擇超連結文本將開啟資料集預覽跨距。
- **[!UICONTROL 上次運行詳細資訊]**:僅當運行失敗時才顯示此資訊。 此處顯示運行失敗原因的資訊，如錯誤代碼。
- **[!UICONTROL 分數定義]**:您為此實例配置的目標的快速概述。

![](../images/user-guide/service-instance-panel.png)

要建立新實例，請選擇 **[!UICONTROL 建立實例]**。

![](../images/user-guide/dashboard.png)

## 設定

將顯示實例建立工作流，從 **[!UICONTROL 設定]** 的子菜單。

以下是有關必須向實例提供的值的重要資訊：

- **[!UICONTROL 名稱]:** 在顯示客戶AI分數的所有位置都使用實例的名稱。 因此，名稱應描述預測分值代表什麼。 例如，「取消雜誌訂閱的可能性」。

- **[!UICONTROL 說明]:** 說明您嘗試預測的內容。

- **[!UICONTROL 傾向類型]:** 傾向類型確定分數的意圖和度量極性。 您可以選擇 **[!UICONTROL 衝]** 或 **[!UICONTROL 轉換]**。 請參閱下面的注釋 [評分摘要](./discover-insights.md#scoring-summary) 的子常式。

![設定螢幕](../images/user-guide/create-instance.png)

提供所需值，然後選擇 **[!UICONTROL 下一個]** 繼續。

## 選擇資料 {#select-data}

按照設計，客戶AI使用Adobe Analytics、Adobe Audience Manager、總體體驗事件和消費者體驗事件資料來計算傾向得分。 選擇資料集時，只列出與客戶AI相容的資料集。 要選擇資料集，請選擇&#x200B;**+**)資料集名稱旁邊的符號，或選中複選框以一次添加多個資料集。 使用搜索選項可快速查找您感興趣的資料集。

![選擇並搜索資料集](../images/user-guide/configure-dataset-page-save-and-exit-cai.png)

選擇要使用的資料集後，選擇 **[!UICONTROL 添加]** 按鈕，將資料集添加到資料集預覽窗格。

![選擇資料集](../images/user-guide/select-datasets.png)

選擇資訊表徵圖 ![資訊表徵圖](../images/user-guide/info-icon.png) 資料集旁邊開啟資料集預覽跨距。

![選擇並搜索資料集](../images/user-guide/dataset-info.png)

資料集預覽包含資料，如上次更新時間、源架構和前十列的預覽。

選擇 **[!UICONTROL 保存]** 在工作流中移動時保存草稿。 也可以保存草稿模型配置並移動到工作流的下一步。 使用 **[!UICONTROL 保存並繼續]** 在模型配置期間建立和保存草稿。 該特徵使您能夠建立和保存模型配置的草稿，在必須定義配置工作流中的許多欄位時，該特徵尤其有用。

![Data Science Services客戶AI頁籤的「建立」工作流，其中「保存」和「保存」並繼續突出顯示。](../images/user-guide/cai-save-and-exit.png)

### 資料集完整性 {#dataset-completeness}

資料集預覽中存在資料集完整性百分比值。 此值提供了資料集中有多少列為空/空的快速快照。 如果資料集包含大量缺失值，並且這些值在其他位置被捕獲，強烈建議您包括包含缺失值的資料集。 在此示例中，人員ID為空，但是，在可以包括的單獨資料集中捕獲人員ID。

>[!NOTE]
>
>使用客戶AI的最大培訓窗口（一年）計算資料集完整性。 這意味著在顯示資料集完整性值時，不會考慮超過一年的資料。

![資料集完整性](../images/user-guide/dataset-info-2.png)

### 選擇標識 {#identity}

現在，您可以基於標識映射（欄位）將多個資料集聯接到彼此。 必須選擇標識類型（也稱為「標識命名空間」）和該命名空間中的標識值。 如果在同一命名空間下將多個欄位指定為架構中的標識，則所有分配的標識值都會出現在由命名空間優先的標識下拉清單中，如 `EMAIL (personalEmail.address)` 或 `EMAIL (workEmail.address)`。

[選擇相同命名空間](../images/user-guide/cai-identity-map.png)

>[!IMPORTANT]
>
>必須對您選擇的每個資料集使用相同的標識類型（命名空間）。 標識列中標識類型旁邊出現綠色複選標籤，表示資料集相容。 例如，當使用Phone命名空間和 `mobilePhone.number` 作為標識符，其餘資料集的所有標識符必須包含並使用Phone命名空間。

要選擇標識，請選擇標識列中帶下划線的值。 將出現選擇標識跨距。

<!-- ![select same namespace](../images/user-guide/identity-type.png) -->
[選擇相同命名空間](../images/user-guide/cai-identity-namespace.png)

如果命名空間中有多個標識可用，請確保為使用案例選擇正確的標識欄位。 例如，電子郵件命名空間中有兩個電子郵件標識，一個是工作電子郵件，另一個是個人電子郵件。 根據使用案例，個人電子郵件更可能被填入，在個人預測中也更有用。 這意味著 `EMAIL (personalEmail.address)` 將被選作身份。

![未選擇資料集密鑰](../images/user-guide/select-identity.png)

>[!NOTE]
>
> 如果資料集不存在有效的標識類型（命名空間），則必須設定主標識並使用 [架構編輯器](../../../xdm/schema/composition.md#identity)。 要瞭解有關命名空間和標識的詳細資訊，請訪問 [標識服務命名空間](../../../identity-service/namespaces.md) 文檔。

## 定義目標 {#define-a-goal}

<!-- https://www.adobe.com/go/cai-define-a-goal -->

的 **[!UICONTROL 定義目標]** 步驟顯示，它提供了互動式環境，供您直觀地定義預測目標。 目標由一個或多個事件組成，其中每個事件的發生基於它所保持的條件。 客戶AI實例的目標是確定在給定時間範圍內實現其目標的可能性。

要建立目標，請選擇 **[!UICONTROL 輸入欄位名稱]** 後跟下拉清單中的欄位。 選擇第二個輸入，即事件條件的子句，然後根據需要提供目標值以完成事件。 可以通過選擇 **[!UICONTROL 添加事件]**。 最後，通過應用預測時間框（天數）來完成目標，然後選擇 **[!UICONTROL 下一個]**。

<!-- ![](../images/user-guide/define-a-goal.png) -->
![](../images/user-guide/cai-define-a-goal.png)

### 將發生且不會發生

在定義目標時，您可以選擇 **[!UICONTROL 將發生]** 或 **[!UICONTROL 不會發生]**。 選擇 **[!UICONTROL 將發生]** 表示需要滿足您定義的事件條件，才能將客戶的事件資料包含在洞察UI中。

例如，如果您想設定應用以預測客戶是否會購買產品，則可以選擇 **[!UICONTROL 將發生]** 後跟 **[!UICONTROL 全部]** 然後輸入 **commerce.purches.id** （或類似欄位） **[!UICONTROL 存在]** 作為運算子。

<!-- ![will occur](../images/user-guide/occur.png) -->
![會發生](../images/user-guide/cai-will-occur.png)

但是，有時您對預測某個事件是否在特定時間範圍內不會發生感興趣。 要使用此選項配置目標，請選擇 **[!UICONTROL 不會發生]** 從頂級下拉清單中。

例如，如果您有興趣預測哪些客戶變得不那麼敬業，則不要在下個月訪問您的帳戶登錄頁。 選擇 **[!UICONTROL 不會發生]** 後跟 **[!UICONTROL 全部]** 然後輸入 **web.webInteraction.URL** （或類似欄位） **[!UICONTROL 等於]** 作為 **帳戶登錄** 值。

![不會發生](../images/user-guide/not-occur.png)

### 所有和任何

在某些情況下，您可能希望預測事件組合是否會發生，而在其它情況下，您可能希望預測預定義集中任何事件的發生。 為了預測客戶是否具有事件組合，請選擇 **[!UICONTROL 全部]** 選項 **[!UICONTROL 定義目標]** 的子菜單。

例如，您可能希望預測客戶是否購買了特定產品。 該預測目標由兩個條件定義：a `commerce.order.purchaseID` **存在** 和 `productListItems.SKU` **等於** 一些特定的價值。

![所有示例](../images/user-guide/all-of.png)

為了預測客戶是否會從給定集中發生任何事件，您可以使用 **[!UICONTROL 任意]** 的雙曲餘切值。

例如，您可能希望預測客戶是訪問特定URL還是訪問具有特定名稱的網頁。 該預測目標由兩個條件定義： `web.webPageDetails.URL` **開頭** 特定值 `web.webPageDetails.name` **開頭** 一個特定值。

![任何示例](../images/user-guide/any-of.png)

### 合格人口 *（可選）*

預設情況下，將為所有配置檔案生成傾向分數，除非指定合格人口。 您可以通過定義條件來基於事件包括或排除配置檔案來指定合格人口。

![合格人口](../images/user-guide/eligible-population.png)

### 自定義事件(*可選*) {#custom-events}

如果除了 [標準事件欄位](../data-requirements.md#standard-events) 由客戶AI用於生成傾向得分，提供自定義事件選項。 使用此選項可以添加您認為具有影響力的其他事件，這些事件可能會提高模型的質量並有助於提供更準確的結果。 如果您選擇的資料集包含在架構中定義的自定義事件，則可以將它們添加到實例中。

>[!NOTE]
>
> 有關自定義事件如何影響客戶AI評分結果的深入說明，請訪問 [自定義事件示例](#custom-event) 的子菜單。

![事件特徵](../images/user-guide/event-feature.png)

要添加自定義事件，請選擇 **[!UICONTROL 添加自定義事件]**。 接下來，輸入自定義事件名稱，然後將其映射到架構中的事件欄位。 在查看影響因素和其他見解時，將顯示自定義事件名稱以代替欄位值。 這意味著將使用自定義事件名稱，而不是事件的ID/值。 有關如何顯示自定義事件的詳細資訊，請參閱 [自定義事件示例部分](#custom-event)。 客戶AI使用這些附加的自定義事件來改進模型質量並提供更準確的結果。

![自定義事件欄位](../images/user-guide/custom-event.png)

接下來，從可用運算子下拉清單中選擇要使用的運算子。 只列出與事件相容的運算子。

![自定義事件運算子](../images/user-guide/custom-operator.png)

最後，如果所選運算子需要一個欄位值，請輸入欄位值。 在此示例中，我們只需要查看是否存在酒店或餐廳預訂。 但是，如果我們想更精確，可以使用equals運算子並在value提示符中輸入一個精確值。

![自定義事件欄位值](../images/user-guide/custom-value.png)

完成後，選擇 **[!UICONTROL 下一個]** 在右上角繼續。

### 自定義配置檔案屬性(*可選*)

除了 [標準事件欄位](../data-requirements.md#standard-events) 由客戶AI生成傾向得分。 使用此選項可以添加您認為具有影響力的附加配置檔案屬性，這些屬性可能會提高模型的質量並提供更準確的結果。 此外，添加自定義配置檔案屬性使客戶AI能夠更好地展示特定配置檔案如何最終出現在傾向桶中。

>[!NOTE]
>
>添加自定義配置檔案屬性與添加自定義事件遵循的工作流相同。 與自定義事件類似，自定義配置檔案屬性也以同樣方式影響模型評分。 有關詳細解釋，請訪問 [自定義事件示例](#custom-event) 的子菜單。

![添加自定義配置檔案屬性](../images/user-guide/profile-attributes.png)

#### 從配置檔案快照導出中選擇配置檔案屬性

您也可以選擇在每日配置檔案快照導出中包括配置檔案屬性。 這些屬性將同步到配置檔案快照導出並顯示最近可用的值。

>[!WARNING]
>
> 請小心不要選擇作為預測目標的結果更新或與預測目標高度相關的配置檔案屬性。 這導致模型資料洩漏和過擬合。 此類屬性的示例是 `total_purchases_in_the_last_3_months` 預測採購轉換。

>[!NOTE]
>
>在UI中，UPS快照導出支援使用配置檔案屬性，請求。

### 添加自定義事件示例 {#custom-event}

在以下示例中，將自定義事件和配置檔案屬性添加到客戶AI實例。 客戶AI實例的目標是預測客戶在未來60天內購買另一個Luma產品的可能性。 通常，產品資料連結到產品SKU。 在這種情況下，SKU `prd1013`。 在客戶AI模型經過培訓/打分後，此SKU可以連結到事件，並作為傾向時段的一個影響因素顯示。

客戶AI自動將功能生成（如「天數自」或「計數」）應用於自定義事件，如 **手錶購買**。 如果將此事件視為客戶傾向高、中或低的一個影響因素，則客戶AI將其顯示為 `Days since prd1013 purchase` 或 `Count of prd1013 purchase`。 通過將其建立為「自定義」事件，可以為該事件指定一個新名稱，使結果更容易讀取。 例如 `Days since Watch purchase`。此外，即使該事件不是標準事件，客戶AI也會在其培訓和評分中使用此事件。 這意味著您可以添加您認為可能有影響的多個事件，並通過包括保留、訪問者日誌等資料來進一步定制模型。 添加這些資料點會進一步提高客戶AI模型的準確性和精度。

![自定義事件示例](../images/user-guide/custom-event-name.png)

## 設定選項

設定選項步驟允許您配置計畫以自動執行預測運行、定義預測排除以過濾某些事件，以及切換 **[!UICONTROL 配置檔案]** 開/關。

### 配置計畫 *（可選）* {#configure-a-schedule}

要設定計分計畫，請首先配置 **[!UICONTROL 評分頻率]**。 自動預測運行可以計畫每週或每月運行。

![](../images/user-guide/schedule.png)

### 預測排除 *（可選）*

如果資料集包含作為test資料添加的任何列，則可以通過選擇將該列或事件添加到排除清單中 **[!UICONTROL 添加排除]** 然後輸入要排除的欄位。 這防止在生成分數時評估滿足特定條件的事件。 此功能可用於過濾無關資料輸入或促銷。

要排除事件，請選擇 **[!UICONTROL 添加排除]** 定義事件。 要刪除排除，請選取橢圓(**[!UICONTROL ...]**)，然後選擇 **[!UICONTROL 刪除容器]**。

![](../images/user-guide/exclusion.png)

### 配置檔案切換

配置檔案切換允許客戶AI將評分結果導出到即時客戶配置檔案。 禁用此切換可防止將模型評分結果添加到「配置檔案」中。 禁用此功能後，客戶AI評分結果仍然可用。

首次使用「客戶AI」時，可以關閉此特徵，直到您對模型輸出結果滿意為止。 這樣，您就無法在微調模型時將多個評分資料集上載到客戶配置檔案。 校準模型後，可以使用 [克隆選項](#set-up-your-instance) 從 **服務實例** 的子菜單。 這允許您建立模型副本並開啟配置檔案。

![配置檔案切換](../images/user-guide/advanced-workflow-save.png)

一旦設定了評分計畫、包括了預測排除，並且配置檔案切換到您希望的位置，請選擇 **[!UICONTROL 完成]** 在右上角建立您的客戶AI實例。

如果實例建立成功，則會立即觸發預測運行，然後根據您定義的計畫執行後續運行。

>[!NOTE]
>
>根據輸入資料的大小，預測運行可能需要24小時才能完成。

按照本節所述，您配置了客戶AI的實例並執行了預測運行。 在運行成功完成後，如果啟用了配置檔案切換，則得分的洞察會自動用預測得分填充配置檔案。 請等待最多24小時，然後繼續本教程的下一部分。

## 後續步驟 {#next-steps}

通過本教程，您已成功配置了客戶AI實例並生成了傾向得分。 現在，您可以選擇使用段生成器 [建立預測分數的客戶段](./create-segment.md) 或 [瞭解客戶AI的見解](./discover-insights.md)。

## 其他資源

以下視頻旨在支援您對客戶AI的配置工作流的理解。 此外，還提供了最佳做法和使用案例示例。

>[!IMPORTANT]
>
> 以下視頻已過期。 有關最新資訊，請參閱文檔。

>[!VIDEO](https://video.tv.adobe.com/v/32665?learn=on&quality=12)
