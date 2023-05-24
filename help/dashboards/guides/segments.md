---
keywords: Experience Platform；配置檔案；段；段；分段；用戶介面；UI；自定義；段儀表板；儀表板
title: 段儀表板指南
description: Adobe Experience Platform提供了一個控制板，您可以通過該控制板查看有關您的組織建立的段的重要資訊。
type: Documentation
exl-id: de5e07bc-2c44-416e-99db-7607059117cb
source-git-commit: 34e0381d40f884cd92157d08385d889b1739845f
workflow-type: tm+mt
source-wordcount: '2105'
ht-degree: 7%

---

# [!UICONTROL 段] 儀表板 {#segment-dashboard}

Adobe Experience Platform用戶介面(UI)提供了一個儀表板，您可以通過該儀表板查看有關資料段的重要資訊，這些資訊在每日快照期間捕獲。 本指南概述了如何訪問和使用UI中的段儀表板，並提供了有關儀表板中顯示的可視化效果的詳細資訊。

有關平台用戶介面中Adobe Experience Platform分段服務的所有功能的概述，請訪問 [分段服務UI指南](../../segmentation/ui/overview.md)。

## [!UICONTROL 段] 儀表板資料

段控制板顯示您的組織在「配置檔案」儲存中Experience Platform的屬性（記錄）資料的快照。 快照不包括任何事件（時間系列）資料。

快照中的屬性資料與拍攝快照時在特定時間點顯示的資料完全相同。 換句話說，快照不是資料的近似值或示例，而且段儀表板不會即時更新。

>[!NOTE]
>
>自拍攝快照以來對資料所做的任何更改或更新不會反映在儀表板中，直到拍攝下一個快照。

## 瀏覽 [!UICONTROL 段] 儀表板 {#explore}

導航到 [!UICONTROL 段] 平台UI中的儀表板，選擇 **[!UICONTROL 段]** 在左滑軌中，選擇 **[!UICONTROL 概述]** 頁籤。

>[!NOTE]
>
>如果您的組織是新加入平台的，並且尚未建立活動的配置檔案資料集或合併策略， [!UICONTROL 段] 儀表板不可見。 相反， [!UICONTROL 概述] 頁籤顯示幫助您開始分段的連結和文檔。

![「段」操控板「概述」(Overview)頁籤，其中「段」(Segments)和「概述」(Overview)突出顯示。](../images/segments/dashboard-overview.png)

### 修改 [!UICONTROL 段] 儀表板 {#modify}

可修改 [!UICONTROL 段] 通過選擇 **[!UICONTROL 修改儀表板]**。 這使您能夠從儀表板中移動、添加和刪除小部件，以及訪問 **[!UICONTROL 小部件庫]** 瀏覽可用小部件並為您的組織建立自定義小部件。

請參閱 [修改儀表板](../customize/modify.md) 和 [小部件庫概述](../customize/widget-library.md) 文檔以瞭解詳細資訊。

### 添加小部件 {#add-widget}

選擇 **[!UICONTROL 添加小部件]** 導航到小部件庫，並查看要添加到儀表板的可用小部件的清單。

![「段」儀表板概述，「添加」構件突出顯示。](../images/segments/segments-overview-add-widget.png)

