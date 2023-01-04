---
keywords: Experience Platform；設定檔；即時客戶設定檔；合併原則；UI；使用者介面；時間戳記順序；資料集優先順序
title: 合併策略UI指南
type: Documentation
description: 在Experience Platform中將多個來源的資料匯整在一起時，Platform會使用合併原則來判斷資料的優先順序，以及將哪些資料合併以建立統一檢視。 本指南提供使用Adobe Experience Platform使用者介面處理合併原則的逐步指示。
exl-id: 0489217a-6a53-428c-a531-fd0a0e5bb71f
source-git-commit: 34e0381d40f884cd92157d08385d889b1739845f
workflow-type: tm+mt
source-wordcount: '2321'
ht-degree: 0%

---


# 合併策略UI指南

Adobe Experience Platform可讓您從多個來源將資料片段匯整在一起，並加以結合，以便查看每個客戶的完整檢視。 將這些資料放在一起時，合併策略是 [!DNL Platform] 用來決定資料的優先順序，以及將結合哪些資料以建立統一檢視。

使用RESTful API或用戶介面，您可以建立新的合併策略、管理現有策略，以及為組織設定預設的合併策略。 本指南提供使用Adobe Experience Platform使用者介面(UI)處理合併原則的逐步指示。

若要進一步了解合併原則及其在Experience Platform中所扮演的角色，請先閱讀 [合併策略概述](overview.md).

## 快速入門

本指南需要對幾項重要事項有充分的了解 [!DNL Experience Platform] 功能。 在遵循本指南之前，請先檢閱以下服務的檔案：

* [即時客戶個人檔案](../home.md):根據來自多個來源的匯總資料，提供統一的即時消費者設定檔。
* [Adobe Experience Platform Identity Service](../../identity-service/home.md):借由橋接從擷取到的不同資料來源的身分識別，來啟用即時客戶設定檔 [!DNL Platform].
* [Experience Data Model(XDM)](../../xdm/home.md):標準化框架 [!DNL Platform] 組織客戶體驗資料。

## 查看合併策略 {#view-merge-policies}

在 [!DNL Experience Platform] UI，您可以透過選取 **[!UICONTROL 設定檔]** ，然後選取 **[!UICONTROL 合併策略]** 標籤。 此頁簽包含貴組織的所有現有合併策略的清單，以及每個合併策略的詳細資訊，包括策略名稱、合併策略是否為預設合併策略以及合併策略相關的架構類。

![合併策略登錄頁](../images/merge-policies/landing.png)

要選擇可見的詳細資訊，或要向顯示添加其他列，請選擇 **[!UICONTROL 設定欄]** 並按一下列名以將其添加或從視圖中刪除。

![](../images/merge-policies/adjust-view.png)

## 建立合併策略 {#create-a-merge-policy}

要建立新合併策略，請選擇 **[!UICONTROL 建立合併策略]** 在「合併策略」頁簽上，輸入新的合併策略工作流。

![合併策略登錄頁面並突出顯示「建立」按鈕。](../images/merge-policies/create-new.png)

此 **[!UICONTROL 新合併策略]** 工作流程，需要您透過一系列引導式步驟，為新的合併原則提供重要資訊。 以下幾節將概述這些步驟。

![新的合併策略工作流。](../images/merge-policies/create.png)

## [!UICONTROL 設定] {#configure}

工作流程的第一步可讓您提供基本資訊，以設定合併原則。 此資訊包括：

