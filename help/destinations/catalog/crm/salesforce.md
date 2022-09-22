---
keywords: crm;CRM;CRM目標；salesforce crm;salesforce crm目標
title: Salesforce CRM連線
description: Salesforce CRM目的地可讓您匯出帳戶資料，並在Salesforce CRM中根據您的業務需求啟用它。
exl-id: bd9cb656-d742-4a18-97a2-546d4056d093
source-git-commit: b243a5f88cadc238ac3edd3bf45a54564598bbf0
workflow-type: tm+mt
source-wordcount: '2256'
ht-degree: 1%

---

# [!DNL Salesforce CRM] 連接

## 總覽 {#overview}

[[!DNL Salesforce CRM]](https://www.salesforce.com/crm/) 是一個熱門的客戶關係管理(CRM)平台，並支援下列功能：

* [銷售機會](https://developer.salesforce.com/docs/atlas.en-us.object_reference.meta/object_reference/sforce_api_objects_lead.htm)  — 銷售機會是指可能（或可能）對您銷售的產品或服務感興趣的個人或公司的名稱。
* [聯繫人](https://developer.salesforce.com/docs/atlas.en-us.object_reference.meta/object_reference/sforce_api_objects_contact.htm)  — 聯絡人是指您的代表與其建立關係，且符合潛在客戶資格的個人。

此 [!DNL Adobe Experience Platform] [目的地](/help/destinations/home.md) 利用 [[!DNL Salesforce composite API]](https://developer.salesforce.com/docs/atlas.en-us.api_rest.meta/api_rest/resources_composite_sobjects_collections_update.htm)，支援上述兩種設定檔類型。

當 [啟用區段](#activate)，您可以在銷售機會或聯繫人之間進行選擇，並將屬性和分段資料更新到 [!DNL Salesforce CRM].

[!DNL Salesforce CRM] 使用OAuth 2搭配「密碼授權」作為驗證機制，與Salesforce REST API通訊。 向您的 [!DNL Salesforce CRM] 執行個體在下方， [驗證到目標](#authenticate) 區段。

## 使用案例 {#use-cases}

身為行銷人員，您可以根據使用者Adobe Experience Platform設定檔的屬性，為使用者提供個人化體驗。 您可以從離線資料建立區段，並將這些區段傳送至Salesforce CRM，以便在Adobe Experience Platform中更新區段和設定檔時，立即在使用者的動態消息中顯示。

## 先決條件 {#prerequisites}

### Experience Platform的必要條件 {#prerequisites-in-experience-platform}

在將資料激活到Salesforce CRM目標之前，您必須 [綱要](/help/xdm/schema/composition.md), [資料集](https://experienceleague.adobe.com/docs/platform-learn/tutorials/data-ingestion/create-datasets-and-ingest-data.html?lang=en)，和 [區段](https://experienceleague.adobe.com/docs/platform-learn/tutorials/segments/create-segments.html?lang=en) 建立於 [!DNL Experience Platform].

### 中的必要條件 [!DNL Salesforce CRM] {#prerequisites-destination}

請注意下列必要條件，位於 [!DNL Salesforce CRM]，以便將資料從Platform匯出至您的Salesforce帳戶：

#### 您需要有Salesforce帳戶 {#prerequisites-account}

前往Salesforce [審判](https://www.salesforce.com/in/form/signup/freetrial-sales/) 頁面來註冊和建立Salesforce帳戶（如果尚未建立）。

#### 設定已連線的應用程式 {#prerequisites-connected-app}

接下來，您需要設定 [連線應用程式](https://help.salesforce.com/s/articleView?id=sf.connected_app_create.htm&amp;language=en_US&amp;r=https%3A%2F%2Fhelp.salesforce.com%2F&amp;type=5) 在您的Salesforce帳戶中，如果您尚未擁有。

在連線的應用程式中，確定 [OAuth設定](https://help.salesforce.com/s/articleView?id=connected_app_create_api_integration.htm&amp;type=5&amp;language=en_US) 啟用。

同時確保 [作用域](https://help.salesforce.com/s/articleView?id=connected_app_create_api_integration.htm&amp;type=5&amp;language=en_US) 已選取下列項目。

* ``chatter_api``
* ``lightning``
* ``visualforce``
* ``content``
* ``openid``
* ``full``
* ``api``
* ``web``
* ``refresh_token``
* ``offline_access``

#### 在Salesforce中建立自訂欄位 {#prerequisites-custom-field}

建立類型的自訂欄位 `Text Area Long`，該Experience Platform將用來更新區段狀態(在 [!DNL Salesforce CRM].
請參閱Salesforce檔案，以 [建立自訂欄位](https://help.salesforce.com/s/articleView?id=sf.adding_fields.htm&amp;type=5) 如果您需要其他指導。

>[!IMPORTANT]
>
>請確定欄位名稱中沒有空白字元。 請改用底線 `(_)` 字元。

>[!NOTE]
>
>* Salesforce中的對象限制為25個外部欄位，請參閱 [自訂欄位屬性](https://help.salesforce.com/s/articleView?id=sf.custom_field_attributes.htm&amp;type=5).
>* 此限制表示您隨時最多只能有25個Experience Platform區段成員作用中。
>* 如果您在Salesforce內達到此限制，則必須從Salesforce中移除自訂屬性，這些屬性用於在新Experience Platform之前，針對舊區段儲存區段狀態 **[!UICONTROL 對應ID]** 可供使用。


如需相關資訊，請參閱Adobe Experience Platform檔案 [區段成員資格詳細資料結構欄位群組](/help/xdm/field-groups/profile/segmentation.md) 如果您需要區段狀態的指引。

#### 收集Salesforce憑據 {#gather-credentials}

在驗證之前，請記下下列項目 [!DNL Salesforce CRM] 目的地：

| 憑據 | 說明 | 範例 |
| --- | --- | --- |
| <ul><li>Salesforce網域首碼</li></ul> | 請參閱 [Salesforce網域首碼](https://help.salesforce.com/s/articleView?id=sf.domain_name_setting_login_policy.htm&amp;type=5) 以取得其他指導。 | <ul><li>如果您的網域如下所示，則需要醒目提示的值。<br> <i>`d5i000000isb4eak-dev-ed`.my.salesforce.com</i></li></ul> |
| <ul><li>使用者金鑰</li><li>使用者密碼</li></ul> | 請參閱 [Salesforce檔案](https://help.salesforce.com/s/articleView?id=sf.connected_app_rotate_consumer_details.htm&amp;type=5) 如果您需要其他指導。 | <ul><li>r23kxxxxxxxx0z05xxxxx</code></li><li>ipxxxxxxxxxxxxT4xxxxxxxxxxxx</code></li></ul> |

### 護欄 {#guardrails}

Salesforce通過施加請求、比率和超時限制來平衡事務處理負載。 請參閱 [API要求限制和分配](https://developer.salesforce.com/docs/atlas.en-us.salesforce_app_limits_cheatsheet.meta/salesforce_app_limits_cheatsheet/salesforce_app_limits_platform_api.htm) 以取得詳細資訊。

>[!IMPORTANT]
>
>當 [啟用區段](#activate) 您必須選擇 *連絡人* 或 *銷售機會* 類型。 您必須確保您的區段根據選取的類型具有適當的資料對應。

## 支援的身分 {#supported-identities}

[!DNL Salesforce CRM] 支援下表所述的身分識別更新。 深入了解 [身分](/help/identity-service/namespaces.md).

| Target身分 | 說明 | 考量事項 |
|---|---|---|
| `SalesforceId` | 此 [!DNL Salesforce CRM] 您透過區段匯出或更新的連絡人或潛在客戶身分識別碼。 | 必要 |

## 匯出類型和頻率 {#export-type-frequency}

有關目標導出類型和頻率的資訊，請參閱下表。

| 項目 | 類型 | 附註 |
---------|----------|---------|
| 匯出類型 | **[!UICONTROL 設定檔]** | <ul><li>您要匯出區段的所有成員，以及所需的結構欄位 *(例如：電子郵件地址、電話號碼、姓氏)*，根據您的欄位對應。</li><li> 中的每個區段狀態 [!DNL Salesforce CRM] 會根據 **[!UICONTROL 對應ID]** 值 [區段排程](#schedule-segment-export-example) 步驟。</li></ul> |
| 匯出頻率 | **[!UICONTROL 串流]** | <ul><li>串流目的地是「一律開啟」API型連線。 一旦根據區段評估在Experience Platform中更新設定檔，連接器就會將更新傳送至下游的目的地平台。 深入了解 [串流目的地](/help/destinations/destination-types.md#streaming-destinations).</li></ul> |

{style=&quot;table-layout:auto&quot;}

## 連接到目標 {#connect}

>[!IMPORTANT]
>
>若要連線至目的地，您需要 **[!UICONTROL 管理目的地]** [存取控制權限](/help/access-control/home.md#permissions). 閱讀 [存取控制概觀](/help/access-control/ui/overview.md) 或聯絡您的產品管理員以取得所需的權限。

若要連線至此目的地，請依照 [目的地設定教學課程](../../ui/connect-destination.md). 在設定目標工作流程中，填寫下列兩節所列的欄位。

內 **[!UICONTROL 目的地]** > **[!UICONTROL 目錄]** 搜尋 [!DNL Salesforce CRM]. 或者，您也可以在 **[!UICONTROL CRM]** 類別。

### 驗證到目標 {#authenticate}

若要驗證目的地，請填寫必填欄位並選取 **[!UICONTROL 連接到目標]**.

![Platform UI螢幕擷取畫面，顯示如何驗證。](../../assets/catalog/crm/salesforce/authenticate-destination.png)

* **[!UICONTROL 密碼]**:您的Salesforce帳戶密碼。
* **[!UICONTROL 自訂網域]**:您的Salesforce網域。
* **[!UICONTROL 用戶端ID]**:您的Salesforce已連接應用程式消費者金鑰。
* **[!UICONTROL 用戶端密碼]**:您的Salesforce已連接應用程式消費者密碼。
* **[!UICONTROL 使用者名稱]**:您的Salesforce帳戶使用者名稱。

如果提供的詳細資料有效，UI會顯示 **[!UICONTROL 已連接]** 狀態（加上綠色勾號），您就可以繼續進行下一個步驟。

### 填寫目的地詳細資訊 {#destination-details}

若要設定目的地的詳細資訊，請填寫下方的必填和選填欄位。 UI中欄位旁的星號表示該欄位為必要欄位。
![Platform UI螢幕擷取畫面，顯示目的地詳細資訊。](../../assets/catalog/crm/salesforce/destination-details.png)

* **[!UICONTROL 名稱]**:日後您將透過此名稱識別此目的地。
* **[!UICONTROL 說明]**:未來可協助您識別此目的地的說明。
* **[!UICONTROL Salesforce ID類型]**:選擇 **[!UICONTROL 連絡人]** 如果您要匯出或更新的身分屬於 *連絡人*. 選擇 **[!UICONTROL 銷售機會]** 如果您要匯出或更新的身分屬於 *銷售機會*.

### 啟用警報 {#enable-alerts}

您可以啟用警報，接收有關資料流到目標狀態的通知。 從清單中選擇要訂閱的警報，以接收有關資料流狀態的通知。 如需警報的詳細資訊，請參閱 [使用UI訂閱目的地警報](../../ui/alerts.md).

完成提供目標連接的詳細資訊後，請選擇 **[!UICONTROL 下一個]**.

## 啟用此目的地的區段 {#activate}

>[!IMPORTANT]
>
>若要啟用資料，您需要 **[!UICONTROL 管理目的地]**, **[!UICONTROL 啟動目的地]**, **[!UICONTROL 檢視設定檔]**，和 **[!UICONTROL 檢視區段]** [存取控制權限](/help/access-control/home.md#permissions). 閱讀 [存取控制概觀](/help/access-control/ui/overview.md) 或聯絡您的產品管理員以取得所需的權限。

閱讀 [啟動設定檔和區段至串流區段匯出目的地](/help/destinations/ui/activate-segment-streaming-destinations.md) 以取得啟用受眾區段至此目的地的指示。

### 對應考量事項和範例 {#mapping-considerations-example}

若要將您的對象資料從Adobe Experience Platform正確傳送至 [!DNL Salesforce CRM] 目的地，您必須執行欄位對應步驟。 對應包含在您的Platform帳戶中的Experience Data Model(XDM)結構欄位與目標目的地對應的欄位之間建立連結。 若要正確將XDM欄位對應至 [!DNL Salesforce CRM] 目標欄位，請遵循下列步驟：

1. 在 **[!UICONTROL 對應]** 步驟，選取 **[!UICONTROL 新增對應]**，畫面上會顯示新的對應列。
   ![Platform UI新增對應的螢幕擷取範例。](../../assets/catalog/crm/salesforce/add-new-mapping.png)

1. 在 **[!UICONTROL 選擇源欄位]** 窗口，選擇 **[!UICONTROL 選取身分命名空間]** 或 **[!UICONTROL 選擇屬性]** 類別和選取 `crmID`.
   ![Platform UI的來源對應螢幕擷取範例。](../../assets/catalog/crm/salesforce/source-mapping.png)

1. 在 **[!UICONTROL 選擇目標欄位]** 窗口，選擇 **[!UICONTROL 選取身分命名空間]** 類別和選取 `SalesforceId`.
   ![Platform UI螢幕擷圖，顯示SalesforceId的Target對應。](../../assets/catalog/crm/salesforce/target-mapping-salesforceid.png)

   * 在XDM設定檔架構與 [!DNL Salesforce CRM] 例項：
   | XDM設定檔結構 | [!DNL Salesforce CRM] 例項 | 必要 |
   |---|---|---|
   | `crmID` | `SalesforceId` | 是 |

   * **[!UICONTROL 選取自訂屬性]**:選擇此選項可將源欄位映射到您已在 **[!UICONTROL 屬性名稱]** 欄位。 請參閱 [[!DNL Salesforce CRM] 檔案](https://help.salesforce.com/s/articleView?id=sf.custom_field_attributes.htm&amp;type=5) 以取得支援屬性的指引。
      ![平台UI螢幕擷圖，顯示LastName的Target對應。](../../assets/catalog/crm/salesforce/target-mapping-lastname.png)

   * 如果您使用 *聯繫人* 在區段內，請參閱Salesforce中的物件參考，以取得 [連絡人](https://developer.salesforce.com/docs/atlas.en-us.object_reference.meta/object_reference/sforce_api_objects_contact.htm) 定義要更新欄位的對應。
   * 通過搜索該詞，可以標識必填欄位 *必填*，這會在上述連結的欄位說明中提及。
   * 根據您要匯出或更新的欄位，新增XDM設定檔架構與 [!DNL Salesforce CRM] 例項：

   | XDM設定檔結構 | [!DNL Salesforce CRM] 例項 | 附註 |
   | --- | --- | --- |
   | `person.name.lastName` | `LastName` | `Required`。聯繫人的姓氏，最多80個字元。 |
   | `person.name.firstName` | `FirstName` | 聯繫人的名字最多40個字元。 |
   | `personalEmail.address` | `Email` | 連絡人的電子郵件地址。 |

   * 使用這些對應的範例如下所示：
      ![Platform UI螢幕擷取範例，顯示Target對應。](../../assets/catalog/crm/salesforce/mappings-contacts.png)

   * 如果您使用 *銷售機會* 在區段內，請參閱Salesforce中的物件參考，以取得 [銷售機會](https://developer.salesforce.com/docs/atlas.en-us.object_reference.meta/object_reference/sforce_api_objects_lead.htm) 定義要更新欄位的對應。
   * 通過搜索該詞，可以標識必填欄位 *必填*，這會在上述連結的欄位說明中提及。
   * 根據您要匯出或更新的欄位，新增XDM設定檔架構與 [!DNL Salesforce CRM] 例項：

   | XDM設定檔結構 | [!DNL Salesforce CRM] 例項 | 附註 |
   | --- | --- | --- |
   | `person.name.lastName` | `LastName` | `Required`。聯繫人的姓氏，最多80個字元。 |
   | `b2b.companyName` | `Company` | `Required`。領隊的公司。 |
   | `personalEmail.address` | `Email` | 連絡人的電子郵件地址。 |

   * 使用這些對應的範例如下所示：
      ![Platform UI螢幕擷取範例，顯示Target對應。](../../assets/catalog/crm/salesforce/mappings-leads.png)




### 排程區段匯出和範例 {#schedule-segment-export-example}

執行 [排程區段匯出](/help/destinations/ui/activate-segment-streaming-destinations.md#scheduling) 步驟中，您必須手動將Platform區段對應至Salesforce中的自訂欄位屬性。

若要這麼做，請選取每個區段，然後在 **[!UICONTROL 對應ID]** 欄位。

>[!IMPORTANT]
>
>* 用於 **[!UICONTROL 對應ID]** 應完全符合在Salesforce中建立的自訂欄位屬性名稱。
>* 請確定您在Salesforce中建立的自訂欄位屬性名稱未使用空白字元。


以下是範例：
![Platform UI螢幕擷取範例，顯示「排程區段」匯出。](../../assets/catalog/crm/salesforce/schedule-segment-export.png)

## 驗證資料匯出 {#exported-data}

若要驗證您是否已正確設定目的地，請遵循下列步驟：

1. 選擇 **[!UICONTROL 目的地]** > **[!UICONTROL 瀏覽]** 導覽至目的地清單。
   ![顯示「瀏覽目的地」的Platform UI螢幕擷圖。](../../assets/catalog/crm/salesforce/browse-destinations.png)

1. 選取目標並驗證狀態為 **[!UICONTROL 已啟用]**.
   ![Platform UI螢幕擷圖，顯示「目的地資料流執行」。](../../assets/catalog/crm/salesforce/destination-dataflow-run.png)

1. 切換至 **[!UICONTROL 啟動資料]** ，然後選取區段名稱。
   ![Platform UI螢幕擷取範例，顯示「目的地啟動資料」。](../../assets/catalog/crm/salesforce/destinations-activation-data.png)

1. 監控區段摘要，並確保設定檔計數與區段內建立的計數相對應。
   ![Platform UI螢幕擷取範例，顯示「區段」。](../../assets/catalog/crm/salesforce/segment.png)

1. 最後，登入Salesforce網站，驗證區段的設定檔是否已新增或更新。
   * 如果你 *聯繫人* 在您的Platform區段中，導覽至 **[!DNL Apps]** > **[!DNL Contacts]** 頁面。
      ![Salesforce CRM螢幕截圖顯示「聯絡人」頁面，其中包含區段中的設定檔。](../../assets/catalog/crm/salesforce/contacts.png)

   * 選取 *連絡人* 並檢查欄位是否已更新。 您可以在 [!DNL Salesforce CRM] 已根據 **[!UICONTROL 對應ID]** 值 [區段排程](#schedule-segment-export-example).
      ![Salesforce CRM螢幕截圖顯示具有更新區段狀態的「聯繫人詳細資訊」頁面。](../../assets/catalog/crm/salesforce/contact-info.png)

   * 如果你 *銷售機會* 在您的Platform區段中，導覽至 **[!DNL Apps]** > **[!DNL Leads]** 頁面。
      ![Salesforce CRM螢幕截圖顯示「銷售機會」頁面，其中包含區段中的設定檔。](../../assets/catalog/crm/salesforce/leads.png)

   * 選取 *銷售機會* 並檢查欄位是否已更新。 您可以在 [!DNL Salesforce CRM] 已根據 **[!UICONTROL 對應ID]** 值 [區段排程](#schedule-segment-export-example).
      ![Salesforce CRM螢幕截圖顯示具有更新區段狀態的「銷售機會詳細資訊」頁面。](../../assets/catalog/crm/salesforce/lead-info.png)

## 資料使用與控管 {#data-usage-governance}

全部 [!DNL Adobe Experience Platform] 處理資料時，目的地符合資料使用原則。 有關如何 [!DNL Adobe Experience Platform] 強制實施資料控管，請參閱 [資料控管概觀](/help/data-governance/home.md).

## 錯誤和疑難排解 {#errors-and-troubleshooting}

### 將事件推送至目的地時發生未知錯誤 {#unknown-errors}

檢查資料流運行時，如果您收到以下錯誤消息： `Unknown errors encountered while pushing events to the destination. Please contact the administrator and try again.`

![Platform UI螢幕擷取畫面顯示錯誤。](../../assets/catalog/crm/salesforce/error.png)

若要修正此錯誤，請確認 **[!UICONTROL 對應ID]** 您在 [!DNL Salesforce CRM] 因為您的平台區段有效且存在於 [!DNL Salesforce CRM].

## 其他資源 {#additional-resources}

來自 [Salesforce開發人員入口網站](https://developer.salesforce.com/) 如下所示：
* [快速入門](https://developer.salesforce.com/docs/atlas.en-us.api_rest.meta/api_rest/quickstart.htm)
* [建立記錄](https://developer.salesforce.com/docs/atlas.en-us.api_rest.meta/api_rest/dome_sobject_create.htm)
* [自訂建議對象](https://developer.salesforce.com/docs/atlas.en-us.236.0.chatterapi.meta/chatterapi/connect_resources_recommendation_audiences_list.htm)
* [使用複合資源](https://developer.salesforce.com/docs/atlas.en-us.api_rest.meta/api_rest/using_composite_resources.htm?q=composite)
* 此目的地利用 [更新多個記錄](https://developer.salesforce.com/docs/atlas.en-us.api_rest.meta/api_rest/resources_composite_sobjects_collections_update.htm) API而非 [添加單條記錄](https://developer.salesforce.com/docs/atlas.en-us.api_rest.meta/api_rest/dome_composite_upsert_example.htm?q=contacts) API呼叫。