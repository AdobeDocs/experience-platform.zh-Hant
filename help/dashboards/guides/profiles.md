---
keywords: Experience Platform；設定檔；即時客戶設定檔；使用者介面；UI；自訂；設定檔控制面板；控制面板
title: 設定檔控制面板
description: Adobe Experience Platform提供控制面板，讓您檢視有關組織即時客戶設定檔資料的重要資訊。
type: Documentation
exl-id: 7b9752b2-460e-440b-a6f7-a1f1b9d22eeb
source-git-commit: e52eb90b64ae9142e714a46017cfd14156c78f8b
workflow-type: tm+mt
source-wordcount: '4995'
ht-degree: 0%

---

# [!UICONTROL 設定檔] 儀表板

Adobe Experience Platform使用者介面(UI)提供了一個儀表板，您可以通過該儀表板檢視關於您的裝置的重要資訊， [!DNL Real-Time Customer Profile] 資料，在每日快照期間擷取。 本指南概述如何存取和使用UI中的設定檔控制面板，並提供控制面板中顯示的量度相關資訊。

請參閱 [即時客戶設定檔UI指南](../../profile/ui/user-guide.md) 以概略瞭解Experience Platform使用者介面中的設定檔功能。

## 設定檔儀表板資料

設定檔儀表板會顯示貴組織在Experience Platform的設定檔存放區中擁有的屬性（記錄）資料快照。 快照不包含任何事件（時間序列）資料。

快照中的屬性資料顯示的資料與拍攝快照的特定時間點完全相同。 換言之，快照不是資料的近似或樣本，而且「設定檔」圖示板不會即時更新。

>[!NOTE]
>
>自拍攝快照以來對資料所做的任何變更或更新都不會反映在儀表板中，直到拍攝下一個快照為止。

## 探索設定檔控制面板 {#explore-dashboard}

若要導覽至Platform UI中的設定檔控制面板，請選取「 」 **[!UICONTROL 設定檔]** 在左側欄中，然後選取 **[!UICONTROL 概觀]** 標籤來顯示控制面板。

>[!NOTE]
>
>如果您的組織剛開始使用Platform，但尚未建立作用中的設定檔資料集或合併原則，則不會顯示設定檔控制面板。 而是 [!UICONTROL 概觀] 索引標籤會顯示連結和檔案，以幫助您開始使用即時客戶個人檔案。

![Experience Platform設定檔控制面板，醒目提示設定檔和概觀。](../images/profiles/dashboard-overview.png)

### 修改設定檔儀表板 {#modify-dashboard}

您可以選取「輪廓」圖示板的外觀 **[!UICONTROL 修改儀表板]**. 您可以移動、新增、調整大小及移除儀表板中的Widget，也可以存取 **[!UICONTROL Widget資料庫]** 探索可用的Widget，並為您的組織建立自訂Widget。

若要進一步瞭解，請參閱 [修改儀表板](../customize/modify.md) 和 [Widget程式庫概觀](../customize/widget-library.md) 檔案。

### 新增Widget {#add-widget}

選取 **[!UICONTROL 新增Widget]** 導覽至Widget資料庫，並檢視可新增至控制面板的可用Widget清單。

![強調顯示「設定檔」儀表板概述中的新增Widget。](../images/profiles/profiles-overview-add-widget.png)

