---
keywords: Experience Platform；首頁；熱門主題；啟用資料集；資料集；資料集
solution: Experience Platform
title: 資料集UI指南
description: 瞭解如何在Adobe Experience Platform使用者介面中使用資料集時執行常見動作。
exl-id: f0d59d4f-4ebd-42cb-bbc3-84f38c1bf973
source-git-commit: a168f61fabddd06d586f7909fd92c0409fd2f51e
workflow-type: tm+mt
source-wordcount: '3203'
ht-degree: 6%

---

# 資料集UI指南

本使用手冊提供在Adobe Experience Platform使用者介面中使用資料集時，執行常見動作的相關指示。

## 快速入門

本使用手冊需要您實際瞭解下列Adobe Experience Platform元件：

* [資料集](overview.md)： [!DNL Experience Platform]中資料持續性的儲存和管理建構。
* [[!DNL Experience Data Model (XDM) System]](../../xdm/home.md)： [!DNL Experience Platform]用來組織客戶體驗資料的標準化架構。
   * [結構描述組合的基本概念](../../xdm/schema/composition.md)：瞭解XDM結構描述的基本建置區塊，包括結構描述組合中的關鍵原則和最佳實務。
   * [結構描述編輯器](../../xdm/tutorials/create-schema-ui.md)：瞭解如何在[!DNL Platform]使用者介面中使用[!DNL Schema Editor]建置您自己的自訂XDM結構描述。
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
>title="資料集有效期"
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


在[!DNL Experience Platform] UI中，選取左側導覽中的&#x200B;**[!UICONTROL 資料集]**&#x200B;以開啟&#x200B;**[!UICONTROL 資料集]**&#x200B;儀表板。 控制面板會列出貴組織的所有可用資料集。 系統會顯示每個列出資料集的詳細資訊，包括其名稱、資料集所遵守的結構描述，以及最新擷取執行的狀態。

![在左側導覽列中反白顯示資料集專案的Platform UI。](../images/datasets/user-guide/browse-datasets.png)

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

* [[!UICONTROL 預覽資料集]](#preview)，
* [[!UICONTROL 管理資料並存取標籤]](#manage-and-enforce-data-governance)
* [[!UICONTROL 啟用統一的設定檔]](#enable-profile)
* [[!UICONTROL 管理標籤]](#manage-tags)
* [[!UICONTROL 移至資料夾]](#move-to-folders)
* [[!UICONTROL 刪除]](#delete)。

如需這些可用動作的詳細資訊，請參閱其各自的章節。 若要瞭解如何同時管理大量資料集，請參閱[大量動作](#bulk-actions)區段。

### 預覽資料集 {#preview}

您可以從[!UICONTROL 瀏覽]索引標籤的內嵌選項以及[!UICONTROL 資料集活動]檢視，預覽資料集範例資料。 從[!UICONTROL 瀏覽]索引標籤，選取您要預覽的資料集名稱旁的省略符號(...)。 選單清單中的選項隨即顯示。 接著，從可用選項清單中選取&#x200B;**[!UICONTROL 預覽資料集]**。 如果資料集空白，預覽連結將會停用，並改為表示無法預覽。

![資料集工作區的「瀏覽」索引標籤中，針對所選的資料集反白顯示省略符號和預覽資料集選項。](../images/datasets/user-guide/preview-dataset-option.png)

這將會開啟預覽視窗，其中資料集的結構描述階層檢視會顯示在右側。

>[!NOTE]
>
>檢視左側的架構圖表只會顯示包含資料的欄位。 沒有資料的欄位會自動隱藏，以簡化UI並專注於相關資訊。

![會顯示資料集預覽對話方塊，其中包含資料集的結構相關資訊以及範例值。](../images/datasets/user-guide/preview-dataset.png)

或者，從&#x200B;**[!UICONTROL 資料集活動]**&#x200B;畫面，選取畫面右上角附近的&#x200B;**[!UICONTROL 預覽資料集]**，以預覽最多100列的資料。

![預覽資料集按鈕已反白顯示。](../images/datasets/user-guide/select-preview.png)

若要以更穩健的方法存取您的資料，[!DNL Experience Platform]可提供下游服務，例如[!DNL Query Service]和[!DNL JupyterLab]，以探索和分析資料。 如需詳細資訊，請參閱下列檔案：

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

如需如何分類商業物件以便輕鬆探索和分類的詳細資訊，請參閱[管理中繼資料分類](../../administrative-tags/ui/managing-tags.md)的指南。 本指南詳細說明具有適當許可權的使用者如何建立預先定義的標籤、將類別指派給標籤，以及在Platform UI中執行標籤和標籤類別的所有相關CRUD作業。

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

依預設，只會顯示您擷取資料的資料集。 如果您想要檢視系統產生的資料集，請選取[!UICONTROL 顯示系統資料集]區段中的&#x200B;**[!UICONTROL 是]**&#x200B;核取方塊。 系統產生的資料集僅用於處理其他元件。 例如，系統產生的設定檔匯出資料集可用來處理設定檔控制面板。

![含有[!UICONTROL 顯示系統資料集]區段的資料集工作區的篩選選項已反白顯示。](../images/datasets/user-guide/show-system-datasets.png)

### 篩選設定檔啟用的資料集 {#filter-profile-enabled-datasets}

為設定檔資料啟用的資料集可在擷取資料後，用來填入客戶設定檔。 請參閱[為設定檔](#enable-profile)啟用資料集的相關小節以瞭解更多資訊。

若要根據資料集是否已為設定檔啟用來篩選資料集，請從篩選選項中選取[!UICONTROL 是]核取方塊。

![包含在設定檔]區段中的[!UICONTROL 資料集工作區的篩選選項已反白顯示。](../images/datasets/user-guide/included-in-profile.png)

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

此使用手冊提供在[!DNL Experience Platform]使用者介面中使用資料集時執行一般動作的指示。 如需執行涉及資料集的常見[!DNL Platform]工作流程的步驟，請參閱下列教學課程：

* [使用API建立資料集](create.md)
* [使用資料存取API查詢資料集資料](../../data-access/home.md)
* [使用API設定即時客戶個人檔案和身分服務的資料集](../../profile/tutorials/dataset-configuration.md)
