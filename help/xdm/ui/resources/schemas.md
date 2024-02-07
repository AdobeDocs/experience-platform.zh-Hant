---
keywords: Experience Platform；首頁；熱門主題；API；API；XDM；XDM系統；體驗資料模型；資料模型；ui；工作區；綱要；綱要；
solution: Experience Platform
title: 在UI中建立和編輯方案
description: 瞭解在Experience Platform使用者介面中建立和編輯方案的基本知識。
exl-id: be83ce96-65b5-4a4a-8834-16f7ef9ec7d1
source-git-commit: 5e57df3fbc22baa1c7abbb02a003ad8663aad040
workflow-type: tm+mt
source-wordcount: '3671'
ht-degree: 2%

---

# 在 UI 中建立和編輯綱要

本指南概述如何在Adobe Experience Platform UI中建立、編輯及管理貴組織的Experience Data Model (XDM)方案。

>[!IMPORTANT]
>
>XDM結構描述是極為可自訂的，因此建立結構描述的相關步驟可能會因您想要結構描述擷取的資料型別而異。 因此，本檔案僅涵蓋您可以在UI中與結構描述進行的基本互動，並排除自訂類別、結構描述欄位群組、資料型別和欄位等相關步驟。
>
>如需架構建立流程的完整導覽，請跟隨以下導覽： [結構描述建立教學課程](../../tutorials/create-schema-ui.md) 以建立完整的範例結構描述，並熟悉 [!DNL Schema Editor].

## 先決條件

本指南需要實際瞭解XDM系統。 請參閱 [XDM概覽](../../home.md) 介紹XDM在Experience Platform生態系統內的角色，以及 [結構描述組合的基本面](../../schema/composition.md) 以取得結構描述建構方式的概觀。

## 建立新結構描述 {#create}

>[!NOTE]
>
>本節說明如何在UI中手動建立新結構描述。 如果您正在將CSV資料內嵌至平台，您可以選擇使用 [將該資料對應到AI產生的建議所建立的XDM結構描述](../../../ingestion/tutorials/map-csv/recommendations.md) （目前為測試版）而不需自行手動建立結構描述。

在 [!UICONTROL 方案] 工作區，選取 **[!UICONTROL 建立結構描述]** 在右上角。

![使用的結構描述工作區 [!UICONTROL 建立結構描述] 反白顯示。](../../images/ui/resources/schemas/create-schema.png)

此 [!UICONTROL 建立結構描述] 工作流程隨即顯示。 您可以選取下列其中一項，為結構描述選擇基底類別 **[!UICONTROL 個別設定檔]**， **[!UICONTROL 體驗事件]**，或 **[!UICONTROL 其他]**，後接 **[!UICONTROL 下一個]** 以確認您的選擇。 請參閱 [XDM個別設定檔](../../classes/individual-profile.md) 和 [XDM ExperienceEvent](../../classes/experienceevent.md) 檔案，以取得這些類別的詳細資訊。

![此 [!UICONTROL 建立結構描述] 包含三個類別選項和的工作流程 [!UICONTROL 下一個] 反白顯示。](../../images/ui/resources/schemas/schema-class-options.png)

選取類別後， [!UICONTROL 名稱和評論] 區段隨即顯示。 您可以在此段落中提供名稱和說明，以識別您的結構描述。&#x200B;URL結構描述的基本結構（由類別提供）會顯示在畫布中，供您檢閱及驗證選取的類別和結構描述結構。

輸入人性化的 [!UICONTROL 結構描述顯示名稱] 在文字欄位中。 接下來，輸入適當的說明來協助識別您的結構描述。 當您檢閱了結構描述結構並對設定感到滿意時，請選取「 」 **[!UICONTROL 完成]** 以建立架構。

![此 [!UICONTROL 名稱和評論] 的區段 [!UICONTROL 建立結構描述] 使用的工作流程 [!UICONTROL 結構描述顯示名稱]， [!UICONTROL 說明]、和 [!UICONTROL 完成] 反白顯示。](../../images/ui/resources/schemas/name-and-review.png)

