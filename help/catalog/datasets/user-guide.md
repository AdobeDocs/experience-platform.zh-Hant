---
keywords: Experience Platform；首頁；熱門主題；啟用資料集；資料集；資料集
solution: Experience Platform
title: 資料集UI指南
description: 瞭解如何在Adobe Experience Platform使用者介面中使用資料集時執行常見動作。
exl-id: f0d59d4f-4ebd-42cb-bbc3-84f38c1bf973
source-git-commit: 47cb1e9851a288961ecca01cf609b72342c58631
workflow-type: tm+mt
source-wordcount: '4551'
ht-degree: 5%

---

# 資料集UI指南

本使用手冊提供在Adobe Experience Platform使用者介面中使用資料集時，執行常見動作的相關指示。

## 快速入門

本使用手冊需要您實際瞭解下列Adobe Experience Platform元件：

* [資料集](overview.md)： [!DNL Experience Platform]中資料持續性的儲存和管理建構。
* [[!DNL Experience Data Model (XDM) System]](../../xdm/home.md)： [!DNL Experience Platform]用來組織客戶體驗資料的標準化架構。
   * [結構描述組合的基本概念](../../xdm/schema/composition.md)：瞭解XDM結構描述的基本建置區塊，包括結構描述組合中的關鍵原則和最佳實務。
   * [結構描述編輯器](../../xdm/tutorials/create-schema-ui.md)：瞭解如何在[!DNL Schema Editor]使用者介面中使用[!DNL Experience Platform]建置您自己的自訂XDM結構描述。
* [[!DNL Real-Time Customer Profile]](../../profile/home.md)：根據來自多個來源的彙總資料，提供統一的即時消費者設定檔。
* [[!DNL Adobe Experience Platform Data Governance]](../../data-governance/home.md)：確保遵守使用客戶資料的相關法規、限制和政策。

## 檢視資料集 {#view-datasets}

>[!CONTEXTUALHELP]
>id="platform_datasets_negative_numbers"
>title="資料集活動中的負數"
>abstract="擷取記錄中的負數表示使用者在選取的時間範圍內刪除了某些批次。"
>text="Learn more in documentation"

>[!CONTEXTUALHELP]
>id="platform_datasets_browse_daysRemaining"
>title="資料集期限"
>abstract="此欄表示目標資料集在自動到期之前剩餘的天數。"

>[!CONTEXTUALHELP]
>id="platform_datasets_browse_datalakeretention"
>title="資料湖保留"
>abstract="顯示每個資料集目前的保留原則。可在每個資料集的保留設定中修改此值。您只能設定 ExperienceEvent 資料集的保留時間。"

>[!CONTEXTUALHELP]
>id="platform_datasets_browse_profileretention"
>title="設定檔保留"
>abstract="顯示每個資料集目前的保留原則。可在每個資料集的保留設定中修改此值。您只能設定 ExperienceEvent 資料集的保留時間。"

>[!CONTEXTUALHELP]
>id="platform_datasets_datalakesettings_datasetretention"
>title="資料集保留"
>abstract="資料湖保留會針對不同服務中的資料儲存時間長度以及何時刪除資料等設定規則。此設定可確保遵循法規、管理儲存成本以及維護資料品質。"

>[!CONTEXTUALHELP]
>id="platform_datasets_orchestratedCampaigns_toggle"
>title="協調的行銷活動"
>abstract="啟用此切換按鈕，允許在 Adobe Journey Optimizer 協調的行銷活動中使用所選資料集。資料集必須使用關聯式結構描述，而且每個結構描述只能建立一個資料集。"

在[!DNL Experience Platform] UI中，選取左側導覽中的&#x200B;**[!UICONTROL 資料集]**&#x200B;以開啟&#x200B;**[!UICONTROL 資料集]**&#x200B;儀表板。 控制面板會列出貴組織的所有可用資料集。 系統會顯示每個列出資料集的詳細資料，包括其名稱、資料集所遵守的結構描述，以及最近一次擷取執行的狀態。

![Experience Platform UI的資料集專案在左側導覽列中反白顯示。](../images/datasets/user-guide/browse-datasets.png)

從[!UICONTROL 瀏覽]索引標籤中選取資料集名稱，以存取其&#x200B;**[!UICONTROL 資料集活動]**&#x200B;畫面，並檢視您選取的資料集詳細資料。 活動索引標籤包含將所使用訊息的比率視覺化的圖形，以及成功和失敗批次的清單。

![您所選取資料集的量度和視覺效果會強調顯示。](../images/datasets/user-guide/dataset-activity-1.png)
![與您選取的資料集相關的範例批次會反白顯示。](../images/datasets/user-guide/dataset-activity-2.png)

## 更多動作 {#more-actions}

