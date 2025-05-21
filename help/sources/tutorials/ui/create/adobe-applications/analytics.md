---
title: 將Adobe Analytics連線至Experience Platform
description: 瞭解如何將Adobe Analytics報表套裝資料帶入Experience Platform
exl-id: 5ddbaf63-feaa-44f5-b2f2-2d5ae507f423
source-git-commit: 086777a09eec17c94a7e0a5d2db58e4a1f6b523f
workflow-type: tm+mt
source-wordcount: '2731'
ht-degree: 3%

---

# 將Adobe Analytics連線至Experience Platform

請閱讀本指南，瞭解如何使用Adobe Analytics來源，將您的Analytics報表套裝資料擷取至Adobe Experience Platform。

## 快速入門

本教學課程需要您實際瞭解下列Experience Platform元件：

* [體驗資料模型(XDM)系統](../../../../../xdm/home.md)： Experience Platform用來組織客戶體驗資料的標準化架構。
* [即時客戶個人檔案](../../../../../profile/home.md)：根據來自多個來源的彙總資料，提供統一的即時客戶個人檔案。
* [沙箱](../../../../../sandboxes/home.md)： Experience Platform提供的虛擬沙箱可將單一Experience Platform執行個體分割成個別的虛擬環境，以利開發及改進數位體驗應用程式。

### 重要術語

請務必瞭解本檔案中使用的下列重要用語：

