---
keywords: Experience Platform；首頁；熱門主題；Analytics來源連接器；Analytics連接器；Analytics來源；Analytics
solution: Experience Platform
title: 在UI中建立Adobe Analytics來源連線
topic-legacy: overview
type: Tutorial
description: 了解如何在UI中建立Adobe Analytics來源連線，將消費者資料匯入Adobe Experience Platform。
exl-id: 5ddbaf63-feaa-44f5-b2f2-2d5ae507f423
source-git-commit: 952b2caa6983b331c046618aff255131a6480e67
workflow-type: tm+mt
source-wordcount: '1450'
ht-degree: 1%

---

# 在UI中建立Adobe Analytics來源連線

本教學課程提供在UI中建立Adobe Analytics來源連線，以將[!DNL Analytics]報表套裝資料匯入Adobe Experience Platform的步驟。

## 快速入門

本教學課程需要妥善了解下列Adobe Experience Platform元件：

* [Experience Data Model(XDM)系統](../../../../../xdm/home.md):Experience Platform組織客戶體驗資料的標準化架構。
* [即時客戶個人檔案](../../../../../profile/home.md):根據來自多個來源的匯總資料，提供統一的即時消費者設定檔。
* [沙箱](../../../../../sandboxes/home.md):Experience Platform提供可將單一Platform執行個體分割成個別虛擬環境的虛擬沙箱，以協助開發及改進數位體驗應用程式。

### 重要術語

請務必了解本檔案中使用的下列主要術語：

