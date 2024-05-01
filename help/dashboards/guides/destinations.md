---
keywords: Experience Platform；設定檔；即時客戶設定檔；使用者介面；UI；自訂；設定檔控制面板；控制面板
title: 目的地控制面板
description: Adobe Experience Platform提供控制面板，讓您檢視有關組織作用中目的地的重要資訊。
type: Documentation
exl-id: 6a34a796-24a1-450a-af39-60113928873e
source-git-commit: a8b5ed09e8e28075a3a4f37ad30f01c1cc389b9c
workflow-type: tm+mt
source-wordcount: '3243'
ht-degree: 19%

---

# [!UICONTROL 目的地] 儀表板

Adobe Experience Platform使用者介面(UI)提供了一個儀表板，您可以透過該儀表板檢視有關您組織活躍目的地的重大資訊，如每日快照期間所擷取。 本指南概述如何存取及使用UI中的目標儀表板，並提供有關儀表板中顯示的量度的詳細資訊。

若需目的地概覽以及Experience Platform中所有可用目的地的目錄，請造訪 [目的地檔案](../../destinations/home.md).

## [!UICONTROL 目的地] 儀表板資料 {#destinations-dashboard-data}

目的地儀表板會顯示貴組織在Experience Platform中啟用的目的地的快照。 快照中的資料顯示資料的方式與拍攝快照的特定時間點完全相同。 換句話說，快照不是資料的近似或範例，而且目的地儀表板沒有即時更新。

>[!NOTE]
>
>自拍攝快照以來對資料所做的任何變更或更新都不會反映在儀表板中，直到拍攝下一個快照為止。

## 探索 [!UICONTROL 目的地] 儀表板 {#explore}

若要導覽至Platform UI中的目的地控制面板，請選取「 」 **[!UICONTROL 目的地]** 在左側欄中，然後選取 **[!UICONTROL 概觀]** 標籤來顯示控制面板。

最近一次快照的日期和時間會顯示在最上方 [!UICONTROL 概觀] ，位於目的地下拉式清單旁。 截至該日期和時間，所有Widget資料都是準確的。 快照的時間戳記會以UTC提供；而不是在個別使用者或組織的時區中。

>[!NOTE]
>
>如果您的組織剛開始使用Experience Platform，但尚未擁有作用中的目的地，則目的地控制面板和 [!UICONTROL 概觀] 標籤不可見。 請改為選取 [!UICONTROL 目的地] 從左側導覽器顯示 [!UICONTROL 目錄] 標籤。 若要進一步瞭解 [!UICONTROL 目錄] 索引標籤，請參閱 [[!UICONTROL 目的地] workspace指南](../../destinations/ui/destinations-workspace.md).

![Platform UI目標總覽以及醒目提示的最新快照。](../images/destinations/snapshot-timestamp.png)

### 修改 [!UICONTROL 目的地] 儀表板 {#modify}

選取 **[!UICONTROL 修改儀表板]** 變更目的地控制面板的外觀。 控制面板的變更是按使用者進行，而非整個組織。 您可以從儀表板移動、新增、調整大小及移除Widget，並存取Widget程式庫來自訂儀表板。 從Widget程式庫，您可以探索可用的Widget並為您的組織建立自訂Widget。

請參閱 [修改儀表板](../customize/modify.md) 和 [Widget程式庫概觀](../customize/widget-library.md) 檔案以深入瞭解。

### 新增Widget {#add-widget}

選取 **[!UICONTROL 新增Widget]** 導覽至Widget資料庫，並檢視可新增至控制面板的可用Widget清單。

![醒目提示目標儀表板的「新增Widget」概述。](../images/destinations/destinations-overview-add-widget.png)

