---
keywords: crm;CRM;CRM目標；Microsoft Dynamics 365;Microsoft Dynamics 365 crm目標
title: Microsoft Dynamics 365連線
description: Microsoft Dynamics 365目的地可讓您匯出帳戶資料，並在Microsoft Dynamics 365中根據您的業務需求啟用它。
last-substantial-update: 2022-11-08T00:00:00Z
exl-id: 49bb5c95-f4b7-42e1-9aae-45143bbb1d73
source-git-commit: 83778bc5d643f69e0393c0a7767fef8a4e8f66e9
workflow-type: tm+mt
source-wordcount: '1787'
ht-degree: 0%

---

# [!DNL Microsoft Dynamics 365] 連接

## 總覽 {#overview}

[[!DNL Microsoft Dynamics 365]](https://dynamics.microsoft.com/en-us/) 是基於雲的業務應用程式平台，它將企業資源規劃(ERP)和客戶關係管理(CRM)與生產力應用程式和AI工具結合在一起，實現端到端更流暢、更受控的操作、更好的增長潛力和降低成本。

此 [!DNL Adobe Experience Platform] [目的地](/help/destinations/home.md) 利用 [[!DNL Contact Entity Reference API]](https://docs.microsoft.com/en-us/dynamics365/customerengagement/on-premises/developer/entities/contact?view=op-9-1)，可讓您將區段內的身分識別更新至 [!DNL Dynamics 365].

[!DNL Dynamics 365] 使用OAuth 2搭配授權授權作為驗證機制，與 [!DNL Contact Entity Reference API]. 向您的 [!DNL Dynamics 365] 執行個體在下方， [驗證到目標](#authenticate) 區段。

## 使用案例 {#use-cases}

身為行銷人員，您可以根據使用者Adobe Experience Platform設定檔的屬性，為使用者提供個人化體驗。 您可以從離線資料建立區段，並將這些區段傳送至 [!DNL Dynamics 365]，可在Adobe Experience Platform中更新區段和設定檔時，立即顯示在使用者的動態消息中。

## 先決條件 {#prerequisites}

### Experience Platform必要條件 {#prerequisites-in-experience-platform}

在將資料啟用至 [!DNL Dynamics 365] 目的地，您必須 [綱要](/help/xdm/schema/composition.md), [資料集](https://experienceleague.adobe.com/docs/platform-learn/tutorials/data-ingestion/create-datasets-and-ingest-data.html?lang=en)，和 [區段](https://experienceleague.adobe.com/docs/platform-learn/tutorials/segments/create-segments.html?lang=en) 建立於 [!DNL Experience Platform].

如需相關資訊，請參閱Adobe的檔案 [區段成員資格詳細資料結構欄位群組](/help/xdm/field-groups/profile/segmentation.md) 如果您需要區段狀態的指引。

### [!DNL Microsoft Dynamics 365] 必要條件 {#prerequisites-destination}

請注意下列必要條件，位於 [!DNL Dynamics 365]，以便將資料從Platform匯出至 [!DNL Dynamics 365] 帳戶：

#### 你需要 [!DNL Microsoft Dynamics 365] 帳戶 {#prerequisites-account}

前往 [!DNL Dynamics 365] [審判](https://dynamics.microsoft.com/en-us/dynamics-365-free-trial/) 頁面來註冊和建立帳戶（如果尚未建立帳戶）。

#### 在中建立欄位 [!DNL Dynamics 365] {#prerequisites-custom-field}

建立類型的自訂欄位 `Simple` 欄位資料類型為 `Single Line of Text` 哪個Experience Platform將用來更新內的區段狀態 [!DNL Dynamics 365].
請參閱 [!DNL Dynamics 365] 檔案 [建立欄位（屬性）](https://docs.microsoft.com/en-us/dynamics365/customerengagement/on-premises/customize/create-edit-fields?view=op-9-1) 如果您需要其他指導。

內的範例設定 [!DNL Dynamics 365] 如下所示：
![Dynamics 365 UI螢幕截圖顯示自訂欄位。](../../assets/catalog/crm/microsoft-dynamics-365/dynamics-365-fields.png)

#### 在Azure Active Directory中註冊應用程式和應用程式用戶 {#prerequisites-app-user}

啟用 [!DNL Dynamics 365] 若要存取您需要的資源，請使用 [!DNL Azure Account] to [[!DNL Azure Active Directory]](https://docs.microsoft.com/en-us/azure/active-directory/develop/howto-create-service-principal-portal#register-an-application-with-azure-ad-and-create-a-service-principal) 並建立下列項目：
* 安 [!DNL Azure Active Directory] 應用程式
* 服務主體
* 應用程式密碼

您還需要 [建立應用程式使用者](https://docs.microsoft.com/en-us/power-platform/admin/manage-application-users#create-an-application-user) in [!DNL Azure Active Directory] 並將其與新建立的應用程式關聯。

#### 收集 [!DNL Dynamics 365] 憑據 {#gather-credentials}

在驗證之前，請記下下列項目 [!DNL Dynamics 365] CRM目標：

| 憑據 | 說明 | 範例 |
| --- | --- | --- |
| `Client ID` | 此 [!DNL Dynamics 365] 用戶端ID [!DNL Azure Active Directory] 應用程式。 請參閱 [[!DNL Dynamics 365] 檔案](https://docs.microsoft.com/en-us/azure/active-directory/develop/howto-create-service-principal-portal#get-tenant-and-app-id-values-for-signing-in) 以取得指引。 | `ababbaba-abab-baba-acac-acacacacacac` |
| `Client Secret` | 此 [!DNL Dynamics 365] 您 [!DNL Azure Active Directory] 應用程式。 您會在 [[!DNL Dynamics 365] 檔案](https://docs.microsoft.com/en-us/azure/active-directory/develop/howto-create-service-principal-portal#authentication-two-options). | `abcde~abcdefghijklmnopqrstuvwxyz12345678` 以取得指引。 |
| `Tenant ID` | 此 [!DNL Dynamics 365] 您 [!DNL Azure Active Directory] 應用程式。 請參閱 [[!DNL Dynamics 365] 檔案](https://docs.microsoft.com/en-us/azure/active-directory/develop/howto-create-service-principal-portal#get-tenant-and-app-id-values-for-signing-in) 以取得指引。 | `1234567-aaaa-12ab-ba21-1234567890` |
| `Environment URL` | 請參閱 [[!DNL Dynamics 365] 檔案](https://docs.microsoft.com/en-us/dynamics365/customerengagement/on-premises/developer/org-service/discover-url-organization-organization-service?view=op-9-1) 以取得指引。 | 若您的 [!DNL Dynamics 365] 網域如下所示，您需要醒目提示的值。<br> *`org57771b33`.crm.dynamics.com* |

## 護欄 {#guardrails}

此 [請求限制和分配](https://docs.microsoft.com/en-us/power-platform/admin/api-request-limits-allocations) 頁面詳細資訊 [!DNL Dynamics 365] 與您的 [!DNL Dynamics 365] 授權。 您必須確定您的資料和裝載符合這些限制。

## 支援的身分 {#supported-identities}

[!DNL Dynamics 365] 支援下表所述的身分識別更新。 深入了解 [身分](/help/identity-service/namespaces.md).

| Target身分 | 範例 | 說明 | 考量事項 |
|---|---|---|---|
| `contactId` | 7eb682f1-ca75-e511-80d4-00155d2a68d1 | 聯繫人的唯一標識符。 | **必要**. 請參閱 [[!DNL Dynamics 365] 檔案](https://docs.microsoft.com/en-us/dynamics365/customerengagement/on-premises/developer/entities/contact?view=op-9-1) 以取得詳細資訊。 |

## 匯出類型和頻率 {#export-type-frequency}

有關目標導出類型和頻率的資訊，請參閱下表。

| 項目 | 類型 | 附註 |
---------|----------|---------|
| 匯出類型 | **[!UICONTROL 設定檔]** | <ul><li>您要匯出區段的所有成員，以及所需的結構欄位 *(例如：電子郵件地址、電話號碼、姓氏)*，根據您的欄位對應。</li><li> 中的每個區段狀態 [!DNL Dynamics 365] 會根據 **[!UICONTROL 對應ID]** 值 [區段排程](#schedule-segment-export-example) 步驟。</li></ul> |
| 匯出頻率 | **[!UICONTROL 串流]** | <ul><li>串流目的地是「一律開啟」API型連線。 一旦根據區段評估在Experience Platform中更新設定檔，連接器就會將更新傳送至下游的目的地平台。 深入了解 [串流目的地](/help/destinations/destination-types.md#streaming-destinations).</li></ul> |

{style="table-layout:auto"}

## 連接到目標 {#connect}

>[!IMPORTANT]
>
>若要連線至目的地，您需要 **[!UICONTROL 管理目的地]** [存取控制權限](/help/access-control/home.md#permissions). 閱讀 [存取控制概觀](/help/access-control/ui/overview.md) 或聯絡您的產品管理員以取得所需的權限。

若要連線至此目的地，請依照 [目的地設定教學課程](../../ui/connect-destination.md). 在設定目標工作流程中，填寫下列兩節所列的欄位。

內 **[!UICONTROL 目的地]** > **[!UICONTROL 目錄]** 搜尋 [!DNL Dynamics 365]. 或者，您也可以在 **[!UICONTROL CRM]** 類別。

### 驗證到目標 {#authenticate}

要驗證到目標，請選擇 **[!UICONTROL 連接到目標]**.
![Platform UI螢幕擷取畫面，顯示如何驗證。](../../assets/catalog/crm/microsoft-dynamics-365/authenticate-destination.png)

填寫下方的必填欄位。 請參閱 [收集Dynamics 365憑證](#gather-credentials) 區段。
* **[!UICONTROL 用戶端ID]**:此 [!DNL Dynamics 365] 用戶端ID [!DNL Azure Active Directory] 應用程式。
* **[!UICONTROL 租用戶ID]**:此 [!DNL Dynamics 365] 您 [!DNL Azure Active Directory] 應用程式。
* **[!UICONTROL 用戶端密碼]**:此 [!DNL Dynamics 365] 您 [!DNL Azure Active Directory] 應用程式。
* **[!UICONTROL 環境URL]**:您的 [!DNL Dynamics 365] 環境URL。

如果提供的詳細資料有效，UI會顯示 **[!UICONTROL 已連接]** 狀態（帶綠色複選標籤）。 接著，您可以繼續進行下一個步驟。

### 填寫目的地詳細資訊 {#destination-details}

若要設定目的地的詳細資訊，請填寫下方的必填和選填欄位。 UI中欄位旁的星號表示該欄位為必要欄位。
![Platform UI螢幕擷取畫面，顯示目的地詳細資訊。](../../assets/catalog/crm/microsoft-dynamics-365/destination-details.png)

* **[!UICONTROL 名稱]**:日後您將透過此名稱識別此目的地。
* **[!UICONTROL 說明]**:未來可協助您識別此目的地的說明。

### 啟用警報 {#enable-alerts}

您可以啟用警報，接收有關資料流到目標狀態的通知。 從清單中選擇要訂閱的警報，以接收有關資料流狀態的通知。 如需警報的詳細資訊，請參閱 [使用UI訂閱目的地警報](../../ui/alerts.md).

完成提供目標連接的詳細資訊後，請選擇 **[!UICONTROL 下一個]**.

## 啟用此目的地的區段 {#activate}

>[!IMPORTANT]
>
>若要啟用資料，您需要 **[!UICONTROL 管理目的地]**, **[!UICONTROL 啟動目的地]**, **[!UICONTROL 檢視設定檔]**，和 **[!UICONTROL 檢視區段]** [存取控制權限](/help/access-control/home.md#permissions). 閱讀 [存取控制概觀](/help/access-control/ui/overview.md) 或聯絡您的產品管理員以取得所需的權限。

閱讀 [啟動設定檔和區段至串流區段匯出目的地](/help/destinations/ui/activate-segment-streaming-destinations.md) 以取得啟用受眾區段至此目的地的指示。

### 對應考量事項和範例 {#mapping-considerations-example}

若要將您的對象資料從Adobe Experience Platform正確傳送至 [!DNL Dynamics 365] 目的地，您必須執行欄位對應步驟。 對應包含在您的Platform帳戶中的Experience Data Model(XDM)結構欄位與目標目的地對應的欄位之間建立連結。 若要正確將XDM欄位對應至 [!DNL Dynamics 365] 目標欄位，請遵循下列步驟：

1. 在 **[!UICONTROL 對應]** 步驟，選取 **[!UICONTROL 新增對應]**. 畫面上會顯示新的對應列。
   ![Platform UI新增對應的螢幕擷取範例。](../../assets/catalog/crm/microsoft-dynamics-365/add-new-mapping.png)

1. 在 **[!UICONTROL 選擇源欄位]** 窗口，選擇 **[!UICONTROL 選取身分命名空間]** 類別和選取 `contactId`.
   ![Platform UI的來源對應螢幕擷取範例。](../../assets/catalog/crm/microsoft-dynamics-365/source-mapping.png)

1. 在 **[!UICONTROL 選擇目標欄位]** 視窗中，選取您要將來源欄位對應至的目標欄位類型。
   * **[!UICONTROL 選取身分命名空間]**:選擇此選項可將源欄位從清單映射到標識命名空間。
      ![平台UI螢幕擷取畫面，顯示contactId的Target對應。](../../assets/catalog/crm/microsoft-dynamics-365/target-mapping-contactid.png)

   * 在XDM設定檔架構與 [!DNL Dynamics 365] 例項： |XDM配置檔案架構|[!DNL Dynamics 365] Instance|強制| |—|—|—| |`contactId`|`contactId`|是 |

   * **[!UICONTROL 選取自訂屬性]**:選擇此選項可將源欄位映射到您在 **[!UICONTROL 屬性名稱]** 欄位。 請參閱 [[!DNL Dynamics 365] 檔案](https://docs.microsoft.com/en-us/dynamics365/customerengagement/on-premises/developer/entities/contact?view=op-9-1#entity-properties) 以取得支援屬性的完整清單。
      ![平台UI螢幕擷圖，顯示LastName的Target對應。](../../assets/catalog/crm/microsoft-dynamics-365/target-mapping-lastname.png)

      >[!IMPORTANT]
      >
      >如果您有對應至的日期或時間戳記來源欄位 [!DNL Dynamics 365] [日期或時間戳記](https://docs.microsoft.com/en-us/power-apps/developer/data-platform/webapi/reference/timestampdatemapping?view=dataverse-latest) 目標欄位，請確定映射的值不是空的。 如果傳遞的值空白，您會遇到 *`Bad request reported while pushing events to the destination. Please contact the administrator and try again.`* 錯誤訊息，且資料將不會更新。 這是 [!DNL Dynamics 365] 限制。

   * 例如，根據您要更新的值，在XDM設定檔架構與 [!DNL Dynamics 365] 例項： |XDM配置檔案架構|[!DNL Dynamics 365] 例項| |—|—| |`person.name.firstName`|`FirstName`| |`person.name.lastName`|`LastName`| |`personalEmail.address`|`Email`|

   * 使用這些對應的範例如下所示：
      ![Platform UI螢幕擷取範例，顯示Target對應。](../../assets/catalog/crm/microsoft-dynamics-365/mappings.png)

### 排程區段匯出和範例 {#schedule-segment-export-example}

在 [[!UICONTROL 排程區段匯出]](/help/destinations/ui/activate-segment-streaming-destinations.md#scheduling) 在啟動工作流程的步驟中，您必須手動將Platform區段對應至 [!DNL Dynamics 365].

若要這麼做，請選取每個區段，然後輸入 [!DNL Dynamics 365] 在 **[!UICONTROL 對應ID]** 欄位。

>[!IMPORTANT]
>
>用於 **[!UICONTROL 對應ID]** 應完全符合中建立的自訂欄位屬性名稱 [!DNL Dynamics 365]. 請參閱 [[!DNL Dynamics 365] 檔案](https://docs.microsoft.com/en-us/dynamics365/customerengagement/on-premises/customize/create-edit-fields?view=op-9-1) 如果您需要尋找自訂欄位屬性的指引。

以下是範例：
![Platform UI螢幕擷取範例，顯示「排程區段」匯出。](../../assets/catalog/crm/microsoft-dynamics-365/schedule-segment-export.png)

## 驗證資料匯出 {#exported-data}

若要驗證您是否已正確設定目的地，請遵循下列步驟：

1. 選擇 **[!UICONTROL 目的地]** > **[!UICONTROL 瀏覽]** 導覽至目的地清單。
   ![顯示「瀏覽目的地」的Platform UI螢幕擷圖。](../../assets/catalog/crm/microsoft-dynamics-365/browse-destinations.png)

1. 選取目標並驗證狀態為 **[!UICONTROL 已啟用]**.
   ![Platform UI螢幕擷圖，顯示「目的地資料流執行」。](../../assets/catalog/crm/microsoft-dynamics-365/destination-dataflow-run.png)

1. 切換至 **[!DNL Activation data]** ，然後選取區段名稱。
   ![Platform UI螢幕擷取範例，顯示「目的地啟動資料」。](../../assets/catalog/crm/microsoft-dynamics-365/destinations-activation-data.png)

1. 監控區段摘要，並確保設定檔計數與區段內建立的計數相對應。
   ![Platform UI螢幕擷取範例，顯示「區段」。](../../assets/catalog/crm/microsoft-dynamics-365/segment.png)

1. 登入 [!DNL Dynamics 365] 網站，然後導覽至 [!DNL Customers] > [!DNL Contacts] 頁面，並檢查區段中的設定檔是否已新增。 您可以在 [!DNL Dynamics 365] 已根據 **[!UICONTROL 對應ID]** 值 [區段排程](#schedule-segment-export-example) 步驟。
   ![Dynamics 365 UI螢幕截圖顯示具有更新段狀態的「聯繫人」頁。](../../assets/catalog/crm/microsoft-dynamics-365/contacts.png)

## 資料使用與控管 {#data-usage-governance}

全部 [!DNL Adobe Experience Platform] 處理資料時，目的地符合資料使用原則。 有關如何 [!DNL Adobe Experience Platform] 強制實施資料控管，請參閱 [資料控管概觀](/help/data-governance/home.md).

## 錯誤和疑難排解 {#errors-and-troubleshooting}

### 將事件推送至目的地時發生未知錯誤 {#unknown-errors}

檢查資料流運行時，如果您收到以下錯誤消息： `Bad request reported while pushing events to the destination. Please contact the administrator and try again.`

![Platform UI螢幕擷取畫面顯示「錯誤請求」錯誤。](../../assets/catalog/crm/microsoft-dynamics-365/error.png)

若要修正此錯誤，請確認 **[!UICONTROL 對應ID]** 您在 [!DNL Dynamics 365] 因為您的平台區段有效且存在於 [!DNL Dynamics 365].

## 其他資源 {#additional-resources}

來自 [[!DNL Dynamics 365] 檔案](https://docs.microsoft.com/en-us/dynamics365/) 如下所示：
* [IOrganizationService.Update(Entity)方法](https://docs.microsoft.com/en-us/dotnet/api/microsoft.xrm.sdk.iorganizationservice.update?view=dataverse-sdk-latest)
* [使用Web API更新和刪除表格列](https://docs.microsoft.com/en-us/power-apps/developer/data-platform/webapi/update-delete-entities-using-web-api#basic-update)
