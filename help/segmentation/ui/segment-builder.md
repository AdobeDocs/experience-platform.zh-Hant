---
keywords: Experience Platform；主題；熱門主題；分段服務；分段服務；分段服務；使用手冊；使用手冊；分段使用手冊；分段使用手冊；分段生成器；分段生成器；
solution: Experience Platform
title: 段生成器UI指南
topic-legacy: ui guide
description: Adobe Experience PlatformUI中的段生成器提供了一個豐富的工作區，允許您與配置檔案資料元素交互。 工作區為生成和編輯規則提供了直觀的控制項，如用於表示資料屬性的拖放拼貼。
exl-id: b27516ea-8749-4b44-99d0-98d3dc2f4c65
source-git-commit: 71741a18c99a003e6401bc324822d50a266350b3
workflow-type: tm+mt
source-wordcount: '2612'
ht-degree: 1%

---

# [!DNL Segment Builder] UI指南

[!DNL Segment Builder] 提供豐富的工作區，允許您與 [!DNL Profile] 資料元素。 工作區為生成和編輯規則提供了直觀的控制項，如用於表示資料屬性的拖放拼貼。

![](../images/ui/segment-builder/segment-builder.png)

## 段定義構件塊 {#building-blocks}

>[!CONTEXTUALHELP]
>id="platform_segments_createsegment_segmentbuilder_fields"
>title="欄位"
>abstract="組成段的三個欄位類型是屬性、事件和受眾。 屬性允許您使用屬於XDM Individual Profile類的Profile屬性，事件允許您根據使用XDM ExperienceEvent資料元素進行的操作或事件建立受眾，而訪問群體允許您使用從外部源導入的受眾。"

段定義的基本構造塊是屬性和事件。 此外，現有受眾中包含的屬性和事件可以用作新定義的元件。

你可以在 **[!UICONTROL 欄位]** 的 [!DNL Segment Builder] 工作區。 **[!UICONTROL 欄位]** 包含每個主要構造塊的頁籤：&quot;[!UICONTROL 屬性]&quot;, &quot;[!UICONTROL 事件]&quot;和&quot;[!UICONTROL 觀眾]。

![](../images/ui/segment-builder/segment-fields.png)

### 屬性

