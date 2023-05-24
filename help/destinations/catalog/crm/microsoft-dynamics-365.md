---
keywords: crm;CRM;CRM目標；MicrosoftDynamics 365;MicrosoftDynamics 365 crm目標
title: Microsoft動力365連接
description: MicrosoftDynamics 365目標允許您導出帳戶資料並在MicrosoftDynamics 365中根據您的業務需要激活它。
last-substantial-update: 2022-11-08T00:00:00Z
exl-id: 49bb5c95-f4b7-42e1-9aae-45143bbb1d73
source-git-commit: 83778bc5d643f69e0393c0a7767fef8a4e8f66e9
workflow-type: tm+mt
source-wordcount: '1787'
ht-degree: 0%

---

# [!DNL Microsoft Dynamics 365] 連接

## 總覽 {#overview}

[[!DNL Microsoft Dynamics 365]](https://dynamics.microsoft.com/en-us/) 是一個基於雲的業務應用平台，它將企業資源規劃(ERP)和客戶關係管理(CRM)與生產力應用程式和AI工具相結合，以帶來端對端更平穩、更受控的操作、更好的增長潛力和降低的成本。

此 [!DNL Adobe Experience Platform] [目標](/help/destinations/home.md) 利用 [[!DNL Contact Entity Reference API]](https://docs.microsoft.com/en-us/dynamics365/customerengagement/on-premises/developer/entities/contact?view=op-9-1)，允許您將段內的標識更新到 [!DNL Dynamics 365]。

[!DNL Dynamics 365] 使用OAuth 2和授權授權作為與 [!DNL Contact Entity Reference API]。 驗證到您 [!DNL Dynamics 365] 下面是實例， [驗證到目標](#authenticate) 的子菜單。

## 使用案例 {#use-cases}

作為營銷人員，您可以根據用戶的Adobe Experience Platform配置檔案的屬性向用戶提供個性化體驗。 您可以從離線資料構建段，並將這些段發送到 [!DNL Dynamics 365]，在Adobe Experience Platform更新段和配置檔案後立即在用戶源中顯示。

## 先決條件 {#prerequisites}

### Experience Platform先決條件 {#prerequisites-in-experience-platform}

在將資料激活到 [!DNL Dynamics 365] 目標，您必須 [架構](/help/xdm/schema/composition.md)的 [資料集](https://experienceleague.adobe.com/docs/platform-learn/tutorials/data-ingestion/create-datasets-and-ingest-data.html?lang=en), [段](https://experienceleague.adobe.com/docs/platform-learn/tutorials/segments/create-segments.html?lang=en) 建立 [!DNL Experience Platform]。

請參閱Adobe的文檔，瞭解 [段成員身份詳細資訊架構欄位組](/help/xdm/field-groups/profile/segmentation.md) 如果需要有關段狀態的指導。

### [!DNL Microsoft Dynamics 365] 先決條件 {#prerequisites-destination}

請注意以下先決條件 [!DNL Dynamics 365]，以便將資料從平台導出到 [!DNL Dynamics 365] 帳戶：

#### 你需要 [!DNL Microsoft Dynamics 365] 帳戶 {#prerequisites-account}

轉到 [!DNL Dynamics 365] [審判](https://dynamics.microsoft.com/en-us/dynamics-365-free-trial/) 頁，以註冊和建立帳戶。

#### 在中建立欄位 [!DNL Dynamics 365] {#prerequisites-custom-field}

建立類型的自定義欄位 `Simple` 將欄位資料類型設定為 `Single Line of Text` 該Experience Platform將用於更新 [!DNL Dynamics 365]。
請參閱 [!DNL Dynamics 365] 文檔 [建立欄位（屬性）](https://docs.microsoft.com/en-us/dynamics365/customerengagement/on-premises/customize/create-edit-fields?view=op-9-1) 如果你需要其他指導。

中的示例設定 [!DNL Dynamics 365] 如下所示：
![顯示自定義欄位的Dynamics 365 UI螢幕快照。](../../assets/catalog/crm/microsoft-dynamics-365/dynamics-365-fields.png)

#### 在Azure Active Directory中註冊應用程式和應用程式用戶 {#prerequisites-app-user}

啟用 [!DNL Dynamics 365] 訪問您需要登錄的資源 [!DNL Azure Account] 至 [[!DNL Azure Active Directory]](https://docs.microsoft.com/en-us/azure/active-directory/develop/howto-create-service-principal-portal#register-an-application-with-azure-ad-and-create-a-service-principal) 並建立以下內容：
* 安 [!DNL Azure Active Directory] 應用
* 服務主體
* 應用程式機密

您還需要 [建立應用程式用戶](https://docs.microsoft.com/en-us/power-platform/admin/manage-application-users#create-an-application-user) 在 [!DNL Azure Active Directory] 並將其與新建立的應用程式關聯。

#### 收集 [!DNL Dynamics 365] 憑據 {#gather-credentials}

在驗證到 [!DNL Dynamics 365] CRM目標：

| 憑據 | 說明 | 範例 |
| --- | --- | --- |
| `Client ID` | 的 [!DNL Dynamics 365] 您的客戶端ID [!DNL Azure Active Directory] 的子菜單。 請參閱 [[!DNL Dynamics 365] 文檔](https://docs.microsoft.com/en-us/azure/active-directory/develop/howto-create-service-principal-portal#get-tenant-and-app-id-values-for-signing-in) 的上界。 | `ababbaba-abab-baba-acac-acacacacacac` |
| `Client Secret` | 的 [!DNL Dynamics 365] 您的客戶端密碼 [!DNL Azure Active Directory] 的子菜單。 您將在 [[!DNL Dynamics 365] 文檔](https://docs.microsoft.com/en-us/azure/active-directory/develop/howto-create-service-principal-portal#authentication-two-options)。 | `abcde~abcdefghijklmnopqrstuvwxyz12345678` 的上界。 |
| `Tenant ID` | 的 [!DNL Dynamics 365] 您的租戶ID [!DNL Azure Active Directory] 的子菜單。 請參閱 [[!DNL Dynamics 365] 文檔](https://docs.microsoft.com/en-us/azure/active-directory/develop/howto-create-service-principal-portal#get-tenant-and-app-id-values-for-signing-in) 的上界。 | `1234567-aaaa-12ab-ba21-1234567890` |
| `Environment URL` | 請參閱 [[!DNL Dynamics 365] 文檔](https://docs.microsoft.com/en-us/dynamics365/customerengagement/on-premises/developer/org-service/discover-url-organization-organization-service?view=op-9-1) 的上界。 | 如果 [!DNL Dynamics 365] 域如下所示，您需要突出顯示的值。<br> *`org57771b33`.crm.dynamics.com* |

## 護欄 {#guardrails}

的 [請求限制和分配](https://docs.microsoft.com/en-us/power-platform/admin/api-request-limits-allocations) 頁面詳細資訊 [!DNL Dynamics 365] 與您的 [!DNL Dynamics 365] 許可證。 您需要確保您的資料和負載在這些限制範圍內。

## 支援的身份 {#supported-identities}

[!DNL Dynamics 365] 支援更新下表中描述的身份。 瞭解有關 [身份](/help/identity-service/namespaces.md)。

| 目標標識 | 範例 | 說明 | 考量事項 |
|---|---|---|---|
| `contactId` | 7eb682f1-ca75-e511-80d4-00155d2a68d1 | 聯繫人的唯一標識符。 | **必要**. 請參閱 [[!DNL Dynamics 365] 文檔](https://docs.microsoft.com/en-us/dynamics365/customerengagement/on-premises/developer/entities/contact?view=op-9-1) 的上界。 |

## 導出類型和頻率 {#export-type-frequency}

有關目標導出類型和頻率的資訊，請參閱下表。

| 項目 | 類型 | 附註 |
---------|----------|---------|
| 導出類型 | **[!UICONTROL 基於配置檔案]** | <ul><li>您正在導出段的所有成員以及所需的架構欄位 *(例如：電子郵件地址、電話號碼、姓氏)*，根據您的欄位映射。</li><li> 中的每個段狀態 [!DNL Dynamics 365] 將根據 **[!UICONTROL 映射ID]** 值 [段調度](#schedule-segment-export-example) 的子菜單。</li></ul> |
| 導出頻率 | **[!UICONTROL 流]** | <ul><li>流目標是基於API的「始終開啟」連接。 一旦基於段評估在Experience Platform中更新配置檔案，連接器就將更新下游發送到目標平台。 閱讀有關 [流目標](/help/destinations/destination-types.md#streaming-destinations)。</li></ul> |

{style="table-layout:auto"}

## 連接到目標 {#connect}

>[!IMPORTANT]
>
>要連接到目標，您需要 **[!UICONTROL 管理目標]** [訪問控制權限](/help/access-control/home.md#permissions)。 閱讀 [訪問控制概述](/help/access-control/ui/overview.md) 或聯繫您的產品管理員以獲取所需權限。

要連接到此目標，請按照 [目標配置教程](../../ui/connect-destination.md)。 在配置目標工作流中，填寫下面兩節中列出的欄位。

在 **[!UICONTROL 目標]** > **[!UICONTROL 目錄]** 搜索 [!DNL Dynamics 365]。 或者，可將其定位在 **[!UICONTROL CRM]** 的子菜單。

### 驗證到目標 {#authenticate}

要驗證到目標，請選擇 **[!UICONTROL 連接到目標]**。
![平台UI螢幕快照，顯示如何進行身份驗證。](../../assets/catalog/crm/microsoft-dynamics-365/authenticate-destination.png)

填寫下面的必填欄位。 請參閱 [收集Dynamics 365憑據](#gather-credentials) 的雙曲餘切值。
* **[!UICONTROL 客戶端ID]**:的 [!DNL Dynamics 365] 您的客戶端ID [!DNL Azure Active Directory] 的子菜單。
* **[!UICONTROL 租戶ID]**:的 [!DNL Dynamics 365] 您的租戶ID [!DNL Azure Active Directory] 的子菜單。
* **[!UICONTROL 客戶端密碼]**:的 [!DNL Dynamics 365] 您的客戶端密碼 [!DNL Azure Active Directory] 的子菜單。
* **[!UICONTROL 環境URL]**:您 [!DNL Dynamics 365] 環境URL。

如果提供的詳細資訊有效，UI將顯示 **[!UICONTROL 已連接]** 狀態為綠色複選標籤。 然後，可以繼續下一步。

### 填寫目標詳細資訊 {#destination-details}

要配置目標的詳細資訊，請填寫以下必需欄位和可選欄位。 UI中某個欄位旁邊的星號表示該欄位是必需的。
![顯示目標詳細資訊的平台UI螢幕快照。](../../assets/catalog/crm/microsoft-dynamics-365/destination-details.png)

* **[!UICONTROL 名稱]**:您將來識別此目標的名稱。
* **[!UICONTROL 說明]**:將幫助您在將來確定此目標的說明。

### 啟用警報 {#enable-alerts}

您可以啟用警報來接收有關目標資料流狀態的通知。 從清單中選擇要訂閱的警報以接收有關資料流狀態的通知。 有關警報的詳細資訊，請參閱上的指南 [使用UI訂閱目標警報](../../ui/alerts.md)。

完成提供目標連接的詳細資訊後，選擇 **[!UICONTROL 下一個]**。

## 將段激活到此目標 {#activate}

>[!IMPORTANT]
>
>要激活資料，您需要 **[!UICONTROL 管理目標]**。 **[!UICONTROL 激活目標]**。 **[!UICONTROL 查看配置檔案]**, **[!UICONTROL 查看段]** [訪問控制權限](/help/access-control/home.md#permissions)。 閱讀 [訪問控制概述](/help/access-control/ui/overview.md) 或聯繫您的產品管理員以獲取所需權限。

閱讀 [激活配置檔案和段以流式處理段導出目標](/help/destinations/ui/activate-segment-streaming-destinations.md) 有關激活此目標受眾段的說明。

### 映射注意事項和示例 {#mapping-considerations-example}

正確將您的受眾資料從Adobe Experience Platform發送到 [!DNL Dynamics 365] 目標，您需要完成欄位映射步驟。 映射包括在您的平台帳戶中的「體驗資料模型」(XDM)架構欄位與目標目標中對應的欄位之間建立連結。 正確將XDM欄位映射到 [!DNL Dynamics 365] 目標欄位，請執行以下步驟：

1. 在 **[!UICONTROL 映射]** 步驟，選擇 **[!UICONTROL 添加新映射]**。 螢幕上將顯示新的映射行。
   ![「添加新映射」的平台UI螢幕快照示例。](../../assets/catalog/crm/microsoft-dynamics-365/add-new-mapping.png)

1. 在 **[!UICONTROL 選擇源欄位]** ，選擇 **[!UICONTROL 選擇標識命名空間]** 選擇 `contactId`。
   ![Platform UI源映射的螢幕快照示例。](../../assets/catalog/crm/microsoft-dynamics-365/source-mapping.png)

1. 在 **[!UICONTROL 選擇目標欄位]** 窗口，選擇要將源欄位映射到的目標欄位的類型。
   * **[!UICONTROL 選擇標識命名空間]**:選擇此選項可將源欄位從清單中映射到標識命名空間。
      ![平台UI螢幕快照，顯示contactId的目標映射。](../../assets/catalog/crm/microsoft-dynamics-365/target-mapping-contactid.png)

   * 在XDM配置檔案架構和 [!DNL Dynamics 365] 實例： |XDM配置檔案架構|[!DNL Dynamics 365] 實例|強制| |—|—| |`contactId`|`contactId`|是 |

   * **[!UICONTROL 選擇自定義屬性]**:選擇此選項可將源欄位映射到您在中定義的自定義屬性 **[!UICONTROL 屬性名稱]** 的子菜單。 請參閱 [[!DNL Dynamics 365] 文檔](https://docs.microsoft.com/en-us/dynamics365/customerengagement/on-premises/developer/entities/contact?view=op-9-1#entity-properties) 的子菜單。
      ![平台UI螢幕快照，顯示LastName的目標映射。](../../assets/catalog/crm/microsoft-dynamics-365/target-mapping-lastname.png)

      >[!IMPORTANT]
      >
      >如果有映射到的日期或時間戳源欄位 [!DNL Dynamics 365] [日期或時間戳](https://docs.microsoft.com/en-us/power-apps/developer/data-platform/webapi/reference/timestampdatemapping?view=dataverse-latest) 目標欄位，確保映射的值不為空。 如果傳遞的值為空，您將遇到 *`Bad request reported while pushing events to the destination. Please contact the administrator and try again.`* 錯誤消息，資料將不會更新。 這是 [!DNL Dynamics 365] 限制。

   * 例如，根據要更新的值，在XDM配置檔案架構和XDM配置檔案架構之間添加以下映射 [!DNL Dynamics 365] 實例： |XDM配置檔案架構|[!DNL Dynamics 365] 實例| |—| |`person.name.firstName`|`FirstName`| |`person.name.lastName`|`LastName`| |`personalEmail.address`|`Email`|

   * 下面顯示了使用這些映射的示例：
      ![平台UI螢幕快照示例，顯示目標映射。](../../assets/catalog/crm/microsoft-dynamics-365/mappings.png)

### 計畫段導出和示例 {#schedule-segment-export-example}

在 [[!UICONTROL 計畫段導出]](/help/destinations/ui/activate-segment-streaming-destinations.md#scheduling) 在激活工作流的步驟中，必須手動將平台段映射到中的自定義欄位屬性 [!DNL Dynamics 365]。

為此，請選擇每個段，然後輸入相應的自定義欄位屬性 [!DNL Dynamics 365] 的 **[!UICONTROL 映射ID]** 的子菜單。

>[!IMPORTANT]
>
>用於 **[!UICONTROL 映射ID]** 應與在中建立的自定義欄位屬性的名稱完全匹配 [!DNL Dynamics 365]。 請參閱 [[!DNL Dynamics 365] 文檔](https://docs.microsoft.com/en-us/dynamics365/customerengagement/on-premises/customize/create-edit-fields?view=op-9-1) 。

下面顯示了一個示例：
![平台UI螢幕快照示例，顯示「計畫」段導出。](../../assets/catalog/crm/microsoft-dynamics-365/schedule-segment-export.png)

## 驗證資料導出 {#exported-data}

要驗證您是否正確設定了目標，請執行以下步驟：

1. 選擇 **[!UICONTROL 目標]** > **[!UICONTROL 瀏覽]** 導航至目標清單。
   ![顯示「瀏覽目標」的平台UI螢幕快照。](../../assets/catalog/crm/microsoft-dynamics-365/browse-destinations.png)

1. 選擇目標並驗證狀態是否為 **[!UICONTROL 啟用]**。
   ![顯示目標資料流運行的平台UI螢幕快照。](../../assets/catalog/crm/microsoft-dynamics-365/destination-dataflow-run.png)

1. 切換到 **[!DNL Activation data]** ，然後選擇段名稱。
   ![平台UI螢幕快照示例，顯示目標激活資料。](../../assets/catalog/crm/microsoft-dynamics-365/destinations-activation-data.png)

1. 監視段摘要並確保配置檔案計數與段內建立的計數相對應。
   ![平台UI螢幕抓圖示例顯示「段」。](../../assets/catalog/crm/microsoft-dynamics-365/segment.png)

1. 登錄到 [!DNL Dynamics 365] ，然後導航到 [!DNL Customers] > [!DNL Contacts] 並檢查是否已添加該段中的配置檔案。 您可以看到 [!DNL Dynamics 365] 已根據 **[!UICONTROL 映射ID]** 值 [段調度](#schedule-segment-export-example) 的子菜單。
   ![Dynamics 365 UI螢幕快照，顯示具有更新的段狀態的「聯繫人」頁。](../../assets/catalog/crm/microsoft-dynamics-365/contacts.png)

## 資料使用和治理 {#data-usage-governance}

全部 [!DNL Adobe Experience Platform] 目標在處理資料時符合資料使用策略。 有關如何 [!DNL Adobe Experience Platform] 強制實施資料治理，請參見 [資料治理概述](/help/data-governance/home.md)。

## 錯誤和故障排除 {#errors-and-troubleshooting}

### 將事件推送到目標時遇到未知錯誤 {#unknown-errors}

檢查資料流運行時，如果收到以下錯誤消息： `Bad request reported while pushing events to the destination. Please contact the administrator and try again.`

![顯示錯誤請求錯誤的平台UI螢幕快照。](../../assets/catalog/crm/microsoft-dynamics-365/error.png)

要修復此錯誤，請驗證 **[!UICONTROL 映射ID]** 您提供 [!DNL Dynamics 365] 您的平台段有效且存在於 [!DNL Dynamics 365]。

## 其他資源 {#additional-resources}

來自 [[!DNL Dynamics 365] 文檔](https://docs.microsoft.com/en-us/dynamics365/) 如下：
* [IOrganizationService.Update（實體）方法](https://docs.microsoft.com/en-us/dotnet/api/microsoft.xrm.sdk.iorganizationservice.update?view=dataverse-sdk-latest)
* [使用Web API更新和刪除表行](https://docs.microsoft.com/en-us/power-apps/developer/data-platform/webapi/update-delete-entities-using-web-api#basic-update)
