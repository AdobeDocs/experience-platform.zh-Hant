---
keywords: Experience Platform；首頁；熱門主題；啟用資料集；資料集；資料集
solution: Experience Platform
title: 資料集UI指南
description: 瞭解如何在Adobe Experience Platform使用者介面中使用資料集時執行常見動作。
exl-id: f0d59d4f-4ebd-42cb-bbc3-84f38c1bf973
source-git-commit: aee82356f1f519398f381e161be14789532561f1
workflow-type: tm+mt
source-wordcount: '2932'
ht-degree: 3%

---

# 資料集UI指南

本使用手冊提供在Adobe Experience Platform使用者介面中使用資料集時，執行常見動作的相關指示。

## 快速入門

本使用手冊需要您實際瞭解下列Adobe Experience Platform元件：

* [資料集](overview.md)：中資料持續性的儲存和管理結構 [!DNL Experience Platform].
* [[!DNL Experience Data Model (XDM) System]](../../xdm/home.md)：作為依據的標準化架構 [!DNL Experience Platform] 組織客戶體驗資料。
   * [結構描述組合基本概念](../../xdm/schema/composition.md)：瞭解XDM結構描述的基本建置區塊，包括結構描述組合中的關鍵原則和最佳實務。
   * [結構描述編輯器](../../xdm/tutorials/create-schema-ui.md)：瞭解如何使用建置您自己的自訂XDM結構描述 [!DNL Schema Editor] 在 [!DNL Platform] 使用者介面。
* [[!DNL Real-Time Customer Profile]](../../profile/home.md)：根據來自多個來源的彙總資料，提供統一的即時消費者個人檔案。
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

在 [!DNL Experience Platform] UI，選取 **[!UICONTROL 資料集]** 在左側導覽以開啟 **[!UICONTROL 資料集]** 儀表板。 控制面板會列出貴組織的所有可用資料集。 系統會顯示每個列出資料集的詳細資訊，包括其名稱、資料集所遵守的結構描述，以及最新擷取執行的狀態。

![Platform UI的資料集專案會在左側導覽列中反白顯示。](../images/datasets/user-guide/browse-datasets.png)

從中選擇資料集的名稱 [!UICONTROL 瀏覽] 標籤以存取其 **[!UICONTROL 資料集活動]** 畫面並檢視您選取之資料集的詳細資訊。 活動索引標籤包含將所使用訊息的比率視覺化的圖形，以及成功和失敗批次的清單。

![您所選資料集的量度和視覺效果會強調顯示。](../images/datasets/user-guide/dataset-activity-1.png)
![會反白顯示與您所選資料集相關的範例批次。](../images/datasets/user-guide/dataset-activity-2.png)

## 更多動作 {#more-actions}

您可以 [!UICONTROL 刪除] 或 [!UICONTROL 為設定檔啟用資料集] 從 [!UICONTROL 資料集] 詳細資料檢視。 若要檢視可用的動作，請選取 **[!UICONTROL ...更多]** （在UI的右上方）。 下拉式選單出現。

![具有的資料集工作區 [!UICONTROL ...更多] 下拉式功能表強調顯示。](../images/datasets/user-guide/more-actions.png)

如果您選取 **[!UICONTROL 為設定檔啟用資料集]**，則會顯示確認對話方塊。 選取 **[!UICONTROL 啟用]** 以確認您的選擇。