的 **[!UICONTROL 屬性]** 頁籤 [!DNL Profile] 屬於屬性 [!DNL XDM Individual Profile] 類。 可展開每個資料夾以顯示其他屬性，其中每個屬性都是一個磁貼，可拖動到工作區中心的規則生成器畫布上。 的 [規則生成器畫布](#rule-builder-canvas) 將在本指南的後面更詳細地討論。

![](../images/ui/segment-builder/attributes.png)

### 活動

的 **[!UICONTROL 事件]** 頁籤允許您根據使用 [!DNL XDM ExperienceEvent] 資料元素。 您還可以在 **[!UICONTROL 事件]** 頁籤，這是常用事件的集合，使您能夠更快地建立段。

除了能夠瀏覽 [!DNL ExperienceEvent] 元素，您也可以搜索事件類型。 事件類型使用與 [!DNL ExperienceEvents]，不要求您搜索 [!DNL XDM ExperienceEvent] 類尋找正確的事件。 例如，使用搜索欄搜索&quot;cart&quot;將返回事件類型&quot;[!UICONTROL 添加購物車]&quot;和&quot;[!UICONTROL 刪除購物車]「 」，這是生成段定義時最常用的兩種操作。

可以通過在搜索欄中鍵入元件名稱來搜索任何類型的元件，該搜索欄使用 [Lucene的搜索語法](https://docs.microsoft.com/en-us/azure/search/query-lucene-syntax)。 在輸入整個詞時，搜索結果開始填充。 例如，要基於XDM欄位生成規則 `ExperienceEvent.commerce.productViews`，開始在搜索欄位中鍵入「產品視圖」。 鍵入「product」一詞後，將開始顯示搜索結果。 每個結果都包括它所屬的對象層次結構。

>[!NOTE]
>
>您的組織定義的自定義架構欄位可能需要24小時才能顯示，並且可用於構建規則。

然後可以輕鬆拖放 [!DNL ExperienceEvents] 和[!UICONTROL 事件類型]」。

![](../images/ui/segment-builder/events-eventTypes.png)

預設情況下，只顯示資料儲存中填充的架構欄位。 這包括「」[!UICONTROL 事件類型]。 如果[!UICONTROL 事件類型]「 」清單不可見，或者您只能選擇「 」[!UICONTROL 任意]&quot;作為&quot;[!UICONTROL 事件類型]，選擇 **齒輪表徵圖** 下 **[!UICONTROL 欄位]**，然後選擇 **[!UICONTROL 顯示完整XDM架構]** 在 **[!UICONTROL 可用欄位]**。 選擇 **齒輪表徵圖** 返回 **[!UICONTROL 欄位]** 頁籤，您現在應能查看多個&quot;[!UICONTROL 事件類型]&quot;和架構欄位，無論它們是否包含資料。

![](../images/ui/segment-builder/show-populated.png)

#### Adobe Analytics報告套件資料集

您可以將來自單個或多個Adobe Analytics報告套件的資料用作分段內的事件。

使用單個分析報告套件中的資料時，平台將自動向eVars添加描述符和友好名稱，使查找這些欄位更容易 [!DNL Segment Builder]。

![顯示如何使用用戶友好名稱映射泛型變數(eVar)的影像。](../images/ui/segment-builder/single-report-suite.png)

使用來自多個分析報告套件的資料時，平台 **不能** 自動將描述符或友好名稱添加到eVars。 因此，在使用分析報告套件中的資料之前，必須映射到XDM欄位。 有關將分析變數映射到XDM的詳細資訊，請參見 [Adobe Analytics源連接指南](../../sources/tutorials/ui/create/adobe-applications/analytics.md#mapping)。

例如，假設您有兩個具有以下變數的報告套件：

| 欄位 | 報表套件架構A | 報表套件架構B |
| ----- | --------------------- | --------------------- |
| eVar1 | 反向連結網域 | 已登錄Y/N |
| eVar2 | 頁面名稱 | 成員會員ID |
| eVar3 | URL | 頁面名稱 |
| eVar4 | 搜索詞 | 產品名稱 |
| 事件1 | 點擊次數 | 頁面檢視 |
| 事件2 | 頁面檢視 | 購物車新增 |
| 事件3 | 購物車新增 | 結帳 |
| 事件4 | 購買 | 購買 |

在這種情況下，可以使用以下架構映射兩個報表套件：

![顯示兩個報表套件如何映射到一個聯合架構的影像。](../images/ui/segment-builder/union-schema.png)

>[!NOTE]
>
>當通用eVar值仍被填充時，應 **不** 在段定義中（如果可能）使用它們，因為這些值可能與它們最初在報告中的內容不同。

一旦映射了報表套件，您就可以在與配置檔案相關的工作流和分段中使用這些新映射的欄位。

| 情境 | 聯合架構體驗 | 分段通用變數 | 分段映射變數 |
| -------- | ----------------------- | ----------------------------- | ---------------------------- |
| 單個報告套件 | 友好名稱描述符隨泛型變數一起提供。 <br><br>**示例：** 頁名(eVar2) | <ul><li>泛型變數包含的友好名稱描述符</li><li>查詢使用特定資料集中的資料，因為它是唯一</li></ul> | 查詢可以使用Adobe Analytics資料和可能的其他源。 |
| 多報表套裝 | 泛型變數不包含友好名稱描述符。 <br><br>**示例：** eVar2 | <ul><li>具有多個描述符的任何欄位都顯示為泛型。 這意味著UI中不顯示友好名稱。</li><li>查詢可以使用包含該eVar的任何資料集中的資料，這可能導致結果混合或不正確。</li></ul> | 查詢使用多個資料集中正確組合的結果。 |

### 對象

的 **[!UICONTROL 觀眾]** 頁籤列出從外部源(如Adobe Audience Manager)導入的所有受眾以及在 [!DNL Experience Platform]。

在 **[!UICONTROL 觀眾]** 頁籤，您可以將所有可用源作為資料夾組查看。 在選擇資料夾時，可以看到可用的子資料夾和受眾。 此外，您可以選擇資料夾表徵圖（如最右圖所示），以查看資料夾結構（複選標籤表示當前所在的資料夾），並通過選擇樹中資料夾的名稱，輕鬆地在資料夾中導航。

您可以將滑鼠懸停在受眾ⓘ旁，查看有關受眾的資訊，包括其ID、說明和資料夾層次結構，以查找受眾。

![](../images/ui/segment-builder/audience-folder-structure.png)

您還可以使用使用搜索欄搜索受眾 [Lucene的搜索語法](https://docs.microsoft.com/en-us/azure/search/query-lucene-syntax)。 在 **[!UICONTROL 觀眾]** 的子菜單。 只有輸入完整單詞後，搜索結果才會開始填充。 例如，要查找名為 `Online Shoppers`，開始在搜索欄中鍵入「Online」。 一旦「Online（聯機）」一詞已全部鍵入，將顯示包含「Online（聯機）」一詞的搜索結果。

## 規則生成器畫布 {#rule-builder-canvas}

段定義是用於描述目標受眾的關鍵特徵或行為的規則集合。 這些規則是使用位於 [!DNL Segment Builder]。

要將新規則添加到段定義，請從 **[!UICONTROL 欄位]** 頁籤並將其放到規則生成器畫布上。 然後，您將根據要添加的資料類型使用特定於上下文的選項。 可用資料類型包括：字串，日期， [!DNL ExperienceEvents]。[!UICONTROL 事件類型]和觀眾。

![](../images/ui/segment-builder/rule-builder-canvas.png)

>[!IMPORTANT]
>
>Adobe Experience Platform的最新更改已更新 `OR` 和 `AND` 事件之間的邏輯運算子。 這些更新不會影響現有段。 但是，對現有段及新段建立的所有後續更新都將受這些更改的影響。 請閱讀 [時間常數更新](./segment-refactoring.md) 的子菜單。

為屬性選擇值時，您將看到屬性可以是的枚舉值清單。

![](../images/ui/segment-builder/enum-list.png)

如果從此枚舉清單中選取一個值，則值將用實體邊框進行概述。 但是，對於使用 `meta:enum` （可變）枚舉，也可選取 **不** 清單中。 如果建立自己的值，則會用虛線邊框來概括該值，並警告該值不在枚舉清單中。

![](../images/ui/segment-builder/enum-warning.png)

### 添加受眾

您可以從 **[!UICONTROL 觀眾]** 頁籤到規則生成器畫布上，以引用新段定義中的訪問群體成員身份。 這允許您在新段規則中將受眾成員資格作為屬性包括或排除。

對於 [!DNL Platform] 建立的受眾 [!DNL Segment Builder]，您可以選擇將受眾轉換為在該受眾的段定義中使用的一組規則。 此轉換會生成規則邏輯的副本，然後可以在不影響原始段定義的情況下修改該副本。 確保在將段定義轉換為規則邏輯之前已保存對段定義的任何最近更改。

>[!NOTE]
>
>從外部源添加受眾時，僅引用受眾成員身份。 您不能將訪問群體轉換為規則，因此在新段定義中不能修改用於建立原始訪問群體的規則。

![](../images/ui/segment-builder/add-audience-to-segment.png)

如果將受眾轉換為規則時出現任何衝突， [!DNL Segment Builder] 會盡量保留現有的選項。

### 代碼視圖

或者，可以查看在 [!DNL Segment Builder]。 在規則生成器畫布中建立規則後，可以選擇 **[!UICONTROL 代碼視圖]** 將段視為PQL。

![](../images/ui/segment-builder/code-view.png)

「代碼」視圖提供了一個按鈕，允許您複製要在API調用中使用的段值。 要獲取段的最新版本，請確保已將最新更改保存到段。

![](../images/ui/segment-builder/copy-code.png)

### 聚合函式

中的聚合 [!DNL Segment Builder] 是對XDM屬性組的計算，其資料類型為數字（雙精度或整數）。 段生成器中支援的四個聚合函式是SUM、AVERAGE、MIN和MAX。

要建立聚合函式，請從左滑軌中選擇一個事件，然後將其插入 [!UICONTROL 事件] 容器。

![](../images/ui/segment-builder/select-event.png)

在「事件」容器中放置事件後，選擇省略號表徵圖(...)，然後 **[!UICONTROL 聚合]**。

![](../images/ui/segment-builder/add-aggregation.png)

現在添加聚合。 現在，您可以選擇聚合函式，選擇要聚合的屬性、等式函式以及值。 對於下例，此段將限定任何採購值總和大於$100的配置檔案，即使每個單獨採購金額小於$100。

![](../images/ui/segment-builder/filled-aggregation.png)

### 計數函式 {#count-functions}

段生成器中的計數函式用於查找指定的事件並計數它們完成的次數。 段生成器中支援的計數函式為「至少」、「最多」、「準確」、「介於」和「全部」。

要建立計數函式，請從左滑軌中選擇一個事件並將其插入 [!UICONTROL 事件] 容器。

![](../images/ui/segment-builder/add-event.png)

將事件置於「事件」容器中後，選擇 [!UICONTROL 至少1] 按鈕

![](../images/ui/segment-builder/add-count.png)

現在添加了count函式。 現在，您可以選擇count函式和該函式的值。 下面的示例將包括至少按一下一次的任何事件。

![](../images/ui/segment-builder/select-count.png)

## 容器

段規則按列出的順序進行評估。 容器允許通過使用嵌套查詢來控制執行順序。

至少將一個磁貼添加到規則生成器畫布後，就可以開始添加容器。 要建立新容器，請選擇磁貼右上角的橢圓(...)，然後選擇 **[!UICONTROL 添加容器]**。

![](../images/ui/segment-builder/add-container.png)

新容器將作為第一個容器的子容器出現，但您可以通過拖動和移動容器來調整層次結構。 容器的預設行為為「[!UICONTROL 包括]&quot;提供的屬性、事件或訪問群體。 可以將規則設定為「」[!UICONTROL 排除]通過選擇符合容器條件的配置檔案 **[!UICONTROL 包括]** 在磁貼的左上角並選擇「[!UICONTROL 排除]。

通過在子容器上選擇「取消包裝容器」，也可以提取子容器並將其內聯添加到父容器。 選擇子容器右上角的橢圓(...)以訪問此選項。

![](../images/ui/segment-builder/include-exclude.png)

一旦選擇 **[!UICONTROL 取消包裝容器]** 子容器被刪除，條件將顯示在內聯。

>[!NOTE]
>
>在展開容器時，請注意邏輯繼續滿足所需的段定義。

![](../images/ui/segment-builder/unwrapped-container-inline.png)

## 合併策略

[!DNL Experience Platform] 使您能夠將來自多個來源的資料合併在一起，以便查看您每個客戶的完整視圖。 將此資料整合在一起時，合併策略是 [!DNL Platform] 用於確定資料的優先順序以及將組合哪些資料以建立配置檔案。

您可以選擇與此受眾的市場營銷目的匹配的合併策略，或使用由 [!DNL Platform]。 您可以建立組織特有的多個合併策略，包括建立自己的預設合併策略。 有關為組織建立合併策略的逐步說明，請首先閱讀 [合併策略概述](../../profile/merge-policies/overview.md)。

要為段定義選擇合併策略，請在 **[!UICONTROL 欄位]** ，則使用 **[!UICONTROL 合併策略]** 下拉菜單，以選擇要使用的合併策略。

![](../images/ui/segment-builder/merge-policy-selector.png)

## 段屬性 {#segment-properties}

>[!CONTEXTUALHELP]
>id="platform_segments_createsegment_segmentbuilder_segmentproperties"
>title="段屬性"
>abstract="段屬性部分顯示結果段的估計大小，顯示與配置檔案總數相比的合格配置檔案數。 這樣，您就可以根據需要調整段定義，然後再構建受眾本身。"

>[!CONTEXTUALHELP]
>id="platform_segments_createsegment_segmentbuilder_refreshestimate"
>title="更新估計"
>abstract="您可以刷新段的估計值，以立即查看有多少配置檔案符合建議段的條件。 使用當天樣本資料的樣本大小生成受眾估計。"
>additional-url="https://experienceleague.adobe.com/docs/experience-platform/segmentation/tutorials/create-a-segment.html?lang=en#estimate-and-preview-an-audience" text="從文檔瞭解更多資訊"


構建段定義時， **[!UICONTROL 段屬性]** 工作區右側的部分顯示結果段的大小估計值，允許您根據需要調整段定義，然後再構建受眾本身。

的 **[!UICONTROL 段屬性]** 節也可在其中指定有關段定義的重要資訊，包括其名稱和說明。 段定義名稱用於在組織定義的段中標識段，因此應是描述性、簡潔和唯一的。

在繼續構建段定義時，可以通過選擇 **[!UICONTROL 查看配置檔案]**。

![](../images/ui/segment-builder/segment-properties.png)

>[!NOTE]
>
>使用當天樣本資料的樣本大小生成受眾估計。 如果配置檔案儲存中的實體少於100萬個，則使用完整的資料集；100萬至2000萬個單位使用100萬個單位；超過2000萬戶，佔全部用戶的5%。 有關生成段估計的詳細資訊，請參閱 [估計生成部分](../tutorials/create-a-segment.md#estimate-and-preview-an-audience) 的子菜單。

## 後續步驟 {#next-steps}

段構建器提供了豐富的工作流，允許您將可銷售的受眾與 [!DNL Real-time Customer Profile] 資料。 閱讀本指南後，您現在應能：

- 使用屬性、事件和現有受眾的組合作為構建塊建立段定義。
- 使用規則生成器畫布和容器來控制段規則的執行順序。
- 查看預期受眾的估計值，以便根據需要調整段定義。
- 啟用所有段定義以執行計劃分段。
- 為流分段啟用指定的段定義。

瞭解有關 [!DNL Segmentation Service]，請繼續閱讀文檔，並通過觀看相關視頻來補充您的學習。 瞭解有關 [!DNL Segmentation Service] UI，請閱讀 [[!DNL Segmentation Service] 使用手冊](./overview.md)
