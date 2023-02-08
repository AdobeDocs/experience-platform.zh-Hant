---
keywords: crm;CRM;CRM目標；salesforce crm;salesforce crm目標
title: Salesforce CRM連線
description: Salesforce CRM目的地可讓您匯出帳戶資料，並在Salesforce CRM中根據您的業務需求啟用它。
exl-id: bd9cb656-d742-4a18-97a2-546d4056d093
source-git-commit: edf49d8a52eeddea65a18c1dad0035ec7e5d2c12
workflow-type: tm+mt
source-wordcount: '3089'
ht-degree: 0%

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

#### 你需要 [!DNL Salesforce] 帳戶 {#prerequisites-account}

前往 [!DNL Salesforce] [審判](https://www.salesforce.com/in/form/signup/freetrial-sales/) 註冊和建立頁面 [!DNL Salesforce] 帳戶，如果尚未建立帳戶。

#### 在內設定已連線的應用程式 [!DNL Salesforce] {#prerequisites-connected-app}

首先，您需要設定 [[!DNL Salesforce] 連線應用程式](https://help.salesforce.com/s/articleView?id=sf.connected_app_create.htm&amp;language=en_US&amp;r=https%3A%2F%2Fhelp.salesforce.com%2F&amp;type=5) 在 [!DNL Salesforce] 帳戶，如果尚未建立帳戶。 [!DNL Salesforce CRM] 將利用連接的應用程式連接到 [!DNL Salesforce].

接下來，啟用 [!DNL OAuth Settings for API Integration] 針對 [!DNL Salesforce connected app]. 請參閱 [[!DNL Salesforce]](https://help.salesforce.com/s/articleView?id=connected_app_create_api_integration.htm&amp;type=5&amp;language=en_US) 指南檔案。

此外，請確定 [作用域](https://help.salesforce.com/s/articleView?id=connected_app_create_api_integration.htm&amp;type=5&amp;language=en_US) 已針對 [!DNL Salesforce connected app].

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

最後，請確定 `password` 在 [!DNL Salesforce] 帳戶。 請參閱 [!DNL Salesforce] [特殊情況的OAuth 2.0使用者名稱 — 密碼流程](https://help.salesforce.com/s/articleView?id=sf.remoteaccess_oauth_username_password_flow.htm&amp;type=5) 說明檔案（若您需要指引）。

>[!IMPORTANT]
>
>若您的 [!DNL Salesforce] 帳戶管理員對受信任IP範圍的存取權限受限，您需要聯絡這些範圍才能取得 [Experience PlatformIP](/help/destinations/catalog/streaming/ip-address-allow-list.md) 允許清單。 請參閱 [!DNL Salesforce] [限制對已連線應用程式的受信任IP範圍的存取](https://help.salesforce.com/s/articleView?id=sf.connected_app_edit_ip_ranges.htm&amp;type=5) 說明檔案。

#### 在中建立自訂欄位 [!DNL Salesforce] {#prerequisites-custom-field}

將區段啟用至 [!DNL Salesforce CRM] 目的地，您必須在 **[!UICONTROL 對應ID]** 欄位中 **[區段排程](#schedule-segment-export-example)** 步驟。

[!DNL Salesforce CRM] 需要此值才能正確讀取和解讀來自Experience Platform的區段，以及在內更新其區段狀態 [!DNL Salesforce]. 請參閱Experience Platform檔案，以了解 [區段成員資格詳細資料結構欄位群組](/help/xdm/field-groups/profile/segmentation.md) 如果您需要區段狀態的指引。

針對您從Platform啟動至 [!DNL Salesforce CRM]，您需要建立類型的自訂欄位 `Text Area (Long)` with [!DNL Salesforce]. 您可以根據業務需求，定義256 - 131,072個字元之間任何大小的欄位字元長度。 請參閱 [!DNL Salesforce] [自訂欄位類型](https://help.salesforce.com/s/articleView?id=sf.custom_field_types.htm&amp;type=5) 檔案頁面，以取得自訂欄位類型的其他資訊。 另請參閱 [!DNL Salesforce] 檔案 [建立自訂欄位](https://help.salesforce.com/s/articleView?id=mc_cab_create_an_attribute.htm&amp;type=5&amp;language=en_US) 如果您需要建立欄位的協助。

>[!IMPORTANT]
>
>欄位名稱中請勿包含空白字元。 請改用底線 `(_)` 字元。
>內 [!DNL Salesforce] 您必須使用 **[!UICONTROL 欄位名稱]** 完全符合 **[!UICONTROL 對應ID]** 針對每個已啟用的平台區段。 例如，下方的螢幕擷圖顯示名為 `crm_2_seg`. 啟用區段至此目的地時，請新增 `crm_2_seg` as **[!UICONTROL 對應ID]** 將區段對象從Experience Platform填入此自訂欄位。

在中建立自訂欄位的範例 [!DNL Salesforce], *步驟1 — 選取資料類型*，如下所示：
![Salesforce UI螢幕擷圖顯示自訂欄位建立，步驟1 — 選取資料類型。](../../assets/catalog/crm/salesforce/create-salesforce-custom-field-step-1.png)

在中建立自訂欄位的範例 [!DNL Salesforce], *步驟2 — 輸入自訂欄位的詳細資訊*，如下所示：
![Salesforce UI螢幕擷圖顯示自訂欄位建立，步驟2 — 輸入自訂欄位的詳細資訊。](../../assets/catalog/crm/salesforce/create-salesforce-custom-field-step-2.png)

>[!TIP]
>
>* 區分用於Platform區段的自訂欄位，以及 [!DNL Salesforce] 建立自訂欄位時，您可以包含可識別的首碼或尾碼。 例如，而非 `test_segment`，使用 `Adobe_test_segment` 或 `test_segment_Adobe`
>* 如果您已在中建立其他自訂欄位 [!DNL Salesforce]，您可以使用與Platform區段相同的名稱，輕鬆識別 [!DNL Salesforce].


>[!NOTE]
>
>* Salesforce中的對象限制為25個外部欄位，請參閱 [自訂欄位屬性](https://help.salesforce.com/s/articleView?id=sf.custom_field_attributes.htm&amp;type=5).
>* 此限制表示您隨時最多只能有25個Experience Platform區段成員作用中。
>* 如果您在Salesforce內達到此限制，則必須從Salesforce中移除自訂屬性，這些自訂屬性用於在新區段之前，針對Experience Platform內較舊的區段儲存區段狀態 **[!UICONTROL 對應ID]** 可供使用。


#### 收集 [!DNL Salesforce CRM] 憑據 {#gather-credentials}

在驗證之前，請記下下列項目 [!DNL Salesforce CRM] 目的地：

| 憑據 | 說明 | 範例 |
| --- | --- | --- |
| `Username` | 您的 [!DNL Salesforce] 帳戶使用者名稱。 |  |
| `Password` | 您的 [!DNL Salesforce] 帳戶密碼。 |  |
| `Security Token` | 您的 [!DNL Salesforce] 安全性代號，您稍後會將此代號附加至 [!DNL Salesforce] 建立串連字串以用作 **[!UICONTROL 密碼]** when [驗證目的地](#authenticate).<br> 請參閱 [!DNL Salesforce] 檔案 [重置安全令牌](https://help.salesforce.com/s/articleView?id=sf.user_security_token.htm&amp;type=5) 學習如何從中重新產生 [!DNL Salesforce] 介面（若您沒有安全代號）。 |  |
| `Custom Domain` | 您的 [!DNL Salesforce] 網域前置詞。 <br> 請參閱 [[!DNL Salesforce] 檔案](https://help.salesforce.com/s/articleView?id=sf.domain_name_setting_login_policy.htm&amp;type=5) 若要了解如何從 [!DNL Salesforce] 介面。 | 若您的 [!DNL Salesforce] 網域為<br> *`d5i000000isb4eak-dev-ed`.my.salesforce.com*,<br> 您需要 `d5i000000isb4eak-dev-ed` 作為值。 |
| `Client ID` | 您的銷售人員 `Consumer Key`. <br> 請參閱 [[!DNL Salesforce] 檔案](https://help.salesforce.com/s/articleView?id=sf.connected_app_rotate_consumer_details.htm&amp;type=5) 若要了解如何從 [!DNL Salesforce] 介面。 |  |
| `Client Secret` | 您的銷售人員 `Consumer Secret`. <br> 請參閱 [[!DNL Salesforce] 檔案](https://help.salesforce.com/s/articleView?id=sf.connected_app_rotate_consumer_details.htm&amp;type=5) 若要了解如何從 [!DNL Salesforce] 介面。 |  |

### 護欄 {#guardrails}

[!DNL Salesforce] 通過施加請求、比率和超時限制來平衡事務處理負載。 請參閱 [API要求限制和分配](https://developer.salesforce.com/docs/atlas.en-us.salesforce_app_limits_cheatsheet.meta/salesforce_app_limits_cheatsheet/salesforce_app_limits_platform_api.htm) 以取得詳細資訊。

若您的 [!DNL Salesforce] 帳戶管理員已強制執行IP限制，您需要新增 [Experience PlatformIP位址](/help/destinations/catalog/streaming/ip-address-allow-list.md) 至 [!DNL Salesforce] 帳戶信任的IP範圍。 請參閱 [!DNL Salesforce] [限制對已連線應用程式的受信任IP範圍的存取](https://help.salesforce.com/s/articleView?id=sf.connected_app_edit_ip_ranges.htm&amp;type=5) 說明檔案。

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

若要驗證目的地，請填寫下方的必填欄位並選取 **[!UICONTROL 連接到目標]**. 請參閱 [收集 [!DNL Salesforce CRM] 憑據](#gather-credentials) 區段。
|憑據 |說明 | | — | — | | **[!UICONTROL 使用者名稱]** |您的 [!DNL Salesforce] 帳戶使用者名稱。 | | **[!UICONTROL 密碼]** |由 [!DNL Salesforce] 帳戶密碼附加在 [!DNL Salesforce] 安全令牌。<br>串連值會以 `{PASSWORD}{TOKEN}`.<br> 注意，請勿使用任何大括弧或空格。<br>例如，若您的 [!DNL Salesforce] 密碼為 `MyPa$$w0rd123` 和 [!DNL Salesforce] 安全令牌為 `TOKEN12345....0000`，您將在 **[!UICONTROL 密碼]** 欄位為 `MyPa$$w0rd123TOKEN12345....0000`. | | **[!UICONTROL 自訂網域]** |您的 [!DNL Salesforce] 網域前置詞。 <br>例如，若您的網域為 *`d5i000000isb4eak-dev-ed`.my.salesforce.com*，您需要提供 `d5i000000isb4eak-dev-ed` 作為值。 | | **[!UICONTROL 用戶端ID]** |您的 [!DNL Salesforce] 連線應用程式 `Consumer Key`. | | **[!UICONTROL 用戶端密碼]** |您的 [!DNL Salesforce] 連線應用程式 `Consumer Secret`. |

![Platform UI螢幕擷取畫面，顯示如何驗證。](../../assets/catalog/crm/salesforce/authenticate-destination.png)

如果提供的詳細資料有效，UI會顯示 **[!UICONTROL 已連接]** 狀態（加上綠色勾號），您就可以繼續進行下一個步驟。

### 填寫目的地詳細資訊 {#destination-details}

若要設定目的地的詳細資訊，請填寫下方的必填和選填欄位。 UI中欄位旁的星號表示該欄位為必要欄位。
* **[!UICONTROL 名稱]**:日後您將透過此名稱識別此目的地。
* **[!UICONTROL 說明]**:未來可協助您識別此目的地的說明。
* **[!UICONTROL Salesforce ID類型]**:
   * 選擇 **[!UICONTROL 連絡人]** 如果您要匯出或更新的身分屬於 *連絡人*.
   * 選擇 **[!UICONTROL 銷售機會]** 如果您要匯出或更新的身分屬於 *銷售機會*.

![Platform UI螢幕擷取畫面，顯示目的地詳細資訊。](../../assets/catalog/crm/salesforce/destination-details.png)

### 啟用警報 {#enable-alerts}

您可以啟用警報，接收有關資料流到目標狀態的通知。 從清單中選擇要訂閱的警報，以接收有關資料流狀態的通知。 如需警報的詳細資訊，請參閱 [使用UI訂閱目的地警報](../../ui/alerts.md).

完成提供目標連接的詳細資訊後，請選擇 **[!UICONTROL 下一個]**.

## 啟用此目的地的區段 {#activate}

>[!IMPORTANT]
>
>若要啟用資料，您需要 **[!UICONTROL 管理目的地]**, **[!UICONTROL 啟動目的地]**, **[!UICONTROL 檢視設定檔]**，和 **[!UICONTROL 檢視區段]** [存取控制權限](/help/access-control/home.md#permissions). 閱讀 [存取控制概觀](/help/access-control/ui/overview.md) 或聯絡您的產品管理員以取得所需的權限。

閱讀 [啟動設定檔和區段至串流區段匯出目的地](/help/destinations/ui/activate-segment-streaming-destinations.md) 以取得啟用受眾區段至此目的地的指示。

### 對應考量事項和範例 {#mapping-considerations-example}

若要將您的對象資料從Adobe Experience Platform正確傳送至 [!DNL Salesforce CRM] 目的地，您必須執行欄位對應步驟。 對應包含在您的Platform帳戶中的Experience Data Model(XDM)結構欄位與目標目的地對應的欄位之間建立連結。

在 **[!UICONTROL 目標欄位]** 名稱應與屬性對應表格中所述完全相同，因為這些屬性將構成請求內文。

在 **[!UICONTROL 源欄位]** 不遵守任何此類限制。 您可以視需要對應，但請根據 [[!DNL Salesforce] 檔案](https://help.salesforce.com/s/articleView?id=sf.custom_field_attributes.htm&amp;type=5). 如果輸入資料無效，則會呼叫 [!DNL Salesforce] 將失敗，您的聯繫人/銷售機會將不會更新。

若要正確將XDM欄位對應至 [!DNL (API) Salesforce CRM] 目標欄位，請遵循下列步驟：

1. 在 **[!UICONTROL 對應]** 步驟，選取 **[!UICONTROL 新增對應]**，畫面上會顯示新的對應列。
   ![Platform UI新增對應的螢幕擷取範例。](../../assets/catalog/crm/salesforce/add-new-mapping.png)
1. 在 **[!UICONTROL 選擇源欄位]** 窗口，選擇 **[!UICONTROL 選擇屬性]** 類別，然後選取XDM屬性或選擇 **[!UICONTROL 選取身分命名空間]** 並選擇身份。
1. 在 **[!UICONTROL 選擇目標欄位]** 窗口，選擇 **[!UICONTROL 選取身分命名空間]** 並選擇身份或 **[!UICONTROL 選取自訂屬性]** 類別，然後使用 **[!UICONTROL 屬性名稱]** 欄位。 請參閱 [[!DNL Salesforce CRM] 檔案](https://help.salesforce.com/s/articleView?id=sf.custom_field_attributes.htm&amp;type=5) 以取得支援屬性的指引。
   * 重複這些步驟，新增XDM設定檔架構與 [!DNL (API) Salesforce CRM]:

   **使用聯繫人**

   * 如果您使用 *聯繫人* 在區段內，請參閱Salesforce中的物件參考，以取得 [連絡人](https://developer.salesforce.com/docs/atlas.en-us.object_reference.meta/object_reference/sforce_api_objects_contact.htm) 定義要更新欄位的對應。
   * 通過搜索該詞，可以標識必填欄位 *必填*，這會在上述連結的欄位說明中提及。
   * 根據您要匯出或更新的欄位，新增XDM設定檔架構與 [!DNL (API) Salesforce CRM]: |源欄位|目標欄位|注 | | — | — | — | |`IdentityMap: crmID`|`Identity: SalesforceId`|`Mandatory`| |`xdm: person.name.lastName`|`Attribute: LastName`| `Mandatory`. 聯繫人的姓氏，最多80個字元。 |\
      |`xdm: person.name.firstName`|`Attribute: FirstName`|聯繫人的名字，最多40個字元。 | |`xdm: personalEmail.address`|`Attribute: Email`|聯繫人的電子郵件地址。 |

   * 使用這些對應的範例如下所示：
      ![Platform UI螢幕擷取範例，顯示Target對應。](../../assets/catalog/crm/salesforce/mappings-contacts.png)

   **使用銷售機會**

   * 如果您使用 *銷售機會* 在區段內，請參閱Salesforce中的物件參考，以取得 [銷售機會](https://developer.salesforce.com/docs/atlas.en-us.object_reference.meta/object_reference/sforce_api_objects_lead.htm) 定義要更新欄位的對應。
   * 通過搜索該詞，可以標識必填欄位 *必填*，這會在上述連結的欄位說明中提及。
   * 根據您要匯出或更新的欄位，新增XDM設定檔架構與 [!DNL (API) Salesforce CRM]: |源欄位|目標欄位|注 | | — | — | — | |`IdentityMap: crmID`|`Identity: SalesforceId`|`Mandatory`| |`xdm: person.name.lastName`|`Attribute: LastName`| `Mandatory`. 最多80個字元的姓氏。 |\
      |`xdm: b2b.companyName`|`Attribute: Company`| `Mandatory`. 領隊的公司。 | |`xdm: personalEmail.address`|`Attribute: Email`|主管的電子郵件地址。 |

   * 使用這些對應的範例如下所示：
      ![Platform UI螢幕擷取範例，顯示Target對應。](../../assets/catalog/crm/salesforce/mappings-leads.png)



完成目標連接的映射後，請選擇 **[!UICONTROL 下一個]**.

### 排程區段匯出和範例 {#schedule-segment-export-example}

執行 [排程區段匯出](/help/destinations/ui/activate-segment-streaming-destinations.md#scheduling) 步驟您必須手動將從Platform啟動的區段對應至其在 [!DNL Salesforce].

若要這麼做，請選取每個區段，然後輸入自訂欄位名稱 [!DNL Salesforce] 在 [!DNL Salesforce CRM] **[!UICONTROL 對應ID]** 欄位。 請參閱 [在中建立自訂欄位 [!DNL Salesforce]](#prerequisites-custom-field) 區段中建立自訂欄位的指引和最佳作法 [!DNL Salesforce].

例如，若您的 [!DNL Salesforce] 自訂欄位為 `crm_2_seg`，請在 [!DNL Salesforce CRM] **[!UICONTROL 對應ID]** 將區段對象從Experience Platform填入此自訂欄位。

來自的自訂欄位範例 [!DNL Salesforce] 如下所示：
![[!DNL Salesforce] 顯示自訂欄位的UI螢幕擷圖。](../../assets/catalog/crm/salesforce/salesforce-custom-field.png)

表示 [!DNL Salesforce CRM] **[!UICONTROL 對應ID]** 如下所示：
![Platform UI螢幕擷取範例，顯示「排程區段」匯出。](../../assets/catalog/crm/salesforce/schedule-segment-export.png)

如上所示 [!DNL Salesforce] **[!UICONTROL 欄位名稱]** 完全符合中指定的值 [!DNL Salesforce CRM] **[!UICONTROL 對應ID]**.

根據您的使用案例，所有啟用的區段皆可對應至相同的 [!DNL Salesforce] 自訂欄位或 **[!UICONTROL 欄位名稱]** in [!DNL Salesforce CRM]. 以上所示影像為基礎的典型範例可能是。
| [!DNL Salesforce CRM] 區段名稱 | [!DNL Salesforce] **[!UICONTROL 欄位名稱]** | [!DNL Salesforce CRM] **[!UICONTROL 對應ID]** | | — | — | — | | crm_1_seg | `crm_1_seg` | `crm_1_seg` | | crm_2_seg | `crm_2_seg` | `crm_2_seg` |

對每個已啟動的Platform區段重複此區段。

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

   **使用聯繫人**

   * 如果您已選取 *聯繫人* 在您的Platform區段中，導覽至 **[!DNL Apps]** > **[!DNL Contacts]** 頁面。
      ![Salesforce CRM螢幕截圖顯示「聯絡人」頁面，其中包含區段中的設定檔。](../../assets/catalog/crm/salesforce/contacts.png)

   * 選取 *連絡人* 並檢查欄位是否已更新。 您可以在 [!DNL Salesforce CRM] 已根據 **[!UICONTROL 對應ID]** 值 [區段排程](#schedule-segment-export-example).
      ![Salesforce CRM螢幕截圖顯示具有更新區段狀態的「聯繫人詳細資訊」頁面。](../../assets/catalog/crm/salesforce/contact-info.png)

   **使用銷售機會**

   * 如果您已選取 *銷售機會* 在您的Platform區段中，導覽至 **[!DNL Apps]** > **[!DNL Leads]** 頁面。
      ![Salesforce CRM螢幕截圖顯示「銷售機會」頁面，其中包含區段中的設定檔。](../../assets/catalog/crm/salesforce/leads.png)

   * 選取 *銷售機會* 並檢查欄位是否已更新。 您可以在 [!DNL Salesforce CRM] 已根據 **[!UICONTROL 對應ID]** 值 [區段排程](#schedule-segment-export-example).
      ![Salesforce CRM螢幕截圖顯示具有更新區段狀態的「銷售機會詳細資訊」頁面。](../../assets/catalog/crm/salesforce/lead-info.png)


## 資料使用與控管 {#data-usage-governance}

全部 [!DNL Adobe Experience Platform] 處理資料時，目的地符合資料使用原則。 有關如何 [!DNL Adobe Experience Platform] 強制實施資料控管，請參閱 [資料控管概觀](/help/data-governance/home.md).

## 錯誤和疑難排解 {#errors-and-troubleshooting}

### 將事件推送至目的地時發生未知錯誤 {#unknown-errors}

* 檢查資料流運行時，您可能會遇到以下錯誤消息： `Unknown errors encountered while pushing events to the destination. Please contact the administrator and try again.`

   ![Platform UI螢幕擷取畫面顯示錯誤。](../../assets/catalog/crm/salesforce/error.png)

   * 若要修正此錯誤，請確認 **[!UICONTROL 對應ID]** 在啟動工作流程中提供給 [!DNL Salesforce CRM] 目的地完全符合您在 [!DNL Salesforce]. 請參閱 [在中建立自訂欄位 [!DNL Salesforce]](#prerequisites-custom-field) 一節以取得指引。

* 啟用區段時，您可能會收到錯誤訊息： `The client's IP address is unauthorized for this account. Allowlist the client's IP address...`
   * 若要修正此錯誤，請連絡您的 [!DNL Salesforce] 帳戶管理員 [Experience PlatformIP位址](/help/destinations/catalog/streaming/ip-address-allow-list.md) 至 [!DNL Salesforce] 帳戶信任的IP範圍。 請參閱 [!DNL Salesforce] [限制對已連線應用程式的受信任IP範圍的存取](https://help.salesforce.com/s/articleView?id=sf.connected_app_edit_ip_ranges.htm&amp;type=5) 說明檔案。

## 其他資源 {#additional-resources}

來自 [Salesforce開發人員入口網站](https://developer.salesforce.com/) 如下所示：
* [快速入門](https://developer.salesforce.com/docs/atlas.en-us.api_rest.meta/api_rest/quickstart.htm)
* [建立記錄](https://developer.salesforce.com/docs/atlas.en-us.api_rest.meta/api_rest/dome_sobject_create.htm)
* [自訂建議對象](https://developer.salesforce.com/docs/atlas.en-us.236.0.chatterapi.meta/chatterapi/connect_resources_recommendation_audiences_list.htm)
* [使用複合資源](https://developer.salesforce.com/docs/atlas.en-us.api_rest.meta/api_rest/using_composite_resources.htm?q=composite)
* 此目的地利用 [更新多個記錄](https://developer.salesforce.com/docs/atlas.en-us.api_rest.meta/api_rest/resources_composite_sobjects_collections_update.htm) API而非 [添加單條記錄](https://developer.salesforce.com/docs/atlas.en-us.api_rest.meta/api_rest/dome_composite_upsert_example.htm?q=contacts) API呼叫。