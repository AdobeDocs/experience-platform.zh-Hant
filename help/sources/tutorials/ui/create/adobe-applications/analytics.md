---
keywords: Experience Platform；首頁；熱門主題；分析源連接器；分析源；分析
solution: Experience Platform
title: 在UI中建立Adobe Analytics源連接
topic-legacy: overview
type: Tutorial
description: 瞭解如何在UI中建立Adobe Analytics源連接，以將消費者資料帶入Adobe Experience Platform。
exl-id: 5ddbaf63-feaa-44f5-b2f2-2d5ae507f423
source-git-commit: 7bc706751a801a9a673590582cf57872c9c4ae95
workflow-type: tm+mt
source-wordcount: '1571'
ht-degree: 1%

---

# 在UI中建立Adobe Analytics源連接

本教程提供了在UI中建立Adobe Analytics源連接的步驟，以便 [!DNL Analytics] 報告套件資料到Adobe Experience Platform。

## 快速入門

本教程需要對Adobe Experience Platform的以下部分進行有效的理解：

* [體驗資料模型(XDM)系統](../../../../../xdm/home.md):Experience Platform組織客戶體驗資料的標準化框架。
* [即時客戶概要資訊](../../../../../profile/home.md):基於來自多個源的聚合資料提供統一、即時的用戶配置檔案。
* [沙箱](../../../../../sandboxes/home.md):Experience Platform提供虛擬沙箱，將單個平台實例分區為獨立的虛擬環境，以幫助開發和發展數字型驗應用程式。

### 重要術語

瞭解本文檔中使用的以下關鍵術語非常重要：