在Widget資料庫中，您可以瀏覽標準與自訂對象Widget的選取專案。 如需如何新增Widget的相關資訊，請參閱如何新增Widget的程式庫檔案 [新增Widget](../customize/widget-library.md#add-widgets).

### 檢視SQL {#view-sql}

您可以透過開啟「 」按鈕來檢視產生在控制面板上視覺化分析的SQL。 [!UICONTROL 概觀] 工作區。 您可以從現有見解的SQL獲得靈感，以建立新的查詢，這些查詢會根據您的業務需求從Platform資料獲得獨特的見解。 若要進一步瞭解此功能，請參閱 [檢視SQL UI指南](../view-sql.md).

## 預設Widget {#default-widgets}

Adobe Experience Platform的所有新執行個體都會提供預設Widget載出，以強調資料中最新可用的深入分析。 下列Widget從一開始便已在您的區段檢視中預先設定。 有關Widget用途和功能的完整詳細資訊，請參閱下文。

* [[!UICONTROL 最常用的目的地]](#most-used-destinations)
* [[!UICONTROL 最近建立的目的地]](#recently-created-destinations)
* [[!UICONTROL 最近啟用的區段]](#recently-activated-segments)

>[!NOTE]
>
>截至2023年7月26日， [!UICONTROL 設定檔]， [!UICONTROL 受眾]、和 [!UICONTROL 目的地] 對於所有在前六個月未修改檢視的使用者，概述儀表板已重設為新的預設Widget載出。
>請參閱以下檔案： [設定檔](./profiles.md#default-widgets) 和 [受眾](./audiences.md#default-widgets) 預設Widget區段，以取得關於哪些小工具屬於預設Widget載入一部分的詳細資訊。 您可以繼續如往常一樣自訂您的儀表板Widget。

## 標準Widget {#standard-widgets}

Adobe提供多種標準Widget，可用來視覺化與目的地相關的不同量度，並評估資料分析可用對象的完整性。 您也可以使用建立自訂Widget並與您的組織共用 [!UICONTROL Widget資料庫]. 若要進一步瞭解如何建立自訂Widget，請先閱讀 [Widget程式庫概觀](../customize/widget-library.md).

### 先決條件 {#prerequisites}

在繼續說明標準Widget之前，請務必熟悉本檔案中使用的下列重要術語定義：

* **區段定義：** 區段定義是 **規則集** 用於說明目標對象的主要特性或行為。 這些規則包含屬性和事件資料，可讓設定檔符合對象資格。
* **對象**：一組具有共同特徵和行為的人員、帳戶、家庭或其他實體。
* **已對應/對應**：資料對應是將來源資料欄位對應到目的地中相關目標欄位的程式。
* **身分**：身分識別是可唯一代表個別客戶的識別碼，例如Cookie ID、裝置ID或電子郵件ID。
* **啟動**：啟動是使用者將對象或設定檔對應至目的地(例如Oracle Eloqua、Google或SalesforceMarketing Cloud)所採取的動作。

若要進一步瞭解每個可用的標準Widget，請從下列清單中選取Widget的名稱：

* [[!UICONTROL 最常用的目的地]](#most-used-destinations)
* [[!UICONTROL 最近建立的目的地]](#recently-created-destinations)
* [[!UICONTROL 最近啟動的對象]](#recently-activated-audiences)
* [[!UICONTROL 最近啟動的對象 (依目的地)]](#recently-activated-audiences-by-destination)
* [[!UICONTROL 對象規模趨勢]](#audience-size-trend)
* [[!UICONTROL 未對應對象 (依身分識別)]](#unmapped-audiences-by-identity)
* [[!UICONTROL 已對應對象 (依身分識別)]](#mapped-audiences-by-identity)
* [[!UICONTROL 通用對象]](#common-audiences)
* [[!UICONTROL 對應的對象]](#mapped-audiences)
* [[!UICONTROL 對應的對象健康狀況]](#mapped-audience-health)
* [[!UICONTROL 目的地計數]](#destinations-count)
* [[!UICONTROL 目的地狀態]](#destination-status)
* [[!UICONTROL 依目的地平台區分的有效目的地]](#active-destinations-by-destination-platform)
* [[!UICONTROL 跨所有目的地的已啟用對象]](#activated-audiences-across-all-destinations)
* [[!UICONTROL 啟用的對象]](#activated-audiences)

### [!UICONTROL 最常用的目的地] {#most-used-destinations}

>[!CONTEXTUALHELP]
>id="platform_dashboards_destinations_mostuseddestinations"
>title="最常用的目的地"
>abstract="此介面工具會依據對應的對象數顯示貴組織最活躍的目的地。這些數字在上次快照時是準確的。此排名會提供對目前使用最多的目的地的分析，同時會強調可能未受到充分利用的目的地。"

此 **[!UICONTROL 最常使用的目的地]** Widget會依對應對象數目（截至上次快照為止）顯示您組織的熱門目的地。 此排名可讓您深入瞭解正在使用的目的地，同時可能會顯示可能未充分利用的目的地。

例如，如果您昨天設定了目的地，但尚未將任何對象對應至該目的地，您便可看到該目的地目前利用不足。

顯示在「 」中的對應對象數 [!UICONTROL 對象計數] 欄是截至上次每日快照的精確資料。 將新對象對應到目的地不會更新計數，直到拍攝下一個快照為止。

從Widget上顯示的清單中選取目的地的名稱，即可導覽至該特定目的地的目的地詳細資料。 您也可以選取 **[!UICONTROL 檢視全部]** 導覽至 **[!UICONTROL 瀏覽]** 標籤，然後選取目的地名稱以檢視其詳細資訊。

![目標儀表板的總覽標籤，其中最常用的目標Widget強調顯示。](../images/destinations/most-used-destinations.png)

### [!UICONTROL 最近建立的目的地] {#recently-created-destinations}

>[!CONTEXTUALHELP]
>id="platform_dashboards_destinations_recentlycreateddestinations"
>title="最近建立的目的地"
>abstract="此介面工具會顯示您組織內最近設定的目的地清單。"

此 **[!UICONTROL 最近建立的目的地]** widget可讓您檢視貴組織最近設定之目的地的清單。

顯示的建立日期與上次的每日快照相符。 換言之，如果您建立新的目的地，則在拍攝下一個快照之前，它不會出現在清單中。

從Widget上顯示的清單中選取目的地的名稱，可帶您前往目的地詳細資料，其連結來自 **[!UICONTROL 瀏覽]** 標籤。 您也可以選取 **[!UICONTROL 檢視全部]** 導覽至 **[!UICONTROL 瀏覽]** 標籤，然後選取目的地名稱以檢視其詳細資訊。

若要進一步瞭解如何設定特定型別的目的地，請造訪 [目的地檔案](../../destinations/home.md).

![「目標」儀表板的「總覽」索引標籤，會醒目顯示最近建立的目標Widget。](../images/destinations/recently-created-destinations.png)

### [!UICONTROL 最近啟動的對象] {#recently-activated-audiences}

>[!CONTEXTUALHELP]
>id="platform_dashboards_destinations_recentlyactivatedsegments"
>title="最近啟動的對象"
>abstract="此介面工具會提供最近對應至目的地的對象清單。此清單會提供系統中正積極使用的對象和目的地的快照，能有助於對任何錯誤的對應進行移難排解。"

此 **[!UICONTROL 最近啟用的對象]** widget提供最近對應至目的地的對象清單。 此清單會提供系統中正積極使用的對象和目的地的快照，能有助於對任何錯誤的對應進行移難排解。

此 [!UICONTROL 已更新] 顯示的日期顯示上次將對象啟動至目的地的時間，而且準確顯示上次的每日快照。 換言之，如果您對目的地啟用對象，則更新日期要等到拍攝下一個快照之後才會變更。

從Widget上顯示的清單中選取對象名稱，可帶您前往對象詳細資料。 您也可以選取 **[!UICONTROL 檢視全部]** 導覽至 [!UICONTROL 受眾] [!UICONTROL 瀏覽] 標籤，然後選取對象名稱以檢視其詳細資訊。

如需在Experience Platform中使用對象的詳細資訊，請參閱 [Segmentation Service概述](../../segmentation/home.md).

![目標儀表板的「總覽」索引標籤，並反白顯示最近啟用的對象Widget。](../images/destinations/recently-activated-audiences.png)

### [!UICONTROL 最近啟動的對象 (依目的地)] {#recently-activated-audiences-by-destination}

>[!CONTEXTUALHELP]
>id="platform_dashboards_destinations_recentlyactivatedsegmentsbydestination"
>title="最近啟動的對象 (依目的地)"
>abstract="此介面工具會根據在概觀下拉選單中選擇的目的地以遞減順序顯示最近啟動的前五個對象。"

此 **[!UICONTROL 目的地最近啟用的對象]** widget會根據在概述下拉式清單中選取的目的地，以遞減順序顯示最近啟用的前五個對象。 它類似於 [!UICONTROL 最近啟用的對象] Widget，但顯示的資料 **僅限** 套用至選取的目的地。

此Widget包含兩個量度：對象名稱和上次將對象啟動至目的地的日期。 顯示的資料與上次的每日快照相同。

您可以從顯示的清單中選取對象名稱，以檢視對象詳細資訊。

![依目的地Widget區分的最近啟用對象。](../images/destinations/recently-activated-audiences-by-destination.png)

請參閱「 」的先決條件一節 [使用的字詞定義](#prerequisites) 在此說明中。

### [!UICONTROL 對象規模趨勢] {#audience-size-trend}

>[!CONTEXTUALHELP]
>id="platform_dashboards_destinations_audiencesizetrend"
>title="對象規模趨勢"
>abstract="此介面工具會說明對象中包含的設定檔數量，這會每天傳送到目的地帳戶。第一個下拉選單會調整對象趨勢的時段。第二個介面工具下拉選單會選取要分析的對象。可從概觀的下拉選單中選擇目的地。"

此 **[!UICONTROL 對象人數趨勢]** Widget針對已對應至目的地帳戶的對象，描述一段時間內設定檔計數的關係。 Widget使用折線圖來說明對象中包含且每日傳送至目的地帳戶的設定檔數量。

過去30天、90天或12個月的對象趨勢時段，可使用第一個下拉式功能表調整。

第二個下拉式功能表會列出所有可傳送至控制面板頂端所選目的地帳戶的可用對象。

![對象人數趨勢Widget。](../images/destinations/audience-size-trend.png)

此 **[!UICONTROL 對象人數趨勢]** Widget提供 [!UICONTROL 註解] 按鈕。 選取 **[!UICONTROL 註解]** 以開啟自動註解對話方塊。 機器學習模型會藉由分析圖表和受眾資料來自動產生標題，以說明關鍵趨勢和重要事件。

![對象人數趨勢Widget的自動註解對話方塊。](../images/destinations/audience-size-trend-captions.png)

### [!UICONTROL 未對應對象 (依身分識別)] {#unmapped-audiences-by-identity}

>[!CONTEXTUALHELP]
>id="platform_dashboards_destinations_unmappedsegmentsbyidentity"
>title="未對應對象 (依身分識別)"
>abstract="此介面工具會針對特定目的地和身分識別列出依遞減的身分識別計數排名的前五個&#x200B;**未對應**&#x200B;對象。介面工具下拉選單中列出的篩選器 ID 會根據在概觀頁面頂端選取的目的地帳戶而變更。"

此 **[!UICONTROL 依身分割槽分的未對應對象]** widget列出前五名 **未對應** 依指定目的地和身分的遞減身分計數排名的對象。 它會根據所選的ID反白標示對對應至所選目的地帳戶最有利的受眾。

目的地ID下拉式清單會篩選您的可用對象。 下拉式清單中列出的篩選器ID會隨著在概覽頁面頂端選取的目的地帳戶而改變。

身分欄會計算對象中，可能對應至在Widget ID下拉式選單中所選ID的來源ID數量。

![「依身分割槽分的未對應對象」Widget。](../images/destinations/unmapped-audiences-by-identity.png)

請參閱「 」的先決條件一節 [使用的字詞定義](#prerequisites) 在此說明中。

### [!UICONTROL 已對應對象 (依身分識別)] {#mapped-audiences-by-identity}

>[!CONTEXTUALHELP]
>id="platform_dashboards_destinations_mappedsegmentsbyidentity"
>title="已對應對象 (依身分識別)"
>abstract="此介面工具會提供前五個&#x200B;**已對應**&#x200B;對象的清單。該清單會根據對象中包含的來源 ID 的數量由高至低排序。要計算的目的地 ID 會從介面工具標題下方的下拉選單中選取。此介面工具下拉選單中可用的目的地 ID 會依據在概觀儀表板頂部選擇的目的地而定。"

此介面工具會提供前五個&#x200B;**已對應**&#x200B;對象的清單。該清單會根據對象中包含的來源 ID 的數量由高至低排序。要計算的目的地 ID 會從介面工具標題下方的下拉選單中選取。Widget中下拉式清單可用的目的地ID會根據在總覽儀表板頂端選取的目的地帳戶篩選器而變更。

![依身分識別的Widget對應的對象。](../images/destinations/mapped-audiences-by-identity.png)

此 **[!UICONTROL 依身分對應的對象]** widget強調一覽，在所選目的地內成功鎖定促銷活動之設定檔商機的可能性。 有效率的鎖定目標行銷活動不取決於傳送至目的地的設定檔數量，而是取決於與目的地ID可能相符的來源ID數量，藉以提供有用且可操作的資料。

### 常見對象 {#common-audiences}

>[!CONTEXTUALHELP]
>id="platform_dashboards_destinations_commonaudiences"
>title="常見對象"
>abstract="此介面工具會提供在頁面頂端選擇的目的地帳戶中啟動的前五個對象的清單，以及在介面工具下拉選單中選取的目的地。對象清單會根據啟動的時間排序。啟動時間最近的對象會顯示在頂端。"

此 **[!UICONTROL 通用對象]** widget提供在頁面頂端所選目的地帳戶中啟用的前五個對象的清單，以及在介面工具下拉式清單中選取的目的地。 對象清單會根據啟動的時間排序。啟動時間最近的對象會顯示在頂端。

此 [!UICONTROL 對象人數] 欄提供每個列出對象的設定檔總數。

![通用對象Widget。](../images/destinations/common-audiences.png)

### 對應的對象 {#mapped-audiences}

此 [!UICONTROL 對應的對象] widget會顯示可在頁面頂端選取的目的地啟用的對應對象總數。

選取 **[!UICONTROL 受眾]** 導覽至「對象」控制面板 [!UICONTROL 瀏覽] 標籤。 此工作區會顯示貴組織的所有區段定義清單。

![對應的對象Widget。](../images/destinations/mapped-audiences.png)

### 已對應對象的健康情況 {#mapped-audience-health}

>[!CONTEXTUALHELP]
>id="platform_dashboards_destinations_mappedaudiencehealth"
>title="已對應對象的健康情況"
>abstract="此介面工具會提供最多包含 20 個已對應對象的清單，這些對象的總設定檔計數和對應至該目的地的 30 天平均對象規模至少有一個標準差的因素偏差。這會為過去 30 天內對象規模和平均值的差異提供計算量度。對象規模的排序為由高至低。"

Widget提供最多20個對應對象的清單，這些對應對象截至上次每日快照的設定檔總數與對應至該目的地的30天平均對象人數至少有一個標準差。

簡言之，它提供過去30天平均值之受眾人數分散的計算量度。 它會比較今天的對象人數是否超過過去30天資料中所顯示的歷史標準差。

系統中的所有受眾規模都是從高到低的受眾規模排序，如 [!UICONTROL 最新大小] 欄。

如果您的對應對象設定檔計數超過過去30天內對映設定檔大小平均值的標準差，這表示系統中出現異常，應加以調查。

如果對象在 [!UICONTROL 對應的對象健康狀況] Widget偏差較大，您應該參考對象人數趨勢圖表，並找出異常對象。 趨勢可讓您更深入瞭解對象的健康情況。

>[!NOTE]
>
>對應對象健康情況Widget的預設大小可能會阻礙表格資訊。 請修改Widget的大小，以改善對應對象名稱和欄標題的清晰度。 如需相關指引，請參閱修改控制面板檔案 [如何調整Widget的大小](../customize/modify.md).

![對應的對象健康狀態Widget。](../images/destinations/mapped-audience-health.png)

### [!UICONTROL 目的地計數] {#destinations-count}

>[!CONTEXTUALHELP]
>id="platform_dashboards_destinations_destinationscount"
>title="目的地計數"
>abstract="此介面工具會提供可以在系統內啟動和傳遞對象的可用端點總數。此數字包括使用中和非使用中的目的地。"

此 [!UICONTROL 目的地計數] widget提供可在系統中啟用及傳遞對象的可用端點總數。 此數字包括使用中和非使用中的目的地。

在總計數之下，選取 **[!UICONTROL 目的地]** 導覽至「目的地瀏覽」標籤。 此頁面列出您目前為止已建立連線的所有目的地。

![目的地計數Widget。](../images/destinations/destinations-count.png)

### [!UICONTROL 目的地狀態] {#destination-status}

此 [!UICONTROL 目的地狀態] widget會將啟用的目的地總數顯示為單一量度，並使用環形圖來說明啟用與停用目的地之間的比例差異。

當游標暫留在環圈圖的個別區段上時，啟用或停用目的地的個別計數會顯示在對話方塊中。

![目的地狀態Widget。](../images/destinations/destination-status.png)

### [!UICONTROL 依目的地平台區分的有效目的地] {#active-destinations-by-destination-platform}

Widget提供兩欄表格，顯示作用中目的地平台清單及每個目的地平台的作用中目的地總數。 目的地平台清單的順序是從高到低。

![依目的地平台Widget區分的有效目的地。](../images/destinations/active-destinations-by-destination-platform.png)

### [!UICONTROL 跨所有目的地的已啟用對象] {#activated-audiences-across-all-destinations}

此 [!UICONTROL 跨所有目的地的已啟用對象] widget會提供在單一量度中，針對所有目的地啟用的對象總數。 此數字與最近的快照相符。

![跨所有目的地Widget的已啟動對象。](../images/destinations/activated-audiences-across-all-destinations.png)

選取 **[!UICONTROL 受眾]** 以導覽至目的地 [!UICONTROL 瀏覽] 標籤。 此頁面提供所有已啟用目的地的清單以及各種相關量度。 請參閱檔案以取得以下專案的詳細資訊： [[!UICONTROL 瀏覽] 標籤](../../destinations/ui/destinations-workspace.md#browse).

請參閱「 」的先決條件一節 [使用的字詞定義](#prerequisites) 在此說明中。

### [!UICONTROL 啟用的對象] {#activated-audiences}

此Widget針對啟用至目的地的對象總數提供單一量度。

![啟用的對象Widget。](../images/destinations/activated-audiences.png)

選取 **[!UICONTROL 受眾]** 導覽至目的地控制面板的詳細資訊頁面。 此 [!UICONTROL 啟用資料] 標籤會顯示已對應至目標的對象清單，包括其開始日期和結束日期（如果適用），以及資料匯出的其他相關資訊，例如匯出型別、排程和頻率。 若要檢視特定對象的詳細資訊，請從以下位置選取其名稱： [!UICONTROL 對象名稱] 欄。

![目標儀表板詳細資訊頁面中醒目提示「啟用資料」索引標籤。](../images/destinations/activation-data-tab.png)

此Widget可協助您根據一目瞭然啟用的對象數，瞭解目的地的價值。 它也能讓您輕鬆存取更多詳細資訊，以便進一步分析。

請參閱「 」的先決條件一節 [使用的字詞定義](#prerequisites) 在此說明中。

## 後續步驟

依照本檔案操作，您現在應該能夠找到目的地控制面板，並瞭解可用介面工具列中顯示的量度。 若要進一步瞭解如何在Experience Platform中使用目的地，請參閱 [目的地檔案](../../destinations/home.md).
