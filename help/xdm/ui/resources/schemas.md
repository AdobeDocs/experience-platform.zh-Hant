---
keywords: Experience Platform；首頁；熱門主題；api;API;XDM;XDM系統；經驗資料模型；資料模型；ui;workspace;schema;schemas;
solution: Experience Platform
title: 在UI中建立和編輯架構
description: 瞭解如何在Experience Platform用戶介面中建立和編輯架構的基本知識。
exl-id: be83ce96-65b5-4a4a-8834-16f7ef9ec7d1
source-git-commit: bed627b945c5392858bcc2dce18e9bbabe8bcdb6
workflow-type: tm+mt
source-wordcount: '3340'
ht-degree: 1%

---

# 在UI中建立和編輯架構

本指南概述了如何在Adobe Experience PlatformUI中為您的組織建立、編輯和管理體驗資料模型(XDM)架構。

>[!IMPORTANT]
>
>XDM架構是極其可自定義的，因此建立架構時涉及的步驟可能因您希望架構捕獲的資料類型而異。 因此，本文檔僅涵蓋您可以與UI中的架構進行的基本交互，並排除了自定義類、架構欄位組、資料類型和欄位等相關步驟。
>
>有關架構建立過程的完整教程，請與 [架構建立教程](../../tutorials/create-schema-ui.md) 建立完整的示例架構並熟悉 [!DNL Schema Editor]。

## 先決條件

本指南要求對XDM系統有正確的瞭解。 請參閱 [XDM概述](../../home.md) 介紹XDM在Experience Platform生態系統中的作用， [架構組合基礎](../../schema/composition.md) 的子菜單。

## 建立新架構 {#create}

>[!NOTE]
>
>本節介紹如何在UI中手動建立新架構。 如果要將CSV資料插入平台，則可以選擇 [將資料映射到由AI生成的建議案建立的XDM模式](../../../ingestion/tutorials/map-csv/recommendations.md) （當前處於beta版），無需親自手動建立架構。

