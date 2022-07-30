---
keywords: Experience Platform；配置檔案；段；段；分段；用戶介面；UI；自定義；段儀表板；儀表板
title: 段操控板
description: 'Adobe Experience Platform提供了一個控制板，您可以通過該控制板查看有關您的組織建立的段的重要資訊。 '
type: Documentation
exl-id: de5e07bc-2c44-416e-99db-7607059117cb
source-git-commit: e1d44c453385b8beaa49e9793eb4858876d865b0
workflow-type: tm+mt
source-wordcount: '1597'
ht-degree: 0%

---

# 段操控板 {#segment-dashboard}

Adobe Experience Platform用戶介面(UI)提供了一個儀表板，您可以通過該儀表板查看有關資料段的重要資訊，這些資訊在每日快照期間捕獲。 本指南概述了如何訪問和使用UI中的段儀表板，並提供了有關儀表板中顯示的可視化效果的詳細資訊。

有關平台用戶介面中Adobe Experience Platform分段服務的所有功能的概述，請訪問 [分段服務UI指南](../../segmentation/ui/overview.md)。

## 段儀表板資料

段控制板顯示您的組織在「配置檔案」儲存中Experience Platform的屬性（記錄）資料的快照。 快照不包括任何事件（時間系列）資料。

快照中的屬性資料與拍攝快照時在特定時間點顯示的資料完全相同。 換句話說，快照不是資料的近似值或示例，而且段儀表板不會即時更新。

>[!NOTE]
>
>自拍攝快照以來對資料所做的任何更改或更新不會反映在儀表板中，直到拍攝下一個快照。

## 瀏覽段儀表板

導航到 [!UICONTROL 段] 平台UI中的儀表板，選擇 **[!UICONTROL 段]** 在左滑軌中，選擇 **[!UICONTROL 概述]** 頁籤。

>[!NOTE]
>
>如果您的組織是新加入平台的，並且尚未建立活動的配置檔案資料集或合併策略， [!UICONTROL 段] 儀表板不可見。 相反， [!UICONTROL 概述] 頁籤顯示幫助您開始分段的連結和文檔。

![](../images/segments/dashboard-overview.png)

### 修改 [!UICONTROL 段] 儀表板

可修改 [!UICONTROL 段] 通過選擇 **[!UICONTROL 修改儀表板]**。 這使您能夠從儀表板中移動、添加和刪除小部件，以及訪問 **[!UICONTROL 小部件庫]** 瀏覽可用小部件並為您的組織建立自定義小部件。

請參閱 [修改儀表板](../customize/modify.md) 和 [小部件庫概述](../customize/widget-library.md) 文檔以瞭解詳細資訊。

## 選擇段

操控板會自動選擇要顯示的段，但是，您可以使用下拉菜單或段選擇器更改段。

要選擇其他段，請選擇段名稱旁邊的下拉清單或使用段選擇器開啟段選擇對話框。

![](../images/segments/change-segment.png)

![](../images/segments/select-segment-dialog.png)

## 小部件和度量

段控制板由小部件組成，這些部件是只讀度量，提供有關所選段的重要資訊。

最近快照的日期和時間顯示在 [!UICONTROL 概述] 頁籤。 截至該日期和時間，所有小部件資料都準確。 快照的時間戳以UTC提供；它不在單個用戶或組織的時區中。

![突出顯示了小部件時間戳的「段概述」頁籤。](../images/segments/widget-timestamp.png)

## 標準小部件 {#standard-widgets}

Adobe提供了多個標準小部件，您可以使用這些小部件來可視化與段相關的不同度量。 您也可以使用 [!UICONTROL 小部件庫]。 要瞭解有關建立自定義小部件的詳細資訊，請首先閱讀 [小部件庫概述](../customize/widget-library.md)。

要瞭解有關每個可用標準小部件的詳細資訊，請從以下清單中選擇小部件的名稱：

