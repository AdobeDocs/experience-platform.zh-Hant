---
keywords: Experience Platform；配置檔案；即時客戶配置檔案；合併策略；UI；用戶介面；時間戳排序；資料集優先順序
title: 合併策略UI指南
type: Documentation
description: 當將來自多個源的資料集中到Experience Platform中時，合併策略是平台用來確定資料優先順序以及將哪些資料合併以建立統一視圖的規則。 本指南提供使用Adobe Experience Platform用戶介面處理合併策略的逐步說明。
exl-id: 0489217a-6a53-428c-a531-fd0a0e5bb71f
source-git-commit: 34e0381d40f884cd92157d08385d889b1739845f
workflow-type: tm+mt
source-wordcount: '2321'
ht-degree: 0%

---


# 合併策略UI指南

Adobe Experience Platform使您能夠將來自多個來源的資料片段組合在一起，並將它們組合起來，以便查看您每個客戶的完整視圖。 將此資料整合在一起時，合併策略是 [!DNL Platform] 用於確定資料的優先順序以及將組合哪些資料以建立統一視圖。

使用REST風格的API或用戶介面，您可以建立新的合併策略、管理現有策略以及為組織設定預設的合併策略。 本指南提供了使用Adobe Experience Platform用戶介面(UI)使用合併策略的逐步說明。

要瞭解有關合併策略及其在Experience Platform中所扮演角色的詳細資訊，請首先閱讀 [合併策略概述](overview.md)。

## 快速入門

本指南要求對以下幾項重要內容進行工作理解 [!DNL Experience Platform] 功能。 在遵循本指南之前，請查看以下服務的文檔：

* [即時客戶配置檔案](../home.md):基於來自多個源的聚合資料提供統一、即時的用戶配置檔案。
* [Adobe Experience Platform身份服務](../../identity-service/home.md):通過將不同資料源的標識橋接到中，實現即時客戶概要資訊 [!DNL Platform]。
* [體驗資料模型(XDM)](../../xdm/home.md):標準化框架 [!DNL Platform] 組織客戶體驗資料。

## 查看合併策略 {#view-merge-policies}

在 [!DNL Experience Platform] UI，您可以通過選擇 **[!UICONTROL 配置檔案]** 在左側導航中，然後選擇 **[!UICONTROL 合併策略]** 頁籤。 此頁籤包含組織的所有現有合併策略的清單，以及每個合併策略的詳細資訊，包括策略名稱、合併策略是否是預設合併策略以及合併策略所關聯的架構類。

![合併策略登錄頁](../images/merge-policies/landing.png)

要選擇哪些詳細資訊可見，或要向顯示添加其他列，請選擇 **[!UICONTROL 配置列]** 並按一下列名以添加或從視圖中刪除它。

![](../images/merge-policies/adjust-view.png)

## 建立合併策略 {#create-a-merge-policy}

要建立新合併策略，請選擇 **[!UICONTROL 建立合併策略]** 在「合併策略」頁籤上輸入新的合併策略工作流。

![將策略登錄頁與「建立」按鈕合併。](../images/merge-policies/create-new.png)

的 **[!UICONTROL 新建合併策略]** 工作流，要求您通過一系列指導性步驟為新合併策略提供重要資訊。 以下各節概述了這些步驟。

![新合併策略工作流。](../images/merge-policies/create.png)

## [!UICONTROL 設定] {#configure}

工作流的第一步允許您通過提供基本資訊來配置合併策略。 此資訊包括：

