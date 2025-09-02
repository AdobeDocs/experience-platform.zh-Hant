---
solution: Experience Platform
title: 區段產生器UI指南
description: Adobe Experience Platform UI中的區段產生器提供豐富的工作區，可讓您與設定檔資料元素互動。 工作區提供用於建置和編輯規則的直覺式控制項，例如用來表示資料屬性的拖放圖磚。
exl-id: b27516ea-8749-4b44-99d0-98d3dc2f4c65
source-git-commit: 52571689c97fdc2ed052b53537e736f03d666ad5
workflow-type: tm+mt
source-wordcount: '5174'
ht-degree: 11%

---

# [!DNL Segment Builder] 使用者介面指南

>[!NOTE]
>
>本指南說明如何使用區段產生器，透過&#x200B;**區段定義**&#x200B;建立對象。 若要瞭解如何使用對象構成建立對象，請參閱[對象構成UI指南](./audience-composition.md)。

[!DNL Segment Builder]提供豐富的工作區，可讓您與[!DNL Profile]資料元素互動。 工作區提供用於建置和編輯規則的直覺式控制項，例如用來表示資料屬性的拖放圖磚。

![會顯示區段產生器UI。](../images/ui/segment-builder/segment-builder.png)

## 分段定義建置區塊 {#building-blocks}

>[!CONTEXTUALHELP]
>id="platform_segments_createsegment_segmentbuilder_fields"
>title="欄位"
>abstract="構成區段定義的三種欄位類型為屬性、事件和對象。屬性可讓您使用屬於 XDM 個人設定檔類別的設定檔屬性，事件可讓您根據使用 XDM ExperienceEvent 資料元素發生的動作或事件來建立對象，而對象則可讓您使用從外部來源匯入的對象。"

>[!CONTEXTUALHELP]
>id="platform_segmentation_segmentbuilder_showfullxdmschema"
>title="呈現完整的 XDM 結構描述"
>abstract="預設情況下，僅會顯示內含資料的欄位。啟用此選項會顯示 XDM 結構描述中所有欄位。"

>[!CONTEXTUALHELP]
>id="platform_segmentation_segmentbuilder_showdeprecatedfields"
>title="顯示已棄用的欄位"
>abstract="預設情況下會顯示已棄用的 XDM 欄位。啟用此選項會顯示已棄用的 XDM 欄位。"

區段定義的基本建置區塊是屬性和事件。 此外，現有對象中包含的屬性和事件可作為新定義的元件。

>[!CONTEXTUALHELP]
>id="platform_segments_createsegment_segmentbuilder_summarydata"
>title="摘要資料"
>abstract="僅有設定檔屬性會顯示摘要資料，事件或對象屬性則<b>不會</b>顯示。<br/><br/>於下列情況下，可能不會顯示設定檔屬性的摘要資料： <ol><li>該屬性部分值的長度超過 100 個字元。</li><li>該屬性有超過 3000 個唯一值。</li></ol>"

>[!NOTE]
>
>如果您選取屬性的資訊泡泡，則可檢視欄位的值分佈（也稱為摘要資料）。 這些是&#x200B;**僅**&#x200B;可在屬性標籤中使用，且不可在事件或對象標籤中使用。
>
>如果屬性符合下列條件，則會顯示摘要資料：屬性的所有值都在100個字元以內，而且屬性的唯一值在3000個以內。
>
>但是，如果屬性是透過關聯性連結至設定檔的多實體資料，則&#x200B;**不會**&#x200B;有摘要資料。 例如，如果您有名為`Vehicle`的自訂結構描述，則&#x200B;**結構描述中的**&#x200B;屬性`Vehicle`將&#x200B;**沒有**&#x200B;摘要資料。

您可以在&#x200B;**[!UICONTROL 工作區左側的]**&#x200B;欄位[!DNL Segment Builder]區段中看到這些建置區塊。 **[!UICONTROL 欄位]**&#x200B;包含每個主要建置區塊的標籤：「[!UICONTROL 屬性]」、「[!UICONTROL 事件]」和「[!UICONTROL 對象]」。

![區段產生器的欄位區段已反白顯示。](../images/ui/segment-builder/segment-fields.png)

### 屬性

**[!UICONTROL 屬性]**&#x200B;索引標籤可讓您瀏覽屬於[!DNL Profile]類別的[!DNL XDM Individual Profile]屬性。 每個資料夾都可以展開以顯示其他屬性，其中每個屬性都是一個可拖曳至工作區中央規則產生器畫布的圖磚。 本指南稍後會更詳細地討論[規則產生器畫布](#rule-builder-canvas)。

![區段產生器欄位的屬性區段會醒目提示。](../images/ui/segment-builder/attributes.png)

### 活動

