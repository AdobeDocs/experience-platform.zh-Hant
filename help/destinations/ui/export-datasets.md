---
title: （測試版）將資料集匯出至雲端儲存目的地
type: Tutorial
description: 了解如何將資料集從Adobe Experience Platform匯出至您偏好的雲端儲存空間位置。
source-git-commit: 92e2d575d92b9d412f473610fc149663e815f5c3
workflow-type: tm+mt
source-wordcount: '1252'
ht-degree: 1%

---

# （測試版）將資料集匯出至雲端儲存目標

>[!IMPORTANT]
>
>* 匯出資料集的功能目前為測試版，不適用於所有使用者。 文件和功能可能會有所變更。
>* 此測試版功能支援匯出第一代資料(如Real-time Customer Data Platform中所定義) [產品說明](https://helpx.adobe.com/legal/product-descriptions/real-time-customer-data-platform-b2c-edition-prime-and-ultimate-packages.html).
>* 已購買Real-Time CDP Prime和Ultimate套件的客戶可使用此功能。 如需詳細資訊，請連絡您的Adobe代表。


本文說明匯出所需的工作流程 [資料集](/help/catalog/datasets/overview.md) 從Adobe Experience Platform移至您偏好的雲端儲存空間位置，例如 [!DNL Amazon S3]、SFTP位置，或 [!DNL Google Cloud Storage].

## 何時啟用區段或匯出資料集 {#when-to-activate-segments-or-activate-datasets}

Experience Platform目錄中有些以檔案為基礎的目的地支援區段啟動和資料集匯出。

* 想要將資料結構化為依讀者興趣或資格分組的設定檔時，請考慮啟用區段。
* 或者，當您想要匯出原始資料集時，可考慮匯出資料集，這些資料集不會依對象興趣或資格進行分組或結構化。 您可以將此資料用於報告、資料科學工作流程、滿足法規遵從性要求以及許多其他使用案例。

本檔案包含匯出資料集所需的所有資訊。 如果您想要將區段啟用至雲端儲存空間或電子郵件行銷目的地，請參閱 [啟用受眾資料以批次設定檔匯出目的地](/help/destinations/ui/activate-batch-profile-destinations.md).

## 先決條件 {#prerequisites}

若要將資料集匯出至雲端儲存目的地，您必須成功 [連接到目的地](./connect-destination.md). 如果尚未這麼做，請前往 [目的地目錄](../catalog/overview.md)，瀏覽支援的目的地，並設定您要使用的目的地。

### 必要權限 {#permissions}

若要匯出資料集，您需要 **[!UICONTROL 管理目的地]**, **[!UICONTROL 檢視目的地]**, **[!UICONTROL 啟動目的地]**，和 **[!UICONTROL 管理和啟用資料集目的地]** [存取控制權限](/help/access-control/home.md#permissions). 閱讀 [存取控制概觀](/help/access-control/ui/overview.md) 或聯絡您的產品管理員以取得所需的權限。

若要確保您擁有匯出資料集的必要權限，且目的地支援匯出資料集，請瀏覽目的地目錄。 如果目的地有 **[!UICONTROL 啟動]** 或 **[!UICONTROL 匯出資料集]** 控制，則您擁有適當的權限。

## 選取您的目的地 {#select-destination}

依照指示選取可匯出資料集的目的地：

1. 前往 **[!UICONTROL 連線>目的地]**，然後選取 **[!UICONTROL 目錄]** 標籤。

   ![目標目錄頁簽，並突出顯示目錄控制項。](/help/destinations/assets/ui/export-datasets/catalog-tab.png)

1. 選擇 **[!UICONTROL 啟動]** 或 **[!UICONTROL 匯出資料集]** 在與您要匯出資料集的目的地對應的卡片上。

   ![「激活」控制項的目標目錄頁簽突出顯示。](/help/destinations/assets/ui/export-datasets/activate-button.png)

1. 選擇 **[!UICONTROL 資料類型資料集]** ，然後選取要匯出資料集的目標連線，然後選取 **[!UICONTROL 下一個]**.

>[!TIP]
> 
>如果要設定要匯出資料集的新目的地，請選取 **[!UICONTROL 配置新目標]** 觸發 [連接到目標](/help/destinations/ui/connect-destination.md) 工作流程。

![以「資料集」控制項強調顯示目標啟動工作流程。](/help/destinations/assets/ui/export-datasets/select-datatype-datasets.png)

1. 此 **[!UICONTROL 選取資料集]** 視圖。 前往下一節，以 [選取資料集](#select-datasets) ，以匯出。

## 選取資料集 {#select-datasets}

使用資料集名稱左側的核取方塊，選取您要匯出至目的地的資料集，然後選取 **[!UICONTROL 下一個]**.

![資料集匯出工作流程，顯示「選取資料集」步驟，您可在此選取要匯出的資料集。](/help/destinations/assets/ui/export-datasets/select-datasets.png)

## 排程資料集匯出 {#scheduling}

在 **[!UICONTROL 排程]** 步驟中，您可以為資料集匯出設定開始日期和匯出順序。

此 **[!UICONTROL 導出增量檔案]** 選項。 這會觸發匯出，第一個檔案是資料集的完整快照，後續檔案是自上次匯出以來資料集的增量新增項目。

>[!IMPORTANT]
>
>第一個匯出的增量檔案包含資料集中的所有現有資料，可作為回填。

![顯示排程步驟的資料集匯出工作流程。](/help/destinations/assets/ui/export-datasets/export-incremental-datasets.png)

1. 使用 **[!UICONTROL 頻率]** 選取器以選取匯出頻率：

   * **[!UICONTROL 每日]**:在您指定的時間，每天安排一次增量檔案導出。
   * **[!UICONTROL 每小時]**:每3、6、8或12小時計畫增量檔案導出。

2. 使用 **[!UICONTROL 時間]** 選取器以選擇一天中的時間，位於 [!DNL UTC] 格式，導出時間。

3. 使用 **[!UICONTROL 日期]** 選取器，以選擇應進行匯出的間隔。 請注意，在測試版功能中，無法設定匯出的結束日期。 如需詳細資訊，請檢視 [已知限制](#known-limitations) 區段。

4. 選擇 **[!UICONTROL 下一個]** 保存計畫並繼續到 **[!UICONTROL 檢閱]** 步驟。

>[!NOTE]
> 
>針對資料集匯出，檔案名稱具有無法修改的預設格式。 請參閱 [驗證資料集匯出是否成功](#verify) 以取得詳細資訊和匯出檔案的範例。

## 檢閱 {#review}

在 **[!UICONTROL 檢閱]** 頁面，您可以看到您所選內容的摘要。 選擇 **[!UICONTROL 取消]** 來分解流， **[!UICONTROL 返回]** 修改設定，或 **[!UICONTROL 完成]** 確認選取項目並開始將資料集匯出至目的地。

![顯示審核步驟的資料集匯出工作流程。](/help/destinations/assets/ui/export-datasets/review.png)

## 驗證資料集匯出是否成功 {#verify}

匯出資料集時，Experience Platform會建立 `.json` 或 `.parquet` 檔案。 根據您提供的匯出排程，預期會在儲存位置中儲存新檔案。

Experience Platform會在您指定的儲存位置中建立資料夾結構，用於存放匯出的資料集檔案。 會依照下列模式，為每次匯出時間建立新資料夾：

`folder-name-you-provided/datasetID/exportTime=YYYYMMDDHHMM`

預設檔案名稱是隨機產生的，可確保匯出的檔案名稱是唯一的。

### 資料集檔案範例 {#sample-files}

這些檔案在您的儲存位置中是否存在，即表明是否成功匯出。 若要了解匯出的檔案的結構，您可以下載範例 [.parquet檔案](../assets/common/part-00000-tid-253136349007858095-a93bcf2e-d8c5-4dd6-8619-5c662e261097-672704-1-c000.parquet) 或 [.json檔案](../assets/common/part-00000-tid-4172098795867639101-0b8c5520-9999-4cff-bdf5-1f32c8c47cb9-451986-1-c000.json).

## 從目的地移除資料集 {#remove-dataset}

要從現有資料流中刪除資料集，請執行以下步驟：

1. 登入 [Experience PlatformUI](https://platform.adobe.com/) 選取 **[!UICONTROL 目的地]** 的下一頁。 選擇 **[!UICONTROL 瀏覽]** 從頂部標題查看現有目標資料流。

   ![顯示了目標連接的目標瀏覽視圖，其餘的模糊。](../assets/ui/export-datasets/browse-dataset-connections.png)

   >[!TIP]
   > 
   >選取篩選圖示 ![篩選器圖示](../assets/ui/edit-activation/filter.png) ，啟動排序面板。 排序面板會提供所有目的地的清單。 您可以從清單中選擇多個目標，以查看與所選目標關聯的資料流的篩選選擇。

1. 從 **[!UICONTROL 啟動資料]** 欄，選擇資料集控制項以查看映射到此導出資料流的所有資料集。

   ![可用的資料集導覽選項在「啟用資料」欄中反白顯示。](../assets/ui/export-datasets/go-to-datasets-data.png)

1. 此 **[!UICONTROL 啟動資料]** 頁面。 選擇 **[!UICONTROL 移除資料集]** ，觸發「移除資料集確認」對話方塊。

   ![移除右側邊欄中顯示「移除資料集」控制項的資料集對話方塊。](../assets/ui/export-datasets/remove-dataset-control.png)

1. 在確認對話方塊中，選取 **[!UICONTROL 移除]** 立即將資料集從匯出至目的地。

   ![顯示資料流中「確認資料集刪除」選項的對話框。](../assets/ui/export-datasets/remove-dataset-confirm.png)

## 已知限制 {#known-limitations}

請記得以下是資料集匯出測試版的限制：

* 目前只有單一權限(**[!UICONTROL 管理和啟用資料集目的地]**)，包括管理和啟用資料集目的地的權限。 這些控制項未來會分割為更精細的權限。 檢閱 [必要權限](#permissions) 區段，取得匯出資料集所需的完整權限清單。
* 目前，您只能匯出增量檔案，且無法為資料集匯出選取結束日期。
* 目前無法自訂匯出的檔案名稱。
* UI目前並未阻擋您刪除要匯出至目的地的資料集。 請勿刪除要匯出至目的地的任何資料集。 [移除資料集](#remove-dataset) 從目標資料流刪除資料流。
* 目前，資料集匯出的監控量度會與設定檔匯出的數字混合，因此不會反映真正的匯出數字。
