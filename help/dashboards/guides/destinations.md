---
keywords: Experience Platform；設定檔；即時客戶設定檔；使用者介面；UI；自訂；設定檔控制面板；控制面板
title: 目的地控制面板指南
description: Adobe Experience Platform提供控制面板，讓您透過該控制面板檢視組織作用中目的地的重要資訊。
type: Documentation
exl-id: 6a34a796-24a1-450a-af39-60113928873e
source-git-commit: 66e8d3c594280d4b40cb2b6170544d4411220a6a
workflow-type: tm+mt
source-wordcount: '3031'
ht-degree: 0%

---

# [!UICONTROL 目的地] 儀表板

Adobe Experience Platform使用者介面(UI)提供控制面板，可讓您檢視有關組織作用中目的地的重要資訊，如每日快照中所擷取。 本指南概述如何在UI中存取和使用目標控制面板，並提供控制面板中所顯示量度的詳細資訊。

如需目的地的概觀，以及Experience Platform內所有可用目的地的目錄，請造訪 [目的地檔案](../../destinations/home.md).

## [!UICONTROL 目的地] 控制面板資料 {#destinations-dashboard-data}

「目標」控制面板會顯示貴組織已在Experience Platform中啟用的目標的快照。 快照中的資料與建立快照時在特定時間點顯示的資料完全相同。 換句話說，快照不是資料的近似值或樣本，目標控制面板不會即時更新。

>[!NOTE]
>
>自拍攝快照以來對資料所做的任何更改或更新都不會反映在儀表板中，直到拍攝下一個快照。

## 探索 [!UICONTROL 目的地] 儀表板 {#explore}

若要導覽至Platform UI中的目的地控制面板，請選取 **[!UICONTROL 目的地]** 在左側邊欄中，選取 **[!UICONTROL 概述]** 標籤來顯示控制面板。

最新快照的日期和時間會顯示在 [!UICONTROL 概述] 在目的地下拉式清單旁。 自該日期和時間起，所有介面工具集資料都是準確的。 快照的時間戳以UTC提供；不在個別使用者或組織的時區。

>[!NOTE]
>
>如果您的組織剛開始Experience Platform，且尚未有作用中的目的地，則「目的地」控制面板和 [!UICONTROL 概述] 標籤未顯示。 而是選取 [!UICONTROL 目的地] 從左側導覽顯示 [!UICONTROL 目錄] 標籤。 若要進一步了解 [!UICONTROL 目錄] 標籤，請參閱 [[!UICONTROL 目的地] 工作區指南](../../destinations/ui/destinations-workspace.md).

![最新的快照突出顯示了Platform UI目標概述。](../images/destinations/snapshot-timestamp.png)

### 修改 [!UICONTROL 目的地] 儀表板 {#modify}

選擇 **[!UICONTROL 修改控制面板]** 變更目的地控制面板的外觀。 這可讓您從控制面板移動、新增和移除介面工具集，以及存取介面工具集程式庫。 從介面工具集庫，您可以探索可用介面工具集，並為貴組織建立自訂介面工具集。

請參閱 [修改控制面板](../customize/modify.md) 和 [介面工具集程式庫概述](../customize/widget-library.md) 檔案以深入了解。

### 新增介面工具集 {#add-widget}

選擇 **[!UICONTROL 新增介面工具集]** 導覽至介面工具集庫，並查看可新增至控制面板的可用介面工具集清單。

![「目標」控制面板概觀，並反白顯示「新增介面工具集」。](../images/destinations/destinations-overview-add-widget.png)

