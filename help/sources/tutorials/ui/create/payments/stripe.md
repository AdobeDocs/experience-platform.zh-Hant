---
title: 使用使用者介面，將付款資料從您的Stripe帳戶擷取至Experience Platform。
description: 瞭解如何使用使用者介面，將付款資料從您的Stripe帳戶擷取到Experience Platform。
badge: Beta
exl-id: f20c5935-a7c0-4387-b29e-73e78cab4972
source-git-commit: fded2f25f76e396cd49702431fa40e8e4521ebf8
workflow-type: tm+mt
source-wordcount: '1658'
ht-degree: 3%

---

# 使用使用者介面將付款資料從您的[!DNL Stripe]帳戶擷取到Experience Platform

>[!NOTE]
>
>[!DNL Stripe]來源是測試版。 閱讀來源概觀中的[條款與條件](../../../../home.md#terms-and-conditions)，以取得有關使用測試版標籤之來源的詳細資訊。

閱讀下列教學課程，瞭解如何使用使用者介面將付款資料從您的[!DNL Stripe]帳戶擷取到Adobe Experience Platform。

## 快速入門

本教學課程需要您實際瞭解下列Experience Platform元件：

* [[!DNL Experience Data Model (XDM)] 系統](../../../../../xdm/home.md)： [!DNL Experience Platform]用來組織客戶體驗資料的標準化架構。
   * [結構描述組合的基本概念](../../../../../xdm/schema/composition.md)：瞭解XDM結構描述的基本建置區塊，包括結構描述組合中的關鍵原則和最佳實務。
   * [結構描述編輯器教學課程](../../../../../xdm/tutorials/create-schema-ui.md)：瞭解如何使用結構描述編輯器使用者介面建立自訂結構描述。
* [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md)：根據來自多個來源的彙總資料，提供統一的即時消費者設定檔。

### Authentication

請閱讀[[!DNL Stripe] 總覽](../../../../connectors/payments/stripe.md)，瞭解如何擷取您的驗證認證的相關資訊。

## 連線您的[!DNL Stripe]帳戶 {#connect}

在Experience Platform UI中，從左側導覽選取&#x200B;**[!UICONTROL 來源]**&#x200B;以存取[!UICONTROL 來源]工作區。 您可以從熒幕左側的目錄中選取適當的類別。 或者，您可以使用搜尋選項來尋找您要使用的特定來源。

在&#x200B;*付款*&#x200B;類別下，選取&#x200B;**[!DNL Stripe]**，然後選取&#x200B;**[!UICONTROL 設定]**。

>[!TIP]
>
>當指定的來源尚未具有已驗證的帳戶時，來源目錄中的來源會顯示&#x200B;**[!UICONTROL 設定]**&#x200B;選項。 一旦驗證帳戶存在，此選項就會變更為&#x200B;**[!UICONTROL 新增資料]**。

![Experience Platform UI中的來源目錄，已選取Stripe來源卡。](../../../../images/tutorials/create/stripe/catalog.png)

**[!UICONTROL 連線Stripe帳戶]**&#x200B;頁面隨即顯示。 您可以在此頁面使用新的或現有的證明資料。

>[!BEGINTABS]

>[!TAB 建立新帳戶]

若要建立新帳戶，請選取&#x200B;**[!UICONTROL 新帳戶]**，並提供名稱、選擇性說明和您的認證。

完成時，請選取&#x200B;**[!UICONTROL 連線到來源]**，然後等待一段時間以建立新連線。

![來源工作流程的新帳戶建立介面。](../../../../images/tutorials/create/stripe/new.png)

| 認證 | 說明 |
| --- | --- |
| 存取權杖 | 您的[!DNL Stripe]存取權杖。 如需如何擷取存取Token的詳細資訊，請閱讀[[!DNL Stripe] 驗證指南](../../../../connectors/payments/stripe.md)。 |

>[!TAB 使用現有的帳戶]

若要使用現有帳戶，請選取&#x200B;**[!UICONTROL 現有帳戶]**，然後從現有帳戶目錄中選取您要使用的帳戶。

選取&#x200B;**[!UICONTROL 下一步]**&#x200B;以繼續。

![來源目錄的現有帳戶選擇頁面。](../../../../images/tutorials/create/stripe/existing.png)

>[!ENDTABS]

## 選取資料 {#select-data}

現在您已擁有帳戶的存取權，您必須識別要擷取之[!DNL Stripe]資料的適當路徑。 選取&#x200B;**[!UICONTROL 資源路徑]**，然後選取您要從中擷取資料的端點。 可用的[!DNL Stripe]端點為：

* 費用
* 訂閱
* 退款
* 餘額交易
* 客戶
* 價格

![資源路徑下拉式視窗。](../../../../images/tutorials/create/stripe/select-resource-path.png)

選取您的端點後，介面會更新為預覽畫面，顯示您選取的[!DNL Stripe]端點的資料結構。 選取&#x200B;**[!UICONTROL 下一步]**&#x200B;以繼續。

![您的Stripe資料預覽視窗。](../../../../images/tutorials/create/stripe/preview.png)

## 提供資料集和資料流詳細資料 {#provide-dataset-and-dataflow-details}

接下來，您必須提供有關資料集和資料流的資訊。

### 資料集詳細資料 {#dataset-details}

資料集是資料集合的儲存和管理結構，通常是包含方案 (欄) 和欄位 (列) 的表格。 成功擷取至Experience Platform的資料會以資料集的形式儲存在資料湖中。 在此步驟中，您可以建立新資料集或使用現有資料集。

>[!BEGINTABS]

>[!TAB 使用新的資料集]

若要使用新的資料集，請選取&#x200B;**[!UICONTROL 新的資料集]**，然後為您的資料集提供名稱和選擇性描述。 您也必須選取您的資料集所要遵守的Experience Data Model (XDM)結構。

![新的資料集選取範圍介面。](../../../../images/tutorials/create/stripe/new-dataset.png)

| 新資料集詳細資料 | 說明 |
| --- | --- |
| 輸出資料集名稱 | 新資料集的名稱。 |
| 說明 | （選用）新資料集的簡短說明。 |
| 結構描述 | 貴組織中現有的結構描述下拉式清單。 您也可以在來源設定程式之前建立自己的結構描述。 如需詳細資訊，請閱讀[在UI](../../../../../xdm/tutorials/create-schema-ui.md)中建立XDM結構描述的指南。 |

>[!TAB 使用現有的資料集]

如果您已有現有的資料集，請選取「**[!UICONTROL 現有的資料集]**」，然後使用「**[!UICONTROL 進階搜尋]**」選項來檢視貴組織中所有資料集的視窗，包括其個別詳細資訊，例如是否啟用這些資料集以擷取至即時客戶設定檔。

![現有的資料集選取介面。](../../../../images/tutorials/create/stripe/existing-dataset.png)

>[!ENDTABS]

+++選取步驟以啟用設定檔擷取、錯誤診斷及部分擷取。

如果您的資料集已啟用即時客戶個人檔案，那麼在此步驟中，您可以切換&#x200B;**[!UICONTROL 個人檔案資料集]**&#x200B;以啟用您的資料以進行個人檔案擷取。 您也可以使用此步驟來啟用&#x200B;**[!UICONTROL 錯誤診斷]**&#x200B;和&#x200B;**[!UICONTROL 部分擷取]**。

* **[!UICONTROL 錯誤診斷]**：選取&#x200B;**[!UICONTROL 錯誤診斷]**&#x200B;以指示來源產生錯誤診斷，以便您稍後在監視資料集活動和資料流狀態時參考。
* **[!UICONTROL 部分擷取]**：部分批次擷取可擷取含有錯誤的資料，最多可達到特定可設定的臨界值。 此功能可讓您將所有精確資料成功擷取到Experience Platform，同時所有不正確的資料會個別批次處理，並提供無效原因的資訊。

+++

### 資料流詳細資料 {#dataflow-details}

設定資料集後，您必須提供資料流的詳細資訊，包括名稱、選用的說明和警報設定。

![資料流詳細資料設定步驟。](../../../../images/tutorials/create/stripe/dataflow-detail.png)

| 資料流設定 | 說明 |
| --- | --- |
| 資料流名稱 | 資料流的名稱。  依預設，這將使用正在匯入的檔案名稱。 |
| 說明 | （選用）資料流的簡短說明。 |
| 警示 | Experience Platform可產生使用者可訂閱的事件型警報。 這些選項都需要執行中的資料流才能觸發。  如需詳細資訊，請閱讀[警示概述](../../alerts.md) <ul><li>**來源資料流執行開始**：選取此警示以在您的資料流執行開始時收到通知。</li><li>**來源資料流執行成功**：選取此警示以在您的資料流結束且沒有任何錯誤時接收通知。</li><li>**來源資料流執行失敗**：選取此警示以在您的資料流執行結束時發生任何錯誤時接收通知。</li></ul> |

完成後，選取&#x200B;**[!UICONTROL 下一步]**&#x200B;以繼續。

## 將欄位對應至XDM結構描述 {#mapping}

**[!UICONTROL 對應]**&#x200B;步驟出現。 使用對應介面將來源資料對應至適當的結構描述欄位，然後再將該資料擷取至Experience Platform。 如需如何使用對應介面的詳細指南，請閱讀[資料準備UI指南](../../../../../data-prep/ui/mapping.md)以取得詳細資訊。

![來源工作流程的對應介面。](../../../../images/tutorials/create/stripe/mapping.png)

## 設定擷取排程 {#scheduling}

接下來，使用排程介面為資料流建立擷取排程。

選取頻率下拉式清單，以設定資料流的擷取頻率。

![頻率下拉式功能表。](../../../../images/tutorials/create/stripe/frequency.png)

您也可以選取行事曆圖示，並使用快顯行事曆來設定擷取開始時間。

![排程的可設定行事曆。](../../../../images/tutorials/create/stripe/calendar.png)

| 正在排程設定 | 說明 |
| --- | --- |
| 頻率 | 設定頻率以指出資料流執行的頻率。 您可以將頻率設為： <ul><li>**一次**：將您的頻率設定為`once`以建立一次性內嵌。 建立一次性擷取資料流時，無法使用間隔和回填的設定。 依預設，排程頻率會設定為一次。</li><li>**分鐘**：將頻率設為`minute`，排程您的資料流以每分鐘擷取資料。</li><li>**小時**：將頻率設為`hour`，排程您的資料流以每小時為基礎擷取資料。</li><li>**天**：將您的頻率設為`day`，排程您的資料流每天擷取資料。</li><li>**周**：將頻率設為`week`，排程您的資料流每週擷取資料。</li></ul> |
| 間隔 | 選取頻率後，您就可以設定間隔設定，以建立每次擷取之間的時間範圍。 例如，如果您將頻率設為「天」，並將間隔設為15，則您的資料流將每隔15天執行一次。 您不能將間隔設定為零。 每個頻率的最小接受間隔值如下：<ul><li>**一次**：不適用</li><li>**分鐘**： 15</li><li>**小時**： 1</li><li>**天**： 1</li><li>**周**： 1</li></ul> |
| 開始時間 | 預計執行的時間戳記，以UTC時區顯示。 |
| 回填 | 回填會決定最初要擷取的資料。 如果已啟用回填，則會在第一次排程擷取期間擷取指定路徑中的所有目前檔案。 如果停用回填，則只會擷取在第一次內嵌執行到開始時間之間載入的檔案。 將不會擷取在開始時間之前載入的檔案。 |

設定資料流的擷取排程後，請選取&#x200B;**[!UICONTROL 下一步]**。

![來源工作流程的排程介面。](../../../../images/tutorials/create/stripe/scheduling.png)

## 檢閱您的資料流

資料流建立流程的最後一步是在執行資料流之前進行檢閱。 使用&#x200B;**[!UICONTROL 檢閱]**&#x200B;步驟，在執行新資料流之前先檢閱其詳細資料。 詳細資料會分組到以下類別中：

* **連線**：顯示來源型別、所選來源檔案的相關路徑，以及該來源檔案中的欄數。
* **指派資料集與對應欄位**：顯示要將來源資料擷取到哪個資料集，包括資料集所堅持的結構描述。
* **排程**：顯示內嵌排程的有效期間、頻率和間隔。

檢閱您的資料流後，請選取&#x200B;**[!UICONTROL 完成]**，並等待一些時間來建立資料流。

![來源工作流程的稽核步驟。](../../../../images/tutorials/create/stripe/review.png)

## 後續步驟

依照本教學課程中的指示，您已成功建立資料流，將您[!DNL Stripe]來源的付款資料帶入Experience Platform。 如需其他資源，請瀏覽以下概述的檔案。

### 監視資料流

建立資料流後，您可以監視透過它擷取的資料，以檢視擷取率、成功和錯誤的資訊。 如需如何監視資料流的詳細資訊，請造訪有關UI[&#128279;](../../../../../dataflows/ui/monitor-sources.md)中監視帳戶和資料流的教學課程。

### 更新您的資料流

若要更新資料流排程、對應和一般資訊的設定，請瀏覽有關[在UI中更新來源資料流的教學課程](../../update-dataflows.md)。

### 刪除您的資料流

您可以刪除不再需要的資料流，或使用&#x200B;**[!UICONTROL 資料流]**&#x200B;工作區中可用的&#x200B;**[!UICONTROL 刪除]**&#x200B;功能建立錯誤的資料流。 如需有關如何刪除資料流的詳細資訊，請瀏覽教學課程，瞭解如何在UI[&#128279;](../../delete.md)中刪除資料流。
