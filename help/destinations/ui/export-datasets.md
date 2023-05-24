---
title: (Beta)將資料集導出到雲儲存目標
type: Tutorial
description: 瞭解如何將資料集從Adobe Experience Platform導出到您首選的雲儲存位置。
exl-id: e89652d2-a003-49fc-b2a5-5004d149b2f4
source-git-commit: d0de642eb6118e6597925c12c76917ffa98c3a5a
workflow-type: tm+mt
source-wordcount: '1359'
ht-degree: 5%

---

# (Beta)將資料集導出到雲儲存目標

>[!IMPORTANT]
>
>* 導出資料集的功能當前處於Beta版中，並且不適用於所有用戶。 文件和功能可能會有所變更。
>* 此測試版功能支援第一代資料的導出，如Real-time Customer Data Platform所定義 [產品說明](https://helpx.adobe.com/legal/product-descriptions/real-time-customer-data-platform-b2c-edition-prime-and-ultimate-packages.html)。
>* 此功能可供購買了Real-Time CDPPrime和Ultimate包的客戶使用。 請聯繫您的Adobe代表以瞭解更多資訊。


本文說明了導出所需的工作流 [資料集](/help/catalog/datasets/overview.md) 從Adobe Experience Platform到您的首選雲儲存位置，如 [!DNL Amazon S3]、 SFTP位置，或 [!DNL Google Cloud Storage] 使用Experience PlatformUI。

您還可以使用Experience PlatformAPI導出資料集。 閱讀 [導出資料集API教程](/help/destinations/api/export-datasets.md) 的子菜單。

## 支援的目標 {#supported-destinations}

當前，您可以將資料集導出到螢幕快照中突出顯示並列出的雲儲存目標。

![支援資料集導出的目標](/help/destinations/assets/ui/export-datasets/destinations-supporting-dataset-exports.png)

* [[!DNL (Beta) Azure Data Lake Storage Gen2]](../../destinations/catalog/cloud-storage/adls-gen2.md)
* [[!DNL (Beta) Data Landing Zone]](../../destinations/catalog/cloud-storage/data-landing-zone.md)
* [[!DNL (Beta) Google Cloud Storage]](../../destinations/catalog/cloud-storage/google-cloud-storage.md)
* [[!DNL (Beta) Amazon S3]](../../destinations/catalog/cloud-storage/amazon-s3.md#changelog)
* [[!DNL (Beta) Azure Blob]](../../destinations/catalog/cloud-storage/azure-blob.md#changelog)
* [[!DNL (Beta) SFTP]](../../destinations/catalog/cloud-storage/sftp.md#changelog)

## 何時激活段或導出資料集 {#when-to-activate-segments-or-activate-datasets}

Experience Platform目錄中某些基於檔案的目標支援段激活和資料集導出。

* 在希望將資料結構化為按受眾興趣或資格分組的配置檔案時，請考慮激活資料段。
* 或者，在您要導出原始資料集時，請考慮資料集導出，這些原始資料集未按受眾興趣或資格進行分組或結構化。 您可以將此資料用於報告、資料科學工作流，以滿足法規遵從性要求和許多其他使用案例。

此文檔包含導出資料集所需的所有資訊。 如果要將段激活到雲儲存或電子郵件營銷目標，請閱讀 [將受眾資料激活到批配置檔案導出目標](/help/destinations/ui/activate-batch-profile-destinations.md)。

## 先決條件 {#prerequisites}

要將資料集導出到雲儲存目標，您必須已成功 [連接到目標](./connect-destination.md)。 如果尚未執行此操作，請轉至 [目標目錄](../catalog/overview.md)，瀏覽支援的目標，並配置要使用的目標。

### 必要權限 {#permissions}

要導出資料集，您需要 **[!UICONTROL 管理目標]**。 **[!UICONTROL 查看目標]**。 **[!UICONTROL 激活目標]**, **[!UICONTROL 管理和激活資料集目標]** [訪問控制權限](/help/access-control/home.md#permissions)。 閱讀 [訪問控制概述](/help/access-control/ui/overview.md) 或聯繫您的產品管理員以獲取所需權限。

要確保您具有導出資料集所需的權限，並且目標支援導出資料集，請瀏覽目標目錄。 如果目標具有 **[!UICONTROL 激活]** 或 **[!UICONTROL 導出資料集]** 控制項，則您具有相應的權限。

## 選擇目標 {#select-destination}

按照說明選擇可以導出資料集的目標：

1. 轉到 **[!UICONTROL 連接>目標]**，然後選擇 **[!UICONTROL 目錄]** 頁籤。

   ![「目標目錄」頁籤，「目錄」控制項突出顯示。](/help/destinations/assets/ui/export-datasets/catalog-tab.png)

1. 選擇 **[!UICONTROL 激活]** 或 **[!UICONTROL 導出資料集]** 在與要將資料集導出到的目標對應的卡上。

   ![「激活」控制項突出顯示的目標目錄頁籤。](/help/destinations/assets/ui/export-datasets/activate-button.png)

1. 選擇 **[!UICONTROL 資料類型資料集]** 選擇要將資料集導出到的目標連接，然後選擇 **[!UICONTROL 下一個]**。

>[!TIP]
> 
>如果要設定新目標以導出資料集，請選擇 **[!UICONTROL 配置新目標]** 觸發 [連接到目標](/help/destinations/ui/connect-destination.md) 工作流。

![突出顯示了資料集控制的目標激活工作流。](/help/destinations/assets/ui/export-datasets/select-datatype-datasets.png)

1. 的 **[!UICONTROL 選擇資料集]** 的上界。 繼續下一節， [選擇資料集](#select-datasets) 的下界。

## 選擇您的資料集 {#select-datasets}

使用資料集名稱左側的複選框選擇要導出到目標的資料集，然後選擇 **[!UICONTROL 下一個]**。

![資料集導出工作流，顯示「選擇資料集」步驟，您可以在其中選擇要導出的資料集。](/help/destinations/assets/ui/export-datasets/select-datasets.png)

## 計畫資料集導出 {#scheduling}

>[!CONTEXTUALHELP]
>id="platform_destinations_activate_datasets_exportoptions"
>title="資料集的檔案匯出選項"
>abstract="選取&#x200B;**匯出增量檔案**，僅匯出上次匯出後新增至資料集的資料。<br>第一個增量檔案匯出包括資料集中的所有資料，充當回填。未來的增量檔案僅包括第一次匯出後新增至資料集的資料。"

在 **[!UICONTROL 計畫]** 步驟，可以為資料集導出設定開始日期和導出節點。

的 **[!UICONTROL 導出增量檔案]** 選項。 這會觸發導出，其中第一個檔案是資料集的完整快照，而後續檔案是自上次導出以來對資料集的增量添加。

>[!IMPORTANT]
>
>第一個導出的增量檔案包括資料集中的所有現有資料，它們用作回填。

![顯示計畫步驟的資料集導出工作流。](/help/destinations/assets/ui/export-datasets/export-incremental-datasets.png)

1. 使用 **[!UICONTROL 頻率]** 選擇器以選擇導出頻率：

   * **[!UICONTROL 每日]**:在您指定的時間每天安排增量檔案導出一次。
   * **[!UICONTROL 每小時]**:計畫每3、6、8或12小時導出一次增量檔案。

2. 使用 **[!UICONTROL 時間]** 選擇器，選擇一天中的時間，在 [!DNL UTC] 格式。

3. 使用 **[!UICONTROL 日期]** 選擇器，以選擇應進行導出的時間間隔。 請注意，在功能的測試版中，無法設定導出的結束日期。 有關詳細資訊，請查看 [已知限制](#known-limitations) 的子菜單。

4. 選擇 **[!UICONTROL 下一個]** 以保存計畫並繼續 **[!UICONTROL 審閱]** 的子菜單。

>[!NOTE]
> 
>對於資料集導出，檔案名具有無法修改的預設預設格式。 請參閱一節 [驗證資料集導出是否成功](#verify) 的子菜單。

## 請檢閱 {#review}

在 **[!UICONTROL 審閱]** 的子菜單。 選擇 **[!UICONTROL 取消]** 分解流， **[!UICONTROL 後退]** 修改設定，或 **[!UICONTROL 完成]** 確認選擇並開始將資料集導出到目標。

![顯示審閱步驟的資料集導出工作流。](/help/destinations/assets/ui/export-datasets/review.png)

## 驗證資料集導出是否成功 {#verify}

導出資料集時，Experience Platform建立 `.json` 或 `.parquet` 檔案。 希望根據您提供的導出計畫將新檔案存入您的儲存位置。

Experience Platform在指定的儲存位置建立資料夾結構，該結構將存放導出的資料集檔案。 每次導出時都會按照以下模式建立新資料夾：

`folder-name-you-provided/datasetID/exportTime=YYYYMMDDHHMM`

預設檔案名是隨機生成的，並確保導出的檔案名是唯一的。

### 示例資料集檔案 {#sample-files}

這些檔案在您的儲存位置中的存在是成功導出的確認。 要瞭解導出檔案的結構，可以下載示例 [.parfe檔案](../assets/common/part-00000-tid-253136349007858095-a93bcf2e-d8c5-4dd6-8619-5c662e261097-672704-1-c000.parquet) 或 [.json檔案](../assets/common/part-00000-tid-4172098795867639101-0b8c5520-9999-4cff-bdf5-1f32c8c47cb9-451986-1-c000.json)。

## 從目標中刪除資料集 {#remove-dataset}

要從現有資料流中刪除資料集，請執行以下步驟：

1. 登錄到 [Experience PlatformUI](https://platform.adobe.com/) 選擇 **[!UICONTROL 目標]** 的下界。 選擇 **[!UICONTROL 瀏覽]** 以查看現有目標資料流。

   ![顯示目標連接的目標瀏覽視圖，其餘內容模糊。](../assets/ui/export-datasets/browse-dataset-connections.png)

   >[!TIP]
   > 
   >選擇篩選器表徵圖 ![篩選器表徵圖](../assets/ui/edit-activation/filter.png) 的子菜單。 排序面板提供所有目標的清單。 可以從清單中選擇多個目標，以查看與所選目標關聯的資料流的篩選選擇。

1. 從 **[!UICONTROL 激活資料]** 列中，選擇datasets control以查看映射到此導出資料流的所有資料集。

   ![在「激活資料」列中突出顯示的可用資料集導航選項。](../assets/ui/export-datasets/go-to-datasets-data.png)

1. 的 **[!UICONTROL 激活資料]** 頁面。 選擇 **[!UICONTROL 刪除資料集]** 在右欄中，觸發刪除資料集確認對話框。

   ![刪除資料集對話框，其中顯示右滑軌中的「刪除資料集」控制項。](../assets/ui/export-datasets/remove-dataset-control.png)

1. 在確認對話框中，選擇 **[!UICONTROL 刪除]** 從導出到目標中立即刪除資料集。

   ![顯示從資料流中確認資料集刪除選項的對話框。](../assets/ui/export-datasets/remove-dataset-confirm.png)

## 已知限制 {#known-limitations}

請記住資料集導出的Beta版本的以下限制：

* 當前有一個權限(**[!UICONTROL 管理和激活資料集目標]**)，包括管理和激活資料集目標上的權限。 這些控制項將在將來拆分為更細粒度的權限。 查看 [所需權限](#permissions) 的子目錄。
* 目前，您只能導出增量檔案，並且無法為資料集導出選擇結束日期。
* 當前無法自定義導出的檔案名。
* UI當前不阻止您刪除正導出到目標的資料集。 不要刪除要導出到目標的任何資料集。 [刪除資料集](#remove-dataset) 從目標資料流中刪除它。
* 監視資料集導出的度量當前與配置檔案導出的數字混合使用，因此它們不反映真正的導出數字。