您可以從[!UICONTROL 資料集]詳細資料檢視[!UICONTROL 刪除]或[!UICONTROL 啟用設定檔]的資料集。 若要檢視可用的動作，請選取&#x200B;**[!UICONTROL ...UI右上角的]**&#x200B;更多。 下拉式選單出現。

![具有[!UICONTROL 的資料集工作區……反白顯示更多]下拉式功能表。](../images/datasets/user-guide/more-actions.png)

如果您選取&#x200B;**[!UICONTROL 為設定檔]**&#x200B;啟用資料集，則會顯示確認對話方塊。 選取&#x200B;**[!UICONTROL 啟用]**&#x200B;以確認您的選擇。

>[!NOTE]
>
>若要為設定檔啟用資料集，資料集堅持的結構必須相容以用於Real-Time Customer Profile。 如需詳細資訊，請參閱[為設定檔](#enable-profile)啟用資料集。

![啟用資料集確認對話方塊。](../images/datasets/user-guide/profile-enable-confirmation-dialog.png)

如果您選取&#x200B;**[!UICONTROL 刪除]**，則會顯示[!UICONTROL 刪除資料集]確認對話方塊。 選取&#x200B;**[!UICONTROL 刪除]**&#x200B;以確認您的選擇。

>[!NOTE]
>
>您無法刪除系統資料集。

您也可以從[!UICONTROL 瀏覽]索引標籤上的內嵌動作中刪除資料集或新增要與即時客戶個人檔案一起使用的資料集。 如需詳細資訊，請參閱[內嵌動作區段](#inline-actions)。

![刪除資料集確認對話方塊。](../images/datasets/user-guide/delete-confirmation-dialog.png)

## 內嵌資料集動作 {#inline-actions}

資料集UI現在為每個可用的資料集提供一組內嵌動作。 選取您要管理的資料集的省略符號(...)，在快顯功能表中檢視可用選項。 可用的動作包括；

* [[!UICONTROL 預覽資料集]](#preview)
* [[!UICONTROL 管理資料並存取標籤]](#manage-and-enforce-data-governance)
* [[!UICONTROL 啟用統一的設定檔]](#enable-profile)
* [[!UICONTROL 管理標籤]](#manage-tags)
* [[!UICONTROL 設定資料保留原則]](#data-retention-policy)
* [[!UICONTROL 移至資料夾]](#move-to-folders)
* [[!UICONTROL 刪除]](#delete)。

如需這些可用動作的詳細資訊，請參閱其各自的章節。 若要瞭解如何同時管理大量資料集，請參閱[大量動作](#bulk-actions)區段。

### 預覽資料集 {#preview}

您可以從[!UICONTROL 瀏覽]索引標籤的內嵌選項以及[!UICONTROL 資料集活動]檢視，預覽資料集範例資料。 新的資料集預覽視窗已推出，並包含其他導覽和內容增強功能。

從[!UICONTROL 瀏覽]索引標籤，選取您要預覽的資料集名稱旁的省略符號(...)。 選項清單隨即顯示。 接著，從可用選項中選取[!UICONTROL 預覽資料集]。 如果資料集空白，預覽連結會停用，並指示預覽無法使用。

![資料集工作區的「瀏覽」索引標籤中，針對所選的資料集反白顯示省略符號和預覽資料集選項。](../images/datasets/user-guide/preview-dataset-option.png)

這樣會開啟預覽視窗，其中資料集的階層架構檢視會顯示在左側。

>[!NOTE]
>
>檢視左側的架構圖表只會顯示包含資料的欄位。 沒有資料的欄位會自動隱藏，以簡化UI並專注於相關資訊。

![會顯示資料集預覽對話方塊，其中包含資料集的結構相關資訊以及範例值。](../images/datasets/user-guide/preview-dataset.png)

或者，從&#x200B;**[!UICONTROL 資料集活動]**&#x200B;畫面，選取畫面右上角附近的&#x200B;**[!UICONTROL 預覽資料集]**，以預覽最多100列的資料。

![預覽資料集按鈕已反白顯示。](../images/datasets/user-guide/select-preview.png)

資料集預覽視窗提供簡化的介面，方便您探索及驗證資料集。

#### 資料集預覽視窗 {#dataset-preview-window}

下列動畫顯示資料集預覽視窗及其導覽和資料探索功能：

![顯示資料集預覽視窗的熒幕錄製。 記錄會醒目提示物件瀏覽器側邊欄、資料型別指示器、SQL查詢顯示和格式化資料表。](../images/datasets/user-guide/dataset-preview-demo.gif)

資料集預覽視窗包含：

* 左側物件瀏覽器側邊欄，用於導覽和篩選資料集欄位。
* 資料集結構中每個欄名稱旁顯示的資料型別指標，可用於快速insight。
* SQL查詢會顯示在視窗頂端，顯示用來產生資料集的查詢。
* 格式化表格檢視，最多可在右下角區域顯示100列，以有效檢閱資料。
* 資料Distiller使用者可直接導覽至「查詢編輯器」，並預先填入SQL查詢以供進一步探索或修改。

這些功能支援快速導覽、結構描述瞭解和透明資料集驗證。

從內嵌動作或&#x200B;**[!UICONTROL 資料集活動]**&#x200B;畫面選取[!UICONTROL 預覽資料集]以開啟預覽視窗。

>[!NOTE]
>
>預覽視窗會顯示最多100列的範例。 不含資料的欄位會從檢視中排除。

#### 進階查詢編輯器捷徑 {#query-editor-shortcut}

如果您的組織有Data Distiller授權，您可以直接從資料集預覽視窗存取進階查詢編輯器。

>[!AVAILABILITY]
>
>只有具備必要Data Distiller授權的使用者才能存取此功能。 如果您的組織沒有Data Distiller，則不會顯示[!UICONTROL 進階查詢編輯器]選項。

在預覽視窗的右上角選取&#x200B;**[!UICONTROL 進階查詢編輯器]**&#x200B;以開啟查詢編輯器。 目前的預覽查詢已預先載入，並準備好執行或進一步分析。

![資料集預覽視窗在右上角顯示進階查詢編輯器按鈕。](../images/datasets/user-guide/dataset-preview-advanced-query-editor.png)

此捷徑可讓您順暢地從預覽範例資料移至在Query Service中執行和修訂查詢，而不需要重新輸入SQL或內容。

如需其他資料存取和分析，請使用下游服務，例如[!DNL Query Service]和[!DNL JupyterLab]。 如需詳細資訊，請參閱下列檔案：

* [查詢服務總覽](../../query-service/home.md)
* [JupyterLab 使用手冊](../../data-science-workspace/jupyterlab/overview.md)

### 管理和強制執行資料集的資料控管 {#manage-and-enforce-data-governance}

您可以選取[!UICONTROL 瀏覽]標籤的內嵌選項，以管理資料集的資料控管標籤。 選取您要管理的資料集名稱旁的省略符號(...)，接著從下拉式選單中選取&#x200B;**[!UICONTROL 管理資料及存取標籤]**。

資料使用標籤（套用至結構描述層級）可讓您根據套用至該資料的使用原則來分類資料集和欄位。 請參閱[資料控管概觀](../../data-governance/home.md)以深入瞭解標籤，或參閱[資料使用標籤使用手冊](../../data-governance/labels/overview.md)，瞭解如何將標籤套用至結構描述，以傳播至資料集。

## 為即時客戶個人檔案啟用資料集 {#enable-profile}

每個資料集都能夠使用其擷取的資料擴充客戶設定檔。 若要這麼做，資料集所遵守的結構描述必須相容以用於[!DNL Real-Time Customer Profile]。 相容的結構描述符合下列需求：

* 結構描述至少指定一個屬性做為身分屬性。
* 結構描述具有定義為主要身分的身分屬性。

如需啟用[!DNL Profile]的結構描述的詳細資訊，請參閱[結構描述編輯器使用手冊](../../xdm/tutorials/create-schema-ui.md)。

您可以從[!UICONTROL 瀏覽]標籤的內嵌選項以及[!UICONTROL 資料集活動]檢視，為設定檔啟用資料集。 從[!UICONTROL 資料集]工作區的[!UICONTROL 瀏覽]索引標籤中，選取您要為設定檔啟用的資料集省略符號。 選單清單中的選項隨即顯示。 接著，從可用選項清單中選取&#x200B;**[!UICONTROL 啟用統一設定檔]**。

![資料集工作區的[瀏覽]索引標籤中會反白顯示省略符號和[啟用統一設定檔]。](../images/datasets/user-guide/enable-for-profile.png)

或者，從資料集的&#x200B;**[!UICONTROL 資料集活動]**&#x200B;畫面，選取&#x200B;**[!UICONTROL 屬性]**&#x200B;欄中的&#x200B;**[!UICONTROL 設定檔]**&#x200B;切換按鈕。 啟用後，會使用擷取到資料集中的資料來填入客戶設定檔。

>[!NOTE]
>
>如果資料集已包含資料，然後又為[!DNL Profile]啟用，則[!DNL Profile]不會自動使用現有的資料。 為[!DNL Profile]啟用資料集後，建議您重新內嵌任何現有資料，以使其貢獻給客戶設定檔。

![資料集詳細資訊頁面中會醒目顯示設定檔切換按鈕。](../images/datasets/user-guide/enable-dataset-profiles.png)

已啟用設定檔的資料集也可依此條件篩選。 如需詳細資訊，請參閱如何[篩選已啟用設定檔的資料集](#filter-profile-enabled-datasets)的章節。

### 管理資料集標籤 {#manage-tags}

新增自訂建立的標籤來組織資料集並改善搜尋、篩選和排序功能。 從[!UICONTROL 資料集]工作區的[!UICONTROL 瀏覽]索引標籤中，選取您要管理的資料集省略符號，接著從下拉式選單中選取&#x200B;**[!UICONTROL 管理標籤]**。

![資料集工作區的「瀏覽」索引標籤中，針對所選資料集反白顯示省略符號和「管理標籤」選項。](../images/datasets/user-guide/manage-tags.png)

[!UICONTROL 管理標籤]對話方塊就會顯示。 輸入簡短說明以建立自訂標籤，或從現有的標籤中選擇，以標籤您的資料集。 選取&#x200B;**[!UICONTROL 儲存]**&#x200B;以確認您的設定。

![反白顯示自訂標籤的「管理標籤」對話方塊。](../images/datasets/user-guide/manage-tags-dialog.png)

[!UICONTROL 管理標籤]對話方塊也可以從資料集中移除現有標籤。 只要選取您要移除之標籤旁的&#39;x&#39;，並選取&#x200B;**[!UICONTROL 儲存]**&#x200B;即可。

將標籤新增到資料集後，即可根據對應的標籤篩選資料集。 如需詳細資訊，請參閱如何[依標籤](#enable-profile)篩選資料集的章節。

如需如何分類商業物件以便輕鬆探索和分類的詳細資訊，請參閱[管理中繼資料分類](../../administrative-tags/ui/managing-tags.md)的指南。 本指南說明具有適當許可權的使用者如何在Experience Platform UI中建立預先定義的標籤、將其指派給類別，以及管理所有相關的CRUD作業。

### 設定資料保留原則 {#data-retention-policy}

使用[!UICONTROL 資料集]工作區的[!UICONTROL 瀏覽]索引標籤中的內嵌動作功能表，管理資料集到期日和保留設定。 您可以使用此功能來設定資料在資料湖和個人資料存放區中保留的時間長度。 到期日是根據資料擷取至Experience Platform的時間和您設定的保留期間而定。

>[!IMPORTANT]
>
>若要套用或更新ExperienceEvent資料集的保留規則，您的使用者角色必須包含&#x200B;**[!UICONTROL 管理資料集]**&#x200B;許可權。 此角色型存取控制可確保只有授權的使用者才能修改資料集保留設定。
>
>如需在Adobe Experience Platform中指派許可權的詳細資訊，請參閱[存取控制總覽](../../access-control/home.md#platform-permissions)。

>[!TIP]
>
>Data Lake會儲存未處理的原始資料（例如事件日誌、點按資料流資料和大量擷取的記錄），以供分析和處理。 設定檔存放區包含客戶可識別的資料，包括身分拼接事件和屬性資訊，以支援即時個人化和啟用。

若要設定保留期間，請選取資料集旁的省略符號，然後從下拉式選單中選取&#x200B;**[!UICONTROL 設定資料保留原則]**。

![資料集工作區的[瀏覽]索引標籤中，省略符號和[設定資料保留原則]選項已反白顯示。](../images/datasets/user-guide/set-data-retention-policy-dropdown.png)

[!UICONTROL 設定資料集保留]對話方塊就會顯示。 此對話方塊會顯示沙箱層級授權使用量度、資料集層級詳細資料和目前的資料保留設定。 這些量度會顯示與您的權益相較之下的使用量，並協助您評估資料集特定的儲存和保留設定。 量度包括資料集名稱、型別、設定檔啟用狀態，以及資料湖和設定檔存放區使用情況。

>[!NOTE]
>
>沙箱層級授權的資料湖儲存量度仍在開發中，可能不會顯示。 您可以在「授權使用情況」控制面板上找到授權使用量度的完整明細。 如需這些量度的說明，請參閱檔案。
<!-- replace this screenshot with a dataset that enabled unified profile so user can see the Profile TTL settings -->
![設定資料集保留對話方塊。](../images/datasets/user-guide/set-data-retention-dialog.png)

在資料保留設定對話方塊中設定您偏好的保留期間。 輸入數字，然後從下拉式選單中選取時間單位（天、月或年）。 您可以為Data Lake和Profile Service設定單獨的保留設定。

>[!NOTE]
> 
>資料湖的最短保留時間為30天。 設定檔服務的最短保留期間為一天。

為了支援透明度和監視，已為&#x200B;**最近**&#x200B;和&#x200B;**下一個**&#x200B;資料保留工作執行提供時間戳記。 時間戳記可協助您瞭解上次資料清理何時發生，以及排程下次清理的時間。

#### 儲存影響分析 {#storage-impact-insights}

若要開啟不同保留原則對儲存體影響的視覺預測，請選取&#x200B;**[!UICONTROL 檢視體驗事件資料分佈]**。

此圖表顯示目前所選資料集在不同保留期中的體驗事件分佈。 將游標停留在每個長條上，即可檢視在套用所選保留期間時將移除的精確記錄數。

您可以使用視覺預測來評估不同保留期間的影響，並做出明智的業務決策。 例如，如果您選取30天的保留期，而圖表顯示將會刪除60%的資料，您可以選擇延長保留期，以保留更多資料進行分析。

>[!NOTE]
>
>體驗事件分佈圖是所選資料集專屬的圖表，僅反映其資料。 它僅適用於儲存在Data Lake中的資料。

![顯示[設定資料保留]對話方塊及[體驗事件]分佈圖。](../images/datasets/user-guide/visual-forecast.png)

若您對組態感到滿意，請選取[儲存]，確認您的設定。**&#x200B;**

>[!IMPORTANT]
>
>套用資料保留規則後，任何超過到期值定義天數的資料都會永久刪除且無法復原。

設定保留設定後，請使用監視UI來確認系統已執行您的變更。 監控UI可集中檢視所有資料集的資料保留活動。 從該位置，您可以追蹤工作執行、檢閱刪除了多少資料，並確保您的保留原則如預期般運作。

若要探索保留原則如何套用至不同的服務，請參閱個人檔案中[體驗事件資料集保留的專用指南](../../profile/event-expirations.md)以及資料湖中[體驗事件資料集保留的專用指南](./experience-event-dataset-retention-ttl-guide.md)。 此可見度可支援治理、法規遵循及有效率的資料生命週期管理。

若要瞭解如何使用監視儀表板在Experience Platform UI中追蹤來源資料流，請參閱UI[檔案中的](../../dataflows/ui/monitor-sources.md)監視來源資料流。

<!-- Improve the link above. I cannot link to a 100% appropriate document yet. -->

如需定義資料集到期日範圍的規則，以及設定資料保留原則的最佳實務的詳細資訊，請參閱[常見問題頁面](../catalog-faq.md)。

#### 提升保留期和儲存量度的可見度 {#retention-and-storage-metrics}

四個新欄可讓您更清楚地瞭解資料管理： **[!UICONTROL 資料湖儲存]**、**[!UICONTROL 資料湖保留]**、**[!UICONTROL 設定檔儲存]**&#x200B;和&#x200B;**[!UICONTROL 設定檔保留]**。 這些量度會顯示您的資料在資料湖和設定檔服務中使用的儲存空間及其保留期。

如此提升的可見度，讓您能夠做出明智的決策，並更有效地管理儲存成本。 依儲存大小排序資料集，以識別目前沙箱中最大的資料集。 這些見解支援資料管理最佳實務，並幫助確保符合您的授權權益。

![資料集工作區的[瀏覽]索引標籤，其中四個新的儲存和保留資料行已反白顯示。](../images/datasets/user-guide/storage-and-retention-columns.png)

下表提供新保留率和儲存量度的概觀。 它詳細說明了每欄的用途，以及支援管理資料保留和儲存的方式。

| 欄標題 | 說明 |
|---|---|
| [!UICONTROL 資料湖保留] | 資料湖中每個資料集的目前保留期。 此值可設定，並決定在刪除之前保留資料的時間。 |
| [!UICONTROL 資料湖儲存空間] | Data Lake中每個資料集的目前儲存使用量。 使用此量度來管理儲存空間限制並最佳化使用量。 |
| [!UICONTROL 設定檔儲存空間] | 設定檔服務中每個資料集的目前儲存使用量。 協助監控儲存耗用量，並支援資料管理決策。 |
| [!UICONTROL 設定檔保留] | 設定檔資料集的目前保留期。 您可以更新此值以控制設定檔資料保留的時間長度。 |

{style="table-layout:auto"}

若要根據儲存和保留量度的深入分析採取行動，請參閱[資料管理授權權益最佳實務指南](../../landing/license-usage-and-guardrails/data-management-best-practices.md)。 用它來管理您擷取和保留的資料、套用篩選器和到期規則，以及控制資料成長，以保持在您的授權使用限制之內。

### 移至資料夾 {#move-to-folders}

您可以將資料集放在資料夾中，以改善資料集管理。 若要將資料集移至資料夾，請選取您要管理的資料集名稱旁的省略符號(...)，然後從下拉式選單中選取&#x200B;**[!UICONTROL 移至資料夾]**。

![含有橢圓形符號的[!UICONTROL 資料集]儀表板，並反白顯示[!UICONTROL 移至資料夾]。](../images/datasets/user-guide/move-to-folder.png)

[!UICONTROL 移動]資料集至資料夾對話方塊就會顯示。 選取您要移動對象的資料夾，然後選取&#x200B;**[!UICONTROL 移動]**。 快顯通知會通知您資料集移動成功。

![含有[!UICONTROL 移動]的[!UICONTROL 移動]資料集對話方塊已反白顯示。](../images/datasets/user-guide/move-dialog.png)

>[!TIP]
>
>您也可以直接從「行動資料集」對話方塊建立資料夾。 若要建立資料夾，請選取建立資料夾圖示(![建立資料夾圖示。](/help/images/icons/folder-add.png))。
>
>![反白顯示建立資料夾圖示的[!UICONTROL 移動]資料集對話方塊。](/help/catalog/images/datasets/user-guide/create-folder.png)

資料集放入資料夾後，您可以選擇僅顯示屬於特定資料夾的資料集。 若要開啟您的資料夾結構，請選取顯示資料夾圖示（![顯示資料夾圖示](/help/images/icons/rail-left.png)）。 接著，選取您選擇的資料夾以檢視所有關聯的資料集。

![資料集資料夾結構已顯示的[!UICONTROL 資料集]儀表板、顯示資料夾圖示，以及反白顯示的選取資料夾。](../images/datasets/user-guide/folder-structure.png)

### 刪除資料集 {#delete}

您可以從[!UICONTROL 瀏覽]索引標籤中的資料集內嵌動作或[!UICONTROL 資料集活動]檢視的右上角刪除資料集。 從[!UICONTROL 瀏覽]檢視中，選取您要刪除的資料集名稱旁的省略符號(...)。 選單清單中的選項隨即顯示。 接著，從下拉式功能表中選取&#x200B;**[!UICONTROL 刪除]**。

![資料集工作區的「瀏覽」索引標籤具有省略符號，並且所選資料集的「刪除」選項反白顯示。](../images/datasets/user-guide/inline-delete-dataset.png)

確認對話方塊隨即顯示。 請選取「**[!UICONTROL 刪除]**」完成確認。

或者，從&#x200B;**[!UICONTROL 資料集活動]**&#x200B;畫面中選取&#x200B;**[!UICONTROL 刪除資料集]**。

>[!NOTE]
>
>無法刪除由Adobe應用程式和服務(例如Adobe Analytics、Adobe Audience Manager或[!DNL Offer Decisioning])建立和使用的資料集。

![資料集詳細資訊頁面中會醒目顯示[刪除資料集]按鈕。](../images/datasets/user-guide/delete-dataset.png)

確認方塊隨即顯示。 選取&#x200B;**[!UICONTROL 刪除]**&#x200B;以確認刪除資料集。

![顯示刪除的確認強制回應視窗，並反白顯示[刪除]按鈕。](../images/datasets/user-guide/confirm-delete.png)

### 刪除啟用設定檔的資料集

如果設定檔已啟用資料集，透過UI刪除該資料集將會從資料湖、身分服務以及在設定檔存放區中刪除與該資料集相關聯的任何設定檔資料。

您可以使用即時客戶設定檔API，從[!DNL Profile]存放區中刪除與資料集相關聯的設定檔資料（將資料留在資料湖中）。 如需詳細資訊，請參閱[設定檔系統工作API端點指南](../../profile/api/profile-system-jobs.md)。

## 搜尋和篩選資料集 {#search-and-filter}

若要搜尋或篩選可用資料集清單，請選取篩選圖示(![篩選圖示。](/help/images/icons/filter.png))。 左側邊欄中會顯示一組篩選器選項。 有幾種方法可篩選您的可用資料集。 這些包括： [[!UICONTROL 顯示系統資料集]](#show-system-datasets)、[[!UICONTROL 包含在設定檔中]](#filter-profile-enabled-datasets)、[[!UICONTROL 標籤]](#filter-by-tag)、[[!UICONTROL 建立日期]](#filter-by-creation-date)、[[!UICONTROL 修改日期]、[!UICONTROL 建立者]](#filter-by-creation-date)以及[[!UICONTROL 結構描述]](#filter-by-schema)。

套用的篩選器清單會顯示在篩選結果上方。

![資料集工作區的[瀏覽]索引標籤，其中反白顯示套用的篩選器清單。](../images/datasets/user-guide/applied-filters.png)

### 顯示系統資料集 {#show-system-datasets}

依預設，只會顯示您擷取資料的資料集。 如果您想要檢視系統產生的資料集，請選取&#x200B;**[!UICONTROL 顯示系統資料集]**&#x200B;區段中的[!UICONTROL 是]核取方塊。 系統產生的資料集僅用於處理其他元件。 例如，系統產生的設定檔匯出資料集可用來處理設定檔控制面板。

![含有[!UICONTROL 顯示系統資料集]區段的資料集工作區的篩選選項已反白顯示。](../images/datasets/user-guide/show-system-datasets.png)

### 篩選設定檔啟用的資料集 {#filter-profile-enabled-datasets}

為設定檔資料啟用的資料集可在擷取資料後，用來填入客戶設定檔。 請參閱[為設定檔](#enable-profile)啟用資料集的相關小節以瞭解更多資訊。

若要根據資料集是否已為設定檔啟用來篩選資料集，請從篩選選項中選取[!UICONTROL 是]核取方塊。

![包含在設定檔[!UICONTROL 區段中的]資料集工作區的篩選選項已反白顯示。](../images/datasets/user-guide/included-in-profile.png)

### 依標籤篩選資料集 {#filter-by-tag}

在[!UICONTROL 標籤]輸入中輸入您的自訂標籤名稱，然後從可用選項清單中選取您的標籤，以搜尋和篩選與該標籤對應的資料集。

![含有[!UICONTROL 標籤]輸入和篩選圖示的資料集工作區的篩選選項。](../images/datasets/user-guide/filter-tags.png)

### 依建立日期篩選資料集 {#filter-by-creation-date}

資料集可以在自訂時段內依建立日期進行篩選。 這可用來排除歷史資料，或產生依時間順序排列的資料深入分析和報表。 選取每個欄位的行事曆圖示，以選擇[!UICONTROL 開始日期]和[!UICONTROL 結束日期]。 之後，只有符合該條件的資料集才會出現在瀏覽標籤中。

### 依修改日期篩選資料集 {#filter-by-modified-date}

與建立日期的篩選類似，您可以根據資料集的上次修改日期來篩選資料集。 在[!UICONTROL 修改日期]區段中，選取每個欄位的行事曆圖示，以選擇[!UICONTROL 開始日期]和[!UICONTROL 結束日期]。 之後，只有在該期間修改的資料集才會出現在瀏覽標籤中。

### 依結構描述篩選 {#filter-by-schema}

您可以根據定義資料集結構的結構來篩選資料集。 選取下拉式圖示或將結構描述名稱輸入文字欄位。 可能的相符專案清單隨即顯示。 從清單中選取適當的結構描述。

## 大量動作 {#bulk-actions}

使用大量動作來提升營運效率，以及同時對多個資料集執行多個動作。 您可以透過大量動作（例如[移至資料夾](#move-to-folders)、[編輯標籤](#manage-tags)和[刪除](#delete)資料集）來節省時間並維持有條理的資料結構。

若要一次對多個資料集執行動作，請以每列的核取方塊選取個別資料集，或選取含有欄標題核取方塊的整個頁面。 選取後，大量動作列隨即顯示。

![資料集瀏覽索引標籤中選取了許多資料集，且大量動作列反白顯示。](../images/datasets/user-guide/bulk-actions.png)

對資料集套用大量動作時，將會套用下列條件：

* 您可以從UI的不同頁面選取資料集。
* 如果您選取篩選器，選取的資料集將會重設。

## 依建立日期排序資料集 {#sort}

[!UICONTROL 瀏覽]索引標籤中的資料集可以依遞增或遞減日期排序。 選取[!UICONTROL 已建立]或[!UICONTROL 上次更新時間]欄標題，在升序與降序之間切換。 選取後，欄會以向上或向下箭頭指向欄標題的側邊來指示此專案。

![資料集工作區的[瀏覽]索引標籤，其中反白顯示已建立和上次更新的資料行。](../images/datasets/user-guide/ascending-descending-columns.png)

## 建立資料集 {#create}

若要建立新的資料集，請在&#x200B;**[!UICONTROL 資料集]**&#x200B;儀表板中選取&#x200B;**[!UICONTROL 建立資料集]**。

![已醒目提示[建立資料集]按鈕。](../images/datasets/user-guide/select-create.png)

在下一個畫面中，畫面會顯示下列兩個建立新資料集的選項：

* [從結構描述建立資料集](#schema)
* [從 CSV 檔案建立資料集](#csv)

### 使用現有結構描述建立資料集 {#schema}

在&#x200B;**[!UICONTROL 建立資料集]**&#x200B;畫面中，選取&#x200B;**[!UICONTROL 從結構描述建立資料集]**&#x200B;以建立新的空白資料集。

![[從結構描述建立資料集]按鈕已反白顯示。](../images/datasets/user-guide/create-dataset-schema.png)

**[!UICONTROL 選取結構描述]**&#x200B;步驟隨即顯示。 瀏覽結構描述清單，並選取資料集將遵循的結構描述，然後再選取&#x200B;**[!UICONTROL 下一步]**。

![顯示結構描述清單。 將用來建立資料集的結構描述已反白顯示。](../images/datasets/user-guide/select-schema.png)

**[!UICONTROL 設定資料集]**&#x200B;步驟隨即顯示。 提供資料集名稱及選擇性說明，然後選取&#x200B;**[!UICONTROL 完成]**&#x200B;以建立資料集。

![已插入資料集的組態詳細資料。 這包括資料集名稱和說明等詳細資料。](../images/datasets/user-guide/configure-dataset-schema.png)

可使用結構描述篩選器從UI中的可用資料集清單中篩選資料集。 如需詳細資訊，請參閱如何依結構描述[篩選資料集](#filter-by-schema)的章節。

### 使用CSV檔案建立資料集 {#csv}

使用CSV檔案建立資料集時，會建立臨時結構描述，為資料集提供符合所提供CSV檔案的結構。 在&#x200B;**[!UICONTROL 建立資料集]**&#x200B;畫面中，選取&#x200B;**[!UICONTROL 從CSV檔案建立資料集]**。

![「從CSV檔案建立資料集」按鈕會醒目提示。](../images/datasets/user-guide/create-dataset-csv.png)

**[!UICONTROL 設定]**&#x200B;步驟隨即顯示。 提供資料集名稱及選擇性說明，然後選取&#x200B;**[!UICONTROL 下一步]**。

![已插入資料集的組態詳細資料。 這包括資料集名稱和說明等詳細資料。](../images/datasets/user-guide/configure-dataset-csv.png)

**[!UICONTROL 新增資料]**&#x200B;步驟隨即顯示。 將CSV檔案拖放到熒幕中央上傳，或選取&#x200B;**[!UICONTROL 瀏覽]**&#x200B;以瀏覽您的檔案目錄。 檔案大小最多可達10GB。 上傳CSV檔案後，請選取&#x200B;**[!UICONTROL 儲存]**&#x200B;以建立資料集。

>[!NOTE]
>
>CSV欄名稱的開頭必須為字母數字字元，並且只能包含字母、數字和底線。

![顯示[新增資料]畫面。 您可以為資料集上傳CSV檔案的位置會醒目提示。](../images/datasets/user-guide/add-csv-data.png)

## 監視資料擷取

在[!DNL Experience Platform] UI中，選取左側導覽中的&#x200B;**[!UICONTROL 監視]**。 **[!UICONTROL 監視]**&#x200B;儀表板可讓您檢視來自批次或串流擷取的傳入資料狀態。 若要檢視個別批次的狀態，請選取&#x200B;**[!UICONTROL 批次端對端]**&#x200B;或&#x200B;**[!UICONTROL 串流端對端]**。 控制面板會列出所有批次或串流擷取執行，包括成功、失敗或仍在進行的作業。 每個清單都提供批次的詳細資訊，包括批次ID、目標資料集的名稱和擷取的記錄數。 如果為[!DNL Profile]啟用目標資料集，也會顯示擷取的身分和設定檔記錄數。

![顯示監控批次端對端畫面。 監視和批次對批次都會反白顯示。](../images/datasets/user-guide/batch-listing.png)

您可以選取個別&#x200B;**[!UICONTROL 批次ID]**&#x200B;以存取&#x200B;**[!UICONTROL 批次總覽]**&#x200B;儀表板，並檢視批次的詳細資料，包括批次擷取失敗時的錯誤記錄。

![顯示選取批次的詳細資料。 這包括擷取的記錄數、失敗的記錄數、批次狀態、檔案大小、擷取開始和結束時間、資料集和批次ID、組織ID、資料集名稱和存取資訊。](../images/datasets/user-guide/batch-overview.png)

如果您想要刪除批次，請選取儀表板右上角附近的&#x200B;**[!UICONTROL 刪除批次]**。 刪除批次也會從批次最初擷取的資料集中移除其記錄。

>[!NOTE]
>
>如果已為設定檔啟用並處理內嵌資料，則刪除批次不會從設定檔存放區中刪除該資料。

![資料集詳細資訊頁面會醒目顯示[刪除批次]按鈕。](../images/datasets/user-guide/delete-batch.png)

## 後續步驟

此使用手冊提供在[!DNL Experience Platform]使用者介面中使用資料集時執行一般動作的指示。 如需執行涉及資料集的常見[!DNL Experience Platform]工作流程的步驟，請參閱下列教學課程：

* [使用API建立資料集](create.md)
* [使用資料存取API查詢資料集資料](../../data-access/home.md)
* [使用API設定即時客戶個人檔案和身分服務的資料集](../../profile/tutorials/dataset-configuration.md)

