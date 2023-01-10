---
keywords: Experience Platform；首頁；熱門主題；同意和偏好設定；同意；onetrust;OneTrust
solution: Experience Platform
title: 使用UI中的「同意」和「首選項」源建立資料流
type: Tutorial
description: 資料流是一個排程任務，可從源中檢索資料並將資料內嵌到Platform資料集。 本教學課程提供如何使用Platform UI為同意和偏好設定來源建立資料流的步驟。
exl-id: 340b5945-baa1-4f79-88fa-2572606f6083
source-git-commit: ed92bdcd965dc13ab83649aad87eddf53f7afd60
workflow-type: tm+mt
source-wordcount: '1425'
ht-degree: 0%

---

# 使用UI中的同意和偏好設定來源建立資料流

資料流是一項排程任務，可從來源擷取資料，並內嵌至Adobe Experience Platform中的資料集。 本教學課程提供如何使用Platform UI為同意和偏好設定來源建立資料流的步驟。

>[!NOTE]
>
>若要建立資料流，您必須已擁有已驗證的帳戶，且 [!DNL OneTrust Integration] 來源。 請參閱 [建立 [!DNL OneTrust Integration] UI中的源連接](../../ui/create/consent-and-preferences/onetrust.md) 以取得更多資訊。

## 快速入門

本教學課程需要妥善了解Platform的下列元件：

* [來源](../../../home.md):Platform可讓您從各種來源擷取資料，同時能使用來建構、加上標籤，以及增強傳入資料 [!DNL Platform] 服務。
* [[!DNL Experience Data Model (XDM)] 系統](../../../../xdm/home.md):Experience Platform組織客戶體驗資料的標準化架構。
   * [結構構成基本概念](../../../../xdm/schema/composition.md):了解XDM結構描述的基本建置組塊，包括結構描述的主要原則和最佳實務。
   * [結構編輯器教學課程](../../../../xdm/tutorials/create-schema-ui.md):了解如何使用結構編輯器UI建立自訂結構。
* [[!DNL Real-Time Customer Profile]](../../../../profile/home.md):根據來自多個來源的匯總資料，提供統一的即時消費者設定檔。
* [[!DNL Data Prep]](../../../../data-prep/home.md):可讓資料工程師將資料對應、轉換及驗證至Experience Data Model(XDM)。

## 新增資料

建立同意和偏好設定來源帳戶後， **[!UICONTROL 新增資料]** 步驟，提供介面供您探索同意和偏好設定帳戶的表格階層。

* 介面的左半部是瀏覽器，顯示帳戶中包含的資料表格清單。 此介面也包含搜尋選項，可讓您快速識別您要使用的來源資料。
* 介面的右半部是預覽面板，可讓您預覽最多100列資料。

>[!NOTE]
>
>搜尋來源資料選項適用於除Adobe Analytics以外的所有以表格為基礎的來源。 [!DNL Amazon Kinesis]，和 [!DNL Azure Event Hubs].

找到源資料後，選擇表，然後選擇 **[!UICONTROL 下一個]**.

![select-data](../../../images/tutorials/dataflow/table-based/select-data.png)

## 提供資料流詳細資訊

此 [!UICONTROL 資料流詳細資訊] 頁面可讓您選取要使用現有資料集或新資料集。 在此程式中，您也可以為 [!UICONTROL 設定檔資料集], [!UICONTROL 錯誤診斷], [!UICONTROL 部分擷取]，和 [!UICONTROL 警報].

![dataflow detail](../../../images/tutorials/dataflow/table-based/dataflow-detail.png)

### 使用現有資料集

若要將資料內嵌至現有資料集，請選取 **[!UICONTROL 現有資料集]**. 您可以使用 [!UICONTROL 進階搜尋] 選項，或透過捲動下拉式選單中的現有資料集清單來執行。 選取資料集後，請提供資料流的名稱和說明。

![現有資料集](../../../images/tutorials/dataflow/table-based/existing-dataset.png)

### 使用新資料集

若要內嵌至新資料集，請選取 **[!UICONTROL 新資料集]** 然後提供輸出資料集名稱和選用說明。 接下來，使用 [!UICONTROL 進階搜尋] 選項，或透過捲動下拉式選單中的現有結構清單來執行。 選擇架構後，請為資料流提供名稱和說明。

![新資料集](../../../images/tutorials/dataflow/table-based/new-dataset.png)

### 啟用 [!DNL Profile] 診斷錯誤

下一步，選取 **[!UICONTROL 設定檔資料集]** 切換為啟用資料集 [!DNL Profile]. 這可讓您建立實體屬性和行為的整體檢視。 所有資料 [!DNL Profile]啟用的資料集將包含在 [!DNL Profile] 和更改會在保存資料流時應用。

[!UICONTROL 錯誤診斷] 為資料流中發生的任何錯誤記錄啟用詳細的錯誤消息生成，同時 [!UICONTROL 部分擷取] 可讓您內嵌包含錯誤的資料，最高可以是您手動定義的特定臨界值。 請參閱 [部分批次內嵌概觀](../../../../ingestion/batch-ingestion/partial.md) 以取得更多資訊。

![設定檔與錯誤](../../../images/tutorials/dataflow/table-based/profile-and-errors.png)

### 啟用警報

您可以啟用警報，以接收有關資料流狀態的通知。 從清單中選擇要訂閱的警報，以接收有關資料流狀態的通知。 如需警報的詳細資訊，請參閱 [使用UI訂閱來源警報](../alerts.md).

