---
keywords: Experience Platform；首頁；熱門主題；分段服務；分段服務；分段服務；使用手冊；使用手冊；分段使用手冊；分段使用手冊；分段生成器；分段生成器；已實現；現有；退出；
solution: Experience Platform
title: 分段服務UI指南
description: Adobe Experience Platform分段服務提供用於建立和管理段定義的用戶介面。
exl-id: 0a2e8d82-281a-4c67-b25b-08b7a1466300
source-git-commit: 229dd08bc5d5dfab068db3be84ad20d10992fd31
workflow-type: tm+mt
source-wordcount: '2650'
ht-degree: 3%

---

# 分段服務UI指南

[!DNL Adobe Experience Platform Segmentation Service] 提供了用於建立和管理段定義的用戶介面。

## 快速入門

使用分部定義需要瞭解各分部 [!DNL Experience Platform] 服務涉及細分。 在閱讀本使用手冊之前，請查看以下服務的文檔：

- [[!DNL Segmentation Service]](../home.md): [!DNL Segmentation Service] 允許您劃分儲存在 [!DNL Experience Platform] 將個人（如客戶、潛在客戶、用戶或組織）關聯到較小的組。
- [[!DNL Real-Time Customer Profile]](../../profile/home.md):基於來自多個源的聚合資料提供統一、即時的用戶配置檔案。
- [[!DNL Adobe Experience Platform Identity Service]](../../identity-service/home.md):通過將來自被接收到的不同資料源的標識橋接到 [!DNL Platform]。
- [[!DNL Experience Data Model (XDM)]](../../xdm/home.md):標準化框架 [!DNL Platform] 組織客戶體驗資料。 為最好地利用分段，請確保根據 [資料建模的最佳做法](../../xdm/schema/best-practices.md)。

瞭解本文檔中使用的兩個關鍵術語並瞭解它們之間的區別也很重要：
- **段定義**:用於描述目標受眾的關鍵特徵或行為的規則集。
- **觀眾**:符合段定義條件的結果配置檔案集。 這可以通過Adobe Experience Platform（平台生成的受眾）或外部來源（外部生成的受眾）建立。

## 總覽

在Experience PlatformUI中，選擇 **[!UICONTROL 段]** 的下界 **[!UICONTROL 概述]** 頁籤顯示 [!UICONTROL 段] 控制項欄。

>[!NOTE]
>
>如果您的組織是新加入平台的，並且尚未建立活動的配置檔案資料集或合併策略， [!UICONTROL 段] 儀表板不可見。 相反， [!UICONTROL 概述] 頁籤顯示幫助您開始使用段的連結和文檔。

### [!UICONTROL 段] 儀表板 {#segments-dashboard}

的 **[!UICONTROL 段]** 儀表板概述了與組織的段資料相關的關鍵度量。

要瞭解更多資訊，請訪問 [段儀表板指南](../../dashboards/guides/segments.md)。

![將顯示段操控板。 它顯示了各種小部件，包括受眾大小、按身份分列的個人資料、身份覆蓋以及受眾大小變化趨勢。](../../dashboards/images/segments/dashboard-overview.png)

## 瀏覽 {#browse}

>[!CONTEXTUALHELP]
>id="platform_segments_browse_churncolumnname"
>title="流失"
>abstract="流失表示和上次執行區段作業時相比，區段定義內正在變更的設定檔的百分比。"

>[!CONTEXTUALHELP]
>id="platform_segments_browse_evaluationmethodcolumnname"
>title="評估方式"
>abstract="區段的評估方式包括批次、串流和邊緣。"

>[!CONTEXTUALHELP]
>id="platform_segments_browse_addallsegmentstoschedule"
>title="將所有區段新增到排程"
>abstract="啟用以在每日排程更新中包含所有批次評估區段。停用以從排程更新中移除所有區段。"

選擇 **[!UICONTROL 瀏覽]** 頁籤，查看組織的所有段定義的清單。