* **標準屬性**:標準屬性是任何由Adobe預定義的屬性。 它們對所有客戶具有相同的含義，在 [!DNL Analytics] 源資料和 [!DNL Analytics] 架構欄位組。
* **自定義屬性**:自定義屬性是中的自定義變數層次結構中的任何屬性 [!DNL Analytics]。 在Adobe Analytics實施中使用自定義屬性將特定資訊捕獲到報告套件中，這些屬性在使用上與報告套件不同。 自定義屬性包括eVars 、道具和清單。 請參閱以下內容 [[!DNL Analytics] 轉換變數文檔](https://experienceleague.adobe.com/docs/analytics/admin/admin-tools/conversion-variables/conversion-var-admin.html?lang=en) 的雙曲餘切值。
* **自定義欄位組中的任何屬性**:源自客戶建立的欄位組的屬性都是用戶定義的，並且不被視為標準屬性或自定義屬性。
* **友好名稱**:友好名稱是中的自定義變數的人為提供的標籤 [!DNL Analytics] 執行。 請參閱以下內容 [[!DNL Analytics] 轉換變數文檔](https://experienceleague.adobe.com/docs/analytics/admin/admin-tools/conversion-variables/conversion-var-admin.html?lang=en) 的子菜單。

## 建立與Adobe Analytics的源連接

在平台UI中，選擇 **[!UICONTROL 源]** 從左側導航 [!UICONTROL 源] 工作區。 的 [!UICONTROL 目錄] 螢幕顯示可建立帳戶的各種源。

可以從螢幕左側的目錄中選擇相應的類別。 還可以使用搜索欄縮小顯示的源。

在 **[!UICONTROL Adobe應用程式]** 類別，選擇 **[!UICONTROL Adobe Analytics]** ，然後選擇 **[!UICONTROL 添加資料]**。

![目錄](../../../../images/tutorials/create/analytics/catalog.png)

### 選擇資料

的 **[!UICONTROL 分析源添加資料]** 的上界。 選擇 **[!UICONTROL 報表套件]** 開始為分析報表套件資料建立源連接，然後選擇要接收的報表套件。 無法選擇的報表套件已在此沙盒或其他沙盒中攝取。 選擇 **[!UICONTROL 下一個]** 繼續。

>[!NOTE]
>
>可以建立多個綁定連接以引入多個報告套件，但一次只能與Real-time Customer Data Platform一起使用一個報告套件。

![](../../../../images/tutorials/create/analytics/add-data.png)

<!---Analytics Report Suites can be configured for one sandbox at a time. To import the same Report Suite into a different sandbox, the dataset flow will have to be deleted and instantiated again via configuration for a different sandbox.--->

### 映射

>[!IMPORTANT]
>
>用於 [!DNL Analytics] 源為beta。

在映射之前 [!DNL Analytics] 資料到目標XDM架構，必須首先選擇是使用預設架構還是使用自定義架構。

預設架構代表您建立新架構，包含 [!DNL Analytics] 欄位組。 要使用預設架構，請選擇 **[!UICONTROL 預設架構]**。

![預設模式](../../../../images/tutorials/create/analytics/default-schema.png)

使用自定義架構，您可以為 [!DNL Analytics] 資料，只要架構 [!DNL Analytics] 欄位組。 要使用自定義架構，請選擇 **[!UICONTROL 自定義架構]**。

![自定義模式](../../../../images/tutorials/create/analytics/custom-schema.png)

的 [!UICONTROL 映射] 頁提供了將源欄位映射到相應目標模式欄位的介面。 在此處，您可以將自定義變數映射到新架構欄位組，並應用資料準備支援的計算。 選擇目標方案以啟動映射進程。

>[!TIP]
>
>僅具有 [!DNL Analytics] 模板欄位組顯示在模式選擇菜單中。 省略其他架構。 如果報表套件資料沒有適當的架構，則必須建立新架構。 有關建立架構的詳細步驟，請參見上的指南 [在UI中建立和編輯架構](../../../../../xdm/ui/resources/schemas.md)。

![選擇模式](../../../../images/tutorials/create/analytics/select-schema.png)

的 [!UICONTROL 映射標準欄位] 剖面顯示面板 [!UICONTROL 已應用標準映射]。 [!UICONTROL 非匹配標準映射] 和 [!UICONTROL 自定義映射]。 有關每個類別的特定資訊，請參閱下表：

| 映射標準欄位 | 說明 |
| --- | --- |
| [!UICONTROL 已應用標準映射] | 的 [!UICONTROL 已應用標準映射] 面板顯示映射屬性的總數。 標準映射指源中所有屬性之間的映射集 [!DNL Analytics] 資料和相應屬性 [!DNL Analytics] 欄位組。 這些是預映射的，無法編輯。 |
| [!UICONTROL 非匹配標準映射] | 的 [!UICONTROL 非匹配標準映射] 面板是指包含友好名稱衝突的映射屬性數。 當您重新使用已從其他報告套件中填充了一組欄位描述符的架構時，會出現這些衝突。 您可以繼續 [!DNL Analytics] 即使存在友好名稱衝突的資料流。 |
| [!UICONTROL 自定義映射] | 的 [!UICONTROL 自定義映射] 面板顯示映射的自定義屬性（包括eVars、props和list）的數量。 自定義映射引用源中自定義屬性之間的映射集 [!DNL Analytics] 所選架構中包含的自定義欄位組中的資料和屬性。 |

![映射標準域](../../../../images/tutorials/create/analytics/map-standard-fields.png)

預覽 [!DNL Analytics] ExperienceEvent模板架構欄位組，選擇 **[!UICONTROL 視圖]** 的 [!UICONTROL 已應用標準映射] 的子菜單。

![檢視](../../../../images/tutorials/create/analytics/view.png)

的 [!UICONTROL Adobe AnalyticsExperienceEvent模板架構欄位組] 頁為您提供了用於檢查架構結構的介面。 完成後，選擇 **[!UICONTROL 關閉]**。

![欄位組預覽](../../../../images/tutorials/create/analytics/field-group-preview.png)

平台自動檢測映射集中是否存在任何友好名稱衝突。 如果映射集沒有衝突，請選擇 **[!UICONTROL 下一個]** 繼續。

![映射](../../../../images/tutorials/create/analytics/mapping.png)

如果源報告套件和所選架構之間存在友好名稱衝突，您仍可以繼續 [!DNL Analytics] 資料流，確認欄位描述符不會更改。 或者，可以選擇使用一組空描述符建立新架構。

選擇 **[!UICONTROL 下一個]** 繼續。

![謹慎](../../../../images/tutorials/create/analytics/caution.png)

#### 自定義映射

要使用「資料準備」功能並為自定義屬性添加新的映射或計算欄位，請選擇 **[!UICONTROL 查看自定義映射]**。

![視圖自定義映射](../../../../images/tutorials/create/analytics/view-custom-mapping.png)

下一步，選擇 **[!UICONTROL 添加新映射]**。

根據您的需要，您可以選擇 **[!UICONTROL 添加新映射]** 或 **[!UICONTROL 添加計算欄位]** 的子菜單。

![新增映射](../../../../images/tutorials/create/analytics/add-new-mapping.png)

出現空映射集。 選擇映射表徵圖以添加源欄位。

![選擇源欄位](../../../../images/tutorials/create/analytics/select-source-field.png)

您可以使用介面瀏覽源架構結構並標識要使用的新源欄位。 選擇要映射的源欄位後，選擇 **[!UICONTROL 選擇]**。

![選擇映射](../../../../images/tutorials/create/analytics/select-mapping.png)

接下來，選擇下面的映射表徵圖 [!UICONTROL 目標欄位] 將所選源欄位映射到其相應的目標欄位。

![選擇目標域](../../../../images/tutorials/create/analytics/select-target-field.png)

與源架構類似，您可以使用介面在目標架構結構中導航並選擇要映射到的目標欄位。 選擇相應的目標欄位後，選擇 **[!UICONTROL 選擇]**。

![選擇目標映射](../../../../images/tutorials/create/analytics/select-target-mapping.png)

完成自定義映射集後，選擇 **[!UICONTROL 下一個]** 繼續。

![完整自定義映射](../../../../images/tutorials/create/analytics/complete-custom-mapping.png)

以下文檔提供了更多資源，用於瞭解資料準備、計算欄位和映射功能：

* [資料準備概述](../../../../../data-prep/home.md)
* [資料準備映射函式](../../../../../data-prep/functions.md)
* [添加計算欄位](../../../../../data-prep/ui/mapping.md#calculated-fields)

### 提供資料流詳細資訊

的 **[!UICONTROL 資料流詳細資訊]** 步驟，您必須在其中為資料流提供名稱和可選說明。 選擇 **[!UICONTROL 下一個]** 的子菜單。

![資料流詳細資訊](../../../../images/tutorials/create/analytics/dataflow-detail.png)

### 審閱

的 [!UICONTROL 審閱] 步驟，允許您在建立新的分析資料流之前查看它。 連接的詳細資訊按類別分組，包括：

* [!UICONTROL 連接]:顯示連接的源平台。
* [!UICONTROL 資料類型]:顯示所選報表套件及其相應的報表套件ID。

![審查](../../../../images/tutorials/create/analytics/review.png)

### 監視資料流

建立資料流後，您可以監視通過它接收的資料。 從 [!UICONTROL 目錄] 螢幕，選擇 **[!UICONTROL 資料流]** 查看與分析帳戶關聯的已建立流的清單。

![選擇資料流](../../../../images/tutorials/create/analytics/select-dataflows.png)

的 **資料流** 的上界。 此頁上是一對資料集流，包括有關其名稱、源資料、建立時間和狀態的資訊。

連接器實例化兩個資料集流。 一個流表示回填資料，另一個流表示即時資料。 回填資料未配置為Profile，但會發送到資料湖以用於分析和資料科學使用案例。

有關回填、即時資料及其各自延遲的詳細資訊，請參見 [分析資料連接器概述](../../../../connectors/adobe-applications/analytics.md)。

從清單中選擇要查看的資料集流。

![選擇 — 目標 — 資料集](../../../../images/tutorials/create/analytics/select-target-dataset.png)

的 **[!UICONTROL 資料集活動]** 的子菜單。 此頁顯示以圖形形式使用的消息的速率。 選擇 **[!UICONTROL 資料治理]** 的子菜單。

![資料集活動](../../../../images/tutorials/create/analytics/dataset-activity.png)

您可以從 [!UICONTROL 資料治理] 的上界。 有關如何標籤來自分析的資料的詳細資訊，請訪問 [資料使用標籤指南](../../../../../data-governance/labels/user-guide.md)。

![資料 — gov](../../../../images/tutorials/create/analytics/data-gov.png)

要刪除資料流，請轉至 [!UICONTROL 資料流] 頁面，然後選擇橢圓(`...`)旁邊，然後選擇 [!UICONTROL 刪除]。

![刪除](../../../../images/tutorials/create/analytics/delete.png)

## 後續步驟和其他資源

建立連接後，將自動建立資料流，以包含傳入資料並使用所選模式填充資料集。 此外，還會進行資料回填，以及內嵌長達 13 個月的歷史資料。初始攝取完成後， [!DNL Analytics] 資料和供下游平台服務使用，例如 [!DNL Real-time Customer Profile] 和分段服務。 有關詳細資訊，請參閱以下文檔：

* [[!DNL Real-time Customer Profile] 概觀](../../../../../profile/home.md)
* [[!DNL Segmentation Service] 概觀](../../../../../segmentation/home.md)
* [[!DNL Data Science Workspace] 概觀](../../../../../data-science-workspace/home.md)
* [[!DNL Query Service] 概觀](../../../../../query-service/home.md)

以下視頻旨在支援您對使用Adobe Analytics源連接器接收資料的理解：

>[!WARNING]
>
> 的 [!DNL Platform] 以下視頻中顯示的UI已過期。 有關最新的UI螢幕截圖和功能，請參閱上面的文檔。

>[!VIDEO](https://video.tv.adobe.com/v/29687?quality=12&learn=on)