此 [!UICONTROL 結構描述] [!UICONTROL 瀏覽] 標籤隨即顯示。 您最近建立的結構描述現在會列在「結構描述資料庫」中，並可在 [!DNL Schema Editor].

![結構描述工作區瀏覽標籤會顯示您最近建立的結構描述。](../../images/ui/resources/schemas/example-schema.png)

## 編輯現有結構描述 {#edit}

>[!NOTE]
>
>一旦結構描述已儲存並用於資料擷取中，就只能對其執行加總變更。 請參閱 [結構描述演化的規則](../../schema/composition.md#evolution) 以取得詳細資訊。

若要編輯現有綱要，請選取 **[!UICONTROL 瀏覽]** 標籤，然後選取您要編輯的綱要名稱。 您也可以使用搜尋列來縮小可用選項清單的範圍。

![結構描述的工作區反白顯示一個結構描述。](../../images/ui/resources/schemas/edit-schema.png)

>[!TIP]
>
>您可以使用工作區的搜尋和篩選功能來協助您更輕鬆地尋找結構。 請參閱以下指南： [探索XDM資源](../explore.md) 以取得詳細資訊。

選取結構描述後， [!DNL Schema Editor] 會在畫布中顯示結構描述的結構。 您現在可以 [新增欄位群組](#add-field-groups) 至結構描述(或 [新增個別欄位](#add-individual-fields) 來自這些群組)， [編輯欄位顯示名稱](#display-names)，或 [編輯現有的自訂欄位群組](./field-groups.md#edit) 如果結構描述採用任何。

## 更多動作 {#more}

在結構編輯器中，您還可以執行快速動作以複製結構描述的JSON結構，或刪除結構（如果尚未為即時客戶個人檔案啟用或具有關聯的資料集）。 選取 [!UICONTROL 更多] 在檢視頂端，顯示包含快速動作的下拉式清單。

複製JSON結構功能可讓您檢視當您仍在建置結構描述和資料管道時，範例裝載的外觀。 在架構中有複雜的物件對應結構（例如身分對應）的情況下，此功能特別實用。

![結構描述編輯器，其反白顯示更多按鈕，並顯示下拉式選項。](../../images/tutorials/create-schema/more-actions.png)

## 顯示名稱切換 {#display-name-toggle}

為方便起見，架構編輯器提供切換功能，以在原始欄位名稱與較容易讀取的顯示名稱之間變更。 此彈性可改善欄位發現能力及結構描述的編輯。 此切換位於架構編輯器檢視的右上角。

>[!NOTE]
>
>從欄位名稱到顯示名稱的變更純粹是裝飾性的，不會變更任何下游資源。

![架構編輯器，具有 [!UICONTROL 顯示欄位顯示名稱] 反白顯示。](../../images/ui/resources/schemas/display-name-toggle.png)

標準欄位群組的顯示名稱由系統產生，但可自訂，如中所述 [顯示名稱](#display-names) 區段。 顯示名稱會反映在多個UI檢視中，包括對應和資料集預覽。 預設設定為關閉，且會依欄位名稱的原始值顯示欄位名稱。

## 將欄位群組新增到結構描述 {#add-field-groups}

>[!NOTE]
>
>本節說明如何將現有欄位群組新增至結構描述。 如果您想要建立新的自訂欄位群組，請參閱以下指南： [建立和編輯欄位群組](./field-groups.md#create) 而非。

當您在中開啟結構描述後 [!DNL Schema Editor]中，您可以使用欄位群組來新增欄位至結構描述。 若要開始，請選取 **[!UICONTROL 新增]** 旁邊 **[!UICONTROL 欄位群組]** 在左側邊欄中。

![結構描述編輯器 [!UICONTROL 新增] 從 [!UICONTROL 欄位群組] 區段反白顯示。](../../images/ui/resources/schemas/add-field-group-button.png)

此時會出現一個對話方塊，顯示您可以為結構描述選取的欄位群組清單。 由於欄位群組僅與一個類別相容，因此只會列出與結構描述所選類別相關聯的欄位群組。 依預設，列出的欄位群組會根據其在您組織內的使用人氣排序。

![此 [!UICONTROL 新增欄位群組] 以反白顯示的對話方塊 [!UICONTROL 人氣] 欄反白顯示。](../../images/ui/resources/schemas/field-group-popularity.png)

如果您知道要新增欄位的一般活動或業務區域，請在左側邊欄中選取一或多個垂直產業類別，以篩選顯示的欄位群組清單。

![此 [!UICONTROL 新增欄位群組] 以反白顯示的對話方塊 [!UICONTROL 產業] 篩選器和 [!UICONTROL 產業] 欄反白顯示。](../../images/ui/resources/schemas/industry-filter.png)

>[!NOTE]
>
>如需有關XDM中特定產業資料模型化最佳實務的詳細資訊，請參閱以下檔案： [產業資料模型](../../schema/industries/overview.md).

您也可以使用搜尋列來協助找出您想要的欄位群組。 名稱與查詢相符的欄位群組會出現在清單頂端。 在 **[!UICONTROL 標準欄位]**，包含描述所需資料屬性之欄位的欄位群組隨即顯示。

![此 [!UICONTROL 新增欄位群組] 對話方塊 [!UICONTROL 標準欄位] 搜尋功能會醒目提示。](../../images/ui/resources/schemas/field-group-search.png)

選取您要新增至結構描述的欄位群組名稱旁的核取方塊。 您可以從清單中選取多個欄位群組，每個選取的欄位群組都會顯示在右側邊欄中。

![此 [!UICONTROL 新增欄位群組] 對話方塊中反白核取方塊選取功能。](../../images/ui/resources/schemas/add-field-group.png)

>[!TIP]
>
>對於任何列出的欄位群組，您可以暫留或焦點在資訊圖示(![](../../images/ui/resources/schemas/info-icon.png))，以檢視欄位群組所擷取的資料型別的簡短說明。 您也可以選取預覽圖示(![](../../images/ui/resources/schemas/preview-icon.png))，以檢視欄位群組提供的欄位結構，然後再決定將其新增至結構描述。

選擇欄位群組後，選擇 **[!UICONTROL 新增欄位群組]** 以將它們新增至結構描述。

![此 [!UICONTROL 新增欄位群組] 對話方塊，其中已選取欄位群組且 [!UICONTROL 新增欄位群組] 反白顯示。](../../images/ui/resources/schemas/add-field-group-finish.png)

此 [!DNL Schema Editor] 會以畫布中顯示的欄位群組提供的欄位重新出現。

![此 [!DNL Schema Editor] 並顯示範例結構描述。](../../images/ui/resources/schemas/field-groups-added.png)

將欄位群組新增到結構描述後，您可以選擇使用 [移除現有欄位](#remove-fields) 或 [新增自訂欄位](#add-fields) 這些群組，視您的需求而定。

### 移除從欄位群組新增的欄位 {#remove-fields}

將欄位群組新增到結構描述後，您可以移除任何不需要的欄位。

>[!NOTE]
>
>從欄位群組中移除欄位只會影響正在處理的結構描述，不會影響欄位群組本身。 如果您移除一個結構描述中的欄位，這些欄位仍然可在採用相同欄位群組的所有其他結構描述中使用。

在以下範例中，標準欄位群組 **[!UICONTROL 人口統計細節]** 已新增至結構描述。 若要移除單一欄位，例如 `taxId`，選取畫布中的欄位，然後選取「 」 **[!UICONTROL 移除]** 在右側邊欄中。

![此 [!DNL Schema Editor] 替換為 [!UICONTROL 移除] 反白顯示。 此動作會移除單一欄位。](../../images/ui/resources/schemas/remove-single-field.png)

如果您想要移除多個欄位，可以整體管理欄位群組。 在畫布中選取屬於群組的欄位，然後選取 **[!UICONTROL 管理相關欄位]** 在右側邊欄中。

![此 [!DNL Schema Editor] 替換為 [!UICONTROL 管理相關欄位] 反白顯示。](../../images/ui/resources/schemas/manage-related-fields.png)

會出現一個對話方塊，顯示相關欄位群組的結構。 在此，您可以使用提供的核取方塊來選取或取消選取所需的欄位。 滿意後，選取 **[!UICONTROL 確認]**.

![此 [!UICONTROL 管理相關欄位] 包含所選欄位和的對話方塊 [!UICONTROL 確認] 反白顯示。](../../images/ui/resources/schemas/select-fields.png)

畫布會重新出現，架構結構中只會顯示選取的欄位。

![欄位已新增](../../images/ui/resources/schemas/fields-added.png)

### 新增自訂欄位至欄位群組 {#add-fields}

將欄位群組新增到結構描述後，您可以為該群組定義其他欄位。 但是，在一個結構描述中新增到欄位群組的任何欄位也會出現在採用相同欄位群組的所有其他結構描述中。

此外，如果將自訂欄位新增到標準欄位群組，則該欄位群組將轉換為自訂欄位群組，並且原始標準欄位群組將不再可用。

如果要將自訂欄位新增到標準欄位群組，請參閱 [區段如下](#custom-fields-for-standard-groups) 以取得特定指示。 如果您新增欄位至自訂欄位群組，請參閱以下章節： [編輯自訂欄位群組](./field-groups.md) 在欄位群組UI指南中。

如果您不想變更任何現有的欄位群組，您可以 [建立新的自訂欄位群組](./field-groups.md#create) 以定義其他欄位。

## 將個別欄位新增到結構描述 {#add-individual-fields}

如果您想避免針對特定使用案例新增整個欄位群組，結構描述編輯器可讓您將個別欄位直接新增到結構描述。 您可以 [從標準欄位群組新增個別欄位](#add-standard-fields) 或 [新增您自己的自訂欄位](#add-custom-fields) 而非。

>[!IMPORTANT]
>
>即使結構描述編輯器在功能上允許您直接將個別欄位新增到結構描述，這不會變更XDM結構描述中的所有欄位必須由其類別或與該類相容的欄位群組提供。 如以下各節所說明，當所有個別欄位新增到結構描述中時，作為關鍵步驟，它們仍會與類別或欄位群組相關聯。

### 新增標準欄位 {#add-standard-fields}

您可以將標準欄位群組中的欄位直接新增到結構描述，而無需預先知道其對應的欄位群組。 若要將標準欄位新增到結構描述，請選取加號(**+**)圖示加以識別（位於畫布中的結構描述名稱旁）。 一個 **[!UICONTROL 未命名的欄位]** 結構描述結構中會顯示預留位置，而右側邊欄會更新，顯示設定欄位的控制項。

![欄位預留位置](../../images/ui/resources/schemas/root-custom-field.png)

在 **[!UICONTROL 欄位名稱]**，開始輸入您要新增的欄位名稱。 系統會自動搜尋符合查詢的標準欄位，並將其列在下 **[!UICONTROL 建議的標準欄位]**，包括他們所屬的欄位群組。

![建議的標準欄位](../../images/ui/resources/schemas/standard-field-search.png)

雖然有些標準欄位會共用相同的名稱，但其結構可能會依其來源欄位群組而有所不同。 如果標準欄位巢狀內嵌在欄位群組結構的父物件中，則新增子欄位時，父欄位也會包含在結構描述中。

選取預覽圖示(![預覽圖示](../../images/ui/resources/schemas/preview-icon.png))，檢視其欄位群組的結構，並更能瞭解其巢狀結構。 若要將標準欄位新增到結構描述，請選取加號圖示(![加號圖示](../../images/ui/resources/schemas/add-icon.png))。

![新增標準欄位](../../images/ui/resources/schemas/add-standard-field.png)

畫布更新以顯示新增到結構描述的標準欄位，包括它巢狀內嵌在欄位群組結構下的任何父欄位。 欄位群組的名稱也會列在 **[!UICONTROL 欄位群組]** 在左側邊欄中。 如果您想從相同的欄位群組新增更多欄位，請選取 **[!UICONTROL 管理相關欄位]** 在右側邊欄中。

![標準欄位已新增](../../images/ui/resources/schemas/standard-field-added.png)

### 新增自訂欄位 {#add-custom-fields}

與標準欄位的工作流程類似，您也可以將自己的自訂欄位直接新增到結構描述。

若要將欄位新增至結構的根層級，請選取加號(**+**)圖示加以識別（位於畫布中的結構描述名稱旁）。 一個 **[!UICONTROL 未命名的欄位]** 結構描述結構中會顯示預留位置，而右側邊欄會更新，顯示設定欄位的控制項。

![根自訂欄位](../../images/ui/resources/schemas/root-custom-field.png)

開始輸入您要新增的欄位名稱，系統就會自動開始搜尋相符的標準欄位。 若要建立新的自訂欄位，請選取最上方的附加選項 **([!UICONTROL 新欄位])**.

![新欄位](../../images/ui/resources/schemas/custom-field-search.png)

為欄位提供顯示名稱和資料型別後，下一步是將欄位指派給父XDM資源。 如果您的結構描述使用自訂類別，您可以選擇 [將欄位新增到指派的類別](#add-to-class) 或 [欄位群組](#add-to-field-group) 而非。 但是，如果您的結構描述使用標準類別，則只能將自訂欄位指派給欄位群組。

#### 將欄位指派給自訂欄位群組 {#add-to-field-group}

>[!NOTE]
>
>本節僅涵蓋如何將欄位指派給自訂欄位群組。 如果您想改用新自訂欄位來擴充標準欄位群組，請參閱 [新增自訂欄位至標準欄位群組](#custom-fields-for-standard-groups).

在 **[!UICONTROL 指派給]**，選取 **[!UICONTROL 欄位群組]**. 如果您的結構描述使用標準類別，這是唯一可用的選項，並且預設會選取此選項。

接下來，您必須選取要與新欄位產生關聯的欄位群組。 在提供的文字輸入中開始鍵入欄位群組的名稱。 如果您有任何符合輸入的現有自訂欄位群組，它們將會顯示在下拉式清單中。 或者，您可以鍵入唯一名稱來建立新的欄位群組。

![選取欄位群組](../../images/ui/resources/schemas/select-field-group.png)

>[!WARNING]
>
>如果您選取現有的自訂欄位群組，則採用該欄位群組的任何其他結構描述在您儲存變更後，也將繼承新新增的欄位。 因此，如果您想要此型別的傳輸，請僅選取現有的欄位群組。 否則，您應該選擇建立新的自訂欄位群組。

從清單中選取欄位群組後，選取 **[!UICONTROL 套用]**.

![套用欄位](../../images/ui/resources/schemas/apply-field.png)

新欄位會新增到畫布中，並在 [租使用者ID](../../api/getting-started.md#know-your-tenant_id) 以避免與標準XDM欄位衝突。 與新欄位相關聯的欄位群組也會顯示在下方 **[!UICONTROL 欄位群組]** 在左側邊欄中。

![租使用者ID](../../images/ui/resources/schemas/tenantId.png)

>[!NOTE]
>
>依預設，所選自訂欄位群組提供的其餘欄位會從結構描述中移除。 如果要將其中一些欄位新增到結構描述中，請選取屬於群組的欄位，然後選取 **[!UICONTROL 管理相關欄位]** 在右側邊欄中。

#### 將欄位指派給自訂類別 {#add-to-class}

在 **[!UICONTROL 指派給]**，選取 **[!UICONTROL 類別]**. 下列輸入欄位會以目前結構描述的自訂類別名稱取代，表示新欄位將會指派給此類別。

![此 [!UICONTROL 類別] 為新欄位指派選取的選項。](../../images/ui/resources/schemas/assign-field-to-class.png)

繼續視需要設定欄位並選取 **[!UICONTROL 套用]** 完成後。

![[!UICONTROL 套用] 已為新欄位選取。](../../images/ui/resources/schemas/assign-field-to-class-apply.png)

新欄位會新增到畫布中，並在 [租使用者ID](../../api/getting-started.md#know-your-tenant_id) 以避免與標準XDM欄位衝突。 在左側邊欄中選取類別名稱，會顯示新欄位作為類別結構的一部分。

![套用至自訂類別結構（以畫布表示）的新欄位。](../../images/ui/resources/schemas/assign-field-to-class-applied.png)

### 將自訂欄位新增至標準欄位群組的結構 {#custom-fields-for-standard-groups}

如果您使用的結構描述具有由標準欄位群組提供的物件型別欄位，您可以將自己的自訂欄位新增到該標準物件。

>[!WARNING]
>
>在一個結構描述中新增到欄位群組的任何欄位也會出現在採用相同欄位群組的所有其他結構描述中。 此外，如果將自訂欄位新增到標準欄位群組，則該欄位群組將轉換為自訂欄位群組，並且原始標準欄位群組將不再可用。
>
>如果您參與此功能的測試版，您將會收到一個對話方塊，通知您之前已自訂的標準欄位群組。 一旦您選取 **[!UICONTROL 認可]**，則列出的資源會轉換為自訂欄位群組。
>
>![轉換標準欄位群組的確認對話方塊](../../images/ui/resources/schemas/beta-extension-confirmation.png)

若要開始，請選取加號(**+**)圖示，位於標準欄位群組提供的物件根目錄旁。

![新增欄位至標準物件](../../images/ui/resources/schemas/add-field-to-standard-object.png)

系統會顯示警告訊息，提示您確認是否要轉換標準欄位群組。 選取 **[!UICONTROL 繼續建立欄位群組]** 以繼續進行。

![確認欄位群組轉換](../../images/ui/resources/schemas/confirm-field-group-conversion.png)

畫布會重新出現，新欄位會有一個未命名的預留位置。 請注意，標準欄位群組的名稱已附加&quot;([!UICONTROL 延伸])」以表示它已從原始版本修改。 從這裡，使用右側邊欄中的控制項來定義欄位的屬性。

![新增至標準物件的欄位](../../images/ui/resources/schemas/standard-field-group-converted.png)

套用變更後，新欄位會顯示在標準物件的租使用者ID名稱空間下。 此巢狀名稱空間可防止欄位群組內的欄位名稱衝突，以避免使用相同欄位群組的其他結構描述發生變更。

![新增至標準物件的欄位](../../images/ui/resources/schemas/added-to-standard-object.png)

## 啟用即時客戶設定檔的方案 {#profile}

>[!CONTEXTUALHELP]
>id="platform_schemas_enableforprofile"
>title="啟用設定檔的方案"
>abstract="為設定檔啟用方案時，從此方案建立的任何資料集都會參與即時客戶設定檔，該設定檔會合併來自不同來源的資料以建構每個客戶的完整視圖。一旦將方案用於擷取資料至設定檔中，即無法停用。如需詳細資訊，請查看文件。"

[即時客戶個人檔案](../../../profile/home.md) 合併來自不同來源的資料，以建構每個個別客戶的完整檢視。 如果您希望結構描述擷取的資料參與此程式，您必須啟用結構描述以供使用 [!DNL Profile].

>[!IMPORTANT]
>
>為了啟用結構描述 [!DNL Profile]，必須定義主要身分欄位。 請參閱以下指南： [定義身分欄位](../fields/identity.md) 以取得詳細資訊。

若要啟用結構描述，請從左側邊欄中選取結構描述名稱開始，然後選取 **[!UICONTROL 個人資料]** 在右側邊欄中切換。

![](../../images/ui/resources/schemas/profile-toggle.png)

此時畫面會顯示彈出視窗，警告您一旦啟用並儲存結構描述，就無法停用它。 選取 **[!UICONTROL 啟用]** 以繼續。

![](../../images/ui/resources/schemas/profile-confirm.png)

畫布會重新出現，其中包含 [!UICONTROL 個人資料] 切換已啟用。

>[!IMPORTANT]
>
>由於結構描述尚未儲存，如果您改變主意，要讓結構描述參與即時客戶設定檔，就沒有回訪點：儲存啟用的結構描述後，就無法再停用它。 選取 **[!UICONTROL 個人資料]** 再次切換以停用結構。

若要完成程式，請選取 **[!UICONTROL 儲存]** 以儲存結構。

![](../../images/ui/resources/schemas/profile-enabled.png)

結構描述現在已啟用以用於即時客戶個人檔案。 當Platform根據此結構描述將資料內嵌到資料集時，該資料將合併到您的整合設定檔資料中。

## 編輯結構欄位的顯示名稱 {#display-names}

指派類別並將欄位群組新增至結構描述後，您可以編輯任何結構描述欄位的顯示名稱，無論這些欄位是由標準或自訂XDM資源提供。

>[!NOTE]
>
>請記住，屬於標準類別或欄位群組的欄位顯示名稱只能在特定結構描述的內容中編輯。 換言之，變更一個結構描述中標準欄位的顯示名稱不會影響其他採用相同關聯類別或欄位群組的結構描述。
>
>一旦您變更了結構描述的欄位顯示名稱，這些變更就會立即反映在基於該結構描述的現有資料集中。

若要編輯綱要欄位的顯示名稱，請選取畫布中的欄位。 在右邊欄中，於下方提供新名稱 **[!UICONTROL 顯示名稱]**.

![](../../images/ui/resources/schemas/display-name.png)

選取 **[!UICONTROL 套用]** 而畫布會更新，顯示該欄位的新顯示名稱。 選取 **[!UICONTROL 儲存]** 將變更套用至結構描述。

![](../../images/ui/resources/schemas/display-name-changed.png)

## 變更結構描述的類別 {#change-class}

您可以在儲存結構描述之前，在初始構成程式期間隨時變更結構描述的類別。

>[!WARNING]
>
>為結構描述重新指派類別時應格外小心。 欄位群組僅與某些類別相容，因此變更類別將會重設畫布以及您新增的任何欄位。

若要重新指派類別，請選取 **[!UICONTROL 指派]** 在畫布的左側。

![](../../images/ui/resources/schemas/assign-class-button.png)

會出現一個對話方塊，顯示所有可用類別的清單，包括貴組織定義的任何類別(擁有者為「[!UICONTROL 客戶]「)以及由Adobe定義的標準類別。

從清單中選取類別，以在對話方塊的右側顯示其說明。 您也可以選取 **[!UICONTROL 預覽類別結構]** 檢視與類別關聯的欄位和中繼資料。 選取 **[!UICONTROL 指派類別]** 以繼續。

![](../../images/ui/resources/schemas/assign-class.png)

隨即開啟新的對話方塊，要求您確認要指派新類別。 選取 **[!UICONTROL 指派]** 以確認。

![](../../images/ui/resources/schemas/assign-confirm.png)

確認類別變更後，畫布將會重設，並且所有構成進度將會遺失。

## 後續步驟

本檔案說明在Platform UI中建立和編輯結構描述的基本知識。 強烈建議您檢閱 [結構描述建立教學課程](../../tutorials/create-schema-ui.md) 適用於在UI中建置完整方案的完整工作流程，包括建立自訂欄位群組，以及獨特使用案例的資料型別。

如需功能的詳細資訊， [!UICONTROL 方案] 工作區，請參閱 [[!UICONTROL 方案] 工作區概觀](../overview.md).

若要瞭解如何在中管理結構描述 [!DNL Schema Registry] API，請參閱 [結構描述端點指南](../../api/schemas.md).
