---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: 在UI中建立Adobe Analytics來源連接器
topic: overview
translation-type: tm+mt
source-git-commit: 3f1c3c77a0755a3e305da0fb8a234be0f0ee1863
workflow-type: tm+mt
source-wordcount: '769'
ht-degree: 1%

---


# 在UI中建立Adobe Analytics來源連接器

本教學課程提供在UI中建立Adobe Analytics來源連接器以將消費者資料匯入Adobe Experience Platform的步驟。

## 快速入門

本教學課程需要對Adobe Experience Platform的下列元件有正確的認識：

* [體驗資料模型(XDM)系統](../../../../../xdm/home.md): Experience Platform組織客戶體驗資料的標準化架構。
* [即時客戶個人檔案](../../../../../profile/home.md): 根據來自多個來源的匯整資料，提供統一、即時的消費者個人檔案。
* [沙盒](../../../../../sandboxes/home.md): Experience Platform提供虛擬沙盒，可將單一Platform實例分割為不同的虛擬環境，以協助開發和發展數位體驗應用程式。

## 使用Adobe Analytics建立來源連線

登入 <a href="https://platform.adobe.com" target="_blank">Adobe Experience Platform</a> ，然後從左側導覽列選 **[!UICONTROL 取Sources]** ，以存取來源工作區。 「目 *錄* 」螢幕顯示可用的源以建立入站連接，每個源顯示與其關聯的現有帳戶和資料集流的數量。

您可以從畫面左側的目錄中選取適當的類別。 或者，您也可以使用搜尋選項找到您要使用的特定來源。

在「 *Adobe應用程式* 」類別下，選取「 **[!UICONTROL Adobe Analytics]** 」以在螢幕右側顯示資訊列。 資訊列提供所選來源的簡短說明，以及與來源連線或檢視其檔案的選項。 要查看現有帳戶，請選擇 **[!UICONTROL 帳戶]**。

![](../../../../images/tutorials/create/analytics/catalog.png)

### 選擇資料

此時 *會顯示Adobe Analytics* 步驟。 此螢幕上會列出先前建立的Analytics資料集流程。 您可以按一下「選取資料」，建立新的資 **[!UICONTROL 料集流程]**。

>[!NOTE]
>
>可以建立多個源的綁定內連接以引入不同的資料。

![](../../../../images/tutorials/create/analytics/dataset-flows.png)

<!---Analytics report suites can be configured for one sandbox at a time. To import the same report suite into a different sandbox, the dataset flow will have to be deleted and instantiated again via configuration for a different sandbox.--->

從可用報表套裝清單中，選取您要匯入「平台」的報表套裝，然後按一下「下 **[!UICONTROL 一步]**」。

![](../../../../images/tutorials/create/analytics/select-data.png)

### 命名資料集流程

此時 *會顯示資料集流程詳細資料* ，您必須在其中提供資料集流程的名稱和選用說明。 選擇 **[UICONTROL! 完成時]** ，下一個。

![](../../../../images/tutorials/create/analytics/dataset-flow-detail.png)

### 檢閱資料集流程

此時 *會顯示* 「檢閱」步驟，讓您在建立新的Analytics內嵌資料集流程之前，先加以檢閱。 連接的詳細資訊按類別分組，包括：

* *連接*: 顯示來源連線和所選報表套裝的類型。
* *指派資料集與地圖欄位*: 建立其他來源連接器時，此容器會顯示來源資料所吸收的資料集，包括資料集所遵守的架構。 輸出結構描述和資料集會自動設定為Analytics資料集流程。

![](../../../../images/tutorials/create/analytics/review.png)

### 監控資料集流程

建立資料集流程後，您就可以監控透過它擷取的資料。 從「目 *錄* 」畫面中，選取「資 *料集流」* ，以檢視與您的Analytics帳戶相關的已建立流清單。

![](../../../../images/tutorials/create/analytics/catalog-dataset-flows.png)

出現 *資料集流* 畫面。 此頁面上是一對資料集流，包括其名稱、來源資料、建立時間和狀態的資訊。

連接器實例化兩個資料集流。 一個流代表回填資料，另一個流代表即時資料。 回填資料未設定為描述檔，但會傳送至資料湖，以用於分析和資料科學使用案例。

如需回填、即時資料及其各自延遲的詳細資訊，請參閱 [Analytics資料連接器概觀](../../../../connectors/adobe-applications/analytics.md)。

從清單中選取您要檢視的資料集流程。

![](../../../../images/tutorials/create/analytics/backfill.png)

此時將 *顯示「資料集* 」活動頁。 此頁面以圖形形式顯示消費訊息的比率。 從上 *方標題選取* 「資料控管」，以存取標籤欄位。

![](../../../../images/tutorials/create/analytics/batches.png)

您可以從「資料控管」畫面中檢視資料集流程的繼 *承標籤* 。 若要存取特定標籤，請選取右上角的編輯按鈕。

![](../../../../images/tutorials/create/analytics/data-gov.png)

此時將 *顯示「編輯控管標籤* 」面板。 此螢幕可讓您存取和編輯資料集流程的合約、身分和敏感標籤。

如需如何為來自Analytics的資料加上標籤的詳細資訊，請造訪資 [料使用標籤指南](../../../../../data-governance/labels/user-guide.md)。

![](../../../../images/tutorials/create/analytics/labels.png)

## 後續步驟和其他資源

建立連線後，會自動建立目標模式和資料集流程，以包含傳入的資料。 此外，還會進行資料回填，以及內嵌長達 13 個月的歷史資料。當初始擷取完成時，Analytics資料並供下游平台服務（例如即時客戶個人檔案和細分服務）使用。 如需詳細資訊，請參閱下列檔案：

* [即時客戶個人檔案總覽](../../../../../profile/home.md)
* [區段服務概觀](../../../../../segmentation/home.md)
* [資料科學工作區概觀](../../../../../data-science-workspace/home.md)
* [查詢服務概述](../../../../../query-service/home.md)

以下視訊旨在支援您對使用Adobe Analytics Source連接器擷取資料的瞭解：

>[!WARNING]
>
> 下 [!DNL Platform] 列視訊中顯示的UI已過時。 請參閱上述檔案以取得最新的UI螢幕擷取和功能。

>[!VIDEO](https://video.tv.adobe.com/v/29687?quality=12&learn=on)