![將顯示段瀏覽螢幕。 將顯示屬於組織的所有段的清單。](../images/ui/overview/segment-browse-all.png)

此視圖列出有關段定義的資訊，包括配置檔案計數、建立日期和上次修改日期。

通過選擇 ![「篩選器屬性」表徵圖](../images/ui/overview/filter-attribute.png)。 這些附加欄位包括細分、評估方法和作業ID。

如果選擇了細分，則顯示的條形圖概述了屬於以下每種計算配置檔案狀態的配置檔案的百分比： [!UICONTROL 已實現] 和 [!UICONTROL 正在退出]。 此外， [!UICONTROL 瀏覽] 頁籤是段狀態的最精確細分。 如果此數字與上所列的數字不同 [!UICONTROL 概述] 頁籤，您應使用 [!UICONTROL 瀏覽] 頁籤，因為 [!UICONTROL 概述] 標籤號每天只更新一次。

| 狀態 | 說明 |
| ------ | ----------- |
| 已實現 | 在過去24小時內符合該段條件的配置檔案計數。 因此，自上次運行批處理段作業以來符合段條件的配置檔案數。 |
| 正在退出 | 過去24小時內退出段的配置檔案計數。 因此，自上次運行批處理段作業以來不再符合段條件的配置檔案數。 |

評價方法可以是流、批或邊。 當資料進入系統時，流段會不斷被評估。 批處理段根據設定的計畫進行評估。 即時評估邊緣段，這允許使用相同的頁面和下一頁個性化使用案例。

![段瀏覽頁面中的段將突出顯示。](../images/ui/overview/segment-browse-segments.png)

頁面頂部有選項，可將所有段添加到調度並建立新段。