在Widget資料庫中，您可以瀏覽標準與自訂對象Widget的選取專案。 如需如何新增Widget的相關資訊，請參閱如何新增Widget的程式庫檔案 [新增Widget](../customize/widget-library.md#add-widgets).

### 檢視 SQL {#view-sql}

您可以透過開啟「 」按鈕來檢視產生在控制面板上視覺化分析的SQL。 [!UICONTROL 概觀] 工作區。 您可以從現有見解的SQL獲得靈感，以建立新的查詢，這些查詢會根據您的業務需求從Platform資料獲得獨特的見解。 若要進一步瞭解此功能，請參閱 [檢視SQL UI指南](../view-sql.md).

<!-- ## (Beta) Profile efficacy insights {#profile-efficacy-insights}

>[!IMPORTANT]
>
>The profile efficacy insight functionality is currently in beta and are not available to all users. The documentation and the functionality are subject to change.

The [!UICONTROL Efficacy] tab provides metrics on the quality and completeness of your profile data through the use of profile efficacy widgets. These widgets illustrate at a glance the composition of your profiles, trends in completeness over time, and assessments on the quality of your profile data.

![The profile efficacy dashboard.](../images/profiles/attributes-quality-assessment.png)

See the [profile efficacy widgets section](#profile-efficacy-widgets) for more information on the widgets currently available.

The layout of this dashboard is also customizable by selecting [**[!UICONTROL Modify dashboard]**](../customize/modify.md) from the [!UICONTROL Overview] tab. -->

## 瀏覽設定檔 {#browse-profiles}

此 [!UICONTROL 瀏覽] 索引標籤可讓您搜尋和檢視擷取到您組織中的唯讀設定檔。 從這裡，您可以看到屬於設定檔的重要資訊，其中包含其偏好設定、過去事件、互動和對象。

## 設定檔詳細資料 {#profile-details}

若要開啟 [!UICONTROL 設定檔] [!UICONTROL 詳細資料] 工作區，選取 [!UICONTROL 設定檔ID] 從清單中。

![設定檔ID反白顯示的「設定檔瀏覽」標籤。](../images/profiles/profile-id.png)

此 [!UICONTROL 設定檔] [!UICONTROL 詳細資料] 工作區會顯示數個預先設定的Widget，傳達該設定檔的特定資訊。 此資訊可讓您一眼瞭解設定檔的關鍵屬性。 您也可以自訂 [!UICONTROL 設定檔] [!UICONTROL 詳細資料] 建立您自己的Widget來工作區。 請參閱以下小節： [如何新增Widget](#add-widgets) 以取得更多詳細資料。

![此 [!UICONTROL 設定檔] [!UICONTROL 詳細資料] 工作區與 [!UICONTROL 詳細資料] 索引標籤反白顯示。](../images/profiles/profile-details-workspace.png)

### 設定檔詳細資訊Widget {#widgets}

預先設定的設定檔詳細資訊Widget如下：

#### 客戶設定檔 {#customer-profile}

此 [!UICONTROL 客戶設定檔] Widget會顯示與設定檔相關聯之使用者的名字和姓氏，以及其 [!UICONTROL 設定檔ID]. 設定檔ID是與身分型別相關聯的自動產生識別碼，代表設定檔。 若要深入瞭解身分識別與身分識別名稱空間，請參閱 [身分概述](../../rtcdp/profile/identities-overview.md).

![客戶設定檔Widget。](../images/profiles/customer-profile.png)

#### 基本屬性 {#basic-attributes}

此 [!UICONTROL 基本屬性] widget會顯示最常用於定義個別設定檔的屬性。

![基本屬性Widget。](../images/profiles/basic-attributes.png)

#### 連結的身分 {#linked-identities}

此 [!UICONTROL 連結的身分] widget會顯示與設定檔相關聯的任何其他身分。

若要更深入檢視設定檔的身分詳細資訊，請導覽至 [!UICONTROL 身分] 工作區，選取 **[!UICONTROL 檢視身分圖表]**.

![連結的身分識別Widget。](../images/profiles/linked-identities.png)

#### 管道偏好設定 {#channel-preferences}

此 [!UICONTROL 頻道偏好設定] widget會顯示使用者同意接收通訊的通訊管道。 核取記號表示使用者已同意接收通訊的每個管道。

<!-- image needs a blue tick added below -->

![管道偏好設定Widget。](../images/profiles/channel-preferences.png)

客戶同意和聯絡人偏好設定是複雜的主題。 若要瞭解如何在Experience Platform中收集、處理和篩選同意和內容偏好設定，建議您閱讀以下檔案：

* 若要瞭解所需的結構描述欄位群組 [根據Adobe標準收集同意資料](../../landing/governance-privacy-security/consent/adobe/overview.md)，請參閱這些已啟用設定檔的結構描述欄位群組的相關檔案。
   * [[!UICONTROL 同意和偏好設定詳細資料]](../../xdm/field-groups/profile/consents.md)
   * [[!UICONTROL 身分對應]](../../xdm/field-groups/profile/identitymap.md) （若使用Platform Web或Mobile SDK傳送同意訊號則為必要）
* 若要瞭解如何使用Adobe標準處理客戶同意和偏好設定資料，請參閱以下概觀： [Experience Platform中的同意處理](../../landing/governance-privacy-security/consent/adobe/overview.md).
* 合併的資料治理和同意原則可用於根據其同意偏好設定和您建立的組織規則篩選要分段的設定檔。 若要瞭解如何建立和使用這些合併原則，請參閱以下內容的使用手冊： [管理資料使用原則](../../data-governance/policies/user-guide.md#combine-policies).

### 新增Widget {#add-widgets}

若要將自訂的Widget新增至 [!UICONTROL 設定檔] [!UICONTROL 詳細資料] 工作區，選取 **[!UICONTROL 自訂設定檔詳細資料]**.

![具有的設定檔詳細資料工作區 [!UICONTROL 自訂設定檔詳細資料] 反白顯示。](../images/profiles/customize-profile-details.png)

您現在可以透過調整大小或重新定位Widget來編輯工作區。 選取 **[!UICONTROL 新增Widget]** 以建立具有自訂屬性的Widget。

![設定檔 [!UICONTROL 詳細資料] 工作區，使用 [!UICONTROL 新增Widget] 反白顯示。](../images/profiles/add-widget.png)

Widget建立器隨即出現。 在「 」中輸入您Widget的描述性名稱 [!UICONTROL 卡片標題] 文字欄位並選取 **[!UICONTROL 新增屬性]**.

![Widget建立器畫布包含 [!UICONTROL 卡片標題] 欄位和 [!UICONTROL 新增屬性] 反白顯示。](../images/profiles/widget-creator.png)

隨即出現一個對話方塊，其中包含設定檔聯合結構的視覺效果。 使用搜尋欄位或捲動來尋找您要以您的Widget報告的屬性。 選取您要包含的任何屬性的核取方塊。 選取 **[!UICONTROL 選取]** 以繼續建立工作流程。

>[!TIP]
>
>選取頂層核取方塊時，會包含任何子元素。

![具有忠誠度屬性的聯合結構描述圖表核取方塊和 [!UICONTROL 選取] 反白顯示。](../images/profiles/union-schema-attributes.png)

畫布上會顯示已完成的Widget預覽。 在您滿意所選的屬性後，請選取 **[!UICONTROL 儲存]** 以確認您的選擇並返回 [!UICONTROL 設定檔] [!UICONTROL 詳細資料] 工作區。 新建立的Widget現在會顯示在工作區中。

![「儲存」反白並顯示Widget預覽的Widget建立器畫布。](../images/profiles/widget-preview.png)

## 合併原則 {#merge-policies}

設定檔控制面板中顯示的量度，是根據套用至即時客戶設定檔資料的合併原則。 將來自多個來源的資料彙集在一起以建立客戶設定檔時，資料可能會包含衝突值。 例如，一個資料集可能將客戶列為「單身」，而另一個資料集可能將客戶列為「已婚」。 合併原則的工作是決定哪些資料要優先處理，並顯示為設定檔的一部分。

如需有關合併原則的詳細資訊，包括如何為貴組織建立、編輯和宣告預設合併原則，請參閱 [合併原則概觀](../../profile/merge-policies/overview.md).

儀表板會自動選取要使用的合併原則。 您可使用合併原則名稱旁邊的下拉式選單來變更套用的合併原則。

>[!NOTE]
>
>下拉式功能表只會顯示使用 `_xdm.context.profile` 綱要。 但是，如果貴組織已建立多個合併原則，則可能表示您需要捲動才能檢視可用合併原則的完整清單。

![設定檔概述索引標籤，並反白顯示合併原則下拉式清單。](../images/profiles/select-merge-policy.png)

## 聯合結構描述

此 [!UICONTROL 聯合結構描述] 儀表板會顯示特定XDM類別的聯合結構描述。 藉由選取 **[!UICONTROL 類別]** 下拉式清單中，您可以檢視不同XDM類別的聯合結構描述。

聯合結構描述由共用相同類別並已為設定檔啟用的多個結構描述組成。 它們可讓您在單一檢視中看到，共用相同類別的每個結構描述中包含的每個欄位都合併在一起。

若要深入瞭解 [在Platform UI中檢視聯合結構描述](../../profile/ui/union-schema.md#view-union-schemas)，請參閱聯合結構描述UI指南。

## Widget和量度

儀表板由Widget組成，這些是唯讀量度，可提供有關設定檔資料的重要資訊。

最近一次快照的日期和時間會顯示在最上方 [!UICONTROL 概觀] 並列於合併原則下拉式清單旁。 截至該日期和時間，所有Widget資料都是準確的。 快照的時間戳記會以UTC提供；而不是在個別使用者或組織的時區中。

![「設定檔」儀表板的「概觀」標籤中會反白最新的快照時間戳記。](../images/profiles/snapshot-timestamp.png)

## 預設Widget {#default-widgets}

Adobe Experience Platform的所有新執行個體都會提供預設Widget載出，以強調資料中最新可用的深入分析。 下列Widget從一開始便已在您的區段檢視中預先設定。 有關Widget用途和功能的完整詳細資訊，請參閱下文。

* [[!UICONTROL 設定檔計數]](#profile-count)
* [[!UICONTROL 設定檔計數變更]](#profile-count-change)
* [[!UICONTROL 設定檔計數變更趨勢]](#profiles-count-change-trend)
* [[!UICONTROL 依身分割槽分的設定檔]](#profiles-by-identity)
* [[!UICONTROL 身分重疊]](#identity-overlap)

>[!NOTE]
>
>截至2023年7月26日， [!UICONTROL 設定檔]， [!UICONTROL 受眾]、和 [!UICONTROL 目的地] 對於所有在前六個月未修改檢視的使用者，概述儀表板已重設為新的預設Widget載出。 請參閱以下檔案： [目的地](./destinations.md#default-widgets) 和 [受眾](./audiences.md#default-widgets) 預設Widget區段，以取得關於哪些小工具屬於預設Widget載入一部分的詳細資訊。 您可以繼續如往常一樣自訂您的儀表板Widget。

## Customer AI Widget {#customer-ai-profiles-widgets}

Customer AI可產生自訂傾向評分，例如大規模個別設定檔的流失和轉換情形。 Customer AI通過分析現有的消費者體驗事件資料來預測這一點 **流失或轉換傾向分數**. 這些高精確度的客戶傾向模型可讓您進行更精確的分段和目標定位。 此 [分數的分佈](#customer-ai-distribution-of-scores) 和 [評分摘要](#customer-ai-scoring-summary) 深入分析會示範您對象中的劃分。 它們會強調哪些設定檔為高/低/中傾向，以及它們在您的設定檔計數中的分配方式。

* [[!UICONTROL Customer AI評分摘要]](#customer-ai-scoring-summary)
* [[!UICONTROL 分數的Customer AI分佈]](#customer-ai-distribution-of-scores)

### [!UICONTROL 分數的Customer AI分佈] {#customer-ai-distribution-of-scores}

>[!CONTEXTUALHELP]
>id="platform_dashboards_profiles_distributionOfScores"
>title="分數的分佈"
>abstract="此Widget會依個人檔案總數的傾向分數，以5%的增量將其分佈視覺化。 設定檔計數的分佈由AI模型和所選的合併原則決定。 您可以從Widget標題下方的下拉式選單中變更AI模型。"

此 [!UICONTROL 分數的Customer AI分佈] Widget會依傾向分數分類設定檔總數。 設定檔計數的分佈取決於AI模型和所選的合併原則，然後以5%的增量進行視覺化，表示其傾向。 設定檔的計數會沿Y軸提供，而傾向分數則會沿X軸提供。

>[!NOTE]
>
>如果視覺效果是轉換傾向分數，則高分會以綠色顯示，低分會以紅色顯示。 如果您預測的是流失傾向，則系統會加以逆轉，高分會以紅色顯示，低分則會以綠色顯示。 無論您選擇哪種傾向型別，中段貯體都會保持黃色。

決定傾向分數的AI模型可從Widget標題下方的下拉式選擇器中選取。 下拉式清單包含所有已設定的Customer AI模型清單。 從可用模型清單中為您的分析選取適當的AI模型。 如果沒有可用的Customer AI模型，Widget中的訊息會指示您設定至少一個Customer AI模型，並提供指向Customer AI模型設定頁面的超連結。 如需相關指示，請參閱檔案 [如何設定Customer AI執行個體](../../intelligent-services/customer-ai/user-guide/configure.md).

>[!NOTE]
>
>選取概述標籤正下方的下拉式清單，以變更決定分析中包含哪些設定檔的合併原則。 請參閱以下小節： [合併原則](#merge-policies) 以取得簡要說明，或 [合併原則概觀](../../profile/merge-policies/overview.md) 以取得更多詳細資料。

若要導覽至所選Customer AI模型的詳細深入分析頁面，請選取 **[!UICONTROL 檢視模型詳細資料]**.

![Experience Platform受眾控制面板，具有 [!UICONTROL 分數的Customer AI分佈] Widget和 [!UICONTROL 檢視模型詳細資料] 反白顯示。](../images/segments/customer-ai-distribution-of-scores.png)

詳細模型深入分析頁面隨即顯示。

![Customer AI的深入分析頁面。](../images/profiles/customer-ai-insights-page.png)

有關Customer AI的更多資訊可在以下網址找到： [探索見解UI指南](../../intelligent-services/customer-ai/user-guide/discover-insights.md).

### [!UICONTROL Customer AI評分摘要] {#customer-ai-scoring-summary}

>[!CONTEXTUALHELP]
>id="platform_dashboards_profiles_scoringSummary"
>title="評分摘要"
>abstract="此Widget顯示已評分設定檔的總數，並將其分類為包含高、中和低傾向性的貯體。 環形圖可說明高、中及低傾向性中總設定檔的成比例。"

此Widget顯示已評分的個人檔案總數，並將其分類為分別包含高、中及低傾向的綠色、黃色及紅色貯體。 環形圖可說明高、中和低傾向性之間設定檔的成比例構成。 設定檔符合75歲以上的高傾向、25到74歲之間的中傾向，以及24歲以下的低傾向。 圖例會指出色彩代碼和傾向性臨界值。 當游標暫留在環圈圖的個別區段上時，高、中和低傾向性的設定檔計數會顯示在對話方塊中。

>[!NOTE]
>
>如果視覺效果是轉換傾向分數，則高分會以綠色顯示，低分會以紅色顯示。 如果您預測的是流失傾向，則系統會加以逆轉，高分會以紅色顯示，低分則會以綠色顯示。 無論您選擇哪種傾向型別，中段貯體都會保持黃色。

Widget標題下方的下拉式選單提供所有已設定的Customer AI模型清單。 從可用模型清單中為您的分析選取適當的AI模型。 如果沒有可用的Customer AI模型，Widget中的訊息會指示您設定至少一個Customer AI模型，並提供指向Customer AI模型設定頁面的超連結。 請參閱以下檔案： [如何設定Customer AI執行個體](../../intelligent-services/customer-ai/user-guide/configure.md) 以取得詳細指示。

>[!NOTE]
>
>計算的設定檔總數取決於所選的合併原則。 若要變更所使用的合併原則，請選取概述標籤正下方的下拉式清單。 請參閱以下小節： [合併原則](#merge-policies) 以取得簡要說明，或 [合併原則概觀](../../profile/merge-policies/overview.md) 以取得更多詳細資料。

![Customer AI評分摘要Widget醒目提示的Experience Platform Audiences儀表板。](../images/segments/customer-ai-scoring-summary.png)

若要導覽至所選Customer AI模型的詳細深入分析頁面，請選取 **[!UICONTROL 檢視模型詳細資料]**. 有關Customer AI的更多資訊可在以下網址找到： [探索見解UI指南](../../intelligent-services/customer-ai/user-guide/discover-insights.md).

## 標準Widget {#standard-widgets}

Adobe提供多個標準Widget，您可用來視覺化與設定檔資料相關的不同量度。 您也可以使用建立自訂Widget並與您的組織共用 [!UICONTROL Widget資料庫]. 若要進一步瞭解如何建立自訂Widget，請先閱讀 [Widget程式庫概觀](../customize/widget-library.md).

若要進一步瞭解每個可用的標準Widget，請從下列清單中選取Widget的名稱：

* [[!UICONTROL 設定檔計數]](#profile-count)
* [[!UICONTROL 設定檔計數趨勢]](#profile-count-trend)
* [[!UICONTROL 設定檔計數變更]](#profile-count-change)
* [[!UICONTROL 設定檔計數變更趨勢]](#profiles-count-change-trend)
* [[!UICONTROL 依身分列出的設定檔計數變更趨勢]](#profiles-count-change-trend-by-identity)
* [[!UICONTROL 依身分割槽分的設定檔]](#profiles-by-identity)
* [[!UICONTROL 身分重疊]](#identity-overlap)
* [[!UICONTROL 單一身分設定檔]](#single-identity-profiles)
* [[!UICONTROL 依身分割槽分的單一身分設定檔]](#single-identity-profiles-by-identity)
* [[!UICONTROL 未分段的設定檔]](#unsegmented-profiles)
* [[!UICONTROL 未分段的設定檔變化趨勢]](#unsegmented-profiles-change-trend)
* [[!UICONTROL 依身分割槽分的未分段設定檔]](#unsegmented-profiles-by-identity)
* [[!UICONTROL 對象]](#audiences)
* [[!UICONTROL 對應到目的地狀態的對象]](#audiences-mapped-to-destination-status)
* [[!UICONTROL 對象人數]](#audiences-size)
* [[!UICONTROL 依合併原則區分的對象重疊]](#audience-overlap-by-merge-policy)
* [[!UICONTROL 對象重疊報表]](#audience-overlap-report)

### [!UICONTROL 設定檔計數] {#profile-count}

>[!CONTEXTUALHELP]
>id="platform_dashboards_profiles_profilecount"
>title="設定檔計數"
>abstract="此Widget會顯示拍攝快照時，設定檔存放區中合併的設定檔總數。 數目取決於套用至您的設定檔資料的所選合併原則。"

此 **[!UICONTROL 設定檔計數]** widget會顯示拍攝快照時設定檔存放區中合併的設定檔總數。 此數字是已將選取的合併原則套用至您的設定檔資料的結果，以便將設定檔片段合併在一起，為每個個人形成一個設定檔。

請參閱 [本檔案前面關於合併原則的章節](#merge-policies) 以進一步瞭解。

>[!NOTE]
>
>此 [!UICONTROL 設定檔計數] Widget可能會顯示與上所示設定檔計數不同的數字 [!UICONTROL 瀏覽] 索引標籤中的 [!UICONTROL 設定檔] 部分UI，原因有多種。 造成此差異的最常見原因為 [!UICONTROL 瀏覽] 索引標籤會根據您組織的預設合併原則參考合併的設定檔總數，而 [!UICONTROL 設定檔計數] widget會根據您選取在控制面板中檢視的合併原則，參考合併的設定檔總數。
>
>另一個常見的原因是，擷取儀表板快照的時間與針對執行範例作業的時間不同 [!UICONTROL 瀏覽] 標籤。 您會看到 [!UICONTROL 設定檔計數] Widget上次更新是透過檢視Widget上的時間戳記完成的。 若要進一步瞭解範例作業如何在上觸發： [!UICONTROL 瀏覽] 索引標籤中，請參閱 [即時客戶個人檔案UI指南中的個人檔案計數區段](../../profile/ui/user-guide.md#profile-count).

![設定檔計數Widget反白顯示的Experience Platform設定檔儀表板。](../images/profiles/profile-count.png)

### [!UICONTROL 設定檔計數趨勢] {#profile-count-trend}

此 [!UICONTROL 設定檔計數趨勢] Widget使用線圖來說明系統中包含的設定檔總數隨時間變化的趨勢。 此總數包含自上次每日快照以來匯入系統的任何設定檔。 30天、90天和12個月期間的資料可視覺化。 期間是從Widget的下拉式功能表中選擇。

![設定檔計數趨勢Widget。](../images/profiles/profile-count-trend.png)

### [!UICONTROL 設定檔計數變更] {#profile-count-change}

>[!CONTEXTUALHELP]
>id="platform_dashboards_profiles_profilescountchange"
>title="設定檔計數變更"
>abstract="此Widget會顯示合併的設定檔總數 **已新增** 到上次快照時的設定檔存放區。 數目取決於套用至您的設定檔資料的所選合併原則。"

此 **[!UICONTROL 設定檔計數變更]** widget會顯示自上次快照集以來，新增至設定檔存放區的合併設定檔數目。 此數字是已將選取的合併原則套用至您的設定檔資料的結果，以便將設定檔片段合併在一起，為每個個人形成一個設定檔。 您可以使用下拉式選擇器來檢視過去30天、90天或12個月內新增的設定檔數。

>[!NOTE]
>
>此 [!UICONTROL 設定檔計數變更] widget會反映新增的設定檔數量 **晚於** 初始設定檔擷取和設定檔存放區設定。 換言之，如果您的組織設定了設定檔存放區並在第1天擷取4,000,000個設定檔，則儀表板將在24小時內可用，但 [!UICONTROL 設定檔計數變更] widget會設為0。 此計數方法旨在避免與將設定檔初始擷取至系統相關的尖峰。 在接下來的30天中，您的組織會額外擷取1,000,000個設定檔至設定檔存放區。 拍攝下一個快照後， [!UICONTROL 設定檔計數變更] widget會顯示總共新增1,000,000個設定檔，而 [!UICONTROL 設定檔計數] widget總共會顯示5,000,000個設定檔。

![Platform UI設定檔儀表板中反白顯示設定檔計數變更Widget。](../images/profiles/profile-count-change.png)

### [!UICONTROL 設定檔計數變更趨勢] {#profiles-count-change-trend}

>[!CONTEXTUALHELP]
>id="platform_dashboards_profiles_profilesaddedtrend"
>title="設定檔計數變更趨勢"
>abstract="此Widget顯示過去30天、90天或12個月每日新增至設定檔存放區的合併設定檔數。 數目也取決於套用至設定檔資料的所選合併原則。"

此 **[!UICONTROL 設定檔計數變更趨勢]** widget會顯示過去30天、90天或12個月每日新增至設定檔存放區的合併設定檔總數。 此數字會每天在擷取快照時更新，因此如果您要將設定檔擷取到Platform，則要等到下次擷取快照時才會反映設定檔的數量。 新增的設定檔計數是選定的合併原則套用至設定檔資料的結果，以便將設定檔片段合併在一起，為每個個人形成一個設定檔。

若要進一步瞭解，請參閱 [本檔案前面關於合併原則的章節](#merge-policies).

此 **[!UICONTROL 設定檔計數變更趨勢]** Widget會在Widget的右上角顯示「標題」按鈕。 若要開啟自動註解對話方塊，請選取 **[!UICONTROL 註解]**.

![設定檔總覽標籤會顯示設定檔計數變更趨勢Widget，並反白顯示註解按鈕。](../images/profiles/profiles-count-change-trend-captions.png)

機器學習模型會通過分析圖表和資料自動產生描述主要趨勢和重要事件的標題。 註解會根據註解新增到圖表中。 選取註解以專注於其對應的註解。

![設定檔計數變更趨勢Widget的自動註解對話方塊。](../images/profiles/profiles-added-trends-automatic-captions-dialog-with-annotation.png)

### [!UICONTROL 依身分列出的設定檔計數變更趨勢] {#profiles-count-change-trend-by-identity}

<!-- This widget uses a line graph to illustrate the change in number of profiles filtered by a chosen source identity and merge policy. -->

此Widget會根據選取的來源身分識別來篩選設定檔計數，並合併原則，然後使用線圖說明各個期間的數目變更。 合併原則是從頁面頂端的概述下拉式清單中選取，來源身分和時段是從Widget下拉式選單中選取。 趨勢可以視覺化呈現超過30天、90天和12個月的期間。

此Widget可協助您示範依所需身分篩選的設定檔成長模式，以管理目的地啟用需求。

![依身分Widget區分的設定檔計數變更趨勢。](../images/profiles/profiles-count-change-trend-by-identity.png)

### [!UICONTROL 依身分割槽分的設定檔] {#profiles-by-identity}

>[!CONTEXTUALHELP]
>id="platform_dashboards_profiles_profilesbyidentity"
>title="依身分區分的設定檔"
>abstract="此Widget會依身分顯示個人資料存放區中所有合併個人資料的劃分。"

此 **[!UICONTROL 依身分割槽分的設定檔]** widget會顯示您設定檔存放區中所有合併設定檔的身分劃分。 依身分割槽分的設定檔總數（也就是將每個名稱空間顯示的值相加）可能會高於合併的設定檔總數，因為一個設定檔可能會有多個相關聯的名稱空間。 例如，如果客戶在多個頻道上與您的品牌互動，則多個名稱空間會與該個別客戶相關聯。

若要進一步瞭解，請參閱 [本檔案前面關於合併原則的章節](#merge-policies).

![設定檔總覽儀表板，醒目提示按身分割槽分的設定檔Widget。](../images/profiles/profiles-by-identity.png)

若要開啟自動註解對話方塊，請選取 **[!UICONTROL 註解]**.

![依身分註解的設定檔對話方塊。](../images/profiles/profiles-by-identity-captions.png)

機器學習模型會通過分析資料的整體分佈與關鍵維度，自動產生資料深入分析。

若要進一步瞭解身分，請參閱 [Adobe Experience Platform Identity Service檔案](../../identity-service/home.md).

### [!UICONTROL 身分重疊] {#identity-overlap}

>[!CONTEXTUALHELP]
>id="platform_dashboards_profiles_identityoverlap"
>title="身分重疊"
>abstract="此Widget使用文氏圖表來顯示個人資料存放區中包含兩個所選身分的設定檔重疊。"

此 **[!UICONTROL 身分重疊]** Widget會使用文氏圖表或設定圖表，來顯示個人資料存放區中，包含兩個所選身分的重疊個人資料。

使用Widget下拉式選單來選取您要比較的身分。 圓圈會顯示包含每個身分的設定檔相對總數。 包含兩種身分的設定檔數目會以圓圈之間的重疊大小表示。 如果客戶透過多個管道與您的品牌互動，則多個身分將會與該個別客戶相關聯。 在此情況下，您的組織可能會有多個包含多個身分識別片段的設定檔。

如需設定檔片段的詳細資訊，請參閱 [設定檔片段與合併的設定檔](../../profile/home.md#profile-fragments-vs-merged-profiles) 在即時客戶個人檔案總覽中。

若要進一步瞭解身分，請參閱 [Adobe Experience Platform Identity Service檔案](../../identity-service/home.md).

![設定檔儀表板總覽中反白顯示身分重疊Widget。](../images/profiles/identity-overlap.png)

### [!UICONTROL 單一身分設定檔] {#single-identity-profiles}

>[!CONTEXTUALHELP]
>id="platform_dashboards_profiles_singleidentityprofiles"
>title="單一身分設定檔"
>abstract="此Widget會提供貴組織只有一種ID型別之設定檔的計數，以建立其身分識別。 此ID型別可以是電子郵件或ECID。"

此 [!UICONTROL 單一身分設定檔] Widget會提供貴組織只有一種型別ID型別的設定檔計數，以建立其身分。 此ID型別可以是電子郵件或ECID。 設定檔計數是從最近快照中所包含的資料產生。

![單一身分設定檔Widget。](../images/profiles/single-identity-profiles.png)

### [!UICONTROL 依身分割槽分的單一身分設定檔] {#single-identity-profiles-by-identity}

此Widget使用長條圖來說明僅以單一唯一識別碼識別的設定檔總數。 Widget最多可支援五種最常發生的身分識別。

若要檢視詳細說明身分設定檔總數的對話方塊，請使用游標暫留在個別長條上。

![依身分識別介面工具集的單一身分識別設定檔。](../images/profiles/single-identity-profiles-by-identity.png)

### [!UICONTROL 未分段的設定檔] {#unsegmented-profiles}

>[!CONTEXTUALHELP]
>id="platform_dashboards_profiles_unsegmentedprofiles"
>title="未分段的設定檔"
>abstract="此Widget提供未附加至任何對象的所有設定檔總數，代表您組織內啟用設定檔的機會。"

此 [!UICONTROL 未分段的設定檔] widget提供未附加至任何對象的所有設定檔總數。 產生的數字在最後一個快照集之前是準確的，代表您組織內設定檔啟用的機會。 它還表示有機會刪除未提供足夠ROI的個人檔案。

![未分段的設定檔Widget。](../images/profiles/unsegmented-profiles.png)

### [!UICONTROL 未分段的設定檔變化趨勢] {#unsegmented-profiles-change-trend}

>[!CONTEXTUALHELP]
>id="platform_dashboards_profiles_unsegmentedprofilestrend"
>title="未分段的設定檔趨勢"
>abstract="此Widget提供在指定期間內未附加至任何對象的設定檔數量的線圖插圖。 未附加至對象的設定檔趨勢可在30天、90天和12個月期間進行視覺化。"

此 [!UICONTROL 未分段的設定檔變化趨勢] Widget使用線圖來說明自上次每日快照以來新增的未附加至任何對象的設定檔數量。 未附加至任何對象的設定檔變化趨勢可以在30天、90天和12個月期間進行視覺化。 期間是從Widget的下拉式功能表中選擇。 輪廓計數會反映在y軸上，而時間則反映在x軸上。

![未分段的設定檔會變更趨勢Widget。](../images/profiles/unsegmented-profiles-change-trend.png)

### [!UICONTROL 依身分割槽分的未分段設定檔] {#unsegmented-profiles-by-identity}

>[!NOTE]
>
>截至2022年10月，「依身分識別Widget未分段的設定檔」已遭淘汰，不再提供。

<!-- 

>[!CONTEXTUALHELP]
>id="platform_dashboards_profiles_unsegmentedprofilesbyidentity"
>title="Unsegmented profiles by identity"
>abstract="This widget categorizes the total number of unsegmented profiles by their unique identifier."

The [!UICONTROL Unsegmented Profiles by Identity] widget categorizes the total number of unsegmented profiles by their unique identifier. The data is visualized in a bar chart for ease of comparison. 

![The Unsegmented Profiles by Identity widget.](../images/profiles/unsegmented-profiles-by-identity.png) -->

### [!UICONTROL 對象] {#audiences}

此Widget會根據套用至您設定檔資料的所選合併原則，提供準備啟用的對象總數。

選取 **[!UICONTROL 受眾]** 導覽至 [!UICONTROL 受眾] 儀表板 [!UICONTROL 瀏覽] 標籤。 從那裡，您可以看到組織的所有區段定義清單。

![受眾Widget。](../images/profiles/audiences.png)

<!-- https://jira.corp.adobe.com/browse/PLAT-115291 -->

<!-- * [[!UICONTROL Audiences change trend]](#audiences-change-trend) -->
<!-- ### [!UICONTROL Audiences change trend] {#audiences-change-trend}

This line graph widget visualizes the change in the total number of audiences each day, trending over time. The change in the number of audiences is dependent on the selected merge policy being applied to your profile data. The period of analysis is selected from the widget dropdown menu. The bar chart can be visualized over 30 days, 90 days, and 12-month periods.

The visualization allows you to monitor the overall health of audiences within Adobe Experience Platform by understanding trends in the growth or decline of the total number of audiences. -->

<!-- ![The Audiences change trend widget.]() -->

### [!UICONTROL 對象重疊報表] {#audience-overlap-report}

此Widget會將合併原則所篩選的所有可用對象中資料重疊的表格化。 針對從畫面頂端的下拉式選單中選擇的合併原則，提供從最高到最低重疊百分比排名的五個對象清單。 兩個已分析的對象會列於 [!UICONTROL 對象A名稱] 和 [!UICONTROL 對象B名稱] 欄。 第三欄提供重疊百分比，精確至小數點十二位數。

對象重疊報表可協助您建立新的高效能對象。 觀察高百分比的重疊可讓您抑制受眾，並防止將相同的受眾傳送至不同的目的地。 它們也可協助您識別隱藏的深入分析，可能有助於更佳的分段。 低百分比重疊有助於找到要追蹤的不重複設定檔。

選取 **[!UICONTROL 檢視更多]** 以開啟包含更多對象重疊資料的全熒幕對話方塊。

![對象重疊報表Widget，其中檢視更加醒目提示。](../images/profiles/profiles-audience-overlap-report.png)

此 [!UICONTROL 對象重疊報表] 對話方塊隨即顯示。 此對話方塊最多可包含50列對象重疊分析，並分為6欄。 若要從表格中移除或新增欄，請選取設定圖示(![設定圖示。](../images/profiles/settings-icon.png))。

![對象重疊報表對話方塊。](../images/profiles/profiles-audience-overlap-report-dialog.png)

>[!NOTE]
>
>若要變更結果在最高到最低或最低到最高之間的排名，請選取 **[!UICONTROL 重疊]** 欄標題。

若要以PDF格式下載整個報表，請選取選項功能表(**`...`**)後接 **[!UICONTROL 下載]**.

![對象重疊報表對話方塊，其省略符號和下載選項會醒目提示。](../images/profiles/profiles-audience-overlap-report-dialog-download.png)

若要開啟重疊分析的文氏圖表，請從報表中選取一列。 若要在對話方塊中檢視設定檔計數，請將游標停留在文氏圖表的某個區段上。

![對象重疊報表對話方塊，會以文氏圖表和強調的列顯示。](../images/profiles/profiles-audience-overlap-report-dialog-venn.png)

選取 **[!UICONTROL 關閉]** 以返回 [!UICONTROL 設定檔] 儀表板。

### [!UICONTROL 對應到目的地狀態的對象] {#audiences-mapped-to-destination-status}

此 [!UICONTROL 對應到目的地狀態的對象] widget會顯示單一量度中對應和未對應的對象總數，並使用環形圖來說明總數之間的比例差異。 計算出的數字取決於所選的合併原則。

當游標暫留在環圈圖的個別區段上時，已對應或未對應對象的個別計數會顯示在對話方塊中。

![對應到目的地狀態Widget的對象。](../images/profiles/audiences-mapped-to-destination-status.png)

### [!UICONTROL 對象人數] {#audiences-size}

此 [!UICONTROL 對象人數] widget提供兩欄表格，列出最多20個對象的名稱及各對象中包含的設定檔總數。 此清單會根據對象中包含的設定檔總數從高到低排序。 總對象人數取決於套用的合併原則。

![受眾大小Widget。](../images/profiles/audiences-size.png)

若要檢視對象的完整資訊，請從提供的清單中選取對象名稱，以導覽至 [!UICONTROL 受眾] [!UICONTROL 詳細資料] 頁面。 此外，透過選取 **[!UICONTROL 檢視所有對象]** 從Widget的結尾，您可以導覽至 [!UICONTROL 受眾] [!UICONTROL 瀏覽] 索引標籤以尋找任何現有的對象。

![具有對象名稱的「對象大小」Widget以及反白顯示的「檢視所有對象」文字。](../images/profiles/audiences-size-view-all-audiences.png)

請參閱檔案以取得以下專案的詳細資訊： [[!UICONTROL 受眾] [!UICONTROL  瀏覽] 標籤](../../segmentation/ui/overview.md#browse).

### [!UICONTROL 依合併原則區分的對象重疊] {#audience-overlap-by-merge-policy}

此Widget使用文氏圖表來顯示兩個所選對象之間的重疊。 合併原則是從頁面頂端的概述下拉式清單中選取，而要分析的對象是從介面工具內的兩個下拉式選單中選取。 透過將滑鼠懸停在圓或交集上可看到相關區段定義中包含的輪廓總數。

由於Widget會顯示區段定義的視覺交叉，因此您可以研究區段定義之間的相似性，以最佳化區段策略。

![Platform UI Profiles控制面板具有醒目提示的合併原則下拉式清單和Widget受眾下拉式清單。](../images/profiles/audience-overlap-by-merge-policy.png)


<!-- ## (Beta) Profile efficacy widgets {#profile-efficacy-widgets}

>[!IMPORTANT]
>
>The profile efficacy widgets are currently in Beta and are not available to all users. The documentation and the functionality are subject to change.

Adobe provides multiple widgets to assess the completeness of the ingested profiles available for your data analysis. Each of the profile efficacy widgets can be filtered by the merge policy. To change the merge policy filter, select the[!UICONTROL Profiles using merge policy] dropdown and choose the appropriate policy from the available list.

To learn more about each of the profile efficacy widgets, select the name of a widget from the following list:

* [[!UICONTROL Attribute quality assessment]](#attributes-quality-assessment)
* [[!UICONTROL Profiles by completeness]](#profiles-by-completeness)
* [[!UICONTROL Profiles completeness trend]](#profiles-completeness-trend)

### (Beta) [!UICONTROL Attributes quality assessment] {#attributes-quality-assessment}

>[!CONTEXTUALHELP]
>id="platform_dashboards_profiles_attributesqualityassessment"
>title="Attributes quality assessment"
>abstract="This widget shows the completeness and cardinality of all profiles according to their attributes. Each row describes one attribute. The **Profiles** column provides the number of profiles that have this attribute and are filled with non-null values. The **Completeness** percentage is determined by the total number of profiles that have this attribute and are filled with non-null values divided by the total number of non-empty values in the profiles for that attribute. **Cardinality** provides the total number of unique non-null values of this attribute across all attributes."

The [!UICONTROL Attribute quality assessment] widget shows the completeness and cardinality of all profiles according to their attributes. The data is accurate to the last processing date. This information is presented as a table with four columns where each row in the table represents a single attribute.

| Column  | Description  |
|---|---|
| Attribute  | The name of the attribute.  |
| Profiles  | The number of profiles that have this attribute and are filled with non-null values.  |
| Completeness  | This percentage is determined by the total number of profiles that have this attribute and are filled with non-null values. The number is calculated by dividing the total number of profiles by the total number of non-empty values in the profiles for that attribute.  |
| Cardinality  | The total number of **unique** non-null values of this attribute. It is measured across all profiles. |

![The attributes quality assessment widget](../images/profiles/attributes-quality-assessment.png)

### (Beta) [!UICONTROL Profiles by completeness] {#profiles-by-completeness}

>[!CONTEXTUALHELP]
>id="platform_dashboards_profiles_profilesbycompleteness"
>title="Profiles by completeness"
>abstract="The donut chart displays the percentage of profile attributes that are filled with non-null values among all observed attributes. It illustrates the proportion of profiles that are of high, medium, or low completeness. High completeness profiles have more than 70% of their attributes filled. Medium completeness profiles have between 30% and 70% of their attributes filled. Low completeness profiles have less than 30% of their attributes filled."

The [!UICONTROL Profiles by completeness] widget creates a donut chart of profile completeness since the last processing date. The completeness of a profile is measured by the percentage of attributes that are filled with non-null values among all observed attributes.

This widget shows the proportion of profiles that are of high, medium, or low completeness. By default, there are three levels of completeness configured: 

* High completeness: Profiles have more than 70% of their attributes filled. 
* Medium completeness: Profiles have between 30% and 70% of their attributes filled. 
* Low completeness: Profiles have less than 30% of their attributes filled. 

![The profiles by completeness widget](../images/profiles/profiles-by-completeness.png)

### (Beta) [!UICONTROL Profiles completeness trend] {#profiles-completeness-trend}

>[!CONTEXTUALHELP]
>id="platform_dashboards_profiles_profilescompletenesstrend"
>title="Profiles completeness trend"
>abstract="This widget creates a stacked area chart to depict the trend of profile completeness over time. Completeness is measured by the percentage of attributes that are filled with non-null values among all observed attributes."

This widget creates a stacked area chart to depict the trend of profile completeness over time. Completeness is measured by the percentage of attributes filled with non-null values among all observed attributes. It categorizes the profile completeness as high, medium, or low completeness since the last processing date.

The x-axis represents time, the y-axis represents the number of profiles, and the colors represent the three levels of profile completeness. 

The three levels of completeness are:

* High completeness: Profiles have more than 70% of attributes filled. 
* Medium completeness: Profiles have less than 70% and more than 30% of attributes filled. 
* Low completeness: Profiles have less than 30% of attributes filled.

![The profiles completeness trend widget](../images/profiles/profiles-completeness-trend.png) -->

## 後續步驟

閱讀本檔案後，您現在應該能夠找到設定檔控制面板，並瞭解可用介面工具列中顯示的量度。 若要進一步瞭解使用 [!DNL Profile] Experience PlatformUI中的資料，請參閱 [即時客戶設定檔UI指南](../../profile/ui/user-guide.md).
