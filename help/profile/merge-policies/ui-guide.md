---
keywords: Experience Platform；設定檔；即時客戶設定檔；合併原則；UI；使用者介面；時間戳記順序；資料集優先順序
title: 合併策略UI指南
type: Documentation
description: 在Experience Platform中將多個來源的資料匯整在一起時，Platform會使用合併原則來判斷資料的優先順序，以及將哪些資料合併以建立統一檢視。 本指南提供使用Adobe Experience Platform使用者介面處理合併原則的逐步指示。
exl-id: 0489217a-6a53-428c-a531-fd0a0e5bb71f
source-git-commit: a6a49b4cf9c89b5c6b4679f36daede93590ffb3c
workflow-type: tm+mt
source-wordcount: '2193'
ht-degree: 0%

---


# 合併策略UI指南

Adobe Experience Platform可讓您從多個來源將資料片段匯整在一起，並加以結合，以便查看每個客戶的完整檢視。 將此資料集合在一起時，[!DNL Platform]會使用合併原則來判斷資料的優先順序，以及將結合哪些資料來建立統一檢視。

使用RESTful API或用戶介面，您可以建立新的合併策略、管理現有策略，以及為組織設定預設的合併策略。 本指南提供使用Adobe Experience Platform使用者介面(UI)處理合併原則的逐步指示。

要了解有關合併策略及其在Experience Platform中所扮演角色的詳細資訊，請從閱讀[合併策略概述](overview.md)開始。

## 快速入門

本指南需要認真了解幾個重要的[!DNL Experience Platform]功能。 在遵循本指南之前，請先檢閱以下服務的檔案：

* [即時客戶個人檔案](../home.md):根據來自多個來源的匯總資料，提供統一的即時消費者設定檔。
* [Adobe Experience Platform Identity Service](../../identity-service/home.md):借由橋接從擷取到的不同資料來源的身分識別，來啟用即時客戶設 [!DNL Platform]定檔。
* [Experience Data Model(XDM)](../../xdm/home.md):組織客戶體驗資 [!DNL Platform] 料的標準化架構。

## 查看合併策略 {#view-merge-policies}

在[!DNL Experience Platform] UI中，您可以通過在左側導航中選擇&#x200B;**[!UICONTROL Profiles]**，然後選擇&#x200B;**[!UICONTROL Merge Policies]**&#x200B;頁簽，開始使用合併策略。 此頁簽包含貴組織的所有現有合併策略的清單，以及每個合併策略的詳細資訊，包括策略名稱、合併策略是否為預設合併策略以及合併策略相關的架構類。

![合併策略登錄頁](../images/merge-policies/landing.png)

要選擇可見的詳細資訊，或要向顯示添加其他列，請選擇&#x200B;**[!UICONTROL 配置列]**，然後按一下列名以添加或從視圖中刪除列。

![](../images/merge-policies/adjust-view.png)

## 建立合併策略 {#create-a-merge-policy}

要建立新合併策略，請在合併策略頁簽上選擇&#x200B;**[!UICONTROL 建立合併策略]**&#x200B;以輸入新的合併策略工作流。

![合併策略登錄頁面並突出顯示「建立」按鈕。](../images/merge-policies/create-new.png)

**[!UICONTROL 新合併策略]**&#x200B;工作流要求您通過一系列引導步驟為新合併策略提供重要資訊。 以下幾節將概述這些步驟。

![新的合併策略工作流。](../images/merge-policies/create.png)

## [!UICONTROL 設定] {#configure}

工作流程的第一步可讓您提供基本資訊，以設定合併原則。 此資訊包括：

