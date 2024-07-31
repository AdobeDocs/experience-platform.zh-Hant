---
keywords: crm；CRM；CRM目的地；外聯；外聯crm目的地
title: 外展連線
description: 外展目的地可讓您匯出帳戶資料，並在外展內根據您的業務需求啟用資料。
exl-id: 7433933d-7a4e-441d-8629-a09cb77d5220
source-git-commit: 5aefa362d7a7d93c12f9997d56311127e548497e
workflow-type: tm+mt
source-wordcount: '1678'
ht-degree: 2%

---

# [!DNL Outreach]個連線

## 概觀 {#overview}

[[!DNL Outreach]](https://www.outreach.io/)是銷售執行平台，擁有世界上最多B2B買賣雙方互動資料，並在專有AI技術方面投入巨資，以將銷售資料轉換為智慧。 [!DNL Outreach]可協助組織自動化銷售參與度，並依據收入情報採取行動，以改善其效率、可預測性及成長。

此[!DNL Adobe Experience Platform] [目的地](/help/destinations/home.md)利用[外展更新資源API](https://api.outreach.io/api/v2/docs#update-an-existing-resource)，可讓您更新與[!DNL Outreach]中潛在客戶相對應的對象中的身分。

[!DNL Outreach]使用具有授權授權的OAuth 2作為驗證機制，與[!DNL Outreach] [!DNL Update Resource API]通訊。 在[向目的地驗證](#authenticate)區段中，進一步說明如何向您的[!DNL Outreach]執行個體進行驗證。

## 使用案例 {#use-cases}

作為行銷人員，您可以根據潛在客戶的Adobe Experience Platform設定檔屬性，為他們提供個人化體驗。 您可以從您的離線資料建立受眾，並將這些受眾傳送至[!DNL Outreach]，以便在Adobe Experience Platform中更新受眾和設定檔後立即顯示在潛在客戶摘要中。

## 先決條件 {#prerequisites}

### Experience Platform必要條件 {#prerequisites-in-experience-platform}

在啟用資料到[!DNL Outreach]目的地之前，您必須在[!DNL Experience Platform]中建立[結構描述](/help/xdm/schema/composition.md)、[資料集](https://experienceleague.adobe.com/docs/platform-learn/tutorials/data-ingestion/create-datasets-and-ingest-data.html)和[區段](https://experienceleague.adobe.com/docs/platform-learn/tutorials/segments/create-segments.html)。

如果您需要對象狀態的指引，請參閱[對象成員資格詳細資料結構描述欄位群組](/help/xdm/field-groups/profile/segmentation.md)的Adobe檔案。

### 外展必要條件 {#prerequisites-destination}

請注意[!DNL Outreach]中的下列必要條件，以便從Platform匯出資料至您的[!DNL Outreach]帳戶：

#### 您必須擁有外展帳戶 {#prerequisites-account}

移至[!DNL Outreach] [登入](https://accounts.outreach.io/users/sign_in)頁面以註冊並建立帳戶（如果尚未建立帳戶）。 如需詳細資訊，另請參閱[!DNL Outreach]支援[頁面](https://support.outreach.io/hc/en-us/articles/207238607-Claim-Your-Outreach-Account)。

在對[!DNL Outreach] CRM目的地進行驗證之前，請記下以下專案：

| 認證 | 說明 |
|---|---|
| 電子郵件 | 您的[!DNL Outreach]帳戶電子郵件 |
| 密碼 | 您的[!DNL Outreach]帳戶密碼 |

#### 設定自訂欄位標籤 {#prerequisites-custom-fields}

[!DNL Outreach]支援[潛在客戶](https://support.outreach.io/hc/en-us/articles/360001557554-Outreach-Prospect-Profile-Overview)的自訂欄位。 如需其他指引，請參閱[如何在延伸中新增自訂欄位](https://support.outreach.io/hc/en-us/articles/219124908-How-To-Add-a-Custom-Field-in-Outreach)。 為方便識別，建議手動將標籤更新至其對應的對象名稱，而非保留預設值。 例如：

潛在客戶的[!DNL Outreach]設定頁面顯示自訂欄位。
![外展UI熒幕擷圖顯示設定頁面上的自訂欄位。](../../assets/catalog/crm/outreach/outreach-custom-fields.png)

潛在客戶的[!DNL Outreach]設定頁面會顯示自訂欄位，其中&#x200B;*個使用者易記的*標籤符合對象名稱。 您可以對照這些標籤在潛在客戶頁面上檢視對象狀態。
![外展UI熒幕擷圖顯示設定頁面上具有相關標籤的自訂欄位。](../../assets/catalog/crm/outreach/outreach-custom-field-labels.png)

>[!NOTE]
>
> 標簽名稱僅供識別之用。 更新潛在客戶時不會使用它們。

## 護欄

[!DNL Outreach] API的速率限製為每位使用者每小時10,000個請求。 如果達到此限制，您將收到包含下列訊息的`429`回應： `You have exceeded your permitted rate limit of 10,000; please try again at 2017-01-01T00:00:00.`。

如果您收到此訊息，您必須更新對象匯出排程以符合速率臨界值。

如需其他詳細資訊，請參閱[[!DNL Outreach] 檔案](https://api.outreach.io/api/v2/docs#rate-limiting)。

## 支援的身分 {#supported-identities}

[!DNL Outreach]支援下表中描述的身分更新。 深入瞭解[身分](/help/identity-service/features/namespaces.md)。

| 目標身分 | 說明 | 考量事項 |
|---|---|---|
| `OutreachId` | <ul><li>[!DNL Outreach]識別碼。 這是對應至潛在客戶設定檔的數值。</li><li>ID必須符合要更新的潛在客戶[!DNL Outreach] URL內的ID。</li><li>如需詳細資訊，請參閱[[!DNL Outreach] 檔案](https://api.outreach.io/api/v2/docs#update-an-existing-resource)。</li></ul> | 強制 |

## 匯出型別和頻率 {#export-type-frequency}

請參閱下表以取得目的地匯出型別和頻率的資訊。

| 項目 | 類型 | 附註 |
---------|----------|---------|
| 匯出類型 | **[!UICONTROL 以設定檔為基礎]** | <ul><li> 您正在匯出區段的所有成員，以及所需的結構描述欄位&#x200B;*（例如：電子郵件地址、電話號碼、姓氏）* （根據您的欄位對應）。</li><li> 根據[對象排程](#schedule-segment-export-example)步驟期間提供的[!UICONTROL 對應ID]值，[!DNL Outreach]中的每個區段狀態都會以來自Platform的對應對象狀態更新。</li></ul> |
| 匯出頻率 | **[!UICONTROL 串流]** | <ul><li> 串流目的地是「一律開啟」的API型連線。 一旦根據對象評估在Experience Platform中更新了設定檔，聯結器就會將更新傳送至下游的目的地平台。 深入瞭解[串流目的地](/help/destinations/destination-types.md#streaming-destinations)。</li></ul> |

{style="table-layout:auto"}

## 連線到目標 {#connect}

>[!IMPORTANT]
> 
> 若要連線到目的地，您需要&#x200B;**[!UICONTROL 管理目的地]** [存取控制許可權](/help/access-control/home.md#permissions)。 閱讀[存取控制總覽](/help/access-control/ui/overview.md)或連絡您的產品管理員以取得必要的許可權。

若要連線到此目的地，請依照[目的地組態教學課程](../../ui/connect-destination.md)中所述的步驟進行。 在設定目標工作流程中，填寫以下兩個區段中列出的欄位。

在&#x200B;**[!UICONTROL 目的地]** > **[!UICONTROL 目錄]**&#x200B;內，搜尋[!DNL Outreach]。 或者，您可以在CRM類別下找到它。

### 驗證目標 {#authenticate}

若要驗證到目的地，請選取&#x200B;**[!UICONTROL 連線到目的地]**。

![平台UI熒幕擷圖顯示如何驗證外展活動。](../../assets/catalog/crm/outreach/authenticate-destination.png)

您將會看到[!DNL Outreach]登入頁面。 提供您的電子郵件。

![外展UI熒幕擷圖顯示輸入電子郵件以驗證外展的欄位。](../../assets/catalog/crm/outreach/authenticate-destination-login-email.png)

接下來，提供您的密碼。

![外展UI熒幕擷圖顯示輸入密碼步驟以驗證外展的欄位。](../../assets/catalog/crm/outreach/authenticate-destination-login-password.png)

* **[!UICONTROL 使用者名稱]**：您的[!DNL Outreach]帳戶電子郵件。
* **[!UICONTROL 密碼]**：您的[!DNL Outreach]帳戶密碼。

如果提供的詳細資料有效，UI會顯示帶有綠色勾號的&#x200B;**已連線**&#x200B;狀態。 然後您可以繼續下一步驟。

### 填寫目標詳細資訊 {#destination-details}

若要設定目的地的詳細資訊，請填寫下方的必填和選用欄位。 UI中欄位旁的星號表示該欄位為必填欄位。
![平台UI熒幕擷圖顯示如何填寫外展目的地詳細資訊。](../../assets/catalog/crm/outreach/destination-details.png)

* **[!UICONTROL 名稱]**：您日後可辨識此目的地的名稱。
* **[!UICONTROL 描述]**：可協助您日後識別此目的地的描述。

### 啟用警示 {#enable-alerts}

您可以啟用警報以接收有關傳送到您目的地的資料流狀態的通知。 從清單中選取警報以訂閱接收有關資料流狀態的通知。 如需警示的詳細資訊，請參閱[使用UI訂閱目的地警示](../../ui/alerts.md)的指南。

當您完成提供目的地連線的詳細資訊後，請選取&#x200B;**[!UICONTROL 下一步]**。

## 啟動此目標的對象 {#activate}

>[!IMPORTANT]
> 
>* 若要啟用資料，您需要&#x200B;**[!UICONTROL 檢視目的地]**、**[!UICONTROL 啟用目的地]**、**[!UICONTROL 檢視設定檔]**&#x200B;和&#x200B;**[!UICONTROL 檢視區段]** [存取控制許可權](/help/access-control/home.md#permissions)。 閱讀[存取控制總覽](/help/access-control/ui/overview.md)或連絡您的產品管理員以取得必要的許可權。
>* 若要匯出&#x200B;*身分*，您需要&#x200B;**[!UICONTROL 檢視身分圖表]** [存取控制許可權](/help/access-control/home.md#permissions)。<br> ![選取工作流程中反白的身分名稱空間，以啟用目的地的對象。](/help/destinations/assets/overview/export-identities-to-destination.png "選取工作流程中反白顯示的身分名稱空間，以啟用目的地的對象。"){width="100" zoomable="yes"}

閱讀[將設定檔和對象啟用至串流對象匯出目的地](../../ui/activate-segment-streaming-destinations.md)，以瞭解啟用此目的地對象的指示。

### 對應考量事項和範例 {#mapping-considerations-example}

若要將對象資料從Adobe Experience Platform正確傳送至[!DNL Outreach]目的地，您必須完成欄位對應步驟。 對應包括在Platform帳戶中的Experience Data Model (XDM)結構描述欄位與來自目標目的地的對應對應專案之間建立連結。 若要將您的XDM欄位正確對應到[!DNL Outreach]目的地欄位，請遵循下列步驟：

1. 在[!UICONTROL 對應]步驟中，按一下&#x200B;**[!UICONTROL 新增對應]**。 您會在畫面上看到新的對應列。
   ![平台UI熒幕擷圖顯示如何新增對應](../../assets/catalog/crm/outreach/add-new-mapping.png)

1. 在[!UICONTROL 選取來源欄位]視窗中，選擇&#x200B;**[!UICONTROL 選取身分名稱空間]**類別並新增所需的對應。
   ![顯示Source對應的平台UI熒幕擷取畫面](../../assets/catalog/crm/outreach/source-mapping.png)

1. 在[!UICONTROL 選取目標欄位]視窗中，選取您要將來源欄位對應到的目標欄位型別。
   * **[!UICONTROL 選取身分名稱空間]**：選取此選項可將您的來源欄位從清單對應至身分名稱空間。
     ![平台UI熒幕擷取畫面顯示使用ExpancationId的Target對應。](../../assets/catalog/crm/outreach/target-mapping.png)

   * 在您的XDM設定檔結構描述與[!DNL Outreach]執行個體之間新增下列對應：

     | XDM設定檔結構描述 | [!DNL Outreach]執行個體 | 強制 |
     |---|---|---|
     | `Oid` | `OutreachId` | 是 |

   * **[!UICONTROL 選取自訂屬性]**：選取此選項可將您的來源欄位對應到您在[!UICONTROL 屬性名稱]欄位中定義的自訂屬性。 如需支援屬性的完整清單，請參閱[[!DNL Outreach] 潛在客戶檔案](https://api.outreach.io/api/v2/docs#prospect)。
     ![平台UI熒幕擷圖顯示使用LastName的目標對應。](../../assets/catalog/crm/outreach/target-mapping-lastname.png)

   * 例如，根據您要更新的值，在您的XDM設定檔結構描述與[!DNL Outreach]執行個體之間新增下列對應：

     | XDM設定檔結構描述 | [!DNL Outreach]執行個體 |
     |---|---|
     | `person.name.firstName` | `firstName` |
     | `person.name.lastName` | `lastName` |

   * 以下顯示使用這些對應的範例：
     ![顯示目標對應的平台UI熒幕擷圖範例。](../../assets/catalog/crm/outreach/mappings.png)

### 排程對象匯出和範例 {#schedule-segment-export-example}

* 執行[排程對象匯出](../../ui/activate-segment-streaming-destinations.md)步驟時，您必須手動將Platform對象對應到[!DNL Outreach]中的自訂欄位屬性。

* 若要這麼做，請選取每個區段，然後輸入對應的數值，該值對應至&#x200B;**[!UICONTROL 對應ID]**&#x200B;欄位中[!DNL Outreach]的&#x200B;*自訂欄位`N`標籤*&#x200B;欄位。

  >[!IMPORTANT]
  >
  > * 在[!UICONTROL 對應ID]內使用的數值&#x200B;*(`N`)*&#x200B;應該與尾碼為[!DNL Outreach]內數值的自訂屬性金鑰相符。 範例： *自訂欄位`N`標籤*。
  > * 您只需要指定數值，不需要指定整個自訂欄位標籤。
  > * [!DNL Outreach]支援最多150個自訂標籤欄位。
  > * 如需詳細資訊，請參閱[[!DNL Outreach] 潛在客戶檔案](https://api.outreach.io/api/v2/docs#prospect)。

   * 例如：

     | [!DNL Outreach]欄位 | 平台對應ID |
     |---|---|
     | 自訂欄位`4`標籤 | `4` |

     ![Platform UI熒幕擷圖顯示排程對象匯出期間的對應ID範例。](../../assets/catalog/crm/outreach/schedule-segment-export.png)

## 驗證資料匯出 {#exported-data}

若要驗證您是否已正確設定目的地，請遵循下列步驟：

1. 選取&#x200B;**[!UICONTROL 目的地]** > **[!UICONTROL 瀏覽]**以瀏覽目的地清單。
   ![顯示瀏覽目的地的Platform UI熒幕擷圖。](../../assets/catalog/crm/outreach/browse-destinations.png)

1. 選取目的地並驗證狀態為&#x200B;**[!UICONTROL 已啟用]**。
   ![平台UI熒幕擷圖顯示所選目的地的目的地資料流執行。](../../assets/catalog/crm/outreach/destination-dataflow-run.png)

1. 切換至&#x200B;**[!DNL Activation data]**標籤，然後選取對象名稱。
   ![顯示目的地啟用資料的Platform UI熒幕擷圖。](../../assets/catalog/crm/outreach/destinations-activation-data.png)

1. 監控對象摘要，並確保設定檔計數對應於在區段內建立的計數。
   ![顯示區段摘要的Platform UI熒幕擷圖。](../../assets/catalog/crm/outreach/segment.png)

1. 登入[!DNL Outreach]網站，然後導覽至[!DNL Apps] > [!DNL Contacts]頁面，並檢查是否已新增對象的設定檔。 您可以看到根據[對象排程](#schedule-segment-export-example)步驟期間提供的[!UICONTROL 對應ID]值，[!DNL Outreach]中的每個對象狀態已更新為來自Platform的對應對象狀態。

![外展UI熒幕擷圖顯示「外展潛在客戶」頁面，其中包含更新的對象狀態。](../../assets/catalog/crm/outreach/outreach-prospect.png)

## 資料使用與控管 {#data-usage-governance}

處理您的資料時，所有[!DNL Adobe Experience Platform]目的地都符合資料使用原則。 如需[!DNL Adobe Experience Platform]如何強制資料控管的詳細資訊，請參閱[資料控管概觀](/help/data-governance/home.md)。

## 錯誤與疑難排解 {#errors-and-troubleshooting}

檢查資料流執行時，您可能會看到下列錯誤訊息： `Bad request reported while pushing events to the destination. Please contact the administrator and try again.`

![平台UI熒幕擷圖顯示錯誤請求錯誤。](../../assets/catalog/crm/outreach/error.png)

若要修正此錯誤，請確認您在Platform中為[!DNL Outreach]對象提供的[!UICONTROL 對應ID]有效且存在於[!DNL Outreach]中。

## 其他資源 {#additional-resources}

[[!DNL Outreach] 檔案](https://api.outreach.io/api/v2/docs/)中包含[錯誤回應](https://api.outreach.io/api/v2/docs#error-responses)的詳細資料，您可以用來偵錯任何問題。