* **標準屬性**:標準屬性是Adobe預先定義的任何屬性。它們對所有客戶都包含相同的含義，可在[!DNL Analytics]源資料和[!DNL Analytics]架構欄位組中使用。
* **自訂屬性**:自訂屬性是中自訂維度階層中的任何 [!DNL Analytics]屬性。它們也屬於Adobe定義的結構，但可由不同客戶以不同方式加以解譯。 自訂屬性包括eVar、prop和清單。 如需eVar的詳細資訊，請參閱以下轉換變數的[[!DNL Analytics] 檔案](https://experienceleague.adobe.com/docs/analytics/admin/admin-tools/conversion-variables/conversion-var-admin.html?lang=en)。
* **自訂欄位群組中的任何屬性**:源自客戶建立的欄位群組的屬性皆為使用者定義，不視為標準或自訂屬性。
* **易記名稱**:好記名稱是人為提供的標籤，用於實作中的自訂 [!DNL Analytics] 變數。如需好記名稱的詳細資訊，請參閱以下轉換變數](https://experienceleague.adobe.com/docs/analytics/admin/admin-tools/conversion-variables/conversion-var-admin.html?lang=en)的相關檔案。[[!DNL Analytics] 

## 使用Adobe Analytics建立來源連線

在平台UI中，從左側導覽中選取&#x200B;**[!UICONTROL Sources]**&#x200B;以存取[!UICONTROL Sources]工作區。 [!UICONTROL 目錄]畫面會顯示您可以用來建立帳戶的各種來源。

您可以從畫面左側的目錄中選取適當的類別。 您也可以使用搜尋列來縮小顯示的來源。

在&#x200B;**[!UICONTROL Adobe應用程式]**&#x200B;類別下，選擇&#x200B;**[!UICONTROL Adobe Analytics]**，然後選擇&#x200B;**[!UICONTROL 添加資料]**。

![目錄](../../../../images/tutorials/create/analytics/catalog.png)

### 選擇資料

此時會出現&#x200B;**[!UICONTROL Analytics來源新增資料]**&#x200B;步驟。 選取&#x200B;**[!UICONTROL 報表套裝]**&#x200B;以開始建立Analytics報表套裝資料的來源連線，然後選取您要擷取的報表套裝。 選擇&#x200B;**[!UICONTROL Next]**&#x200B;以繼續。

>[!NOTE]
>
>可進行多個與來源的內部連線，以匯入不同的資料。

![](../../../../images/tutorials/create/analytics/add-data.png)

<!---Analytics report suites can be configured for one sandbox at a time. To import the same report suite into a different sandbox, the dataset flow will have to be deleted and instantiated again via configuration for a different sandbox.--->

### 映射

>[!IMPORTANT]
>
>[!DNL Analytics]源的「資料準備」支援功能處於測試版。

「[!UICONTROL 映射]」頁提供了一個介面，用於將源欄位映射到其相應的目標架構欄位。 從這裡，您可以將自訂變數對應至新結構欄位群組，並套用資料準備支援的計算。 選擇目標架構以啟動映射進程。

>[!TIP]
>
>只有具有[!DNL Analytics]模板欄位組的架構才會顯示在架構選擇菜單中。 會忽略其他結構。 如果報表套裝資料沒有適當的結構，則您必須建立新的結構。 有關建立結構的詳細步驟，請參閱UI](../../../../../xdm/ui/resources/schemas.md)中[建立和編輯結構的指南。

![select-schema](../../../../images/tutorials/create/analytics/select-schema.png)

「[!UICONTROL 映射標準欄位]」部分顯示[!UICONTROL 已應用的標準映射]、「[!UICONTROL 非匹配標準映射]」和「[!UICONTROL 自定義映射]」的面板。 有關每個類別的特定資訊，請參閱下表：

| 映射標準欄位 | 說明 |
| --- | --- |
| [!UICONTROL 套用標準對應] | 套用的[!UICONTROL 標準對應]面板會顯示已對應標準屬性的總數。 標準映射指源[!DNL Analytics]資料中的標準屬性和[!DNL Analytics]欄位組中的標準屬性之間的映射集。 這些項目已預先對應，且無法編輯。 |
| [!UICONTROL 非匹配標準映射] | [!UICONTROL 非匹配標準映射]面板表示包含易記名稱衝突的映射標準屬性的數量。 當您重新使用已填入一組欄位描述元的架構時，會出現這些衝突。 即使名稱衝突友好，您也可以繼續[!DNL Analytics]資料流。 |
| [!UICONTROL 自訂對應] | [!UICONTROL 自訂對應]面板顯示對應的自訂屬性數量，包括eVar、prop和清單。 自定義映射指源[!DNL Analytics]資料中的自定義屬性和[!DNL Analytics]欄位組中的自定義屬性之間的映射集。 自訂屬性可對應至其他自訂屬性，以及標準屬性。 |

![map-standard-fields](../../../../images/tutorials/create/analytics/map-standard-fields.png)

若要預覽[!DNL Analytics] ExperienceEvent範本結構欄位群組，請在[!UICONTROL 套用的標準對應]面板中選取&#x200B;**[!UICONTROL 檢視]**。

![檢視](../../../../images/tutorials/create/analytics/view.png)

「[!UICONTROL Adobe Analytics ExperienceEvent範本結構欄位群組]」頁面提供您用來檢查結構的介面。 完成後，選擇&#x200B;**[!UICONTROL Close]**。

![欄位 — 群組 — 預覽](../../../../images/tutorials/create/analytics/field-group-preview.png)

Platform會自動偵測您的對應集，以找出任何好記的名稱衝突。 如果映射集沒有衝突，請選擇&#x200B;**[!UICONTROL Next]**&#x200B;以繼續。

![映射](../../../../images/tutorials/create/analytics/mapping.png)

如果映射集中存在易記名稱衝突，您仍然可以繼續[!DNL Analytics]資料流，確認欄位描述符將相同。 或者，您也可以選擇使用一組空白描述符建立新架構。

選擇&#x200B;**[!UICONTROL Next]**&#x200B;以繼續。

![謹慎](../../../../images/tutorials/create/analytics/caution.png)

#### 自訂對應

要使用資料準備函式並為自定義屬性添加新映射或計算欄位，請選擇&#x200B;**[!UICONTROL 查看自定義映射]**。

![view-custom-mapping](../../../../images/tutorials/create/analytics/view-custom-mapping.png)

接下來，選擇&#x200B;**[!UICONTROL 添加新映射]**。

根據您的需求，您可以從顯示的選項中選擇&#x200B;**[!UICONTROL 添加新映射]**&#x200B;或&#x200B;**[!UICONTROL 添加計算欄位]**。

![add-new-mapping](../../../../images/tutorials/create/analytics/add-new-mapping.png)

出現空映射集。 選擇映射表徵圖以添加源欄位。

![select-source-field](../../../../images/tutorials/create/analytics/select-source-field.png)

您可以使用介面瀏覽源架構結構，並標識要使用的新源欄位。 選擇要映射的源欄位後，選擇&#x200B;**[!UICONTROL Select]**。

![選擇映射](../../../../images/tutorials/create/analytics/select-mapping.png)

接下來，在[!UICONTROL 目標欄位]下選擇映射表徵圖，將所選源欄位映射到其相應的目標欄位。

![select-target-field](../../../../images/tutorials/create/analytics/select-target-field.png)

與源架構類似，您可以使用介面來瀏覽目標架構結構，並選擇要映射的目標欄位。 選擇適當的目標欄位後，請選擇&#x200B;**[!UICONTROL 選擇]**。

![select-target-mapping](../../../../images/tutorials/create/analytics/select-target-mapping.png)

完成自定義映射集後，選擇&#x200B;**[!UICONTROL Next]**&#x200B;繼續。

![complete-custom-mapping](../../../../images/tutorials/create/analytics/complete-custom-mapping.png)

以下文檔提供了有關資料準備、計算欄位和映射函式的進一步資源：

* [資料準備概述](../../../../../data-prep/home.md)
* [資料準備映射函式](../../../../../data-prep/functions.md)
* [將CSV檔案對應至XDM結構並新增計算欄位](../../../../../ingestion/tutorials/map-a-csv-file.md#add-calculated-field)

### 提供資料流詳細資訊

此時將顯示&#x200B;**[!UICONTROL 資料流詳細資訊]**&#x200B;步驟，您必須在其中提供資料流的名稱和可選說明。 完成後，選擇&#x200B;**[!UICONTROL Next]**。

![dataflow detail](../../../../images/tutorials/create/analytics/dataflow-detail.png)

### 檢閱

此時會顯示[!UICONTROL 檢閱]步驟，讓您在建立新Analytics資料流之前先檢閱該資料流。 連線的詳細資訊會依類別分組，包括：

* [!UICONTROL 連線]:顯示連接的源平台。
* [!UICONTROL 資料類型]:顯示選取的報表套裝及其對應的報表套裝ID。

![審查](../../../../images/tutorials/create/analytics/review.png)

### 監視資料流

建立資料流後，您就可以監視正在通過它進行內嵌的資料。 從[!UICONTROL 目錄]螢幕中，選擇&#x200B;**[!UICONTROL 資料流]**&#x200B;以查看與Analytics帳戶關聯的已建立流的清單。

![select-dataflows](../../../../images/tutorials/create/analytics/select-dataflows.png)

此時將顯示&#x200B;**資料流**&#x200B;螢幕。 此頁面上有一組資料集流程，包括其名稱、來源資料、建立時間和狀態的相關資訊。

連接器可具現化兩個資料集流。 一個流程代表回填資料，另一個流程則代表即時資料。 回填資料未針對「設定檔」設定，但會傳送至資料湖，以用於分析和資料科學的使用案例。

如需回填、即時資料及其各自延遲的詳細資訊，請參閱[Analytics Data Connector概述](../../../../connectors/adobe-applications/analytics.md)。

從清單中選取您要檢視的資料集流程。

![select-target-dataset](../../../../images/tutorials/create/analytics/select-target-dataset.png)

此時會出現&#x200B;**[!UICONTROL 資料集活動]**&#x200B;頁面。 此頁面以圖表形式顯示訊息的使用率。 從頂部標題中選擇&#x200B;**[!UICONTROL 資料控管]**&#x200B;以訪問標籤欄位。

![資料集 — 活動](../../../../images/tutorials/create/analytics/dataset-activity.png)

您可以在[!UICONTROL 資料控管]畫面中檢視資料集流的繼承標籤。 如需如何標籤來自Analytics資料的詳細資訊，請造訪[資料使用標籤指南](../../../../../data-governance/labels/user-guide.md)。

![data-gov](../../../../images/tutorials/create/analytics/data-gov.png)

要刪除資料流，請轉至[!UICONTROL 資料流]頁，然後選擇資料流名稱旁的點(`...`)，然後選擇[!UICONTROL 刪除]。

![刪除](../../../../images/tutorials/create/analytics/delete.png)

## 後續步驟和其他資源

建立連接後，將自動建立目標架構和資料流以包含傳入的資料。 此外，還會進行資料回填，以及內嵌長達 13 個月的歷史資料。初始內嵌完成時，[!DNL Analytics]資料供下游Platform服務（例如[!DNL Real-time Customer Profile]和分段服務）使用。 如需詳細資訊，請參閱下列檔案：

* [[!DNL Real-time Customer Profile] 概觀](../../../../../profile/home.md)
* [[!DNL Segmentation Service] 概觀](../../../../../segmentation/home.md)
* [[!DNL Data Science Workspace] 概觀](../../../../../data-science-workspace/home.md)
* [[!DNL Query Service] 概觀](../../../../../query-service/home.md)

以下影片旨在協助您了解如何使用Adobe Analytics來源連接器擷取資料：

>[!WARNING]
>
> 以下影片中顯示的[!DNL Platform] UI已過期。 請參閱上述檔案，了解最新的UI螢幕擷取畫面和功能。

>[!VIDEO](https://video.tv.adobe.com/v/29687?quality=12&learn=on)
