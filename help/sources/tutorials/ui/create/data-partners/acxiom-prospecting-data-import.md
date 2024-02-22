---
title: Acxiom潛在客戶資料匯入
description: 瞭解如何使用UI將Acxiom潛在資料連線到Adobe Experience Platform和Adobe Real-time Customer Data Platform。
last-substantial-update: 2024-02-21T00:00:00Z
badge: Beta
source-git-commit: bf7e2e08d54f113c6e2cc5060f51725555c2c049
workflow-type: tm+mt
source-wordcount: '1752'
ht-degree: 2%

---

# 建立 [!DNL Acxiom Prospecting Data Import] UI中的來源連線和資料流

>[!NOTE]
>
>此 [!DNL Acxiom Prospecting Data Import] 來源為測試版。 請閱讀 [來源概觀](../../../../home.md#terms-and-conditions) 以取得有關使用測試版標籤來源的詳細資訊。

[!DNL Acxiom]的Adobe Real-time Customer Data Platform潛在客戶資料匯入是儘可能提供最高生產力的潛在客戶對象的程式。 [!DNL Acxiom] 透過安全匯出擷取Real-Time CDP第一方資料，並透過獲獎的衛生和身分解析系統執行資料。 這會產生資料檔案，以用作隱藏清單。 然後，此資料檔案會與「Acxiom全域」資料庫進行比對，如此即可針對匯入量身打造潛在客戶清單。

您可以使用 [!DNL Acxiom] 來源以使用Amazon S3作為放置點，從Acxiom潛在客戶服務擷取及對應回應。

閱讀本教學課程以瞭解如何建立 [!DNL Acxiom Prospecting Data Import] 使用Adobe Experience Platform使用者介面的來源連線和資料流。

## 先決條件 {#prerequisites}

本教學課程需要您實際瞭解下列Experience Platform元件：

* [[!DNL Experience Data Model (XDM)] 系統](../../../../../xdm/home.md)：Experience Platform組織客戶體驗資料的標準化架構。
   * [結構描述組合基本概念](../../../../../xdm/schema/composition.md)：瞭解XDM結構描述的基本建置區塊，包括結構描述組合中的關鍵原則和最佳實務。
   * [結構描述編輯器教學課程](../../../../../xdm/tutorials/create-schema-ui.md)：瞭解如何使用結構編輯器UI建立自訂結構描述。
* [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md)：根據來自多個來源的彙總資料，提供統一的即時消費者個人檔案。
* [[!DNL Prospect Profile]](../../../../../profile/ui/prospect-profile.md)：瞭解如何建立和使用潛在客戶設定檔，以使用第三方資訊收集有關未知客戶的資訊。

### 收集必要的認證

若要在Experience Platform上存取貯體，您必須提供下列憑證的有效值：

| 認證 | 說明 |
| --- | --- |
| [!DNL Acxiom] 驗證金鑰 | 驗證金鑰。 此值可取自 [!DNL Acxiom] 團隊。 |
| [!DNL Amazon S3] 存取金鑰 | 貯體的存取金鑰ID。 此值可取自 [!DNL Acxiom] 團隊。 |
| [!DNL Amazon S3] 秘密金鑰 | 貯體的秘密金鑰ID。 此值可取自 [!DNL Acxiom] 團隊。 |
| 貯體名稱 | 這是您的貯體，檔案將在此共用。 此值可取自 [!DNL Acxiom] 團隊。 |

>[!IMPORTANT]
>
>您必須同時擁有兩者 **[!UICONTROL 檢視來源]** 和 **[!UICONTROL 管理來源]** 為您的帳戶啟用的許可權以連線您的 [!DNL Acxiom] 要Experience Platform的帳戶。 請聯絡您的產品管理員以取得必要許可權。 如需詳細資訊，請閱讀 [存取控制UI指南](../../../../../access-control/ui/overview.md).

## 連線您的 [!DNL Acxiom] 帳戶

在Platform UI中選取 **[!UICONTROL 來源]** 從左側導覽列存取 [!UICONTROL 來源] 工作區。 此 [!UICONTROL 目錄] 畫面會顯示各種來源，供您建立帳戶。

您可以從熒幕左側的目錄中選取適當的類別。 或者，您可以使用搜尋選項來尋找您要使用的特定來源。

在 **[!UICONTROL 資料與身分識別合作夥伴]** 類別，選取 **[!UICONTROL Acxiom潛在客戶資料匯入]** 然後選取 **[!UICONTROL 設定]**.

>[!TIP]
>
>顯示的來源卡片 **[!UICONTROL 新增資料]** 表示來源已有已驗證的帳戶。 另一方面，顯示的來源卡片 **[!UICONTROL 設定]** 這表示您必須提供認證並建立新帳戶才能使用該來源。

![已選取Acxiom來源的來源目錄。](../../../../images/tutorials/create/acxiom-prospect-suppression-data-sourcing/image-source-catalog.png)

### 建立新帳戶

如果您正在使用新認證，請選取 **[!UICONTROL 新帳戶]**. 在出現的輸入表單上，提供名稱、選擇性說明，以及 [!DNL Acxiom] 認證。 完成後，選取 **[!UICONTROL 連線到來源]** 然後等待一段時間以建立新連線。

![來源工作流程的新帳戶介面。](../../../../images/tutorials/create/acxiom-prospect-suppression-data-sourcing/image-source-new-account.png)

| 認證 | 說明 |
| --- | --- |
| 帳戶名稱 | 帳戶的名稱。 |
| 說明 | （選用）帳戶用途的簡短說明。 |
| [!DNL Acxiom] 驗證金鑰 | 此 [!DNL Acxiom]帳戶核准需要提供的金鑰。 在連線到資料庫之前，這必須符合適當的值。  此索引鍵必須是24個字元，而且只能包含： A-Z、a-z和0-9。 |
| S3存取金鑰 | S3存取金鑰會參照Amazon S3位置。 這由您的管理員在定義S3角色許可權時提供。 |
| S3秘密金鑰 | S3秘密金鑰會參照Amazon S3位置。 這由您的管理員在定義S3角色許可權時提供。 |
| s3SessionToken | （選用）連線至S3時的驗證Token值。 |
| serviceUrl | （選用）連線至非標準位置的S3時要使用的URL位置。 |
| 貯體名稱 | （選用）在S3上設定的S3貯體名稱，可作為資料選取的開始路徑。 |
| 檔案夾路徑 | 如果使用貯體中的子目錄，則也可以在資料選取中將路徑指定為起始路徑。 |

### 使用現有帳戶

若要使用現有帳戶，請選取 **[!UICONTROL 現有帳戶]**.

從清單中選取一個帳戶，以檢視該帳戶的詳細資訊。 選取帳戶後，選取 **[!UICONTROL 下一個]** 以繼續進行。

![來源工作流程的現有帳戶介面。](../../../../images/tutorials/create/acxiom-prospect-suppression-data-sourcing/image-source-existing-account.png)

## 選取資料

選取您要從所需儲存貯體和子目錄中擷取的檔案。 一旦定義了分隔符號和壓縮型別，就可以提供資料的預覽。 選取檔案後，選取 **[!UICONTROL 下一個]** 以繼續進行。

![來源工作流程的選取資料和檔案預覽介面。](../../../../images/tutorials/create/acxiom-prospect-suppression-data-sourcing/image-source-preview.png)

>[!NOTE]
>
>雖然JSON和Parquet檔案型別已列出，但您並非需要在以下期間使用這些型別： [!DNL Acxiom] 來源工作流程。

## 提供資料集和資料流詳細資料

接下來，您必須提供有關資料集和資料流的資訊。

### 資料集詳細資訊

>[!BEGINTABS]

>[!TAB 使用新資料集]

資料集是資料集合的儲存和管理結構，通常是包含方案 (欄) 和欄位 (列) 的表格。 成功擷取至Experience Platform的資料會以資料集的形式保留在資料湖中。 若要使用新資料集，請選取「 」 **[!UICONTROL 新資料集]**.

![新資料集介面。](../../../../images/tutorials/create/acxiom-prospect-suppression-data-sourcing/image-source-new-dataset.png)

| 新資料集詳細資料 | 說明 |
| --- | --- |
| 輸出資料集名稱 | 新資料集的名稱。 |
| 說明 | （選用）資料集用途的簡短說明。 |
| 綱要 | 貴組織中現有的結構描述下拉式清單。 您也可以在來源設定程式之前建立自己的結構描述。 如需詳細資訊，請閱讀以下指南： [在UI中建立結構描述](../../../../../xdm/tutorials/create-schema-ui.md). |

>[!TAB 使用現有的資料集]

若要使用現有的資料集，請選取 **[!UICONTROL 現有資料集]**.

您可以選取 **[!UICONTROL 進階搜尋]** 以檢視貴組織所有資料集的視窗，包括其各自的詳細資料，例如是否啟用這些資料集以擷取至Real-Time Customer Profile。

![現有的資料集介面。](../../../../images/tutorials/create/acxiom-prospect-suppression-data-sourcing/image-source-dataset.png)

>[!ENDTABS]

### 資料流詳細資料

在此步驟中，如果您的資料集已啟用設定檔，那麼您可以選取 **[!UICONTROL 設定檔資料集]** 切換以啟用設定檔擷取的資料。 您也可以啟用 [!UICONTROL 錯誤診斷] 和 [!UICONTROL 部分擷取].

* **錯誤診斷**  — 選取 **錯誤診斷** 指示來源產生錯誤診斷，以便您稍後使用API來參照。 如需詳細資訊，請閱讀 [錯誤診斷概述](../../../../../ingestion/quality/error-diagnostics.md)
* **啟用部分擷取**  — 部分批次擷取是指擷取包含錯誤的資料，上限為特定臨界值的功能。 有了這項功能，使用者可以成功地將其所有正確的資料擷取到Adobe Experience Platform，同時將其所有不正確的資料單獨分批處理，以及關於其無效原因的詳細資訊。  如需詳細資訊，請閱讀 [部分擷取概觀](../../../../../ingestion/batch-ingestion/partial.md)

![資料流詳細資料設定介面。](../../../../images/tutorials/create/acxiom-prospect-suppression-data-sourcing/image-source-dataset-details.png)

| 資料流設定 | 說明 |
| --- | --- |
| 資料流名稱 | 資料流的名稱。  依預設，這將使用正在匯入的檔案名稱。 |
| 說明 | （選用）資料流的簡短說明。 |
| 警報 | Experience Platform可產生使用者可訂閱的事件型警報，這些選項都是執行中的資料流以觸發這些警報。  如需詳細資訊，請閱讀 [警報概觀](../../alerts.md) <ul><li>**來源資料流執行開始**：選取此警報以在資料流執行開始時收到通知。</li><li>**來源資料流執行成功**：選取此警報可在您的資料流結束且沒有任何錯誤時收到通知。</li><li>**來源資料流執行失敗**：選取此警報可在您的資料流執行結束時，收到任何錯誤的通知。</li></ul> |

## 映射

使用對應介面將來源資料對應到適當的結構描述欄位，然後再將資料擷取到Experience Platform。  如需詳細資訊，請閱讀 [UI中的對應指南](../../../../../data-prep/ui/mapping.md)

![對應介面。](../../../../images/tutorials/create/acxiom-prospect-suppression-data-sourcing/image-source-mapping.png)

## 排程您的資料流擷取

使用排程介面來定義資料流程的擷取排程。

* **頻率**：設定頻率以指出資料流執行的頻率。 您可以將頻率設為：一次、分鐘、小時、天或周。
* **間隔**：選取頻率後，您就可以設定間隔設定，以建立每次擷取之間的時間範圍。 例如，如果您將頻率設為「天」，並將間隔設為15，則您的資料流將每隔15天執行一次。 間隔不能設為零，而且至少必須設為15。
* **開始時間**  — 預計執行的時間戳記，以UTC時區顯示。
* **回填**  — 回填會決定最初要擷取的資料。 如果已啟用回填，則會在第一次排程擷取期間擷取指定路徑中的所有目前檔案。 如果停用回填，則只會擷取在第一次內嵌執行到開始時間之間載入的檔案。 將不會擷取在開始時間之前載入的檔案。

![排程設定介面。](../../../../images/tutorials/create/acxiom-prospect-suppression-data-sourcing/image-source-scheduling.png)

## 檢閱您的資料流

使用「複查」頁面可在擷取前取得資料流的摘要。 詳細資料會分組到以下類別中：

* **連線**  — 顯示來源型別、所選來源檔案的相關路徑，以及該來源檔案中的欄數。
* **指派資料集並對映欄位**  — 顯示要將來源資料擷取到哪個資料集中，包括資料集所堅持的結構描述。
* **正在排程**  — 顯示擷取排程的有效期間、頻率和間隔。
檢閱資料流後，請按一下「完成」 ，然後等待一些時間建立資料流。

![檢閱頁面。](../../../../images/tutorials/create/acxiom-prospect-suppression-data-sourcing/image-source-review.png)

## 後續步驟

依照本教學課程中的指示，您已成功建立資料流，以將批次資料從 [!DNL Acxiom] 來源以Experience Platform。 如需其他資源，請瀏覽以下概述的檔案。

### 監視資料流

建立資料流後，您可以監視透過它擷取的資料，以檢視擷取率、成功和錯誤的資訊。 如需如何監視資料流的詳細資訊，請瀏覽上的教學課程 [在UI中監視帳戶和資料流](../../monitor.md).

### 更新您的資料流

若要更新資料流排程、對應和一般資訊的設定，請造訪本教學課程： [在UI中更新來源資料流程](../../update-dataflows.md)

### 刪除您的資料流

您可以刪除不再需要的資料流，或是使用建立的資料流不正確。 **[!UICONTROL 刪除]** 函式位於 **[!UICONTROL 資料流]** 工作區。 如需如何刪除資料流的詳細資訊，請前往上的教學課程： [在UI中刪除資料流](../../delete.md).

## 其他資源 {#additional-resources}

[!DNL Acxiom] 對象資料與分佈： https://www.acxiom.com/customer-data/audience-data-distribution/
