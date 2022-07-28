---
keywords: crm;CRM;CRM目標；salesforce crm;salesforce crm目標
title: Salesforce CRM連接
description: Salesforce CRM目標允許您導出帳戶資料並在Salesforce CRM中根據您的業務需要將其激活。
source-git-commit: 154cca31c5b434a2f036773ef9cda088f84eb1e5
workflow-type: tm+mt
source-wordcount: '1730'
ht-degree: 2%

---


# [!DNL Salesforce CRM] 連接

## 總覽 {#overview}

[Salesforce CRM](https://www.salesforce.com/) 是一個流行的客戶關係管理(CRM)平台。

此 [!DNL Adobe Experience Platform] [目標](/help/destinations/home.md) 利用 [Salesforce REST API](https://developer.salesforce.com/docs/atlas.en-us.api_rest.meta/api_rest/dome_composite_upsert_example.htm?q=contacts)，允許您將段內的標識更新到Salesforce CRM。

Salesforce CRM使用帶密碼授權的OAuth 2作為驗證機制與Salesforce REST API通信。 下面是驗證到Salesforce CRM實例的說明，位於 [驗證到目標](#authenticate) 的子菜單。

## 使用案例 {#use-cases}

作為營銷人員，您可以根據用戶的Adobe Experience Platform配置檔案的屬性向用戶提供個性化體驗。 您可以從離線資料構建段，並將這些段發送到Salesforce CRM，以便在段和配置檔案在Adobe Experience Platform更新後立即顯示在用戶源中。

## 先決條件 {#prerequisites}

### Experience Platform中的先決條件 {#prerequisites-in-experience-platform}

在將資料激活到Salesforce CRM目標之前，必須有 [架構](/help/xdm/schema/composition.md)的 [資料集](https://experienceleague.adobe.com/docs/platform-learn/tutorials/data-ingestion/create-datasets-and-ingest-data.html?lang=en), [段](https://experienceleague.adobe.com/docs/platform-learn/tutorials/segments/create-segments.html?lang=en) 建立 [!DNL Experience Platform]。

### Salesforce CRM中的先決條件 {#prerequisites-destination}

請注意Salesforce中的以下先決條件，以便將資料從Platform導出到Salesforce帳戶：

#### 您需要有Salesforce帳戶 {#prerequisites-account}

轉到Salesforce [審判](https://www.salesforce.com/in/form/signup/freetrial-sales/) 頁，以註冊並建立Salesforce帳戶（如果尚未）。

#### 配置連接的應用 {#prerequisites-connected-app}

接下來，您需要配置 [連接的應用](https://help.salesforce.com/s/articleView?id=sf.connected_app_create.htm&amp;language=en_US&amp;r=https%3A%2F%2Fhelp.salesforce.com%2F&amp;type=5) 在Salesforce帳戶中，如果您還沒有。

在已連接的應用中，確保 [OAuth設定](https://help.salesforce.com/s/articleView?id=connected_app_create_api_integration.htm&amp;type=5&amp;language=en_US) 的子菜單。

同時確保 [作用域](https://help.salesforce.com/s/articleView?id=connected_app_create_api_integration.htm&amp;type=5&amp;language=en_US) 下面提到的。

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

#### 在Salesforce中建立自定義欄位 {#prerequisites-custom-field}

建立類型的自定義欄位 `Text Area Long` 該Experience Platform將用於更新Salesforce CRM中的段狀態。
請參閱Salesforce文檔，以 [建立自定義欄位](https://help.salesforce.com/s/articleView?id=sf.adding_fields.htm&amp;type=5) 如果你需要其他指導。

>[!IMPORTANT]
>
> 確保欄位名稱中沒有空格字元。 而是使用下划線 `(_)` 字元作為分隔符。

>[!NOTE]
>
> * Salesforce中的對象被限制為25個外部欄位，請參閱 [自定義欄位屬性](https://help.salesforce.com/s/articleView?id=sf.custom_field_attributes.htm&amp;type=5)。
> * 此限制意味著您在任何時候最多只能有25個Experience Platform段成員資格處於活動狀態。
> * 如果您在Salesforce內已達到此限制，則需要從Salesforce中刪除自定義屬性，該屬性用於將段狀態儲存在Experience Platform內較舊的段上，然後才能使用新的mappingId。


請參閱Adobe Experience Platform文檔，瞭解 [段成員身份詳細資訊架構欄位組](/help/xdm/field-groups/profile/segmentation.md) 如果需要有關段狀態的指導。

#### 收集Salesforce憑據 {#gather-credentials}

在驗證到Salesforce CRM目標之前，請記下以下項：

| 憑據 | 說明 | 範例 |
| --- | --- | --- |
| <ul><li>Salesforce域前置詞</li></ul> | 請參閱 [Salesforce域前置詞](https://help.salesforce.com/s/articleView?id=sf.domain_name_setting_login_policy.htm&amp;type=5) 的下界。 | <ul><li>如果域如下所示，則需要突出顯示的值。<br> <i>`d5i000000isb4eak-dev-ed`.my.salesforce.com</i></li></ul> |
| <ul><li>使用者密鑰</li><li>消費者秘密</li></ul> | 請參閱 [Salesforce文檔](https://help.salesforce.com/s/articleView?id=sf.connected_app_rotate_consumer_details.htm&amp;type=5) 如果你需要其他指導。 | <ul><li>r23kxxxxxxx0z05xxxxxx</li><li>ipxxxxxxxxxxT4xxxxxxxx</li></ul> |

## 支援的身份 {#supported-identities}

Salesforce CRM支援下表中描述的身份更新。 瞭解有關 [身份](/help/identity-service/namespaces.md)。

| 目標標識 | 說明 | 考量事項 |
|---|---|---|
| SalesforceId | 支援任何標識映射的自定義Salesforce CRM標識符。 | 必要. 您可以發送任何 [身份](../../../identity-service/namespaces.md) 到 [!DNL Salesforce CRM] 目標，只要你將其映射到 `SalesforceId`。 |

## 導出類型和頻率 {#export-type-frequency}

有關目標導出類型和頻率的資訊，請參閱下表。

| 項目 | 類型 | 附註 |
---------|----------|---------|
| 導出類型 | **[!UICONTROL 基於配置檔案]** | <ul><li>您正在導出段的所有成員以及所需的架構欄位 *(例如：電子郵件地址、電話號碼、姓氏)*，根據您的欄位映射。</li><li> 平台段狀態導出到 [!DNL Salesforce CRM] 通過指定其相應的自定義欄位屬性 [!DNL Salesforce CRM] 的 **[!UICONTROL 激活目標]** > **[!UICONTROL 計畫段導出]** > **[!UICONTROL 映射ID]** 的子菜單。</li></ul> |
| 導出頻率 | **[!UICONTROL 流]** | <ul><li>流目標是基於API的「始終開啟」連接。 一旦基於段評估在Experience Platform中更新配置檔案，連接器就將更新下游發送到目標平台。 閱讀有關 [流目標](/help/destinations/destination-types.md#streaming-destinations)。</li></ul> |

{style=&quot;table-layout:auto&quot;}

## 連接到目標 {#connect}

>[!IMPORTANT]
> 
>要連接到目標，您需要 **[!UICONTROL 管理目標]** [訪問控制權限](/help/access-control/home.md#permissions)。 閱讀 [訪問控制概述](/help/access-control/ui/overview.md) 或聯繫您的產品管理員以獲取所需權限。

要連接到此目標，請按照 [目標配置教程](../../ui/connect-destination.md)。 在配置目標工作流中，填寫下面兩節中列出的欄位。

![目錄](../../assets/catalog/crm/salesforce/catalog.png)

### 驗證到目標 {#authenticate}

要驗證到目標，請填寫必填欄位並選擇 **[!UICONTROL 連接到目標]**。

![示例螢幕截圖，顯示如何驗證到Salesforce CRM](../../assets/catalog/crm/salesforce/authenticate-destination.png)

* **[!UICONTROL 密碼]**:您的Salesforce帳戶密碼。
* **[!UICONTROL 客戶端ID]**:您的Salesforce連接的應用用戶密鑰。
* **[!UICONTROL 客戶端密碼]**:您的Salesforce已連接應用Consumer Secret。
* **[!UICONTROL 用戶名]**:您的Salesforce帳戶用戶名。

如果提供的詳細資訊有效，UI將顯示 **已連接** 狀態為綠色複選標籤，然後可以繼續執行下一步。

### 填寫目標詳細資訊 {#destination-details}

要配置目標的詳細資訊，請填寫以下必需欄位和可選欄位。 UI中某個欄位旁邊的星號表示該欄位是必需的。
![示例螢幕截圖，顯示如何填寫Salesforce CRM的詳細資訊](../../assets/catalog/crm/salesforce/destination-details.png)

* **[!UICONTROL 名稱]**:您將來識別此目標的名稱。
* **[!UICONTROL 說明]**:將幫助您在將來確定此目標的說明。
* **[!UICONTROL 自定義域]**:您的Salesforce域。

### 啟用警報 {#enable-alerts}

您可以啟用警報來接收有關目標資料流狀態的通知。 從清單中選擇要訂閱的警報以接收有關資料流狀態的通知。 有關警報的詳細資訊，請參閱上的指南 [使用UI訂閱目標警報](../../ui/alerts.md)。

完成提供目標連接的詳細資訊後，選擇 **[!UICONTROL 下一個]**。

## 將段激活到此目標 {#activate}

>[!IMPORTANT]
> 
>要激活資料，您需要 **[!UICONTROL 管理目標]**。 **[!UICONTROL 激活目標]**。 **[!UICONTROL 查看配置檔案]**, **[!UICONTROL 查看段]** [訪問控制權限](/help/access-control/home.md#permissions)。 閱讀 [訪問控制概述](/help/access-control/ui/overview.md) 或聯繫您的產品管理員以獲取所需權限。

閱讀 [激活配置檔案和段以流式處理段導出目標](/help/destinations/ui/activate-segment-streaming-destinations.md) 有關激活此目標受眾段的說明。

### 映射注意事項和示例 {#mapping-considerations-example}

要正確將受眾資料從Adobe Experience Platform發送到Salesforce CRM目標，您需要執行欄位映射步驟。 映射包括在您的平台帳戶中的「體驗資料模型」(XDM)架構欄位與目標目標中對應的欄位之間建立連結。 要正確將XDM欄位映射到Salesforce CRM目標欄位，請執行以下步驟：

1. 在映射步驟中，按一下 **[!UICONTROL 添加新映射]**，您將在螢幕上看到新的映射行。

   ![添加新映射](../../assets/catalog/crm/salesforce/add-new-mapping.png)

1. 在「選擇源欄位」窗口中，選擇源欄位時，選擇 **[!UICONTROL 選擇屬性]** 類別，並添加所需的映射。

   ![源映射](../../assets/catalog/crm/salesforce/source-mapping.png)

1. 在「選擇目標欄位」窗口中，選擇目標欄位，然後選擇 **[!UICONTROL 選擇標識命名空間]** 類別，並添加所需的映射。

   ![使用SalesforceId的目標映射](../../assets/catalog/crm/salesforce/target-mapping-salesforceid.png)

1. 對於自定義屬性，在「選擇目標欄位」窗口中，選擇目標欄位並選擇 **[!UICONTROL 選擇自定義屬性]** 類別，下一步提供所需的目標屬性名稱並添加所需的映射。

   ![使用LastName的目標映射](../../assets/catalog/crm/salesforce/target-mapping-lastname.png)

1. 例如，您可以在XDM配置檔案架構和 [!DNL Salesforce CRM] 實例：

   |  | XDM配置檔案架構 | [!DNL Salesforce CRM] 例項 | 必要 |
   |---|---|---|---|
   | 屬性 | <ul><li>person.name.firstName</code></li><li>person.name.lastName</code></li><li>personalEmail.address</code></li></ul> | <ul><li>名字</code></li><li>姓氏</code></li><li>電子郵件</code></li></ul> |
   | 身分 | <ul><li>crmID</code></li></ul> | <ul><li>SalesforceId</code></li></ul> | 是 |

1. 下面顯示了使用這些映射的示例：

   ![目標對應](../../assets/catalog/crm/salesforce/mappings.png)

### 計畫段導出和示例 {#schedule-segment-export-example}

執行 [計畫段導出](/help/destinations/ui/activate-segment-streaming-destinations.md#scheduling) 步驟必須手動將平台段映射到Salesforce中的自定義欄位屬性。

為此，請選擇每個段，然後從Salesforce中輸入相應的自定義欄位屬性 **[!UICONTROL 映射ID]** 的子菜單。

>[!IMPORTANT]
>
>* 用於 **[!UICONTROL 映射ID]** 應與在Salesforce中建立的自定義欄位屬性的名稱完全匹配。
>* 確保在Salesforce中建立的自定義欄位屬性的名稱不使用空格字元。


下面顯示了一個示例：
![計畫段導出](../../assets/catalog/crm/salesforce/schedule-segment-export.png)

## 驗證資料導出 {#exported-data}

要驗證您是否正確設定了目標，請執行以下步驟：

1. 選擇 **[!UICONTROL 目標]** > **[!UICONTROL 瀏覽]** 導航至目標清單。
   ![瀏覽目標](../../assets/catalog/crm/salesforce/browse-destinations.png)

1. 選擇目標並驗證狀態是否為 **[!UICONTROL 啟用]**。
   ![目標資料流運行](../../assets/catalog/crm/salesforce/destination-dataflow-run.png)

1. 切換到 **[!DNL Activation data]** ，然後選擇段名稱。
   ![目標激活資料](../../assets/catalog/crm/salesforce/destinations-activation-data.png)

1. 監視段摘要並確保配置檔案計數與段內建立的計數相對應。
   ![區段](../../assets/catalog/crm/salesforce/segment.png)

1. 登錄到Salesforce網站，然後導航到 **[!DNL Apps]** > **[!DNL Contacts]** 並檢查是否已添加該段中的配置檔案。
   ![Salesforce聯繫人](../../assets/catalog/crm/salesforce/contacts.png)

1. 按一下聯繫人並檢查欄位是否已更新。 您將注意到Experience Platform中的段狀態已根據中提供的相應自定義欄位屬性更新 **映射ID** 欄位 **[!UICONTROL 激活目標]** > **[!UICONTROL 計畫段導出]** 的子菜單。
   ![Salesforce聯繫人](../../assets/catalog/crm/salesforce/contact-info.png)

## 資料使用和治理 {#data-usage-governance}

全部 [!DNL Adobe Experience Platform] 目標在處理資料時符合資料使用策略。 有關如何 [!DNL Adobe Experience Platform] 強制實施資料治理，請參見 [資料治理概述](/help/data-governance/home.md)。

## 錯誤和故障排除 {#errors-and-troubleshooting}

### 將事件推送到目標時遇到未知錯誤 {#unknown-errors}

檢查資料流運行時，如果看到下面的錯誤消息，請驗證中提供的映射ID [!DNL Salesforce CRM] 您的平台段有效且存在於 [!DNL Salesforce CRM]。
![錯誤](../../assets/catalog/crm/salesforce/error.png)

## 其他資源 {#additional-resources}

來自 [Salesforce開發人員門戶](https://developer.salesforce.com/) 如下：
* [建立記錄](https://developer.salesforce.com/docs/atlas.en-us.api_rest.meta/api_rest/dome_sobject_create.htm)
* [自定義建議受眾](https://developer.salesforce.com/docs/atlas.en-us.236.0.chatterapi.meta/chatterapi/connect_resources_recommendation_audiences_list.htm)
* [使用複合資源](https://developer.salesforce.com/docs/atlas.en-us.api_rest.meta/api_rest/using_composite_resources.htm?q=composite)
* [快速入門](https://developer.salesforce.com/docs/atlas.en-us.api_rest.meta/api_rest/quickstart.htm)

### 限制 {#limits}

Salesforce通過施加請求、費率和超時限制來平衡事務負載。 請參閱 [API請求限制和分配](https://developer.salesforce.com/docs/atlas.en-us.salesforce_app_limits_cheatsheet.meta/salesforce_app_limits_cheatsheet/salesforce_app_limits_platform_api.htm) 的雙曲餘切值。