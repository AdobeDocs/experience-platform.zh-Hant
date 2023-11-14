---
keywords: Experience Platform；首頁；熱門主題；行銷自動化聯結器
solution: Experience Platform
title: 在UI中使用行銷自動化來源建立資料流
type: Tutorial
description: 資料流是排程的工作，可擷取來源中的資料並將其擷取至Platform資料集。 本教學課程提供如何使用Platform UI為行銷自動化來源建立資料流的步驟。
exl-id: 8d31fc2d-b952-44f7-98e7-f51b0acc19ed
source-git-commit: 62ca31bc8499e822e0da25270bd4fe8871520f9b
workflow-type: tm+mt
source-wordcount: '1439'
ht-degree: 0%

---

# 在UI中使用行銷自動化來源建立資料流

資料流是排程的工作，可擷取來源中的資料並將資料擷取到Adobe Experience Platform中的資料集。 本教學課程提供如何使用Platform UI為行銷自動化來源建立資料流的步驟。

>[!NOTE]
>
>為了建立資料流，您必須擁有已驗證的帳戶，且帳戶具有行銷自動化來源。 在UI中建立不同行銷自動化來源帳戶的教學課程清單可在以下網址找到： [來源概觀](../../../home.md#marketing-automation).

## 快速入門

本教學課程需要您實際瞭解下列Platform元件：

* [來源](../../../home.md)：Platform可讓您從各種來源擷取資料，同時能夠使用來建構、加標籤及增強傳入資料 [!DNL Platform] 服務。
* [[!DNL Experience Data Model (XDM)] 系統](../../../../xdm/home.md)：Experience Platform組織客戶體驗資料的標準化架構。
   * [結構描述組合基本概念](../../../../xdm/schema/composition.md)：瞭解XDM結構描述的基本建置區塊，包括結構描述組合中的關鍵原則和最佳實務。
   * [結構描述編輯器教學課程](../../../../xdm/tutorials/create-schema-ui.md)：瞭解如何使用結構編輯器UI建立自訂結構描述。
* [[!DNL Real-Time Customer Profile]](../../../../profile/home.md)：根據來自多個來源的彙總資料，提供統一的即時消費者個人檔案。
* [[!DNL Data Prep]](../../../../data-prep/home.md)：可讓資料工程師對應、轉換及驗證與Experience Data Model (XDM)之間的資料。

## 新增資料

建立您的行銷自動化來源帳戶後， **[!UICONTROL 新增資料]** 步驟隨即顯示，為您提供介面，以便探索行銷自動化來源帳戶的表格階層。

* 介面的左半部分是瀏覽器，顯示帳戶中包含的資料表清單。 介面也包含搜尋選項，可讓您快速識別要使用的來源資料。
* 介面的右半部分是預覽面板，可讓您預覽最多100列的資料。

>[!NOTE]
>
>搜尋來源資料選項適用於除Adobe Analytics以外的所有表格來源。 [!DNL Amazon Kinesis]、和 [!DNL Azure Event Hubs].

找到來源資料後，請選取表格，然後選取 **[!UICONTROL 下一個]**.

![select-data](../../../images/tutorials/dataflow/table-based/select-data.png)

## 提供資料流詳細資料

此 [!UICONTROL 資料流詳細資料] 頁面可讓您選取要使用現有資料集還是新資料集。 在此程式中，您還可以配置以下專案的設定 [!UICONTROL 設定檔資料集]， [!UICONTROL 錯誤診斷]， [!UICONTROL 部分擷取]、和 [!UICONTROL 警報].

![資料流 — 詳細資料](../../../images/tutorials/dataflow/table-based/dataflow-detail.png)

### 使用現有的資料集

若要將資料內嵌至現有的資料集，請選取「 」 **[!UICONTROL 現有資料集]**. 您可以使用來擷取現有的資料集 [!UICONTROL 進階搜尋] 選項，或捲動下拉式選單中的現有資料集清單來進行分類。 選取資料集後，請為資料流提供名稱和說明。

![existing-data](../../../images/tutorials/dataflow/table-based/existing-dataset.png)

### 使用新資料集

若要擷取到新資料集中，請選取「 」 **[!UICONTROL 新資料集]** 然後提供輸出資料集名稱和選用的說明。 接下來，使用 [!UICONTROL 進階搜尋] 選項或捲動下拉式選單中的現有方案清單。 選取結構描述後，請為資料流提供名稱和說明。

![新資料集](../../../images/tutorials/dataflow/table-based/new-dataset.png)

### 啟用 [!DNL Profile] 和錯誤診斷

接下來，選取 **[!UICONTROL 設定檔資料集]** 切換以啟用您的資料集 [!DNL Profile]. 這可讓您建立實體屬性和行為的整體檢視。 來自所有人的資料 [!DNL Profile]啟用的資料集將包含在 [!DNL Profile] 和變更會在您儲存資料流時套用。

[!UICONTROL 錯誤診斷] 針對資料流中發生的任何錯誤記錄，啟用詳細的錯誤訊息產生，同時 [!UICONTROL 部分擷取] 可讓您擷取包含錯誤的資料，最多可擷取您手動定義的特定臨界值。 請參閱 [部分批次擷取概觀](../../../../ingestion/batch-ingestion/partial.md) 以取得詳細資訊。

![設定檔與錯誤](../../../images/tutorials/dataflow/table-based/profile-and-errors.png)

### 啟用警示

您可以啟用警報以接收有關資料流狀態的通知。 從清單中選取警報以訂閱接收有關資料流狀態的通知。 如需警示的詳細資訊，請參閱以下指南： [使用UI訂閱來源警報](../alerts.md).

當您完成提供詳細資訊給資料流時，請選取「 」 **[!UICONTROL 下一個]**.

![警報](../../../images/tutorials/dataflow/table-based/alerts.png)

## 將資料欄位對應至XDM結構描述

此 [!UICONTROL 對應] 步驟隨即顯示，為您提供介面，用於將來源結構描述中的來源欄位對應到目標結構描述中適當的目標XDM欄位。

Platform會根據您選取的目標結構或資料集，為自動對應的欄位提供智慧型建議。 您可以手動調整對應規則以符合您的使用案例。 您可以根據自己的需求，選擇直接對應欄位，或使用資料準備函式來轉換來源資料，以衍生計算或計算的值。 如需使用對應程式介面和計算欄位的完整步驟，請參閱 [資料準備UI指南](../../../../data-prep/ui/mapping.md).

成功對應來源資料後，請選取 **[!UICONTROL 下一個]**.

![對應](../../../images/tutorials/dataflow/table-based/mapping.png)

## 排程內嵌執行

此 [!UICONTROL 正在排程] 步驟隨即顯示，可讓您設定擷取排程，以使用已設定的對應自動擷取選取的來源資料。 根據預設，排程設定為 `Once`. 若要調整您的擷取頻率，請選取 **[!UICONTROL 頻率]** ，然後從下拉式選單中選取選項。

>[!TIP]
>
>在一次性內嵌期間看不到間隔和回填。

![排程](../../../images/tutorials/dataflow/table-based/scheduling.png)

如果您將擷取頻率設為 `Minute`， `Hour`， `Day`，或 `Week`，則您必須設定間隔，以建立每次擷取之間的設定時間範圍。 例如，擷取頻率設為 `Day` 而間隔設為 `15` 表示您的資料流已排程每15天擷取一次資料。

在此步驟中，您也可以啟用 **回填** 和定義資料增量內嵌欄。 回填是用來擷取歷史資料，而您為增量擷取定義的欄則可區分新資料與現有資料。

請參閱下表以取得排程設定的詳細資訊。

| 欄位 | 說明 |
| --- | --- |
| 頻率 | 內嵌發生的頻率。 可選取的頻率包括 `Once`， `Minute`， `Hour`， `Day`、和 `Week`. |
| 間隔 | 設定所選頻率間隔的整數。 間隔值應為非零整數，且應設定為大於或等於15。 |
| 開始時間 | UTC時間戳記，指出第一次擷取設定的時間。 開始時間必須大於或等於您目前的UTC時間。 |
| 回填 | 布林值，決定最初擷取的資料。 如果已啟用回填，則會在第一次排程擷取期間擷取指定路徑中的所有目前檔案。 如果停用回填，則只會擷取在第一次內嵌執行到開始時間之間載入的檔案。 將不會擷取在開始時間之前載入的檔案。 |
| 載入增量資料者： | 一個選項，其中包含一組型別、日期或時間的篩選來源結構描述欄位。 您為選取的欄位 **[!UICONTROL 載入增量資料者：]** 必須具有UTC時區的日期時間值，才能正確載入增量資料。 所有以表格為基礎的批次來源都會挑選增量資料，方法是比較差異欄時間戳記值與對應的流程執行視窗UTC時間，然後複製來源中的資料（如果在UTC時間視窗中找到任何新資料）。 |

![回填](../../../images/tutorials/dataflow/table-based/backfill.png)

## 檢閱您的資料流

此 **[!UICONTROL 檢閱]** 步驟隨即顯示，可讓您在建立新資料流之前對其進行檢閱。 詳細資料會分組到以下類別中：

* **[!UICONTROL 連線]**：顯示來源型別、所選來源檔案的相關路徑，以及該來源檔案中的欄數。
* **[!UICONTROL 指派資料集並對映欄位]**：顯示要將來源資料擷取到哪個資料集中，包括資料集所堅持的結構描述。
* **[!UICONTROL 正在排程]**：顯示擷取排程的作用中期間、頻率和間隔。

檢閱資料流後，選取「 」 **[!UICONTROL 完成]** 並留出一些時間建立資料流。

![評論](../../../images/tutorials/dataflow/table-based/review.png)

## 監視資料流

建立資料流後，您可以監視透過該資料流擷取的資料，以檢視擷取率、成功和錯誤的資訊。 如需如何監視資料流的詳細資訊，請參閱以下教學課程： [在UI中監視帳戶和資料流](../monitor.md).

## 刪除您的資料流

您可以刪除不再需要的資料流，或是使用建立的資料流不正確。 **[!UICONTROL 刪除]** 函式位於 **[!UICONTROL 資料流]** 工作區。 如需如何刪除資料流程的詳細資訊，請參閱以下教學課程： [在UI中刪除資料流](../delete.md).

## 後續步驟

依照本教學課程中的指示，您已成功建立資料流，將資料從行銷自動化來源帶入Platform。 下游現在可以使用傳入的資料 [!DNL Platform] 服務，例如 [!DNL Real-Time Customer Profile] 和 [!DNL Data Science Workspace]. 如需更多詳細資訊，請參閱下列檔案：

* [[!DNL Real-Time Customer Profile] 概覽](../../../../profile/home.md)
* [[!DNL Data Science Workspace] 概覽](../../../../data-science-workspace/home.md)


>[!WARNING]
>
> 下列影片中顯示的Platform UI已過期。 請參閱上述檔案，瞭解最新的UI熒幕擷取畫面及功能。
>
>[!VIDEO](https://video.tv.adobe.com/v/29711?quality=12&learn=on)