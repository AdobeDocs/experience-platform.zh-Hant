---
keywords: crm;CRM;CRM目標；salesforce crm;salesforce crm目標
title: Salesforce CRM連接
description: Salesforce CRM目標允許您導出帳戶資料並在Salesforce CRM中根據您的業務需要將其激活。
exl-id: bd9cb656-d742-4a18-97a2-546d4056d093
source-git-commit: edf49d8a52eeddea65a18c1dad0035ec7e5d2c12
workflow-type: tm+mt
source-wordcount: '3086'
ht-degree: 0%

---

# [!DNL Salesforce CRM] 連接

## 總覽 {#overview}

[[!DNL Salesforce CRM]](https://www.salesforce.com/crm/) 是一個流行的客戶關係管理(CRM)平台，它支援以下內容：

* [銷售線索](https://developer.salesforce.com/docs/atlas.en-us.object_reference.meta/object_reference/sforce_api_objects_lead.htm)  — 潛在顧客是指可能（或可能不會）對您銷售的產品或服務感興趣的個人或公司的名稱。
* [聯繫人](https://developer.salesforce.com/docs/atlas.en-us.object_reference.meta/object_reference/sforce_api_objects_contact.htm)  — 聯繫人是您的一位代表已與其建立關係，並且有資格成為潛在客戶的個人。

此 [!DNL Adobe Experience Platform] [目標](/help/destinations/home.md) 利用 [[!DNL Salesforce composite API]](https://developer.salesforce.com/docs/atlas.en-us.api_rest.meta/api_rest/resources_composite_sobjects_collections_update.htm)，它支援上述兩種類型的配置檔案。

當 [激活段](#activate)您可以在潛在客戶或聯繫人之間進行選擇，並將屬性和段資料更新到 [!DNL Salesforce CRM]。

[!DNL Salesforce CRM] 使用OAuth 2和Password Grant作為驗證機制與Salesforce REST API通信。 驗證到您 [!DNL Salesforce CRM] 下面是實例， [驗證到目標](#authenticate) 的子菜單。

## 使用案例 {#use-cases}

作為營銷人員，您可以根據用戶的Adobe Experience Platform配置檔案的屬性向用戶提供個性化體驗。 您可以從離線資料構建段，並將這些段發送到Salesforce CRM，以便在段和配置檔案在Adobe Experience Platform更新後立即顯示在用戶源中。

## 先決條件 {#prerequisites}

### Experience Platform中的先決條件 {#prerequisites-in-experience-platform}

在將資料激活到Salesforce CRM目標之前，必須有 [架構](/help/xdm/schema/composition.md)的 [資料集](https://experienceleague.adobe.com/docs/platform-learn/tutorials/data-ingestion/create-datasets-and-ingest-data.html?lang=en), [段](https://experienceleague.adobe.com/docs/platform-learn/tutorials/segments/create-segments.html?lang=en) 建立 [!DNL Experience Platform]。

### 中的先決條件 [!DNL Salesforce CRM] {#prerequisites-destination}

請注意以下先決條件 [!DNL Salesforce CRM]，以便將資料從平台導出到Salesforce帳戶：

#### 你需要 [!DNL Salesforce] 帳戶 {#prerequisites-account}

轉到 [!DNL Salesforce] [審判](https://www.salesforce.com/in/form/signup/freetrial-sales/) 要註冊和建立的頁 [!DNL Salesforce] 帳戶，如果你還沒有。

#### 在中配置連接的應用 [!DNL Salesforce] {#prerequisites-connected-app}

首先，您需要配置 [[!DNL Salesforce] 連接的應用](https://help.salesforce.com/s/articleView?id=sf.connected_app_create.htm&amp;language=en_US&amp;r=https%3A%2F%2Fhelp.salesforce.com%2F&amp;type=5) 在 [!DNL Salesforce] 帳戶，如果你還沒有。 [!DNL Salesforce CRM] 將利用連接的應用連接到 [!DNL Salesforce]。

接下來，啟用 [!DNL OAuth Settings for API Integration] 為 [!DNL Salesforce connected app]。 請參閱 [[!DNL Salesforce]](https://help.salesforce.com/s/articleView?id=connected_app_create_api_integration.htm&amp;type=5&amp;language=en_US) 文檔以獲取指導。

另外，確保 [作用域](https://help.salesforce.com/s/articleView?id=connected_app_create_api_integration.htm&amp;type=5&amp;language=en_US) 下面提到的內容 [!DNL Salesforce connected app]。

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

最後，確保 `password` 在 [!DNL Salesforce] 帳戶。 請參閱 [!DNL Salesforce] [用於特殊方案的OAuth 2.0用戶名 — 密碼流](https://help.salesforce.com/s/articleView?id=sf.remoteaccess_oauth_username_password_flow.htm&amp;type=5) 文檔。

>[!IMPORTANT]
>
>如果 [!DNL Salesforce] 帳戶管理員對受信任的IP範圍有限制的訪問權限，您需要聯繫他們以獲取 [Experience PlatformIP](/help/destinations/catalog/streaming/ip-address-allow-list.md) 已列出。 請參閱 [!DNL Salesforce] [限制對已連接應用的受信任IP範圍的訪問](https://help.salesforce.com/s/articleView?id=sf.connected_app_edit_ip_ranges.htm&amp;type=5) 文檔。

#### 在中建立自定義欄位 [!DNL Salesforce] {#prerequisites-custom-field}

將段激活到 [!DNL Salesforce CRM] 目標，必須在 **[!UICONTROL 映射ID]** 欄位中 **[段計畫](#schedule-segment-export-example)** 的子菜單。

[!DNL Salesforce CRM] 要求此值正確讀取和解釋從Experience Platform傳入的段，並更新其段狀態 [!DNL Salesforce]。 請參閱Experience Platform文檔，瞭解 [段成員身份詳細資訊架構欄位組](/help/xdm/field-groups/profile/segmentation.md) 如果需要有關段狀態的指導。

對於從平台激活到 [!DNL Salesforce CRM]，需要建立類型的自定義欄位 `Text Area (Long)` 內 [!DNL Salesforce]。 您可以根據業務要求定義任意大小的欄位字元長度（256 - 131,072個字元）。 查看 [!DNL Salesforce] [自定義欄位類型](https://help.salesforce.com/s/articleView?id=sf.custom_field_types.htm&amp;type=5) 文檔」頁，以獲取有關自定義欄位類型的其他資訊。 另請參閱 [!DNL Salesforce] 文檔 [建立自定義欄位](https://help.salesforce.com/s/articleView?id=mc_cab_create_an_attribute.htm&amp;type=5&amp;language=en_US) 在建立欄位時需要幫助。

>[!IMPORTANT]
>
>欄位名稱中不包含空格字元。 而是使用下划線 `(_)` 字元作為分隔符。
>在 [!DNL Salesforce] 必須使用 **[!UICONTROL 欄位名稱]** 與指定的值完全匹配 **[!UICONTROL 映射ID]** 每個激活的平台段。 例如，下面的螢幕快照顯示一個名為 `crm_2_seg`。 激活段到此目標時，添加 `crm_2_seg` 如 **[!UICONTROL 映射ID]** 將段訪問群體從Experience Platform填充到此自定義欄位。

在中建立自定義欄位的示例 [!DNL Salesforce]。 *步驟1 — 選擇資料類型*，如下所示：
![顯示自定義欄位建立的Salesforce UI螢幕快照，步驟1 — 選擇資料類型。](../../assets/catalog/crm/salesforce/create-salesforce-custom-field-step-1.png)

在中建立自定義欄位的示例 [!DNL Salesforce]。 *步驟2 — 輸入自定義欄位的詳細資訊*，如下所示：
![顯示自定義欄位建立的Salesforce UI螢幕快照，步驟2 — 輸入自定義欄位的詳細資訊。](../../assets/catalog/crm/salesforce/create-salesforce-custom-field-step-2.png)

>[!TIP]
>
>* 區分用於平台段的自定義欄位和中的其他自定義欄位 [!DNL Salesforce] 在建立自定義欄位時，可以包含可識別的前置詞或尾碼。 例如， `test_segment`。 `Adobe_test_segment` 或 `test_segment_Adobe`
>* 如果已在中建立了其他自定義欄位 [!DNL Salesforce]，可以使用與平台段相同的名稱，以便輕鬆識別 [!DNL Salesforce]。


>[!NOTE]
>
>* Salesforce中的對象被限制為25個外部欄位，請參閱 [自定義欄位屬性](https://help.salesforce.com/s/articleView?id=sf.custom_field_attributes.htm&amp;type=5)。
>* 此限制意味著您在任何時候最多只能有25個Experience Platform段成員資格處於活動狀態。
>* 如果您在Salesforce內已達到此限制，則必須從Salesforce中刪除自定義屬性，這些屬性用於將段狀態儲存在Experience Platform內舊段之後，再添加新段 **[!UICONTROL 映射ID]** 可使用。


#### 收集 [!DNL Salesforce CRM] 憑據 {#gather-credentials}

在驗證到 [!DNL Salesforce CRM] 目標：

| 憑據 | 說明 | 範例 |
| --- | --- | --- |
| `Username` | 您 [!DNL Salesforce] 帳戶用戶名。 |  |
| `Password` | 您 [!DNL Salesforce] 帳戶密碼。 |  |
| `Security Token` | 您 [!DNL Salesforce] 安全令牌，稍後您將附加到 [!DNL Salesforce] 用於建立要用作 **[!UICONTROL 密碼]** 何時 [向目的地驗證](#authenticate)。<br> 請參閱 [!DNL Salesforce] 文檔 [重置安全令牌](https://help.salesforce.com/s/articleView?id=sf.user_security_token.htm&amp;type=5) 學習如何從 [!DNL Salesforce] 的子菜單。 |  |
| `Custom Domain` | 您 [!DNL Salesforce] 域前置詞。 <br> 查看 [[!DNL Salesforce] 文檔](https://help.salesforce.com/s/articleView?id=sf.domain_name_setting_login_policy.htm&amp;type=5) 瞭解如何從 [!DNL Salesforce] 。 | 如果 [!DNL Salesforce] 域<br> *`d5i000000isb4eak-dev-ed`.my.salesforce.com*。<br> 你需要 `d5i000000isb4eak-dev-ed` 值。 |
| `Client ID` | 您的銷售人員 `Consumer Key`。 <br> 請參閱 [[!DNL Salesforce] 文檔](https://help.salesforce.com/s/articleView?id=sf.connected_app_rotate_consumer_details.htm&amp;type=5) 瞭解如何從 [!DNL Salesforce] 。 |  |
| `Client Secret` | 您的銷售人員 `Consumer Secret`。 <br> 請參閱 [[!DNL Salesforce] 文檔](https://help.salesforce.com/s/articleView?id=sf.connected_app_rotate_consumer_details.htm&amp;type=5) 瞭解如何從 [!DNL Salesforce] 。 |  |

### 護欄 {#guardrails}

[!DNL Salesforce] 通過施加請求、費率和超時限制來平衡事務負載。 請參閱 [API請求限制和分配](https://developer.salesforce.com/docs/atlas.en-us.salesforce_app_limits_cheatsheet.meta/salesforce_app_limits_cheatsheet/salesforce_app_limits_platform_api.htm) 的雙曲餘切值。

如果 [!DNL Salesforce] 帳戶管理員已強制實施IP限制，您需要添加 [Experience PlatformIP地址](/help/destinations/catalog/streaming/ip-address-allow-list.md) 到 [!DNL Salesforce] 帳戶的受信任IP範圍。 請參閱 [!DNL Salesforce] [限制對已連接應用的受信任IP範圍的訪問](https://help.salesforce.com/s/articleView?id=sf.connected_app_edit_ip_ranges.htm&amp;type=5) 文檔。

>[!IMPORTANT]
>
>當 [激活段](#activate) 必須選擇 *聯繫人* 或 *線索* 的下界。 您需要根據所選類型確保段具有適當的資料映射。

## 支援的身份 {#supported-identities}

[!DNL Salesforce CRM] 支援更新下表中描述的身份。 瞭解有關 [身份](/help/identity-service/namespaces.md)。

| 目標標識 | 說明 | 考量事項 |
|---|---|---|
| `SalesforceId` | 的 [!DNL Salesforce CRM] 聯繫人或潛在顧客標識的標識符，您可以通過您的網段導出或更新。 | 必要 |

## 導出類型和頻率 {#export-type-frequency}

有關目標導出類型和頻率的資訊，請參閱下表。

| 項目 | 類型 | 附註 |
---------|----------|---------|
| 導出類型 | **[!UICONTROL 基於配置檔案]** | <ul><li>您正在導出段的所有成員以及所需的架構欄位 *(例如：電子郵件地址、電話號碼、姓氏)*，根據您的欄位映射。</li><li> 中的每個段狀態 [!DNL Salesforce CRM] 將根據 **[!UICONTROL 映射ID]** 值 [段調度](#schedule-segment-export-example) 的子菜單。</li></ul> |
| 導出頻率 | **[!UICONTROL 流]** | <ul><li>流目標是基於API的「始終開啟」連接。 一旦基於段評估在Experience Platform中更新配置檔案，連接器就將更新下游發送到目標平台。 閱讀有關 [流目標](/help/destinations/destination-types.md#streaming-destinations)。</li></ul> |

{style="table-layout:auto"}

## 連接到目標 {#connect}

>[!IMPORTANT]
>
>要連接到目標，您需要 **[!UICONTROL 管理目標]** [訪問控制權限](/help/access-control/home.md#permissions)。 閱讀 [訪問控制概述](/help/access-control/ui/overview.md) 或聯繫您的產品管理員以獲取所需權限。

要連接到此目標，請按照 [目標配置教程](../../ui/connect-destination.md)。 在配置目標工作流中，填寫下面兩節中列出的欄位。

在 **[!UICONTROL 目標]** > **[!UICONTROL 目錄]** 搜索 [!DNL Salesforce CRM]。 或者，可將其定位在 **[!UICONTROL CRM]** 的子菜單。

### 驗證到目標 {#authenticate}

要向目標進行身份驗證，請填寫下面的必填欄位，然後選擇 **[!UICONTROL 連接到目標]**。 請參閱 [收集 [!DNL Salesforce CRM] 憑據](#gather-credentials) 的雙曲餘切值。
|憑據 |描述 | | - | - | | **[!UICONTROL 用戶名]** |您的 [!DNL Salesforce] 帳戶用戶名。 | | **[!UICONTROL 密碼]** |由 [!DNL Salesforce] 附加了帳戶密碼 [!DNL Salesforce] 安全令牌。<br>級連值的形式為 `{PASSWORD}{TOKEN}`。<br> 注意，不要使用任何大括弧或空格。<br>例如，如果 [!DNL Salesforce] 密碼為 `MyPa$$w0rd123` 和 [!DNL Salesforce] 安全令牌是 `TOKEN12345....0000`，將在 **[!UICONTROL 密碼]** 欄位 `MyPa$$w0rd123TOKEN12345....0000`。 | | **[!UICONTROL 自定義域]** |您的 [!DNL Salesforce] 域前置詞。 <br>例如，如果域 *`d5i000000isb4eak-dev-ed`.my.salesforce.com*&#x200B;您需要提供 `d5i000000isb4eak-dev-ed` 值。 | | **[!UICONTROL 客戶端ID]** |您的 [!DNL Salesforce] 連接的應用 `Consumer Key`。 | | **[!UICONTROL 客戶端密碼]** |您的 [!DNL Salesforce] 連接的應用 `Consumer Secret`。 |

![平台UI螢幕快照，顯示如何進行身份驗證。](../../assets/catalog/crm/salesforce/authenticate-destination.png)

如果提供的詳細資訊有效，UI將顯示 **[!UICONTROL 已連接]** 狀態為綠色複選標籤，然後可以繼續執行下一步。

### 填寫目標詳細資訊 {#destination-details}

要配置目標的詳細資訊，請填寫以下必需欄位和可選欄位。 UI中某個欄位旁邊的星號表示該欄位是必需的。
* **[!UICONTROL 名稱]**:您將來識別此目標的名稱。
* **[!UICONTROL 說明]**:將幫助您在將來確定此目標的說明。
* **[!UICONTROL Salesforce ID類型]**:
   * 選擇 **[!UICONTROL 聯繫人]** 如果您要導出或更新的標識類型 *聯繫人*。
   * 選擇 **[!UICONTROL 線索]** 如果您要導出或更新的標識類型 *線索*。

![顯示目標詳細資訊的平台UI螢幕快照。](../../assets/catalog/crm/salesforce/destination-details.png)

### 啟用警報 {#enable-alerts}

您可以啟用警報來接收有關目標資料流狀態的通知。 從清單中選擇要訂閱的警報以接收有關資料流狀態的通知。 有關警報的詳細資訊，請參閱上的指南 [使用UI訂閱目標警報](../../ui/alerts.md)。

完成提供目標連接的詳細資訊後，選擇 **[!UICONTROL 下一個]**。

## 將段激活到此目標 {#activate}

>[!IMPORTANT]
>
>要激活資料，您需要 **[!UICONTROL 管理目標]**。 **[!UICONTROL 激活目標]**。 **[!UICONTROL 查看配置檔案]**, **[!UICONTROL 查看段]** [訪問控制權限](/help/access-control/home.md#permissions)。 閱讀 [訪問控制概述](/help/access-control/ui/overview.md) 或聯繫您的產品管理員以獲取所需權限。

閱讀 [激活配置檔案和段以流式處理段導出目標](/help/destinations/ui/activate-segment-streaming-destinations.md) 有關激活此目標受眾段的說明。

### 映射注意事項和示例 {#mapping-considerations-example}

正確將您的受眾資料從Adobe Experience Platform發送到 [!DNL Salesforce CRM] 目標，您需要完成欄位映射步驟。 映射包括在您的平台帳戶中的「體驗資料模型」(XDM)架構欄位與目標目標中對應的欄位之間建立連結。

在 **[!UICONTROL 目標欄位]** 應按照屬性映射表中所述命名，因為這些屬性將構成請求正文。

在 **[!UICONTROL 源欄位]** 不要遵守任何此類限制。 您可以根據需要映射它，但是，根據 [[!DNL Salesforce] 文檔](https://help.salesforce.com/s/articleView?id=sf.custom_field_attributes.htm&amp;type=5)。 如果輸入資料無效，則更新調用 [!DNL Salesforce] 將失敗，您的聯繫人/線索將不會更新。

正確將XDM欄位映射到 [!DNL (API) Salesforce CRM] 目標欄位，請執行以下步驟：

1. 在 **[!UICONTROL 映射]** 步驟，選擇 **[!UICONTROL 添加新映射]**，您將在螢幕上看到新的映射行。
   ![「添加新映射」的平台UI螢幕快照示例。](../../assets/catalog/crm/salesforce/add-new-mapping.png)
1. 在 **[!UICONTROL 選擇源欄位]** ，選擇 **[!UICONTROL 選擇屬性]** 類別，然後選擇XDM屬性或 **[!UICONTROL 選擇標識命名空間]** 並選擇標識。
1. 在 **[!UICONTROL 選擇目標欄位]** ，選擇 **[!UICONTROL 選擇標識命名空間]** 選擇標識或 **[!UICONTROL 選擇自定義屬性]** 類別，然後使用 **[!UICONTROL 屬性名稱]** 欄位。 請參閱 [[!DNL Salesforce CRM] 文檔](https://help.salesforce.com/s/articleView?id=sf.custom_field_attributes.htm&amp;type=5) 的子目錄。
   * 重複這些步驟，在XDM配置檔案架構和 [!DNL (API) Salesforce CRM]:

   **使用聯繫人**

   * 如果您正在 *聯繫人* 在段內，請參閱Salesforce中的Object Reference [聯繫人](https://developer.salesforce.com/docs/atlas.en-us.object_reference.meta/object_reference/sforce_api_objects_contact.htm) 定義要更新的欄位的映射。
   * 您可以通過搜索該詞來標識必填欄位 *必需*，上述連結的欄位說明中提到。
   * 根據要導出或更新的欄位，在XDM配置檔案架構和 [!DNL (API) Salesforce CRM]: |源欄位|目標欄位|注釋 | | - | - | - | |`IdentityMap: crmID`|`Identity: SalesforceId`|`Mandatory`| |`xdm: person.name.lastName`|`Attribute: LastName`| `Mandatory`。 聯繫人的姓，最多80個字元。 |\
      |`xdm: person.name.firstName`|`Attribute: FirstName`|聯繫人的名字，最多40個字元。 | |`xdm: personalEmail.address`|`Attribute: Email`|聯繫人的電子郵件地址。 |

   * 下面顯示了使用這些映射的示例：
      ![平台UI螢幕快照示例，顯示目標映射。](../../assets/catalog/crm/salesforce/mappings-contacts.png)

   **使用Lead**

   * 如果您正在 *銷售線索* 在段內，請參閱Salesforce中的Object Reference [線索](https://developer.salesforce.com/docs/atlas.en-us.object_reference.meta/object_reference/sforce_api_objects_lead.htm) 定義要更新的欄位的映射。
   * 您可以通過搜索該詞來標識必填欄位 *必需*，上述連結的欄位說明中提到。
   * 根據要導出或更新的欄位，在XDM配置檔案架構和 [!DNL (API) Salesforce CRM]: |源欄位|目標欄位|注釋 | | - | - | - | |`IdentityMap: crmID`|`Identity: SalesforceId`|`Mandatory`| |`xdm: person.name.lastName`|`Attribute: LastName`| `Mandatory`。 最多80個字元的線索的姓。 |\
      |`xdm: b2b.companyName`|`Attribute: Company`| `Mandatory`。 領導的公司。 | |`xdm: personalEmail.address`|`Attribute: Email`|潛在顧客的電子郵件地址。 |

   * 下面顯示了使用這些映射的示例：
      ![平台UI螢幕快照示例，顯示目標映射。](../../assets/catalog/crm/salesforce/mappings-leads.png)



完成為目標連接提供映射後，選擇 **[!UICONTROL 下一個]**。

### 計畫段導出和示例 {#schedule-segment-export-example}

執行 [計畫段導出](/help/destinations/ui/activate-segment-streaming-destinations.md#scheduling) 步驟必須手動將從平台激活的段映射到其相應的自定義欄位 [!DNL Salesforce]。

為此，請選擇每個段，然後輸入自定義欄位名 [!DNL Salesforce] 的 [!DNL Salesforce CRM] **[!UICONTROL 映射ID]** 的子菜單。 請參閱 [在中建立自定義欄位 [!DNL Salesforce]](#prerequisites-custom-field) 中有關建立自定義欄位的指導和最佳做法部分 [!DNL Salesforce]。

例如，如果 [!DNL Salesforce] 自定義域 `crm_2_seg`，在 [!DNL Salesforce CRM] **[!UICONTROL 映射ID]** 將段訪問群體從Experience Platform填充到此自定義欄位。

自定義欄位的示例 [!DNL Salesforce] 如下所示：
![[!DNL Salesforce] 顯示自定義欄位的UI螢幕快照。](../../assets/catalog/crm/salesforce/salesforce-custom-field.png)

一個示例，指示 [!DNL Salesforce CRM] **[!UICONTROL 映射ID]** 如下所示：
![平台UI螢幕快照示例，顯示「計畫」段導出。](../../assets/catalog/crm/salesforce/schedule-segment-export.png)

如 [!DNL Salesforce] **[!UICONTROL 欄位名稱]** 與中指定的值完全匹配 [!DNL Salesforce CRM] **[!UICONTROL 映射ID]**。

根據您的使用案例，所有激活的段都可以映射到相同的 [!DNL Salesforce] 自定義域或不同 **[!UICONTROL 欄位名稱]** 在 [!DNL Salesforce CRM]。 以上影像為基礎，可以作為典型實例。
| [!DNL Salesforce CRM] 段名稱 | [!DNL Salesforce] **[!UICONTROL 欄位名稱]** | [!DNL Salesforce CRM] **[!UICONTROL 映射ID]** | | - | - | - | | crm_1_seg | `crm_1_seg` | `crm_1_seg` | | crm_2_seg | `crm_2_seg` | `crm_2_seg` |

對每個激活的平台段重複此部分。

## 驗證資料導出 {#exported-data}

要驗證您是否正確設定了目標，請執行以下步驟：

1. 選擇 **[!UICONTROL 目標]** > **[!UICONTROL 瀏覽]** 導航至目標清單。
   ![顯示「瀏覽目標」的平台UI螢幕快照。](../../assets/catalog/crm/salesforce/browse-destinations.png)

1. 選擇目標並驗證狀態是否為 **[!UICONTROL 啟用]**。
   ![顯示目標資料流運行的平台UI螢幕快照。](../../assets/catalog/crm/salesforce/destination-dataflow-run.png)

1. 切換到 **[!UICONTROL 激活資料]** ，然後選擇段名稱。
   ![平台UI螢幕快照示例，顯示目標激活資料。](../../assets/catalog/crm/salesforce/destinations-activation-data.png)

1. 監視段摘要並確保配置檔案計數與段內建立的計數相對應。
   ![平台UI螢幕抓圖示例顯示「段」。](../../assets/catalog/crm/salesforce/segment.png)

1. 最後，登錄Salesforce網站並驗證是否添加或更新了該段中的配置檔案。

   **使用聯繫人**

   * 如果已選擇 *聯繫人* 在平台段內，導航至 **[!DNL Apps]** > **[!DNL Contacts]** 的子菜單。
      ![Salesforce CRM螢幕快照顯示「聯繫人」頁，其中包含段中的配置檔案。](../../assets/catalog/crm/salesforce/contacts.png)

   * 選擇 *聯繫人* 並檢查欄位是否已更新。 您可以看到 [!DNL Salesforce CRM] 已根據 **[!UICONTROL 映射ID]** 值 [段調度](#schedule-segment-export-example)。
      ![Salesforce CRM螢幕快照，顯示具有更新的段狀態的「聯繫人詳細資訊」頁。](../../assets/catalog/crm/salesforce/contact-info.png)

   **使用Lead**

   * 如果已選擇 *銷售線索* 在平台段內，然後導航至 **[!DNL Apps]** > **[!DNL Leads]** 的子菜單。
      ![Salesforce CRM螢幕快照，顯示帶有段中配置檔案的Lead頁。](../../assets/catalog/crm/salesforce/leads.png)

   * 選擇 *線索* 並檢查欄位是否已更新。 您可以看到 [!DNL Salesforce CRM] 已根據 **[!UICONTROL 映射ID]** 值 [段調度](#schedule-segment-export-example)。
      ![Salesforce CRM螢幕快照，顯示具有更新的段狀態的「銷售線索詳細資訊」頁。](../../assets/catalog/crm/salesforce/lead-info.png)


## 資料使用和治理 {#data-usage-governance}

全部 [!DNL Adobe Experience Platform] 目標在處理資料時符合資料使用策略。 有關如何 [!DNL Adobe Experience Platform] 強制實施資料治理，請參見 [資料治理概述](/help/data-governance/home.md)。

## 錯誤和故障排除 {#errors-and-troubleshooting}

### 將事件推送到目標時遇到未知錯誤 {#unknown-errors}

* 檢查資料流運行時，可能會遇到以下錯誤消息： `Unknown errors encountered while pushing events to the destination. Please contact the administrator and try again.`

   ![顯示錯誤的平台UI螢幕快照。](../../assets/catalog/crm/salesforce/error.png)

   * 要修復此錯誤，請驗證 **[!UICONTROL 映射ID]** 您在激活工作流中提供的 [!DNL Salesforce CRM] 目標與您在中建立的自定義欄位類型的值完全匹配 [!DNL Salesforce]。 請參閱 [在中建立自定義欄位 [!DNL Salesforce]](#prerequisites-custom-field) 的子菜單。

* 激活段時，可能會獲得錯誤消息： `The client's IP address is unauthorized for this account. Allowlist the client's IP address...`
   * 要修復此錯誤，請與 [!DNL Salesforce] 帳戶管理員添加 [Experience PlatformIP地址](/help/destinations/catalog/streaming/ip-address-allow-list.md) 到 [!DNL Salesforce] 帳戶的受信任IP範圍。 請參閱 [!DNL Salesforce] [限制對已連接應用的受信任IP範圍的訪問](https://help.salesforce.com/s/articleView?id=sf.connected_app_edit_ip_ranges.htm&amp;type=5) 文檔。

## 其他資源 {#additional-resources}

來自 [Salesforce開發人員門戶](https://developer.salesforce.com/) 如下：
* [快速入門](https://developer.salesforce.com/docs/atlas.en-us.api_rest.meta/api_rest/quickstart.htm)
* [建立記錄](https://developer.salesforce.com/docs/atlas.en-us.api_rest.meta/api_rest/dome_sobject_create.htm)
* [自定義建議受眾](https://developer.salesforce.com/docs/atlas.en-us.236.0.chatterapi.meta/chatterapi/connect_resources_recommendation_audiences_list.htm)
* [使用複合資源](https://developer.salesforce.com/docs/atlas.en-us.api_rest.meta/api_rest/using_composite_resources.htm?q=composite)
* 此目標利用 [更新多個記錄](https://developer.salesforce.com/docs/atlas.en-us.api_rest.meta/api_rest/resources_composite_sobjects_collections_update.htm) API而不是 [Upsert單條記錄](https://developer.salesforce.com/docs/atlas.en-us.api_rest.meta/api_rest/dome_composite_upsert_example.htm?q=contacts) API調用。