* **[!UICONTROL 名稱]**:合併策略的名稱應具有描述性，但應簡明扼要。
* **[!UICONTROL 架構類]**:與合併策略關聯的XDM架構類。這指定為其建立此合併策略的架構類。 組織可以為每個架構類建立多個合併策略。 目前，UI中僅提供[!UICONTROL XDM個別設定檔]類別。 通過選擇&#x200B;**[!UICONTROL 查看聯合架構]**，可預覽架構類的聯合架構。 如需詳細資訊，請參閱以下關於[檢視聯合架構](#view-union-schema)的區段。
* **[!UICONTROL ID匯整]**:此欄位定義如何判斷客戶的相關身分。身分匯整有兩個可能的值，請務必了解您選取的身分匯整類型對資料有何影響。 若要進一步了解，請參閱[合併原則概述](overview.md)。
   * **[!UICONTROL 無]**:不執行身分匯整。
   * **[!UICONTROL 專用圖表]**:根據您的私人身分圖表執行身分拼接。
* **[!UICONTROL 預設合併策略]**:一個切換按鈕，允許您選擇此合併策略是否為貴組織的預設策略。如果切換了選取器，系統會顯示警告，要求您確認您要變更組織的預設合併原則。 請參閱[合併原則概述](overview.md)以深入了解預設合併原則。
   ![](../images/merge-policies/create-make-default.png)

完成必填欄位後，您可以選取&#x200B;**[!UICONTROL Next]**&#x200B;以繼續工作流程。

![「Configure（配置）」完整螢幕，其中「Next（下一步）」按鈕突出顯示。](../images/merge-policies/create-complete.png)

## [!UICONTROL 查看聯合架構] {#view-union-schema}

建立或編輯合併策略時，可以通過選擇&#x200B;**[!UICONTROL 查看聯合架構]**&#x200B;來查看所選架構類的聯合架構。

![](../images/merge-policies/view-union-schema.png)

這將開啟[!UICONTROL 查看聯合架構]對話框，顯示與聯合架構關聯的所有貢獻架構、身份和關係。 您可以使用對話方塊，以存取Platform UI中[!UICONTROL Profiles]區段中的[!UICONTROL Union Schema]標籤，以相同方式探索聯合架構。

有關聯合架構的詳細資訊，包括如何在[!UICONTROL 聯合架構]頁簽或合併策略工作流中顯示的[!UICONTROL 查看聯合架構]對話框中與它們交互，請訪問[聯合架構UI指南](../ui/union-schema.md)。

![](../images/merge-policies/view-union-schema-dialog.png)

## [!UICONTROL 選取設定檔資料集] {#select-profile-datasets}

在&#x200B;**[!UICONTROL 選擇配置檔案資料集]**&#x200B;螢幕上，必須選擇要用於合併策略的&#x200B;**[!UICONTROL 合併方法]**。 螢幕上還顯示貴組織中與上一個螢幕上所選架構類別相關的[!UICONTROL 設定檔資料集]總數。

根據您選擇的合併方法，所有設定檔資料集將按上次更新的順序合併（按時間戳順序排列），或者您需要選擇要納入合併策略的設定檔資料集以及合併它們的順序（資料集優先順序）。

有關合併方法的詳細資訊，請參閱[合併策略概述](overview.md)。

### 已訂購時間戳 {#timestamp-ordered-profile}

選擇&#x200B;**[!UICONTROL 按順序排列的時間戳]**&#x200B;作為合併方法，表示將優先於最近更新資料集中的屬性。 這適用於所有設定檔資料集。

>[!NOTE]
>
>**[!UICONTROL 設定檔資料集]**&#x200B;旁方括弧中的數字（例如，所顯示影像中的`(37)`）會顯示將包含的設定檔資料集總數。

![](../images/merge-policies/timestamp-ordered.png)

### 資料集優先順序 {#dataset-precedence-profile}

選取&#x200B;**[!UICONTROL 資料集優先順序]**&#x200B;作為合併方法時，您必須選取「設定檔」資料集，並手動排定其優先順序。 列出的每個資料集也包含上次批次擷取的狀態，或會顯示通知，告知尚未將任何批次擷取至該資料集。

您可以從資料集清單中選取最多50個資料集，以納入合併原則。

>[!NOTE]
>
>**[!UICONTROL 設定檔資料集]**&#x200B;旁方括弧中的數字（例如，所顯示影像中的`(37)`）顯示可供選取的設定檔資料集總數。

