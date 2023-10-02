---
title: 將資料集匯出至雲端儲存空間目標
type: Tutorial
description: 瞭解如何將資料集從Adobe Experience Platform匯出至您偏好的雲端儲存位置。
exl-id: e89652d2-a003-49fc-b2a5-5004d149b2f4
source-git-commit: 8b8abea65ee0448594113ca77f75b84293646146
workflow-type: tm+mt
source-wordcount: '1750'
ht-degree: 5%

---

# 將資料集匯出至雲端儲存空間目的地

>[!AVAILABILITY]
>
>* 已購買Real-Time CDP Prime或Ultimate套件、Adobe Journey Optimizer或Customer Journey Analytics的客戶可使用此功能。 如需詳細資訊，請聯絡您的Adobe代表。

本文會說明匯出所需的工作流程 [資料集](/help/catalog/datasets/overview.md) 從Adobe Experience Platform到您偏好的雲端儲存位置，例如 [!DNL Amazon S3]、 SFTP位置或 [!DNL Google Cloud Storage] 藉由使用Experience Platform UI。

您也可以使用Experience Platform API來匯出資料集。 閱讀 [匯出資料集API教學課程](/help/destinations/api/export-datasets.md) 以取得詳細資訊。

## 可用於匯出的資料集 {#datasets-to-export}

您可以匯出的資料集因Experience Platform應用程式(Real-Time CDP、Adobe Journey Optimizer)、階層（Prime或Ultimate）以及您購買的任何附加元件(例如：Data Distiller)而異。

根據您購買的應用程式、產品層級和任何附加元件，從下表瞭解您可以匯出的資料集型別：

<table>
<thead>
  <tr>
    <th>應用程式/附加元件</th>
    <th>階層</th>
    <th>可供匯出的資料集</th>
  </tr>
</thead>
<tbody>
  <tr>
    <td rowspan="2">Real-Time CDP</td>
    <td>Prime</td>
    <td>透過Sources、Web SDK、Mobile SDK、Analytics Data Connector和Audience Manager擷取或收集資料後，在Experience Platform UI中建立的設定檔和體驗事件資料集。</td>
  </tr>
  <tr>
    <td>Ultimate</td>
    <td><ul><li>透過Sources、Web SDK、Mobile SDK、Analytics Data Connector和Audience Manager擷取或收集資料後，在Experience Platform UI中建立的設定檔和體驗事件資料集。</li><li> <a href="https://experienceleague.adobe.com/docs/experience-platform/dashboards/query.html?lang=en#profile-attribute-datasets">系統產生的設定檔快照集資料集</a>.</li></td>
  </tr>
  <tr>
    <td rowspan="2">Adobe Journey Optimizer</td>
    <td>Prime</td>
    <td>請參閱 <a href="https://experienceleague.adobe.com/docs/journey-optimizer/using/data-management/datasets/export-datasets.html?lang=zh-Hant"> Adobe Journey Optimizer</a> 檔案。 （更新為深層連結至支援資料集的AJO表格或區段）</td>
  </tr>
  <tr>
    <td>Ultimate</td>
    <td>請參閱 <a href="https://experienceleague.adobe.com/docs/journey-optimizer/using/data-management/datasets/export-datasets.html?lang=zh-Hant"> Adobe Journey Optimizer</a> 檔案。 （更新為深層連結至支援資料集的AJO表格或區段）</td>
  </tr>
  <tr>
    <td>資料Distiller</td>
    <td>資料Distiller （附加元件）</td>
    <td>透過查詢服務建立的衍生資料集。</td>
  </tr>
</tbody>
</table>

## 支援的目的地 {#supported-destinations}

目前，您可以將資料集匯出至熒幕擷取畫面中強調並列於下方的雲端儲存空間目的地。

![支援資料集匯出的目的地](/help/destinations/assets/ui/export-datasets/destinations-supporting-dataset-exports.png)