**[!UICONTROL 事件]**&#x200B;索引標籤可讓您根據使用[!DNL XDM ExperienceEvent]資料元素發生的事件或動作來建立對象。 您也可在&#x200B;**[!UICONTROL 事件]**&#x200B;標籤上找到事件型別，這是常用事件的集合，可讓您更快速地建立區段定義。

除了可以瀏覽[!DNL ExperienceEvent]元素之外，您還可以搜尋事件型別。 事件型別使用與[!DNL ExperienceEvents]相同的編碼邏輯，不需要您搜尋[!DNL XDM ExperienceEvent]類別以尋找正確的事件。 例如，使用搜尋列搜尋「購物車」會傳回事件型別&quot;[!UICONTROL AddCart]&quot;和&quot;[!UICONTROL RemoveCart]&quot;，這是建立區段定義時最常用的兩個購物車動作。

任何型別的元件都可透過在搜尋列中輸入名稱來搜尋，該搜尋列使用[Lucene的搜尋語法](https://docs.microsoft.com/en-us/azure/search/query-lucene-syntax)。 輸入整個字詞時，搜尋結果會開始填入。 例如，若要根據XDM欄位`ExperienceEvent.commerce.productViews`建立規則，開始在搜尋欄位中輸入「產品檢視」。 輸入「product」一詞後，搜尋結果就會開始出現。 每個結果都包含其所屬的物件階層。

>[!NOTE]
>
>貴組織定義的自訂結構欄位最多可能需要24小時的時間才會顯示，並且可在建置規則中使用。

然後，您就可以輕鬆地將[!DNL ExperienceEvents]和&quot;[!UICONTROL 事件型別]&quot;拖放到您的區段定義中。

![區段產生器UI的事件區段已反白顯示。](../images/ui/segment-builder/events.png)

依預設，只會顯示資料存放區中填入的結構欄位。 這包括[!UICONTROL 事件型別]。 如果「[!UICONTROL 事件型別]」清單未顯示，或您只能選取「[!UICONTROL 任何]」作為「[!UICONTROL 事件型別]」，請選取「**欄位**」旁的&#x200B;**[!UICONTROL 齒輪圖示]**，然後在「**[!UICONTROL 可用欄位]**」下選取「**[!UICONTROL 顯示完整XDM結構描述]**」。 再次選取&#x200B;**齒輪圖示**&#x200B;以返回&#x200B;**[!UICONTROL 欄位]**&#x200B;標籤，您現在應該能夠檢視多個「[!UICONTROL 事件型別]」和結構描述欄位，無論它們是否包含資料。

![選項按鈕可讓您在只顯示含有資料的欄位或顯示所有XDM欄位之間選擇，反白顯示。](../images/ui/segment-builder/show-populated.png)

#### Adobe Analytics報表套裝資料集

您可以將單一或多個Adobe Analytics報表套裝的資料當成區段內的事件使用。

使用單一Analytics報告套裝中的資料時，Experience Platform會自動新增描述項和易記名稱至eVar，以便在[!DNL Segment Builder]中更輕鬆地尋找這些欄位。

![此影像顯示一般變數(eVar)如何以使用者易記名稱對應。](../images/ui/segment-builder/single-report-suite.png)

使用來自多個Analytics報表套裝的資料時，Experience Platform **無法**&#x200B;自動將描述項或易記名稱新增到eVar。 因此，您必須先對應至XDM欄位，才能使用Analytics報表套裝的資料。 如需將Analytics變數對應至XDM的詳細資訊，請參閱[Adobe Analytics來源連線指南](../../sources/tutorials/ui/create/adobe-applications/analytics.md#mapping)。

例如，假設您有兩個報表套裝包含以下變數：

| 欄位 | 報表套裝結構描述A | 報告套裝結構描述B |
| ----- | --------------------- | --------------------- |
| EVAR1 | 反向連結網域 | 登入Y/N |
| EVAR2 | 頁面名稱 | 會員忠誠度ID |
| EVAR3 | URL | 頁面名稱 |
| EVAR4 | 搜尋字詞 | 產品名稱 |
| event1 | 點按次數 | 頁面檢視 |
| event2 | 頁面檢視 | 購物車新增 |
| event3 | 購物車新增 | 結帳次數 |
| event4 | 購買次數 | 購買次數 |

在此情況下，您可以使用以下結構描述對應這兩個報表套裝：

![顯示如何將兩個報表套裝對應到一個聯合結構描述的影像。](../images/ui/segment-builder/union-schema.png)

>[!NOTE]
>
>雖然仍會填入通用eVar值，但您應該&#x200B;**不**&#x200B;在區段定義（如果可能）中使用這些值，因為這些值的意義可能與其報表中的原始值不同。

報告套裝對應後，您即可在設定檔相關工作流程和區段中使用這些新對應的欄位。

| 情境 | 聯合結構描述體驗 | 分段通用變數 | 分段對應變數 |
| -------- | ----------------------- | ----------------------------- | ---------------------------- |
| 單一報告套裝 | 泛型變數中包含易記名稱描述項。 <br><br>**範例：**&#x200B;頁面名稱(eVar2) | <ul><li>泛型變數中包含的易記名稱描述項</li><li>查詢使用來自特定資料集的資料，因為這是唯一使用資料</li></ul> | 查詢可以使用Adobe Analytics資料，也可能使用其他來源。 |
| 多報表套裝 | 泛型變數未包含任何易記名稱描述元。 <br><br>**範例：** eVar2 | <ul><li>任何具有多個描述元的欄位都會顯示為一般。 這表示UI中未出現任何好記的名稱。</li><li>查詢可以使用任何包含eVar的資料集中的資料，這可能會導致混合或不正確的結果。</li></ul> | 查詢會正確使用來自多個資料集的合併結果。 |

### 客群

>[!CONTEXTUALHELP]
>id="platform_segmentation_segmentBuilder_b2b_decomposition"
>title="複雜評估"
>abstract="下面的運算式太複雜，無法作為單一對象來表達。若要在相同區段定義中同時使用 B2B 規則和以人員為基礎的事件，請依照下列步驟操作。<ol><li>建立僅引用以人員為基礎事件的區段定義，並將其另存為自己專有的區段定義。</li><li>在新的區段定義中，匯入先前建立的區段定義，同時引用 B2B 規則。</li></ol>"

>[!CONTEXTUALHELP]
>id="platform_segmentation_segmentbuilder_externalaudiences"
>title="外部客群"
>abstract="透過客群索引標籤匯入的客群，現在會自動透過客群入口網站顯示。可以隨時取得來自 Audience Manager、Customer Journey Analytics、Segment Match 和其他自訂整合的客群，無需事先在客戶細分工具中進行設定。自 2025 年 9 月 1 日起，所有客群將僅能透過 Unified Search 進行擷取，並且不再支援先前的工作流程。"
>additional-url="https://experienceleague.adobe.com/zh-hant/docs/experience-platform/segmentation/ui/audience-portal#list" text="Audience Portal"

>[!NOTE]
>
>對於在Experience Platform中建立的對象，只會顯示具有&#x200B;**相同**&#x200B;合併原則的對象。

**[!UICONTROL 對象]**&#x200B;索引標籤會列出從外部來源(例如Adobe Audience Manager或Customer Journey Analytics)匯入的所有對象，以及在[!DNL Experience Platform]內建立的對象。

在&#x200B;**[!UICONTROL 對象]**&#x200B;標籤上，您可以將所有可用的來源視為一組資料夾。 選取資料夾時，可以看到可用的子資料夾和對象。 此外，您可以選取資料夾圖示（如最右邊影像所示）來檢視資料夾結構（核取記號代表您目前所在的資料夾），並藉由選取樹狀結構中資料夾的名稱，輕鬆導覽至資料夾。

您可以將滑鼠停留在對象旁的ⓘ結上，即可檢視對象的相關資訊，包括其ID、說明，以及用來尋找對象的資料夾階層。

![展示資料夾階層如何為對象運作的影像。](../images/ui/segment-builder/audience-folder-structure.png)

## 規則產生器畫布 {#rule-builder-canvas}

>[!IMPORTANT]
>
>自2024年6月版本起，「本月」和「今年」時間限制分別代表「月至今」和「年初至今」。 例如，如果您在7月18日建立受眾，尋找「本月生日發生的所有客戶」，則受眾會獲得其生日從7月1日到7月31日的所有客戶。 8月1日當天，此對象將收到生日從8月1日到8月31日的所有客戶。
>
>先前，「本月」和「今年」分別代表30天和365天，分別未能說明月份為31天和閏年。
>
>為了更新您的對象邏輯，請重新儲存您先前建立的對象。

區段定義是規則的集合，用來描述目標對象的主要特性或行為。 這些規則是使用位於[!DNL Segment Builder]中心的規則產生器畫布所建立。

若要將新規則新增至您的區段定義，請從&#x200B;**[!UICONTROL 欄位]**&#x200B;標籤中拖曳圖磚，並將其拖曳至規則產生器畫布。 接著，會根據要新增的資料型別，為您顯示內容專屬選項。 可用的資料型別包括：字串、日期、[!DNL ExperienceEvents]、[!UICONTROL 事件型別]和對象。

![空白規則產生器畫布。](../images/ui/segment-builder/rule-builder-canvas.png)

>[!IMPORTANT]
>
>Adobe Experience Platform的最新變更已更新事件之間`OR`和`AND`邏輯運運算元的使用情形。 這些更新不會影響現有的區段定義。 然而，現有區段定義和新建立區段定義的所有後續更新都將受這些變更影響。 如需詳細資訊，請閱讀[時間常數更新](./segment-refactoring.md)。

選取屬性的值時，您會看到屬性可以成為的列舉值清單。

![顯示屬性可以成為之列舉值清單的影像。](../images/ui/segment-builder/enum-list.png)

如果從此列舉清單中選取值，該值將以實線框線列出。 不過，對於使用`meta:enum` （可變）列舉的欄位，您也可以從列舉清單中選取&#x200B;**not**&#x200B;的值。 如果您建立自己的值，則會以虛線框線標示出來，並警告您該值不在列舉清單中。

![如果您插入的值不是列舉清單的一部分，則會顯示警告。](../images/ui/segment-builder/enum-warning.png)

如果您要建立多個值，可以使用大量上傳一次新增所有值。 選取![加號圖示](/help/images/icons/add-circle.png)以大量顯示&#x200B;**[!UICONTROL 新增值]**&#x200B;彈出視窗。

![加號圖示會反白顯示，顯示您可以選取以存取大量上傳彈出視窗的按鈕。](../images/ui/segment-builder/add-bulk-values.png)

在&#x200B;**[!UICONTROL 大量新增值]**&#x200B;彈出視窗上，您可以上傳CSV或TSV檔案。

![顯示大量彈出視窗中的新增值。 您可以選取用來上傳CSV或TSV檔案的對話方塊會反白顯示。](../images/ui/segment-builder/bulk-values-popover.png)

或者，您也可以手動新增逗號分隔值。

![顯示大量彈出視窗中的新增值。 您可以用來插入值的對話方塊和新增的值都會反白顯示。](../images/ui/segment-builder/bulk-values-comma-separated.png)

請注意，最多允許250個值。 如果超過此數量，則必須先移除一些值，才能新增更多值。

![會顯示警告，指出您已達到值的數量上限。](../images/ui/segment-builder/maximum-values.png)

### 新增客群

>[!CONTEXTUALHELP]
>id="platform_segmentation_segmentbuilder_addaudiences"
>title="搜尋更新"
>abstract="現有搜尋系統已更新為使用整合式搜尋。整合式搜尋讓您可以更輕鬆果斷地為區段會籍搜尋對象。"

您可以從&#x200B;**[!UICONTROL 對象]**&#x200B;標籤將對象拖放到規則產生器畫布上，以參考新區段定義中的對象成員資格。 這可讓您在新的區段定義規則中，以屬性的形式包含或排除對象成員資格。

針對使用[!DNL Experience Platform]建立的[!DNL Segment Builder]個對象，您可以選擇將對象轉換為用於該對象區段定義的規則集。 此轉換會建立規則邏輯的副本，之後可加以修改而不會影響原始區段定義。 在將區段定義轉換為規則邏輯之前，請確定您已儲存對區段定義所做的任何最近變更。

>[!NOTE]
>
>從外部來源新增對象時，只會參考對象成員資格。 您無法將對象轉換為規則，因此在新的區段定義中無法修改用來建立原始對象的規則。

![此影像顯示如何將對象屬性轉換為規則。](../images/ui/segment-builder/add-audience-to-segment.png)

如果在將對象轉換為規則時發生任何衝突，[!DNL Segment Builder]將嘗試儘可能保留現有選項。

### 程式碼檢視

或者，您也可以檢視在[!DNL Segment Builder]中建立的規則之程式碼型版本。 在規則產生器畫布中建立規則後，您可以選取「**[!UICONTROL 程式碼檢視]**」來檢視您的區段定義為PQL。

![程式碼檢視按鈕會反白顯示，讓您看到區段定義為PQL。](../images/ui/segment-builder/code-view.png)

程式碼檢視提供按鈕，可讓您複製區段定義的值，以用於API呼叫。 若要取得最新版本的區段定義，請確定您已儲存對區段定義進行的最新變更。

![反白顯示複製代碼按鈕，可讓您](../images/ui/segment-builder/copy-code.png)

### 聚合函式

[!DNL Segment Builder]中的彙總是資料型別為數字（雙精度或整數）的一組XDM屬性的計算。 區段產生器中支援的四個彙總函式為SUM、AVERAGE、MIN和MAX。

若要建立彙總函式，請從左側邊欄選取事件，然後將其插入[!UICONTROL 事件]容器。

![事件區段已反白顯示。](../images/ui/segment-builder/events.png)

將事件放入Events容器後，選取省略符號圖示(...)，然後選取&#x200B;**[!UICONTROL 彙總]**。

![彙總文字會反白顯示。 選取此選項可讓您選取彙總函式。](../images/ui/segment-builder/add-aggregation.png)

現在已新增彙總。 您現在可以選取彙總函式、選擇要彙總的屬性、相等函式以及值。 在以下範例中，即使每次購買少於$100，此區段定義仍會限定購買值總和大於$100的任何設定檔。

![事件規則，顯示彙總函式。](../images/ui/segment-builder/filled-aggregation.png)

### 計數函式 {#count-functions}

區段產生器中的計數函式用於尋找指定事件並計算其完成次數。 「區段產生器」中支援的計數函式為「最少」、「最多」、「完全符合」、「介於」和「全部」。

若要建立計數函式，請從左側邊欄選取一個事件，並將其插入至[!UICONTROL 事件]容器。

![事件欄位會反白顯示。](../images/ui/segment-builder/events.png)

將事件放入「事件」容器後，請選取[!UICONTROL 至少1]按鈕。

![至少會反白顯示，顯示要選取的區域以檢視完整的計數函式清單。](../images/ui/segment-builder/add-count.png)

現在已新增計數函式。 您現在可以選取計數函式及函式值。 以下範例將包含具有至少一次點按的任何事件。

![會顯示並反白計數函式的清單。](../images/ui/segment-builder/select-count.png)

### 時間限制 {#time-constraints}

時間限制可讓您對以時間為基礎的屬性、事件以及事件之間的順序套用時間限制。

>[!IMPORTANT]
>
>如果您在2024年6月之前以「本月」或「今年」時間限制建立區段定義，則需要重新儲存區段定義。 2024年6月之前，「本月」是以30天為基準，而「今年」是以365天為基準。

>[!NOTE]
>
>[忽略年度時間限制](./ignore-year.md)和[規則層級時間限制](./segment-refactoring.md)兩者先前都已重構，在連結的概覽中有更多資訊可用。

可用的時間限制清單如下：

+++ 可用的時間限制

>[!NOTE]
>
>所有時間限制都是以UTC為基礎。
>
>此外，如果已啟用[!UICONTROL 忽略年份]核取方塊，則年份將&#x200B;**不會**&#x200B;作為區段定義評估的一部分進行比較。

| 時間限制 | 說明 | 可啟用忽略年份 | 範例 |
| --------------- | ----------- | ------------------- | ------- |
| 今天 | 正在比較的屬性或事件必須發生在今天&#x200B;****。 | 是 | ![正在使用的「今天」時間限制範例。](../images/ui/segment-builder/time-constraints/today.png){width="100" zoomable="yes"} |
| 昨天 | 進行比較的屬性或事件&#x200B;**必須**&#x200B;發生在昨天。 | 是 | ![使用的「昨天」時間限制範例。](../images/ui/segment-builder/time-constraints/yesterday.png){width="100" zoomable="yes"} |
| 本月 | 正在比較的屬性或事件必須&#x200B;**發生在這個行事曆月份。** | 是 | ![正在使用的「本月」時間限制範例。](../images/ui/segment-builder/time-constraints/this-month.png){width="100" zoomable="yes"} |
| 今年 | 正在比較的屬性或事件&#x200B;**必須**&#x200B;發生在此行事曆年度。 | 無 | ![正在使用的「今年」時間限制範例。](../images/ui/segment-builder/time-constraints/this-year.png){width="100" zoomable="yes"} |
| 自訂日期 | 進行比較的屬性或事件&#x200B;**必須**&#x200B;在指定的日期發生。 | 是 | ![正在使用的「自訂日期」時間限制範例。](../images/ui/segment-builder/time-constraints/custom-date.png){width="100" zoomable="yes"} |
| 最近 | 進行比較的屬性或事件&#x200B;**必須**&#x200B;發生在最後選擇的時段內。 在評估時間之前，這段時間是&#x200B;**包含**。 | 無 | ![正在使用的「最近」時間限制範例。](../images/ui/segment-builder/time-constraints/in-last.png){width="100" zoomable="yes"} |
| 從（至） | 正在比較的屬性或事件&#x200B;**必須**&#x200B;發生在所選的兩個行事曆日期內。 此時間週期為兩個日期的&#x200B;**包含**。 | 是，如果自訂日期 | ![正在使用的「從到」範例。](../images/ui/segment-builder/time-constraints/from-to.png){width="100" zoomable="yes"} |
| 期間 | 進行比較的屬性或事件&#x200B;**必須**&#x200B;發生在選取的月份或年度內。 如果選取月份，您必須同時選擇屬性或事件發生所在的月份和年份。  如果選取年份，您只需要選擇屬性或事件發生的年份。 如果您選取月份，也可以啟用[!UICONTROL 忽略年份]核取方塊。 | 是 | ![正在使用的「During」時間限制範例。](../images/ui/segment-builder/time-constraints/during.png){width="100" zoomable="yes"} |
| 以內(+/-) | 要比較的屬性或事件必須&#x200B;**發生在選取日期後的數天、數週、數月或數年內。**&#x200B;此時間週期為兩個日期的&#x200B;**包含**。 選取的日期可以是今天、昨天或您選擇的其他自訂日期。 | 是 | ![正在使用的「Within」時間限制範例。](../images/ui/segment-builder/time-constraints/within.png){width="100" zoomable="yes"} |
| 早於 | 要比較的屬性或事件&#x200B;**必須**&#x200B;發生在選取的日期之前。 選取的日期可以是您選擇的自訂日期，或是天、周、月或年之間的選擇。 | 是 | ![正在使用的「之前」時間限制範例。](../images/ui/segment-builder/time-constraints/before.png){width="100" zoomable="yes"} |
| 晚於 | 比較的屬性或事件&#x200B;**必須**&#x200B;發生在選取的日期之後。 選取的日期可以是您選擇的自訂日期，或是天、周、月或年之間的選擇。 | 是 | ![正在使用的「After」時間限制範例。](../images/ui/segment-builder/time-constraints/after.png){width="100" zoomable="yes"} |
| 滾動範圍 | 要比較的屬性或事件必須發生在兩個相對日期之間。 日期能以秒、分鐘、小時、天、周、月或年表示。 | 無 | ![正在使用的「滾動範圍」時間限制範例。](../images/ui/segment-builder/time-constraints/rolling-range.png){width="100" zoomable="yes"} |
| 下一 | 要比較的屬性或事件必須在下一個選取的時段內發生。 所選的時段包括分鐘、小時、天、周、月和年。 | 無 | ![正在使用的「In next」時間限制範例。](../images/ui/segment-builder/time-constraints/in-next.png){width="100" zoomable="yes"} |
| 存在 | 屬性已存在。 | 無 | ![正在使用的「存在」時間限制範例。](../images/ui/segment-builder/time-constraints/exists.png){width="100" zoomable="yes"} |
| 不存在 | 屬性不存在。 | 無 | ![正在使用的「不存在」時間限制範例。](../images/ui/segment-builder/time-constraints/does-not-exist.png){width="100" zoomable="yes"} |

+++

當您在事件上套用時間限制時，可以在畫布層級、卡片層級或事件之間套用。

#### 畫布層級限制

若要套用畫布層級時間限制，請選取出現在事件時間表上方的時鐘圖示。

![畫布層級時間限制選取器已反白顯示。](../images/ui/segment-builder/time-constraints/canvas-level.png)

當您在畫布層級套用時間限制時，這會將時間限制套用至對象中的&#x200B;**所有**&#x200B;個事件。

#### 卡片層級限制

若要套用卡片層級限制，請選取要套用時間限制的卡片，接著選取省略符號圖示，然後&#x200B;**[!UICONTROL 套用時間規則]**。 這可讓您在&#x200B;**[!UICONTROL 事件規則]**&#x200B;容器中選取時間限制。

![卡片層級時間限制選擇器已反白顯示。](../images/ui/segment-builder/time-constraints/card-level.png)

當您在卡片層級套用時間限制時，這會針對對象中的&#x200B;**指定**&#x200B;事件套用時間限制。

#### 介於事件條件約束

若要在事件之間套用時間限制，請選取要套用時間限制的兩個事件之間的時鐘圖示。

![事件之間的時間限制選取器會反白顯示。](../images/ui/segment-builder/time-constraints/between-event.png)

當您在事件之間套用時間限制時，這會將時間限制套用至事件之間&#x200B;**的時間**。

此作業的可用時間限制清單與主要時間限制清單不同，如下所示：

+++ 可用的時間限制

| 時間限制 | 說明 |
| --------------- | ----------- |
| 晚於 | 後一個事件&#x200B;**必須至少**&#x200B;發生在前一個事件之後。 |
| 範圍 | 兩個事件&#x200B;**必須**&#x200B;發生在時間限制內所列的時段內。 |

>[!NOTE]
>
>使用「之後」時間限制時，後一個事件發生的次數可能會超過時間限制內所列的時間量。 >
>>例如，如果您有「頁面檢視」事件和「結帳」事件，且在這兩個事件之間放置「1小時後」時間限制，則在「頁面檢視」事件發生2小時後，含有「結帳」事件的區段定義即符合條件。
>
>此外，這兩個時間限制可以相互協調使用。
>
>例如，如果您有「頁面檢視」事件和「結帳」事件，並放入「1小時後」和「24小時內」時間限制，則在「頁面檢視」事件後12小時含有「結帳」事件的區段定義即符合條件，但在「頁面檢視」事件後36小時含有「結帳」事件的區段定義即不符合條件。

+++

## 容器 {#containers}

區段規則會依照其列出順序進行評估。 容器可讓您透過使用巢狀查詢來控制執行順序。

將至少一個圖磚新增至規則產生器畫布後，您就可以開始新增容器。 若要建立新容器，請選取圖磚右上角的省略符號(...)，然後選取&#x200B;**[!UICONTROL 新增容器]**。

![新增容器按鈕會反白顯示，讓您新增一個容器，做為第一個容器的子系。](../images/ui/segment-builder/add-container.png)

新容器會顯示為第一個容器的子系，但您可以拖曳並移動容器來調整階層。 容器的預設行為是&quot;[!UICONTROL 包含]&quot;所提供的屬性、事件或對象。 您可以選取圖磚左上角的[!UICONTROL 包含]，並選取&#x200B;**[!UICONTROL 排除]**，將規則設定為符合容器條件的「[!UICONTROL 排除]」設定檔。

您也可以擷取子容器，並在內嵌新增至父容器中，方法是選取子容器上的「解除容器包裝」。 選取子容器右上角的省略符號(...)以存取此選項。

![讓您解除包裝或刪除容器的選項會反白顯示。](../images/ui/segment-builder/include-exclude.png)

選取&#x200B;**[!UICONTROL 解除容器包裝]**&#x200B;後，子容器會被移除，條件會內嵌顯示。

>[!NOTE]
>
>展開容器時，請留意邏輯是否持續符合所需的區段定義。

![容器在展開後顯示。](../images/ui/segment-builder/unwrapped-container.png)

## 合併原則

>[!CONTEXTUALHELP]
>id="platform_segmentation_createSegment_segmentBuilder_mergePolicies"
>title="合併原則"
>abstract="合併原則可讓不同的資料集合併，形成您的設定檔。Experience Platform 已提供預設的合併原則，您也可以在輪廓中建立新的預設合併原則。針對此客群選擇和您行銷目的相符的合併原則。"

[!DNL Experience Platform]可讓您將來自多個來源的資料彙集在一起，並加以合併，以便檢視每個個別客戶的完整檢視。 彙總此資料時，合併原則是[!DNL Experience Platform]用來決定資料優先順序的方式以及將合併哪些資料以建立設定檔的規則。

您可以為此對象選取符合行銷目的的合併原則，或使用[!DNL Experience Platform]提供的預設合併原則。 您可以建立組織專屬的多個合併原則，包括建立您自己的預設合併原則。 如需建立組織合併原則的逐步指示，請先閱讀[合併原則概觀](../../profile/merge-policies/overview.md)。

若要為您的區段定義選取合併原則，請選取&#x200B;**[!UICONTROL 欄位]**&#x200B;索引標籤上的齒輪圖示，然後使用&#x200B;**[!UICONTROL 合併原則]**&#x200B;下拉式功能表來選取您要使用的合併原則。

![合併原則選擇器會反白顯示。 這可讓您選擇要為區段定義選取的合併原則。](../images/ui/segment-builder/merge-policy-selector.png)

## 客群屬性 {#audience-properties}

>[!CONTEXTUALHELP]
>id="platform_segments_createsegment_segmentbuilder_segmentproperties"
>title="客群屬性"
>abstract="客群屬性區段會顯示所產生之客群大小的預估值，展示符合條件的輪廓數與輪廓總數的比較。這樣您便能夠在建置該客群之前，視需要進行客群調整。"

>[!CONTEXTUALHELP]
>id="platform_segments_createsegment_segmentbuilder_refreshestimate"
>title="重新整理預估值"
>abstract="重新整理區段定義的預估值，即可立即預覽有多少設定檔符合提議的區段定義的資格。對象預估值會透過使用當天的樣本資料的樣本大小產生。"
>additional-url="https://experienceleague.adobe.com/docs/experience-platform/segmentation/tutorials/create-a-segment.html#estimate-and-preview-an-audience" text="預估和預覽對象"

>[!CONTEXTUALHELP]
>id="platform_segments_createsegment_segmentbuilder_qualifiedprofiles"
>title="合格的設定檔"
>abstract="符合條件的輪廓是指符合客群規則之輪廓的實際數量。執行區段評估工作之後，此數字每 24 小時更新一次。"

>[!CONTEXTUALHELP]
>id="platform_segments_createsegment_segmentbuilder_estimatedprofiles"
>title="預估的設定檔"
>abstract="預估的輪廓是指以範例工作為依據，符合客群規則之輪廓的大致數量。"

建立區段定義時，工作區右側的&#x200B;**[!UICONTROL 對象屬性]**&#x200B;區段會顯示結果區段定義的大小預估值，好讓您在建立對象本身之前根據需要調整區段定義。

**[!UICONTROL 合格的設定檔]**&#x200B;表示符合區段定義規則的&#x200B;**實際**&#x200B;個設定檔數目。 執行區段評估工作之後，此數字每 24 小時更新一次。

合格設定檔的時間戳記表示最近的&#x200B;**批次**&#x200B;區段評估工作，且對於使用串流或邊緣區段評估的區段定義顯示為&#x200B;**not**。 如果您編輯區段定義，則在下次執行區段評估工作之前，合格設定檔的數量將保持不變。

根據&#x200B;**[!UICONTROL 範例工作]**，**預估的設定檔**&#x200B;表示設定檔的大致範圍&#x200B;**為**。 這表示樣本資料是以更大的設定檔集進行預計，因此會產生可能與合格設定檔實際數量不同的預估數量。預估的設定檔範例具有95%信賴區間。

此數字在兩種情況下更新：

1. 客戶資料變更超過3%，或最後一個範例工作超過三天。
2. 對象的規則已修改或移除。

選取資訊泡泡圖會提供上次執行範例工作的日期和時間。

![對象屬性區段中會強調顯示合格的設定檔和預估的設定檔。](../images/ui/segment-builder/audience-estimates.png)

**[!UICONTROL 對象屬性]**&#x200B;區段也可讓您指定對象的重要資訊，包括其名稱、說明和評估型別。 名稱是用來在您的組織所定義的區段定義中識別您的區段定義，因此應是描述性、簡潔及唯一的。

當您繼續建立對象時，可以選取&#x200B;**[!UICONTROL 檢視設定檔]**&#x200B;來檢視對象的編頁預覽。

![對象屬性區段會醒目提示。 對象屬性包含但不限於名稱、說明和評估方法。](../images/ui/segment-builder/segment-properties.png)

>[!NOTE]
>
>使用當天樣本資料的樣本大小會產生對象預估。 如果您的設定檔存放區中有少於100萬個實體，則會使用完整的資料集；對於100萬到2,000萬個之間的實體，會使用100萬個實體；而對於2,000萬個以上的實體，則會使用全部實體的5%。
>
>此外，此估計值是根據上次執行設定檔範例工作的時間。 這表示如果您使用相對日期函式，例如&quot;Today&quot;或&quot;This week&quot;，估計將會根據最後一個設定檔範例工作執行時間進行計算。 例如，如果今天是1月24日，而最後一個設定檔範例工作是在1月22日執行，則「昨天」相對日期函式將以1月21日為基礎，而不是1月23日。
>
>如需有關產生區段定義之預估的詳細資訊，請參閱區段定義建立教學課程的[預估產生區段](../tutorials/create-a-segment.md#estimate-and-preview-an-audience)。

您也可以選取評估方法。 如果您知道要使用的評估方法，可以使用下拉式清單選取所需的評估方法。 如果您想要瞭解此區段定義符合哪些評估型別，可以選取帶有放大鏡的瀏覽圖示![資料夾圖示](/help/images/icons/folder-search.png)，以檢視可用區段定義評估方法的清單。

[!UICONTROL 評估方法資格]彈出視窗即會顯示。 此彈出視窗會顯示可用的評估方法，包括批次、串流和邊緣。 彈出視窗會顯示哪些評估方法符合資格和不符合資格。 根據您在區段定義中使用的引數，它可能不符合某些評估方法的資格。 如需每個評估方法需求的詳細資訊，請閱讀[串流區段](../methods/streaming-segmentation.md#query-types)或[邊緣區段](../methods/edge-segmentation.md#query-types)概述。

完成建立區段定義後，您也可以變更區段定義的評估方法。 如果您將評估方法從Edge或串流變更為「批次」，您將&#x200B;**無法**&#x200B;將其變更回Edge或串流。 在彈出視窗中選取&#x200B;**儲存**&#x200B;後，對評估方法的變更將&#x200B;**[!UICONTROL 僅]**&#x200B;生效。 取消對話方塊將&#x200B;**保留**&#x200B;原始的評估方法。

![評估方法適用性快顯視窗會出現。 這會顯示哪些評估方法符合區段定義，且不符合區段定義。](../images/ui/segment-builder/select-evaluation-method.png)

如果選取無效的評估方法，系統會提示您變更區段定義規則或變更評估方法。

![評估方法快顯視窗。 如果選取了不符合資格的評估方法，快顯視窗會說明它不符合資格的原因。](../images/ui/segment-builder/ineligible-evaluation-method.png)

如需不同區段定義評估方法的詳細資訊，請參閱[區段概述](../home.md#evaluate-segments)。

## 後續步驟 {#next-steps}

區段產生器提供豐富的工作流程，可讓您從[!DNL Real-Time Customer Profile]資料中隔離可行銷對象。 閱讀本指南後，您現在應該能夠：

- 使用屬性、事件和現有對象的組合作為建置區塊來建立區段定義。
- 使用規則產生器畫布和容器可控制區段規則的執行順序。
- 檢視潛在對象的預估值，讓您視需要調整區段定義。
- 啟用已排程區段的所有區段定義。
- 啟用串流區段的指定區段定義。

若要深入瞭解[!DNL Segmentation Service]，請繼續閱讀檔案，並觀看相關影片以補充您的學習。 若要進一步瞭解[!DNL Segmentation Service] UI的其他部分，請閱讀[[!DNL Segmentation Service] 使用手冊](./overview.md)。
