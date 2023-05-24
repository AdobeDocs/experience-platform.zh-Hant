---
keywords: 流；HTTP目標
title: HTTP API連接
description: 使用Adobe Experience Platform的HTTP API目標將配置檔案資料發送到第三方HTTP終結點以運行您自己的分析或對導出出Experience Platform的配置檔案資料執行可能需要的任何其他操作。
exl-id: 165a8085-c8e6-4c9f-8033-f203522bb288
source-git-commit: 4d1f9fa19bd35095e3ccbd8d83bcc33dcd4c45a8
workflow-type: tm+mt
source-wordcount: '2431'
ht-degree: 8%

---

# HTTP API連接

## 總覽 {#overview}

>[!IMPORTANT]
>
> 此目標僅可用於 [Adobe Real-time Customer Data Platform旗艦](https://helpx.adobe.com/jp/legal/product-descriptions/real-time-customer-data-platform.html) 客戶。

HTTP API目標是 [!DNL Adobe Experience Platform] 流目標，幫助您將配置檔案資料發送到第三方HTTP終結點。

要向HTTP終結點發送配置檔案資料，必須首先 [連接到目標](#connect-destination) 在 [!DNL Adobe Experience Platform]。

## 使用案例 {#use-cases}

HTTP API目標允許您將XDM配置檔案資料和訪問群體段導出到通用HTTP終結點。 在此，您可以運行自己的分析，或對導出出Experience Platform的配置檔案資料執行可能需要的任何其他操作。

HTTP端點可以是客戶自己的系統或第三方解決方案。

## 導出類型和頻率 {#export-type-frequency}

有關目標導出類型和頻率的資訊，請參閱下表。

| 項目 | 類型 | 附註 |
---------|----------|---------|
| 導出類型 | **[!UICONTROL 基於配置檔案]** | 您正在導出段的所有成員以及所需的架構欄位(例如：電子郵件地址、電話號碼、姓氏)，如在 [目標激活工作流](../../ui/activate-segment-streaming-destinations.md#mapping)。 |
| 導出頻率 | **[!UICONTROL 流]** | 流目標是基於API的「始終開啟」連接。 一旦基於段評估在Experience Platform中更新配置檔案，連接器就將更新下游發送到目標平台。 閱讀有關 [流目標](/help/destinations/destination-types.md#streaming-destinations)。 |

{style="table-layout:auto"}

## 先決條件 {#prerequisites}

要使用HTTP API目標導出Experience Platform外的資料，必須滿足以下先決條件：

* 必須具有支援REST API的HTTP終結點。
* 您的HTTP終結點必須支援Experience Platform配置檔案架構。 HTTP API目標中不支援對第三方負載架構的轉換。 請參閱 [導出的資料](#exported-data) 的子節。
* HTTP終結點必須支援標頭。

>[!TIP]
>
> 您還可以使用 [Adobe Experience Platform Destination SDK](/help/destinations/destination-sdk/overview.md) 設定整合併將Experience Platform配置檔案資料發送到HTTP終結點。

## IP地址允許清單 {#ip-address-allowlist}

為滿足客戶的安全性和合規性要求，Experience Platform提供了一個靜態IP清單，您可以允許列出該HTTP API目標。 請參閱 [流目標的IP地址允許清單](/help/destinations/catalog/streaming/ip-address-allow-list.md) 清單。

## 支援的身份驗證類型 {#supported-authentication-types}

HTTP API目標支援對HTTP終結點的多種身份驗證類型：

* 無驗證的HTTP終結點；
* 持有者令牌認證；
* [OAuth 2.0客戶端憑據](https://www.oauth.com/oauth2-servers/access-tokens/client-credentials/) 驗證主體形式，使用 [!DNL client ID]。 [!DNL client secret] 和 [!DNL grant type] 在HTTP請求的正文中，如下例所示。

```shell
curl --location --request POST '<YOUR_API_ENDPOINT>' \
--header 'Content-Type: application/x-www-form-urlencoded' \
--data-urlencode 'grant_type=client_credentials' \
--data-urlencode 'client_id=<CLIENT_ID>' \
--data-urlencode 'client_secret=<CLIENT_SECRET>'
```

* [OAuth 2.0客戶端憑據](https://www.oauth.com/oauth2-servers/access-tokens/client-credentials/) 具有基本授權，具有包含URL編碼的授權標頭 [!DNL client ID] 和 [!DNL client secret]。

```shell
curl --location --request POST 'https://some-api.com/token' \
--header 'Authorization: Basic base64(clientId:clientSecret)' \
--header 'Content-type: application/x-www-form-urlencoded; charset=UTF-8' \
--data-urlencode 'grant_type=client_credentials'
```

* [OAuth 2.0密碼授予](https://www.oauth.com/oauth2-servers/access-tokens/password-grant/)。

## 連接到目標 {#connect-destination}

>[!IMPORTANT]
> 
>要連接到目標，您需要 **[!UICONTROL 管理目標]** [訪問控制權限](/help/access-control/home.md#permissions)。 閱讀 [訪問控制概述](/help/access-control/ui/overview.md) 或聯繫您的產品管理員以獲取所需權限。

要連接到此目標，請按照 [目標配置教程](../../ui/connect-destination.md)。 連接到此目標時，必須提供以下資訊：

### 驗證資訊 {#authentication-information}

>[!CONTEXTUALHELP]
>id="platform_destinations_connect_http_clientcredentialstype"
>title="用戶端憑證類型"
>abstract="選取&#x200B;**內文表單已編碼**，以在要求的內文中包含用戶端 ID 和用戶端密碼，或選取&#x200B;**基本授權**，以在要求的內文中包含用戶端 ID 和用戶端密碼。檢視文件中的範例。"

#### 持有者令牌驗證 {#bearer-token-authentication}

如果選擇 **[!UICONTROL 持有者令牌]** 連接到HTTP終結點的驗證類型，輸入下面的欄位並選擇 **[!UICONTROL 連接到目標]**:

![UI螢幕的影像，您可以在其中使用承載令牌驗證連接到HTTP API目標](../../assets/catalog/http/http-api-authentication-bearer.png)

* **[!UICONTROL 持有者令牌]**:插入承載令牌以驗證到HTTP位置。

#### 無身份驗證 {#no-authentication}

如果選擇 **[!UICONTROL 無]** 連接到HTTP終結點的身份驗證類型：

![UI螢幕的映像，您可以在此連接到HTTP API目標，但不使用身份驗證](../../assets/catalog/http/http-api-authentication-none.png)

當您選擇開啟此身份驗證時，您只需選擇 **[!UICONTROL 連接到目標]** 並且已建立與終結點的連接。

#### OAuth 2密碼驗證 {#oauth-2-password-authentication}

如果選擇 **[!UICONTROL OAuth 2密碼]** 連接到HTTP終結點的驗證類型，輸入下面的欄位並選擇 **[!UICONTROL 連接到目標]**:

![UI螢幕的影像，您可以在其中使用OAuth 2和密碼驗證連接到HTTP API目標](../../assets/catalog/http/http-api-authentication-oauth2-password.png)

* **[!UICONTROL 訪問令牌URL]**:發出訪問令牌（可選）和刷新令牌的URL。
* **[!UICONTROL 客戶端ID]**:的 [!DNL client ID] 你的系統給Adobe Experience Platform的。
* **[!UICONTROL 客戶端密碼]**:的 [!DNL client secret] 你的系統給Adobe Experience Platform的。
* **[!UICONTROL 用戶名]**:訪問HTTP終結點的用戶名。
* **[!UICONTROL 密碼]**:訪問HTTP終結點的密碼。

#### OAuth 2客戶端憑據身份驗證 {#oauth-2-client-credentials-authentication}

如果選擇 **[!UICONTROL OAuth 2客戶端憑據]** 連接到HTTP終結點的驗證類型，輸入下面的欄位並選擇 **[!UICONTROL 連接到目標]**:

![UI螢幕的影像，您可以在其中使用OAuth 2和客戶端憑據身份驗證連接到HTTP API目標](../../assets/catalog/http/http-api-authentication-oauth2-client-credentials.png)

* **[!UICONTROL 訪問令牌URL]**:發出訪問令牌（可選）和刷新令牌的URL。
* **[!UICONTROL 客戶端ID]**:的 [!DNL client ID] 你的系統給Adobe Experience Platform的。
* **[!UICONTROL 客戶端密碼]**:的 [!DNL client secret] 你的系統給Adobe Experience Platform的。
* **[!UICONTROL 客戶端憑據類型]**:選擇終結點支援的OAuth2客戶端憑據授予的類型：
   * **[!UICONTROL 體形編碼]**:在這個例子中， [!DNL client ID] 和 [!DNL client secret] 包括 *在請求正文中* 送到你的目的地。 有關示例，請參見 [支援的身份驗證類型](#supported-authentication-types) 的子菜單。
   * **[!UICONTROL 基本授權]**:在這個例子中， [!DNL client ID] 和 [!DNL client secret] 包括 *在 `Authorization` 標題* 將base64編碼併發送到目標。 有關示例，請參見 [支援的身份驗證類型](#supported-authentication-types) 的子菜單。

### 填寫目標詳細資訊 {#destination-details}

>[!CONTEXTUALHELP]
>id="platform_destinations_connect_http_headers"
>title="標頭"
>abstract="按照以下格式輸入您希望包含在目的地呼叫中的任何自訂標頭：`header1:value1,header2:value2,...headerN:valueN`"

>[!CONTEXTUALHELP]
>id="platform_destinations_connect_http_endpoint"
>title="HTTP 端點"
>abstract="要將設定檔資料傳送到的 HTTP 端點的 URL。"

>[!CONTEXTUALHELP]
>id="platform_destinations_connect_http_includesegmentnames"
>title="包括區段名稱"
>abstract="切換是否希望資料匯出包括您正在匯出的區段的名稱。檢視選取此選項時的資料匯出範例的文件。"

>[!CONTEXTUALHELP]
>id="platform_destinations_connect_http_includesegmenttimestamps"
>title="包括區段時間戳記"
>abstract="切換是否希望資料匯出包括建立和更新區段時的 Unix 時間戳記，以及區段對應至啟動目的地時的 Unix 時間戳記。檢視選取此選項時的資料匯出範例的文件。"

>[!CONTEXTUALHELP]
>id="platform_destinations_connect_http_queryparameters"
>title="查詢參數"
>abstract="或者，您可以將查詢參數新增到 HTTP 端點 URL。將您使用的查詢參數格式化，類似這樣：`parameter1=value&parameter2=value`。"

要配置目標的詳細資訊，請填寫以下必需欄位和可選欄位。 UI中某個欄位旁邊的星號表示該欄位是必需的。

![顯示HTTP目標詳細資訊的已完成欄位的UI螢幕影像](../../assets/catalog/http/http-api-destination-details.png)

* **[!UICONTROL 名稱]**:輸入將來用於識別此目標的名稱。
* **[!UICONTROL 說明]**:輸入將幫助您在將來確定此目標的說明。
* **[!UICONTROL 標題]**:按照以下格式輸入要包括在目標調用中的任何自定義標頭： `header1:value1,header2:value2,...headerN:valueN`。
* **[!UICONTROL HTTP終結點]**:要將配置檔案資料發送到的HTTP終結點的URL。
* **[!UICONTROL 查詢參數]**:也可以將查詢參數添加到HTTP終結點URL。 將您使用的查詢參數格式化，類似這樣：`parameter1=value&parameter2=value`。
* **[!UICONTROL 包括段名稱]**:如果希望資料導出包含要導出的段的名稱，則切換。 有關選擇此選項的資料導出示例，請參閱 [導出的資料](#exported-data) 的下一頁。
* **[!UICONTROL 包括段時間戳]**:如果希望資料導出包括建立和更新段時的UNIX時間戳，以及將段映射到要激活的目標時的UNIX時間戳，則切換。 有關選擇此選項的資料導出示例，請參閱 [導出的資料](#exported-data) 的下一頁。

### 啟用警報 {#enable-alerts}

您可以啟用警報來接收有關目標資料流狀態的通知。 從清單中選擇要訂閱的警報以接收有關資料流狀態的通知。 有關警報的詳細資訊，請參閱上的指南 [使用UI訂閱目標警報](../../ui/alerts.md)。

完成提供目標連接的詳細資訊後，選擇 **[!UICONTROL 下一個]**。

## 將段激活到此目標 {#activate}

>[!IMPORTANT]
> 
>要激活資料，您需要 **[!UICONTROL 管理目標]**。 **[!UICONTROL 激活目標]**。 **[!UICONTROL 查看配置檔案]**, **[!UICONTROL 查看段]** [訪問控制權限](/help/access-control/home.md#permissions)。 閱讀 [訪問控制概述](/help/access-control/ui/overview.md) 或聯繫您的產品管理員以獲取所需權限。

請參閱 [激活受眾資料以流式處理配置檔案導出目標](../../ui/activate-streaming-profile-destinations.md) 有關激活此目標受眾段的說明。

### 目標屬性 {#attributes}

在 [[!UICONTROL 選擇屬性]](../../ui/activate-streaming-profile-destinations.md#select-attributes) 步驟，Adobe建議您從 [聯合架構](../../../profile/home.md#profile-fragments-and-union-schemas)。 選擇要導出到目標的唯一標識符和任何其他XDM欄位。

## 配置檔案導出行為 {#profile-export-behavior}

Experience Platform可優化配置檔案導出行為到HTTP API目標，以便在經過段限定或其他重要事件之後對配置檔案進行相關更新時，才將資料導出到API終結點。 配置式在以下情況下導出到目標：

* 配置檔案更新由映射到目的地的至少一個段的段成員資格的改變確定。 例如，配置檔案已限定映射到目標的段之一或已退出映射到目標的段之一。
* 配置檔案更新由 [身份映射](/help/xdm/field-groups/profile/identitymap.md)。 例如，已為映射到目標的段之一限定的配置檔案已在標識映射屬性中添加了新標識。
* 配置檔案更新由映射到目的地的至少一個屬性的屬性的改變確定。 例如，映射步驟中映射到目標的屬性之一被添加到配置檔案。

在上述所有情況下，只將發生相關更新的配置檔案導出到目標。 例如，如果映射到目標流的段有100個成員，並且有5個新配置檔案符合該段的條件，則向目標的導出是增量的，並且只包括5個新配置檔案。

請注意，無論更改位於何處，都會為配置檔案導出所有映射的屬性。 因此，在上面的示例中，即使屬性本身沒有更改，也會導出這五個新配置檔案的所有映射屬性。

### 什麼決定資料導出以及導出中包含的內容 {#what-determines-export-what-is-included}

對於為給定配置檔案導出的資料，瞭解以下兩個不同概念非常重要 *決定資料導出到HTTP API目標的內容* 和 *資料包含在導出中*。

| 決定目標導出的因素 | 目標導出中包含的內容 |
|---------|----------|
| <ul><li>映射的屬性和段用作目標導出的提示。 這表示如果任何映射的段更改狀態(從 `null` 至 `realized` 或 `realized` 至 `exiting`)或更新任何映射屬性時，將啟動目標導出。</li><li>由於標識當前無法映射到HTTP API目標，因此給定配置檔案上任何標識的更改也會決定目標導出。</li><li>屬性的更改定義為屬性上的任何更新，無論其值是否相同。 這意味著，即使值本身未更改，屬性上的覆蓋也被視為更改。</li></ul> | <ul><li>的 `segmentMembership` 對象包括在激活資料流中映射的段，在限定或段退出事件後配置檔案的狀態已更改。 請注意，如果配置檔案限定用於的其他未映射段屬於相同的段，則這些段可以是目標導出的一部分 [合併策略](/help/profile/merge-policies/overview.md) 激活資料流中映射的段。 </li><li>中的所有標識 `identityMap` 對象也包括在內(Experience Platform當前不支援HTTP API目標中的標識映射)。</li><li>目標導出中只包含映射的屬性。</li></ul> |

{style="table-layout:fixed"}

例如，將此資料流視為HTTP目標，其中在資料流中選擇了三個段，並將四個屬性映射到目標。

![HTTP API目標資料流](/help/destinations/assets/catalog/http/profile-export-example-dataflow.png)

導出到目標的配置檔案可由符合或退出其中一個配置檔案來確定 *三個映射段*。 但是，在資料導出中，在 `segmentMembership` 對象（請參見） [導出的資料](#exported-data) )中，如果特定配置檔案是其成員，並且這些配置檔案與觸發導出的段共用相同的合併策略，則可能會出現其他未映射的段。 如果配置檔案符合 **DeLorean汽車的客戶** 部，但亦為 **觀看《回到未來》** 電影和 **科幻迷** 段，則這兩個段也將 `segmentMembership` 資料導出的對象，即使這些對象未在資料流中映射，如果它們與 **DeLorean汽車的客戶** 段。

從配置檔案屬性的視點來看，對上述四個屬性的任何更改都將確定目標導出，並且配置檔案上存在的四個映射屬性中的任何一個都將出現在資料導出中。

## 歷史資料回填 {#historical-data-backfill}

當您將新段添加到現有目標或建立新目標並將段映射到該目標時，Experience Platform會將歷史段限定資料導出到目標。 限定段的配置檔案 *先* 已添加到目標的段在大約一小時內導出到目標。

## 導出的資料 {#exported-data}

已導出 [!DNL Experience Platform] 資料到達 [!DNL HTTP] JSON格式的目標。 例如，下面的導出包含符合特定段條件的配置檔案，是另兩個段的成員，並退出另一個段。 導出還包括配置檔案屬性的名字、姓氏、出生日期和個人電子郵件地址。 此配置檔案的標識為ECID和電子郵件。

```json
{
  "person": {
    "birthDate": "YYYY-MM-DD",
    "name": {
      "firstName": "John",
      "lastName": "Doe"
    }
  },
  "personalEmail": {
    "address": "john.doe@acme.com"
  },
  "segmentMembership": {
   "ups":{
      "7841ba61-23c1-4bb3-a495-00d3g5fe1e93":{
         "lastQualificationTime":"2022-01-11T21:24:39Z",
         "status":"exited"
      },
      "59bd2fkd-3c48-4b18-bf56-4f5c5e6967ae":{
         "lastQualificationTime":"2022-01-02T23:37:33Z",
         "status":"realized"
      },
      "947c1c46-008d-40b0-92ec-3af86eaf41c1":{
         "lastQualificationTime":"2021-08-25T23:37:33Z",
         "status":"realized"
      },
      "5114d758-ce71-43ba-b53e-e2a91d67b67f":{
         "lastQualificationTime":"2022-01-11T23:37:33Z",
         "status":"realized"
      }
   }
},
  "identityMap": {
    "ecid": [
      {
        "id": "14575006536349286404619648085736425115"
      },
      {
        "id": "66478888669296734530114754794777368480"
      }
    ],
    "email_lc_sha256": [
      {
        "id": "655332b5fa2aea4498bf7a290cff017cb4"
      },
      {
        "id": "66baf76ef9de8b42df8903f00e0e3dc0b7"
      }
    ]
  }
}
```

下面是導出資料的進一步示例，具體取決於您在連接目標流中為 **[!UICONTROL 包括段名稱]** 和 **[!UICONTROL 包括段時間戳]** 選項：

+++ 以下資料導出示例包括 `segmentMembership` 節

```json
"segmentMembership": {
        "ups": {
          "5b998cb9-9488-4ec3-8d95-fa8338ced490": {
            "lastQualificationTime": "2019-04-15T02:41:50+0000",
            "status": "realized",
            "createdAt": 1648553325000,
            "updatedAt": 1648553330000,
            "mappingCreatedAt": 1649856570000,
            "mappingUpdatedAt": 1649856570000,
            "name": "First name equals John"
          }
        }
      }
```

+++

+++ 以下資料導出示例包括 `segmentMembership` 節

```json
"segmentMembership": {
        "ups": {
          "5b998cb9-9488-4ec3-8d95-fa8338ced490": {
            "lastQualificationTime": "2019-04-15T02:41:50+0000",
            "status": "realized",
            "createdAt": 1648553325000,
            "updatedAt": 1648553330000,
            "mappingCreatedAt": 1649856570000,
            "mappingUpdatedAt": 1649856570000,
          }
        }
      }
```

+++

## 限制和重試策略 {#limits-retry-policy}

在95%的時間內，Experience Platform會嘗試為成功發送的消息提供少於10分鐘的吞吐量延遲，每個資料流的請求速率低於每秒10,000次，到HTTP目標。

如果向HTTP API目標發出失敗請求，Experience Platform將儲存失敗的請求並重試兩次，以將請求發送到終結點。