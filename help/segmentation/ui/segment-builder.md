---
keywords: Experience Platform;home;popular topics;Segmentation Service;segmentation;segmentation service;user guide;ui guide;segmentation ui guide;segment builder;Segment builder;
solution: Experience Platform
title: 區段服務區段產生器使用指南
topic: ui guide
description: '「區段產生器」提供豐富的工作區，可讓您與描述檔資料元素互動。 工作區提供建立和編輯規則的直覺式控制項，例如用來表示資料屬性的拖放圖格。 '
translation-type: tm+mt
source-git-commit: d2f098cb9e4aaf5beaad02173a22a25a87a43756
workflow-type: tm+mt
source-wordcount: '1723'
ht-degree: 0%

---


# [!DNL Segment Builder] 使用者指南

[!DNL Segment Builder] 提供多樣化工作區，讓您與資料元素 [!DNL Profile] 互動。 工作區提供建立和編輯規則的直覺式控制項，例如用來表示資料屬性的拖放圖格。

![](../images/ui/segment-builder/segment-builder.png)

## 區段定義構建區塊

區段定義的基本建置區塊是「屬 **[!UICONTROL 性]** 」和 **[!UICONTROL 「事件」]**。 此外，現有「觀眾」中包含的屬性和 **[!UICONTROL 事件]** ，也可當成新定義的元件。

您可以在工作區左側的「欄 **[!UICONTROL 位]** 」區段中看到這些構 [!DNL Segment Builder] 建區塊。 **[!UICONTROL 欄位]** (Fields)包含每個主要建置區塊的標籤： **[!UICONTROL 屬性]**、 **[!UICONTROL 事件]**&#x200B;和 **[!UICONTROL 觀眾]**。

![](../images/ui/segment-builder/segment-fields.png)

### 屬性

