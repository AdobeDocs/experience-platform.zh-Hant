---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: 區段服務使用指南
topic: ui guide
translation-type: tm+mt
source-git-commit: ab43c677ab45c7aa047a50049c0dd8613b003403
workflow-type: tm+mt
source-wordcount: '1361'
ht-degree: 0%

---


# [!UICONTROL 區段服務] (Segmentation Service)使用指南

[!DNL Adobe Experience Platform Segmentation Service] 提供建立和管理區段定義的使用者介面。

## 快速入門

使用區段定義需要瞭解區段所涉 [!DNL Experience Platform] 及的各種服務。 閱讀本使用指南之前，請先閱讀下列服務的說明檔案：

- [[!DNL分段服務]](../home.md): [!DNL Segmentation Service] 可讓您將儲存在與個人( [!DNL Experience Platform] 如客戶、潛在客戶、使用者或組織)相關的資料分割為較小的群組。
- [[!DNL即時客戶基本資料]](../../profile/home.md): 根據來自多個來源的匯整資料，提供統一、即時的消費者個人檔案。
- [[!DNL Adobe Experience Platform Identity Service]](../../identity-service/home.md): 借由將不同資料來源的身分整合到其中，以建立客戶個人檔案 [!DNL Platform]。
- [[!DNL體驗資料模型(XDM)]](../../xdm/home.md): 組織客戶體驗資料 [!DNL Platform] 的標準化架構。

此外，務必瞭解本檔案使用的兩個關鍵詞，並瞭解它們之間的差異：
- **區段定義**: 用於描述目標對象的關鍵特性或行為的規則集。
- **觀眾**: 符合區段定義條件的結果描述檔集。

## 概述