* **[!UICONTROL 名稱]**:合併策略的名稱應具有描述性，但應簡明扼要。
* **[!UICONTROL 架構類]**:與合併策略關聯的XDM架構類。 這指定為其建立此合併策略的架構類。 組織可以為每個架構類建立多個合併策略。 目前僅 [!UICONTROL XDM個別設定檔] 類別可在UI中使用。 通過選擇 **[!UICONTROL 查看聯合架構]**. 如需詳細資訊，請參閱 [查看聯合架構](#view-union-schema) 接下來。
* **[!UICONTROL ID匯整]**:此欄位定義如何判斷客戶的相關身分。 身分匯整有兩個可能的值，請務必了解您選取的身分匯整類型對資料有何影響。 若要進一步了解，請參閱 [合併策略概述](overview.md).
   * **[!UICONTROL 無]**:不執行身分匯整。
   * **[!UICONTROL 專用圖表]**:根據您的私人身分圖表執行身分拼接。
* **[!UICONTROL 預設合併策略]**:一個切換按鈕，允許您選擇此合併策略是否為貴組織的預設策略。 如果切換了選取器，系統會顯示警告，要求您確認您要變更組織的預設合併原則。 請參閱 [合併策略概述](overview.md) 以深入了解預設合併原則。
   ![](../images/merge-policies/create-make-default.png)
* **[!UICONTROL 邊緣活動合併策略]**:此切換按鈕可讓您選取此合併原則是否在邊緣上處於作用中狀態。 為確保所有配置檔案使用者在邊緣上使用相同的視圖，可以將合併策略標籤為邊緣上的活動策略。 要在邊緣上激活段（標籤為邊緣段），必須將其綁定到標籤為邊緣上活動的合併策略。 如果區段為 **not** 系結至標示為在邊緣處於作用中狀態的合併原則，區段不會標示為在邊緣處於作用中狀態，且會標示為串流區段。 此外，組織中的每個沙箱只能 **one** 在邊緣處活動的合併策略。

完成必填欄位後，您可以選取 **[!UICONTROL 下一個]** 繼續工作流程。

![「Configure（配置）」完整螢幕，其中「Next（下一步）」按鈕突出顯示。](../images/merge-policies/create-complete.png)

## [!UICONTROL 查看聯合架構] {#view-union-schema}

建立或編輯合併策略時，可以通過選擇 **[!UICONTROL 查看聯合架構]**.

![](../images/merge-policies/view-union-schema.png)

這會開啟 [!UICONTROL 查看聯合架構] 對話方塊，顯示與聯合架構相關聯的所有貢獻結構、身分和關係。 您可以使用對話方塊，以存取 [!UICONTROL 聯合架構] 標籤 [!UICONTROL 設定檔] Platform UI的區段。

如需聯合結構的詳細資訊，包括如何在 [!UICONTROL 聯合架構] 標籤或 [!UICONTROL 查看聯合架構] 在「合併策略」工作流中顯示的對話框，請訪問 [union schema UI指南](../ui/union-schema.md).

![](../images/merge-policies/view-union-schema-dialog.png)

## [!UICONTROL 選取設定檔資料集] {#select-profile-datasets}

在 **[!UICONTROL 選取設定檔資料集]** 螢幕上，您必須選取 **[!UICONTROL 合併方法]** 用於合併策略的。 畫面上顯示的也是 [!UICONTROL 設定檔資料集] 在您的組織中，與上一個畫面上選取的架構類別相關。

根據您選擇的合併方法，所有設定檔資料集將按上次更新的順序合併（按時間戳順序排列），或者您需要選擇要納入合併策略的設定檔資料集以及合併它們的順序（資料集優先順序）。

有關合併方法的詳細資訊，請參閱 [合併策略概述](overview.md).

### 已訂購時間戳 {#timestamp-ordered-profile}

選取 **[!UICONTROL 已訂購時間戳]** 因為合併方法表示，最近更新資料集的屬性優先。 這適用於所有設定檔資料集。

>[!NOTE]
>
>旁方括弧中的數字 **[!UICONTROL 設定檔資料集]** (例如， `(37)` )顯示將包含的設定檔資料集總數。

![](../images/merge-policies/timestamp-ordered.png)

### 資料集優先順序 {#dataset-precedence-profile}

選取 **[!UICONTROL 資料集優先順序]** 因為合併方法需要您選取「設定檔」資料集，並手動排定其優先順序。 列出的每個資料集也包含上次批次擷取的狀態，或顯示通知，告知尚未將任何批次擷取至該資料集。

您可以從資料集清單中選取最多50個資料集，以納入合併原則。

>[!NOTE]
>
>旁方括弧中的數字 **[!UICONTROL 設定檔資料集]** (例如， `(37)` )顯示可供選取的設定檔資料集總數。

資料集經選取後，會新增至 **[!UICONTROL 選取資料集]** 區段，可讓您拖放資料集，並依所需優先順序排序。 當清單中調整資料集時，資料集旁的序數（1、2、3等）會更新，顯示優先順序（1為最高優先順序，2後再更新）。

選取資料集也會更新 **[!UICONTROL 聯合架構]** 區段中，顯示每個資料集貢獻資料的聯合結構中的欄位。 如需聯合結構的詳細資訊，包括如何與UI中的視覺效果互動，請參考 [union schema UI指南](../ui/union-schema.md)

![](../images/merge-policies/dataset-precedence.png)

## [!UICONTROL 選取ExperienceEvent資料集] {#select-experienceevent-datasets}

工作流程的下一步需要您選取ExperienceEvent資料集。 此畫面會受您在 [[!UICONTROL 選取設定檔資料集]](#select-profile-datasets) 螢幕。

### 已訂購時間戳 {#timestamp-ordered-experienceevent}

如果您選取 **[!UICONTROL 已訂購時間戳]** 設定檔資料集的合併方法，也會以最近更新之ExperienceEvent資料集的屬性優先。

>[!NOTE]
>
>旁方括弧中的數字 **[!UICONTROL ExperienceEvent資料集]** (例如， `(20)` )顯示貴組織建立的、與您在合併原則設定畫面上選取的結構類別相關的ExperienceEvent資料集總數。

![](../images/merge-policies/timestamp-experienceevent.png)

### 資料集優先順序 {#dataset-precedence-experienceevent}

如果您選取 **[!UICONTROL 資料集優先順序]** 設定檔資料集的合併方法，您必須選取要包含的ExperienceEvent資料集。 從資料集清單中最多可選取50個ExperienceEvent資料集。

>[!NOTE]
>
>旁方括弧中的數字 **[!UICONTROL ExperienceEvent資料集]** (例如， `(20)` )顯示貴組織建立的、與您在合併原則設定畫面上選取的結構類別相關的ExperienceEvent資料集總數。

選取資料集後，資料集會顯示在 [!UICONTROL 選取資料集] 區段。

無法手動排序ExperienceEvent資料集，只要ExperienceEvent資料集中的屬性屬於相同設定檔片段，就會附加至設定檔資料集。

與選取設定檔資料集類似，選取ExperienceEvent資料集也會更新 **[!UICONTROL 聯合架構]** 區段中，顯示每個資料集貢獻資料的聯合結構中的欄位。 如需聯合結構的詳細資訊，包括如何與UI中的視覺效果互動，請參考 [union schema UI指南](../ui/union-schema.md)

![](../images/merge-policies/dataset-precedence-experienceevent.png)

## [!UICONTROL 檢閱] {#review}

工作流程的最後一步是檢閱您的合併原則。 此 **[!UICONTROL 檢閱]** 畫面會顯示合併原則的相關資訊，包括選取的ID匯整方法、選取的合併方法，以及包含的資料集。 （若要檢視包含的所有設定檔或ExperienceEvent資料集，請選取要展開下拉式清單的資料集數量。）

檢閱畫面中也包含 **[!UICONTROL 預覽資料]** 表格顯示使用您的合併原則的設定檔記錄範例。 這可讓您在儲存合併原則前，預覽客戶設定檔的外觀。

請務必先仔細檢查合併策略配置並預覽資料，然後再選擇 **[!UICONTROL 完成]** 以完成建立工作流程。

### 已訂購時間戳 {#timestamp-ordered-review}

如果您選取 **[!UICONTROL 已訂購時間戳]** 作為合併策略的合併方法，配置檔案資料集清單包含貴組織建立的與架構類相關的所有資料集（按時間戳的順序）。 ExperienceEvent資料集清單包含貴組織針對所選結構類別建立的所有資料集，且這些資料集將附加至設定檔資料集。

此 **[!UICONTROL 預覽資料]** 表格根據資料集的時間戳記順序顯示設定檔記錄範例。 這可讓您在儲存合併原則前，預覽客戶設定檔的外觀。

![](../images/merge-policies/timestamp-review.png)

### 資料集優先順序 {#dataset-precedence-review}

如果您選取 **[!UICONTROL 資料集優先順序]** 作為合併原則的合併方法，「設定檔」和「ExperienceEvent」資料集清單僅包含您在建立工作流程期間分別選取的「設定檔」和「ExperienceEvent」資料集。 設定檔資料集的順序應與您在建立期間指定的優先順序相符。 如果沒有，請使用 [!UICONTROL 返回] 按鈕，返回到上一工作流步驟並調整優先順序。

此 **[!UICONTROL 預覽資料]** 表格顯示使用所選資料集的設定檔記錄範例。 這可讓您在儲存合併原則前，預覽客戶設定檔的外觀。

![](../images/merge-policies/dataset-precedence-review.png)

### 更新合併策略清單 {#updated-list}

完成建立新合併策略的工作流後，將返回到 **[!UICONTROL 合併策略]** 標籤。 貴組織的合併原則清單現在應包含您剛建立的合併原則。

![](../images/merge-policies/new-merge-policy-created.png)

## 編輯合併策略

從 [!UICONTROL 合併策略] 頁簽，您可以修改為 [!DNL XDM Individual Profile] 類別，方法是選取 **[!UICONTROL 策略名稱]** 針對要編輯的合併策略。

![合併策略登錄頁](../images/merge-policies/select-edit.png)

當 **[!UICONTROL 編輯合併策略]** 畫面中，您可以變更名稱和 [!UICONTROL ID匯整] 方法，並更改此策略是否為貴組織的預設合併策略。

選擇 **[!UICONTROL 下一個]** 繼續執行合併策略工作流以更新合併策略中包含的合併方法和資料集。

![](../images/merge-policies/edit-screen.png)

完成必要的更改後，請查看合併策略並選擇 **[!UICONTROL 完成]** 儲存變更並返回 [!UICONTROL 合併策略] 標籤。

>[!WARNING]
>
>更改合併策略可能會影響分段和配置檔案結果，因為它將改變解決資料衝突的方式。 保存合併策略之前，請務必仔細查看這些更改。

![](../images/merge-policies/edit-review.png)

## 違反資料控管政策

建立或更新合併原則時，會執行檢查，以判斷合併原則是否違反貴組織定義的任何資料使用原則。 資料使用原則是Adobe Experience Platform資料控管的一部分，也是描述您可針對特定執行或限制執行之行銷動作種類的規則 [!DNL Platform] 資料。 例如，如果使用合併策略建立激活到第三方目標的段，並且您的組織具有阻止將特定資料導出到第三方的資料使用策略，則您將收到 **[!UICONTROL 檢測到資料控管策略違規]** 通知。

此通知包括已違反的資料使用策略清單，允許您通過從清單中選擇策略來查看違規的詳細資訊。 選擇違反的策略時， **[!UICONTROL 資料處理]** 索引標籤提供違反和受影響啟用的原因，每個都提供資料使用原則遭違反的詳細資訊。

若要進一步了解Adobe Experience Platform中如何執行資料控管，請先閱讀 [資料控管概觀](../../data-governance/home.md).

![](../images/merge-policies/policy-violation.png)

## 後續步驟

現在您已為組織建立並設定合併原則，您可以使用這些原則來調整Platform中客戶設定檔的檢視，並從您的設定檔資料建立受眾區段。 請參閱 [細分概述](../../segmentation/home.md) 以取得如何使用建立和使用區段的詳細資訊 [!DNL Experience Platform] UI和API。