「屬 **[!UICONTROL 性]** 」(Attributes [!DNL Profile] )頁籤允許您瀏覽屬 [!DNL XDM Individual Profile] 於該類的屬性。 每個檔案夾都可展開以顯示其他屬性，其中每個屬性都是一個方塊，可拖曳至工作區中央的規則產生器畫布上。 本指 [南稍後會詳細討論規則產生器畫布](#rule-builder-canvas) 。

![](../images/ui/segment-builder/attributes.png)

### 事件

「事 **[!UICONTROL 件]** 」標籤可讓您根據使用資料元素發生的事件或動作來建立 [!DNL XDM ExperienceEvent] 對象。 您也可以在「事件」標籤上找 **[!UICONTROL 到事件類型]** ，這是常用事件的集合，可讓您更快速地建立區段。

除了能夠瀏覽元素外，您還 [!DNL ExperienceEvent] 可以搜尋事件類型。 事件類型使用與相同的編碼邏 [!DNL ExperienceEvents]輯，而不需要您在類別中搜尋， [!DNL XDM ExperienceEvent] 以尋找正確的事件。 例如，使用搜尋列來搜尋「購物車」會傳回「事件類型」「[!UICONTROL AddCart]」和「[!UICONTROL RemoveCart]」，這兩個動作在建立區段定義時非常常用。

在使用 [Lucene搜尋語法的搜尋列中輸入元件名稱，即可搜尋任何類型的元件](https://docs.microsoft.com/en-us/azure/search/query-lucene-syntax)。 當輸入整個字詞時，搜尋結果開始填入。 例如，若要根據XDM欄位建立規則，請 `ExperienceEvent.commerce.productViews`開始在搜尋欄位中輸入「產品檢視」。 輸入&quot;product&quot;後，搜尋結果就會開始顯示。 每個結果都包括它所屬的對象層次。

>[!NOTE]
>
>您的組織定義的自訂結構欄位可能需要24小時才能顯示，並可用於建立規則。

然後，您可以輕鬆將「事 [!DNL ExperienceEvents] 件類 [!UICONTROL 型] 」拖放至區段定義。

![](../images/ui/segment-builder/events-eventTypes.png)

依預設，只會顯示資料儲存區中已填入的架構欄位。 這包括事 [!UICONTROL 件類型]。 如果事 [!UICONTROL 件類型] ，或您只能選擇「[!UICONTROL Any]」作為 [!UICONTROL 事件類型，請選擇]Fields旁的「 ************ ShowShow fullDear」（全部顯示）「可用OradChad」(Orad)「可用OradChad」(OrayVailable Fields)」(可用Ciable 再次選擇齒輪表徵圖以返回「 **[!UICONTROL Fields]** 」(欄位 [!UICONTROL )頁籤，您現在應該可以查看多個「] Event Types」（事件類型）和模式欄位，而不管它們是否包含資料。

![](../images/ui/segment-builder/show-populated.png)

### 受眾

「對 **[!UICONTROL 像]** 」索引標籤會列出從外部來源匯入的所有對象，例如Adobe Audience Manager，以及在內部建立的對象 [!DNL Experience Platform]。

在「對 **[!UICONTROL 像]** 」索引標籤上，您可以將所有可用來源視為資料夾群組。 當您選取資料夾時，可檢視可用的子資料夾和對象。 此外，您可以選取資料夾圖示（如最右側的影像所示），以檢視資料夾結構（核取標籤表示您目前所在的資料夾），並透過選取樹狀結構中資料夾的名稱，輕鬆地在資料夾間導覽。

您可以將滑鼠指標暫留在ⓘ對象旁，以檢視有關對象的資訊，包括其ID、說明和資料夾階層，以找出對象。

![](../images/ui/segment-builder/audience-folder-structure.png)

您也可以使用搜 [!UICONTROL 尋列] (使用 [Lucene的搜尋語法)來搜尋「](https://docs.microsoft.com/en-us/azure/search/query-lucene-syntax)觀眾」。 在「對 **[!UICONTROL 像]** 」索引標籤中，選取頂層檔案夾會顯示搜尋列，讓您在該檔案夾內進行搜尋。 只有輸入完整字詞後，搜尋結果才會開始填入。 例如，若要尋找名為 [!UICONTROL 的對象] ，請 `Online Shoppers`開始在搜尋列中輸入「線上」。 在完整輸入&quot;Online&quot;後，會顯示包含&quot;Online&quot;的搜尋結果。

## 規則產生器畫布 {#rule-builder-canvas}

區段定義是用於描述目標對象之主要特性或行為的規則集合。 這些規則是使用位於中心的規則產生器畫布來建立的 [!DNL Segment Builder]。

若要將新規則新增至區段定義，請從「欄位」標籤拖曳圖格 **** ，並將其拖曳至規則產生器畫布。 然後，您會根據所新增資料的類型，看到內容特定的選項。 可用的資料類型包括：字串、日期、 [!DNL ExperienceEvents]事件 [!UICONTROL 類型]和 [!UICONTROL 觀眾]。

![](../images/ui/segment-builder/rule-builder-canvas.png)

### 新增觀眾

您可以從「對象」索引標籤將對象拖放至 **[!UICONTROL 規則產生器畫布上]** ，以參考新區段定義中的對象成員資格。 這可讓您在新區段規則中加入或排除對象成員資格作為屬性。

對於 [!DNL Platform] 使用建立 [!DNL Segment Builder]的觀眾，您可以選擇將觀眾轉換為用於該觀眾區段定義的規則集。 此轉換會建立規則邏輯的復本，然後可修改該邏輯，而不會影響原始區段定義。 在將區段定義轉換為規則邏輯之前，請確定您已儲存區段定義的任何最近變更。

>[!NOTE]
>
>從外部來源新增對象時，只會參考對象會籍。 您無法將對象轉換為規則，因此，用於建立原始對象的規則無法在新區段定義中修改。

![](../images/ui/segment-builder/add-audience-to-segment.png)

如果在將觀眾轉換為規則時發生任何 [!DNL Segment Builder] 衝突，將嘗試將現有選項保留至其最佳能力。

### 程式碼檢視

或者，您也可以檢視在中建立之規則的程式碼型版本 [!DNL Segment Builder]。 在規則產生器畫布中建立規則後，您可以選取「程式碼檢視」 **** ，將區段視為PQL。

![](../images/ui/segment-builder/code-view.png)

程式碼檢視提供一個按鈕，可讓您複製要用於API呼叫的區段值。 若要取得區段的最新版本，請確定您已儲存區段的最新變更。

![](../images/ui/segment-builder/copy-code.png)

## 容器

區段規則依其列出順序進行評估。 容器允許使用巢狀查詢來控制執行順序。

在規則產生器畫布中至少新增一個方塊後，您就可以開始新增容器。 若要建立新容器，請選取圖格右上角的橢圓(...)，然後選取「新增容 **[!UICONTROL 器」]**。

![](../images/ui/segment-builder/add-container.png)

新容器會以第一個容器的子系出現，但您可以拖曳並移動容器來調整階層。 容器的預設行為是「包[!UICONTROL 含]」提供的屬性、事件或對象。 您可以選取方塊左上角的「包含」，並選取「排除」，將規則設定為符合容器條件的「排除[!UICONTROL 」描述檔]****。

您也可以選取子容器上的「解除包裝容器」，將子容器擷取並內嵌至父容器。 選取子容器右上角的省略號(...)以存取此選項。

![](../images/ui/segment-builder/include-exclude.png)

選取「取消 **[!UICONTROL 包住容器]** 」(Unwrap container)後，子容器即會移除，標準會內嵌顯示。

>[!NOTE]
>
>展開容器時，請小心邏輯是否仍符合所需的區段定義。

![](../images/ui/segment-builder/unwrapped-container-inline.png)

## 合併原則

[!DNL Experience Platform] 可讓您從多個來源匯整資料並加以合併，以便瞭解每個客戶的完整視圖。 將這些資料整合在一起時，合併原則是用來 [!DNL Platform] 決定資料的優先順序以及將哪些資料合併以建立描述檔的規則。

您可以選取符合此對象行銷目的的合併原則，或使用由提供的預設合併原則 [!DNL Platform]。 您可以建立組織專屬的多個合併原則，包括建立您自己的預設合併原則。 有關為組織建立合併策略的逐步說明，請參閱有關使用UI使 [用合併策略的教程](../../profile/ui/merge-policies.md)。

要為段定義選擇合併策略，請在「欄位」( **[!UICONTROL Fields]** )頁籤上選擇齒輪表徵圖，然後使用「合併策略 **[!UICONTROL 」(]** Merge Policy)下拉菜單選擇要使用的合併策略。

![](../images/ui/segment-builder/merge-policy-selector.png)

## 區段屬性

建立區段定義時，工作區右側的「區段屬性 **** 」區段會顯示產生區段的估計大小，讓您在建立對象本身之前，視需要調整區段定義。

「區 **[!UICONTROL 段屬性]** 」區段也可讓您指定區段定義的重要資訊，包括 **[!UICONTROL 名稱]****[!UICONTROL 和說明]**。 區段定義名稱用於識別組織所定義的區段，因此應具有描述性、簡明扼要和獨特性。

當您繼續建立區段定義時，您可以選取「檢視設定檔」來檢視對象的編頁 **[!UICONTROL 預覽]**。

![](../images/ui/segment-builder/segment-properties.png)

>[!NOTE]
>
>觀眾估計是使用當天樣本資料的樣本大小產生。 如果您的描述檔儲存區中有少於100萬個實體，則會使用完整資料集；100萬到2000萬個單位使用100萬個單位；超過2000萬個單位，佔全部單位的5%。 有關產生區段估計的詳細資訊，請參閱區 [段建立教學課程的](../tutorials/create-a-segment.md#estimate-and-preview-an-audience) 「估計產生」區段。

## 後續步驟和其他資源 {#next-steps}

「區段產生器」提供豐富的工作流程，讓您將有價值的受眾與資料隔 [!DNL Real-time Customer Profile] 離。 閱讀本指南後，您現在可以：

- 使用屬性、事件和現有對象的組合來建立區段定義，做為建立區塊。
- 使用規則產生器畫布和容器來控制區段規則的執行順序。
- 檢視您潛在讀者的估計值，讓您視需要調整區段定義。
- 為排程的區段啟用所有區段定義。
- 為串流區段啟用指定的區段定義。

若要進一步了 [!DNL Segmentation Service]解，請繼續閱讀檔案，並觀賞以下影片以補充您的學習。 若要進一步瞭解UI的其他部 [!DNL Segmentation Service] 分，請閱讀使 [[!DNL Segmentation Service] 用指南](./overview.md)

>[!WARNING]
>
> 下 [!DNL Platform] 列影片中顯示的UI已過時。 請參閱上述檔案以取得最新的UI螢幕擷取和功能。

**建立區段：**

>[!VIDEO](https://video.tv.adobe.com/v/27254?quality=12&learn=on)

**建立動態區段：**

>[!VIDEO](https://video.tv.adobe.com/v/27428?quality=12&learn=on)