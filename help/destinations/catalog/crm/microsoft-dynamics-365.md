---
keywords: crm；CRM；CRM目的地；Microsoft Dynamics 365；Microsoft Dynamics 365 crm目的地
title: Microsoft Dynamics 365連線
description: Microsoft Dynamics 365目的地可讓您匯出帳戶資料，並在Microsoft Dynamics 365中根據您的業務需求加以啟用。
last-substantial-update: 2022-11-08T00:00:00Z
exl-id: 49bb5c95-f4b7-42e1-9aae-45143bbb1d73
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '2038'
ht-degree: 2%

---

# [!DNL Microsoft Dynamics 365]個連線

## 概觀 {#overview}

[[!DNL Microsoft Dynamics 365]](https://dynamics.microsoft.com/en-us/)是以雲端為基礎的業務應用程式平台，結合企業資源規劃(ERP)、客戶關係管理(CRM)以及生產力應用程式和AI工具，讓端對端的作業更順暢、控制更嚴密、增長潛力更大、成本更低。

此[!DNL Adobe Experience Platform] [目的地](/help/destinations/home.md)利用[[!DNL Contact Entity Reference API]](https://docs.microsoft.com/en-us/dynamics365/customerengagement/on-premises/developer/entities/contact?view=op-9-1)，可讓您將對象中的身分識別更新為[!DNL Dynamics 365]。

[!DNL Dynamics 365]使用具有授權授權的OAuth 2作為驗證機制，與[!DNL Contact Entity Reference API]通訊。 [向目的地驗證](#authenticate)區段中進一步說明如何向您的[!DNL Dynamics 365]執行個體進行驗證。

## 使用案例 {#use-cases}

行銷人員可以根據使用者Adobe Experience Platform設定檔中的屬性，將個人化體驗提供給使用者。 您可以從您的離線資料建立對象，並將這些對象傳送至[!DNL Dynamics 365]，以便在Adobe Experience Platform中更新對象和設定檔後立即顯示在使用者的摘要中。

## 先決條件 {#prerequisites}

### Experience Platform必要條件 {#prerequisites-in-experience-platform}

在啟用資料至[!DNL Dynamics 365]目的地之前，您必須在[!DNL Experience Platform]中建立[結構描述](/help/xdm/schema/composition.md)、[資料集](https://experienceleague.adobe.com/docs/platform-learn/tutorials/data-ingestion/create-datasets-and-ingest-data.html)和[對象](https://experienceleague.adobe.com/docs/platform-learn/tutorials/audiences/create-audiences.html)。

如果您需要對象狀態的指引，請參閱Adobe關於[對象成員資格詳細資料結構描述欄位群組](/help/xdm/field-groups/profile/segmentation.md)的檔案。

### [!DNL Microsoft Dynamics 365]必要條件 {#prerequisites-destination}

請注意[!DNL Dynamics 365]中的下列必要條件，以便從Experience Platform將資料匯出至您的[!DNL Dynamics 365]帳戶：

#### 您必須擁有[!DNL Microsoft Dynamics 365]帳戶 {#prerequisites-account}

移至[!DNL Dynamics 365] [試用版](https://dynamics.microsoft.com/en-us/dynamics-365-free-trial/)頁面以註冊並建立帳戶（如果尚未建立）。

#### 在[!DNL Dynamics 365]中建立欄位 {#prerequisites-custom-field}

建立型別`Simple`的自訂欄位，欄位資料型別為`Single Line of Text`，Experience Platform將用來更新[!DNL Dynamics 365]內的對象狀態。

如需其他指引，請參閱[!DNL Dynamics 365] [建立或編輯欄位（屬性）](https://docs.microsoft.com/en-us/dynamics365/customerengagement/on-premises/customize/create-edit-fields?view=op-9-1)檔案。

寫下您在[!DNL Dynamics 365]中建立的自訂欄位的&#x200B;**[!UICONTROL 自訂前置詞]**。 在[填寫目的地詳細資料](#destination-details)步驟期間，您將需要此首碼。 如需詳細資訊，請參閱[!DNL Dynamics 365]檔案的[建立及編輯欄位](https://learn.microsoft.com/en-us/dynamics365/customerengagement/on-premises/customize/create-edit-fields?view=op-9-1#create-and-edit-fields)區段。
![顯示自訂前置碼的Dynamics 365 UI熒幕擷圖。](../../assets/catalog/crm/microsoft-dynamics-365/dynamics-365-customization-prefix.png)

以下顯示[!DNL Dynamics 365]中的設定範例：
![顯示自訂欄位的Dynamics 365 UI熒幕擷圖。](../../assets/catalog/crm/microsoft-dynamics-365/dynamics-365-fields.png)

#### 在Azure Active Directory中註冊應用程式和應用程式使用者 {#prerequisites-app-user}

若要讓[!DNL Dynamics 365]存取資源，您必須使用[!DNL Azure Account]登入[[!DNL Azure Active Directory]](https://docs.microsoft.com/en-us/azure/active-directory/develop/howto-create-service-principal-portal#register-an-application-with-azure-ad-and-create-a-service-principal)，並建立下列專案：
* [!DNL Azure Active Directory]應用程式
* 服務主體
* 應用程式密碼

您還需要在[!DNL Azure Active Directory]中[建立應用程式使用者](https://docs.microsoft.com/en-us/power-platform/admin/manage-application-users#create-an-application-user)，並將其與新建立的應用程式建立關聯。

#### 收集[!DNL Dynamics 365]認證 {#gather-credentials}

在對[!DNL Dynamics 365] CRM目的地進行驗證之前，請記下以下專案：

| 認證 | 說明 | 範例 |
| --- | --- | --- |
| `Client ID` | [!DNL Azure Active Directory]應用程式的[!DNL Dynamics 365]使用者端識別碼。 請參閱[[!DNL Dynamics 365] 檔案](https://docs.microsoft.com/en-us/azure/active-directory/develop/howto-create-service-principal-portal#get-tenant-and-app-id-values-for-signing-in)以取得指引。 | `ababbaba-abab-baba-acac-acacacacacac` |
| `Client Secret` | 您的[!DNL Azure Active Directory]應用程式的[!DNL Dynamics 365]使用者端密碼。 您可能會在[[!DNL Dynamics 365] 檔案](https://docs.microsoft.com/en-us/azure/active-directory/develop/howto-create-service-principal-portal#authentication-two-options)中使用選項#2。 | `abcde~abcdefghijklmnopqrstuvwxyz12345678`作為指引。 |
| `Tenant ID` | 您[!DNL Azure Active Directory]應用程式的[!DNL Dynamics 365]租使用者識別碼。 請參閱[[!DNL Dynamics 365] 檔案](https://docs.microsoft.com/en-us/azure/active-directory/develop/howto-create-service-principal-portal#get-tenant-and-app-id-values-for-signing-in)以取得指引。 | `1234567-aaaa-12ab-ba21-1234567890` |
| `Region` | 與環境URL相關聯的Microsoft區域。<br>請參閱[[!DNL Dynamics 365] 檔案](https://learn.microsoft.com/en-us/power-platform/admin/new-datacenter-regions)以取得指引。 | 如果您的網域如下所示，在向[目的地](#authenticate).<br>進行驗證時，您需要在下拉式選取器中提供醒目提示的CRM欄位值 *組織57771b33。`crm`.dynamics.com*<br>&#x200B;例如：如果您的公司已布建在北美(NAM)地區，則您的URL會是`crm.dynamics.com`，而且您必須選取`crm`。 如果您的公司已布建在加拿大(CAN)地區，則您的URL會是`crm3.dynamics.com`，您需要選取`crm3`。 |
| `Environment URL` | 請參閱[[!DNL Dynamics 365] 檔案](https://docs.microsoft.com/en-us/dynamics365/customerengagement/on-premises/developer/org-service/discover-url-organization-organization-service?view=op-9-1)以取得指引。 | 如果您的[!DNL Dynamics 365]網域如下所示，則需要反白顯示的值。<br> *`org57771b33`.crm.dynamics.com* |

{style="table-layout:auto"}

## 護欄 {#guardrails}

[要求限制和配置](https://docs.microsoft.com/en-us/power-platform/admin/api-request-limits-allocations)頁面詳細說明與您的[!DNL Dynamics 365]授權相關的[!DNL Dynamics 365] API限制。 您必須確保資料與承載皆符合這些限制。

## 支援的身分 {#supported-identities}

[!DNL Dynamics 365]支援下表中描述的身分更新。 深入瞭解[身分](/help/identity-service/features/namespaces.md)。

| 目標身分 | 範例 | 說明 | 考量事項 |
|---|---|---|---|
| `contactid` | 7eb682f1-ca75-e511-80d4-00155d2a68d1 | 連絡人的唯一識別碼。 | **必要**。 如需詳細資訊，請參閱[[!DNL Dynamics 365] 檔案](https://docs.microsoft.com/en-us/dynamics365/customerengagement/on-premises/developer/entities/contact?view=op-9-1)。 |

{style="table-layout:auto"}

## 支援的對象 {#supported-audiences}

本節說明您可以匯出至此目的地的所有對象。

此目的地支援啟用所有透過Experience Platform [細分服務](../../../segmentation/home.md)產生的對象。

## 匯出型別和頻率 {#export-type-frequency}

請參閱下表以取得目的地匯出型別和頻率的資訊。

| 項目 | 類型 | 附註 |
---------|----------|---------|
| 匯出類型 | **[!UICONTROL 以設定檔為基礎]** | <ul><li>您正在匯出對象的所有成員，以及所需的結構描述欄位&#x200B;*（例如：電子郵件地址、電話號碼、姓氏）* （根據您的欄位對應）。</li><li> 根據[對象排程](#schedule-audience-export-example)步驟期間提供的&#x200B;**[!UICONTROL 對應ID]**&#x200B;值，[!DNL Dynamics 365]中的每個對象狀態都會以來自Experience Platform的對應對象狀態更新。</li></ul> |
| 匯出頻率 | **[!UICONTROL 串流]** | <ul><li>串流目的地是「一律開啟」的API型連線。 根據對象評估在Experience Platform中更新設定檔後，聯結器會立即將更新傳送至下游的目標平台。 深入瞭解[串流目的地](/help/destinations/destination-types.md#streaming-destinations)。</li></ul> |

{style="table-layout:auto"}

## 連線到目標 {#connect}

>[!IMPORTANT]
>
>若要連線到目的地，您需要&#x200B;**[!UICONTROL 檢視目的地]**&#x200B;和&#x200B;**[!UICONTROL 管理目的地]** [存取控制許可權](/help/access-control/home.md#permissions)。 閱讀[存取控制總覽](/help/access-control/ui/overview.md)或連絡您的產品管理員以取得必要的許可權。

若要連線到此目的地，請依照[目的地組態教學課程](../../ui/connect-destination.md)中所述的步驟進行。 在設定目標工作流程中，填寫以下兩個區段中列出的欄位。

在&#x200B;**[!UICONTROL 目的地]** > **[!UICONTROL 目錄]**&#x200B;內，搜尋[!DNL Dynamics 365]。 或者，您可以在&#x200B;**[!UICONTROL CRM]**&#x200B;類別下找到它。

### 驗證目標 {#authenticate}

若要驗證到目的地，請選取&#x200B;**[!UICONTROL 連線到目的地]**。
![Experience Platform UI熒幕擷圖顯示如何驗證。](../../assets/catalog/crm/microsoft-dynamics-365/authenticate-destination.png)

填寫以下必填欄位。 如需任何指引，請參閱[收集Dynamics 365認證](#gather-credentials)區段。
* **[!UICONTROL 使用者端識別碼]**： [!DNL Azure Active Directory]應用程式的[!DNL Dynamics 365]使用者端識別碼。
* **[!UICONTROL 租使用者識別碼]**：您[!DNL Azure Active Directory]應用程式的[!DNL Dynamics 365]租使用者識別碼。
* **[!UICONTROL 使用者端密碼]**：您[!DNL Azure Active Directory]應用程式的[!DNL Dynamics 365]使用者端密碼。
* **[!UICONTROL 地區]**：您的[[!DNL Dynamics 365]](https://learn.microsoft.com/en-us/power-platform/admin/new-datacenter-regions)地區。 例如：如果您的公司布建在北美(NAM)區域，則您的URL會是`crm.dynamics.com`，您需要選取`crm`。 如果您的公司已布建在加拿大(CAN)地區，則您的URL會是`crm3.dynamics.com`，您需要選取`crm3`。
* **[!UICONTROL 環境URL]**：您的[!DNL Dynamics 365]環境URL。

如果提供的詳細資料有效，UI會顯示帶有綠色勾號的&#x200B;**[!UICONTROL 已連線]**&#x200B;狀態。 然後您可以繼續下一步驟。

### 填寫目標詳細資訊 {#destination-details}

若要設定目的地的詳細資訊，請填寫下方的必填和選用欄位。 UI中欄位旁的星號表示該欄位為必填欄位。
![Experience Platform UI熒幕擷圖顯示目的地詳細資料。](../../assets/catalog/crm/microsoft-dynamics-365/destination-details.png)

* **[!UICONTROL 名稱]**：您日後可辨識此目的地的名稱。
* **[!UICONTROL 描述]**：可協助您日後識別此目的地的描述。
* **[!UICONTROL 自訂字首]**：您在[!DNL Dynamics 365]中建立的自訂欄位`Customization prefix`。 如需詳細資訊，請參閱[!DNL Dynamics 365]檔案的[建立及編輯欄位](https://learn.microsoft.com/en-us/dynamics365/customerengagement/on-premises/customize/create-edit-fields?view=op-9-1#create-and-edit-fields)區段。

### 啟用警示 {#enable-alerts}

您可以啟用警報以接收有關傳送到您目的地的資料流狀態的通知。 從清單中選取警報以訂閱接收有關資料流狀態的通知。 如需警示的詳細資訊，請參閱[使用UI訂閱目的地警示](../../ui/alerts.md)的指南。

當您完成提供目的地連線的詳細資訊後，請選取&#x200B;**[!UICONTROL 下一步]**。

## 啟動此目標的對象 {#activate}

>[!IMPORTANT]
> 
>* 若要啟用資料，您需要&#x200B;**[!UICONTROL 檢視目的地]**、**[!UICONTROL 啟用目的地]**、**[!UICONTROL 檢視設定檔]**&#x200B;和&#x200B;**[!UICONTROL 檢視區段]** [存取控制許可權](/help/access-control/home.md#permissions)。 閱讀[存取控制總覽](/help/access-control/ui/overview.md)或連絡您的產品管理員以取得必要的許可權。
>* 若要匯出&#x200B;*身分*，您需要&#x200B;**[!UICONTROL 檢視身分圖表]** [存取控制許可權](/help/access-control/home.md#permissions)。<br> ![選取工作流程中反白的身分名稱空間，以啟用目的地的對象。](/help/destinations/assets/overview/export-identities-to-destination.png "選取工作流程中反白顯示的身分名稱空間，以啟用目的地的對象。"){width="100" zoomable="yes"}

閱讀[將設定檔和對象啟用至串流對象匯出目的地](/help/destinations/ui/activate-segment-streaming-destinations.md)，以瞭解啟用此目的地對象的指示。

### 對應考量事項和範例 {#mapping-considerations-example}

若要將對象資料從Adobe Experience Platform正確傳送至[!DNL Dynamics 365]目的地，您必須完成欄位對應步驟。 對應包括在Experience Platform帳戶中的Experience Data Model (XDM)結構描述欄位與來自目標目的地的對應對應專案之間建立連結。 若要將您的XDM欄位正確對應到[!DNL Dynamics 365]目的地欄位，請遵循下列步驟：

1. 在&#x200B;**[!UICONTROL 對應]**&#x200B;步驟中，選取&#x200B;**[!UICONTROL 新增對應]**。 您會在畫面上看到新的對應列。
   ![新增對應之Experience Platform UI熒幕擷圖範例。](../../assets/catalog/crm/microsoft-dynamics-365/add-new-mapping.png)

1. 在&#x200B;**[!UICONTROL 選取來源欄位]**&#x200B;視窗中，選擇&#x200B;**[!UICONTROL 選取身分名稱空間]**&#x200B;類別並選取`contactid`。
   ![適用於Source對應的Experience Platform UI熒幕擷圖範例。](../../assets/catalog/crm/microsoft-dynamics-365/source-mapping.png)

1. 在&#x200B;**[!UICONTROL 選取目標欄位]**&#x200B;視窗中，選取您要將來源欄位對應到的目標欄位型別。
   * **[!UICONTROL 選取身分名稱空間]**：選取此選項可將您的來源欄位從清單對應至身分名稱空間。

     ![Experience Platform UI熒幕擷圖顯示連絡人的Target對應。](../../assets/catalog/crm/microsoft-dynamics-365/target-mapping-contactid.png)

   * 在您的XDM設定檔結構描述與[!DNL Dynamics 365]執行個體之間新增下列對應：

     | XDM設定檔結構描述 | [!DNL Dynamics 365]執行個體 | 強制 |
     |---|---|---|
     | `contactid` | `contactid` | 是 |

   * **[!UICONTROL 選取自訂屬性]**：選取此選項可將您的來源欄位對應到您在&#x200B;**[!UICONTROL 屬性名稱]**&#x200B;欄位中定義的自訂屬性。 如需支援屬性的完整清單，請參閱[[!DNL Dynamics 365] 檔案](https://docs.microsoft.com/en-us/dynamics365/customerengagement/on-premises/developer/entities/contact?view=op-9-1#entity-properties)。

     ![Experience Platform UI熒幕擷圖顯示電子郵件的Target對應。](../../assets/catalog/crm/microsoft-dynamics-365/target-mapping-email.png)

     >[!IMPORTANT]
     >
     > * 目標欄位名稱應在`lowercase`中。
     > * 此外，如果您有對應至[!DNL Dynamics 365] [日期或時間戳記](https://docs.microsoft.com/en-us/power-apps/developer/data-platform/webapi/reference/timestampdatemapping?view=dataverse-latest)目標欄位的日期或時間戳記來源欄位，請確定對應的值不是空的。 如果匯出的欄位值為空，您將會遇到&#x200B;*`Bad request reported while pushing events to the destination. Please contact the administrator and try again.`*&#x200B;錯誤訊息，而且將不會更新資料。 這是[!DNL Dynamics 365]限制。

   * 例如，根據您要更新的值，在您的XDM設定檔結構描述與[!DNL Dynamics 365]執行個體之間新增下列對應：

     | XDM設定檔結構描述 | [!DNL Dynamics 365]執行個體 |
     |---|---|
     | `person.name.firstName` | `firstname` |
     | `person.name.lastName` | `lastname` |
     | `personalEmail.address` | `emailaddress1` |

   * 以下顯示使用這些對應的範例：

   ![Experience Platform UI熒幕擷圖範例顯示Target對應。](../../assets/catalog/crm/microsoft-dynamics-365/mappings.png)

### 排程對象匯出和範例 {#schedule-audience-export-example}

在啟動工作流程的[[!UICONTROL 排程對象匯出]](/help/destinations/ui/activate-segment-streaming-destinations.md#scheduling)步驟中，您必須手動將Experience Platform對象對應到[!DNL Dynamics 365]中的自訂欄位屬性。

若要這麼做，請選取每個對象，然後在&#x200B;**[!UICONTROL 對應ID]**&#x200B;欄位中，從[!DNL Dynamics 365]輸入對應的自訂欄位屬性。

>[!IMPORTANT]
>
>用於&#x200B;**[!UICONTROL 對應ID]**&#x200B;的值應該與[!DNL Dynamics 365]內建立的自訂欄位屬性名稱完全相符。 如果您需要尋找自訂欄位屬性的指引，請參閱[[!DNL Dynamics 365] 檔案](https://docs.microsoft.com/en-us/dynamics365/customerengagement/on-premises/customize/create-edit-fields?view=op-9-1)。

範例如下：
![Experience Platform UI熒幕擷圖範例，顯示排程對象匯出。](../../assets/catalog/crm/microsoft-dynamics-365/schedule-segment-export.png)

## 驗證資料匯出 {#exported-data}

若要驗證您是否已正確設定目的地，請遵循下列步驟：

1. 選取&#x200B;**[!UICONTROL 目的地]** > **[!UICONTROL 瀏覽]**&#x200B;以瀏覽目的地清單。
   ![Experience Platform UI熒幕擷圖顯示瀏覽目的地。](../../assets/catalog/crm/microsoft-dynamics-365/browse-destinations.png)

1. 選取目的地並驗證狀態為&#x200B;**[!UICONTROL 已啟用]**。
   ![Experience Platform UI熒幕擷圖顯示目的地資料流執行。](../../assets/catalog/crm/microsoft-dynamics-365/destination-dataflow-run.png)

1. 切換至&#x200B;**[!DNL Activation data]**&#x200B;標籤，然後選取對象名稱。
   ![顯示目的地啟用資料的Experience Platform UI熒幕擷圖範例。](../../assets/catalog/crm/microsoft-dynamics-365/destinations-activation-data.png)

1. 監控對象摘要，並確保設定檔計數對應於在對象內建立的計數。
   ![顯示對象的Experience Platform UI熒幕擷圖範例。](../../assets/catalog/crm/microsoft-dynamics-365/segment.png)

1. 登入[!DNL Dynamics 365]網站，然後導覽至[!DNL Customers] > [!DNL Contacts]頁面，並檢查是否已新增對象的設定檔。 您可以看到根據[對象排程](#schedule-audience-export-example)步驟期間提供的&#x200B;**[!UICONTROL 對應ID]**&#x200B;值，[!DNL Dynamics 365]中的每個對象狀態已更新為Experience Platform中的對應對象狀態。
   ![Dynamics 365 UI熒幕擷取畫面顯示「連絡人」頁面，其對象狀態已更新。](../../assets/catalog/crm/microsoft-dynamics-365/contacts.png)

## 資料使用與控管 {#data-usage-governance}

處理您的資料時，所有[!DNL Adobe Experience Platform]目的地都符合資料使用原則。 如需[!DNL Adobe Experience Platform]如何強制資料控管的詳細資訊，請參閱[資料控管概觀](/help/data-governance/home.md)。

## 錯誤與疑難排解 {#errors-and-troubleshooting}

### 將事件推播到目的地時遇到未知錯誤 {#unknown-errors}

檢查資料流執行時，如果收到下列錯誤訊息： `Bad request reported while pushing events to the destination. Please contact the administrator and try again.`

![Experience Platform UI熒幕擷圖顯示錯誤請求錯誤。](../../assets/catalog/crm/microsoft-dynamics-365/error.png)

若要修正此錯誤，請確認您在[!DNL Dynamics 365]中為Experience Platform對象提供的&#x200B;**[!UICONTROL 對應ID]**&#x200B;有效且存在於[!DNL Dynamics 365]中。

## 其他資源 {#additional-resources}

[[!DNL Dynamics 365] 檔案](https://docs.microsoft.com/en-us/dynamics365/)的其他實用資訊如下：
* [IOrganizationService.Update(Entity)方法](https://docs.microsoft.com/en-us/dotnet/api/microsoft.xrm.sdk.iorganizationservice.update?view=dataverse-sdk-latest)
* [使用Web API更新及刪除資料表資料列](https://docs.microsoft.com/en-us/power-apps/developer/data-platform/webapi/update-delete-entities-using-web-api#basic-update)

### Changelog

本節擷取此目的地聯結器的功能和重要檔案更新。

+++ 檢視變更記錄檔

| 發行月份 | 更新型別 | 說明 |
|---|---|---|
| 2023 年 10 月 | 文件更新 | 已更新指引，在[對應考量事項和範例](#mapping-considerations-example)步驟中，指出所有目標屬性名稱應為小寫。 |
| 2023 年 8 月 | 功能和檔案更新 | 新增對未在[!DNL Dynamics 365]中預設方案內建立之自訂欄位的[!DNL Dynamics 365]自訂欄位首碼的支援。 已在[填寫目的地詳細資料](#destination-details)步驟中新增輸入欄位&#x200B;**[!UICONTROL 自訂字首]**。 (PLATIR-31602)。 |
| 2022年11 | 首次發行 | 初始目的地版本和檔案發佈。 |

{style="table-layout:auto"}

+++