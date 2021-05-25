---
keywords: Experience Platform；首頁；熱門主題；分段服務；分段服務；使用手冊；ui指南；分段ui指南；區段產生器；區段產生器；
solution: Experience Platform
title: 區段產生器UI指南
topic-legacy: ui guide
description: Adobe Experience Platform UI中的「區段產生器」提供豐富的工作區，可讓您與設定檔資料元素互動。 工作區提供建立和編輯規則的直覺式控制項，例如用來表示資料屬性的拖放圖磚。
exl-id: b27516ea-8749-4b44-99d0-98d3dc2f4c65
source-git-commit: 11e8acc3da7f7540421b5c7f3d91658c571fdb6f
workflow-type: tm+mt
source-wordcount: '1996'
ht-degree: 0%

---

# [!DNL Segment Builder] UI指南

[!DNL Segment Builder] 提供豐富的工作區，可讓您與資料元素 [!DNL Profile] 互動。工作區提供建立和編輯規則的直覺式控制項，例如用來表示資料屬性的拖放圖磚。

![](../images/ui/segment-builder/segment-builder.png)

## 區段定義建置區塊

區段定義的基本組成要素為屬性和事件。 此外，現有對象中包含的屬性和事件也可作為新定義的元件。

您可以在[!DNL Segment Builder]工作區左側的&#x200B;**[!UICONTROL 欄位]**&#x200B;區段中看到這些建置區塊。 **** 欄位包含每個主要建置區塊的索引標籤：「[!UICONTROL 屬性]」、「[!UICONTROL 事件]」和「[!UICONTROL 對象]」。

![](../images/ui/segment-builder/segment-fields.png)

### 屬性

**[!UICONTROL Attributes]**&#x200B;頁簽允許您瀏覽屬於[!DNL XDM Individual Profile]類的[!DNL Profile]屬性。 每個資料夾都可展開，以顯示其他屬性，其中每個屬性都是一個圖磚，可拖曳至工作區中央的規則產生器畫布上。 本指南稍後會詳細說明[規則產生器畫布](#rule-builder-canvas)。

![](../images/ui/segment-builder/attributes.png)

### 事件

**[!UICONTROL Events]**&#x200B;標籤可讓您根據使用[!DNL XDM ExperienceEvent]資料元素發生的事件或動作來建立對象。 您也可以在&#x200B;**[!UICONTROL Events]**&#x200B;標籤上找到事件類型，這是常用事件的集合，可讓您更快建立區段。

除了能夠瀏覽[!DNL ExperienceEvent]元素之外，您還可以搜索事件類型。 事件類型使用與[!DNL ExperienceEvents]相同的編碼邏輯，無需您在[!DNL XDM ExperienceEvent]類中搜索以查找正確的事件。 例如，使用搜尋列來搜尋「購物車」時，會傳回事件類型「[!UICONTROL AddCart]」和「[!UICONTROL RemoveCart]」，這是建立區段定義時最常用的兩種購物車動作。

