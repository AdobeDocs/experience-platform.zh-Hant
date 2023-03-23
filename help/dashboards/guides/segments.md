---
keywords: Experience Platform；設定檔；區段；區段；使用者介面；UI；自訂；區段控制面板；控制面板
title: 區段控制面板指南
description: Adobe Experience Platform提供控制面板，供您檢視貴組織已建立區段的重要資訊。
type: Documentation
exl-id: de5e07bc-2c44-416e-99db-7607059117cb
source-git-commit: 34e0381d40f884cd92157d08385d889b1739845f
workflow-type: tm+mt
source-wordcount: '2105'
ht-degree: 7%

---

# [!UICONTROL 區段] 儀表板 {#segment-dashboard}

Adobe Experience Platform使用者介面(UI)提供控制面板，讓您透過控制面板檢視每日快照擷取之區段的重要資訊。 本指南概述如何存取和使用UI中的區段控制面板，並提供控制面板中所顯示視覺效果的詳細資訊。

如需Platform使用者介面中所有Adobe Experience Platform區段服務功能的概觀，請造訪 [區段服務UI指南](../../segmentation/ui/overview.md).

## [!UICONTROL 區段] 控制面板資料

區段控制面板會顯示您的組織在「設定檔」存放區內Experience Platform的屬性（記錄）資料快照。 快照不包含任何事件（時間系列）資料。

快照中的屬性資料與建立快照時在特定時間點顯示的資料完全相同。 換句話說，快照不是資料的近似值或樣本，而且區段控制面板不會即時更新。

>[!NOTE]
>
>自拍攝快照以來對資料所做的任何更改或更新都不會反映在儀表板中，直到拍攝下一個快照。

## 探索 [!UICONTROL 區段] 儀表板 {#explore}

導覽至 [!UICONTROL 區段] 平台UI中的控制面板，請選取 **[!UICONTROL 區段]** 在左側邊欄中，選取 **[!UICONTROL 概述]** 標籤來顯示控制面板。

>[!NOTE]
>
>如果您的組織剛接觸Platform，且尚未建立作用中的設定檔資料集或合併原則，請 [!UICONTROL 區段] 控制面板未顯示。 反之， [!UICONTROL 概述] 索引標籤會顯示可協助您開始使用區段的連結和檔案。

![區段控制面板概述標籤會反白顯示區段和概述。](../images/segments/dashboard-overview.png)

### 修改 [!UICONTROL 區段] 儀表板 {#modify}

您可以修改 [!UICONTROL 區段] 控制面板，選取 **[!UICONTROL 修改控制面板]**. 這可讓您從控制面板移動、新增和移除小工具，以及存取 **[!UICONTROL 介面工具集程式庫]** 探索可用的介面工具集，並為貴組織建立自訂介面工具集。

請參閱 [修改控制面板](../customize/modify.md) 和 [介面工具集程式庫概觀](../customize/widget-library.md) 檔案以深入了解。

### 新增介面工具集 {#add-widget}

選擇 **[!UICONTROL 新增介面工具集]** 導覽至介面工具集庫，並查看可新增至控制面板的可用介面工具集清單。

![區段控制面板概觀，並反白顯示新增介面工具集。](../images/segments/segments-overview-add-widget.png)

