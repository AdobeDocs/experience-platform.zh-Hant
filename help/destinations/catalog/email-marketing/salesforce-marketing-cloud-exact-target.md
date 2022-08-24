---
keywords: 電子郵件；電子郵件；電子郵件；電子郵件目標；salesforce;api salesforce市場營銷雲目標
title: (API)SalesforceMarketing Cloud連接
description: SalesforceMarketing Cloud（以前稱為ExactTarget）目標允許您導出帳戶資料並在SalesforceMarketing Cloud中根據您的業務需要將其激活。
exl-id: 0cf068e6-8a0a-4292-a7ec-c40508846e27
source-git-commit: 2dda77c3d9a02b53a02128e835abf77ab97ad033
workflow-type: tm+mt
source-wordcount: '1906'
ht-degree: 2%

---

# [!DNL (API) Salesforce Marketing Cloud] 連接

## 總覽 {#overview}

[[!DNL Salesforce Marketing Cloud]](https://www.salesforce.com/products/marketing-cloud/overview/) （以前稱為ExactTarget）是一個數字營銷套件，允許您為訪問者和客戶構建和定制行程，以個性化其體驗。

>[!IMPORTANT]
> 
> 注意此連接與其他連接之間的差異 [SalesforceMarketing Cloud連接](https://experienceleague.adobe.com/docs/experience-platform/destinations/catalog/email-marketing/salesforce-marketing-cloud.html?lang=en) 在「電子郵件營銷目錄」部分中存在。 其他SalesforceMarketing Cloud連接允許您將檔案導出到指定的儲存位置，而這是基於API的流連接。

此 [!DNL Adobe Experience Platform] [目標](/help/destinations/home.md) 利用 [Salesforce更新聯繫人REST API](https://developer.salesforce.com/docs/marketing/marketing-cloud/guide/updateContacts.html)，它允許您在新Salesforce段中激活聯繫人/更新聯繫人資料以滿足您的業務需要。

SalesforceMarketing Cloud使用OAuth 2和客戶端憑據作為與Salesforce REST API通信的身份驗證機制。 下面是驗證到Salesforce實例的說明，位於 [驗證到目標](#authenticate) 的子菜單。

## 使用案例 {#use-cases}

為了幫助您更好地瞭解您應如何以及何時使用SalesforceMarketing Cloud目標，以下是Adobe Experience Platform客戶可以使用此目標解決的示例使用案例。

### 將電子郵件發送到營銷活動的聯繫人 {#use-case-send-emails}

一個房屋租賃平台的銷售部門希望向目標客戶廣播一封營銷電子郵件。 平台的營銷團隊可以添加新聯繫人/更新現有聯繫人 *（及其電子郵件地址）* 通過Adobe Experience Platform，從他們自己的離線資料中構建段，並將這些段發送到SalesforceMarketing Cloud，然後，Salesforce可用於發送營銷活動電子郵件。

## 先決條件 {#prerequisites}

### Experience Platform中的先決條件 {#prerequisites-in-experience-platform}

在將資料激活到SalesforceMarketing Cloud目標之前，您必須 [架構](/help/xdm/schema/composition.md)的 [資料集](https://experienceleague.adobe.com/docs/platform-learn/tutorials/data-ingestion/create-datasets-and-ingest-data.html?lang=en), [段](https://experienceleague.adobe.com/docs/platform-learn/tutorials/segments/create-segments.html?lang=en) 建立 [!DNL Experience Platform]。

### Salesforce CRM中的先決條件 {#prerequisites-destination}

請注意Salesforce中的以下先決條件，以便將資料從Platform導出到SalesforceMarketing Cloud帳戶：

#### 您需要有Salesforce帳戶 {#prerequisites-account}

轉到Salesforce [審判](https://www.salesforce.com/in/form/signup/freetrial-sales/) 頁，以註冊並建立Salesforce帳戶（如果尚未）。

#### 在Salesforce中建立自定義欄位 {#prerequisites-custom-field}

必須建立該類型的自定義屬性 `Text Area Long`，該Experience Platform將用於更新SalesforceMarketing Cloud中的段狀態。 在工作流中，將段激活到目標，在 **[段計畫](#schedule-segment-export-example)** 步驟，將使用自定義屬性作為激活的每個段的映射ID。

請參閱SalesforceMarketing Cloud文檔，以 [建立自定義欄位](https://help.salesforce.com/s/articleView?id=mc_cab_create_an_attribute.htm&amp;type=5&amp;language=en_US) 如果你需要其他指導。

>[!IMPORTANT]
>
> 確保在SalesforceMarketing Cloud帳戶中的「電子郵件統計資訊」屬性集下建立自定義屬性。

>[!NOTE]
>
> * 每個對象允許的自定義屬性數量因Salesforce Edition而異。 請參閱Salesforce文檔，瞭解 [每個對象允許的自定義欄位](https://help.salesforce.com/s/articleView?id=sf.custom_field_allocations.htm&amp;type=5) 如果你需要其他指導。
> * 如果您在Salesforce內已達到此限制，則需要從Salesforce中刪除自定義屬性，該屬性用於將段狀態儲存在Experience Platform內較舊的段上，然後才能使用新的mappingId。


請參閱Adobe Experience Platform文檔，瞭解 [段成員身份詳細資訊架構欄位組](/help/xdm/field-groups/profile/segmentation.md) 如果需要有關段狀態的指導。

#### 收集Salesforce憑據 {#gather-credentials}

在驗證到SalesforceMarketing Cloud目標之前，請記下以下項目。

| 憑據 | 說明 | 範例 |
| --- | --- | --- |
| <ul><li>SalesforceMarketing Cloud前置詞</li></ul> | 請參閱 [SalesforceMarketing Cloud域前置詞](https://help.salesforce.com/s/articleView?id=sf.domain_name_setting_login_policy.htm&amp;type=5) 的下界。 | <ul><li>如果域如下所示，則需要突出顯示的值。<br> <i>`mcq4jrssqdlyc4lph19nnqgzzs84`.login.exacttarget.com</i></li></ul> |
| <ul><li>客戶端ID</li><li>客戶端密碼</li></ul> | 請參閱 [Salesforce文檔](https://developer.salesforce.com/docs/marketing/marketing-cloud/guide/access-token-s2s.html) 如果你需要其他指導。 | <ul><li>r23kxxxxxxx0z05xxxxxx</li><li>ipxxxxxxxxxxT4xxxxxxxx</li></ul> |

{style=&quot;table-layout:auto&quot;}

## 支援的身份 {#supported-identities}

SalesforceMarketing Cloud支援激活下表中描述的身份。 瞭解有關 [身份](/help/identity-service/namespaces.md)。

| 目標標識 | 說明 | 考量事項 |
|---|---|---|
| 聯繫人密鑰 | Salesforce聯繫人密鑰。 請參閱 [Salesforce文檔](https://help.salesforce.com/s/articleView?id=sf.mc_cab_contact_builder_best_practices.htm&amp;type=5) 如果你需要其他指導。 | 必要 |

## 導出類型和頻率 {#export-type-frequency}

有關目標導出類型和頻率的資訊，請參閱下表。

| 項目 | 類型 | 附註 |
---------|----------|---------|
| 導出類型 | **[!UICONTROL 基於配置檔案]** | 您正在導出段的所有成員以及所需的架構欄位(例如：電子郵件地址、電話號碼、姓氏)，在「選擇配置檔案屬性」螢幕中選擇 [目標激活工作流](/help/destinations/ui/activate-batch-profile-destinations.md#select-attributes)。 |
| 導出頻率 | **[!UICONTROL 流]** | 流目標是基於API的「始終開啟」連接。 一旦基於段評估在Experience Platform中更新配置檔案，連接器就將更新下游發送到目標平台。 閱讀有關 [流目標](/help/destinations/destination-types.md#streaming-destinations)。 |

{style=&quot;table-layout:auto&quot;&quot;

## 連接到目標 {#connect}

>[!IMPORTANT]
> 
>要連接到目標，您需要 **[!UICONTROL 管理目標]** [訪問控制權限](/help/access-control/home.md#permissions)。 閱讀 [訪問控制概述](/help/access-control/ui/overview.md) 或聯繫您的產品管理員以獲取所需權限。

要連接到此目標，請按照 [目標配置教程](../../ui/connect-destination.md)。 在配置目標工作流中，填寫下面兩節中列出的欄位。

![目錄](../../assets/catalog/email-marketing/salesforce-marketing-cloud-exact-target/catalog.png)

### 驗證到目標 {#authenticate}

要驗證到目標，請填寫必填欄位並選擇 **[!UICONTROL 連接到目標]**。

![示例螢幕截圖，顯示如何驗證到SalesforceMarketing Cloud](../../assets/catalog/email-marketing/salesforce-marketing-cloud-exact-target/authenticate-destination.png)

* **[!UICONTROL 子域]**:您的SalesforceMarketing Cloud域前置詞。 例如，如果域 *`mcq4jrssqdlyc4lph19nnqgzzs84`.login.exacttarget.com*，需要加亮的值。
* **[!UICONTROL 客戶端ID]**:您的Salesforce客戶端ID。
* **[!UICONTROL 客戶端密碼]**:您的Salesforce客戶機密碼。

如果提供的詳細資訊有效，UI將顯示 **已連接** 狀態為綠色複選標籤，然後可以繼續執行下一步。

### 填寫目標詳細資訊 {#destination-details}

要配置目標的詳細資訊，請填寫以下必需欄位和可選欄位。 UI中某個欄位旁邊的星號表示該欄位是必需的。

![示例螢幕截圖，顯示如何填寫SalesforceMarketing Cloud的詳細資訊](../../assets/catalog/email-marketing/salesforce-marketing-cloud-exact-target/destination-details.png)

* **[!UICONTROL 名稱]**:您將來識別此目標的名稱。
* **[!UICONTROL 說明]**:將幫助您在將來確定此目標的說明。
* **[!UICONTROL 客戶名稱]**:這可以是任何值，但是值是必需的。 否則，目標激活將失敗。

### 啟用警報 {#enable-alerts}

您可以啟用警報來接收有關目標資料流狀態的通知。 從清單中選擇要訂閱的警報以接收有關資料流狀態的通知。 有關警報的詳細資訊，請參閱上的指南 [使用UI訂閱目標警報](../../ui/alerts.md)。

完成提供目標連接的詳細資訊後，選擇 **[!UICONTROL 下一個]**。

## 將段激活到此目標 {#activate}

>[!IMPORTANT]
> 
>要激活資料，您需要 **[!UICONTROL 管理目標]**。 **[!UICONTROL 激活目標]**。 **[!UICONTROL 查看配置檔案]**, **[!UICONTROL 查看段]** [訪問控制權限](/help/access-control/home.md#permissions)。 閱讀 [訪問控制概述](/help/access-control/ui/overview.md) 或聯繫您的產品管理員以獲取所需權限。

閱讀 [激活配置檔案和段以流式處理段導出目標](/help/destinations/ui/activate-segment-streaming-destinations.md) 有關激活此目標受眾段的說明。

### 映射注意事項和示例 {#mapping-considerations-example}

要正確將受眾資料從Adobe Experience Platform發送到SalesforceMarketing Cloud目標，您需要執行欄位映射步驟。 映射包括在您的平台帳戶中的「體驗資料模型」(XDM)架構欄位與目標目標中對應的欄位之間建立連結。 要正確將XDM欄位映射到SalesforceMarketing Cloud目標欄位，請執行以下步驟。

可為 [Salesforce REST API](https://developer.salesforce.com/docs/atlas.en-us.api_rest.meta/api_rest/dome_composite_upsert_example.htm?q=contacts) 的下方。 目標使用 [Salesforce搜索屬性集定義REST API](https://developer.salesforce.com/docs/marketing/marketing-cloud/guide/retrieveAttributeSetDefinitions.html) 檢索在Salesforce中為您的聯繫人定義且特定於您的帳戶的屬性。

>[!IMPORTANT]
> 
> 雖然您的屬性名稱與Salesforce帳戶相同，但是 `contactKey` 和 `personalEmail.address` 的子菜單。

1. 在映射步驟中，按一下 **[!UICONTROL 添加新映射]**。 現在，您可以在螢幕上看到新的映射行。
   ![添加新映射](../../assets/catalog/email-marketing/salesforce-marketing-cloud-exact-target/add-new-mapping.png)

1. 在「選擇源欄位」窗口中，選擇源欄位時，選擇 **[!UICONTROL 選擇屬性]** 類別，並添加所需的映射。
   ![源映射](../../assets/catalog/email-marketing/salesforce-marketing-cloud-exact-target/source-mapping.png)

1. 在「選擇目標欄位」窗口中，選擇目標欄位，然後選擇 **[!UICONTROL 選擇標識命名空間]** 類別，並添加所需的映射。
   ![目標對應](../../assets/catalog/email-marketing/salesforce-marketing-cloud-exact-target/target-mapping.png)

1. 要映射任何自定義屬性，請選擇目標欄位窗口，選擇目標欄位並選擇 **[!UICONTROL 選擇屬性]** > **電子郵件統計** 的子菜單。 接下來提供所需的目標屬性名稱並添加所需的映射。
   ![目標對應](../../assets/catalog/email-marketing/salesforce-marketing-cloud-exact-target/target-mapping-custom.png)

1. 例如，您可以在XDM配置檔案架構和 [!DNL Salesforce Marketing Cloud] 實例：

   |  | XDM配置檔案架構 | [!DNL Salesforce Marketing Cloud] 例項 | 必要 |
   |---|---|---|---|
   | 屬性 | <ul><li>person.name.firstName</code></li><li>personalEmail.address</code></li></ul> | <ul><li>電子郵件人口統計資訊。名</code></li><li>電子郵件地址。電子郵件地址</code></li></ul> | <ul><li>-</li><li>是</code></li></ul> |
   | 身分 | <ul><li>聯繫人密鑰</code></li></ul> | <ul><li>salesforceContactKey</code></li></ul> | 是 |

1. 下面顯示了使用這些映射的示例：
   ![目標映射LastName](../../assets/catalog/email-marketing/salesforce-marketing-cloud-exact-target/mappings.png)

### 計畫段導出和示例 {#schedule-segment-export-example}

執行 [計畫段導出](/help/destinations/ui/activate-segment-streaming-destinations.md#scheduling) 步驟，必須手動將平台段映射到Salesforce中的自定義屬性。

為此，請選擇每個段，然後從Salesforce中輸入相應的自定義屬性 **[!UICONTROL 映射ID]** 的子菜單。

>[!IMPORTANT]
>
> 用於映射ID的值應與Salesforce中「E-mail Stegomits」屬性集下建立的自定義屬性的名稱完全匹配。

下面顯示了一個示例：
![計畫段導出](../../assets/catalog/email-marketing/salesforce-marketing-cloud-exact-target/schedule-segment-export.png)

## 驗證資料導出 {#exported-data}

要驗證您是否正確設定了目標，請執行以下步驟：

1. 選擇 **[!UICONTROL 目標]** > **[!UICONTROL 瀏覽]** 導航至目標清單。

   ![瀏覽目標](../../assets/catalog/email-marketing/salesforce-marketing-cloud-exact-target/browse-destinations.png)

1. 選擇目標並驗證狀態是否為 **[!UICONTROL 啟用]**。

   ![目標資料流運行](../../assets/catalog/email-marketing/salesforce-marketing-cloud-exact-target/destination-dataflow-run.png)

1. 切換到 **[!DNL Activation data]** ，然後選擇段名稱。

   ![目標激活資料](../../assets/catalog/email-marketing/salesforce-marketing-cloud-exact-target/destinations-activation-data.png)

1. 監視段摘要並確保配置檔案計數與段內建立的計數相對應。

   ![區段](../../assets/catalog/email-marketing/salesforce-marketing-cloud-exact-target/segment.png)

1. 登錄到SalesforceMarketing Cloud網站。 然後導航到 **[!DNL Audience Builder]** > **[!DNL Contact Builder]** > **[!DNL All contacts]** > **[!DNL Email]** 並檢查是否已添加該段中的配置檔案。

   ![Salesforce聯繫人](../../assets/catalog/email-marketing/salesforce-marketing-cloud-exact-target/contacts.png)

1. 要檢查是否更新了任何配置檔案，請導航到 **[!DNL Email]** 頁檢查是否更新了段中配置檔案的屬性值。

   ![Salesforce聯繫人](../../assets/catalog/email-marketing/salesforce-marketing-cloud-exact-target/contact-detail.png)

## 資料使用和治理 {#data-usage-governance}

全部 [!DNL Adobe Experience Platform] 目標在處理資料時符合資料使用策略。 有關如何 [!DNL Adobe Experience Platform] 強制實施資料治理，請參見 [資料治理概述](/help/data-governance/home.md)。

## 錯誤和故障排除 {#errors-and-troubleshooting}

### 將事件推送到SalesforceMarketing Cloud時遇到未知錯誤 {#unknown-errors}

檢查資料流運行時，如果看到下面的錯誤消息，請驗證中提供的映射ID [!DNL Salesforce CRM] 您的平台段有效且存在於 [!DNL Salesforce CRM]。
![錯誤](../../assets/catalog/email-marketing/salesforce-marketing-cloud-exact-target/error.png)

## 其他資源 {#additional-resources}

* [Salesforce開發人員門戶](https://developer.salesforce.com/)

### 限制 {#limits}

* Salesforce強制 [速率限制](https://developer.salesforce.com/docs/marketing/marketing-cloud/guide/rate-limiting.html)。
* 請參閱 [速率限制錯誤](https://developer.salesforce.com/docs/marketing/marketing-cloud/guide/rate-limiting-errors.html) 頁，以檢查您可能遇到的任何錯誤。
* 請參閱 [SalesforceMarketing Cloud項目定價](https://www.salesforce.com/editions-pricing/marketing-cloud/email/) 頁 *下載完整版比較圖表* 作為pdf，詳細列出計畫施加的限制。
* 的 [API概述](https://developer.salesforce.com/docs/marketing/marketing-cloud/guide/apis-overview.html) 頁面詳細資訊附加限制。
* 整理這些詳細資訊的KB項目可用 [這裡](https://salesforce.stackexchange.com/questions/205898/marketing-cloud-api-limits#:~:text=Day%2FHour%2FMinute%20Limit&amp;text=We%20recommend%20a%20limit%20of,per%20minute%20for%20SOAP%20calls.&amp;text=As%20已%20已%20已添加%20英吋，正在與%20t%20REST%2DAPI交互%20)。