>[!NOTE]
>
>若要為設定檔啟用資料集，資料集堅持的結構必須相容以用於Real-Time Customer Profile。 請參閱 [為設定檔啟用資料集](#enable-profile) 區段以取得詳細資訊。

![啟用資料集確認對話方塊。](../images/datasets/user-guide/profile-enable-confirmation-dialog.png)

如果您選取 **[!UICONTROL 刪除]**，則 [!UICONTROL 刪除資料集] 確認對話方塊隨即顯示。 選取 **[!UICONTROL 刪除]** 以確認您的選擇。

>[!NOTE]
>
>您無法刪除系統資料集。

您也可以刪除資料集或新增資料集，以便用於「即時客戶個人檔案」，其來源為 [!UICONTROL 瀏覽] 標籤。 請參閱 [內嵌動作區段](#inline-actions) 以取得詳細資訊。

![刪除資料集確認對話方塊。](../images/datasets/user-guide/delete-confirmation-dialog.png)

## 內嵌資料集動作 {#inline-actions}

資料集UI現在為每個可用的資料集提供一組內嵌動作。 選取您要管理的資料集的省略符號(...)，在快顯功能表中檢視可用選項。 可用的動作包括； [[!UICONTROL 預覽資料集]](#preview)， [[!UICONTROL 管理資料和存取標籤]](#manage-and-enforce-data-governance)， [[!UICONTROL 啟用統一的設定檔]](#enable-profile)， [[!UICONTROL 管理標籤]](#add-tags)， [[!UICONTROL 移至資料夾]](#move-to-folders)、和 [[!UICONTROL 刪除]](#delete). 如需這些可用動作的詳細資訊，請參閱其各自的章節。

### 新增資料集標籤 {#add-tags}

新增自訂建立的標籤來組織資料集並改善搜尋、篩選和排序功能。 從 [!UICONTROL 瀏覽] 的標籤 [!UICONTROL 資料集] 在工作區中，選取您要管理的資料集省略符號，然後選取 **[!UICONTROL 管理標籤]** 下拉式選單中的。

![針對所選資料集反白顯示具有省略符號和「管理標籤」選項的「資料集」工作區的「瀏覽」索引標籤。](../images/datasets/user-guide/manage-tags.png)

此 [!UICONTROL 管理標籤] 對話方塊隨即顯示。 輸入簡短說明以建立自訂標籤，或從現有的標籤中選擇，以標籤您的資料集。 選取 **[!UICONTROL 儲存]** 以確認您的設定。

![管理標籤對話方塊中會反白顯示自訂標籤。](../images/datasets/user-guide/manage-tags-dialog.png)

此 [!UICONTROL 管理標籤] 對話方塊也可以從資料集中移除現有標籤。 只要選取您要移除之標籤旁的「x」，然後選取 **[!UICONTROL 儲存]**.

將標籤新增到資料集後，即可根據對應的標籤篩選資料集。 請參閱如何操作的區段 [依標籤篩選資料集](#enable-profile) 以取得詳細資訊。

如需如何分類商業物件以便輕鬆探索和分類的詳細資訊，請參閱以下指南中的 [管理中繼資料分類](../../administrative-tags/ui/managing-tags.md). 本指南詳細說明具有適當許可權的使用者如何建立預先定義的標籤、將類別指派給標籤，以及在Platform UI中執行標籤和標籤類別的所有相關CRUD作業。

## 搜尋和篩選資料集 {#search-and-filter}

若要搜尋或篩選可用資料集清單，請選取篩選圖示(![篩選圖示。](../images/datasets/user-guide/icon.png))。 左側邊欄中會顯示一組篩選器選項。 有幾種方法可篩選您的可用資料集。 這些功能包括： [[!UICONTROL 顯示系統資料集]](#show-system-datasets)， [[!UICONTROL 包含在設定檔中]](#filter-profile-enabled-datasets)， [[!UICONTROL 標籤]](#filter-by-tag)， [[!UICONTROL 建立日期]](#filter-by-creation-date)， [[!UICONTROL 修改日期]， [!UICONTROL 建立者]](#filter-by-creation-date)、和 [[!UICONTROL 結構描述]](#filter-by-schema).

套用的篩選器清單會顯示在篩選結果上方。

![「資料集」工作區的「瀏覽」索引標籤，其中反白顯示已套用篩選器的清單。](../images/datasets/user-guide/applied-filters.png)

### 顯示系統資料集 {#show-system-datasets}

依預設，只會顯示您擷取資料的資料集。 如果您想檢視系統產生的資料集，請選取 **[!UICONTROL 是]** 中的核取方塊 [!UICONTROL 顯示系統資料集] 區段。 系統產生的資料集僅用於處理其他元件。 例如，系統產生的設定檔匯出資料集可用來處理設定檔控制面板。

![使用的資料集工作區的篩選選項 [!UICONTROL 顯示系統資料集] 區段反白顯示。](../images/datasets/user-guide/show-system-datasets.png)

### 篩選設定檔啟用的資料集 {#filter-profile-enabled-datasets}

為設定檔資料啟用的資料集可在擷取資料後，用來填入客戶設定檔。 請參閱以下小節： [為設定檔啟用資料集](#enable-profile) 以進一步瞭解。

若要根據資料集是否已為設定檔啟用來篩選資料集，請選取 [!UICONTROL 是] 核取方塊。

![使用的資料集工作區的篩選選項 [!UICONTROL 包含在設定檔中] 區段反白顯示。](../images/datasets/user-guide/included-in-profile.png)

### 依標籤篩選資料集 {#filter-by-tag}

在「 」中輸入您的自訂標籤名稱 [!UICONTROL 標籤] 輸入，然後從可用選項清單中選取您的標籤，以搜尋和篩選與該標籤對應的資料集。

![使用的資料集工作區的篩選選項 [!UICONTROL 標籤] 反白顯示輸入和篩選圖示。](../images/datasets/user-guide/filter-tags.png)

### 依建立日期篩選資料集 {#filter-by-creation-date}

資料集可以在自訂時段內依建立日期進行篩選。 這可用來排除歷史資料，或產生依時間順序排列的資料深入分析和報表。 選擇 [!UICONTROL 開始日期] 和 [!UICONTROL 結束日期] 為每個欄位選取行事曆圖示。 之後，只有符合該條件的資料集才會出現在瀏覽標籤中。

### 依修改日期篩選資料集 {#filter-by-modified-date}

與建立日期的篩選類似，您可以根據資料集的上次修改日期來篩選資料集。 在 [!UICONTROL 修改日期] 區段，選擇 [!UICONTROL 開始日期] 和 [!UICONTROL 結束日期] 為每個欄位選取行事曆圖示。 之後，只有在該期間修改的資料集才會出現在瀏覽標籤中。

### 依結構描述篩選 {#filter-by-schema}

您可以根據定義資料集結構的結構來篩選資料集。 選取下拉式圖示或將結構描述名稱輸入文字欄位。 可能的相符專案清單隨即顯示。 從清單中選取適當的結構描述。

## 依建立日期排序資料集 {#sort}

中的資料集 [!UICONTROL 瀏覽] 索引標籤可依遞增或遞減日期排序。 選取 [!UICONTROL 已建立] 或 [!UICONTROL 上次更新時間] 欄標題在升序和降序之間切換。 選取後，欄會以向上或向下箭頭指向欄標題的側邊來指示此專案。

![「資料集」工作區的「瀏覽」索引標籤中，已建立和上次更新欄會反白顯示。](../images/datasets/user-guide/ascending-descending-columns.png)

## 預覽資料集 {#preview}

您可以預覽資料集範例資料，其來源為 [!UICONTROL 瀏覽] 標籤以及 [!UICONTROL 資料集活動] 檢視。 從 [!UICONTROL 瀏覽] 索引標籤中，選取您要預覽的資料集名稱旁邊的省略符號(...)。 選單清單中的選項隨即顯示。 接下來，選取 **[!UICONTROL 預覽資料集]** 從可用選項清單中選取。 如果資料集空白，預覽連結將會停用，並改為表示無法預覽。

![針對所選資料集反白顯示具有省略符號和預覽資料集選項的「資料集」工作區的「瀏覽」索引標籤。](../images/datasets/user-guide/preview-dataset-option.png)

這將會開啟預覽視窗，其中資料集的結構描述階層檢視會顯示在右側。

![隨即顯示資料集預覽對話方塊，其中包含資料集的結構相關資訊以及範例值。](../images/datasets/user-guide/preview-dataset.png)

或者，從 **[!UICONTROL 資料集活動]** 熒幕，選取 **[!UICONTROL 預覽資料集]** 靠近熒幕右上角，可預覽最多100列資料。

![預覽資料集按鈕會醒目提示。](../images/datasets/user-guide/select-preview.png)

如需存取資料的更強大方法， [!DNL Experience Platform] 提供下游服務，例如 [!DNL Query Service] 和 [!DNL JupyterLab] 以探索及分析資料。 如需詳細資訊，請參閱下列檔案：

* [查詢服務總覽](../../query-service/home.md)
* [JupyterLab使用手冊](../../data-science-workspace/jupyterlab/overview.md)

## 建立資料集 {#create}

若要建立新資料集，請從選取 **[!UICONTROL 建立資料集]** 在 **[!UICONTROL 資料集]** 儀表板。

![建立資料集按鈕會醒目提示。](../images/datasets/user-guide/select-create.png)

在下一個畫面中，畫面會顯示下列兩個建立新資料集的選項：

* [從結構描述建立資料集](#schema)
* [從CSV檔案建立資料集](#csv)

### 使用現有結構描述建立資料集 {#schema}

在 **[!UICONTROL 建立資料集]** 熒幕，選取 **[!UICONTROL 從結構描述建立資料集]** 以建立新的空白資料集。

![會醒目顯示「從結構描述建立資料集」按鈕。](../images/datasets/user-guide/create-dataset-schema.png)

此 **[!UICONTROL 選取結構描述]** 步驟隨即顯示。 瀏覽結構描述清單，並選取資料集將遵循的結構描述，然後再選取 **[!UICONTROL 下一個]**.

![隨即顯示結構描述清單。 將會用來建立資料集的結構描述會醒目提示。](../images/datasets/user-guide/select-schema.png)

此 **[!UICONTROL 設定資料集]** 步驟隨即顯示。 提供資料集的名稱和選擇性說明，然後選取「 」 **[!UICONTROL 完成]** 以建立資料集。

![已插入資料集的設定詳細資料。 這包括資料集名稱和說明等詳細資訊。](../images/datasets/user-guide/configure-dataset-schema.png)

可使用結構描述篩選器從UI中的可用資料集清單中篩選資料集。 請參閱如何操作的區段 [依結構描述篩選資料集](#filter-by-schema) 以取得詳細資訊。

### 使用CSV檔案建立資料集 {#csv}

使用CSV檔案建立資料集時，會建立臨時結構描述，為資料集提供符合所提供CSV檔案的結構。 在 **[!UICONTROL 建立資料集]** 熒幕，選取 **[!UICONTROL 從CSV檔案建立資料集]**.

![會醒目顯示「從CSV檔案建立資料集」按鈕。](../images/datasets/user-guide/create-dataset-csv.png)

此 **[!UICONTROL 設定]** 步驟隨即顯示。 提供資料集的名稱和選擇性說明，然後選取「 」 **[!UICONTROL 下一個]**.

![已插入資料集的設定詳細資料。 這包括資料集名稱和說明等詳細資訊。](../images/datasets/user-guide/configure-dataset-csv.png)

此 **[!UICONTROL 新增資料]** 步驟隨即顯示。 將CSV檔案拖放到熒幕中央或選取「 」，即可上傳該CSV檔案 **[!UICONTROL 瀏覽]** 以探索您的檔案目錄。 檔案大小最多可達10GB。 上傳CSV檔案後，選取「 」 **[!UICONTROL 儲存]** 以建立資料集。

>[!NOTE]
>
>CSV欄名稱的開頭必須為字母數字字元，並且只能包含字母、數字和底線。

![隨即顯示「新增資料」畫面。 上傳資料集CSV檔案的位置會醒目提示。](../images/datasets/user-guide/add-csv-data.png)

## 為即時客戶個人檔案啟用資料集 {#enable-profile}

每個資料集都能夠使用其擷取的資料擴充客戶設定檔。 要執行此操作，資料集所遵守的結構描述必須相容以用於 [!DNL Real-Time Customer Profile]. 相容的結構描述符合下列需求：

* 結構描述至少指定一個屬性做為身分屬性。
* 結構描述具有定義為主要身分的身分屬性。

如需為下列專案啟用結構的詳細資訊： [!DNL Profile]，請參閱 [結構描述編輯器使用手冊](../../xdm/tutorials/create-schema-ui.md).

您可以從以下兩個內嵌選項為設定檔啟用資料集： [!UICONTROL 瀏覽] 標籤以及 [!UICONTROL 資料集活動] 檢視。 從 [!UICONTROL 瀏覽] 的標籤 [!UICONTROL 資料集] 在工作區中，選取您要為設定檔啟用的資料集省略符號。 選單清單中的選項隨即顯示。 接下來，選取 **[!UICONTROL 啟用統一的設定檔]** 從可用選項清單中選取。

![資料集工作區的「瀏覽」索引標籤中會反白顯示省略符號和啟用統一的設定檔。](../images/datasets/user-guide/enable-for-profile.png)

或者，從資料集的 **[!UICONTROL 資料集活動]** 熒幕，選取 **[!UICONTROL 個人資料]** 在「 」內切換 **[!UICONTROL 屬性]** 欄。 啟用後，會使用擷取到資料集中的資料來填入客戶設定檔。

>[!NOTE]
>
>如果資料集已包含資料，且已啟用 [!DNL Profile]，現有的資料不會自動被 [!DNL Profile]. 為啟用資料集後 [!DNL Profile]，建議您重新內嵌任何現有資料，以貢獻給客戶設定檔。

![資料集詳細資訊頁面會醒目顯示設定檔切換按鈕。](../images/datasets/user-guide/enable-dataset-profiles.png)

已啟用設定檔的資料集也可依此條件篩選。 請參閱如何操作的區段 [篩選設定檔啟用的資料集](#filter-profile-enabled-datasets) 以取得詳細資訊。

## 管理和強制執行資料集的資料控管 {#manage-and-enforce-data-governance}

您可以選取「 」的內嵌選項，管理資料集的資料控管標籤。 [!UICONTROL 瀏覽] 標籤。 選取您要管理的資料集名稱旁的省略符號(...)，然後選取 **[!UICONTROL 管理資料和存取標籤]** 下拉式選單中的。

資料使用標籤（套用至結構描述層級）可讓您根據套用至該資料的使用原則來分類資料集和欄位。 請參閱 [資料控管概觀](../../data-governance/home.md) 以進一步瞭解標籤，或參閱 [資料使用標籤使用手冊](../../data-governance/labels/overview.md) 以取得如何套用標籤至結構描述，以傳播至資料集的指示。

## 移至資料夾 {#move-to-folders}

您可以將資料集放在資料夾中，以改善資料集管理。 若要將資料集移至資料夾，請選取您要管理的資料集名稱旁的省略符號(...)，然後選取 **[!UICONTROL 移至資料夾]** 下拉式選單中的。

![此 [!UICONTROL 資料集] 儀表板，帶有橢圓和 [!UICONTROL 移至資料夾] 反白顯示。](../images/datasets/user-guide/move-to-folder.png)

此 [!UICONTROL 移動] 資料集至資料夾對話方塊隨即顯示。 選取您要移動對象的資料夾，然後選取「 」 **[!UICONTROL 移動]**. 快顯通知會通知您資料集移動成功。

![此 [!UICONTROL 移動] 資料集對話方塊，使用 [!UICONTROL 移動] 反白顯示。](../images/datasets/user-guide/move-dialog.png)

>[!TIP]
>
>您也可以直接從「行動資料集」對話方塊建立資料夾。 若要建立資料夾，請選取建立資料夾圖示(![建立資料夾圖示。](../images/datasets/user-guide/create-folder-icon.png))。
>
>![此 [!UICONTROL 移動] 資料集對話方塊，其中的「建立資料夾」圖示會強調顯示。](/help/catalog/images/datasets/user-guide/create-folder.png)

資料集放入資料夾後，您可以選擇僅顯示屬於特定資料夾的資料集。 若要開啟資料夾結構，請選取顯示資料夾圖示(![顯示資料夾圖示](../images/datasets/user-guide/show-folders-icon.png))。 接著，選取您選擇的資料夾以檢視所有關聯的資料集。

![此 [!UICONTROL 資料集] 控制面板上會顯示資料集資料夾結構、顯示資料夾圖示，以及反白顯示的選定資料夾。](../images/datasets/user-guide/folder-structure.png)

## 刪除資料集 {#delete}

您可以從中的資料集內嵌動作刪除資料集 [!UICONTROL 瀏覽] 標籤或右上角 [!UICONTROL 資料集活動] 檢視。 從 [!UICONTROL 瀏覽] 檢視，選取您要刪除的資料集名稱旁邊的省略符號(...)。 選單清單中的選項隨即顯示。 接下來，選取 **[!UICONTROL 刪除]** 下拉式選單中的。

![針對所選資料集，具有省略符號和醒目提示刪除選項的資料集工作區的「瀏覽」索引標籤。](../images/datasets/user-guide/inline-delete-dataset.png)

確認對話方塊隨即顯示。 請選取「**[!UICONTROL 刪除]**」完成確認。

或者，選取 **[!UICONTROL 刪除資料集]** 從 **[!UICONTROL 資料集活動]** 畫面。

>[!NOTE]
>
>Adobe應用程式和服務(例如Adobe Analytics、Adobe Audience Manager或 [!DNL Offer Decisioning])無法刪除。

![「刪除資料集」按鈕在資料集詳細資訊頁面中會醒目提示。](../images/datasets/user-guide/delete-dataset.png)

確認方塊隨即顯示。 選取 **[!UICONTROL 刪除]** 以確認刪除資料集。

![系統會顯示刪除的確認強制回應視窗，並反白顯示「刪除」按鈕。](../images/datasets/user-guide/confirm-delete.png)

## 刪除啟用設定檔的資料集

如果已為設定檔啟用資料集，透過UI刪除該資料集將會從資料湖、身分服務和Platform內的設定檔存放區中刪除該資料集。

您可以從中刪除資料集 [!DNL Profile] 使用即時客戶個人檔案API僅儲存（將資料留在資料湖中）。 如需詳細資訊，請參閱 [設定檔系統作業API端點指南](../../profile/api/profile-system-jobs.md).

## 監視資料擷取

在 [!DNL Experience Platform] UI，選取 **[!UICONTROL 監視]** ，位於左側導覽器中。 此 **[!UICONTROL 監視]** 控制面板可讓您檢視批次或串流擷取的傳入資料狀態。 若要檢視個別批次的狀態，請選取 **[!UICONTROL 批次端對端]** 或 **[!UICONTROL 端對端串流]**. 控制面板會列出所有批次或串流擷取執行，包括成功、失敗或仍在進行的作業。 每個清單都提供批次的詳細資訊，包括批次ID、目標資料集的名稱和擷取的記錄數。 如果目標資料集已啟用 [!DNL Profile]，也會顯示內嵌的身分和設定檔記錄數。

![此時會顯示監控批次端對端畫面。 監視和批次對批次都會反白顯示。](../images/datasets/user-guide/batch-listing.png)

您可以選取個人 **[!UICONTROL 批次識別碼]** 以存取 **[!UICONTROL 批次總覽]** 控制面板和檢視批次的詳細資訊，包括批次擷取失敗時的錯誤記錄。

![所選批次的詳細資訊隨即顯示。 這包括擷取的記錄數、失敗的記錄數、批次狀態、檔案大小、擷取開始和結束時間、資料集和批次ID、組織ID、資料集名稱和存取資訊。](../images/datasets/user-guide/batch-overview.png)

如果要刪除批次，請選取 **[!UICONTROL 刪除批次]** 靠近控制面板右上角。 刪除批次也會從批次最初擷取的資料集中移除其記錄。

>[!NOTE]
>
>如果已為設定檔啟用並處理內嵌資料，則刪除批次不會從設定檔存放區中刪除該資料。

![資料集詳細資訊頁面會醒目顯示「刪除批次」按鈕。](../images/datasets/user-guide/delete-batch.png)

## 後續步驟

本使用手冊提供在中處理資料集時執行常見動作的指示。 [!DNL Experience Platform] 使用者介面。 有關執行常見問題的步驟 [!DNL Platform] 涉及資料集的工作流程，請參閱下列教學課程：

* [使用API建立資料集](create.md)
* [使用資料存取API查詢資料集資料](../../data-access/home.md)
* [使用API設定即時客戶個人檔案和身分服務的資料集](../../profile/tutorials/dataset-configuration.md)