在 [!UICONTROL 架構] 工作區，選擇 **[!UICONTROL 建立架構]** 在右上角。 在顯示的下拉清單中，您可以選擇 **[!UICONTROL XDM個人配置檔案]** 和 **[!UICONTROL XDM體驗事件]** 作為架構的基類。 或者，可以選擇 **[!UICONTROL 瀏覽]** 從可用類的完整清單中進行選擇，或 [建立新的自定義類](./classes.md#create) 的雙曲餘切值。

![](../../images/ui/resources/schemas/create-schema.png)

選擇類後， [!DNL Schema Editor] 框中顯示，並在畫布中顯示架構的基本結構（由類提供）。 在此處，您可以使用右滑軌添加 **[!UICONTROL 顯示名稱]** 和 **[!UICONTROL 說明]** 的子菜單。

![](../../images/ui/resources/schemas/schema-details.png)

現在，可以開始通過 [添加架構欄位組](#add-field-groups)。

## 編輯現有架構 {#edit}

>[!NOTE]
>
>一旦保存了一個架構並將其用於資料接收，則只能對其進行附加更改。 查看 [模式演化規則](../../schema/composition.md#evolution) 的子菜單。

要編輯現有架構，請選擇 **[!UICONTROL 瀏覽]** 頁籤，然後選擇要編輯的架構的名稱。

![](../../images/ui/resources/schemas/edit-schema.png)

>[!TIP]
>
>可以使用工作區的搜索和篩選功能幫助更輕鬆地查找架構。 請參閱上的指南 [探索XDM資源](../explore.md) 的子菜單。

選擇架構後， [!DNL Schema Editor] 顯示，其中在畫布中顯示架構的結構。 你現在可以 [添加欄位組](#add-field-groups) 到架構(或 [添加單個欄位](#add-individual-fields) 從這些組中， [編輯欄位顯示名稱](#display-names)或 [編輯現有自定義域組](./field-groups.md#edit) 如果架構使用任何。

## 顯示名稱切換 {#display-name-toggle}

為方便起見，「架構編輯器」提供切換功能，以便在原始欄位名稱和更易人讀的顯示名稱之間進行更改。 這種靈活性允許改進欄位可發現性並編輯您的架構。 在「架構編輯器」視圖的右上角找到切換。

>[!NOTE]
>
>從欄位名稱更改為顯示名稱純粹是修飾性的，不會更改任何下游資源。

![具有的架構編輯器 [!UICONTROL 顯示欄位的顯示名稱] 。](../../images/ui/resources/schemas/display-name-toggle.png)

標準欄位組的顯示名稱是系統生成的，但可以自定義，如 [顯示名稱](#display-names) 的子菜單。 顯示名稱反映在多個UI視圖中，包括映射和資料集預覽。 預設設定為off，並按欄位名稱的原始值顯示欄位名稱。

## 將欄位組添加到架構 {#add-field-groups}

>[!NOTE]
>
>本節介紹如何將現有欄位組添加到架構。 如果要建立新的自定義欄位組，請參閱上的指南 [建立和編輯欄位組](./field-groups.md#create) 的雙曲餘切值。

在中開啟架構後 [!DNL Schema Editor]，可以通過使用欄位組將欄位添加到架構。 要開始，請選擇 **[!UICONTROL 添加]** 下 **[!UICONTROL 欄位組]** 左欄。

![具有的架構編輯器 [!UICONTROL 添加] 從 [!UICONTROL 欄位組] 的子菜單。](../../images/ui/resources/schemas/add-field-group-button.png)

此時將顯示一個對話框，其中顯示可為架構選擇的欄位組清單。 由於欄位組只與一個類相容，因此將只列出與架構的選定類關聯的那些欄位組。 預設情況下，列出的欄位組會根據其在您組織中的使用情況進行排序。

![](../../images/ui/resources/schemas/field-group-popularity.png)

如果您知道要添加的欄位的一般活動或業務區域，請在左滑軌中選擇一個或多個行業垂直類別，以過濾顯示的欄位組清單。

![](../../images/ui/resources/schemas/industry-filter.png)

>[!NOTE]
>
>有關XDM中特定於行業的資料建模的最佳做法的詳細資訊，請參閱 [行業資料模型](../../schema/industries/overview.md)。

您還可以使用搜索欄幫助查找所需的欄位組。 名稱與查詢匹配的欄位組顯示在清單頂部。 下 **[!UICONTROL 標準欄位]**，將顯示包含描述所需資料屬性的欄位的欄位組。

![](../../images/ui/resources/schemas/field-group-search.png)

選中要添加到架構的欄位組名稱旁邊的複選框。 您可以從清單中選擇多個欄位組，每個選定的欄位組出現在右滑軌中。

![](../../images/ui/resources/schemas/add-field-group.png)

>[!TIP]
>
>對於任何列出的欄位組，可以懸停或聚焦於資訊表徵圖(![](../../images/ui/resources/schemas/info-icon.png))查看欄位組捕獲的資料類型的簡要說明。 也可以選擇預覽表徵圖(![](../../images/ui/resources/schemas/preview-icon.png))查看欄位組提供的欄位的結構，然後再決定將其添加到架構中。

選擇欄位組後，選擇 **[!UICONTROL 添加欄位組]** 將其添加到架構。

![](../../images/ui/resources/schemas/add-field-group-finish.png)

的 [!DNL Schema Editor] 重新顯示，畫布中顯示了欄位組提供的欄位。

![](../../images/ui/resources/schemas/field-groups-added.png)

將欄位組添加到架構後，您可以選擇 [刪除現有欄位](#remove-fields) 或 [添加新自定義域](#add-fields) 根據你的需要。

### 刪除從欄位組添加的欄位 {#remove-fields}

將欄位組添加到架構後，可以刪除不需要的任何欄位。

>[!NOTE]
>
>從欄位組中刪除欄位只影響正在處理的架構，而不影響欄位組本身。 如果刪除一個方案中的欄位，則這些欄位在使用相同欄位組的所有其他方案中仍然可用。

在以下示例中，標準欄位組 **[!UICONTROL 人口結構詳細資訊]** 已添加到架構。 刪除單個欄位，如 `taxId`，選擇畫布中的欄位，然後選擇 **[!UICONTROL 刪除]** 右欄。

![刪除單個欄位](../../images/ui/resources/schemas/remove-single-field.png)

如果要刪除多個欄位，則可以將欄位組作為一個整體進行管理。 選擇畫布中屬於組的欄位，然後選擇 **[!UICONTROL 管理相關欄位]** 右欄。

![管理相關欄位](../../images/ui/resources/schemas/manage-related-fields.png)

將出現一個對話框，顯示有關欄位組的結構。 在此處，您可以使用提供的複選框來選擇或取消選擇所需欄位。 滿足後，選擇 **[!UICONTROL 確認]**。

![從欄位組中選擇欄位](../../images/ui/resources/schemas/select-fields.png)

畫布將重新顯示，只顯示架構結構中的選定欄位。

![已添加欄位](../../images/ui/resources/schemas/fields-added.png)

### 將自定義欄位添加到欄位組 {#add-fields}

在將欄位組添加到架構後，可以為該組定義其他欄位。 但是，添加到一個架構中的欄位組的任何欄位也會出現在使用該欄位組的所有其他方案中。

此外，如果將自定義欄位添加到標準欄位組，則該欄位組將轉換為自定義欄位組，並且原始標準欄位組將不再可用。

如果要將自定義欄位添加到標準欄位組，請參閱 [下面](#custom-fields-for-standard-groups) 的子菜單。 如果要將欄位添加到自定義欄位組，請參閱上的部分 [編輯自定義域組](./field-groups.md) 中。

如果不想更改任何現有欄位組，則 [建立新的自定義欄位組](./field-groups.md#create) 來修改標籤元素的屬性。

## 將單個欄位添加到架構 {#add-individual-fields}

如果希望避免為特定用例添加整個欄位組，則「架構編輯器」允許將單個欄位直接添加到架構。 你可以 [從標準欄位組添加單個欄位](#add-standard-fields) 或 [添加自己的自定義域](#add-custom-fields) 的雙曲餘切值。

>[!IMPORTANT]
>
>即使模式編輯器在功能上允許您將單個欄位直接添加到模式，但這不會改變以下事實： XDM模式中的所有欄位都必須由其類或與該類相容的欄位組提供。 正如下面各節所說明的，在將各個欄位添加到架構時，仍將其作為關鍵步驟與類或欄位組相關聯。

### 添加標準欄位 {#add-standard-fields}

您可以直接將標準欄位組中的欄位添加到架構中，而無需事先知道相應的欄位組。 要向架構添加標準欄位，請選擇加號(**+**)表徵圖。 安 **[!UICONTROL 無標題欄位]** 佔位符顯示在架構結構中，右滑軌更新顯示用於配置欄位的控制項。

![欄位佔位符](../../images/ui/resources/schemas/root-custom-field.png)

下 **[!UICONTROL 欄位名]**，開始鍵入要添加的欄位的名稱。 系統會自動搜索與查詢匹配的標準欄位，並將它們列在 **[!UICONTROL 建議的標準欄位]**，包括它們所屬的欄位組。

![建議的標準欄位](../../images/ui/resources/schemas/standard-field-search.png)

雖然某些標準欄位具有相同的名稱，但其結構可能會因其來源的欄位組而異。 如果標準欄位嵌套在欄位組結構中的父對象中，則如果添加子欄位，則父欄位也將包括在方案中。

選擇預覽表徵圖(![預覽表徵圖](../../images/ui/resources/schemas/preview-icon.png))旁邊，查看其欄位組的結構，並更好地瞭解該欄位可能嵌套的方式。 要將標準欄位添加到方案，請選擇加號表徵圖(![加號表徵圖](../../images/ui/resources/schemas/add-icon.png))。

![添加標準欄位](../../images/ui/resources/schemas/add-standard-field.png)

畫布將更新，以顯示添加到架構的標準欄位，包括它嵌套在欄位組結構中的任何父欄位。 欄位組的名稱也列在 **[!UICONTROL 欄位組]** 左欄。 如果要從同一欄位組中添加更多欄位，請選擇 **[!UICONTROL 管理相關欄位]** 右欄。

![已添加標準欄位](../../images/ui/resources/schemas/standard-field-added.png)

### 新增自訂欄位 {#add-custom-fields}

與標準欄位的工作流類似，您也可以將您自己的自定義欄位直接添加到架構中。

要將欄位添加到架構的根級別，請選擇加號(**+**)表徵圖。 安 **[!UICONTROL 無標題欄位]** 佔位符顯示在架構結構中，右滑軌更新顯示用於配置欄位的控制項。

![根自定義欄位](../../images/ui/resources/schemas/root-custom-field.png)

開始鍵入要添加的欄位的名稱，系統將自動開始搜索匹配的標準欄位。 要改為建立新的自定義欄位，請選擇附加了 **([!UICONTROL 新建欄位])**。

![新建欄位](../../images/ui/resources/schemas/custom-field-search.png)

為欄位提供顯示名稱和資料類型後，下一步是將欄位分配給父XDM資源。 如果您的架構使用自定義類，則可以選擇 [將欄位添加到分配的類](#add-to-class) 或 [欄位組](#add-to-field-group) 的雙曲餘切值。 但是，如果您的架構使用標準類，則只能將自定義欄位分配給欄位組。

#### 將欄位分配給自定義欄位組 {#add-to-field-group}

>[!NOTE]
>
>本節僅介紹如何將欄位分配給自定義欄位組。 如果希望用新自定義欄位擴展標準欄位組，請參閱上的部分 [將自定義欄位添加到標準欄位組](#custom-fields-for-standard-groups)。

下 **[!UICONTROL 分配給]**&#x200B;選中 **[!UICONTROL 欄位組]**。 如果方案使用標準類，則此選項是唯一可用的選項，並且預設情況下處於選中狀態。

接下來，必須為要關聯的新欄位選擇一個欄位組。 開始在提供的文本輸入中鍵入欄位組的名稱。 如果有任何與輸入匹配的現有自定義欄位組，它們將出現在下拉清單中。 或者，可鍵入唯一名稱以改為建立新欄位組。

![選擇欄位組](../../images/ui/resources/schemas/select-field-group.png)

>[!WARNING]
>
>如果選擇現有的自定義欄位組，則使用該欄位組的任何其它方案也將在保存更改後繼承新添加的欄位。 因此，僅當要選擇此類型的傳播時，才選擇現有欄位組。 否則，應選擇建立新的自定義欄位組。

從清單中選擇欄位組後，選擇 **[!UICONTROL 應用]**。

![應用欄位](../../images/ui/resources/schemas/apply-field.png)

新欄位將添加到畫布中，並在您的 [租戶ID](../../api/getting-started.md#know-your-tenant_id) 以避免與標準XDM欄位衝突。 與新欄位關聯的欄位組也顯示在 **[!UICONTROL 欄位組]** 左欄。

![租戶ID](../../images/ui/resources/schemas/tenantId.png)

>[!NOTE]
>
>預設情況下，所選自定義欄位組提供的其餘欄位將從架構中刪除。 如果要將其中的一些欄位添加到方案，請選擇屬於該組的欄位，然後選擇 **[!UICONTROL 管理相關欄位]** 右欄。

#### 將欄位分配給自定義類 {#add-to-class}

下 **[!UICONTROL 分配給]**&#x200B;選中 **[!UICONTROL 類]**。 下面的輸入欄位將替換為當前架構的自定義類的名稱，這表示新欄位將分配給此類。

![的 [!UICONTROL 類] 的子菜單。](../../images/ui/resources/schemas/assign-field-to-class.png)

繼續根據需要配置欄位並選擇 **[!UICONTROL 應用]** 的子菜單。

![[!UICONTROL 應用] 為新欄位選擇。](../../images/ui/resources/schemas/assign-field-to-class-apply.png)

新欄位將添加到畫布中，並在您的 [租戶ID](../../api/getting-started.md#know-your-tenant_id) 以避免與標準XDM欄位衝突。 在左滑軌中選擇類名後，將顯示新欄位作為類結構的一部分。

![應用於自定義類結構的新欄位，在畫布中表示。](../../images/ui/resources/schemas/assign-field-to-class-applied.png)

### 將自定義欄位添加到標準欄位組的結構 {#custom-fields-for-standard-groups}

如果正在處理的方案具有由標準欄位組提供的對象類型欄位，則可以將您自己的自定義欄位添加到該標準對象。

>[!WARNING]
>
>添加到一個架構中的欄位組的任何欄位也將出現在使用該欄位組的所有其他方案中。 此外，如果將自定義欄位添加到標準欄位組，則該欄位組將轉換為自定義欄位組，並且原始標準欄位組將不再可用。
>
>如果您參與了此功能的測試版，您將收到一個對話框，通知您以前已自定義的標準欄位組。 一旦選擇 **[!UICONTROL 確認]**，列出的資源將轉換為自定義欄位組。
>
>![「確認」對話框，用於轉換標準欄位組](../../images/ui/resources/schemas/beta-extension-confirmation.png)

要開始，請選擇加號(**+**)表徵圖。

![將欄位添加到標準對象](../../images/ui/resources/schemas/add-field-to-standard-object.png)

出現警告消息，提示您確認是否要轉換標準欄位組。 選擇 **[!UICONTROL 繼續建立欄位組]** 繼續。

![確認欄位組轉換](../../images/ui/resources/schemas/confirm-field-group-conversion.png)

畫布將重新顯示，並帶有新欄位的未命名佔位符。 請注意，標準欄位組的名稱已附加「([!UICONTROL 擴展])」，表示已從原始版本中修改。 在此處，使用右滑軌中的控制項定義欄位的屬性。

![添加到標準對象的欄位](../../images/ui/resources/schemas/standard-field-group-converted.png)

應用更改後，新欄位將顯示在標準對象中的租戶ID命名空間下。 此嵌套命名空間可防止欄位組本身內的欄位名稱衝突，以避免中斷使用相同欄位組的其他架構中的更改。

![添加到標準對象的欄位](../../images/ui/resources/schemas/added-to-standard-object.png)

## 為即時客戶配置檔案啟用方案 {#profile}

>[!CONTEXTUALHELP]
>id="platform_schemas_enableforprofile"
>title="啟用設定檔的方案"
>abstract="為設定檔啟用方案時，從此方案建立的任何資料集都會參與即時客戶設定檔，該設定檔會合併來自不同來源的資料以建構每個客戶的完整視圖。一旦將方案用於擷取資料至設定檔中，即無法停用。如需詳細資訊，請參閱文件。"

[即時客戶配置檔案](../../../profile/home.md) 合併來自不同源的資料以構建每個客戶的完整視圖。 如果希望方案捕獲的資料參與此進程，則必須啟用該方案以供使用 [!DNL Profile]。

>[!IMPORTANT]
>
>為了為 [!DNL Profile]，它必須定義主標識欄位。 請參閱上的指南 [定義標識欄位](../fields/identity.md) 的子菜單。

要啟用架構，請從選擇左欄中架構的名稱開始，然後選擇 **[!UICONTROL 配置檔案]** 在右滑軌中切換。

![](../../images/ui/resources/schemas/profile-toggle.png)

出現一個跨距，警告您一旦啟用並保存了方案，就無法禁用它。 選擇 **[!UICONTROL 啟用]** 繼續。

![](../../images/ui/resources/schemas/profile-confirm.png)

畫布將用 [!UICONTROL 配置檔案] 啟用切換。

>[!IMPORTANT]
>
>由於尚未保存架構，因此如果您改變主意，讓架構參與即時客戶配置檔案，則此點不會返回：一旦保存了啟用的架構，就不能再禁用它。 選擇 **[!UICONTROL 配置檔案]** 再次切換以禁用架構。

要完成該流程，請選擇 **[!UICONTROL 保存]** 的子菜單。

![](../../images/ui/resources/schemas/profile-enabled.png)

此架構現在已啟用，可在Real-Time Customer Profile中使用。 當平台基於此架構將資料插入資料集時，該資料將合併到合併的Profile資料中。

## 編輯架構欄位的顯示名稱 {#display-names}

一旦為架構分配了類並添加了欄位組，您就可以編輯該架構的任何欄位的顯示名稱，而不管這些欄位是由標準XDM資源還是由自定義XDM資源提供的。

>[!NOTE]
>
>請記住，屬於標準類或欄位組的欄位的顯示名稱只能在特定架構的上下文中編輯。 換句話說，更改一個方案中標準欄位的顯示名稱不會影響使用相同關聯類或欄位組的其他方案。
>
>一旦更改了架構欄位的顯示名稱，這些更改將立即反映在基於該架構的任何現有資料集中。

要編輯架構欄位的顯示名稱，請在畫布中選擇該欄位。 在右欄中，在 **[!UICONTROL 顯示名稱]**。

![](../../images/ui/resources/schemas/display-name.png)

選擇 **[!UICONTROL 應用]** 在右欄中，畫布將更新以顯示欄位的新顯示名稱。 選擇 **[!UICONTROL 保存]** 將更改應用到架構。

![](../../images/ui/resources/schemas/display-name-changed.png)

## 更改架構的類 {#change-class}

在保存架構之前，可以在初始合成過程中的任何時刻更改架構的類。

>[!WARNING]
>
>為架構重新指派類應非常謹慎。 欄位組僅與某些類相容，因此更改該類將重置畫布和添加的任何欄位。

要重新指配類，請選擇 **[!UICONTROL 分配]** 畫布的左側。

![](../../images/ui/resources/schemas/assign-class-button.png)

此時將出現一個對話框，其中顯示所有可用類的清單，包括由您的組織定義的任何類(所有者為「」[!UICONTROL 客戶]&quot;)以及由Adobe定義的標準類。

從清單中選擇一個類，以在對話框的右側顯示其說明。 也可以選擇 **[!UICONTROL 預覽類結構]** 查看與類關聯的欄位和元資料。 選擇 **[!UICONTROL 分配類]** 繼續。

![](../../images/ui/resources/schemas/assign-class.png)

將開啟一個新對話框，要求您確認要分配新類。 選擇 **[!UICONTROL 分配]** 確認。

![](../../images/ui/resources/schemas/assign-confirm.png)

確認類更改後，將重置畫布，並丟失所有合成進度。

## 後續步驟

本文檔介紹了在平台UI中建立和編輯架構的基礎知識。 強烈建議您查看 [架構建立教程](../../tutorials/create-schema-ui.md) 用於在UI中構建完整架構的全面工作流，包括為唯一使用案例建立自定義欄位組和資料類型。

有關功能的詳細資訊 [!UICONTROL 架構] 工作區，請參閱 [[!UICONTROL 架構] 工作區概述](../overview.md)。

瞭解如何管理中的架構 [!DNL Schema Registry] API，請參見 [架構終結點指南](../../api/schemas.md)。