從介面工具集庫，您可以瀏覽標準和自訂區段介面工具集的選取項目。 有關如何添加介面工具集的資訊，請參閱介面工具集庫文檔，了解如何 [新增介面工具集](../customize/widget-library.md#add-widgets).

## 標準介面工具集 {#standard-widgets}

Adobe提供多個標準Widget，可用來視覺化與目的地相關的不同量度，並評估資料分析可用區段的完整性。 您也可以使用 [!UICONTROL 介面工具集程式庫]. 若要進一步了解建立自訂Widget，請先閱讀 [介面工具集程式庫概觀](../customize/widget-library.md).

### 先決條件 {#prerequisites}

繼續說明標準小工具之前，請務必熟悉本檔案中使用的下列主要字詞的定義：

* **區段：** 區段是 **規則集** 包括屬性和事件資料，這些資料會限定許多設定檔為受眾。
* **對象**:對象是 **設定檔集** 符合區段定義的條件。
* **已映射/映射**:資料映射是將源資料欄位映射到目標中相關目標欄位的過程。
* **身分**:身分識別碼可唯一代表個別客戶，例如Cookie ID、裝置ID或電子郵件ID。
* **啟動**:「啟用」是使用者為將區段或設定檔對應至目的地(例如Analytics Eloqua、Google或SalesforceOracle)而採取的動作。

若要進一步了解每個可用的標準介面工具集，請從下列清單中選取介面工具集的名稱：

* [[!UICONTROL 最常使用的目的地]](#most-used-destinations)
* [[!UICONTROL 最近建立的目的地]](#recently-created-destinations)
* [[!UICONTROL 最近啟動的區段]](#recently-activated-segments)
* [[!UICONTROL 依目的地的最近啟用區段]](#recently-activated-segments-by-destination)
* [[!UICONTROL 對象大小趨勢]](#audience-size-trend)
* [[!UICONTROL 依身分未對應的區段]](#unmapped-segments-by-identity)
* [[!UICONTROL 依身分對應區段]](#mapped-segments-by-identity)
* [[!UICONTROL 常見對象]](#common-audiences)
* [[!UICONTROL 對應對象]](#mapped-audiences)
* [[!UICONTROL 對應的受眾健康狀況]](#mapped-audience-health)
* [[!UICONTROL 目的地計數]](#destinations-count)
* [[!UICONTROL 目標狀態]](#destination-status)
* [[!UICONTROL 依目的地平台的作用中目的地]](#active-destinations-by-destination-platform)
* [[!UICONTROL 所有目的地的啟用對象]](#activated-audiences-across-all-destinations)
* [[!UICONTROL 已啟用的對象]](#activated-audiences)

### [!UICONTROL 最常使用的目的地] {#most-used-destinations}

>[!CONTEXTUALHELP]
>id="platform_dashboards_destinations_mostuseddestinations"
>title="最常使用的目的地"
>abstract="此介面工具集會依對應的區段數，顯示貴組織最活躍的目的地。 這些數字在上次快照時是準確的。 此排名可深入分析目前最常使用的目的地，同時強調可能未充分利用的目的地。"

此 **[!UICONTROL 最常使用的目的地]** 介面工具集會以自上次快照起已映射的區段數顯示貴組織的最上層目的地。 此排名可深入分析正在使用哪些目的地，同時可能顯示未充分利用的目標。

例如，如果您昨天配置了目標，但未將任何段映射到該目標，則您將會看到該目標當前未充分利用。

自上次每日快照起，區段計數欄中顯示的對應區段數是準確的。 將新區段對應至目標要等到下一個快照建立後，才會更新計數。

從介面工具集上顯示的清單中選取目的地名稱后，您就會前往連結自 **[!UICONTROL 瀏覽]** 標籤。 您也可以選取 **[!UICONTROL 查看全部]** 導覽至 **[!UICONTROL 瀏覽]** 頁簽，然後選擇目標的名稱以查看其詳細資訊。

![「目標」控制面板的「概述」標籤中會反白顯示「最常使用的目標」Widget。](../images/destinations/most-used-destinations.png)

### [!UICONTROL 最近建立的目的地] {#recently-created-destinations}

>[!CONTEXTUALHELP]
>id="platform_dashboards_destinations_recentlycreateddestinations"
>title="最近建立的目的地"
>abstract="此介面工具集會顯示貴組織內最近設定的目標清單。"

此 **[!UICONTROL 最近建立的目的地]** 介面工具集可讓您查看組織最近設定的目標清單。

顯示的建立日期與上次每日快照準確。 換言之，如果建立新目標，則要等到建立下一個快照後，它才會出現在清單中。

從介面工具集上顯示的清單中選取目的地名稱后，您就會前往連結自 **[!UICONTROL 瀏覽]** 標籤。 您也可以選取 **[!UICONTROL 查看全部]** 導覽至 **[!UICONTROL 瀏覽]** 頁簽，然後選擇目標的名稱以查看其詳細資訊。

若要進一步了解如何設定特定類型的目的地，請造訪 [目的地檔案](../../destinations/home.md).

![「目標」控制面板的「概述」標籤中會反白顯示「最近建立的目標」Widget。](../images/destinations/recently-created-destinations.png)

### [!UICONTROL 最近啟動的區段] {#recently-activated-segments}

>[!CONTEXTUALHELP]
>id="platform_dashboards_destinations_recentlyactivatedsegments"
>title="最近啟動的區段"
>abstract="此介面工具集提供最近對應至目的地的區段清單。 此清單提供系統中正在使用的區段和目的地的快照，有助於疑難排解任何錯誤對應。"

此 **[!UICONTROL 最近啟動的區段]** 介面工具集提供最近對應至目的地的區段清單。 此清單提供系統中正在使用的區段和目的地的快照，有助於疑難排解任何錯誤對應。

顯示的更新日期會顯示上次啟動區段至目的地的時間，且對最後的每日快照準確。 換言之，如果您對目的地啟用區段，則更新的日期要等到下次快照建立後才會變更。

從介面工具集上顯示的清單中選取區段名稱，會帶您前往區段詳細資訊。 您也可以選取 **[!UICONTROL 查看全部]** 若要導覽至「區段瀏覽」標籤，然後選取區段名稱以檢視其詳細資料。

如需在Experience Platform中使用區段的詳細資訊，請參閱 [區段服務概觀](../../segmentation/home.md).

![「目的地」控制面板的「概述」標籤會反白顯示「最近啟用的區段」介面工具集。](../images/destinations/recently-activated-segments.png)

### [!UICONTROL 依目的地的最近啟用區段] {#recently-activated-segments-by-destination}

>[!CONTEXTUALHELP]
>id="platform_dashboards_destinations_recentlyactivatedsegmentsbydestination"
>title="依目的地的最近啟用區段"
>abstract="此介面工具集會根據「概述」下拉式清單中所選的目的地，以遞減順序顯示前五個最近啟動的區段。"

此 **[!UICONTROL 依目的地的最近啟用區段]** 介面工具集會根據「概述」下拉式清單中選取的目的地，以遞減順序顯示前五個最近啟動的區段。 類似 [!UICONTROL 最近啟動的區段] 介面工具集，但資料顯示 **僅限** 會套用至選取的目的地。

此介面工具集包含兩個量度：區段名稱和上次啟動至目的地的區段日期。 顯示的資料自上次每日快照時起是正確的。

您可以從顯示的清單中選取區段名稱，以檢視區段的詳細資料。

![依目的地介面工具集的「最近啟用」區段。](../images/destinations/recently-activated-segments-by-destination.png)

請參閱 [使用的詞語定義](#prerequisites) 中。

### [!UICONTROL 對象大小趨勢] {#audience-size-trend}

>[!CONTEXTUALHELP]
>id="platform_dashboards_destinations_audiencesizetrend"
>title="對象大小趨勢"
>abstract="此介面工具集說明區段中包含的設定檔數量，會每天傳送至目的地帳戶。 第一個下拉式功能表會調整對象趨勢的時段。 第二個Widget下拉式選單會選取區段進行分析。 從「概述」下拉式清單中選取目標。"

此 **[!UICONTROL 對象大小趨勢]** 介面工具集描述已對應至該目的地帳戶之區段在一段時間內的設定檔計數關係。 介面工具集使用折線圖來說明區段中包含的設定檔數量，這些設定檔會每天傳送至目的地帳戶。

過去30天、90天或12個月的受眾趨勢時段，可使用第一個下拉式功能表進行調整。

第二個下拉式功能表會列出每個可傳送至控制面板頂端所選目的地帳戶的可用區段。

![對象大小趨勢介面工具集。](../images/destinations/audience-size-trend.png)

此 **[!UICONTROL 對象大小趨勢]** 介面工具集提供 [!UICONTROL 字幕] 按鈕。 選擇 **[!UICONTROL 字幕]** 開啟自動字幕對話框。 機器學習模型通過分析圖表和區段資料自動生成字幕以描述關鍵趨勢和重要事件。

![「對象大小」趨勢Widget的自動字幕對話方塊。](../images/destinations/audience-size-trend-captions.png)

### [!UICONTROL 依身分未對應的區段] {#unmapped-segments-by-identity}

>[!CONTEXTUALHELP]
>id="platform_dashboards_destinations_unmappedsegmentsbyidentity"
>title="依身分未對應的區段"
>abstract="此介面工具集列出前5個 **未映射** 依指定目的地和身分的遞減身分計數排名的區段。 介面工具集下拉式清單中列出的篩選器ID會隨著在概述頁面頂端選取的目的地帳戶而改變。"

此 **[!UICONTROL 依身分未對應的區段]** 介面工具集列出前五名 **未映射** 依指定目的地和身分的遞減身分計數排名的區段。 它會反白標示根據所選ID最有利於對應至所選目的地帳戶的區段。

目的地ID下拉式清單會篩選您的可用區段。 下拉式清單中列出的篩選ID會隨著在概述頁面頂端選取的目的地帳戶而改變。

身分欄會計算區段內可對應至介面工具集ID下拉式清單中所選ID的來源ID數量。

![依身分介面工具集的未對應區段。](../images/destinations/unmapped-segments-by-identity.png)

請參閱 [使用的詞語定義](#prerequisites) 中。

### [!UICONTROL 依身分對應區段] {#mapped-segments-by-identity}

>[!CONTEXTUALHELP]
>id="platform_dashboards_destinations_mappedsegmentsbyidentity"
>title="依身分對應區段"
>abstract="此介面工具集提供前5個 **已映射** 區段。 清單會根據區段中包含的來源ID數量，從高到低排序。 系統會從介面工具集標題下方的下拉式功能表中選取要計算的目標ID。 介面工具集下拉式清單中可用的目標ID取決於在概述控制面板頂端所選取的目標。"

此介面工具集提供前5個 **已映射** 區段。 清單會根據區段中包含的來源ID數量，從高到低排序。 系統會從介面工具集標題下方的下拉式功能表中選取要計算的目標ID。 介面工具集中下拉式清單中可用的目標ID會根據「概述」控制面板頂端所選的目標帳戶篩選條件而變更。

![依身分介面工具集對應區段。](../images/destinations/mapped-segments-by-identity.png)

此 **[!UICONTROL 依身分對應區段]** 介面工具集一覽，即說明在所選目的地內成功鎖定促銷活動設定檔商機的可能性。 有效的目標式行銷活動不取決於傳送至目的地的設定檔數量，而是取決於可能與目的地ID相符的來源ID數量，以提供有用且可操作的資料。

### 常見對象 {#common-audiences}

>[!CONTEXTUALHELP]
>id="platform_dashboards_destinations_commonaudiences"
>title="常見對象"
>abstract="此介面工具集提供在頁面頂端所選目的地帳戶中啟動的前五個區段，以及介面工具集下拉式清單中選取的目的地清單。 區段清單會根據區段啟動的最近時間排序。 最近啟動的區段會顯示在頂端。"

此 **[!UICONTROL 常見對象]** 介面工具集提供在頁面頂端所選目的地帳戶中啟動的前五個區段，以及介面工具集下拉式清單中選取的目的地的清單。 區段清單會根據區段啟動的最近時間排序。 最近啟動的區段會顯示在頂端。

此 [!UICONTROL 對象規模] 欄提供每個列出區段的設定檔總數。

![常見對象小工具集。](../images/destinations/common-audiences.png)

### 對應對象 {#mapped-audiences}

此 [!UICONTROL 對應對象] 介面工具集會顯示可在頁面頂端啟動至所選目的地的對應對象總數。

選擇 **[!UICONTROL 區段]** 導覽至「區段」控制面板 [!UICONTROL 瀏覽] 標籤。 此工作區會顯示貴組織的所有區段定義清單。

![「對應的對象」小工具集。](../images/destinations/mapped-audiences.png)

### 對應的受眾健康狀況 {#mapped-audience-health}

>[!CONTEXTUALHELP]
>id="platform_dashboards_destinations_mappedaudiencehealth"
>title="對應的受眾健康狀況"
>abstract="此介面工具集提供最多20個已對應區段的清單，其總設定檔計數與對應至該目的地的30天平均受眾大小至少有一個標準差的因數有偏差。 它提供過去30天內，受眾大小與平均值的分散度計算量度。 對象大小會從高到低排序。"

介面工具集提供最多20個已對應區段的清單，其總設定檔計數截至上次每日快照時，會偏離對應至該目的地的30天平均受眾大小至少一個標準差的因數。

簡言之，它提供過去30天中受眾規模平均值分散的計算量度。 它會比較今天的受眾規模是否超出過去30天在資料中看到的歷史標準差。

系統中的所有對象大小都會從高到低排序，如 [!UICONTROL 最新大小] 欄。

如果您的區段對應設定檔計數與過去30天內平均對應設定檔大小的標準差以外，表示系統中有異常，應加以調查。

若 [!UICONTROL 對應的受眾健康狀況] 介面工具集差異很大，您應參考對象大小趨勢圖並找出異常區段。 此趨勢可提供您區段健康狀況的進一步分析。

>[!NOTE]
>
>對應對象健康狀況介面工具集的預設大小可能會妨礙表格資訊。 請修改介面工具集的大小，以提高對應區段名稱和欄標題的清晰度。 如需相關指引，請參閱修改控制面板檔案 [如何調整小工具集的大小](../customize/modify.md).

![已對應的受眾健康狀態Widget。](../images/destinations/mapped-audience-health.png)

### [!UICONTROL 目的地計數] {#destinations-count}

>[!CONTEXTUALHELP]
>id="platform_dashboards_destinations_destinationscount"
>title="目的地計數"
>abstract="此介面工具集提供可在系統中啟用和傳遞受眾的可用端點總數。 此數字包含使用中和非使用中目的地。"

此 [!UICONTROL 目的地計數] 介面工具集提供可在系統內啟用和傳遞受眾的可用端點總數。 此數字包含使用中和非使用中目的地。

在總計之下，選取 **[!UICONTROL 目的地]** 導覽至「目的地」瀏覽標籤。 此頁面列出您目前已建立連線的所有目的地。

![目的地計數介面工具集。](../images/destinations/destinations-count.png)

### [!UICONTROL 目標狀態] {#destination-status}

此 [!UICONTROL 目標狀態] 介面工具集會以單一量度顯示已啟用目的地的總數，並使用環圈圖來說明已啟用和已停用目的地之間的比例差異。

當游標停留在環圈圖的相應部分上時，對話框中將顯示啟用或禁用目的地的單個計數。

![目標狀態介面工具集。](../images/destinations/destination-status.png)

### [!UICONTROL 依目的地平台的作用中目的地] {#active-destinations-by-destination-platform}

介面工具集提供兩欄表格，用於顯示作用中目的地平台的清單，以及每個目的地平台的作用中目的地總數。 目標平台的清單從高到低排序。

![依目的地平台Widget的作用中目的地。](../images/destinations/active-destinations-by-destination-platform.png)

### [!UICONTROL 所有目的地的啟用對象] {#activated-audiences-across-all-destinations}

此 [!UICONTROL 所有目的地的啟用對象] 介面工具集可提供在單一量度中啟用所有目的地的受眾總數。 此介面工具集會顯示對象計數，而非區段計數。 此數字對於最近的快照是準確的。

![所有目的地介面工具集的「已啟用」對象。](../images/destinations/activated-audiences-across-all-destinations.png)

選擇 **[!UICONTROL 對象]** 導覽至目的地 [!UICONTROL 瀏覽] 標籤。 此頁面提供所有已啟用的目的地和各種相關量度的清單。 如需 [[!UICONTROL 瀏覽] 標籤](../../destinations/ui/destinations-workspace.md#browse).

請參閱 [使用的詞語定義](#prerequisites) 中。

### [!UICONTROL 已啟用的對象] {#activated-audiences}

此介面工具集提供單一量度，可計算啟動至目的地的受眾總數。

![「已啟用的對象」小工具。](../images/destinations/activated-audiences.png)

選擇 **[!UICONTROL 對象]** 導覽至目的地控制面板的詳細資訊頁面。 此 [!UICONTROL 啟動資料] 索引標籤會顯示已對應至目的地的區段清單，包括其開始日期和結束日期（若適用），以及資料匯出的其他相關資訊，例如匯出類型、排程和頻率。 若要檢視特定區段的詳細資訊，請從清單中選取其名稱。

![「啟動資料」索引標籤醒目顯示「目標控制面板詳細資料」頁面。](../images/destinations/activation-data-tab.png)

此介面工具集可協助您根據一覽啟動的對象數量，了解目的地的價值。 它還提供了更詳細資訊的輕鬆訪問，以供進一步分析。

請參閱 [使用的詞語定義](#prerequisites) 中。

## 後續步驟

依照本檔案操作，您現在應該能夠找到目的地控制面板並了解可用介面工具集中顯示的量度。 若要進一步了解如何使用Experience Platform中的目的地，請參閱 [目的地檔案](../../destinations/home.md).
