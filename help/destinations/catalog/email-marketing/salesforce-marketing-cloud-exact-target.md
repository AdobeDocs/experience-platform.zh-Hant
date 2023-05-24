---
keywords: 電子郵件；電子郵件；電子郵件；電子郵件目標；salesforce;api salesforce市場營銷雲目標
title: (API)SalesforceMarketing Cloud連接
description: SalesforceMarketing Cloud（以前稱為ExactTarget）目標允許您導出帳戶資料並在SalesforceMarketing Cloud中根據您的業務需要將其激活。
exl-id: 0cf068e6-8a0a-4292-a7ec-c40508846e27
source-git-commit: 877bf4886e563e8a571f067c06107776a0c81d5d
workflow-type: tm+mt
source-wordcount: '2911'
ht-degree: 1%

---

# [!DNL (API) Salesforce Marketing Cloud] 連接

## 總覽 {#overview}

[[!DNL (API) Salesforce Marketing Cloud]](https://www.salesforce.com/products/marketing-cloud/engagement/) (前稱 [!DNL ExactTarget])是一個數字營銷套件，允許您為訪問者和客戶構建和定制行程，以個性化其體驗。

>[!IMPORTANT]
>
>注意此連接與其他連接之間的差異 [[!DNL Salesforce Marketing Cloud] 連接](/help/destinations/catalog/email-marketing/salesforce-marketing-cloud.md) 在「電子郵件營銷目錄」部分中存在。 其他SalesforceMarketing Cloud連接允許您將檔案導出到指定的儲存位置，而這是基於API的流連接。

與 [!DNL Salesforce Marketing Cloud Account Engagement] 更傾向於 **B2B** 營銷， [!DNL (API) Salesforce Marketing Cloud] 目的地是理想的 **B2C** 使用事務性決策週期較短的案例。 您可以整合代表目標受眾行為的較大資料集，通過對聯繫人進行優先順序排序和分段來調整和改進營銷活動，尤其是從外部資料集中 [!DNL Salesforce]。 *注意，Experience Platform還與 [[!DNL Salesforce Marketing Cloud Account Engagement]](/help/destinations/catalog/email-marketing/salesforce-marketing-cloud-account-engagement.md)。*

此 [!DNL Adobe Experience Platform] [目標](/help/destinations/home.md) 利用 [!DNL Salesforce Marketing Cloud] [更新聯繫人](https://developer.salesforce.com/docs/marketing/marketing-cloud/guide/updateContacts.html) API，它允許您 **添加聯繫人和更新聯繫人資料** 在新內激活後滿足您的業務需求 [!DNL Salesforce Marketing Cloud] 段。

[!DNL Salesforce Marketing Cloud] 使用OAuth 2和客戶端憑據作為與 [!DNL Salesforce Marketing Cloud] API。 驗證到您 [!DNL Salesforce Marketing Cloud] 下面是實例， [驗證到目標](#authenticate) 的子菜單。

## 使用案例 {#use-cases}

幫助您更好地瞭解您應如何以及何時使用 [!DNL (API) Salesforce Marketing Cloud] 目的地，這裡是Adobe Experience Platform客戶可通過使用此目的地解決的示例使用案例。

### 將電子郵件發送到營銷活動的聯繫人 {#use-case-send-emails}

一個房屋租賃平台的銷售部門希望向目標客戶廣播一封營銷電子郵件。 平台的營銷團隊可以添加新聯繫人/更新現有聯繫人 *（及其電子郵件地址）* 通過Adobe Experience Platform，從自己的離線資料構建資料段，並將這些資料段發送到 [!DNL Salesforce Marketing Cloud]，然後可用於發送營銷活動電子郵件。

## 先決條件 {#prerequisites}

### Experience Platform中的先決條件 {#prerequisites-in-experience-platform}

在將資料激活到 [!DNL (API) Salesforce Marketing Cloud] 目標，您必須 [架構](/help/xdm/schema/composition.md)的 [資料集](https://experienceleague.adobe.com/docs/platform-learn/tutorials/data-ingestion/create-datasets-and-ingest-data.html?lang=en), [段](https://experienceleague.adobe.com/docs/platform-learn/tutorials/segments/create-segments.html?lang=en) 建立 [!DNL Experience Platform]。

### 中的先決條件 [!DNL (API) Salesforce Marketing Cloud] {#prerequisites-destination}

請注意以下先決條件，以便將資料從平台導出到 [!DNL Salesforce Marketing Cloud] 帳戶：

#### 你需要 [!DNL Salesforce Marketing Cloud] 帳戶 {#prerequisites-account}

A [!DNL Salesforce Marketing Cloud] 具有訂閱的帳戶 [[!DNL Marketing Cloud Engagement]](https://www.salesforce.com/products/marketing-cloud/engagement/) 產品必須繼續。

伸向 [[!DNL Salesforce] 支援](https://www.salesforce.com/company/contact-us/?d=cta-glob-footer-10) 如果你沒有 [!DNL Salesforce Marketing Cloud] 帳戶或你的帳戶丟失 [!DNL Marketing Cloud Engagement] 產品訂閱。

#### 在中建立屬性 [!DNL Salesforce Marketing Cloud] {#prerequisites-attribute}

將段激活到 [!DNL (API) Salesforce Marketing Cloud] 目標，必須在 **[!UICONTROL 映射ID]** 欄位中 **[段計畫](#schedule-segment-export-example)** 的子菜單。

[!DNL Salesforce] 要求此值正確讀取和解釋從Experience Platform傳入的段，並更新其段狀態 [!DNL Salesforce Marketing Cloud]。 請參閱Experience Platform文檔，瞭解 [段成員身份詳細資訊架構欄位組](/help/xdm/field-groups/profile/segmentation.md) 如果需要有關段狀態的指導。

對於從平台激活到 [!DNL Salesforce Marketing Cloud]，需要建立類型的屬性 `Text` 內 [!DNL Salesforce]。 使用 [!DNL Salesforce Marketing Cloud] [!DNL Contact Builder] 的子菜單。 屬性欄位名用於 [!DNL (API) Salesforce Marketing Cloud] 目標欄位，應在 `[!DNL Email Demographics system attribute-set]`。 您可以根據業務要求定義欄位字元，最多4000個字元。 查看 [!DNL Salesforce Marketing Cloud] [資料擴展資料類型](https://help.salesforce.com/s/articleView?id=sf.mc_es_data_extension_data_types.htm&amp;type=5) 的子菜單。

請參閱 [!DNL Salesforce Marketing Cloud] 文檔 [建立屬性](https://help.salesforce.com/s/articleView?id=mc_cab_create_an_attribute.htm&amp;type=5&amp;language=en_US) 的子菜單。

中資料設計器螢幕的示例 [!DNL Salesforce Marketing Cloud]，將在其中添加屬性如下所示：
![SalesforceMarketing CloudUI資料設計器。](../../assets/catalog/email-marketing/salesforce-marketing-cloud-exact-target/salesforce-data-designer.png)

視圖 [!DNL Salesforce Marketing Cloud] [!DNL Email Demographics] attribute-set如下所示：
![SalesforceMarketing CloudUI電子郵件統計屬性集。](../../assets/catalog/email-marketing/salesforce-marketing-cloud-exact-target/salesforce-email-demograhics-fields.png)

的 [!DNL (API) Salesforce Marketing Cloud] 目標使用 [!DNL Salesforce Marketing Cloud] [!DNL Search Attribute-Set Definitions REST] [API](https://developer.salesforce.com/docs/marketing/marketing-cloud/guide/retrieveAttributeSetDefinitions.html) 動態檢索屬性及其在中定義的屬性集 [!DNL Salesforce Marketing Cloud]。

這些資訊顯示在 **[!UICONTROL 目標欄位]** 設定時的「選擇」窗口 [映射](#mapping-considerations-example) 在工作流中 [將段激活到目標](#activate)。 請注意，只有在 [!DNL Salesforce Marketing Cloud] `[!DNL Email Demographics]` 支援屬性集。

>[!IMPORTANT]
>
>在 [!DNL Salesforce Marketing Cloud]，必須使用 **[!UICONTROL 欄位名稱]** 與指定的值完全匹配 **[!UICONTROL 映射ID]** 每個激活的平台段。 例如，下面的螢幕快照顯示一個名為 `salesforce_mc_segment_1`。 激活段到此目標時，添加 `salesforce_mc_segment_1` 如 **[!UICONTROL 映射ID]** 將段群體從Experience Platform填充到此屬性中。

在中建立屬性的示例 [!DNL Salesforce Marketing Cloud]，如下所示：
![顯示屬性的SalesforceMarketing CloudUI螢幕快照。](../../assets/catalog/email-marketing/salesforce-marketing-cloud-exact-target/salesforce-custom-field.png)

>[!TIP]
>
>* 建立屬性時，不要在欄位名稱中包含空格字元。 而是使用下划線 `(_)` 字元作為分隔符。
>* 區分用於平台段的屬性和中的其他屬性 [!DNL Salesforce Marketing Cloud]，您可以為用於Adobe段的屬性包含可識別的前置詞或尾碼。 例如， `test_segment`。 `Adobe_test_segment` 或 `test_segment_Adobe`。
>* 如果已在中建立其他屬性 [!DNL Salesforce Marketing Cloud]，可以使用與平台段相同的名稱，以便輕鬆識別 [!DNL Salesforce Marketing Cloud]。


#### 分配用戶角色和權限 [!DNL Salesforce Marketing Cloud] {#prerequisites-roles-permissions}

作為 [!DNL Salesforce Marketing Cloud] 支援自定義角色（取決於您的使用案例），應為您的用戶分配相關角色以更新您的 [!DNL Salesforce Marketing Cloud] 屬性集。 分配給用戶的角色示例如下所示：
![顯示其分配角色的選定用戶的SalesforceMarketing CloudUI。](../../assets/catalog/email-marketing/salesforce-marketing-cloud-exact-target/salesforce-edit-roles.png)

根據您的角色 [!DNL Salesforce Marketing Cloud] 已分配用戶，您還需要為 [!DNL Salesforce Marketing Cloud] 屬性集，其中包含要更新的欄位。

因為此目標需要訪問 `[!DNL Email Demographics system attribute-set]`，您需要允許 `Email` 如下所示：
![顯示具有允許權限的電子郵件屬性集的SalesforceMarketing CloudUI。](../../assets/catalog/email-marketing/salesforce-marketing-cloud-exact-target/salesforce-permisions-list.png)

要限制訪問級別，您還可以使用粒度權限覆蓋單個訪問。
![SalesforceMarketing CloudUI，顯示具有細粒度權限的電子郵件屬性集。](../../assets/catalog/email-marketing/salesforce-marketing-cloud-exact-target/sales-email-attribute-set-permission.png)

請參閱 [[!DNL Marketing Cloud Roles]](https://help.salesforce.com/s/articleView?language=en_US&amp;id=sf.mc_overview_marketing_cloud_roles.htm&amp;type=5) 和 [[!DNL Marketing Cloud Roles and Permissions]](https://help.salesforce.com/s/articleView?language=en_US&amp;id=sf.mc_overview_roles.htm&amp;type=5) 的子菜單。

#### 收集 [!DNL Salesforce Marketing Cloud] 憑據 {#gather-credentials}

在驗證到 [!DNL (API) Salesforce Marketing Cloud] 目標。

| 憑據 | 說明 | 範例 |
| --- | --- | --- |
| 子網域 | 請參閱 [[!DNL Salesforce Marketing Cloud domain prefix]](https://developer.salesforce.com/docs/marketing/marketing-cloud/guide/your-subdomain-tenant-specific-endpoints.html) 瞭解如何從 [!DNL Salesforce Marketing Cloud] 。 | 如果 [!DNL Salesforce Marketing Cloud] 域<br> *`mcq4jrssqdlyc4lph19nnqgzzs84`.login.exacttarget.com*。 <br>你需要提供 `mcq4jrssqdlyc4lph19nnqgzzs84` 值。 |
| 客戶端ID | 查看 [!DNL Salesforce Marketing Cloud] [文檔](https://developer.salesforce.com/docs/marketing/marketing-cloud/guide/access-token-s2s.html) 瞭解如何從 [!DNL Salesforce Marketing Cloud] 。 | r23kxxxxxxxx0z05xxxxxx |
| 客戶端密碼 | 查看 [!DNL Salesforce Marketing Cloud] [文檔](https://developer.salesforce.com/docs/marketing/marketing-cloud/guide/access-token-s2s.html) 瞭解如何從 [!DNL Salesforce Marketing Cloud] 。 | ipxxxxxxxxxxT4xxxxxxxxxx |

{style="table-layout:auto"}

### 護欄 {#guardrails}

* Salesforce強制 [速率限制](https://developer.salesforce.com/docs/marketing/marketing-cloud/guide/rate-limiting.html)。
   * 請參閱 [!DNL Salesforce Marketing Cloud] [文檔](https://developer.salesforce.com/docs/marketing/marketing-cloud/guide/rate-limiting-errors.html) 解決您在執行過程中可能遇到的任何可能限制並減少錯誤。
   * 請參閱 [[!DNL Salesforce Marketing Cloud] 項目定價](https://www.salesforce.com/editions-pricing/marketing-cloud/email/) 頁 *下載完整版比較圖表* 作為pdf，詳細列出計畫施加的限制。
   * 的 [API概述](https://developer.salesforce.com/docs/marketing/marketing-cloud/guide/apis-overview.html) 頁面詳細資訊附加限制。
   * 參考 [這裡](https://salesforce.stackexchange.com/questions/205898/marketing-cloud-api-limits) 的子菜單。
* 計數 *每個對象允許的自定義欄位* 根據您的Salesforce版本而有所不同。
   * 請參閱 [!DNL Salesforce] [文檔](https://help.salesforce.com/s/articleView?id=sf.custom_field_allocations.htm&amp;type=5) 的下界。
   * 如果已達到為定義的限制 *每個對象允許的自定義欄位* 內 [!DNL Salesforce Marketing Cloud] 你需要
      * 在中添加新屬性之前刪除舊屬性 [!DNL Salesforce Marketing Cloud]。
      * 更新或刪除平台目標中使用這些舊屬性名稱作為提供的值的任何激活的段 **[!UICONTROL 映射ID]** 在 [段調度](#schedule-segment-export-example) 的子菜單。

## 支援的身份 {#supported-identities}

[!DNL (API) Salesforce Marketing Cloud] 支援激活下表中描述的身份。 瞭解有關 [身份](/help/identity-service/namespaces.md)。

| 目標標識 | 說明 | 考量事項 |
|---|---|---|
| 聯繫人密鑰 | [!DNL Salesforce Marketing Cloud] 聯繫密鑰。 請參閱 [!DNL Salesforce Marketing Cloud] [文檔](https://help.salesforce.com/s/articleView?id=sf.mc_cab_contact_builder_best_practices.htm&amp;type=5) 如果你需要其他指導。 | 必要 |

## 導出類型和頻率 {#export-type-frequency}

有關目標導出類型和頻率的資訊，請參閱下表。

| 項目 | 類型 | 附註 |
---------|----------|---------|
| 導出類型 | **[!UICONTROL 基於配置檔案]** | <ul><li>您正在導出段的所有成員以及所需的架構欄位 *(例如：電子郵件地址、電話號碼、姓氏)*，根據您的欄位映射。</li><li> 中的每個段狀態 [!DNL Salesforce Marketing Cloud] 將根據 **[!UICONTROL 映射ID]** 值 [段調度](#schedule-segment-export-example) 的子菜單。</li></ul> |
| 導出頻率 | **[!UICONTROL 流]** | 流目標是基於API的「始終開啟」連接。 一旦基於段評估在Experience Platform中更新配置檔案，連接器就將更新下游發送到目標平台。 閱讀有關 [流目標](/help/destinations/destination-types.md#streaming-destinations)。 |

{style="table-layout:auto"}

## 連接到目標 {#connect}

>[!IMPORTANT]
>
>要連接到目標，您需要 **[!UICONTROL 管理目標]** [訪問控制權限](/help/access-control/home.md#permissions)。 閱讀 [訪問控制概述](/help/access-control/ui/overview.md) 或聯繫您的產品管理員以獲取所需權限。

要連接到此目標，請按照 [目標配置教程](../../ui/connect-destination.md)。 在配置目標工作流中，填寫下面兩節中列出的欄位。

在 **[!UICONTROL 目標]** > **[!UICONTROL 目錄]**，搜索 [!DNL (API) Salesforce Marketing Cloud]。 或者，可將其定位在 **[!UICONTROL 電子郵件營銷]** 的子菜單。

### 驗證到目標 {#authenticate}

要向目標進行身份驗證，請填寫下面的必填欄位，然後選擇 **[!UICONTROL 連接到目標]**。 請參閱 [收集 [!DNL Salesforce Marketing Cloud] 憑據](#gather-credentials) 的雙曲餘切值。

| [!DNL (API) Salesforce Marketing Cloud] 目標 | [!DNL Salesforce Marketing Cloud] |
| --- | --- |
| **[!UICONTROL 子網域]** | 您 [!DNL Salesforce Marketing Cloud] 域前置詞。 <br>例如，如果域 <br> *`mcq4jrssqdlyc4lph19nnqgzzs84`.login.exacttarget.com*。 <br> 你需要提供 `mcq4jrssqdlyc4lph19nnqgzzs84` 值。 |
| **[!UICONTROL 客戶端ID]** | 您 [!DNL Salesforce Marketing Cloud] `Client ID`。 |
| **[!UICONTROL 客戶端密碼]** | 您 [!DNL Salesforce Marketing Cloud] `Client Secret`。 |

![平台UI螢幕快照，顯示如何驗證到SalesforceMarketing Cloud。](../../assets/catalog/email-marketing/salesforce-marketing-cloud-exact-target/authenticate-destination.png)

如果提供的詳細資訊有效，UI將顯示 **[!UICONTROL 已連接]** 狀態為綠色複選標籤，然後可以繼續執行下一步。

### 填寫目標詳細資訊 {#destination-details}

要配置目標的詳細資訊，請填寫以下必需欄位和可選欄位。 UI中某個欄位旁邊的星號表示該欄位是必需的。
![顯示目標詳細資訊的平台UI螢幕快照。](../../assets/catalog/email-marketing/salesforce-marketing-cloud-exact-target/destination-details.png)

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

正確將您的受眾資料從Adobe Experience Platform發送到 [!DNL (API) Salesforce Marketing Cloud] 目標，您需要完成欄位映射步驟。 映射包括在您的平台帳戶中的「體驗資料模型」(XDM)架構欄位與目標目標中對應的欄位之間建立連結。

正確將XDM欄位映射到 [!DNL (API) Salesforce Marketing Cloud] 目標欄位，請執行以下步驟。

>[!IMPORTANT]
>
>雖然您的屬性名稱與 [!DNL Salesforce Marketing Cloud] 帳戶，兩者的映射 `contactKey` 和 `personalEmail.address` 的子菜單。 映射屬性時，僅Experience Platform中的屬性 `Email Demographics` 在目標欄位中應使用attribute-set。

1. 在 **[!UICONTROL 映射]** 步驟，選擇 **[!UICONTROL 添加新映射]**。 螢幕上將顯示新的映射行。
   ![「添加新映射」的平台UI螢幕快照示例。](../../assets/catalog/email-marketing/salesforce-marketing-cloud-exact-target/add-new-mapping.png)
1. 在 **[!UICONTROL 選擇源欄位]** ，選擇 **[!UICONTROL 選擇屬性]** 類別，然後選擇XDM屬性或 **[!UICONTROL 選擇標識命名空間]** 並選擇標識。
1. 在 **[!UICONTROL 選擇目標欄位]** ，選擇 **[!UICONTROL 選擇標識命名空間]** 選擇標識或 **[!UICONTROL 選擇自定義屬性]** 類別，然後從 `Email Demographics` 按需要顯示的屬性。 的 [!DNL (API) Salesforce Marketing Cloud] 目標使用 [!DNL Salesforce Marketing Cloud] [!DNL Search Attribute-Set Definitions REST] [API](https://developer.salesforce.com/docs/marketing/marketing-cloud/guide/retrieveAttributeSetDefinitions.html) 動態檢索在中定義的屬性及其屬性集 [!DNL Salesforce Marketing Cloud]。 這些資訊顯示在 **[!UICONTROL 目標欄位]** 設定 [映射](#mapping-considerations-example) 的 [將段激活至工作流](#activate)。 注意，僅映射在 [!DNL Salesforce Marketing Cloud] `[!DNL Email Demographics]` 支援屬性集。

   * 重複這些步驟，在XDM配置檔案架構和 [!DNL (API) Salesforce Marketing Cloud]: |源欄位|目標欄位|強制| |—|—| |`IdentityMap: contactKey`|`Identity: salesforceContactKey`| `Mandatory` |\
      |`xdm: person.name.firstName`|`Attribute: Email Demographics.First Name`| - |
|`xdm: personalEmail.address`|`Attribute: Email Addresses.Email Address`| - |

   * 下面顯示了使用這些映射的示例：
      ![平台UI螢幕快照示例，顯示目標映射。](../../assets/catalog/email-marketing/salesforce-marketing-cloud-exact-target/mappings.png)

完成為目標連接提供映射後，選擇 **[!UICONTROL 下一個]**。

### 計畫段導出和示例 {#schedule-segment-export-example}

執行 [計畫段導出](/help/destinations/ui/activate-segment-streaming-destinations.md#scheduling) 步驟，必須手動將平台段映射到 [屬性](#prerequisites-attribute) 在 [!DNL Salesforce Marketing Cloud]。

為此，請選擇每個段，然後從中輸入屬性名稱 [!DNL Salesforce Marketing Cloud] 的 [!DNL (API) Salesforce Marketing Cloud] **[!UICONTROL 映射ID]** 的子菜單。 請參閱 [在中建立屬性 [!DNL Salesforce Marketing Cloud]](#prerequisites-custom-field) 中建立屬性的指導和最佳做法部分 [!DNL Salesforce Marketing Cloud]。

例如，如果 [!DNL Salesforce Marketing Cloud] 屬性 `salesforce_mc_segment_1`，在 [!DNL (API) Salesforce Marketing Cloud] **[!UICONTROL 映射ID]** 將段群體從Experience Platform填充到此屬性中。

來自的示例屬性 [!DNL Salesforce Marketing Cloud] 如下所示：
![顯示屬性的SalesforceMarketing CloudUI螢幕快照。](../../assets/catalog/email-marketing/salesforce-marketing-cloud-exact-target/salesforce-custom-field.png)

一個示例，指示 [!DNL (API) Salesforce Marketing Cloud] **[!UICONTROL 映射ID]** 如下所示：
![平台UI螢幕快照示例，顯示「計畫」段導出。](../../assets/catalog/email-marketing/salesforce-marketing-cloud-exact-target/schedule-segment-export.png)

如所示 [!DNL (API) Salesforce Marketing Cloud] **[!UICONTROL 映射ID]** 應與中指定的值完全匹配 [!DNL Salesforce Marketing Cloud] **[!UICONTROL 欄位名稱]**。

對每個激活的平台段重複此部分。

根據您的使用案例，所有激活的段都可以映射到相同的 [!DNL Salesforce Marketing Cloud] **[!UICONTROL 欄位名稱]** 或 **[!UICONTROL 欄位名稱]** 在 [!DNL (API) Salesforce Marketing Cloud]。 以上影像為基礎，可以作為典型實例。
| [!DNL (API) Salesforce Marketing Cloud] 段名稱 | [!DNL Salesforce Marketing Cloud] **[!UICONTROL 欄位名稱]** | [!DNL (API) Salesforce Marketing Cloud] **[!UICONTROL 映射ID]** | | - | - | - | | salesforce mc段1 | `salesforce_mc_segment_1` | `salesforce_mc_segment_1` | | salesforce mc段2 | `salesforce_mc_segment_2` | `salesforce_mc_segment_2` |

## 驗證資料導出 {#exported-data}

要驗證您是否正確設定了目標，請執行以下步驟：

1. 選擇 **[!UICONTROL 目標]** > **[!UICONTROL 瀏覽]** 導航至目標清單。
   ![顯示「瀏覽目標」的平台UI螢幕快照。](../../assets/catalog/email-marketing/salesforce-marketing-cloud-exact-target/browse-destinations.png)

1. 選擇目標並驗證狀態是否為 **[!UICONTROL 啟用]**。
   ![顯示目標資料流運行的平台UI螢幕快照。](../../assets/catalog/email-marketing/salesforce-marketing-cloud-exact-target/destination-dataflow-run.png)

1. 切換到 **[!DNL Activation data]** ，然後選擇段名稱。
   ![平台UI螢幕快照示例，顯示目標激活資料。](../../assets/catalog/email-marketing/salesforce-marketing-cloud-exact-target/destinations-activation-data.png)

1. 監視段摘要並確保配置檔案計數與段內建立的計數相對應。
   ![平台UI螢幕抓圖示例顯示「段」。](../../assets/catalog/email-marketing/salesforce-marketing-cloud-exact-target/segment.png)

1. 登錄到 [[!DNL Salesforce Marketing Cloud]](https://mc.exacttarget.com/) 的子菜單。 然後導航到 **[!DNL Audience Builder]** > **[!DNL Contact Builder]** > **[!DNL All contacts]** > **[!DNL Email]** 並檢查是否已添加該段中的配置檔案。
   ![SalesforceMarketing CloudUI螢幕快照，顯示「聯繫人」頁，其中包含段中使用的配置檔案。](../../assets/catalog/email-marketing/salesforce-marketing-cloud-exact-target/contacts.png)

1. 要檢查是否更新了任何配置檔案，請導航到 **[!UICONTROL 電子郵件]** 並驗證是否更新了段中配置檔案的屬性值。 如果成功，您可以看到 [!DNL Salesforce Marketing Cloud] 已根據 **[!UICONTROL 映射ID]** 值 [段調度](#schedule-segment-export-example) 的子菜單。
   ![SalesforceMarketing CloudUI螢幕快照，顯示具有更新的段狀態的選定「聯繫人電子郵件」頁。](../../assets/catalog/email-marketing/salesforce-marketing-cloud-exact-target/contact-detail.png)

## 資料使用和治理 {#data-usage-governance}

全部 [!DNL Adobe Experience Platform] 目標在處理資料時符合資料使用策略。 有關如何 [!DNL Adobe Experience Platform] 強制實施資料治理，請參見 [資料治理概述](/help/data-governance/home.md)。

## 錯誤和故障排除 {#errors-and-troubleshooting}

### 將事件推送到SalesforceMarketing Cloud時遇到未知錯誤 {#unknown-errors}

* 檢查資料流運行時，可能會遇到以下錯誤消息： `Unknown errors encountered while pushing events to the destination. Please contact the administrator and try again.`

   ![顯示錯誤的平台UI螢幕快照。](../../assets/catalog/email-marketing/salesforce-marketing-cloud-exact-target/error.png)

   * 要修復此錯誤，請驗證 **[!UICONTROL 映射ID]** 您在激活工作流中提供的 [!DNL (API) Salesforce Marketing Cloud] 目標與您在中建立的屬性的名稱完全匹配 [!DNL Salesforce Marketing Cloud]。 請參閱 [在中建立屬性 [!DNL Salesforce Marketing Cloud]](#prerequisites-custom-field) 的子菜單。

* 激活段時，可能會獲得錯誤消息： `The client's IP address is unauthorized for this account. Allowlist the client's IP address...`
   * 要修復此錯誤，請與 [!DNL Salesforce Marketing Cloud] 帳戶管理員添加 [Experience PlatformIP地址](/help/destinations/catalog/streaming/ip-address-allow-list.md) 到 [!DNL Salesforce Marketing Cloud] 帳戶的受信任IP範圍。 請參閱 [!DNL Salesforce Marketing Cloud] [包含在Marketing Cloud中允許清單中的IP地址](https://help.salesforce.com/s/articleView?id=sf.mc_es_ip_addresses_for_inclusion.htm&amp;type=5) 文檔。

## 其他資源 {#additional-resources}

* [!DNL Salesforce Marketing Cloud] [API](https://developer.salesforce.com/docs/marketing/marketing-cloud/guide/apis-overview.html)
* [!DNL Salesforce Marketing Cloud] [文檔](https://developer.salesforce.com/docs/marketing/marketing-cloud/guide/updateContacts.html) 說明如何使用指定屬性組中的指定資訊更新聯繫人。

### 更改日誌 {#changelog}

本節將捕獲對此目標連接器進行的功能和重要文檔更新。

+++ 查看更改日誌

| 發放月 | 更新類型 | 說明 |
|---|---|---|
| 2023 年 4 月 | 文檔更新 | <ul><li>我們更正了 [(API)SalesforceMarketing Cloud中的先決條件](#prerequisites-destination) 區域， [!DNL Salesforce Marketing Cloud Engagement] 是使用此目標的必需訂閱。 此部分先前錯誤地指出用戶需要訂閱Marketing Cloud **帳戶** 接洽繼續。</li> <li>我們在 [先決條件](#prerequisites) 為 [角色和權限](#prerequisites-roles-permissions) 分配給 [!DNL Salesforce] 用戶。 (PLATIR-26299)</li></ul> |
| 2023 年 2 月 | 文檔更新 | 我們更新了 [(API)SalesforceMarketing Cloud中的先決條件](#prerequisites-destination) 包含引用連結調用的部分 [!DNL Salesforce Marketing Cloud Engagement] 是使用此目標的必需訂閱。 |
| 2023 年 2 月 | 功能更新 | 我們解決了目標中配置不正確導致格式錯誤的JSON被發送到Salesforce的問題。 這導致一些用戶在激活時看到大量身份失敗。 (PLATIR-26299) |
| 2023 年 1 月 | 文檔更新 | <ul><li>我們更新了 [中的先決條件 [!DNL Salesforce]](#prerequisites-destination) 調用需要在 [!DNL Salesforce] 邊。 本節現在包括有關如何執行此操作的詳細說明以及有關命名中屬性的最佳做法 [!DNL Salesforce]。 (PLATIR-25602)</li><li>我們為中的每個激活段添加了有關如何使用映射ID的明確說明 [段調度](#schedule-segment-export-example) 的子菜單。 (PLATIR-25602)</li></ul> |
| 2022 年 10 月 | 首次發行 | 初始目標版本和文檔發佈。 |

{style="table-layout:auto"}

+++
