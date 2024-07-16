---
title: 在UI中建立自訂活動資料的Source連線和資料流Marketo Engage
description: 本教學課程提供在UI中建立Marketo Engage來源連線和資料流的步驟，以便將自訂活動資料引進Adobe Experience Platform。
exl-id: 05a7b500-11d2-4d58-be43-a2c4c0ceeb87
source-git-commit: ba39f62cd77acedb7bfc0081dbb5f59906c9b287
workflow-type: tm+mt
source-wordcount: '1470'
ht-degree: 0%

---

# 在UI中建立自訂活動資料的[!DNL Marketo Engage]來源連線和資料流

>[!NOTE]
>
>本教學課程提供如何設定並將&#x200B;**自訂活動**&#x200B;資料從[!DNL Marketo]帶入Experience Platform的特定步驟。 如需如何匯入&#x200B;**標準活動**&#x200B;資料的步驟，請閱讀[[!DNL Marketo] UI指南](./marketo.md)。

除了[標準活動](../../../../connectors/adobe-applications/mapping/marketo.md#activities)之外，您也可以使用[!DNL Marketo]來源將自訂活動資料帶入Adobe Experience Platform。 本檔案提供如何在UI中使用[!DNL Marketo]來源建立自訂活動資料的來源連線和資料流的步驟。

## 快速入門

本教學課程需要您實際瞭解下列Adobe Experience Platform元件：

* [B2B名稱空間與結構描述自動產生公用程式](../../../../connectors/adobe-applications/marketo/marketo-namespaces.md)： B2B名稱空間與結構描述自動產生公用程式可讓您使用[!DNL Postman]自動產生B2B名稱空間與結構描述的值。 您必須先完成B2B名稱空間和結構描述，才能建立[!DNL Marketo]來源連線和資料流。
* [來源](../../../../home.md)：Experience Platform允許從各種來源擷取資料，同時讓您能夠使用Platform服務來建構、加標籤以及增強傳入的資料。
* [體驗資料模型(XDM)](../../../../../xdm/home.md)：Experience Platform用來組織客戶體驗資料的標準化架構。
   * [在UI中建立和編輯結構描述](../../../../../xdm/ui/resources/schemas.md)：瞭解如何在UI中建立和編輯結構描述。
* [身分識別名稱空間](../../../../../identity-service/features/namespaces.md)：身分識別名稱空間是[!DNL Identity Service]的元件，用來做為身分識別相關內容的指標。 完整身分包含ID值和名稱空間。
* [[!DNL Real-Time Customer Profile]](/help/profile/home.md)：根據來自多個來源的彙總資料，提供統一的即時消費者設定檔。
* [沙箱](../../../../../sandboxes/home.md)：Experience Platform提供的虛擬沙箱可將單一Platform執行個體分割成個別的虛擬環境，以利開發及改進數位體驗應用程式。

## 擷取您的自訂活動詳細資料

將自訂活動資料從[!DNL Marketo]引進Experience Platform的第一個步驟是擷取API名稱和自訂活動的顯示名稱。

使用[[!DNL Marketo]](https://app-sjint.marketo.com/#MM0A1)介面登入您的帳戶。 在左側導覽列中的[!DNL Database Management]下方，選取&#x200B;**Marketo自訂活動**。

介面會更新為自訂活動的顯示，包括有關其各自顯示名稱和API名稱的資訊。 您也可以使用滑鼠右邊欄來選取並檢視您帳戶中的其他自訂活動。

![Adobe Marketo Engage UI中的自訂活動介面。](../../../../images/tutorials/create/marketo-custom-activities/marketo-custom-activity.png)

從頂端標題選取&#x200B;**欄位**&#x200B;以檢視與自訂活動相關聯的欄位。 在此頁面中，您可以檢視自訂活動中欄位的名稱、API名稱、說明和資料型別。 有關個別欄位的詳細資訊將在建立結構描述時的後續步驟中使用。

![Marketo EngageUI中的Marketo自訂活動欄位詳細資訊頁面。](../../../../images/tutorials/create/marketo-custom-activities/marketo-custom-activity-fields.png)

## 在B2B活動結構中設定自訂活動的欄位群組

在Experience PlatformUI的&#x200B;*[!UICONTROL 結構描述]*&#x200B;儀表板中，選取&#x200B;**[!UICONTROL 瀏覽]**，然後從結構描述清單中選取&#x200B;**[!UICONTROL B2B活動]**。

>[!TIP]
>
>使用搜尋列可加快您在方案清單中的導覽。

![已選取B2B活動結構描述的Experience PlatformUI中的結構描述工作區。](../../../../images/tutorials/create/marketo-custom-activities/b2b-activity.png)

### 為自訂活動建立新的欄位群組

接下來，將新的欄位群組新增至[!DNL B2B Activity]結構描述。 此欄位群組應該對應至您要擷取的自訂活動，且應該使用您先前擷取的自訂活動的顯示名稱。

若要新增欄位群組，請選取&#x200B;*[!UICONTROL 構成]*&#x200B;下的&#x200B;*[!UICONTROL 欄位群組]*&#x200B;面板旁的&#x200B;**[!UICONTROL +新增]**。

![結構描述結構。](../../../../images/tutorials/create/marketo-custom-activities/add-new-field-group.png)

出現&#x200B;*[!UICONTROL 新增欄位群組]*&#x200B;視窗。 選取「**[!UICONTROL 建立新欄位群組]**」，然後為您在先前步驟中擷取的自訂活動提供相同的顯示名稱，並為您的新欄位群組提供選擇性說明。 完成後，選取&#x200B;**[!UICONTROL 新增欄位群組]**。

![標籤與建立新欄位群組的視窗。](../../../../images/tutorials/create/marketo-custom-activities/create-new-field-group.png)

建立後，您自訂活動的新欄位群組會出現在[!UICONTROL 欄位群組]目錄中。

![結構描述結構包含新增至欄位群組面板下的新欄位群組。](../../../../images/tutorials/create/marketo-custom-activities/new-field-group-created.png)

### 將新欄位新增至您的結構描述結構

接下來，將新欄位新增至您的結構描述。 此新欄位必須設為`type: object`，並將包含自訂活動的個別欄位。

若要新增欄位，請選取結構描述名稱旁的加號(`+`)。 *[!UICONTROL 未命名欄位的專案 | 型別]*&#x200B;出現。 接下來，使用&#x200B;*[!UICONTROL 欄位屬性]*&#x200B;面板來設定欄位屬性。 將欄位名稱設為自訂活動的API名稱，並將顯示名稱設為自訂活動的顯示名稱。 然後，將型別設定為`object`並將欄位群組指派給您在上一步建立的自訂活動欄位群組。 完成後，選取&#x200B;**[!UICONTROL 套用]**。

![選取加號(`+`)的結構描述結構，以便可以新增欄位。](../../../../images/tutorials/create/marketo-custom-activities/add-new-object.png)

新欄位會顯示在您的結構描述中。

![新欄位已新增至結構描述。](../../../../images/tutorials/create/marketo-custom-activities/new-object-field-added.png)

### 將子欄位新增至物件欄位 {#add-sub-fields-to-the-object-field}

準備結構描述的最後一步是在您在上一步建立的欄位中新增個別欄位。

![新增到結構描述內欄位的一組子欄位。](../../../../images/tutorials/create/marketo-custom-activities/add-sub-fields.png)

## 建立資料流

結構描述設定完成後，您現在可以繼續為自訂活動資料建立資料流。

在Platform UI中，從左側導覽列選取&#x200B;**[!UICONTROL 來源]**&#x200B;以存取[!UICONTROL 來源]工作區。 [!UICONTROL 目錄]畫面會顯示您可以建立帳戶的各種來源。

您可以從熒幕左側的目錄中選取適當的類別。 或者，您可以使用搜尋列來尋找您要使用的特定來源。

在[!UICONTROL Adobe應用程式]類別下，選取&#x200B;**[!UICONTROL Marketo Engage]**。 然後，選取&#x200B;**[!UICONTROL 新增資料]**&#x200B;以建立新的[!DNL Marketo]資料流。

![已選取Marketo Engage來源的Experience PlatformUI上的來源目錄。](../../../../images/tutorials/create/marketo/catalog.png)

### 選取資料

從[!DNL Marketo]資料集清單中選取&#x200B;**[!UICONTROL 活動]**，然後選取&#x200B;**[!UICONTROL 下一步]**。

![已選取活動資料集的來源工作流程中的選取資料步驟。](../../../../images/tutorials/create/marketo-custom-activities/select-data.png)

### 資料流詳細資料

接下來，[提供您的資料流](./marketo.md#provide-dataflow-details)的資訊，包括資料集和資料流的名稱和說明、您將使用的結構描述，以及[!DNL Profile]擷取、錯誤診斷和部分擷取的設定。

![資料流詳細資料步驟。](../../../../images/tutorials/create/marketo-custom-activities/dataflow-detail.png)

### 對應

系統會自動填入標準活動欄位的對應，但自訂活動欄位必須手動對應至其對應的目標欄位。

若要開始對應您的自訂活動欄位，請選取&#x200B;**[!UICONTROL 新增欄位型別]**，然後選取&#x200B;**[!UICONTROL 新增欄位]**。

![包含下拉式功能表的對應步驟可新增欄位。](../../../../images/tutorials/create/marketo-custom-activities/add-new-mapping-field.png)

瀏覽來源資料結構，並尋找您要內嵌的自訂活動欄位。 完成後，選取&#x200B;**[!UICONTROL 選取]**。

>[!TIP]
>
>為避免混淆並處理重複的欄位名稱，自訂活動欄位將以API名稱為前置詞。

![來源資料結構。](../../../../images/tutorials/create/marketo-custom-activities/select-new-mapping-field.png)

若要新增目標欄位，請選取結構描述圖示![結構描述圖示](../../../../images/tutorials/create/marketo-custom-activities/schema-icon.png)，然後從目標結構描述中選取自訂活動欄位。

![目標結構描述結構。](../../../../images/tutorials/create/marketo-custom-activities/add-target-mapping-field.png)

重複步驟以新增其餘的自訂活動對應欄位。 完成後，選取&#x200B;**[!UICONTROL 下一步]**。

![來源與目標資料的所有對應。](../../../../images/tutorials/create/marketo-custom-activities/all-mappings.png)

### 檢閱

*[!UICONTROL 檢閱]*&#x200B;步驟隨即顯示，可讓您在建立新資料流之前先檢閱該資料流。 詳細資料會分組到以下類別中：

* **[!UICONTROL 連線]**：顯示來源型別、所選來源實體的相關路徑，以及該來源實體中的資料行數量。
* **[!UICONTROL 指派資料集與對應欄位]**：顯示要將來源資料擷取到哪個資料集，包括資料集所堅持的結構描述。

檢閱您的資料流後，請選取「**[!UICONTROL 儲存並擷取]**」，並等待一些時間來建立資料流。

![總結連線、資料集和對映欄位資訊的最終稽核步驟。](../../../../images/tutorials/create/marketo-custom-activities/review.png)

### 將自訂活動新增至現有活動資料流 {#add-to-existing-dataflows}

若要將自訂活動資料新增至現有資料流，請修改現有活動資料流的對應，並使用您要擷取的自訂活動資料。 這可讓您將自訂活動擷取至相同的現有活動資料集中。 如需有關如何更新現有資料流對應的詳細資訊，請參閱[在UI](../../update-dataflows.md)中更新資料流的指南。

### 使用[!DNL Query Service]篩選自訂活動的活動 {#query-service-filter}

資料流完成後，您可以使用[查詢服務](../../../../../query-service/home.md)來篩選自訂活動資料的活動。

將自訂活動內嵌到Platform中時，自訂活動的API名稱會自動變成其`eventType`。 使用`eventType={API_NAME}`篩選自訂活動資料。

```sql
SELECT * FROM with_custom_activities_ds_today WHERE eventType='aepCustomActivityDemo1' 
```

使用`IN`子句篩選多個自訂活動：

```sql
SELECT * FROM $datasetName WHERE eventType='{API_NAME}'
SELECT * FROM $datasetName WHERE eventType IN ('aepCustomActivityDemo1', 'aepCustomActivityDemo2')
```

下圖顯示[查詢編輯器](../../../../../query-service/ui/user-guide.md)中篩選自訂活動資料的範例SQL陳述式。

![顯示自訂活動查詢範例的平台UI。](../../../../images/tutorials/create/marketo-custom-activities/queries.png)

## 後續步驟

依照此教學課程中的指示，您已為[!DNL Marketo]個自訂活動資料設定Platform結構描述，並建立資料流以將該資料引進Platform。 如需[!DNL Marketo]來源的一般資訊，請閱讀[[!DNL Marketo] 來源概觀](../../../../connectors/adobe-applications/marketo/marketo.md)。