在 [[!DNL Experience Platform] UI中](http://platform.adobe.com/)，選取左側導 **[!UICONTROL 覽中的「區段]** 」以開啟「 **[!UICONTROL 概述]** 」標籤。 此標籤提供檔案和影片的連結，以協助您瞭解並開始使用區段。

![](../images/ui/overview/segment-overview.png)

## 瀏覽

選取「 **[!UICONTROL 瀏覽]** 」標籤，查看IMS組織的所有區段定義清單。

![](../images/ui/overview/segment-browse-all.png)

此檢視會列出區段定義的相關資訊，包括評估方法、建立日期和上次修改日期。

評估方法可以是流式或批式。 當資料進入系統時，會持續評估串流區段。 批次區段會根據設定的排程進行評估。

![](../images/ui/overview/segment-browse-segments.png)

頁面頂端有「新增所有區段 **[!UICONTROL 至排程和建立區段]** 」 **[!UICONTROL 的選項]**。

切換新 **[!UICONTROL 增所有區段以排程]** ，將啟用排程的區段。 如需排程分段的詳細資訊，請參閱本使 [用指南的排程分段區段](#scheduled-segmentation)。

選取「 **[!UICONTROL 建立區段]** 」會帶您前往「區段產生器」。 若要進一步瞭解建立區段，請閱讀使用指 [南中有關建立區段的章節](#create-segment)。

![](../images/ui/overview/segment-browse-top.png)

右側邊欄包含有關IMS組織內所有區段的資訊，列出區段總數、上次評估日期、下次評估日期，以及依評估方法劃分區段。

![](../images/ui/overview/segment-browse-segment-info.png)

選取區段定義的列可提供區段定義的摘要，包括編輯或刪除區段的選項、區段的合格對象、總對象大小，以及區段的名稱、說明、評估方法、建立日期和上次修改日期。

![](../images/ui/overview/segment-browse-details.png)

## 區段定義詳細資訊 {#segment-details}

若要查看特定區段定義的詳細資訊，請在「瀏覽」索引標籤中選取區段 **[!UICONTROL 名稱]** 。

此時會顯示區段詳細資訊頁面。 在上方，有區段定義的摘要、符合資格對象大小的相關資訊，以及區段的啟動目標。

![](../images/ui/overview/segment-details-summary.png)

### 區段摘要

「區 *[!UICONTROL 段摘要]* 」區段提供如屬性的ID、名稱、說明和詳細資訊等資訊。

此外，您也可以選擇編輯區段。 選取 **[!UICONTROL 「編輯]** 」區段會帶您進入 [!DNL Segment Builder]。 有關使用工作區的更多詳 [!DNL Segment Builder] 細資訊，請閱讀使 [[!DNL Segment Builder] 用指南](./segment-builder.md)。

### 群體中的受眾總數

「區 **[!UICONTROL 段中的觀眾總數]** 」區段會顯示符合區段資格的設定檔總數。

估計值是使用當天樣本資料的樣本大小來產生。 如果您的描述檔儲存區中有少於100萬個實體，則會使用完整資料集； 100萬到2000萬個單位使用100萬個單位； 超過2000萬個單位，佔全部單位的5%。 有關產生區段估計的詳細資訊，請參閱區 [段建立教學課程的](../tutorials/create-a-segment.md#estimate-and-preview-an-audience) 「估計產生」區段。

### 已啟動的目標

「啟 **[!UICONTROL 動的目標]** 」區段顯示此區段的啟動目標。

>[!NOTE]
>
> 目標是可用的功能， [!DNL Real-time Customer Data Platform]可讓您將資料匯出至外部平台。 有關目標的詳細資訊，請閱讀目 [標概述](../../rtcdp/destinations/destinations-overview.md)。 若要瞭解如何將區段啟用至目的地，請閱讀 [啟用區段至目的地的指南](../../rtcdp/destinations/activate-destinations.md)。

### 描述檔範例

下面是符合區段資格的個人檔案範例，其中詳列資訊，包括 [!DNL Profile] ID、名字、姓氏和個人電子郵件。

資料採樣觸發方式取決於提取方法。

對於批次擷取，描述檔存放區會每十五分鐘自動掃描一次，以查看自上次執行取樣工作以來是否成功擷取新批次。 如果是這樣，則隨後掃描配置檔案儲存，以查看記錄數是否至少有5%的變化。 如果滿足這些條件，則觸發新的採樣作業。

對於串流擷取，會每小時自動掃描描述檔存放區，以查看記錄數是否至少有5%的變更。 如果符合此條件，則會觸發新的取樣工作。

掃描的樣本大小取決於配置檔案儲存中的實體總數。 下表列出了這些樣本大小：

| 描述檔儲存中的實體 | 樣本大小 |
| ------------------------- | ----------- |
| 不到100萬 | 完整資料集 |
| 1000萬到2000萬 | 100萬 |
| 超過2000萬 | 總共5% |

若需有關每項資訊 [!DNL Profile] 的詳細資訊，請選取 [!DNL Profile] ID。 若要進一步瞭解描述檔的詳細資訊，請閱讀使 [[!DNL Real-time Customer Profile] 用指南](../../profile/ui/user-guide.md#profile-detail)。

![](../images/ui/overview/segment-details-profiles.png)

## 建立區段 {#create-segment}

選取 **[!UICONTROL 右上角的]** 「建立區段」(Create segment [!DNL Segment Builder] in top-right corner)會開啟工作區，您可在其中開始建立區段定義。

![](../images/ui/overview/segment-browse-create.png)

### [!DNL Segment Builder] 工作區

[!DNL Segment Builder] 提供多樣化工作區，讓您與資料元素 [!DNL Profile] 互動。 工作區提供建立和編輯規則的直覺式控制項，例如用來表示資料屬性的拖放圖格。

有關使用工作區的更多詳 [!DNL Segment Builder] 細資訊，請閱讀使 [[!DNL Segment Builder] 用指南](./segment-builder.md)。

![](../images/ui/overview/segment-builder.png)

## 排程的區段 {#scheduled-segmentation}

建立區段定義後，您就可以透過隨選或排程（持續）評估來評估區段定義。 評估意指透過 [!DNL Real-time Customer Profile] 區段定義來移動資料，以產生對應的觀眾。 建立後，觀眾會儲存並儲存，以便使用API匯出 [!DNL Experience Platform] 觀眾。

隨選評估包括視需要使用API來執行評估並建立觀眾，而排程評估（也稱為「排程區段」）可讓您建立循環排程，以評估特定時間（最多每天一次）的區段定義。

### 啟用排程的分段 {#enable-scheduled-segmentation}

您可使用UI或API來啟用計畫評估的區段定義。 在UI中，返回「區段」中的 **[!UICONTROL 「瀏覽]** 」標 **[!UICONTROL 簽]** ，並切換「 **[!UICONTROL 新增所有區段至排程」]**。 這會導致根據您組織所設定的排程評估所有區段。

>[!NOTE]
>
>對於最多5(5)個合併策略的沙盒，可啟用計畫評估 [!DNL XDM Individual Profile]。 如果貴組織在單一沙盒環境中有5 [!DNL XDM Individual Profile] 種以上的合併原則，您將無法使用排程的評估。

目前只能使用API建立排程。 有關使用API建立、編輯和使用排程的詳細步驟，請依照教學課程來評估和存取區段結果，尤其是使用API進行排 [程評估的章節](../tutorials/evaluate-a-segment.md#scheduled-evaluation)。

![](../images/ui/overview/segment-browse-scheduled.png)

## 串流區段 {#streaming-segmentation}

串流分段功能可讓您近乎即時地 [!DNL Platform] 進行分段，同時專注於資料的豐富性。 透過串流分段，區段資格現在會在資料進入時進行 [!DNL Platform]，減輕排程和執行分段工作的需求。

有關串流分段的詳細資訊，請參閱串 [流分段使用指南](./streaming-segmentation.md)。

>[!NOTE]
>
>為了讓串流區段正常運作，您必須啟用組織的排程區段。 如需啟用排程分段的詳細資訊，請參 [閱本使用指南中的串流分段](#scheduled-segmentation)。

## DULE策略違規

>[!NOTE]
>
>DULE策略違規僅在建立已分配給目標的段時適用。

建立完區段後，會依據區段進行分析，以 [!DNL Data Governance] 確保區段內沒有違反原則的情況。 有關DULE和違反策略的詳細資訊，請參閱數 [據使用標籤概述](../../data-governance/labels/overview.md)。

![](../images/ui/overview/segment-dule-policy-violations.png)

## 後續步驟和其他資源 {#next-steps}

UI提 [!DNL Segmentation Service] 供豐富的工作流程，讓您將有價值的受眾與資料隔 [!DNL Real-time Customer Profile] 離。

若要進一步了 [!DNL Segmentation Service]解，請繼續閱讀檔案。 若要瞭解如何使用 [!DNL Segmentation Service] API，請閱讀開發 [[!DNL Segmentation Service] 人員指南](../api/overview.md)。
