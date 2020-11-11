---
keywords: Experience Platform;profile;real-time customer profile;merge policies;UI;user interface;timestamp ordered;dataset precedence
title: 合併策略UI指南
topic: guide
translation-type: tm+mt
source-git-commit: 6bfc256b50542e88e28f8a0c40cec7a109a05aa6
workflow-type: tm+mt
source-wordcount: '2667'
ht-degree: 0%

---


# 合併策略UI指南

Adobe Experience Platform可讓您從多個來源匯整資料片段，並加以匯整，以全面瞭解每個客戶。 將這些資料整合在一起時，合併原則是用來決定 [!DNL Platform] 資料的優先順序以及將哪些資料合併以建立該統一檢視的規則。

例如，如果客戶透過多個通道與您的品牌互動，您的組織將會在多個資料集中顯示與該單一客戶相關的多個描述檔片段。 當這些片段被收錄到Platform中時，會將它們合併在一起，以便為該客戶建立單一個人檔案。 當來自多個來源的資料發生衝突（例如，一個片段將客戶列為「單一」，而另一個片段將客戶列為「已婚」）時，合併原則會決定要包含在個人描述檔中的資訊。

使用REST風格的API或用戶介面，您可以建立新的合併策略、管理現有策略，並為組織設定預設的合併策略。 本指南提供使用Adobe Experience Platform使用者介面(UI)處理合併原則的逐步指示。

如果您希望使用 [!DNL Real-time Customer Profile] API處理合併策略，請遵循合併策略API指南 [中的說明](../api/merge-policies.md)。

## 快速入門

本指南需要對幾項重要功能有充分的 [!DNL Experience Platform] 認識。 在遵循本指南或使用描述檔API之前，請先閱讀下列服務的檔案：

* [[!DNL Real-time Customer Profile]](../home.md):根據來自多個來源的匯整資料，提供統一、即時的消費者個人檔案。
* [Adobe Experience Platform Identity Service](../../identity-service/home.md):借由將不同資料來源的身分融入其中，以建立即時客戶個人檔案 [!DNL Platform]。
* [[!DNL Experience Data Model] (XDM)](../../xdm/home.md):組織客戶體驗資料 [!DNL Platform] 的標準化架構。

## 合併方法 {#merge-methods}

每個描述檔片段包含的資訊，僅包含個人可能存在的身分總數中的一個身分。 將這些資料合併以形成客戶個人檔案時，可能會有該資訊發生衝突，且必須指定優先順序。 選擇合併方法可讓您指定在資料集之間發生合併衝突時要優先排序的資料集屬性。

合併策略有兩種可能的合併方法。 以下各節將概述這些方法，並提供其他詳細資料：

