---
keywords: Experience Platform；配置檔案；即時客戶配置檔案；用戶介面；UI；自定義；配置檔案面板；儀表板
title: 配置式儀表板
description: Adobe Experience Platform提供了一個儀表板，您可以通過該儀表板查看有關您組織的即時客戶配置檔案資料的重要資訊。
type: Documentation
exl-id: 7b9752b2-460e-440b-a6f7-a1f1b9d22eeb
source-git-commit: b4cd7bc0d8c038346aacdda7c4c9def12864065c
workflow-type: tm+mt
source-wordcount: '2976'
ht-degree: 0%

---

# [!UICONTROL 配置檔案] 儀表板

Adobe Experience Platform用戶介面(UI)提供了一個儀表板，您可以通過該儀表板查看有關 [!DNL Real-time Customer Profile] 資料，在每日快照期間捕獲。 本指南概括介紹了如何訪問和使用 [!UICONTROL 配置檔案] UI中的儀表板，並提供有關儀表板中顯示的度量的資訊。

有關Experience Platform用戶介面中所有配置式功能的概述，請訪問 [即時客戶概要檔案UI指南](../../profile/ui/user-guide.md)。

## 配置檔案儀表板資料

的 [!UICONTROL 配置檔案] 儀表板顯示您的組織在「配置檔案儲存」Experience Platform中擁有的屬性（記錄）資料的快照。 快照不包括任何事件（時間系列）資料。

快照中的屬性資料與拍攝快照時在特定時間點顯示的資料完全相同。 換句話說，快照不是資料的近似值或示例，而「配置檔案」儀表板不會即時更新。

>[!NOTE]
>
>自拍攝快照以來對資料所做的任何更改或更新不會反映在儀表板中，直到拍攝下一個快照。

## 探索 [!UICONTROL 配置檔案] 儀表板

導航到 [!UICONTROL 配置檔案] 平台UI中的儀表板，選擇 **[!UICONTROL 配置檔案]** 在左滑軌中，選擇 **[!UICONTROL 概述]** 頁籤。

>[!NOTE]
>
>如果您的組織是新加入平台的，並且尚未建立活動的配置檔案資料集或合併策略， [!UICONTROL 配置檔案] 儀表板不可見。 相反， [!UICONTROL 概述] 頁籤顯示幫助您開始使用即時客戶配置檔案的連結和文檔。

![](../images/profiles/dashboard-overview.png)

### 修改 [!UICONTROL 配置檔案] 儀表板

可修改 [!UICONTROL 配置檔案] 通過選擇 **[!UICONTROL 修改儀表板]**。 這使您能夠從儀表板中移動、添加和刪除小部件，以及訪問 **[!UICONTROL 小部件庫]** 瀏覽可用小部件並為您的組織建立自定義小部件。

請參閱 [修改儀表板](../customize/modify.md) 和 [小部件庫概述](../customize/widget-library.md) 文檔以瞭解詳細資訊。

## (Beta)簡介功效洞察 {#profile-efficacy-insights}

>[!IMPORTANT]
>
>配置檔案功效透視功能當前處於測試版中，並且不適用於所有用戶。 文件和功能可能會有所變更。

的 [!UICONTROL 功效] 頁籤通過使用配置檔案效能小部件提供有關配置檔案資料的質量和完整性的度量。 這些小部件可一目瞭然地說明您的配置檔案的構成、隨時間推移的完整性趨勢，以及對配置檔案資料質量的評估。

![配置檔案效能儀表板。](../images/profiles/attributes-quality-assessment.png)