選取資料集後，資料集會新增至&#x200B;**[!UICONTROL 選取資料集]**&#x200B;區段，讓您拖放資料集，並依所需優先順序排序。 當清單中調整資料集時，資料集旁的序數（1、2、3等）會更新，顯示優先順序（1為最高優先順序，2後再更新）。

選取資料集也會更新&#x200B;**[!UICONTROL 聯合結構]**&#x200B;區段，顯示每個資料集貢獻資料的聯合結構中的欄位。 如需聯合結構的詳細資訊，包括如何與UI中的視覺效果互動，請參閱[聯合結構UI指南](../ui/union-schema.md)

![](../images/merge-policies/dataset-precedence.png)

## [!UICONTROL 選取ExperienceEvent資料集] {#select-experienceevent-datasets}

工作流程的下一步需要您選取ExperienceEvent資料集。 此畫面會受您在[[!UICONTROL 選取設定檔資料集]](#select-profile-datasets)畫面上選取的合併方法影響。

### 已訂購時間戳 {#timestamp-ordered-experienceevent}

如果您選取&#x200B;**[!UICONTROL 已排序時間戳記]**&#x200B;作為設定檔資料集的合併方法，此處也會優先使用最近更新之ExperienceEvent資料集的屬性。

>[!NOTE]
>
>**[!UICONTROL ExperienceEvent資料集]**&#x200B;旁方括弧中的數字（例如，顯示的影像中的`(20)`）顯示貴組織所建立、與您在合併原則設定畫面上選取的架構類別相關的ExperienceEvent資料集總數。

![](../images/merge-policies/timestamp-experienceevent.png)

### 資料集優先順序 {#dataset-precedence-experienceevent}

如果您選取&#x200B;**[!UICONTROL 資料集優先順序]**&#x200B;作為設定檔資料集的合併方法，則需要選取要包含的ExperienceEvent資料集。 從資料集清單中最多可選取50個ExperienceEvent資料集。

>[!NOTE]
>
>**[!UICONTROL ExperienceEvent資料集]**&#x200B;旁方括弧中的數字（例如，顯示的影像中的`(20)`）顯示貴組織所建立、與您在合併原則設定畫面上選取的架構類別相關的ExperienceEvent資料集總數。

選取資料集後，資料集會顯示在[!UICONTROL 選取資料集]區段中。

無法手動排序ExperienceEvent資料集，只要ExperienceEvent資料集中的屬性屬於相同設定檔片段，就會附加至設定檔資料集。

與選取「設定檔」資料集類似，選取ExperienceEvent資料集也會更新&#x200B;**[!UICONTROL 聯合結構]**&#x200B;區段，顯示每個資料集貢獻資料的聯合結構中的欄位。 如需聯合結構的詳細資訊，包括如何與UI中的視覺效果互動，請參閱[聯合結構UI指南](../ui/union-schema.md)

![](../images/merge-policies/dataset-precedence-experienceevent.png)

## [!UICONTROL 檢閱] {#review}

工作流程的最後一步是檢閱您的合併原則。 **[!UICONTROL Review]**&#x200B;螢幕顯示有關合併策略的資訊，包括所選ID拼接方法、所選合併方法以及包含的資料集。 （若要檢視包含的所有設定檔或ExperienceEvent資料集，請選取要展開下拉式清單的資料集數量。）

審核螢幕中還包含&#x200B;**[!UICONTROL 預覽資料]**&#x200B;表，顯示使用合併策略的配置檔案記錄示例。 這可讓您在儲存合併原則前，預覽客戶設定檔的外觀。

在選擇&#x200B;**[!UICONTROL 完成]**&#x200B;以完成建立工作流之前，請確保仔細檢查合併策略配置並預覽資料。

### 已訂購時間戳 {#timestamp-ordered-review}

如果您選擇&#x200B;**[!UICONTROL 按順序排列的時間戳]**&#x200B;作為合併策略的合併方法，則配置檔案資料集清單將按時間戳順序包括貴組織建立的與架構類相關的所有資料集。 ExperienceEvent資料集清單包含貴組織針對所選結構類別建立的所有資料集，且這些資料集將附加至設定檔資料集。

**[!UICONTROL 預覽資料]**&#x200B;表格根據資料集的時間戳記順序顯示設定檔記錄範例。 這可讓您在儲存合併原則前，預覽客戶設定檔的外觀。

![](../images/merge-policies/timestamp-review.png)

### 資料集優先順序 {#dataset-precedence-review}

如果您選取&#x200B;**[!UICONTROL 資料集優先順序]**&#x200B;作為合併原則的合併方法，則設定檔和ExperienceEvent資料集清單只會包含您在建立工作流程期間分別選取的設定檔和ExperienceEvent資料集。 設定檔資料集的順序應與您在建立期間指定的優先順序相符。 如果沒有，請使用[!UICONTROL Back]按鈕返回到以前的工作流步驟並調整優先順序。

**[!UICONTROL 預覽資料]**&#x200B;表格顯示使用所選資料集的設定檔記錄範例。 這可讓您在儲存合併原則前，預覽客戶設定檔的外觀。

![](../images/merge-policies/dataset-precedence-review.png)

### 更新合併策略清單 {#updated-list}

完成建立新合併策略的工作流後，您將返回到&#x200B;**[!UICONTROL Merge Policies]**&#x200B;頁簽。 貴組織的合併原則清單現在應包含您剛建立的合併原則。

![](../images/merge-policies/new-merge-policy-created.png)

## 編輯合併策略

從[!UICONTROL 合併策略]頁簽中，可以通過為要編輯的合併策略選擇&#x200B;**[!UICONTROL 策略名稱]**&#x200B;來修改為[!DNL XDM Individual Profile]類建立的現有合併策略。

![合併策略登錄頁](../images/merge-policies/select-edit.png)

出現&#x200B;**[!UICONTROL 編輯合併策略]**&#x200B;螢幕時，您可以更改名稱和[!UICONTROL ID拼接]方法，並更改此策略是否為貴組織的預設合併策略。

選擇&#x200B;**[!UICONTROL Next]**&#x200B;以繼續執行合併策略工作流以更新合併策略中包含的合併方法和資料集。

![](../images/merge-policies/edit-screen.png)

完成必要的更改後，請查看合併策略並選擇&#x200B;**[!UICONTROL 完成]**&#x200B;以保存更改並返回[!UICONTROL 合併策略]頁簽。

>[!WARNING]
>
>更改合併策略可能會影響分段和配置檔案結果，因為它將改變解決資料衝突的方式。 保存合併策略之前，請務必仔細查看這些更改。

![](../images/merge-policies/edit-review.png)

## 違反資料控管政策

建立或更新合併原則時，會執行檢查，以判斷合併原則是否違反貴組織定義的任何資料使用原則。 資料使用原則是Adobe Experience Platform [!DNL Data Governance]的一部分，也是描述您可對特定[!DNL Platform]資料執行或限制的行銷動作類型的規則。 例如，如果使用合併策略建立激活到第三方目標的段，並且您的組織具有阻止將特定資料導出到第三方的資料使用策略，則在嘗試保存合併策略時，您將收到&#x200B;**[!UICONTROL 檢測到]**&#x200B;資料治理策略違規通知。

此通知包括已違反的資料使用策略清單，允許您通過從清單中選擇策略來查看違規的詳細資訊。 在選擇違反的策略時，**[!UICONTROL 資料處理]**&#x200B;頁簽提供了違反的原因和受影響的激活，每個頁簽都提供了有關資料使用策略被違反情況的更詳細資訊。

若要進一步了解如何在Adobe Experience Platform中執行資料控管，請先閱讀[資料控管概述](../../data-governance/home.md)開始。

![](../images/merge-policies/policy-violation.png)

## 後續步驟

現在您已為組織建立並設定合併原則，您可以使用這些原則來調整Platform中客戶設定檔的檢視，並從您的設定檔資料建立受眾區段。 如需如何使用[!DNL Experience Platform] UI和API建立及使用區段的詳細資訊，請參閱[區段概觀](../../segmentation/home.md)。