完成向資料流提供詳細資訊後，請選擇 **[!UICONTROL 下一個]**.

![警報](../../../images/tutorials/dataflow/table-based/alerts.png)

## 將資料欄位對應至XDM結構

>[!IMPORTANT]
>
>您無法將任何動態索引鍵組值對應為 [!DNL OneTrust] 至平台，且必須在目標架構中指定這些索引鍵，以便在擷取期間對應您的資料。

此 [!UICONTROL 對應] 步驟，提供您一個介面，將來源架構的來源欄位對應至目標架構中適當的目標XDM欄位。

Platform會根據您選取的目標結構或資料集，為自動對應欄位提供智慧型建議。 您可以手動調整對應規則以符合您的使用案例。 您可以視需要選擇直接映射欄位，或使用資料準備函式來轉換源資料，以導出計算值或計算值。 有關使用映射器介面和計算欄位的完整步驟，請參閱 [資料準備UI指南](../../../../data-prep/ui/mapping.md).

成功映射源資料後，請選擇 **[!UICONTROL 下一個]**.

![映射](../../../images/tutorials/dataflow/table-based/mapping.png)

## 排程擷取執行

此 [!UICONTROL 排程] 步驟，可讓您設定擷取排程，以使用已設定的對應自動擷取選取的來源資料。 預設情況下，排程設為 `Once`. 若要調整擷取頻率，請選取 **[!UICONTROL 頻率]** ，然後從下拉式功能表中選取選項。

>[!TIP]
>
>一次性擷取期間不會顯示間隔和回填。

![排程](../../../images/tutorials/dataflow/table-based/scheduling.png)

如果您將擷取頻率設為 `Minute`, `Hour`, `Day`，或 `Week`，則您必須設定間隔，以在每次擷取之間建立設定的時間範圍。 例如，擷取頻率設為 `Day` 和間隔設定為 `15` 表示資料流計畫每15天內嵌一次資料。

在此步驟中，您也可以啟用 **回填** 並定義資料增量擷取的欄。 回填可用來內嵌歷史資料，而您為增量內嵌定義的欄則可讓新資料與現有資料有所區別。

如需排程設定的詳細資訊，請參閱下表。

| 欄位 | 說明 |
| --- | --- |
| 頻率 | 擷取發生的頻率。 可選頻率包括 `Once`, `Minute`, `Hour`, `Day`，和 `Week`. |
| 間隔 | 設定所選頻率間隔的整數。 間隔的值應為非零整數，應設為大於或等於15。 |
| 開始時間 | UTC時間戳記，指出第一次擷取的設定何時發生。 開始時間必須大於或等於當前UTC時間。 |
| 回填 | 一個布林值，可決定最初擷取的資料。 如果啟用回填，則在首次排程擷取期間，會擷取指定路徑中所有目前的檔案。 如果停用回填，則只會擷取在首次擷取執行與開始時間之間載入的檔案。 在開始時間之前載入的檔案將不會被擷取。 |
| 載入增量資料的方式 | 具有類型、日期或時間的源架構欄位集的篩選選項。 此欄位可用來區分新資料和現有資料。 將根據所選欄的時間戳記擷取增量資料。 |

![回填](../../../images/tutorials/dataflow/table-based/backfill.png)

## 查看資料流

此 **[!UICONTROL 檢閱]** 步驟顯示，允許您在建立新資料流之前對其進行查看。 詳細資料會分組為下列類別：

* **[!UICONTROL 連線]**:顯示源類型、所選源檔案的相關路徑以及該源檔案中的列數。
* **[!UICONTROL 指派資料集和對應欄位]**:顯示要擷取來源資料的資料集，包括資料集所遵守的結構。
* **[!UICONTROL 排程]**:顯示擷取排程的作用中期間、頻率和間隔。

審核資料流後，請選擇 **[!UICONTROL 完成]** 並允許建立資料流的時間。

![審查](../../../images/tutorials/dataflow/table-based/review.png)

## 監視資料流

建立資料流後，您可以監視正在通過資料流進行內嵌的資料，以查看有關內嵌率、成功和錯誤的資訊。 有關如何監視資料流的詳細資訊，請參閱 [監視UI中的帳戶和資料流](../monitor.md).

## 刪除資料流

您可以刪除不再需要的資料流，或使用 **[!UICONTROL 刪除]** 函式 **[!UICONTROL 資料流]** 工作區。 有關如何刪除資料流的詳細資訊，請參閱 [刪除UI中的資料流](../delete.md).

## 後續步驟

依照本教學課程，您已成功建立資料流，將同意和偏好設定來源的資料匯入Platform。 下游現在可以使用傳入的資料 [!DNL Platform] 服務，例如 [!DNL Real-Time Customer Profile] 和 [!DNL Data Science Workspace]. 如需詳細資訊，請參閱下列檔案：

* [[!DNL Real-Time Customer Profile] 概覽](../../../../profile/home.md)
* [[!DNL Data Science Workspace] 概覽](../../../../data-science-workspace/home.md)


>[!WARNING]
>
> 下列影片中顯示的Platform UI已過期。 請參閱上述檔案，了解最新的UI螢幕擷取畫面和功能。
>
>[!VIDEO](https://video.tv.adobe.com/v/29711?quality=12&learn=on)