查看 [配置檔案效能小部件部分](#profile-efficacy-widgets) 的子菜單。

通過選擇 [**[!UICONTROL 修改儀表板]**](../customize/modify.md) 從 [!UICONTROL 概述] 頁籤。

## 瀏覽配置檔案 {#browse-profiles}

的 [!UICONTROL 瀏覽] 頁籤允許您搜索和查看已接收到IMS組織中的只讀配置檔案。 從此處，您可以看到屬於配置檔案的重要資訊，這些資訊涉及其首選項、過去的事件、交互和段

要瞭解有關平台UI中提供的配置檔案查看功能的詳細資訊，請參閱上的文檔 [瀏覽Real-time Customer Data Platform個人資料](../../rtcdp/profile/profile-browse.md)。

## 合併策略 {#merge-policies}

顯示在 [!UICONTROL 配置檔案] 儀表板基於應用於您的即時客戶配置檔案資料的合併策略。 當從多個源將資料匯集到一起以建立客戶配置檔案時，資料可能包含衝突的值。 例如，一個資料集可以將客戶列為「單一」，而另一個資料集可以將客戶列為「已婚」。 合併策略的任務是確定哪些資料要作為配置檔案的一部分進行優先順序排序和顯示。

有關合併策略的詳細資訊，包括如何為您的組織建立、編輯和聲明預設的合併策略，請從閱讀 [合併策略概述](../../profile/merge-policies/overview.md)。

儀表板將自動選擇要顯示的合併策略，但您可以更改使用下拉菜單選擇的合併策略。 要選擇其他合併策略，請選擇合併策略名稱旁的下拉清單，然後選擇要查看的合併策略。

>[!NOTE]
>
>下拉菜單僅顯示與XDM單個配置檔案類相關的合併策略。 但是，如果您的組織已建立多個合併策略，這可能意味著您需要滾動才能查看可用合併策略的完整清單。

![](../images/profiles/select-merge-policy.png)

## 聯合架構

的 [!UICONTROL 聯合架構] 儀表板顯示特定XDM類的聯合架構。 通過選擇 **[!UICONTROL 類]** 下拉菜單，可以查看不同XDM類的聯合架構。

聯合架構由多個共用同一類且已為配置檔案啟用的架構組成。 它們使您能夠在單個視圖中查看，即共用同一類的每個架構中包含的每個欄位的合併。

請參閱聯合架構UI指南以瞭解有關 [查看平台UI中的聯合架構](../../profile/ui/union-schema.md#view-union-schemas)。

## 小部件和度量

儀表板由小部件組成，這些部件是只讀度量，提供有關配置檔案資料的重要資訊。

小部件上的「上次更新」日期和時間顯示了上次拍攝資料快照的時間。 快照的日期和時間以UTC提供；它不在單個用戶或IMS組織的時區。

## 標準小部件

Adobe提供了多個標準小部件，您可以使用這些小部件來可視化與配置檔案資料相關的不同度量。 您也可以使用 [!UICONTROL 小部件庫]。 要瞭解有關建立自定義小部件的詳細資訊，請首先閱讀 [小部件庫概述](../customize/widget-library.md)。

要瞭解有關每個可用標準小部件的詳細資訊，請從以下清單中選擇小部件的名稱：

* [[!UICONTROL 配置檔案計數]](#profile-count)
* [[!UICONTROL 已添加配置檔案]](#profiles-added)
* [[!UICONTROL 配置檔案添加趨勢]](#profiles-added-trend)
* [[!UICONTROL 按身份顯示的配置檔案]](#profiles-by-identity)
* [[!UICONTROL 身份重疊]](#identity-overlap)
* [[!UICONTROL 單個身份配置檔案]](#single-identity-profiles)
* [[!UICONTROL 未分段的配置檔案]](#unsegmented-profiles)
* [[!UICONTROL 未分段配置檔案趨勢]](#unsegmented-profiles-trend)
* [[!UICONTROL 按身份分段的配置檔案]](#unsegmented-profiles-by-identity)
* [[!UICONTROL 映射到目標狀態的受眾]](#audiences-mapped-to-destination-status)
* [[!UICONTROL 觀眾大小]](#audiences-size)
* [[!UICONTROL 配置檔案計數趨勢]](#profile-count-trend)
* [[!UICONTROL 單個身份配置檔案（按身份）]](#single-identity-profiles-by-identity)

### [!UICONTROL 配置檔案計數] {#profile-count}

的 **[!UICONTROL 配置檔案計數]** 小部件顯示拍攝快照時配置檔案儲存中合併的配置檔案總數。 此數字是將所選合併策略應用於配置檔案資料的結果，以便將配置檔案片段合併到一起，為每個個體形成單個配置檔案。

查看 [本文檔前面的合併策略部分](#merge-policies) 來瞭解更多資訊。

>[!NOTE]
>
>的 [!UICONTROL 配置檔案計數] 小部件可能顯示的數字與在 [!UICONTROL 瀏覽] 的 [!UICONTROL 配置檔案] 的子菜單。 最常見的原因是 [!UICONTROL 瀏覽] 頁籤引用基於組織的預設合併策略的合併配置檔案總數，而 [!UICONTROL 配置檔案計數] 構件引用基於選定要在儀表板中查看的合併策略的合併配置檔案總數。
>
>另一個常見原因是由於獲取儀表板快照的時間與為 [!UICONTROL 瀏覽] 頁籤。 您可以看到 [!UICONTROL 配置檔案計數] 通過查看小部件上的時間戳上次更新小部件，並瞭解有關如何在該小部件上觸發示例作業的詳細資訊 [!UICONTROL 瀏覽] ，請參閱 [即時客戶配置檔案用戶介面指南中的配置檔案計數部分](https://experienceleague.adobe.com/docs/experience-platform/profile/ui/user-guide.html?lang=en#profile-count)。

![](../images/profiles/profile-count.png)

### [!UICONTROL 已添加配置檔案] {#profiles-added}

的 **[!UICONTROL 已添加配置檔案]** 小部件顯示自上次拍攝快照以來添加到配置檔案儲存的合併配置檔案總數。 此數字是將所選合併策略應用於配置檔案資料的結果，以便將配置檔案片段合併到一起，為每個個體形成單個配置檔案。 您可以使用下拉選擇器查看過去30天、90天或12個月中添加的配置檔案。

>[!NOTE]
>
>的 [!UICONTROL 已添加配置檔案] 構件反映添加的配置檔案數 **後** 初始配置檔案接收和配置檔案儲存設定。 換句話說，如果您的組織在第1天設定了配置檔案儲存並接收了4,000,000，那麼在24小時內，儀表板將可用，但 [!UICONTROL 已添加配置檔案] 小部件將設定為0。 這樣做是為了避免與將配置檔案初始接收到系統中相關的尖峰。 在接下來的30天中，您的組織將另外1,000,000個配置檔案添加到配置檔案儲存中。 拍攝下一個快照後， [!UICONTROL 已添加配置檔案] 小部件將顯示添加的共1,000,000個配置檔案，而 [!UICONTROL 配置檔案計數] 小部件將顯示5,000,000個配置檔案。

![](../images/profiles/profiles-added.png)

### [!UICONTROL 配置檔案添加趨勢] {#profiles-added-trend}

的 **[!UICONTROL 配置檔案添加趨勢]** 構件顯示過去30天、90天或12個月中每天添加到配置檔案儲存的合併配置檔案總數。 此數字在每天拍攝快照時都會更新，因此，如果要將配置式導入到平台中，則在拍攝下一個快照之前不會反映配置檔案的數量。 添加的配置檔案計數是將所選合併策略應用於配置檔案資料的結果，以便將配置檔案片段合併到一起，為每個個體形成單個配置檔案。

查看 [本文檔前面的合併策略部分](#merge-policies) 來瞭解更多資訊。

的 **[!UICONTROL 配置檔案添加趨勢]** 小部件在小部件的右上角顯示「字幕」按鈕。 選擇 **[!UICONTROL 字幕]** 的子菜單。

![「配置檔案概述」頁籤顯示「配置檔案」添加的趨勢構件，並突出顯示標題按鈕。](../images/profiles/profiles-added-trend-captions.png)

機器學習模型通過分析圖表和資料自動生成描述關鍵趨勢和重要事件的字幕。

![「配置檔案」添加的趨勢構件的自動字幕對話框。](../images/profiles/profiles-added-trends-automatic-captions-dialog.png)

### [!UICONTROL 按身份顯示的配置檔案] {#profiles-by-identity}

的 **[!UICONTROL 按身份顯示的配置檔案]** 小部件顯示配置檔案儲存中所有合併配置檔案的標識細分。 按標識列出的配置檔案總數（即，將每個命名空間顯示的值相加）可能高於合併的配置檔案總數，因為一個配置檔案可能具有與其關聯的多個命名空間。 例如，如果客戶在多個渠道上與您的品牌進行交互，則多個命名空間將與該客戶關聯。

查看 [本文檔前面的合併策略部分](#merge-policies) 來瞭解更多資訊。

![「配置式」概述儀表板，突出顯示了「按身份構件配置式」。](../images/profiles/profiles-by-identity.png)

選擇 **[!UICONTROL 字幕]** 的子菜單。

![按標識標題顯示的配置檔案對話框。](../images/profiles/profiles-by-identity-captions.png)

機器學習模型通過分析資料的總體分佈和關鍵維度自動生成資料洞察力。

要瞭解有關身份的詳細資訊，請訪問 [Adobe Experience Platform身份服務文檔](../../identity-service/home.md)。

### [!UICONTROL 身份重疊] {#identity-overlap}

的 **[!UICONTROL 身份重疊]** 小部件顯示一個Venn圖或設定圖，顯示配置檔案儲存中包含多個標識的配置檔案的重疊。

使用小部件上的下拉菜單選擇要比較的標識後，會出現圓圈顯示每個標識的相對大小，其中包含兩個命名空間的配置檔案的數量由圓圈之間重疊的大小表示。 如果客戶在多個渠道上與您的品牌進行交互，則多個身份將與該個別客戶關聯，因此您的組織很可能具有多個配置檔案，其中包含來自多個身份的片段。

有關配置檔案片段的詳細資訊，請首先閱讀上的部分 [配置檔案片段與合併的配置檔案](https://experienceleague.adobe.com/docs/experience-platform/profile/home.html?lang=en#profile-fragments-vs-merged-profiles) 在即時客戶概要資訊概述中。

要瞭解有關身份的詳細資訊，請訪問 [Adobe Experience Platform身份服務文檔](../../identity-service/home.md)。

![](../images/profiles/identity-overlap.png)

### [!UICONTROL 單個身份配置檔案] {#single-identity-profiles}

的 [!UICONTROL 單個身份配置檔案] 小部件提供了組織的配置檔案計數，這些配置檔案只具有一種類型的ID類型，可建立其標識。 此ID類型可以是電子郵件或ECID。 配置檔案計數是從最近快照中包含的資料生成的。

![單個身份配置檔案構件。](../images/profiles/single-identity-profiles.png)

### [!UICONTROL 未分段的配置檔案] {#unsegmented-profiles}

的 [!UICONTROL 未分段的配置檔案] 構件提供未附加到任何段的所有配置檔案的總數。 生成的數字在上次快照時準確無誤，表示整個組織中配置檔案激活的機會。 它還表明了擴展不能提供足夠ROI的配置檔案的機會。

![未分段的配置檔案構件。](../images/profiles/unsegmented-profiles.png)

### [!UICONTROL 未分段配置檔案趨勢] {#unsegmented-profiles-trend}

的 [!UICONTROL 未分段配置檔案趨勢] 構件提供線形圖圖，說明在給定時間段內未附加到任何段的配置檔案數。 未附加到任何段的配置檔案的趨勢可以在30天、90天和12個月期間進行可視化。 時間段從小部件的下拉菜單中選擇。 輪廓計數反映在y軸上，時間反映在x軸上。

![未分段配置檔案趨勢構件。](../images/profiles/unsegmented-profiles-trend.png)

### [!UICONTROL 按身份分段的配置檔案] (#unsegmented-profiles-by-identity)

的 [!UICONTROL 按身份分段的配置檔案] 小部件按其唯一標識符對未分段的配置檔案總數進行分類。 資料以條形圖可視化，便於比較。

![按身份構件分段的配置檔案。](../images/profiles/unsegmented-profiles-by-identity.png)

### [!UICONTROL 映射到目標狀態的受眾] {#audiences-mapped-to-destination-status}

的 [!UICONTROL 映射到目標狀態的受眾] 小部件顯示單個度量中映射和未映射的受眾的總數，並使用圓環圖來說明其合計之間的比例差。 計算的數字取決於所選的合併策略。

當游標懸停在圓形圖的相應部分上時，對話框中顯示映射或未映射受眾的單個計數。

![映射到目標狀態構件的受眾。](../images/profiles/audiences-mapped-to-destination-status.png)

### [!UICONTROL 觀眾大小] {#audiences-size}

的 [!UICONTROL 觀眾大小] 小部件提供一個雙清單，其中列出最多20個段以及每個段中包含的訪問群體總數。 根據觀眾總數從高到低排序該清單。 總受眾大小數字取決於應用的合併策略。

![受眾大小小部件。](../images/profiles/audiences-size.png)

要查看段的綜合資訊，請從提供的清單中選擇一個段名稱以定位至 [!UICONTROL 段] [!UICONTROL 詳細資訊] 的子菜單。 另外，通過 **[!UICONTROL 查看所有段]** 從小部件的末尾，您可以導航到 [!UICONTROL 段] [!UICONTROL 瀏覽] 的子菜單。

![具有段名稱的「受眾大小」小部件，並查看突出顯示的所有段文本。](../images/profiles/audiences-size-view-all-segments.png)

有關 [[!UICONTROL 段] [!UICONTROL  瀏覽] 頁籤](https://experienceleague.adobe.com/docs/experience-platform/segmentation/ui/overview.html#browse)。

### [!UICONTROL 配置檔案計數趨勢] {#profile-count-trend}

的 [!UICONTROL 配置檔案計數趨勢] 小部件使用線形圖來說明一段時間內系統中包含的配置檔案總數的趨勢。 此總數包括自上次每日快照後導入到系統的任何配置檔案。 資料可以在30天、90天和12個月期間進行可視化。 時間段從小部件的下拉菜單中選擇。

![配置檔案計數趨勢小部件。](../images/profiles/profile-count-trend.png)

### [!UICONTROL 單個身份配置檔案（按身份）] {#single-identity-profiles-by-identity}

此小部件使用條形圖來說明僅使用單個唯一標識符標識的配置檔案總數。 該小部件最多支援五種最常見的身份。

將滑鼠懸停在各個條上，查看一個對話框，詳細列出標識的配置檔案總數。

![按身份構件顯示的單個身份配置檔案。](../images/profiles/single-identity-profiles-by-identity.png)

## (Beta)配置檔案功效小部件 {#profile-efficacy-widgets}

>[!IMPORTANT]
>
>配置檔案有效性小部件當前位於Beta中，並且不適用於所有用戶。 文件和功能可能會有所變更。

Adobe提供多個小部件，用於評估可用於資料分析的所攝取配置檔案的完整性。 每個配置檔案功效小部件都可通過合併策略進行篩選。 要更改合併策略篩選器，請選擇[!UICONTROL 使用合併策略的配置檔案] 下拉清單，然後從可用清單中選擇相應的策略。

要瞭解有關每個配置檔案功效小部件的詳細資訊，請從以下清單中選擇一個小部件的名稱：

* [[!UICONTROL 屬性質量評估]](#attribute-quality-assessment)
* [[!UICONTROL 配置檔案完整性]](#profile-completeness)
* [[!UICONTROL 配置檔案完整性趨勢]](#profile-completeness-trend)

### (Beta) [!UICONTROL 屬性質量評估] {#attribute-quality-assessment}

此小部件顯示自上次處理日期以來每個配置檔案屬性的完整性和基數。 此資訊以具有四列的表形式顯示，其中表中的每一行表示單個屬性。

| 欄目 | 說明 |
|---|---|
| 屬性 | 屬性的名稱。 |
| 設定檔 | 具有此屬性並填充了非空值的配置檔案數。 |
| 完整性 | 此百分比由具有此屬性並填充了非空值的配置檔案總數確定。 該數字通過將配置檔案總數除以該屬性配置檔案中非空值的總數來計算。 |
| 基數 | 總數 **獨特** 此屬性的非空值。 它是在所有輪廓上測量的。 |

![屬性質量評估構件](../images/profiles/attributes-quality-assessment.png)

### (Beta) [!UICONTROL 按完整性列出的配置檔案] {#profile-completeness}

此小部件建立自上次處理日期以來配置檔案完整性的圓圖。 配置檔案的完整性由所有觀察屬性中填充了非空值的屬性的百分比來衡量。

此小部件顯示高、中或低完整性的配置檔案的比例。 預設情況下，配置了三個完整性級別：

* 高完整性：配置檔案已填充70%以上的屬性。
* 中等完整性：配置檔案填充的屬性少於70%，超過30%。
* 低完整性：配置檔案中填充的屬性不到30%。

![按完整性構件列出的配置檔案](../images/profiles/profiles-by-completeness.png)

### (Beta) [!UICONTROL 配置檔案完整性趨勢] {#profile-completeness-trend}

此小部件建立堆積面積圖，以描述隨時間推移配置檔案完整性的趨勢。 完整性由所有觀察屬性中填充非空值的屬性的百分比度量。 它將配置檔案完整性分類為自上次處理日期以來的高、中或低完整性。

x軸表示時間，y軸表示輪廓的數量，顏色表示輪廓完整性的三個級別。

完整性的三個層次是：

* 高完整性：配置檔案已填充70%以上的屬性。
* 中等完整性：配置檔案填充的屬性少於70%，超過30%。
* 低完整性：配置檔案中填充的屬性不到30%。

![配置檔案完整性趨勢構件](../images/profiles/profiles-completeness-trend.png)

## 後續步驟

現在，通過遵循本文檔，您應該能夠找到「配置式」儀表板並瞭解可用小部件中顯示的度量。 瞭解有關使用的詳細資訊 [!DNL Profile] Experience PlatformUI中的資料，請參閱 [即時客戶概要檔案UI指南](../../profile/ui/user-guide.md)。
