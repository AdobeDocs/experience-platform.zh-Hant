---
keywords: Experience Platform；首頁；熱門主題；Analytics來源連接器；Analytics來源；分析；篩選；設定檔篩選；即時客戶設定檔；篩選；篩選設定檔資料；列層級篩選；欄層級篩選
title: 在UI中建立Adobe Analytics來源連線
description: 了解如何在UI中建立Adobe Analytics來源連線，將消費者資料匯入Adobe Experience Platform。
exl-id: 5ddbaf63-feaa-44f5-b2f2-2d5ae507f423
source-git-commit: 23a99a46cfd6e42dd0f4815bb972dbe46104b60f
workflow-type: tm+mt
source-wordcount: '2380'
ht-degree: 5%

---

# 在UI中建立Adobe Analytics來源連線

本教學課程提供在UI中建立Adobe Analytics來源連線，將Adobe Analytics報表套裝資料匯入Adobe Experience Platform的步驟。

## 快速入門

本教學課程需要妥善了解下列Experience Platform元件：

* [Experience Data Model(XDM)系統](../../../../../xdm/home.md):Experience Platform組織客戶體驗資料的標準化架構。
* [即時客戶個人檔案](../../../../../profile/home.md):根據來自多個來源的匯總資料，提供統一的即時消費者設定檔。
* [沙箱](../../../../../sandboxes/home.md):Experience Platform提供可將單一Platform執行個體分割成個別虛擬環境的虛擬沙箱，以協助開發及改進數位體驗應用程式。

### 重要術語

請務必了解本檔案中使用的下列主要術語：