從介面工具集庫中，您可以瀏覽標準和自定義段介面工具集的選擇。有關如何添加介面工具集的資訊，請參閱介面工具集庫文檔，了解如何 [新增介面工具集](../customize/widget-library.md#add-widgets).

## 選取區段

控制面板會自動選取要顯示的區段，但您可以使用下拉式功能表或區段選取器來變更區段。

若要選擇不同的區段，請選取區段名稱旁的下拉式清單，或使用區段選取器開啟區段選取對話方塊。

>[!IMPORTANT]
>
>選取區段清單中只會顯示設定檔計數超過零的區段。

![區段控制面板概觀，會強調顯示全域區段下拉式功能表。](../images/segments/change-segment.png)

![顯示所有可用區段的「選取區段」對話方塊。](../images/segments/select-segment-dialog.png)

## Widget和量度

區段控制面板由Widget組成，Widget是唯讀量度，提供與您所選區段相關的重要資訊。

最新快照的日期和時間會顯示在 [!UICONTROL 概述] 標籤。 自該日期和時間起，所有介面工具集資料都是準確的。 快照的時間戳以UTC提供；不在個別使用者或組織的時區。

![區段概述標籤會強調顯示介面工具集時間戳記。](../images/segments/widget-timestamp.png)

## 標準介面工具集 {#standard-widgets}

Adobe提供多個標準Widget，您可用來視覺化與區段相關的不同量度。 您也可以使用 [!UICONTROL 介面工具集程式庫]. 若要進一步了解建立自訂Widget，請先閱讀 [介面工具集程式庫概觀](../customize/widget-library.md).

若要進一步了解每個可用的標準介面工具集，請從下列清單中選取介面工具集的名稱：

* [[!UICONTROL 對象規模]](#audience-size)
* [[!UICONTROL 對象啟動順序]](#audience-activation-order)
* [[!UICONTROL 對象規模趨勢]](#audience-size-trend)
* [[!UICONTROL 對象大小變更趨勢]](#audience-size-change-trend)
* [[!UICONTROL 受眾規模（依身分）趨勢]](#audience-size-trend-by-identity)
* [[!UICONTROL 對象重疊]](#audience-overlap)
* [[!UICONTROL 對象重疊報表]](#audience-overlap-report)
* [[!UICONTROL 身分識別覆蓋]](#identity-overlap)
* [[!UICONTROL 依身分識別劃分的設定檔]](#profiles-by-identity)
* [[!UICONTROL 已排程的啟動]](#scheduled-activations)

### [!UICONTROL 對象規模] {#audience-size}

>[!CONTEXTUALHELP]
>id="platform_dashboards_segments_audiencesize"
>title="對象規模"
>abstract="此 Widget 會顯示選取區段內合併設定檔的總數。此數字會依據套用於您的資料的合併原則而定，並且在最近快照時是正確的。"

此 **[!UICONTROL 對象大小]** 介面工具集會顯示拍攝快照時，所選區段內合併的設定檔總數。 此數字是將區段合併原則套用至您的設定檔資料的結果，以便將設定檔片段合併在一起，為區段中的每個個人形成單一設定檔。

如需片段和已合併設定檔的詳細資訊，請參閱 [即時客戶個人檔案概觀](../../profile/home.md).

![區段控制面板概述，並反白顯示對象大小介面工具集。](../images/segments/audience-size.png)

### [!UICONTROL 對象規模趨勢] {#audience-size-trend}

>[!CONTEXTUALHELP]
>id="platform_dashboards_segments_audiencesizetrend"
>title="對象規模趨勢"
>abstract="此 Widget 會提供有關符合&#x200B;**任何**&#x200B;區段定義標準的設定檔總數的資訊，這會在過去 30 天、90 天或 12 個月每日快照期間擷取。"

此 **[!UICONTROL 對象大小趨勢]** 介面工具集提供符合以下條件的設定檔總數的折線圖插圖： **any** 指定時段的區段定義。 對象大小趨勢可以在30天、90天和12個月期間內視覺化。 時段是從介面工具集的下拉式選單中選擇。 對象大小會反映在Y軸上，而時間會反映在X軸上。

此介面工具集也包含自動 [!UICONTROL 字幕] 其中，機器學習模型會分析圖表和區段資料並自動產生字幕，以描述主要趨勢和重要事件。 選擇 **[!UICONTROL 字幕]** 開啟自動字幕對話框。

![「區段」概觀會顯示對象大小趨勢Widget。](../images/segments/audience-size-trend-captions.png)

自動字幕對話方塊隨即開啟，提供您資料的深入分析。

![「對象大小」趨勢Widget的自動字幕對話方塊。](../images/segments/audience-size-trend-automatic-captions-dialog.png)

若要進一步了解區段評估，以及設定檔如何限定和退出區段，請參閱 [區段服務檔案](../../segmentation/home.md).

### [!UICONTROL 對象大小變更趨勢] {#audience-size-change-trend}

此介面工具集提供折線圖圖示，說明在最近的每日快照中符合指定區段資格的設定檔總數之間的差異。 從「概述」下拉式清單中選取了選擇進行分析的區段。 趨勢分析的期間可以視覺化為30天、90天和12個月期間。 時段是從介面工具集的下拉式選單中選擇。 對象大小會反映在Y軸上，而時間會反映在X軸上。

![對象大小變更趨勢介面工具集。](../images/segments/audience-size-change-trend.png)

### [!UICONTROL 受眾規模（依身分）趨勢] {#audience-size-trend-by-identity}

此介面工具集會根據從介面工具集下拉式功能表中選擇的身分類型，來說明特定區段的對象大小趨勢。 用於分析的區段是從概述下拉式清單中選取。 趨勢分析的期間可以視覺化為30天、90天和12個月期間。 時段是從介面工具集的下拉式選單中選擇。

![依身分介面工具集的受眾大小趨勢。](../images/segments/audience-size-trend-by-identity.png)

### [!UICONTROL 對象啟動順序] {#audience-activation-order}

此 [!UICONTROL 對象啟動順序] 介面工具集提供三欄表格，列出 [!UICONTROL 目的地名稱], [!UICONTROL 平台]，和啟動 [!UICONTROL 日期] 觀眾。 清單會根據最近一次從高到低排序，最多可容納10列。

![Audience啟動順序介面工具集。](../images/segments/audience-activation-order.png)

### [!UICONTROL 對象重疊] {#audience-overlap}

此介面工具集代表來自兩個區段的設定檔數，這些區段符合兩個區段定義的條件。 比較用的區段是從介面工具集下拉式功能表中選取。 將滑鼠游標暫留在社交圈或Venn圖表的交集上，即可查看相關區段定義中包含的設定檔總數。

此介面工具集可讓您透過將區段定義的結果中的相似性視覺化，來最佳化您的區段策略。

![對象重疊Widget。](../images/segments/audience-overlap.png)

### [!UICONTROL 對象重疊報表] {#audience-overlap-report}

此介面工具集會列出特定區段的受眾重疊資料。 針對從螢幕頂端的下拉式功能表中選擇的區段，提供從最高到最低重疊百分比排名的五個對象清單。 為清楚起見，您選取的區段會列於 [!UICONTROL 區段名稱] 欄。 會針對列於 [!UICONTROL 區段B名稱] 欄。 第三欄中提供的重疊百分比精確至十二位小數。

對象重疊報表可協助您建立新的高效能區段。 觀察高百分比重疊可讓您隱藏對象，並防止將相同的對象傳送至不同的目的地。 它們也可協助您識別隱藏的深入分析，以協助您改善細分。 低百分比重疊有助於找到要追蹤的唯一設定檔。

選擇 **[!UICONTROL 查看更多]** 以開啟包含更多區段重疊資料的全螢幕對話方塊。

![對象重疊報表介面工具集，以更醒目顯示檢視。](../images/segments/audience-overlap-report.png)

此 [!UICONTROL 對象重疊報表] 對話框。 此對話方塊最多可包含50列受眾重疊分析，分為六欄。 選取設定圖示(![設定圖示。](../images/segments/settings-icon.png))，移除或新增表格中的欄。

![對象重疊報表對話方塊。](../images/segments/audience-overlap-report-dialog.png)

>[!NOTE]
>
>選取 **[!UICONTROL 重疊]** 欄標題，將結果的排名從最高到最低或從最低到最高。

若要以PDF格式下載整個報表，請選取選項功能表(**`...`**)後面跟著 **[!UICONTROL 下載]**.

![「對象重疊報表」對話方塊中會強調顯示點與「下載」選項。](../images/segments/segments-audience-overlap-report-dialog-download.png)

從報表中選取一列，以開啟重疊分析的文氏圖表。 將滑鼠指標暫留在Venn圖表的某個區段上，即可在對話方塊中查看設定檔計數。

![對象重疊報表對話方塊中會顯示文氏圖表和醒目提示的列。](../images/segments/audience-overlap-report-dialog-venn.png)

選擇 **[!UICONTROL 關閉]** 返回 [!UICONTROL 區段] 控制面板。

### [!UICONTROL 身分識別覆蓋] {#identity-overlap}

>[!CONTEXTUALHELP]
>id="platform_dashboards_segments_identityoverlap"
>title="身分識別覆蓋"
>abstract="此 Widget 會顯示包含兩個所選身分識別的區段中設定檔的覆蓋。圓圈會顯示每個身分識別的相對大小。包含兩個命名空間的設定檔的數量由圓圈之間的覆蓋表示。"

此 **[!UICONTROL 身分重疊]** 介面工具集會顯示Venn圖表或設定圖表，顯示您包含多個身分的區段中設定檔的重疊。

使用介面工具集上的下拉式功能表，選取您要比較的身分。 社交圈會顯示每個所選身分的相對大小，包含兩個命名空間的設定檔數目會以社交圈之間重疊的大小表示。

如果客戶在多個管道上與您的品牌互動，則多個身分會與該個別客戶相關聯，因此您的組織可能會有多個設定檔，其中包含來自多個身分的片段。

若要進一步了解身分，請造訪 [Adobe Experience Platform Identity Service檔案](../../identity-service/home.md).

![區段控制面板概述，並反白顯示身分重疊Widget。](../images/segments/identity-overlap.png)

### [!UICONTROL 依身分識別劃分的設定檔] {#profiles-by-identity}

>[!CONTEXTUALHELP]
>id="platform_dashboards_segments_profilesbyidentity"
>title="依身分識別劃分的設定檔"
>abstract="此 Widget 會顯示選取區段中每個合併設定檔身分識別的劃分。"

此 **[!UICONTROL 依身分設定檔]** 介面工具集會顯示您所選區段中每個合併設定檔的身分劃分。 依身分劃分的設定檔總數可能高於區段中的設定檔總數，因為一個設定檔可能有多個與其相關聯的身分。 換句話說，將每個身分顯示的值加總後，可能會超過區段中的總受眾規模，因為如果客戶在多個管道上與您的品牌互動，則多個身分可能會與該個別客戶相關聯。

選擇 **[!UICONTROL 字幕]** 開啟自動字幕對話框。

![「區段」控制面板概觀，並反白顯示「依身分識別Widget設定檔」和「註解」選項。](../images/segments/profiles-by-identity.png)

機器學習模型會透過分析資料的整體分佈和關鍵維度，自動產生資料洞察。

若要進一步了解身分，請造訪 [Adobe Experience Platform Identity Service檔案](../../identity-service/home.md).

### 已排程的啟動 {#scheduled-activations}

此 [!UICONTROL 已排程的啟動] 介面工具集可提供最近啟動之目的地的表格檢視。 表格包含目標平台、您前往此目標的啟動流程名稱，以及所選區段的啟動開始和結束日期。 如果未提供啟動的結束日期，則會顯示為 [!UICONTROL 持續存在]. 要分析的區段是從頁面頂端的下拉式清單中選取。

介面工具集可讓您一目瞭然地探索對象啟動的位置和時機，讓重複或不必要的啟動更加透明。 此累積的資訊還突出顯示了任何激活被遺漏的位置。

![已排程的啟動介面工具集。](../images/segments/scheduled-activations.png)

## 後續步驟

依照本檔案操作，您現在應該能夠找到區段控制面板，並選取要檢視的區段。 您也應了解可用介面工具集中顯示的量度。 若要進一步了解如何在Experience PlatformUI中使用區段，請參閱 [區段服務UI指南](../../segmentation/ui/overview.md).