從小部件庫中，可以瀏覽選擇的標準小部件和自定義小部件。有關如何添加小部件的資訊，請參閱小部件庫文檔，瞭解如何 [添加小部件](../customize/widget-library.md#add-widgets)。

## 選擇段

操控板會自動選擇要顯示的段，但是，您可以使用下拉菜單或段選擇器更改段。

要選擇其他段，請選擇段名稱旁邊的下拉清單或使用段選擇器開啟段選擇對話框。

>[!IMPORTANT]
>
>只有輪廓計數大於零的段才顯示在可選段清單中。

![「段」操控板概述，全局段下拉菜單突出顯示。](../images/segments/change-segment.png)

![「選擇段」(Select segment)對話框，其中顯示所有可用段。](../images/segments/select-segment-dialog.png)

## 小部件和度量

段控制板由小部件組成，這些部件是只讀度量，提供有關所選段的重要資訊。

最近快照的日期和時間顯示在 [!UICONTROL 概述] 頁籤。 截至該日期和時間，所有小部件資料都準確。 快照的時間戳以UTC提供；它不在單個用戶或組織的時區中。

![突出顯示了小部件時間戳的「段概述」頁籤。](../images/segments/widget-timestamp.png)

## 標準小部件 {#standard-widgets}

Adobe提供了多個標準小部件，您可以使用這些小部件來可視化與段相關的不同度量。 您也可以使用 [!UICONTROL 小部件庫]。 要瞭解有關建立自定義小部件的詳細資訊，請首先閱讀 [小部件庫概述](../customize/widget-library.md)。

要瞭解有關每個可用標準小部件的詳細資訊，請從以下清單中選擇小部件的名稱：

* [[!UICONTROL 對象規模]](#audience-size)
* [[!UICONTROL 受眾激活順序]](#audience-activation-order)
* [[!UICONTROL 對象規模趨勢]](#audience-size-trend)
* [[!UICONTROL 受眾大小變化趨勢]](#audience-size-change-trend)
* [[!UICONTROL 按身份分類的受眾規模趨勢]](#audience-size-trend-by-identity)
* [[!UICONTROL 受眾重疊]](#audience-overlap)
* [[!UICONTROL 受眾重疊報告]](#audience-overlap-report)
* [[!UICONTROL 身分識別覆蓋]](#identity-overlap)
* [[!UICONTROL 依身分識別劃分的設定檔]](#profiles-by-identity)
* [[!UICONTROL 計畫激活]](#scheduled-activations)

### [!UICONTROL 對象規模] {#audience-size}

>[!CONTEXTUALHELP]
>id="platform_dashboards_segments_audiencesize"
>title="對象規模"
>abstract="此 Widget 會顯示選取區段內合併設定檔的總數。此數字會依據套用於您的資料的合併原則而定，並且在最近快照時是正確的。"

的 **[!UICONTROL 受眾大小]** 構件顯示拍攝快照時選定段內合併的配置檔案總數。 此數字是將段合併策略應用於配置檔案資料的結果，以便將配置檔案片段合併到一起，為段中的每個個體形成單個配置檔案。

有關碎片和合併配置檔案的詳細資訊，請參閱 [即時客戶概要資訊概述](../../profile/home.md)。

![「段」儀表板概述，「受眾大小」構件突出顯示。](../images/segments/audience-size.png)

### [!UICONTROL 對象規模趨勢] {#audience-size-trend}

>[!CONTEXTUALHELP]
>id="platform_dashboards_segments_audiencesizetrend"
>title="對象規模趨勢"
>abstract="此 Widget 會提供有關符合&#x200B;**任何**&#x200B;區段定義標準的設定檔總數的資訊，這會在過去 30 天、90 天或 12 個月每日快照期間擷取。"

的 **[!UICONTROL 受眾規模趨勢]** 構件提供了符合以下條件的配置檔案總數的線形圖圖 **任何** 段定義。 觀眾人數趨勢可以在30天、90天和12個月期間進行可視化。 時間段從小部件的下拉菜單中選擇。 觀眾大小反映在y軸上，時間反映在x軸上。

此小部件還包括自動 [!UICONTROL 字幕] 其中機器學習模型分析圖表和分段資料並自動生成字幕以描述關鍵趨勢和重要事件。 選擇 **[!UICONTROL 字幕]** 的子菜單。

![「段」概述顯示「受眾大小」趨勢構件。](../images/segments/audience-size-trend-captions.png)

此時將開啟自動字幕對話框，提供有關資料的見解。

![「受眾大小趨勢」小部件的自動字幕對話框。](../images/segments/audience-size-trend-automatic-captions-dialog.png)

要瞭解有關段評估的詳細資訊以及配置檔案如何限定和退出段，請參閱 [分段服務文檔](../../segmentation/home.md)。

### [!UICONTROL 受眾大小變化趨勢] {#audience-size-change-trend}

此小部件提供線形圖圖，說明在最近的每日快照之間限定給定段的配置檔案總數之間的差異。 從「概述」(overview)下拉清單中選擇了用於分析的段。 趨勢分析期可以在30天、90天和12個月期間顯示。 時間段從小部件的下拉菜單中選擇。 觀眾大小反映在y軸上，時間反映在x軸上。

![「受眾大小」更改趨勢小部件。](../images/segments/audience-size-change-trend.png)

### [!UICONTROL 按身份分類的受眾規模趨勢] {#audience-size-trend-by-identity}

此小部件根據從小部件下拉菜單中選擇的標識類型，說明特定段的受眾大小趨勢。 用於分析的段是從概述下拉清單中選擇的。 趨勢分析期可以在30天、90天和12個月期間顯示。 時間段從小部件的下拉菜單中選擇。

![按身份小部件顯示的受眾大小趨勢。](../images/segments/audience-size-trend-by-identity.png)

### [!UICONTROL 受眾激活順序] {#audience-activation-order}

的 [!UICONTROL 受眾激活順序] 小部件提供了一個三清單，其中列出了 [!UICONTROL 目標名稱]，也請參見Wiki頁。 [!UICONTROL 平台]，並激活 [!UICONTROL 日期] 觀眾中。 清單根據頻率從高到低排序，最多可容納10行。

![受眾激活順序構件。](../images/segments/audience-activation-order.png)

### [!UICONTROL 受眾重疊] {#audience-overlap}

此構件表示兩個段中滿足兩個段定義條件的配置檔案數。 用於比較的段是從構件下拉菜單中選擇的。 通過懸停在圓上或Venn圖的交點上，可以看到相關段定義中包含的輪廓總數。

此小部件使您能夠通過可視化段定義結果中的相似性來優化分割策略。

![受眾重疊小部件。](../images/segments/audience-overlap.png)

### [!UICONTROL 受眾重疊報告] {#audience-overlap-report}

此小部件將特定段的受眾重疊資料清單化。 從螢幕頂部的下拉菜單中選擇的段提供了從最高到最低重疊百分比排列的五個受眾的清單。 為了清晰起見，您選擇的網段列在 [!UICONTROL 段名稱] 的雙曲餘切值。 為第二分部提供觀眾重疊分析。 [!UICONTROL 段B名稱] 的雙曲餘切值。 在第三列中提供的重疊百分比精確到十二位小數。

受眾重疊報告可幫助您構建新的高效能網段。 通過觀察高百分比重疊，可以抑制觀眾並防止將同一觀眾發送到不同的目標。 它們還有助於您識別隱藏的洞察力，這些洞察力有助於更好地分割。 低百分比重疊有助於查找要追蹤的獨特配置檔案。

選擇 **[!UICONTROL 查看更多]** 開啟包含更多段重疊資料的全屏對話框。

![「受眾」重疊報表構件，「查看」則更加突出顯示。](../images/segments/audience-overlap-report.png)

的 [!UICONTROL 受眾重疊報告] 對話框。 此對話框最多可包含50行受眾重疊分析，分為六列。 選擇設定表徵圖(![設定表徵圖。](../images/segments/settings-icon.png))以從表中刪除或添加列。

![「受眾重疊報告」對話框。](../images/segments/audience-overlap-report-dialog.png)

>[!NOTE]
>
>選擇 **[!UICONTROL 重疊]** 列標題，將結果的排名從最高到最低或從最低更改為最高。

要以PDF格式下載整個報告，請選擇「選項」菜單(**`...`**)後跟 **[!UICONTROL 下載]**。

![「觀眾重疊」報告對話框，並突出顯示了省略號和「下載」選項。](../images/segments/segments-audience-overlap-report-dialog-download.png)

從報表中選擇一行以開啟重疊分析的Venn圖。 將滑鼠懸停在Venn圖的一部分上，以在對話框中查看配置檔案計數。

![「受眾」報告對話框與「參數」圖和突出顯示的行重疊。](../images/segments/audience-overlap-report-dialog-venn.png)

選擇 **[!UICONTROL 關閉]** 返回 [!UICONTROL 段] 控制項欄。

### [!UICONTROL 身分識別覆蓋] {#identity-overlap}

>[!CONTEXTUALHELP]
>id="platform_dashboards_segments_identityoverlap"
>title="身分識別覆蓋"
>abstract="此 Widget 會顯示包含兩個所選身分識別的區段中設定檔的覆蓋。圓圈會顯示每個身分識別的相對大小。包含兩個命名空間的設定檔的數量由圓圈之間的覆蓋表示。"

的 **[!UICONTROL 身份重疊]** 小部件顯示一個Venn圖或設定圖，顯示包含多個標識的段中配置檔案的重疊。

使用小部件上的下拉菜單選擇要比較的身份。 圓顯示每個所選標識的相對大小，其中包含兩個命名空間的配置檔案的數目由圓之間重疊的大小表示。

如果客戶在多個渠道上與您的品牌進行交互，則多個身份將與該個別客戶關聯，因此您的組織很可能具有多個配置檔案，其中包含來自多個身份的片段。

要瞭解有關身份的詳細資訊，請訪問 [Adobe Experience Platform身份服務文檔](../../identity-service/home.md)。

![突出顯示了「段」儀表板的「標識重疊」構件概述。](../images/segments/identity-overlap.png)

### [!UICONTROL 依身分識別劃分的設定檔] {#profiles-by-identity}

>[!CONTEXTUALHELP]
>id="platform_dashboards_segments_profilesbyidentity"
>title="依身分識別劃分的設定檔"
>abstract="此 Widget 會顯示選取區段中每個合併設定檔身分識別的劃分。"

的 **[!UICONTROL 按身份顯示的配置檔案]** 小部件顯示選定段中每個合併配置檔案的標識細目。 按標識列出的配置檔案總數可能高於段中的配置檔案總數，因為一個配置檔案可能具有與其關聯的多個標識。 換句話說，將每個身份顯示的值加在一起，可能總和會超過網段中的總受眾規模，因為如果客戶在多個渠道與您的品牌進行交互，則多個身份可能與該個別客戶相關聯。

選擇 **[!UICONTROL 字幕]** 的子菜單。

![「段」儀表板概述，「按身份構件配置的概要檔案」和「標題」選項突出顯示。](../images/segments/profiles-by-identity.png)

機器學習模型通過分析資料的總體分佈和關鍵維度自動生成資料洞察力。

要瞭解有關身份的詳細資訊，請訪問 [Adobe Experience Platform身份服務文檔](../../identity-service/home.md)。

### 計畫激活 {#scheduled-activations}

的 [!UICONTROL 計畫激活] 小部件提供了最近激活的目標的表格化視圖。 該表包括目標平台、到此目標的激活流的名稱以及所選段的激活開始和結束日期。 如果沒有為激活提供結束日期，則顯示為 [!UICONTROL 持續]。 從頁面頂部的下拉清單中選擇分析的段。

通過該小部件，您可以快速發現激活受眾的位置和時間，並使重複或不必要的激活更加透明。 這些累積的資訊還突出顯示了任何激活被排除的地方。

![計畫激活小部件。](../images/segments/scheduled-activations.png)

## 後續步驟

現在，通過遵循本文檔，您應該能夠找到段操控板並選擇要查看的段。 您還應瞭解可用小部件中顯示的度量。 要瞭解有關在Experience PlatformUI中使用段的詳細資訊，請參閱 [分段服務UI指南](../../segmentation/ui/overview.md)。