* [[!UICONTROL 對象規模]](#audience-size)
* [[!UICONTROL 受眾激活順序]](#audience-activation-order)
* [[!UICONTROL 受眾規模趨勢]](#audience-size-trend)
* [[!UICONTROL 受眾大小變化趨勢]](#audience-size-change-trend)
* [[!UICONTROL 按身份分類的受眾規模趨勢]](#audience-size-trend-by-identity)
* [[!UICONTROL 受眾重疊]](#audience-overlap)
* [[!UICONTROL 身份重疊]](#identity-overlap)
* [[!UICONTROL 按身份顯示的配置檔案]](#profiles-by-identity)

### [!UICONTROL 對象規模] {#audience-size}

>[!CONTEXTUALHELP]
>id="platform_dashboards_segments_audiencesize"
>title="對象規模"
>abstract="此小部件顯示選定段內合併的配置檔案總數。 此數字取決於應用於資料的合併策略，在最新快照時是正確的。"
>additional-url="https://experienceleague.adobe.com/docs/experience-platform/dashboards/guides/segments.html#audience-size" text="從文檔瞭解更多資訊"

的 **[!UICONTROL 受眾大小]** 構件顯示拍攝快照時選定段內合併的配置檔案總數。 此數字是將段合併策略應用於配置檔案資料的結果，以便將配置檔案片段合併到一起，為段中的每個個體形成單個配置檔案。

有關碎片和合併配置檔案的詳細資訊，請首先閱讀 [即時客戶概要資訊概述](../../profile/home.md)。

![](../images/segments/audience-size.png)

### [!UICONTROL 受眾規模趨勢] {#audience-size-trend}

>[!CONTEXTUALHELP]
>id="platform_dashboards_segments_audiencesizetrend"
>title="受眾規模趨勢"
>abstract="此小部件提供有關滿足以下條件的配置檔案總數的資訊： **任何** 段定義，如在每日快照中捕獲的，用於過去30天、90天或12個月。"
>additional-url="https://experienceleague.adobe.com/docs/experience-platform/dashboards/guides/segments.html#audience-size-trend" text="從文檔瞭解更多資訊"

的 **[!UICONTROL 受眾規模趨勢]** 構件提供了符合以下條件的配置檔案總數的線形圖圖 **任何** 段定義。 觀眾人數趨勢可以在30天、90天和12個月期間進行可視化。 時間段從小部件的下拉菜單中選擇。 觀眾大小反映在y軸上，時間反映在x軸上。

此小部件還包括自動 [!UICONTROL 字幕] 其中機器學習模型分析圖表和分段資料並自動生成字幕以描述關鍵趨勢和重要事件。 選擇 **[!UICONTROL 字幕]** 的子菜單。

![段概述顯示「受眾大小」趨勢構件。](../images/segments/audience-size-trend-captions.png)

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

<!-- * [[!UICONTROL Audience overlap report]](#audience-overlap-report) -->
<!-- ### [!UICONTROL Audience overlap report] {#audience-overlap-report} -->

<!-- View an ordered list of audiences by Highest or Lowest overlap percentages. -->

<!-- ![The Audience overlap report widget.]() -->

<!-- https://jira.corp.adobe.com/browse/PLAT-125511 -->

### [!UICONTROL 身份重疊] {#identity-overlap}

>[!CONTEXTUALHELP]
>id="platform_dashboards_segments_identityoverlap"
>title="身份重疊"
>abstract="此小部件顯示段中包含兩個選定標識的配置檔案的重疊。 圓顯示每個標識的相對大小。 包含兩個命名空間的配置檔案數由圓之間的重疊表示。"
>additional-url="https://experienceleague.adobe.com/docs/experience-platform/dashboards/guides/segments.html#identity-overlap" text="從文檔瞭解更多資訊"

的 **[!UICONTROL 身份重疊]** 小部件顯示一個Venn圖或設定圖，顯示包含多個標識的段中配置檔案的重疊。

使用小部件上的下拉菜單選擇要比較的身份。 圓顯示每個所選標識的相對大小，其中包含兩個命名空間的配置檔案的數目由圓之間重疊的大小表示。

如果客戶在多個渠道上與您的品牌進行交互，則多個身份將與該個別客戶關聯，因此您的組織很可能具有多個配置檔案，其中包含來自多個身份的片段。

要瞭解有關身份的詳細資訊，請訪問 [Adobe Experience Platform身份服務文檔](../../identity-service/home.md)。

![](../images/segments/identity-overlap.png)

### [!UICONTROL 按身份顯示的配置檔案] {#profiles-by-identity}

>[!CONTEXTUALHELP]
>id="platform_dashboards_segments_profilesbyidentity"
>title="按身份顯示的配置檔案"
>abstract="此小部件顯示所選段中每個合併配置檔案的標識細分。"
>additional-url="https://experienceleague.adobe.com/docs/experience-platform/dashboards/guides/segments.html#profiles-by-identity" text="從文檔瞭解更多資訊"

的 **[!UICONTROL 按身份顯示的配置檔案]** 小部件顯示選定段中每個合併配置檔案的標識細目。 按標識列出的配置檔案總數可能高於段中的配置檔案總數，因為一個配置檔案可能具有與其關聯的多個標識。 換句話說，將每個身份顯示的值加在一起，可能總和會超過網段中的總受眾規模，因為如果客戶在多個渠道與您的品牌進行交互，則多個身份可能與該個別客戶相關聯。

選擇 **[!UICONTROL 字幕]** 的子菜單。

![按標識標題顯示的配置檔案對話框。](../images/segments/profiles-by-identity.png)

機器學習模型通過分析資料的總體分佈和關鍵維度自動生成資料洞察力。

要瞭解有關身份的詳細資訊，請訪問 [Adobe Experience Platform身份服務文檔](../../identity-service/home.md)。

## 後續步驟

現在，通過遵循本文檔，您應該能夠找到段操控板並選擇要查看的段。 您還應瞭解可用小部件中顯示的度量。 要瞭解有關在Experience PlatformUI中使用段的詳細資訊，請參閱 [分段服務UI指南](../../segmentation/ui/overview.md)。