* **標準屬性**:標準屬性是Adobe預先定義的任何屬性。 它們對所有客戶具有相同的含義，並可在 [!DNL Analytics] 來源資料和 [!DNL Analytics] 架構欄位群組。
* **自訂屬性**:自訂屬性是自訂變數階層中的任何屬性，位於 [!DNL Analytics]. 自訂屬性用於Adobe Analytics實作中，以將特定資訊擷取至報表套裝中，而且其用途因報表套裝而異。 自訂屬性包括eVar、prop和清單。 請參閱下列內容 [[!DNL Analytics] 轉換變數檔案](https://experienceleague.adobe.com/docs/analytics/admin/admin-tools/conversion-variables/conversion-var-admin.html?lang=en) 以取得eVar的詳細資訊。
* **自訂欄位群組中的任何屬性**:源自客戶建立的欄位群組的屬性皆為使用者定義，不視為標準或自訂屬性。
* **易記名稱**:好記名稱是人工提供的標籤，適用於 [!DNL Analytics] 實作。 請參閱下列內容 [[!DNL Analytics] 轉換變數檔案](https://experienceleague.adobe.com/docs/analytics/admin/admin-tools/conversion-variables/conversion-var-admin.html?lang=en) 以取得好記名稱的詳細資訊。

## 使用Adobe Analytics建立來源連線

在平台UI中，選取 **[!UICONTROL 來源]** 從左側導覽器存取 [!UICONTROL 來源] 工作區。 此 [!UICONTROL 目錄] 畫面會顯示您可以用來建立帳戶的各種來源。

您可以從畫面左側的目錄中選取適當的類別。 您也可以使用搜尋列來縮小顯示的來源。

在 **[!UICONTROL Adobe應用程式]** 類別，選擇 **[!UICONTROL Adobe Analytics]** 然後選取 **[!UICONTROL 新增資料]**.

![目錄](../../../../images/tutorials/create/analytics/catalog.png)

### 選擇資料

>[!IMPORTANT]
>
>畫面上列出的報表套裝可能來自不同地區。 您有責任了解資料的限制和義務，以及如何在Adobe Experience Platform跨地區使用這些資料。 請確定這是貴公司允許的。

此 **[!UICONTROL Analytics來源新增資料]** 步驟會提供 [!DNL Analytics] 報表套裝資料，以建立來源連線。

報表套裝是構成 [!DNL Analytics] 報告。 組織可以有許多報表套裝，每個報表套裝都包含不同的資料集。

只要報表套裝對應至與建立來源連線的Experience Platform沙箱例項相同的組織，您就可以從任何地區（美國、英國或新加坡）內嵌報表套裝。 只能使用單一活動資料流來內嵌報表套裝。 無法選取的報表套裝已擷取，位於您所使用的沙箱中，或位於不同的沙箱中。

可以建立多個內部連線，將多個報表套裝帶入同一個沙箱。 如果報表套裝的變數結構不同（例如eVar或事件），應將其對應至自訂欄位群組中的特定欄位，並避免使用 [資料準備](../../../../../data-prep/ui/mapping.md). 報表套裝只能新增至單一沙箱。

![](../../../../images/tutorials/create/analytics/report-suite.png)

>[!NOTE]
>
>只有在沒有資料衝突(例如兩個具有不同意義的自訂屬性（eVar、清單和Prop）)時，才能為「即時客戶設定檔」啟用來自多個報表套裝的資料。

若要建立 [!DNL Analytics] 來源連線，選取報表套裝，然後選取 **[!UICONTROL 下一個]** 繼續。

![](../../../../images/tutorials/create/analytics/add-data.png)

&lt;! — 可一次為一個沙箱設定Analytics報表套裝。 若要將相同的報表套裝匯入不同的沙箱中，資料集流量必須透過不同沙箱的設定再次遭到刪除和實例化。—>

### 映射

>[!IMPORTANT]
>
>資料準備轉換可能會增加整體資料流的延遲。 增加的額外延遲會因轉換邏輯的複雜度而異。

在您可以對應 [!DNL Analytics] 資料來鎖定目標XDM架構時，您必須先選取使用預設架構或自訂架構。

預設架構代表您建立新架構，包含 [!DNL Adobe Analytics ExperienceEvent Template] 欄位群組。 要使用預設架構，請選擇 **[!UICONTROL 預設結構]**.

![default-schema](../../../../images/tutorials/create/analytics/default-schema.png)

使用自訂結構，您可以為 [!DNL Analytics] 資料，只要該架構具有 [!DNL Adobe Analytics ExperienceEvent Template] 欄位群組。 若要使用自訂結構，請選取 **[!UICONTROL 自訂結構]**.

![自訂綱要](../../../../images/tutorials/create/analytics/custom-schema.png)

此 [!UICONTROL 對應] 「 」頁面提供一個介面，用於將源欄位映射到相應的目標架構欄位。 從這裡，您可以將自訂變數對應至新結構欄位群組，並套用資料準備支援的計算。 選擇目標架構以啟動映射進程。

>[!TIP]
>
>僅限具有 [!DNL Adobe Analytics ExperienceEvent Template] 欄位組顯示在方案選擇菜單中。 會忽略其他結構。 如果您的報表套裝資料沒有適當的結構，則必須建立新的結構。 如需建立結構的詳細步驟，請參閱 [在UI中建立和編輯結構](../../../../../xdm/ui/resources/schemas.md).

![select-schema](../../../../images/tutorials/create/analytics/select-schema.png)

此 [!UICONTROL 映射標準欄位] 區段會顯示面板 [!UICONTROL 套用標準對應], [!UICONTROL 非匹配標準映射] 和 [!UICONTROL 自訂對應]. 有關每個類別的特定資訊，請參閱下表：

| 映射標準欄位 | 說明 |
| --- | --- |
| [!UICONTROL 套用標準對應] | 此 [!UICONTROL 套用標準對應] 面板顯示映射屬性的總數。 標準映射是指源中所有屬性之間的映射集 [!DNL Analytics] 資料和對應屬性 [!DNL Analytics] 欄位群組。 這些項目已預先對應，且無法編輯。 |
| [!UICONTROL 非匹配標準映射] | 此 [!UICONTROL 非匹配標準映射] 面板是指包含易記名稱衝突的已映射屬性數量。 當您重新使用已從不同報表套裝填入一組欄位描述元的架構時，會出現這些衝突。 您可以繼續 [!DNL Analytics] 資料流，即使名稱衝突友好。 |
| [!UICONTROL 自訂對應] | 此 [!UICONTROL 自訂對應] 面板會顯示對應的自訂屬性數量，包括eVar、prop和清單。 自訂對應指源中自訂屬性之間的對應集 [!DNL Analytics] 自訂欄位群組中包含的資料和屬性。 |

![map-standard-fields](../../../../images/tutorials/create/analytics/map-standard-fields.png)

若要預覽 [!DNL Analytics] ExperienceEvent範本結構欄位群組，請選取 **[!UICONTROL 檢視]** 在 [!UICONTROL 套用標準對應] 中。

![檢視](../../../../images/tutorials/create/analytics/view.png)

此 [!UICONTROL Adobe Analytics ExperienceEvent範本結構欄位群組] 「 」頁面提供用於檢查架構結構的介面。 完成後，請選取 **[!UICONTROL 關閉]**.

![欄位 — 群組 — 預覽](../../../../images/tutorials/create/analytics/field-group-preview.png)

Platform會自動偵測您的對應集，以找出任何好記的名稱衝突。 如果映射集沒有衝突，請選擇 **[!UICONTROL 下一個]** 繼續。

![映射](../../../../images/tutorials/create/analytics/mapping.png)

如果來源報表套裝和您選取的結構之間有好記的名稱衝突，您仍可繼續使用 [!DNL Analytics] dataflow，確認欄位描述符將不會更改。 或者，您也可以選擇使用一組空白描述符建立新架構。

選擇 **[!UICONTROL 下一個]** 繼續。

![謹慎](../../../../images/tutorials/create/analytics/caution.png)

#### 自訂對應

要使用資料準備函式並為自定義屬性添加新的映射或計算欄位，請選擇 **[!UICONTROL 檢視自訂對應]**.

![view-custom-mapping](../../../../images/tutorials/create/analytics/view-custom-mapping.png)

下一步，選擇 **[!UICONTROL 新增對應]**.

您可以視您的需求選擇 **[!UICONTROL 新增對應]** 或 **[!UICONTROL 新增計算欄位]** 從顯示的選項。

![add-new-mapping](../../../../images/tutorials/create/analytics/add-new-mapping.png)

出現空映射集。 選擇映射表徵圖以添加源欄位。

![select-source-field](../../../../images/tutorials/create/analytics/select-source-field.png)

您可以使用介面瀏覽源架構結構，並標識要使用的新源欄位。 選擇要映射的源欄位後，請選擇 **[!UICONTROL 選擇]**.

![選擇映射](../../../../images/tutorials/create/analytics/select-mapping.png)

下一步，選取下方的對應圖示 [!UICONTROL 目標欄位] 將所選源欄位映射到其相應的目標欄位。

![select-target-field](../../../../images/tutorials/create/analytics/select-target-field.png)

與源架構類似，您可以使用介面來瀏覽目標架構結構，並選擇要映射的目標欄位。 選取適當的目標欄位後，請選取 **[!UICONTROL 選擇]**.

![select-target-mapping](../../../../images/tutorials/create/analytics/select-target-mapping.png)

完成自訂對應集後，請選取 **[!UICONTROL 下一個]** 繼續。

![complete-custom-mapping](../../../../images/tutorials/create/analytics/complete-custom-mapping.png)

以下文檔提供了有關資料準備、計算欄位和映射函式的進一步資源：

* [資料準備概述](../../../../../data-prep/home.md)
* [資料準備映射函式](../../../../../data-prep/functions.md)
* [新增計算欄位](../../../../../data-prep/ui/mapping.md#calculated-fields)

### 篩選即時客戶設定檔 {#filtering-for-profile}

>[!CONTEXTUALHELP]
>id="platform_data_prep_analytics_filtering"
>title="建立篩選規則 "
>abstract="將資料傳送到即時客戶設定檔時定義列層級和欄層級的篩選規則。使用列層級篩選來套用條件並指示要&#x200B;**包含哪些資料以用於設定檔擷取**。使用欄層級篩選來選取您要&#x200B;**為設定檔擷取排除**&#x200B;的資料欄。篩選規則不適用於傳送到資料湖的資料。"

完成對應後 [!DNL Analytics] 報表套裝資料，您可以套用篩選規則和條件，以選擇性地將資料納入或排除不匯入至即時客戶設定檔。 篩選支援僅適用於 [!DNL Analytics] 只會在輸入前篩選資料和資料 [!DNL Profile.] 所有資料都會擷取至資料湖。

#### 列層級篩選

>[!IMPORTANT]
>
>使用列層級篩選來套用條件並指示要&#x200B;**包含哪些資料以用於設定檔擷取**。使用欄層級篩選來選取您要&#x200B;**為設定檔擷取排除**&#x200B;的資料欄。

您可以篩選資料 [!DNL Profile] 在列層級和欄層級擷取。 列層級篩選可讓您定義條件，例如字串包含、等於、開頭或結尾為。 您也可以使用列層級篩選來連結條件，使用 `AND` 和 `OR`，使用 `NOT`.

若要篩選 [!DNL Analytics] 資料，請選取 **[!UICONTROL 列篩選]**.

![列篩選](../../../../images/tutorials/create/analytics/row-filter.png)

使用左側邊欄瀏覽架構階層，並選取您選擇的架構屬性，以進一步深入鑽研特定架構。

![左側邊欄](../../../../images/tutorials/create/analytics/left-rail.png)

識別您要設定的屬性後，請選取屬性，並從左側邊欄拖曳至篩選面板。

![篩選面板](../../../../images/tutorials/create/analytics/filtering-panel.png)

若要設定不同的條件，請選取 **[!UICONTROL 等於]** 然後從下拉式視窗中選取出現的條件。

可設定條件的清單包括：

* [!UICONTROL 等於]
* [!UICONTROL 不等於]
* [!UICONTROL 開始於]
* [!UICONTROL 終止於]
* [!UICONTROL 不終止於]
* [!UICONTROL 包含]
* [!UICONTROL 不包含]
* [!UICONTROL 存在]
* [!UICONTROL 不存在]

![條件](../../../../images/tutorials/create/analytics/conditions.png)

接下來，根據所選屬性輸入要包含的值。 在以下範例中， [!DNL Apple] 和 [!DNL Google] 會選取以擷取作為 **[!UICONTROL 製造商]** 屬性。

![包括製造商](../../../../images/tutorials/create/analytics/include-manufacturer.png)

若要進一步指定篩選條件，請從結構中新增其他屬性，然後根據該屬性新增值。 在以下範例中， **[!UICONTROL 模型]** 屬性並新增模型，例如 [!DNL iPhone 13] 和 [!DNL Google Pixel 6] 會篩選以擷取。

![包括模型](../../../../images/tutorials/create/analytics/include-model.png)

若要新增容器，請選取點(`...`)，然後選取 **[!UICONTROL 新增容器]**.

![新增容器](../../../../images/tutorials/create/analytics/add-container.png)

新增容器後，請選取 **[!UICONTROL 包括]** 然後選取 **[!UICONTROL 排除]** 從顯示的下拉式視窗中。

![排除](../../../../images/tutorials/create/analytics/exclude.png)

接下來，拖曳結構屬性並新增您要排除於篩選條件之外的對應值，以完成相同的程式。 在以下範例中， [!DNL iPhone 12], [!DNL iPhone 12 mini]，和 [!DNL Google Pixel 5] 都是從排除中篩選而得 **[!UICONTROL 模型]** 屬性中，橫向會從 **[!UICONTROL 螢幕方向]**，型號 [!DNL A1633] 從中排除 **[!UICONTROL 型號]**.

完成後，請選取 **[!UICONTROL 下一個]**.

![exclude-examples](../../../../images/tutorials/create/analytics/exclude-examples.png)

#### 欄層級篩選

選擇 **[!UICONTROL 欄篩選]** 從標題套用欄層級篩選。

![欄篩選](../../../../images/tutorials/create/analytics/column-filter.png)

頁面會更新為互動式結構樹狀結構，在欄層級顯示您的結構屬性。 從此處，您可以選取要排除的資料欄 [!DNL Profile] 擷取。 或者，您也可以展開欄並選取特定屬性以排除。

依預設，全部 [!DNL Analytics] 轉到 [!DNL Profile] 此程式可將XDM資料的分支從 [!DNL Profile] 擷取。

完成後，請選取 **[!UICONTROL 下一個]**.

![列選定](../../../../images/tutorials/create/analytics/columns-selected.png)

### 提供資料流詳細資訊

此 **[!UICONTROL 資料流詳細資訊]** 此時將出現一個步驟，您必須在其中為資料流提供名稱和可選說明。 選擇 **[!UICONTROL 下一個]** 完成時。

![dataflow detail](../../../../images/tutorials/create/analytics/dataflow-detail.png)

### 請檢閱

此 [!UICONTROL 檢閱] 步驟，讓您在建立新Analytics資料流之前先加以檢閱。 連線的詳細資訊會依類別分組，包括：

* [!UICONTROL 連線]:顯示連接的源平台。
* [!UICONTROL 資料類型]:顯示選取的報表套裝及其對應的報表套裝ID。

![審查](../../../../images/tutorials/create/analytics/review.png)

### 監視資料流

建立資料流後，您就可以監視正在通過它進行內嵌的資料。 從 [!UICONTROL 目錄] 螢幕，選擇 **[!UICONTROL 資料流]** 檢視與您的Analytics帳戶相關聯的已建立流程清單。

![select-dataflows](../../../../images/tutorials/create/analytics/select-dataflows.png)

此 **資料流** 畫面。 此頁面上有一組資料集流程，包括其名稱、來源資料、建立時間和狀態的相關資訊。

連接器可具現化兩個資料集流。 一個流程代表回填資料，另一個流程則代表即時資料。 回填資料未針對「設定檔」設定，但會傳送至資料湖，以用於分析和資料科學的使用案例。

如需回填、即時資料及其個別延遲的詳細資訊，請參閱 [Analytics Data Connector概觀](../../../../connectors/adobe-applications/analytics.md).

從清單中選取您要檢視的資料集流程。

![select-target-dataset](../../../../images/tutorials/create/analytics/select-target-dataset.png)

此 **[!UICONTROL 資料集活動]** 頁。 此頁面以圖表形式顯示訊息的使用率。 選擇 **[!UICONTROL 資料控管]** 以存取標籤欄位。

![資料集 — 活動](../../../../images/tutorials/create/analytics/dataset-activity.png)

您可以檢視資料集流的繼承標籤， [!UICONTROL 資料控管] 螢幕。 如需如何標籤來自Analytics的資料的詳細資訊，請造訪 [資料使用標籤指南](../../../../../data-governance/labels/user-guide.md).

![data-gov](../../../../images/tutorials/create/analytics/data-gov.png)

要刪除資料流，請轉至 [!UICONTROL 資料流] 頁面，然後選取點(`...`)，然後選取 [!UICONTROL 刪除].

![delete](../../../../images/tutorials/create/analytics/delete.png)

## 後續步驟和其他資源

建立連線後，會自動建立資料流以包含傳入的資料，並將您選取的架構填入資料集。 此外，還會進行資料回填，以及內嵌長達 13 個月的歷史資料。初始擷取完成時， [!DNL Analytics] 供下游Platform服務(例如 [!DNL Real-Time Customer Profile] 和分段服務。 如需詳細資訊，請參閱下列檔案：

* [[!DNL Real-Time Customer Profile] 概覽](../../../../../profile/home.md)
* [[!DNL Segmentation Service] 概覽](../../../../../segmentation/home.md)
* [[!DNL Data Science Workspace] 概覽](../../../../../data-science-workspace/home.md)
* [[!DNL Query Service] 概覽](../../../../../query-service/home.md)

以下影片旨在協助您了解如何使用Adobe Analytics來源連接器擷取資料：

>[!WARNING]
>
> 此 [!DNL Platform] 下列影片中顯示的UI已過期。 請參閱上述檔案，了解最新的UI螢幕擷取畫面和功能。

>[!VIDEO](https://video.tv.adobe.com/v/29687?quality=12&learn=on)