* **[!UICONTROL 名稱]**:合併策略的名稱應描述性而簡潔。
* **[!UICONTROL 架構類]**:與合併策略關聯的XDM架構類。 這指定為其建立此合併策略的架構類。 組織可以為每個架構類建立多個合併策略。 當前僅 [!UICONTROL XDM個人配置檔案] 類在UI中可用。 通過選擇 **[!UICONTROL 查看聯合架構]**。 有關詳細資訊，請參閱 [查看聯合架構](#view-union-schema) 接下來。
* **[!UICONTROL ID拼接]**:此欄位定義如何確定客戶的相關標識。 身份拼接有兩個可能的值，瞭解您選擇的身份拼接類型將如何影響資料非常重要。 要瞭解更多資訊，請參閱 [合併策略概述](overview.md)。
   * **[!UICONTROL 無]**:不執行身份拼接。
   * **[!UICONTROL 專用圖]**:根據您的個人身份圖執行身份拼接。
* **[!UICONTROL 預設合併策略]**:一個切換按鈕，允許您選擇此合併策略是否是您組織的預設策略。 如果選擇器處於切換狀態，則會出現警告，要求您確認要更改組織的預設合併策略。 查看 [合併策略概述](overview.md) 瞭解有關預設合併策略的詳細資訊。
   ![](../images/merge-policies/create-make-default.png)
* **[!UICONTROL 活動 — 邊緣合併策略]**:一個切換按鈕，允許您選擇此合併策略是否在邊緣上處於活動狀態。 為確保所有配置檔案使用者都使用相同的邊緣視圖，合併策略可標籤為邊緣上處於活動狀態。 要使段在邊上激活（標籤為邊段），必須將其綁定到在邊上標籤為活動的合併策略。 如果段為 **不** 綁定到標籤為邊緣上活動的合併策略，該段將不會標籤為邊緣上的活動段，並將標籤為流段。 此外，組織中的每個沙箱只能 **一個** 邊緣上處於活動狀態的合併策略。

完成必填欄位後，您可以選擇 **[!UICONTROL 下一個]** 以繼續工作流。

![選中「Next（下一步）」按鈕的完整「Configure（配置）」螢幕。](../images/merge-policies/create-complete.png)

## [!UICONTROL 查看聯合架構] {#view-union-schema}

建立或編輯合併策略時，可以通過選擇 **[!UICONTROL 查看聯合架構]**。

![](../images/merge-policies/view-union-schema.png)

開啟 [!UICONTROL 查看聯合架構] 對話框，顯示與聯合架構關聯的所有參與架構、標識和關係。 可以使用對話框以與訪問 [!UICONTROL 聯合架構] 的 [!UICONTROL 配置檔案] 的子菜單。

有關聯合架構的詳細資訊，包括如何在 [!UICONTROL 聯合架構] 頁籤 [!UICONTROL 查看聯合架構] 對話框顯示在合併策略工作流中，請訪問 [聯合架構UI指南](../ui/union-schema.md)。

![](../images/merge-policies/view-union-schema-dialog.png)

## [!UICONTROL 選擇配置檔案資料集] {#select-profile-datasets}

在 **[!UICONTROL 選擇配置檔案資料集]** 螢幕，必須選擇 **[!UICONTROL 合併方法]** 用於合併策略。 螢幕上還顯示 [!UICONTROL 配置檔案資料集] 與上一螢幕上選定的架構類相關的組織中。

根據您選擇的合併方法，所有配置檔案資料集將按上次更新的順序（按時間戳順序排列）合併，或者您需要選擇合併策略中要包括的配置檔案資料集以及合併它們的順序（資料集優先順序）。

有關合併方法的詳細資訊，請參閱 [合併策略概述](overview.md)。

### 按時間戳排序 {#timestamp-ordered-profile}

選擇 **[!UICONTROL 按時間戳排序]** 因為合併方法意味著來自最近更新的資料集的屬性將優先。 這適用於所有Profile資料集。

>[!NOTE]
>
>括弧旁的數字 **[!UICONTROL 配置檔案資料集]** (例如， `(37)` )顯示將包含的配置檔案資料集總數。

![](../images/merge-policies/timestamp-ordered.png)

### 資料集優先順序 {#dataset-precedence-profile}

選擇 **[!UICONTROL 資料集優先順序]** 因為合併方法要求您選擇配置檔案資料集並手動確定它們的優先順序。 列出的每個資料集還包括所攝取的最後一個批處理的狀態，或顯示未將任何批處理納入該資料集的通知。

您可以從資料集清單中選擇最多50個資料集以包括在合併策略中。

>[!NOTE]
>
>括弧旁的數字 **[!UICONTROL 配置檔案資料集]** (例如， `(37)` 顯示可供選擇的配置檔案資料集的總數。

在選擇資料集時，會將其添加到 **[!UICONTROL 選擇資料集]** 的子目錄。 當資料集在清單中進行調整時，資料集旁邊的序號（1、2、3等）將更新，顯示優先順序（1被指定為最高優先順序，然後是2，然後是繼續）。

選擇資料集還會更新 **[!UICONTROL 聯合架構]** 部分，顯示每個資料集提供資料的聯合架構中的欄位。 有關聯合架構的詳細資訊，包括如何與UI中的可視化效果交互，請參考 [聯合架構UI指南](../ui/union-schema.md)

![](../images/merge-policies/dataset-precedence.png)

## [!UICONTROL 選擇ExperienceEvent資料集] {#select-experienceevent-datasets}

工作流的下一步需要您選擇ExperienceEvent資料集。 此螢幕受您在 [[!UICONTROL 選擇配置檔案資料集]](#select-profile-datasets) 的上界。

### 按時間戳排序 {#timestamp-ordered-experienceevent}

如果已選擇 **[!UICONTROL 按時間戳排序]** 作為Profile資料集的合併方法，最近更新的ExperienceEvent資料集的屬性也將在此處優先。

>[!NOTE]
>
>括弧旁的數字 **[!UICONTROL ExperienceEvent資料集]** (例如， `(20)` 在所示影像中)顯示由您的組織建立的與您在合併策略配置螢幕上選擇的架構類相關的ExperienceEvent資料集的總數。

![](../images/merge-policies/timestamp-experienceevent.png)

### 資料集優先順序 {#dataset-precedence-experienceevent}

如果已選擇 **[!UICONTROL 資料集優先順序]** 作為Profile資料集的合併方法，您需要選擇要包括的ExperienceEvent資料集。 可以從資料集清單中選擇最多50個ExperienceEvent資料集。

>[!NOTE]
>
>括弧旁的數字 **[!UICONTROL ExperienceEvent資料集]** (例如， `(20)` 在所示影像中)顯示由您的組織建立的與您在合併策略配置螢幕上選擇的架構類相關的ExperienceEvent資料集的總數。

當選擇資料集時，它們將出現在 [!UICONTROL 選擇資料集] 的子菜單。

無法手動對ExperienceEvent資料集進行排序，而ExperienceEvent資料集中的屬性將附加到Profile資料集（如果屬於同一配置檔案片段）。

與選擇Profile資料集類似，選擇ExperienceEvent資料集也會更新 **[!UICONTROL 聯合架構]** 部分，顯示每個資料集提供資料的聯合架構中的欄位。 有關聯合架構的詳細資訊，包括如何與UI中的可視化效果交互，請參考 [聯合架構UI指南](../ui/union-schema.md)

![](../images/merge-policies/dataset-precedence-experienceevent.png)

## [!UICONTROL 請檢閱] {#review}

工作流中的最後一步是查看合併策略。 的 **[!UICONTROL 審閱]** 螢幕顯示有關合併策略的資訊，包括選定的ID拼接方法、選定的合併方法以及包含的資料集。 （要查看包含的所有Profile或ExperieEvent資料集，請選擇要展開下拉清單的資料集數。）

此外，在審閱螢幕中還包括 **[!UICONTROL 預覽資料]** 顯示使用合併策略的示例配置檔案記錄的表。 這使您能夠在保存合併策略之前預覽客戶配置檔案的外觀。

請確保在選擇合併策略之前仔細檢查合併策略配置並預覽資料 **[!UICONTROL 完成]** 的子菜單。

### 按時間戳排序 {#timestamp-ordered-review}

如果已選擇 **[!UICONTROL 按時間戳排序]** 作為合併策略的合併方法，配置檔案資料集清單按時間戳順序包括由您的組織建立的與架構類相關的所有資料集。 ExperienceEvent資料集清單包括您的組織為所選架構類建立的所有資料集，並將附加到配置檔案資料集。

的 **[!UICONTROL 預覽資料]** 該表顯示基於資料集時間戳順序的示例配置檔案記錄。 這使您能夠在保存合併策略之前預覽客戶配置檔案的外觀。

![](../images/merge-policies/timestamp-review.png)

### 資料集優先順序 {#dataset-precedence-review}

如果已選擇 **[!UICONTROL 資料集優先順序]** 作為合併策略的合併方法，Profile和ExperienceEvent資料集清單僅分別包含您在建立工作流期間選擇的Profile和ExperienceEvent資料集。 配置檔案資料集的順序應與建立期間指定的優先順序相匹配。 否則，使用 [!UICONTROL 後退] 按鈕，來調整優先順序。

的 **[!UICONTROL 預覽資料]** 表顯示了使用所選資料集的示例配置檔案記錄。 這使您能夠在保存合併策略之前預覽客戶配置檔案的外觀。

![](../images/merge-policies/dataset-precedence-review.png)

### 更新的合併策略清單 {#updated-list}

完成工作流以建立新合併策略後，您將返回到 **[!UICONTROL 合併策略]** 頁籤。 您組織的合併策略清單現在應包括您剛剛建立的合併策略。

![](../images/merge-policies/new-merge-policy-created.png)

## 編輯合併策略

從 [!UICONTROL 合併策略] 頁籤，您可以修改為 [!DNL XDM Individual Profile] 類 **[!UICONTROL 策略名稱]** 合併策略。

![合併策略登錄頁](../images/merge-policies/select-edit.png)

當 **[!UICONTROL 編輯合併策略]** 螢幕中，您可以更改名稱和 [!UICONTROL ID拼接] 方法，以及更改此策略是否是您組織的預設合併策略。

選擇 **[!UICONTROL 下一個]** 繼續通過合併策略工作流更新合併策略中包含的合併方法和資料集。

![](../images/merge-policies/edit-screen.png)

完成必要的更改後，查看合併策略並選擇 **[!UICONTROL 完成]** 保存更改並返回 [!UICONTROL 合併策略] 頁籤。

>[!WARNING]
>
>更改合併策略可能會影響分段和配置檔案結果，因為它將改變解決資料衝突的方式。 在保存合併策略之前，請務必仔細檢查對合併策略所做的更改。

![](../images/merge-policies/edit-review.png)

## 違反資料治理策略

在建立或更新合併策略時，會執行檢查以確定合併策略是否違反了組織定義的任何資料使用策略。 資料使用策略是Adobe Experience Platform資料治理的一部分，是描述您在特定情況下可以執行或限制執行的營銷操作類型的規則 [!DNL Platform] 資料。 例如，如果合併策略用於建立激活到第三方目標的段，並且您的組織具有阻止將特定資料導出到第三方的資料使用策略，則您將收到 **[!UICONTROL 檢測到資料治理策略違規]** 嘗試保存合併策略時發出通知。

此通知包括已違反的資料使用策略清單，並允許您通過從清單中選擇策略來查看違規的詳細資訊。 選擇違反的策略時， **[!UICONTROL 資料沿襲]** 頁籤提供違規的原因和受影響的激活，每個選項都提供了違反資料使用策略的更詳細資訊。

要瞭解有關在Adobe Experience Platform內如何執行資料治理的更多資訊，請首先閱讀 [資料治理概述](../../data-governance/home.md)。

![](../images/merge-policies/policy-violation.png)

## 後續步驟

現在，您已經為您的組織建立和配置了合併策略，您可以使用這些策略來調整平台內客戶配置檔案的視圖，並從您的配置檔案資料建立受眾段。 查看 [分段概述](../../segmentation/home.md) 有關如何使用 [!DNL Experience Platform] UI和API。