* **標準屬性**：標準屬性是Adobe預先定義的任何屬性。 它們對所有客戶都包含相同涵義，並且可在Analytics來源資料和Analytics結構描述欄位群組中取得。
* **自訂屬性**：自訂屬性是Analytics中自訂變數階層中的任何屬性。 自訂屬性用於Adobe Analytics實作，將特定資訊擷取至報表套裝，各報表套裝的屬性使用方式可能有所不同。 自訂屬性包括eVar、prop和清單。 如需有關eVar的詳細資訊，請參閱下列有關轉換變數[&#128279;](https://experienceleague.adobe.com/docs/analytics/admin/admin-tools/conversion-variables/conversion-var-admin.html?lang=zh-Hant)的Analytics檔案。
* **自訂欄位群組中的任何屬性**：源自客戶建立的欄位群組的屬性都是使用者定義的，且不屬於標準或自訂屬性。

## 瀏覽來源目錄

>[!NOTE]
>
>在生產沙箱中建立Analytics來源資料流時，會建立兩個資料流：
>
>* 此資料流會將13個月的歷史報表套裝資料回填至Data Lake。 此資料流會在回填完成時結束。
>* 將即時資料傳送到資料湖和[!DNL Real-Time Customer Profile]的資料流流程。 此資料流會持續執行。

在Experience Platform UI中，從左側導覽選取&#x200B;**[!UICONTROL 來源]**&#x200B;以存取[!UICONTROL 來源]工作區。 在&#x200B;*[!UICONTROL Adobe應用程式]*&#x200B;類別中，選取Adobe Analytics卡片，然後選取&#x200B;**[!UICONTROL 新增資料]**。

![已選取Adobe Analytics來源卡的來源目錄。](../../../../images/tutorials/create/analytics/catalog.png)

## 選取資料

>[!IMPORTANT]
>
>* 畫面上列出的報表套裝可能來自不同區域。 您有責任瞭解您資料的限制與義務，以及如何在Adobe Experience Platform中跨區域使用該資料。 請確定貴公司允許這樣做。
>* 只有在沒有資料衝突(例如兩個具有不同含義的自訂屬性（eVar、清單和prop）)時，才能為即時客戶個人檔案啟用多個報表套裝的資料。

報表套裝是資料容器，構成Analytics報表的基礎。 一個組織可以有許多報表套裝，每個報表套裝都包含不同的資料集。

您可以從任何區域擷取報表套裝（美國、英國或新加坡），前提是這些報表套裝對應至與Experience Platform沙箱例項（正在其中建立來源連線）相同的組織。 報告套裝只能使用單一作用中資料流擷取。 如果報表套裝為灰色且無法選取，表示已在您使用的沙箱或其他沙箱中擷取該報表套裝。

可以建立多個繫結連線，將多個報告套裝帶入同一個沙箱。 如果報表套裝中變數（例如eVar或事件）的結構描述不同，則應將其對應至自訂欄位群組中的特定欄位，並使用「資料準備」[避免資料衝突。 ](../../../../../data-prep/ui/mapping.md)報告套裝只能新增至單一沙箱。

選取&#x200B;**[!UICONTROL 報表套裝]**，然後使用&#x200B;*[!UICONTROL Analytics來源新增資料]*&#x200B;介面來瀏覽清單，並識別您要擷取至Experience Platform的Analytics報表套裝。 選取&#x200B;**[!UICONTROL 下一步]**&#x200B;以繼續。

![已選取要內嵌的分析報表套裝，且[下一步]按鈕會反白顯示](../../../../images/tutorials/create/analytics/add-data.png)

&lt;!—Analytics報表套裝一次只能設定一個沙箱。 若要將相同的報告套裝匯入不同的沙箱，必須透過不同沙箱的設定刪除資料集流程並再次例項化。—>

## 對應 {#mapping}

>[!IMPORTANT]
>
>「資料準備」轉換可能會增加整體資料流程的延遲。 新增的額外延遲因轉換邏輯的複雜度而異。

在將Analytics資料對應到目標XDM結構描述之前，您必須先判斷您是使用預設結構描述還是自訂結構描述。

>[!BEGINTABS]

>[!TAB 預設結構描述]

預設結構描述會代表您建立新結構描述。 這個新建立的結構描述包含[!DNL Adobe Analytics ExperienceEvent Template]欄位群組。 若要使用預設結構描述，請選取&#x200B;**[!UICONTROL 預設結構描述]**。

![Analytics來源工作流程的結構描述選取步驟，已選取「預設結構描述」。](../../../../images/tutorials/create/analytics/default-schema.png)

>[!TAB 自訂結構描述]

使用自訂結構描述時，只要該結構描述具有[!DNL Adobe Analytics ExperienceEvent Template]欄位群組，您就可以為Analytics資料選擇任何可用的結構描述。 若要使用自訂結構描述，請選取&#x200B;**[!UICONTROL 自訂結構描述]**。

![已選取「自訂結構描述」的Analytics來源工作流程的結構描述選取步驟。](../../../../images/tutorials/create/analytics/custom-schema.png)

>[!ENDTABS]

使用&#x200B;*[!UICONTROL 對應]*&#x200B;介面將來源欄位對應到適當的目標結構描述欄位。 您可以將自訂變數對應到新的結構欄位群組，並套用資料準備支援的計算。 選取目標結構描述以開始對應程式。

>[!TIP]
>
>只有具有[!DNL Adobe Analytics ExperienceEvent Template]欄位群組的結構描述才會顯示在結構描述選取功能表中。 省略其他結構描述。 如果您的報表套裝資料沒有適用的結構描述，則必須建立新的結構描述。 如需建立結構描述的詳細步驟，請參閱[在UI](../../../../../xdm/ui/resources/schemas.md)中建立和編輯結構描述的指南。

![對應介面的目標結構描述選取面板。](../../../../images/tutorials/create/analytics/select-schema.png)

您可以參考[!UICONTROL 對應標準欄位]面板，以取得已套用[!UICONTROL 標準對應]的量度。 [!UICONTROL 描述項名稱有衝突的標準對應]和[!DNL Custom mappings]。

| 對應標準欄位 | 說明 |
| --- | --- |
| [!UICONTROL 已套用標準對應] | 套用的[!UICONTROL 標準對應]面板會顯示對應屬性的總數。 標準對應是指來源Analytics資料中的所有屬性與Analytics欄位群組中的對應屬性之間的對應。 這些專案已預先對應，無法編輯。 |
| [!UICONTROL 描述項名稱衝突的標準對應] | 描述項名稱衝突的[!UICONTROL 標準對應]面板參考包含名稱衝突的對應屬性數目。 當您重複使用已有來自不同報表套裝之欄位描述項填入集的結構描述時，這些衝突就會出現。 即使名稱衝突，您也可以繼續進行Analytics資料流。 |
| [!UICONTROL 自訂對應] | [!UICONTROL 自訂對應]面板會顯示對應自訂屬性的數量，包括eVar、prop和清單。 自訂對應是指來源Analytics資料中的自訂屬性與所選結構描述中所包含自訂欄位群組中的屬性之間的對應。 |

### 標準對應 {#standard-mappings}

Experience Platform會自動偵測您的對應是否有任何名稱衝突。 如果對應沒有衝突，請選取[下一步] **[!UICONTROL 繼續。]**

![顯示無名稱衝突的標準對應標頭](../../../../images/tutorials/create/analytics/standard.png)

>[!TIP]
>
>如果來源報表套裝與選取的結構描述之間出現名稱衝突，您仍可繼續使用Analytics資料流，確認欄位描述項不會變更。 或者，您可以選擇使用一組空白的描述項建立新結構描述。

## 自訂對應 {#custom-mappings}

您可以使用「資料準備」函式，為自訂屬性新增自訂對應或計算欄位。 若要新增自訂對應，請選取&#x200B;**[!UICONTROL 自訂]**。

![Analytics來源工作流程中的自訂對應標籤。](../../../../images/tutorials/create/analytics/custom.png)

* **[!UICONTROL 篩選欄位]**：使用[!UICONTROL 篩選欄位]文字輸入來篩選對應中的特定對應欄位。
* **[!UICONTROL 新增對應]**：若要新增來源欄位與目標欄位對應，請選取&#x200B;**[!UICONTROL 新增對應]**。
* **[!UICONTROL 新增計算欄位]**：如有需要，您可以選取&#x200B;**[!UICONTROL 新增計算欄位]**，為您的對應建立新的計算欄位。
* **[!UICONTROL 匯入對應]**：您可以使用「資料準備」的匯入對應功能，減少資料擷取程式的手動設定時間，並限制錯誤。 選取&#x200B;**[!UICONTROL 匯入對應]**&#x200B;以從現有流程或匯出的檔案匯入對應。 如需詳細資訊，請閱讀[匯入和匯出對應指南](../../../../../data-prep/ui/mapping.md#import-mapping)。
* **[!UICONTROL 下載範本]**：您也可以下載對應的CSV復本，並在本機裝置設定對應。 選取[下載]範本&#x200B;**以下載您對應的CSV復本。**&#x200B;您必須確保僅使用來源檔案和目標結構描述中提供的欄位。

請參閱下列檔案以取得有關「資料準備」的詳細資訊。

* [資料準備總覽](../../../../../data-prep/home.md)
* [資料準備對應函式](../../../../../data-prep/functions.md)
* [新增計算欄位](../../../../../data-prep/ui/mapping.md#calculated-fields)

<!-- 
To use Data Prep functions and add new mapping or calculated fields for custom attributes, select **[!UICONTROL View custom mappings]**.

![view-custom-mapping](../../../../images/tutorials/create/analytics/view-custom-mapping.png)

Next, select **[!UICONTROL Add new mapping]**.

Depending on your needs, you can select either **[!UICONTROL Add new mapping]** or **[!UICONTROL Add calculated field]** from the options that appear. 

![add-new-mapping](../../../../images/tutorials/create/analytics/add-new-mapping.png)

An empty mapping set appears. Select the mapping icon to add a source field.

![select-source-field](../../../../images/tutorials/create/analytics/select-source-field.png)

You can use the interface to navigate through the source schema structure and identify the new source field that you want to use. Once you have selected the source field that you want to map, select **[!UICONTROL Select]**.

![select-mapping](../../../../images/tutorials/create/analytics/select-mapping.png)

Next, select the mapping icon under [!UICONTROL Target Field] to map your selected source field to its appropriate target field.

![select-target-field](../../../../images/tutorials/create/analytics/select-target-field.png)

Similar to the source schema, you can use the interface to navigate through the target schema structure and select the target field you want to map to. Once you have selected the appropriate target field, select **[!UICONTROL Select]**.

![select-target-mapping](../../../../images/tutorials/create/analytics/select-target-mapping.png)

With your custom mapping set completed, select **[!UICONTROL Next]** to proceed.

![complete-custom-mapping](../../../../images/tutorials/create/analytics/complete-custom-mapping.png) -->

## 篩選即時客戶設定檔 {#filtering-for-profile}

>[!CONTEXTUALHELP]
>id="platform_data_prep_analytics_filtering"
>title="建立篩選規則 "
>abstract="將資料傳送到即時客戶設定檔時定義列層級和欄層級的篩選規則。使用列層級篩選來套用條件並指示要&#x200B;**包含哪些資料以用於攝取設定檔**。使用欄層級篩選來選取您要&#x200B;**為攝取設定檔排除**&#x200B;的資料欄。篩選規則不適用於傳送到資料湖的資料。"

完成Analytics報表套裝資料的對映後，您可以套用篩選規則和條件，選擇性地將資料納入或排除於擷取至Real-time Customer Profile的資料之外。 篩選支援僅適用於Analytics資料，且資料僅在輸入[!DNL Profile.]前進行篩選。所有資料都會擷取到資料湖。

>[!BEGINSHADEBOX]

**針對即時客戶設定檔準備資料和篩選分析資料的其他資訊**

* 您可以將篩選功能用於傳送到個人資料的資料，但不能用於傳送到資料湖的資料。
* 您可以使用篩選即時資料，但無法篩選回填資料。
   * Analytics來源不會將資料回填到設定檔中。
* 如果您在Analytics流程的初始設定期間使用「資料準備」設定，這些變更也會套用至13個月自動回填。
   * 不過，不適用於篩選，因為篩選僅保留給即時資料。
* 「資料準備」會套用至串流和批次擷取路徑。 如果您修改現有的「資料準備」設定，這些變更會套用至串流和批次擷取路徑上的新傳入資料。
   * 不過，無論資料是串流或批次資料，任何「資料準備」設定都不會套用至已擷取至Experience Platform的資料。
* 來自Analytics的標準屬性一律會自動對應。 因此，您無法將轉換套用至標準屬性。
   * 不過，您可以篩選掉標準屬性，只要Identity Service或設定檔中不需要這些屬性。
* 您不能使用欄層級篩選來篩選必填欄位和身分欄位。
* 雖然您可以篩選掉次要身分，尤其是AAID和AACustomID，但您無法篩選ECID。
* 發生轉換錯誤時，對應的欄會產生NULL。

>[!ENDSHADEBOX]

### 列層級篩選

>[!IMPORTANT]
>
>使用列層級篩選來套用條件並指示要&#x200B;**包含哪些資料以用於攝取設定檔**。使用資料行層級篩選來選取您要&#x200B;**排除以進行設定檔擷取**&#x200B;的資料資料行。

您可以在列層級和欄層級篩選設定檔擷取的資料。 使用列層級篩選來定義條件，例如字串包含、等於、開頭或結尾為。 您也可以使用資料列層級篩選來使用`AND`以及`OR`聯結條件，並使用`NOT`否定條件。

若要在列層級篩選您的Analytics資料，請選取&#x200B;**[!UICONTROL 列篩選]**，並使用左側邊欄瀏覽結構描述階層，並識別您要選取的結構描述屬性。

![Analytics資料的資料列篩選介面。](../../../../images/tutorials/create/analytics/row-filter.png)

識別您要設定的屬性後，選取該屬性，並將其從左側邊欄拖曳至篩選面板。

![選取要篩選的「製造商」屬性。](../../../../images/tutorials/create/analytics/filtering-panel.png)

若要設定不同的條件，請選取&#x200B;**[!UICONTROL 等於]**，然後從出現的下拉式視窗中選取條件。

可設定的條件清單包括：

* [!UICONTROL 等於]
* [!UICONTROL 不等於]
* [!UICONTROL 開頭為]
* [!UICONTROL 結尾為]
* [!UICONTROL 結尾不是]
* [!UICONTROL 包含]
* [!UICONTROL 不包含]
* [!UICONTROL 存在]
* [!UICONTROL 不存在]

![條件下拉式清單，內含條件運運算元清單。](../../../../images/tutorials/create/analytics/conditions.png)

接著，根據您選取的屬性輸入您要包含的值。 在下列範例中，已選取[!DNL Apple]和[!DNL Google]作為&#x200B;**[!UICONTROL Manufacturer]**&#x200B;屬性的一部分進行內嵌。

![包含所選屬性和值的篩選面板。](../../../../images/tutorials/create/analytics/include.png)

若要進一步指定篩選條件，請從結構描述新增另一個屬性，然後根據該屬性新增值。 在下列範例中，已新增&#x200B;**[!UICONTROL Model]**&#x200B;屬性，而且已篩選[!DNL iPhone 16]和[!DNL Google Pixel 9]等模型以供擷取。

![包含在容器中的其他屬性和值。](../../../../images/tutorials/create/analytics/include-model.png)

若要新增容器，請選取篩選介面右上方的省略符號(`...`)，然後選取&#x200B;**[!UICONTROL 新增容器]**。

![已選取[新增容器]下拉式功能表。](../../../../images/tutorials/create/analytics/add-container.png)

新增容器後，請選取「**[!UICONTROL 包含]**」，然後從下拉式功能表中選取「**[!UICONTROL 排除]**」。 新增要排除的屬性和值，完成後，選取&#x200B;**[!UICONTROL 下一步]**。

![篩選為排除的屬性和值。](../../../../images/tutorials/create/analytics/exclude.png)

### 欄層級篩選

從標題選取&#x200B;**[!UICONTROL 欄篩選器]**&#x200B;以套用欄層級篩選。

頁面會更新為互動式架構樹狀結構，在欄層級顯示您的架構屬性。 從這裡，您可以選取要從設定檔擷取中排除的資料欄。 或者，您可以展開欄並選取要排除的特定屬性。

依預設，所有Analytics都會移至設定檔，此程式允許從設定檔擷取中排除XDM資料的分支。

![具有結構描述樹狀結構的資料行篩選介面。](../../../../images/tutorials/create/analytics/column-filter.png)

### 篩選次要身分

使用欄篩選器從設定檔擷取中排除次要身分。 若要篩選次要身分，請選取&#x200B;**[!UICONTROL 資料行篩選]**，然後選取&#x200B;**[!UICONTROL _身分]**。

此篩選器僅適用於將身分標示為次要身分時。 如果選取身分，但事件到達時其中一個身分標示為主要身分，則這些身分不會篩選掉。

![結構描述樹狀結構中用於資料行篩選的次要身分。](../../../../images/tutorials/create/analytics/secondary-identities.png)

### 提供資料流詳細資訊

**[!UICONTROL 資料流詳細資料]**&#x200B;步驟隨即顯示，您必須在此為資料流提供名稱和選擇性說明。 完成時選取&#x200B;**[!UICONTROL 下一步]**。

![資料流詳細資料介面。 內嵌工作流程的](../../../../images/tutorials/create/analytics/dataflow-detail.png)。

### 審核

[!UICONTROL 檢閱]步驟隨即顯示，可讓您在建立新的Analytics資料流之前先檢閱該資料流。 連線的詳細資訊會依類別分組，包括：

* [!UICONTROL 連線]：顯示連線的來源平台。
* [!UICONTROL 資料型別]：顯示選取的報表套裝及其對應的報表套裝ID。

![擷取工作流程的檢閱介面。](../../../../images/tutorials/create/analytics/review.png)

## 監視資料流 {#monitor-your-dataflow}

資料流完成後，您可以使用&#x200B;*[!UICONTROL 資料流]*&#x200B;介面來監視Analytics資料流的狀態。

使用[!UICONTROL 資料集活動]介面，取得從Analytics傳送到Experience Platform的資料進度資訊。 介面會顯示量度，例如上個月的總記錄數、過去七天的總擷取記錄數，以及上個月的資料大小。

來源會將兩個資料集流程例項化。 一個流程代表回填資料，另一個流程代表即時資料。 回填資料未設定為擷取至即時客戶個人檔案，而是傳送至資料湖，以用於分析和資料科學的使用案例。

如需回填、即時資料及其各自延遲的詳細資訊，請閱讀[Analytics來源概觀](../../../../connectors/adobe-applications/analytics.md)。

![Adobe Analytics資料之指定目標資料集的資料集活動頁面。](../../../../images/tutorials/create/analytics/dataset-activity.png)

>[!NOTE]
>
>資料集活動頁面不會顯示批次的相關資訊，因為Analytics來源聯結器完全由Adobe管理。 您可以檢視所擷取記錄周圍的量度，以監控資料流程。

## 刪除您的資料流 {#delete-dataflow}

若要刪除您的Analytics資料流，請從來源工作區的頂端標題中選取&#x200B;**[!UICONTROL 資料流]**。 使用資料流頁面來找出您要刪除的Analytics資料流，然後選取它旁邊的省略符號(`...`)。 接下來，使用下拉式功能表並選取&#x200B;**[!UICONTROL 刪除]**。

* 刪除即時Analytics資料流也會刪除其基礎資料集。
* 刪除回填Analytics資料流不會刪除基礎資料集，但會停止其對應報表套裝的回填程式。 如果您刪除回填資料流，擷取的資料可能仍會透過資料集檢視。

## 後續步驟和其他資源

建立連線後，系統會自動建立資料流以包含傳入的資料，並以您選取的結構描述填入資料集。 此外，還會進行資料回填，以及內嵌長達13個月的歷史資料。 初始內嵌完成時，會傳送Analytics資料，供下游Experience Platform服務（例如[!DNL Real-Time Customer Profile]和分段服務）使用。 如需更多詳細資訊，請參閱下列檔案：

* [[!DNL Real-Time Customer Profile] 概觀](../../../../../profile/home.md)
* [[!DNL Segmentation Service] 概觀](../../../../../segmentation/home.md)
* [[!DNL Data Science Workspace] 概觀](../../../../../data-science-workspace/home.md)
* [[!DNL Query Service] 概觀](../../../../../query-service/home.md)

以下影片旨在協助您瞭解如何使用Adobe Analytics Source聯結器擷取資料：

>[!WARNING]
>
> 下列影片中顯示的[!DNL Experience Platform] UI已過期。 請參閱上述檔案，瞭解最新的UI熒幕擷取畫面及功能。

>[!VIDEO](https://video.tv.adobe.com/v/3430259?quality=12&learn=on&captions=chi_hant)