在搜索欄中鍵入元件名稱可搜索任何類型的元件，該搜索欄使用[Lucene的搜索語法](https://docs.microsoft.com/en-us/azure/search/query-lucene-syntax)。 在輸入整個字詞時，搜尋結果會開始填入。 例如，若要根據XDM欄位`ExperienceEvent.commerce.productViews`建立規則，請開始在搜尋欄位中輸入&quot;product views&quot;。 輸入&quot;product&quot;一字後，搜尋結果就會開始顯示。 每個結果都包含其所屬的物件階層。

>[!NOTE]
>
>貴組織定義的自訂結構欄位可能需要最多24小時才會顯示，並可在建立規則時使用。

接著，您可以輕鬆將[!DNL ExperienceEvents]和「[!UICONTROL 事件類型]」拖放至區段定義中。

![](../images/ui/segment-builder/events-eventTypes.png)

依預設，只會顯示資料存放區中填入的結構欄位。 這包括「[!UICONTROL 事件類型]」。 如果「[!UICONTROL 事件類型]」清單不可見，或者您只能選擇「[!UICONTROL Any]」作為「[!UICONTROL 事件類型]」，請選擇&#x200B;**[!UICONTROL 欄位]**&#x200B;旁的&#x200B;**齒輪表徵圖**，然後選擇&#x200B;**[!UICONTROL &lt;a12/A]**]**下的**[!UICONTROL &#x200B;可用欄位。 再次選擇&#x200B;**齒輪表徵圖**&#x200B;以返回&#x200B;**[!UICONTROL 欄位]**&#x200B;頁簽，無論它們是否包含資料，您現在都應該能夠查看多個「[!UICONTROL 事件類型]」和架構欄位。

![](../images/ui/segment-builder/show-populated.png)

### 受眾

**[!UICONTROL 對象]**&#x200B;索引標籤會列出從外部來源(例如Adobe Audience Manager)匯入的所有對象，以及在[!DNL Experience Platform]中建立的對象。

在&#x200B;**[!UICONTROL 對象]**&#x200B;標籤上，您可以將所有可用來源視為資料夾群組。 選取資料夾時，可以看到可用的子資料夾和對象。 此外，您可以選取資料夾圖示（如最右側影像所示）以檢視資料夾結構（勾選記號表示您目前所在的資料夾），並透過選取樹狀結構中資料夾的名稱來輕鬆導覽資料夾。

您可以將游標暫留在對象ⓘ旁的上方，以檢視對象的相關資訊，包括其ID、說明，以及資料夾階層，以便找出對象。

![](../images/ui/segment-builder/audience-folder-structure.png)

您也可以使用搜尋列來搜尋對象，搜尋列利用[Lucene的搜尋語法](https://docs.microsoft.com/en-us/azure/search/query-lucene-syntax)。 在&#x200B;**[!UICONTROL 對象]**&#x200B;標籤中，選取頂層資料夾會顯示搜尋列，讓您在該資料夾中進行搜尋。 只有輸入完整的字詞後，搜尋結果才會開始填入。 例如，若要尋找名為`Online Shoppers`的對象，請開始在搜尋列中輸入「Online」。 完整輸入「Online」後，將顯示包含「Online」字的搜索結果。

## 規則產生器畫布{#rule-builder-canvas}

區段定義是一組規則，用於描述目標對象的關鍵特徵或行為。 這些規則是使用位於[!DNL Segment Builder]中央的規則產生器畫布來建立。

若要將新規則新增至區段定義，請從&#x200B;**[!UICONTROL Fields]**&#x200B;標籤拖曳圖磚，並將其拖曳至規則產生器畫布。 接著，系統會根據要新增的資料類型，為您顯示內容特定選項。 可用的資料類型包括：字串、日期、[!DNL ExperienceEvents]、「[!UICONTROL 事件類型]」和對象。

![](../images/ui/segment-builder/rule-builder-canvas.png)

>[!IMPORTANT]
>
>Adobe Experience Platform的最新變更已更新事件之間`OR`和`AND`邏輯運算子的使用方式。 這些更新不會影響現有區段。 但是，對現有區段和新區段建立的所有後續更新都將受到這些變更的影響。 請閱讀[時間常數更新](./segment-refactoring.md)以了解更多資訊。

### 新增對象

您可以從&#x200B;**[!UICONTROL Audience]**&#x200B;標籤將對象拖放至規則產生器畫布，以參考新區段定義中的對象成員資格。 這可讓您在新區段規則中，將對象成員資格納入或排除為屬性。

對於使用[!DNL Segment Builder]建立的[!DNL Platform]對象，您有選項可將對象轉換為該對象在區段定義中使用的一組規則。 此轉換會製作規則邏輯的復本，然後可在不影響原始區段定義的情況下加以修改。 將區段定義轉換為規則邏輯之前，請確定您已儲存區段定義的近期變更。

>[!NOTE]
>
>從外部來源新增對象時，只會參考對象成員資格。 您無法將對象轉換為規則，因此，用於建立原始對象的規則無法在新區段定義中修改。

![](../images/ui/segment-builder/add-audience-to-segment.png)

如果在將對象轉換為規則時發生任何衝突， [!DNL Segment Builder]會嘗試將現有選項保留為最佳能力。

### 程式碼檢視

或者，您也可以檢視在[!DNL Segment Builder]中建立之規則的程式碼版本。 在規則產生器畫布中建立規則後，您可以選取&#x200B;**[!UICONTROL 程式碼檢視]** ，將區段顯示為PQL。

![](../images/ui/segment-builder/code-view.png)

程式碼檢視提供一個按鈕，可讓您複製要在API呼叫中使用的區段值。 若要取得最新版區段，請確定您已儲存區段的最新變更。

![](../images/ui/segment-builder/copy-code.png)

### 聚合函式

[!DNL Segment Builder]中的匯總是對資料類型為數字（雙倍或整數）的一組XDM屬性的計算。 「區段產生器」中支援的四個匯總函式為「總和」、「平均」、「最小值」和「最大值」。

若要建立匯總函式，請從左側邊欄選取事件，並將其插入[!UICONTROL Events]容器中。

![](../images/ui/segment-builder/select-event.png)

將事件放入「事件」容器後，選取點圖示(...)，後面接著&#x200B;**[!UICONTROL 匯總]**。

![](../images/ui/segment-builder/add-aggregation.png)

現在已新增匯總。 您現在可以選取匯總函式、選擇要匯總的屬性、相等函式以及值。 在以下範例中，此區段會限定任何購買值總和大於$100的設定檔，即使每次個別購買小於$100亦然。

![](../images/ui/segment-builder/filled-aggregation.png)

### 計數函式{#count-functions}

區段產生器中的計數函式可用來尋找指定的事件並計算完成的次數。 「區段產生器」中支援的計數函式為「至少」、「最多」、「精確」、「介於」和「全部」。

若要建立計數函式，請從左側邊欄選取事件，並將其插入至[!UICONTROL Events]容器中。

![](../images/ui/segment-builder/add-event.png)

將事件放入「事件」容器後，請選取「[!UICONTROL 至少1]」按鈕。

![](../images/ui/segment-builder/add-count.png)

現在已新增計數函式。 您現在可以選取計數函式和函式的值。 以下範例將包含至少點擊一次的事件。

![](../images/ui/segment-builder/select-count.png)

## 容器

區段規則的評估順序為。 容器可透過使用巢狀查詢來控制執行順序。

在您將至少一個圖磚新增至規則產生器畫布後，就可以開始新增容器。 若要建立新容器，請選取圖磚右上角的點(...)，然後選取&#x200B;**[!UICONTROL 新增容器]**。

![](../images/ui/segment-builder/add-container.png)

新容器顯示為第一個容器的子容器，但您可以拖曳和移動容器來調整階層。 容器的預設行為是「[!UICONTROL Include]」提供的屬性、事件或對象。 您可以選取方塊左上角的&#x200B;**[!UICONTROL Include]**&#x200B;並選取「[!UICONTROL Exclude]」，將規則設為符合容器條件的「[!UICONTROL Exclude]」設定檔。

您也可以選取子容器上的「取消包裝容器」，以內嵌方式擷取子容器並新增至父容器。 選取子容器右上角的點(...)以存取此選項。

![](../images/ui/segment-builder/include-exclude.png)

選取&#x200B;**[!UICONTROL 取消包裝容器]**&#x200B;後，子容器即會移除，條件會內嵌顯示。

>[!NOTE]
>
>展開容器時，請留意邏輯是否仍符合所需的區段定義。

![](../images/ui/segment-builder/unwrapped-container-inline.png)

## 合併策略

[!DNL Experience Platform] 可讓您從多個來源匯整資料，並加以結合，以便查看每個客戶的完整檢視。將此資料集合在一起時，[!DNL Platform]會使用合併原則來判斷資料的優先順序，以及要合併哪些資料來建立設定檔。

您可以選取符合您針對此對象之行銷目的的合併原則，或使用[!DNL Platform]提供的預設合併原則。 您可以建立組織特有的多個合併原則，包括建立自己的預設合併原則。 有關為貴組織建立合併策略的逐步說明，請從閱讀[合併策略概述](../../profile/merge-policies/overview.md)開始。

要為段定義選擇合併策略，請在&#x200B;**[!UICONTROL 欄位]**&#x200B;頁簽上選擇齒輪表徵圖，然後使用&#x200B;**[!UICONTROL 合併策略]**&#x200B;下拉菜單選擇要使用的合併策略。

![](../images/ui/segment-builder/merge-policy-selector.png)

## 區段屬性

建立區段定義時，工作區右側的&#x200B;**[!UICONTROL 區段屬性]**&#x200B;區段會顯示所產生區段的預估大小，讓您在建立對象本身之前，可視需要調整區段定義。

您也可以在&#x200B;**[!UICONTROL 區段屬性]**&#x200B;區段中指定有關區段定義的重要資訊，包括其名稱和說明。 區段定義名稱是用來在組織定義的區段中識別區段，因此應具有描述性、簡潔明瞭且獨特。

當您繼續建立區段定義時，可以選取&#x200B;**[!UICONTROL 檢視設定檔]**&#x200B;來檢視對象的編頁預覽。

![](../images/ui/segment-builder/segment-properties.png)

>[!NOTE]
>
>觀眾預估是使用當天範例資料的樣本大小產生。 如果您的設定檔存放區中實體少於100萬個，則會使用完整資料集；100萬至2000萬個實體使用100萬個實體；超過2,000萬個實體，佔實體總數的5%。 有關生成段估計的更多資訊，請參見段建立教程的[估計生成部分](../tutorials/create-a-segment.md#estimate-and-preview-an-audience)。

## 下一步 {#next-steps}

區段產生器提供豐富的工作流程，可讓您將有價對象與[!DNL Real-time Customer Profile]資料隔離。 閱讀本指南後，您現在應該能夠：

- 使用屬性、事件和現有對象的組合作為建置區塊，建立區段定義。
- 使用規則產生器畫布和容器來控制執行區段規則的順序。
- 檢視潛在對象的預估值，以便您視需要調整區段定義。
- 啟用排程分段的所有區段定義。
- 為串流細分啟用指定的區段定義。

若要進一步了解[!DNL Segmentation Service]，請繼續閱讀本檔案，並觀看相關影片以補充學習內容。 若要進一步了解[!DNL Segmentation Service] UI的其他部分，請閱讀[[!DNL Segmentation Service] 使用手冊](./overview.md)