* **[!UICONTROL 排序時間戳]:** 發生衝突時，會優先處理最近更新的描述檔片段。
   * **自訂時間戳記：**[!UICONTROL 排序的時間戳] ，也支援自訂時間戳記，當合併相同資料集（多重身分）或跨資料集的資料時，這些時間戳記優先於系統時間戳記。 如需詳細資訊，請參閱使用自訂 [時間戳記的章節](#custom-timestamps)。
* **[!UICONTROL 資料集優先順序]:** 在發生衝突時，請根據個人資料片段的來源資料集，優先處理其片段。 選擇此選項時，必須選擇相關資料集及其優先順序順序。

### 排序時間戳記 {#timestamp-ordered}

當描述檔記錄被收錄到Experience Platform時，系統會在擷取時取得系統時間戳記並新增至記錄。 當選 **[!UICONTROL 擇Timestamp ordered]** 作為合併策略的合併方法時，將基於系統時間戳合併配置檔案。 換言之，合併是根據記錄被收錄到平台的時間戳記進行。

#### 使用自訂時間戳記 {#custom-timestamps}

有時，有時需要提供自訂時間戳記，並讓合併原則遵循自訂時間戳記，而非系統時間戳記的使用情形。 例如，回填資料或在記錄未依順序收錄時，確保事件順序正確。

為了使用自定義時間戳記，必須將 **[!UICONTROL External Source System Audit Details Mixin]** 添加到您的Profile架構中。 新增後，可使用欄位填入自訂時間 `lastUpdatedDate` 戳記。 當記錄已填入欄位時， `lastUpdatedDate` Experience Platform會使用該欄位來合併資料集上的記錄。 如果 `lastUpdatedDate` 未顯示或未填入，平台將繼續使用系統時間戳記。

>[!NOTE]
>
>您必須確保在同 `lastUpdatedDate` 一記錄上接收更新時填入時間戳記。

以下螢幕抓圖顯示「外部源系統 [!UICONTROL 審計詳細資訊混合」中的欄位]。 有關使用平台UI使用架構（包括如何將混合新增至架構）的逐步指示，請造訪使用 [UI建立架構的教學課程](../../xdm/tutorials/create-schema-ui.md)。

![](../images/merge-policies/custom-timestamp-mixin.png)

若要使用API使用自訂時間戳記，請參閱「合 [並原則端點指南」中的「使用自訂時間戳記」一節](../api/merge-policies.md#custom-timestamps)。

### 資料集優先順序 {#dataset-precedence}

當選 **[!UICONTROL 擇「資料集優先]** 」作為合併策略的合併方法時，您可以根據個人資料片段的來源資料集，為其指定優先順序。 例如，如果貴組織在一個資料集中顯示的資訊比另一個資料集中的資料更偏好或受信任，則使用案例會是範例。

為了使用資料集優先順序建立合併策略 ****，必須選擇包含的Profile和ExperienceEvent資料集，然後可以手動為Profile資料集排序優先順序。 在選取並排序資料集後，最高優先順序的資料集會優先順序最高，第二個資料集會排在第二位，依此類推。

## [!UICONTROL ID拼接] {#id-stitching}

身分拼接([!UICONTROL ID拼接])是識別資料片段並將它們組合起來形成完整描述檔記錄的過程。 為了說明不同的聯繫行為，請考慮使用兩個不同電子郵件地址與品牌互動的單一客戶。

* **[!UICONTROL 無]:** 選取此選項時，ID將不會銜接在一起。 當區段發生時，屬於同一人的身分識別將不會銜接在一起，而區段只會在判斷客戶是否符合區段成員資格時考慮附加至每個個別ID的屬性。 這可能導致單一客戶擁有多個個人檔案，而每個個人檔案可符合不同細分的資格，導致多個行銷訊息被傳送給同一客戶。
* **[!UICONTROL 專用圖]:** 當選取私用圖形時，與同一個人相關的多個身份會銜接在一起。 這會導致客戶擁有單一描述檔，並允許區段在決定區段資格時考慮來自多個相關身分的多個屬性。 在此案例中，客戶可能擁有單一個人檔案、根據不同身分的屬性組合符合一個群體的資格，並且只會收到一則行銷訊息。

若要進一步瞭解身分及其在產生描述檔和區段中的角色，請先閱讀 [Identity Service總覽](../../identity-service/home.md)。

## 預設合併原則 {#default-merge-policy}

組織可以為其組織建立預設合併策略，以便在合併配置檔案片段時使用。 這可讓使用者在Experience Platform中執行動作（例如檢視客戶個人檔案或建立區段）時，輕鬆選取預設原則。 在大多數情況下，除非指定其他合併策略，否則將使用預設的合併策略。

每個組織都可以建立與單個XDM架構類相關的多個合併策略，但每個類只能聲明一個預設合併策略。 例如，您的組織可能具有與類相關的預設合併策略， [!DNL XDM Individual Profile] 以及自定義「產品庫存」類的不同預設合併策略。

如果您建立新的合併原則並將其設為預設，系統會自動更新先前的預設合併原則，使其不再為預設原則。

>[!WARNING]
>
>具有現有關聯預設合併原則的描述檔計數和區段可能會受到影響。 任何已套用預設合併原則的區段，都會更新為新的預設合併原則。

## 查看合併策略 {#view-merge-policies}

在 [!DNL Experience Platform] UI中，您可以開始使用合併原則，方法是在左側導覽中選取「描述檔」，然後選取「合 **[!UICONTROL 並原則」標籤]****** 。 此頁籤包含組織的所有現有合併策略的清單，以及每個合併策略的詳細資訊，包括策略名稱、合併策略是否為預設合併策略以及合併策略相關的方案類。

![合併策略登錄頁](../images/merge-policies/landing.png)

要選擇顯示哪些詳細資訊，或向顯示添加其他列，請選擇 **[!UICONTROL Configure columns]** ，然後按一下列名以添加或從視圖中刪除列。

![](../images/merge-policies/adjust-view.png)

## 建立合併策略 {#create-a-merge-policy}

要建立新的合併策略，請在合 **[!UICONTROL 並策略頁籤上]** ，選擇建立合併策略。

![合併策略登錄頁並突出顯示「建立」按鈕。](../images/merge-policies/create-new.png)

在「新 **[!UICONTROL 合併原則]** 」工作流程畫面中，您可以透過一系列引導步驟，為新的合併原則提供重要資訊。

![新的合併原則工作流程。](../images/merge-policies/create.png)

### [!UICONTROL 設定] {#configure}

工作流的第一步允許您通過提供基本資訊來配置合併策略。 這些資訊包括：

* **[!UICONTROL 名稱]**:合併策略的名稱應具有描述性，但應簡明扼要。
* **[!UICONTROL 架構類]**:與合併策略關聯的XDM模式類。 這指定為其建立此合併策略的方案類。 組織可以為每個方案類建立多個合併策略。 目前，UI中 [!UICONTROL 僅提供XDM個人設定檔類別] 。
* **[!UICONTROL ID拼接]**:此欄位定義如何確定客戶的相關身份。 請參閱本指南稍 [早的](#id-stitching) 「ID拼接」一節，瞭解更多資訊。 有兩個可能的值：
   * **[!UICONTROL 無]**:不執行身份聯繫。
   * **[!UICONTROL 專用圖]**:根據您的個人身分圖表執行身分識別接合。
* **[!UICONTROL 預設合併策略]**:切換按鈕，可讓您選擇此合併原則是否為您組織的預設原則。 如果選取器已開啟，則會出現警告，要求您確認您要變更組織的預設合併原則。 請參閱本指南稍 [早的預設合併原則](#default-merge-policy) 一節，瞭解更多資訊。
   ![](../images/merge-policies/create-make-default.png)

填寫完必要欄位後，您可以選取「下 **[!UICONTROL 一步]** 」繼續工作流程。

![完整的「設定」畫面，並反白顯示「下一個」按鈕。](../images/merge-policies/create-complete.png)

### [!UICONTROL 選擇配置檔案資料集] {#select-profile-datasets}

在「選 **[!UICONTROL 擇配置檔案資料集]** 」螢幕上，必須選擇要用於合 **[!UICONTROL 並策略的合併方法]** 。 此外，螢幕上還顯示了組織中與在上一個螢幕上選擇的架構類相關的  Profile資料集的總數。

根據您選擇的合併方法，所有配置檔案資料集將按上次更新的順序合併（按時間戳順序排列），或者您需要選擇合併策略中要包括的配置檔案資料集和合併它們的順序（資料集優先順序）。 有關合併方法的更多資訊，請參閱本文 [檔前面提供的](#merge-methods) 「合併方法」部分。

#### 排序時間戳記 {#timestamp-ordered-profile}

選擇 **[!UICONTROL Timestamp sordered作為合併方法]** ，表示最近更新資料集的屬性優先。 這適用於所有Profile資料集。

![](../images/merge-policies/timestamp-ordered.png)

#### 資料集優先順序 {#dataset-precedence-profile}

選擇 **[!UICONTROL 資料集優先順序]** (Dataset precerence)作為合併方法時，需要選擇配置檔案資料集並手動對其進行優先順序排序。 您可從資料集清單中選取最多50個資料集。 當選取資料集時，資料集會顯示在畫面的右側，讓您拖放資料集並排序。 當資料集在清單中調整時，資料集旁的序數（1、2、3等）會更新，顯示優先順序（1是最高優先順序，2接著再繼續）。

![](../images/merge-policies/dataset-precedence.png)

### [!UICONTROL 選擇ExperienceEvent資料集] {#select-experienceevent-datasets}

工作流程的下一個步驟需要您選取ExperienceEvent資料集。 此螢幕受您在「選擇配置檔案」資料集螢幕上選擇的合 [[!UICONTROL 並方法的影響]](#select-profile-datasets) 。

此螢幕上還顯示您的組織建立的與您在合併策略配置螢幕上選擇的架構類相關的 **** ExperienceEvent資料集總數。

#### 排序時間戳記 {#timestamp-ordered-experienceevent}

如果您選取 **[!UICONTROL Timestamp sordered]** （排序時間戳記）作為Profile資料集的合併方法，則最近更新的ExperienceEvent資料集的屬性也將優先於此。

![](../images/merge-policies/timestamp-experienceevent.png)

#### 資料集優先順序 {#dataset-precedence-experienceevent}

如果您選擇 **[!UICONTROL Dataset優先順序]** ，作為Profile資料集的合併方法，則需要選擇要包含的ExperienceEvent資料集。 您可以從資料集清單中選取最多50個ExperienceEvent資料集。 當選取資料集時，資料集會顯示在畫面的右側。 ExperienceEvent資料集無法手動排序，而ExperienceEvent資料集中的屬性會附加至Profile資料集（如果屬於相同的描述檔片段）。

![](../images/merge-policies/dataset-precedence-experienceevent.png)

### [!UICONTROL 評論] {#review}

工作流程的最後一個步驟是檢閱您的合併原則。 「 **[!UICONTROL Review]** 」螢幕顯示新合併策略的名稱、其所基於的架構類、您選擇的  ID拼接選項，以及合併方法和合併策略中包含的資料集。 若要檢視包含的所有Profile或ExperienceEvent資料集，請選取要展開下拉式清單的資料集數目。

請務必仔細檢查合併策略，然後再選擇「完 **[!UICONTROL 成]** 」以完成建立工作流。

#### 排序時間戳記 {#timestamp-ordered-review}

如果您為合併策略選擇了 **[!UICONTROL Timestamp sordered]** （排序的時間戳）作為合併方法，則Profile資料集清單將按照時間戳的順序包括由您的組織建立的與方案類相關的所有資料集。 ExperienceEvent資料集的清單包含貴組織為所選模式類別所建立的所有資料集，並會附加至描述檔資料集。

![](../images/merge-policies/timestamp-review.png)

#### 資料集優先順序 {#dataset-precedence-review}

如果您為合 **[!UICONTROL 並策略選擇了Dataset優先順序]** ，則Profile和ExperienceEvent資料集的清單僅包括您在建立工作流程中分別選擇的Profile和ExperienceEvent資料集。 配置檔案資料集的順序應與建立過程中指定的優先順序相匹配。 如果沒有，請使用「上 [!UICONTROL 一步] 」按鈕返回到前一個工作流步驟並調整優先順序。

![](../images/merge-policies/dataset-precedence-review.png)

### 更新合併原則清單 {#updated-list}

完成建立新合併策略的工作流後，將返回到「合 **[!UICONTROL 並策略]** 」頁籤。 您組織的合併原則清單現在應包含您剛建立的合併原則。

![](../images/merge-policies/new-merge-policy-created.png)

## 編輯合併原則

在「合 [!UICONTROL 並策略][!DNL XDM Individual Profile]**** 」頁籤中，通過為要編輯的合併策略選擇策略名稱，可以修改為類建立的現有合併策略。

![合併策略登錄頁](../images/merge-policies/select-edit.png)

出現「 **[!UICONTROL Edit merge policy]** (編輯合併策略 [!UICONTROL )」螢幕時，您可以更改名稱和]ID拼接，還可以更改此策略是否是組織的預設合併策略。

選擇 **[!UICONTROL 下一步]** ，繼續執行合併策略工作流以更新合併策略中包含的合併方法和資料集。

![](../images/merge-policies/edit-screen.png)

完成必要的更改後，請查看合併策略，然後選擇「完 **[!UICONTROL 成]** 」返回 **[!UICONTROL 「合併策略]** 」頁籤。

>[!WARNING]
>
>變更合併原則可能會影響區段和描述檔結果，因為這會改變資料衝突的解決方式。

![](../images/merge-policies/edit-review.png)

## 違反資料治理政策

建立或更新合併策略時，會執行檢查以確定合併策略是否違反您組織定義的任何資料使用策略。 資料使用政策是Adobe Experience Platform的一部分， [!DNL Data Governance] 是描述您可對特定資料執行或受限制之行銷動作類型的規 [!DNL Platform] 則。 例如，如果合併策略用於建立激活到第三方目標的段，而您的組織有阻止將特定資料導出到第三方的資料使用策略，則在嘗試保存合併策略時，您會收到檢測到的 **** Data governance策略違規通知。

此通知包括已違反的資料使用策略清單，允許您通過從清單中選擇策略來查看違規的詳細資訊。 在選擇違反的策略時，「資料世系 **** 」頁籤提供了違規的原因和受影響的激活，每個頁籤提供了有關違反資料使用策略的詳細資訊。

若要進一步瞭解如何在Adobe Experience Platform中執行資料治理，請先閱讀資料治 [理概觀](../../data-governance/home.md)。

![](../images/merge-policies/policy-violation.png)

## 後續步驟

現在，您已為組織建立並設定合併原則，您可以使用這些原則來調整平台中客戶個人檔案的檢視，並從個人檔案資料建立受眾細分。 如需如何 [使用UI和API建立和使用區段的詳細資訊](../../segmentation/home.md) ，請參閱區 [!DNL Experience Platform] 段概觀。