* [[!DNL Azure Data Lake Storage Gen2]](../../destinations/catalog/cloud-storage/adls-gen2.md)
* [[!DNL Data Landing Zone]](../../destinations/catalog/cloud-storage/data-landing-zone.md)
* [[!DNL Google Cloud Storage]](../../destinations/catalog/cloud-storage/google-cloud-storage.md)
* [[!DNL Amazon S3]](../../destinations/catalog/cloud-storage/amazon-s3.md#changelog)
* [[!DNL Azure Blob]](../../destinations/catalog/cloud-storage/azure-blob.md#changelog)
* [[!DNL SFTP]](../../destinations/catalog/cloud-storage/sftp.md#changelog)

## 何時啟用對象或匯出資料集 {#when-to-activate-audiences-or-activate-datasets}

Experience Platform目錄中的某些檔案型目的地同時支援對象啟用和資料集匯出。

* 當您想要將資料結構化為依對象興趣或資格分組的設定檔時，請考慮啟用對象。
* 或者，當您想要匯出原始資料集時，也可以考慮匯出資料集，這些資料集未根據對象興趣或資格進行分組或結構化。 您可以將這些資料用於報表、資料科學工作流程和其他許多使用案例。 例如，身為管理員、資料工程師或分析師，您可以從Experience Platform匯出資料，以便與資料倉儲同步、在BI分析工具、外部雲端ML工具中使用，或儲存在您的系統中以符合長期儲存需求。

本檔案包含匯出資料集所需的所有資訊。 如果您要啟動 *對象* 若要存取雲端儲存空間或電子郵件行銷目的地，請閱讀 [啟用對象資料至批次設定檔匯出目的地](/help/destinations/ui/activate-batch-profile-destinations.md).

## 先決條件 {#prerequisites}

若要將資料集匯出至雲端儲存空間目的地，您必須已成功完成 [已連線至目的地](./connect-destination.md). 如果您尚未這麼做，請前往 [目的地目錄](../catalog/overview.md)，瀏覽支援的目的地，並設定您要使用的目的地。

### 必要權限 {#permissions}

若要匯出資料集，您需要 **[!UICONTROL 檢視目的地]**， **[!UICONTROL 檢視資料集]**、和 **[!UICONTROL 管理和啟用資料集目的地]** [存取控制許可權](/help/access-control/home.md#permissions). 閱讀 [存取控制總覽](/help/access-control/ui/overview.md) 或聯絡您的產品管理員以取得必要許可權。

為確保您擁有匯出資料集的必要許可權以及目的地支援匯出資料集，請瀏覽目的地目錄。 如果目的地有 **[!UICONTROL 啟動]** 或 **[!UICONTROL 匯出資料集]** 控制項，則表示您擁有適當的許可權。

## 選取您的目的地 {#select-destination}

依照指示選取可匯出資料集的目的地：

1. 前往 **[!UICONTROL 連線>目的地]**，然後選取 **[!UICONTROL 目錄]** 標籤。

   ![反白顯示目錄控制項的目的地目錄標籤。](/help/destinations/assets/ui/export-datasets/catalog-tab.png)

1. 選取 **[!UICONTROL 啟動]** 或 **[!UICONTROL 匯出資料集]** 位於對應您要匯出資料集之目的地的卡片上。

   ![反白顯示「啟動」控制項的目的地目錄標籤。](/help/destinations/assets/ui/export-datasets/activate-button.png)

1. 選取 **[!UICONTROL 資料型別資料集]** 並選取您要匯出資料集的目的地連線，然後選取「 」 **[!UICONTROL 下一個]**.

>[!TIP]
> 
>如果要設定匯出資料集的新目的地，請選取「 」 **[!UICONTROL 設定新目的地]** 以觸發 [連線到目的地](/help/destinations/ui/connect-destination.md) 工作流程。

![強調資料集控制項的目的地啟用工作流程。](/help/destinations/assets/ui/export-datasets/select-datatype-datasets.png)

1. 此 **[!UICONTROL 選取資料集]** 檢視出現。 繼續下一節至 [選取您的資料集](#select-datasets) 以匯出。

## 選取您的資料集 {#select-datasets}

使用資料集名稱左側的核取方塊來選取您要匯出至目的地的資料集，然後選取「 」 **[!UICONTROL 下一個]**.

![資料集匯出工作流程會顯示選取資料集步驟，您可在此選取要匯出的資料集。](/help/destinations/assets/ui/export-datasets/select-datasets.png)

## 排程資料集匯出 {#scheduling}

>[!CONTEXTUALHELP]
>id="platform_destinations_activate_datasets_exportoptions"
>title="資料集的檔案匯出選項"
>abstract="選取&#x200B;**匯出增量檔案**，僅匯出上次匯出後新增至資料集的資料。<br>第一個增量檔案匯出包括資料集中的所有資料，充當回填。未來的增量檔案僅包括第一次匯出後新增至資料集的資料。"

在 **[!UICONTROL 正在排程]** 步驟，您可以設定資料集匯出的開始日期和匯出步調。

此 **[!UICONTROL 匯出增量檔案]** 選項會自動選取。 這會觸發匯出，其中第一個檔案是資料集的完整快照，後續檔案是自上次匯出以來資料集的增量新增。

>[!IMPORTANT]
>
>第一個匯出的增量檔案包含資料集中的所有現有資料，可作為回填。

![顯示排程步驟的資料集匯出工作流程。](/help/destinations/assets/ui/export-datasets/export-incremental-datasets.png)

1. 使用 **[!UICONTROL 頻率]** 選擇器以選取匯出頻率：

   * **[!UICONTROL 每日]**：排程增量檔案每天於您指定的時間匯出一次。
   * **[!UICONTROL 每小時]**：排程每3、6、8或12小時匯出一次增量檔案。

2. 使用 **[!UICONTROL 時間]** 選擇器來選擇一天中的時間，在 [!DNL UTC] 格式，應何時進行匯出。

3. 使用 **[!UICONTROL 日期]** 選擇器來選擇應進行匯出的間隔。 請注意，您目前無法設定匯出的結束日期。 如需詳細資訊，請檢視 [已知限制](#known-limitations) 區段。

4. 選取 **[!UICONTROL 下一個]** 以儲存排程並前往 **[!UICONTROL 檢閱]** 步驟。

>[!NOTE]
> 
>對於資料集匯出，檔案名稱具有無法修改的預設集預設格式。 請參閱區段 [驗證資料集匯出成功](#verify) 以取得詳細資訊和匯出檔案的範例。

## 請檢閱 {#review}

在 **[!UICONTROL 檢閱]** 頁面中，您可以看到選取範圍的摘要。 選取 **[!UICONTROL 取消]** 若要分解流量， **[!UICONTROL 返回]** 以修改您的設定，或 **[!UICONTROL 完成]** 以確認您的選取範圍並開始將資料集匯出至目的地。

![顯示檢閱步驟的資料集匯出工作流程。](/help/destinations/assets/ui/export-datasets/review.png)

## 驗證資料集匯出成功 {#verify}

匯出資料集時，Experience Platform會建立 `.json` 或 `.parquet` 檔案中所指定的儲存位置。 預期會根據您提供的匯出排程，將新檔案儲存在您的儲存位置。

Experience Platform會在您指定的儲存位置中建立資料夾結構，並存放匯出的資料集檔案。 每次匯出時都會建立一個新資料夾，其模式如下：

`folder-name-you-provided/datasetID/exportTime=YYYYMMDDHHMM`

預設檔案名稱是隨機產生的，並確保匯出的檔案名稱是唯一的。

### 範例資料集檔案 {#sample-files}

這些檔案存在於您的儲存位置即表示匯出成功。 若要瞭解匯出檔案的結構，您可以下載範例 [.parquet檔案](../assets/common/part-00000-tid-253136349007858095-a93bcf2e-d8c5-4dd6-8619-5c662e261097-672704-1-c000.parquet) 或 [.json檔案](../assets/common/part-00000-tid-4172098795867639101-0b8c5520-9999-4cff-bdf5-1f32c8c47cb9-451986-1-c000.json).

#### 壓縮的資料集檔案 {#compressed-dataset-files}

在 [連線到目標工作流程](/help/destinations/ui/connect-destination.md#file-formatting-and-compression-options)，您可以選取要壓縮的匯出資料集檔案，如下所示：

![連線到目的地以匯出資料集時，檔案型別和壓縮選取專案。](/help/destinations/assets/ui/export-datasets/compression-format-datasets.gif)

請注意兩種檔案型別在壓縮時的檔案格式差異：

* 匯出壓縮的JSON檔案時，匯出的檔案格式為 `json.gz`
* 匯出壓縮的parquet檔案時，匯出的檔案格式為 `gz.parquet`

## 從目的地移除資料集 {#remove-dataset}

若要從現有資料流移除資料集，請遵循下列步驟：

1. 登入 [EXPERIENCE PLATFORMUI](https://experience.adobe.com/platform/) 並選取 **[!UICONTROL 目的地]** 從左側導覽列。 選取 **[!UICONTROL 瀏覽]** 以檢視您現有的目的地資料流。

   ![目的地瀏覽檢視，其中顯示目的地連線，其餘則模糊化。](../assets/ui/export-datasets/browse-dataset-connections.png)

   >[!TIP]
   > 
   >選取篩選器圖示 ![Filter-icon](../assets/ui/edit-activation/filter.png) 以啟動「排序」面板。 排序面板會提供您所有目的地的清單。 您可以從清單中選取多個目的地，以檢視與所選目的地相關聯的資料流篩選選取專案。

1. 從 **[!UICONTROL 啟用資料]** 欄，選取資料集控制項以檢視對應至此匯出資料流的所有資料集。

   ![可用的資料集導覽選項在「啟動資料」欄中反白顯示。](../assets/ui/export-datasets/go-to-datasets-data.png)

1. 此 **[!UICONTROL 啟用資料]** 目的地頁面隨即顯示。 選取 **[!UICONTROL 移除資料集]** 在右側邊欄中，以觸發移除資料集確認對話方塊。

   ![移除資料集對話方塊會在右側邊欄中顯示「移除資料集」控制項。](../assets/ui/export-datasets/remove-dataset-control.png)

1. 在確認對話方塊中，選取 **[!UICONTROL 移除]** 立即將資料集從匯出至目的地時移除。

   ![對話方塊，其中顯示確認從資料流移除資料集選項。](../assets/ui/export-datasets/remove-dataset-confirm.png)


## 資料集匯出權益 {#licensing-entitlement}

請參閱產品說明檔案，瞭解您每年有權為每個Experience Platform應用程式匯出多少資料。 例如，您可以檢視Real-Time CDP產品說明 [此處](https://helpx.adobe.com/legal/product-descriptions/real-time-customer-data-platform-b2c-edition-prime-and-ultimate-packages.html).

請注意，不同應用程式的資料匯出許可權並非累加。 例如，這表示如果您購買Real-Time CDP Ultimate和Adobe Journey Optimizer Ultimate，則根據產品說明，設定檔匯出許可權將是兩個許可權中較大者。 您的容量權益的計算方式為：取用您的授權設定檔總數，再乘以Real-Time CDP Prime的500 KB或Real-Time CDP Ultimate的700 KB，以判斷您有權取得的資料量。

另一方面，如果您購買Data Distiller等附加元件，您有權取得的資料匯出限制則代表產品層級和附加元件的總和。

您可以在授權儀表板中，根據合約限制檢視及追蹤您的設定檔匯出。

## 已知限制 {#known-limitations}

針對資料集匯出的一般可用性版本，請記住下列限制：

* 目前，您只能匯出增量檔案，並且無法為資料集匯出選取結束日期。
* 匯出的檔案名稱目前無法自訂。
* 透過API建立的資料集目前無法匯出。
* UI目前不會阻止您刪除匯出至目的地的資料集。 請勿刪除匯出至目的地的資料集。 [移除資料集](#remove-dataset) 從目的地資料流中刪除之前。
* 資料集匯出的監控量度目前與設定檔匯出的數字混合在一起，因此不能反映真正的匯出數字。