切換 **[!UICONTROL 將所有段添加到計畫]** 將啟用計畫的分段。 有關計劃分段的詳細資訊，請參閱 [此使用手冊的計劃分段部分](#scheduled-segmentation)。

選擇 **[!UICONTROL 建立段]** 將帶您到段生成器。 要瞭解有關建立段的詳細資訊，請閱讀上 [在使用手冊中建立段](#create-segment)。

![段瀏覽頁面上的頂部導航欄將突出顯示。 此欄包含將所有段添加到調度的切換和建立段的按鈕。](../images/ui/overview/segment-browse-top.png)

右側欄包含有關組織內所有段的資訊，列出段總數、上次評估日期、下次評估日期，以及按評估方法細分的段。

![段瀏覽頁面上的右側欄將突出顯示。 將顯示有關組織中的段的資訊。 這包括段總數、上次評估時間、下一次評估時間以及不同段類型的細分等資訊。](../images/ui/overview/segment-browse-segment-info.png)

選擇段定義的行提供了段定義的摘要，包括編輯或刪除段、激活到目標的段、段的限定受眾、總受眾大小以及段的名稱、說明、評估方法、建立日期和上次修改日期的選項。

>[!NOTE]
>
> 你會的 **不** 能夠刪除在目標激活中使用的段。

![將顯示有關選定段的詳細資訊。 這包括有關合格配置檔案數、合格配置檔案與總配置檔案的百分比細分、最後評估日期的詳細資訊。](../images/ui/overview/segment-browse-details.png)

## 段定義詳細資訊 {#segment-details}

要查看有關特定段定義的詳細資訊，請在 **[!UICONTROL 瀏覽]** 頁籤。

此時將顯示段詳細資訊頁面。 在頂部，有段定義的摘要、有關限定受眾大小的資訊以及該段被激活的目標。

![此時將顯示段定義詳細資訊頁。 會突出顯示段摘要、段中的總受眾和激活的目標卡。](../images/ui/overview/segment-details-summary.png)

### 段摘要 {#segment-summary}

的 **[!UICONTROL 段摘要]** 部分提供了屬性的ID、名稱、說明和詳細資訊等資訊。

此外，您還可以選擇將段激活到目標或編輯段。 選擇 **[!UICONTROL 激活到目標]** 將激活段到目標。 有關將段激活到目標的詳細資訊，請閱讀 [激活概述](../../destinations/ui/activation-overview.md)。

![「激活到目標」(Activate to destination)按鈕將突出顯示。](../images/ui/overview/segment-details-activate.png)

選擇 **[!UICONTROL 編輯段]** 會帶你去 [!DNL Segment Builder]。 有關使用 [!DNL Segment Builder] 工作區，請閱讀 [[!DNL Segment Builder] 使用手冊](./segment-builder.md)。

![](../images/ui/overview/segment-details-edit-segment.png)

### 段中的受眾總數

的 **[!UICONTROL 段中的受眾總數]** 部分顯示符合段條件的配置檔案總數。

使用當天樣本資料的樣本大小生成估計。 如果配置檔案儲存中的實體少於100萬個，則使用完整的資料集；100萬至2000萬個單位使用100萬個單位；超過2000萬戶，佔全部用戶的5%。 有關生成段估計的詳細資訊，請參閱 [估計生成部分](../tutorials/create-a-segment.md#estimate-and-preview-an-audience) 的子菜單。

### 激活的目標

的 **[!UICONTROL 激活的目標]** 部分顯示此段的激活目標。

>[!NOTE]
>
> 目標是 [!DNL Adobe Real-Time Customer Data Platform]，並允許您將資料導出到外部平台。 有關目標的詳細資訊，請閱讀 [目標概述](../../destinations/home.md)。 要瞭解如何激活到目標的段，請參閱 [激活概述](../../destinations/ui/activation-overview.md)。

### 配置檔案示例

下面是符合該段條件的配置檔案的採樣，詳細列出包括 [!DNL Profile] ID、名、姓和個人電子郵件。

資料採樣的觸發方式取決於攝入方法。

對於批處理接收，配置檔案儲存會每十五分鐘自動掃描一次，以查看自上次執行採樣作業以來是否成功接收了新批處理。 如果是，隨後掃描配置檔案儲存以查看記錄數是否至少有5%的變化。 如果滿足這些條件，則觸發新的採樣作業。

對於流式接收，每小時自動掃描配置檔案儲存，以查看記錄數是否至少有5%的變化。 如果滿足此條件，則觸發新的採樣作業。

掃描的樣本大小取決於配置檔案儲存中的實體總數。 下表顯示了這些示例大小：

| 配置檔案儲存中的實體 | 示例大小 |
| ------------------------- | ----------- |
| 不到100萬 | 完整資料集 |
| 1到2000萬 | 100萬 |
| 2000多萬 | 5% |

有關每個 [!DNL Profile] 通過選擇 [!DNL Profile] ID。 要瞭解有關配置檔案詳細資訊的詳細資訊，請閱讀 [[!DNL Real-Time Customer Profile] 使用手冊](../../profile/ui/user-guide.md#profile-detail)。

![段定義的示例輪廓被加亮。 配置檔案資訊示例包括配置檔案ID、名、姓和人員的電子郵件。](../images/ui/overview/segment-details-profiles.png)

## 建立區段 {#create-segment}

選擇 **[!UICONTROL 建立段]** 右上角開啟 [!DNL Segment Builder] 工作區，在此可開始建立段定義。

![在「段」瀏覽頁面上，「建立段」按鈕會突出顯示。](../images/ui/overview/segment-browse-create.png)

### [!DNL Segment Builder] 工作區

[!DNL Segment Builder] 提供豐富的工作區，允許您與 [!DNL Profile] 資料元素。 工作區為生成和編輯規則提供了直觀的控制項，如用於表示資料屬性的拖放拼貼。

有關使用 [!DNL Segment Builder] 工作區，請閱讀 [[!DNL Segment Builder] 使用手冊](./segment-builder.md)。

![將顯示段生成器工作區。](../images/ui/overview/segment-builder.png)

## 計畫的分段 {#scheduled-segmentation}

一旦建立了段定義，您就可以通過按需或計畫（連續）評估來評估它們。 評估裝置移動 [!DNL Real-Time Customer Profile] 資料通過段定義來產生相應的受眾。 建立後，將保存和儲存受眾，以便使用 [!DNL Experience Platform] API。

按需評估包括使用API執行評估並根據需要構建受眾，而計畫評估（也稱為「計劃分段」）允許您建立定期計畫以在特定時間（最多每天一次）評估段定義。

### 啟用計畫的分段 {#enable-scheduled-segmentation}

可以使用UI或API為計畫評估啟用段定義。 在UI中，返回到 **[!UICONTROL 瀏覽]** 頁籤 **[!UICONTROL 段]** 開啟 **[!UICONTROL 將所有段添加到計畫]**。 這將導致根據組織設定的計畫評估所有段。

>[!NOTE]
>
>可以為最多五(5)個合併策略的沙箱啟用計畫評估 [!DNL XDM Individual Profile]。 如果您的組織有五個以上的合併策略 [!DNL XDM Individual Profile] 在單個沙箱環境中，您將無法使用計畫的評估。

當前只能使用API建立計畫。 有關使用API建立、編輯和使用計畫的詳細步驟，請按照本教程來評估和訪問段結果，特別是有關 [使用API進行計畫評估](../tutorials/evaluate-a-segment.md#scheduled-evaluation)。

![在「段瀏覽」(Segments Browse)頁上，突出顯示了「將所有段添加到調度」(Add all segments to a schedule)的切換。](../images/ui/overview/segment-browse-scheduled.png)

## 對象 {#audiences}

>[!IMPORTANT]
>
>受眾功能當前處於有限的測試版中，並且不適用於所有用戶。 文件和功能可能會有所變更。

選擇 **[!UICONTROL 觀眾]** 頁籤，查看組織的所有受眾的清單。

![組織的受眾清單。](../images/ui/overview/list-audiences.png)

預設情況下，此視圖列出有關受眾的資訊，包括名稱、配置檔案計數、來源、建立日期和上次修改日期。

可以選擇 ![自定義表](../images/ui/overview/customize-table.png) 表徵圖以更改顯示的欄位。

![「定制表」(customize table)按鈕被突出顯示。 選擇此按鈕可以自定義「觀眾」瀏覽頁上顯示的欄位。](../images/ui/overview/select-customize-table.png)

出現跨距，列出表中可顯示的所有欄位。

![可為瀏覽「訪問群體」部分顯示的屬性。](../images/ui/overview/customize-table-attributes.png)

| 欄位 | 說明 |
| ----- | ----------- | 
| [!UICONTROL 名稱] | 對象名稱。 |
| [!UICONTROL 設定檔計數] | 符合受眾資格的配置檔案總數。 |
| [!UICONTROL Origin] | 觀眾的來源。 如果此受眾是平台生成的，則它將具有分段服務的來源。 |
| [!UICONTROL 生命週期狀態] | 受眾的狀態。 此欄位的可能值包括 `Draft`。 `Published`, `Archived`。 |
| [!UICONTROL 更新頻率] | 一個值，用於說明更新受眾資料的頻率。 此欄位的可能值包括 `On Demand`。 `Scheduled`, `Continuous`。 |
| [!UICONTROL 上次更新者] | 上次更新受眾的人員的姓名。 |
| [!UICONTROL 已建立] | 建立訪問群體的時間和日期。 |
| [!UICONTROL 上次更新時間] | 上次建立訪問群體的時間和日期。 |
| [!UICONTROL 訪問標籤] | 受眾的訪問標籤。 訪問標籤允許您根據應用於該資料的使用策略對資料集和欄位進行分類。 這些標籤可以隨時應用，在選擇管理資料的方式上提供了靈活性。 有關訪問標籤的詳細資訊，請閱讀 [管理標籤](../../access-control/abac/ui/labels.md)。 |

可以選擇 **[!UICONTROL 建立受眾]** 來建立受眾。

![將突出顯示「建立受眾」按鈕，向您顯示要選擇在何處建立受眾。](../images/ui/overview/create-audience.png)

出現跨距，允許您在合成受眾或構建規則之間進行選擇。

![一個跨距，顯示可建立的兩種類型的受眾。](../images/ui/overview/create-audience-type.png)

選擇 **[!UICONTROL 撰寫受眾]** 帶您到「受眾構建器」。 要瞭解有關建立觀眾的更多資訊，請閱讀 [受眾構建器指南](./audience-builder.md)。

選擇 **[!UICONTROL 生成規則]** 帶您到段生成器。 要瞭解有關建立段的詳細資訊，請閱讀 [段生成器指南](./segment-builder.md)

## 受眾詳細資訊 {#audience-details}

要查看有關特定受眾的詳細資訊，請在 [!UICONTROL 觀眾] 頁籤。

此時將顯示「訪問群體詳細資訊」頁面。 此頁的詳細資訊有所不同，具體取決於受眾是使用Adobe Experience Platform還是從外部源（如受眾業務流程）生成的。

### 平台生成的受眾

有關平台生成的受眾的詳細資訊，請閱讀 [段摘要部分](#segment-summary)。

### 外部生成的受眾

在受眾詳細資訊頁面的頂部，提供了受眾的摘要以及有關受眾保存在中的資料集的詳細資訊。

![為外部生成的觀眾提供的詳細資訊。](../images/ui/overview/externally-generated-audience.png)

的 **[!UICONTROL 受眾摘要]** 部分提供了屬性的ID、名稱、說明和詳細資訊等資訊。

的 **[!UICONTROL 資料集詳細資訊]** 節提供了名稱、說明、表名、源和架構等資訊。 可以選擇 **[!UICONTROL 查看資料集]** 查看有關資料集的詳細資訊。

| 欄位 | 說明 |
| ----- | ----------- |
| [!UICONTROL 名稱] | 資料集的名稱。 |
| [!UICONTROL 說明] | 資料集的說明。 |
| [!UICONTROL 表名] | 資料集的表名。 |
| [!UICONTROL 來源] | 資料集的源。 對於外部生成的受眾，此值將 **架構**。 |
| [!UICONTROL 方案] | 資料集對應的XDM架構的類型。 |

要瞭解有關資料集的詳細資訊，請閱讀 [資料集概述](../../catalog/datasets/overview.md)。

## 流分段 {#streaming-segmentation}

流分割是在 [!DNL Platform] 接近即時，同時關注資料豐富度。 隨著流分割，資料進入時段的限定現在發生 [!DNL Platform]，緩解了調度和運行分段作業的需要。

有關流分割的詳細資訊，請參閱 [流式分段使用手冊](./streaming-segmentation.md)。

>[!NOTE]
>
>為了使流分段工作，您需要為組織啟用計劃分段。 有關啟用計劃分段的詳細資訊，請參閱 [本使用手冊中的流分段部分](#scheduled-segmentation)。

## 邊緣分割 {#edge-segmentation}

邊緣分割是指能夠即時評估平台中的邊緣段，從而實現相同的頁面和下一頁個性化使用案例。

有關邊緣分割的詳細資訊，請參閱 [邊緣分割UI指南](./edge-segmentation.md)

## 違反策略

>[!NOTE]
>
>僅當您正在建立已分配給目標的段時，才適用策略違規。

建立完網段後，Adobe Experience Platform資料治理將對網段進行分析，以確保網段內沒有違反策略的情況。 查看 [資料治理概述](../../data-governance/home.md) 的子菜單。

![將顯示段的策略違規。](../images/ui/overview/segment-dule-policy-violations.png)

## 後續步驟和其他資源 {#next-steps}

的 [!DNL Segmentation Service] UI提供了豐富的工作流，允許您將有市場的受眾與 [!DNL Real-Time Customer Profile] 資料。

瞭解有關 [!DNL Segmentation Service]，請繼續閱讀文檔。 瞭解如何使用 [!DNL Segmentation Service] API，請閱讀 [[!DNL Segmentation Service] 開發者指南](../api/overview.md)。
