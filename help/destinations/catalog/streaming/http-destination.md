---
keywords: 流；HTTP目的地
title: HTTP API連線
description: 使用Adobe Experience Platform中的HTTP API目的地，將設定檔資料傳送至協力廠商HTTP端點，以執行您自己的分析，或對匯出出Experience Platform的設定檔資料執行任何其他可能需要的作業。
exl-id: 165a8085-c8e6-4c9f-8033-f203522bb288
source-git-commit: 1c844d86834ef78d1206a8698dbcbfe2fae49661
workflow-type: tm+mt
source-wordcount: '2442'
ht-degree: 0%

---

# HTTP API連線

## 總覽 {#overview}

>[!IMPORTANT]
>
> 此目的地僅適用於 [Adobe Real-time Customer Data Platform Ultimate](https://helpx.adobe.com/legal/product-descriptions/real-time-customer-data-platform.html) 客戶。

HTTP API目的地為 [!DNL Adobe Experience Platform] 可協助您將設定檔資料傳送至協力廠商HTTP端點的串流目的地。

若要將設定檔資料傳送至HTTP端點，您必須先 [連接到目標](#connect-destination) in [!DNL Adobe Experience Platform].

## 使用案例 {#use-cases}

HTTP API目的地可讓您將XDM設定檔資料和對象區段匯出至一般HTTP端點。 在此，您可以執行自己的分析，或對匯出為Experience Platform外的設定檔資料執行任何其他可能需要的操作。

HTTP端點可以是客戶自己的系統或協力廠商解決方案。

## 匯出類型和頻率 {#export-type-frequency}

有關目標導出類型和頻率的資訊，請參閱下表。

| 項目 | 類型 | 附註 |
---------|----------|---------|
| 匯出類型 | **[!UICONTROL 設定檔]** | 您要匯出區段的所有成員，以及所需的結構欄位(例如：電子郵件地址、電話號碼、姓氏)，如 [目的地啟動工作流程](../../ui/activate-segment-streaming-destinations.md#mapping). |
| 匯出頻率 | **[!UICONTROL 串流]** | 串流目的地是「一律開啟」API型連線。 一旦根據區段評估在Experience Platform中更新設定檔，連接器就會將更新傳送至下游的目的地平台。 深入了解 [串流目的地](/help/destinations/destination-types.md#streaming-destinations). |

{style=&quot;table-layout:auto&quot;}

## 先決條件 {#prerequisites}

若要使用HTTP API目的地將資料匯出Experience Platform，您必須符合下列必要條件：

* 您必須有支援REST API的HTTP端點。
* 您的HTTP端點必須支援Experience Platform設定檔架構。 HTTP API目的地不支援轉換為第三方裝載結構。 請參閱 [匯出的資料](#exported-data) 區段，以取得Experience Platform輸出結構的範例。
* 您的HTTP端點必須支援標頭。

>[!TIP]
>
> 您也可以使用 [Adobe Experience Platform Destination SDK](/help/destinations/destination-sdk/overview.md) 設定整合，並將Experience Platform設定檔資料傳送至HTTP端點。

## IP位址允許清單 {#ip-address-allowlist}

為符合客戶的安全性和法規遵循需求，Experience Platform提供靜態IP清單，您可以將這些IP放入HTTP API目的地允許清單中。 請參閱 [串流目的地的IP位址允許清單](/help/destinations/catalog/streaming/ip-address-allow-list.md) 以取得允許清單的完整IP清單。

## 支援的驗證類型 {#supported-authentication-types}

HTTP API目的地支援數種驗證類型至HTTP端點：

* 沒有驗證的HTTP端點；
* 承載令牌驗證；
* [OAuth 2.0用戶端認證](https://www.oauth.com/oauth2-servers/access-tokens/client-credentials/) 使用body表單進行驗證，使用 [!DNL client ID], [!DNL client secret] 和 [!DNL grant type] ，如下列範例所示。

```shell
curl --location --request POST '<YOUR_API_ENDPOINT>' \
--header 'Content-Type: application/x-www-form-urlencoded' \
--data-urlencode 'grant_type=client_credentials' \
--data-urlencode 'client_id=<CLIENT_ID>' \
--data-urlencode 'client_secret=<CLIENT_SECRET>'
```

* [OAuth 2.0用戶端認證](https://www.oauth.com/oauth2-servers/access-tokens/client-credentials/) 具有基本授權，具有包含URL編碼的授權標題 [!DNL client ID] 和 [!DNL client secret].

```shell
curl --location --request POST 'https://some-api.com/token' \
--header 'Authorization: Basic base64(clientId:clientSecret)' \
--header 'Content-type: application/x-www-form-urlencoded; charset=UTF-8' \
--data-urlencode 'grant_type=client_credentials'
```

* [OAuth 2.0密碼授予](https://www.oauth.com/oauth2-servers/access-tokens/password-grant/).

## 連接到目標 {#connect-destination}

>[!IMPORTANT]
> 
>若要連線至目的地，您需要 **[!UICONTROL 管理目的地]** [存取控制權限](/help/access-control/home.md#permissions). 閱讀 [存取控制概觀](/help/access-control/ui/overview.md) 或聯絡您的產品管理員以取得所需的權限。

若要連線至此目的地，請依照 [目的地設定教學課程](../../ui/connect-destination.md). 連接到此目的地時，必須提供以下資訊：

### 驗證資訊 {#authentication-information}

>[!CONTEXTUALHELP]
>id="platform_destinations_connect_http_clientcredentialstype"
>title="客戶端憑據類型"
>abstract="選擇 **體型編碼** 在要求內文或 **基本授權** 將用戶端ID和用戶端密碼包含在授權標題中。 在檔案中檢視範例。"

#### 承載令牌驗證 {#bearer-token-authentication}

如果您選取 **[!UICONTROL 承載令牌]** 要連接到HTTP端點的驗證類型，請輸入以下欄位，然後選取 **[!UICONTROL 連接到目標]**:

![UI畫面的影像，您可在此使用承載權杖驗證連線至HTTP API目的地](../../assets/catalog/http/http-api-authentication-bearer.png)

* **[!UICONTROL 承載令牌]**:插入承載令牌以驗證到您的HTTP位置。

#### 無驗證 {#no-authentication}

如果您選取 **[!UICONTROL 無]** 連接到HTTP端點的身份驗證類型：

![UI畫面的影像，您可以在此連線至HTTP API目的地，不需驗證](../../assets/catalog/http/http-api-authentication-none.png)

當您選取此驗證開啟時，您只需要選取 **[!UICONTROL 連接到目標]** 並建立與端點的連線。

#### OAuth 2密碼驗證 {#oauth-2-password-authentication}

如果您選取 **[!UICONTROL OAuth 2密碼]** 要連接到HTTP端點的驗證類型，請輸入以下欄位，然後選取 **[!UICONTROL 連接到目標]**:

![使用OAuth 2搭配密碼驗證連線至HTTP API目的地的UI畫面影像](../../assets/catalog/http/http-api-authentication-oauth2-password.png)

* **[!UICONTROL 存取權杖URL]**:您發出存取權杖的URL，並選擇性地重新整理權杖。
* **[!UICONTROL 用戶端ID]**:此 [!DNL client ID] 由系統指派給Adobe Experience Platform。
* **[!UICONTROL 用戶端密碼]**:此 [!DNL client secret] 由系統指派給Adobe Experience Platform。
* **[!UICONTROL 使用者名稱]**:用於訪問HTTP端點的用戶名。
* **[!UICONTROL 密碼]**:訪問HTTP端點的密碼。

#### OAuth 2用戶端認證驗證 {#oauth-2-client-credentials-authentication}

如果您選取 **[!UICONTROL OAuth 2用戶端認證]** 要連接到HTTP端點的驗證類型，請輸入以下欄位，然後選取 **[!UICONTROL 連接到目標]**:

![使用OAuth 2搭配用戶端憑證驗證的UI畫面影像，您可在此連線至HTTP API目的地](../../assets/catalog/http/http-api-authentication-oauth2-client-credentials.png)

* **[!UICONTROL 存取權杖URL]**:您發出存取權杖的URL，並選擇性地重新整理權杖。
* **[!UICONTROL 用戶端ID]**:此 [!DNL client ID] 由系統指派給Adobe Experience Platform。
* **[!UICONTROL 用戶端密碼]**:此 [!DNL client secret] 由系統指派給Adobe Experience Platform。
* **[!UICONTROL 客戶端憑據類型]**:選取端點支援的OAuth2用戶端憑證授予類型：
   * **[!UICONTROL 體型編碼]**:在此情況下， [!DNL client ID] 和 [!DNL client secret] 包括 *在請求正文中* 傳送至您的目的地。 如需範例，請參閱 [支援的驗證類型](#supported-authentication-types) 區段。
   * **[!UICONTROL 基本授權]**:在此情況下， [!DNL client ID] 和 [!DNL client secret] 包括 *在 `Authorization` 標題* 編碼並傳送至目的地後。 如需範例，請參閱 [支援的驗證類型](#supported-authentication-types) 區段。

### 填寫目的地詳細資訊 {#destination-details}

>[!CONTEXTUALHELP]
>id="platform_destinations_connect_http_headers"
>title="標頭"
>abstract="依照以下格式，輸入您要納入目的地呼叫的任何自訂標題： `header1:value1,header2:value2,...headerN:valueN`"

>[!CONTEXTUALHELP]
>id="platform_destinations_connect_http_endpoint"
>title="HTTP端點"
>abstract="您要將設定檔資料傳送至的HTTP端點URL。"

>[!CONTEXTUALHELP]
>id="platform_destinations_connect_http_includesegmentnames"
>title="包含區段名稱"
>abstract="如果要讓資料匯出包含要匯出的區段名稱，請切換。 檢視已選取此選項之資料匯出範例的檔案。"

>[!CONTEXTUALHELP]
>id="platform_destinations_connect_http_includesegmenttimestamps"
>title="包含區段時間戳記"
>abstract="如果您希望資料匯出包含建立和更新區段時的UNIX時間戳記，以及將區段對應至要啟用的目的地時的UNIX時間戳記，則切換。 檢視已選取此選項之資料匯出範例的檔案。"

>[!CONTEXTUALHELP]
>id="platform_destinations_connect_http_queryparameters"
>title="查詢參數"
>abstract="您可以選擇將查詢參數新增至HTTP端點URL。 使用的查詢參數格式如下： `parameter1=value&parameter2=value`."

若要設定目的地的詳細資訊，請填寫下方的必填和選填欄位。 UI中欄位旁的星號表示該欄位為必要欄位。

![UI畫面的影像，顯示HTTP目的地詳細資訊的已完成欄位](../../assets/catalog/http/http-api-destination-details.png)

* **[!UICONTROL 名稱]**:輸入一個名稱，您將用該名稱來識別此目標。
* **[!UICONTROL 說明]**:輸入說明，以便您在未來識別此目的地。
* **[!UICONTROL 標題]**:依照以下格式，輸入您要納入目的地呼叫的任何自訂標題： `header1:value1,header2:value2,...headerN:valueN`.
* **[!UICONTROL HTTP端點]**:您要將設定檔資料傳送至的HTTP端點URL。
* **[!UICONTROL 查詢參數]**:您可以選擇將查詢參數新增至HTTP端點URL。 使用的查詢參數格式如下： `parameter1=value&parameter2=value`.
* **[!UICONTROL 包含區段名稱]**:如果要讓資料匯出包含要匯出的區段名稱，請切換。 如需選取此選項的資料匯出範例，請參閱 [匯出的資料](#exported-data) 下文一節。
* **[!UICONTROL 包含區段時間戳記]**:如果您希望資料匯出包含建立和更新區段時的UNIX時間戳記，以及將區段對應至要啟用的目的地時的UNIX時間戳記，則切換。 如需選取此選項的資料匯出範例，請參閱 [匯出的資料](#exported-data) 下文一節。

### 啟用警報 {#enable-alerts}

您可以啟用警報，接收有關資料流到目標狀態的通知。 從清單中選擇要訂閱的警報，以接收有關資料流狀態的通知。 如需警報的詳細資訊，請參閱 [使用UI訂閱目的地警報](../../ui/alerts.md).

完成提供目標連接的詳細資訊後，請選擇 **[!UICONTROL 下一個]**.

## 啟用此目的地的區段 {#activate}

>[!IMPORTANT]
> 
>若要啟用資料，您需要 **[!UICONTROL 管理目的地]**, **[!UICONTROL 啟動目的地]**, **[!UICONTROL 檢視設定檔]**，和 **[!UICONTROL 檢視區段]** [存取控制權限](/help/access-control/home.md#permissions). 閱讀 [存取控制概觀](/help/access-control/ui/overview.md) 或聯絡您的產品管理員以取得所需的權限。

請參閱 [對串流設定檔匯出目的地啟用受眾資料](../../ui/activate-streaming-profile-destinations.md) 以取得啟用受眾區段至此目的地的指示。

### 目標屬性 {#attributes}

在 [[!UICONTROL 選擇屬性]](../../ui/activate-streaming-profile-destinations.md#select-attributes) 步驟，Adobe建議您從 [聯合方案](../../../profile/home.md#profile-fragments-and-union-schemas). 選取唯一識別碼，以及您要匯出至目的地的任何其他XDM欄位。

## 設定檔匯出行為 {#profile-export-behavior}

Experience Platform會最佳化將設定檔匯出行為匯出至您的HTTP API目的地，以僅在符合區段資格或其他重大事件後發生設定檔的相關更新時，將資料匯出至API端點。 設定檔會在下列情況下匯出至您的目的地：

* 設定檔更新是由對應至目的地的至少一個區段的區段成員資格變更所決定。 例如，設定檔已符合對應至目的地的其中一個區段資格，或已退出對應至目的地的其中一個區段。
* 設定檔更新是由 [身分圖](/help/xdm/field-groups/profile/identitymap.md). 例如，已符合其中一個對應至目的地區段資格的設定檔，已在「身分對應」屬性中新增身分識別。
* 配置檔案更新由至少一個映射到目標的屬性的屬性的屬性變化確定。 例如，對應步驟中對應至目的地的其中一個屬性會新增至設定檔。

在上述所有情況中，只有發生相關更新的設定檔會匯出至您的目的地。 例如，如果對應至目的地流程的區段有100個成員，且有5個新設定檔符合該區段的資格，則匯出至目的地的作業會是增量的，且僅包含5個新設定檔。

請注意，無論變更在何處，所有對應屬性都會針對設定檔匯出。 因此，在上述範例中，即使屬性本身未變更，這五個新設定檔的所有對應屬性也會匯出。

### 決定資料匯出的項目，以及匯出中包含的項目 {#what-determines-export-what-is-included}

對於針對指定設定檔匯出的資料，請務必了解 *決定要匯出至HTTP API目的地的資料的因素* 和 *匯出中包含的資料*.

| 決定目標匯出的因素 | 目的地匯出包含的項目 |
|---------|----------|
| <ul><li>對應的屬性和區段可作為目的地匯出的提示。 這表示，如果任何映射的段更改狀態（從null更改為已實現或從已實現/現有更新為正在退出）或任何映射的屬性被更新，則將啟動目標導出。</li><li>由於身分目前無法對應至HTTP API目的地，因此指定設定檔上任何身分的變更也會決定目的地匯出。</li><li>屬性的更改定義為對屬性的任何更新，無論其是否為相同值。 這表示即使值本身未變更，屬性的覆寫仍視為變更。</li></ul> | <ul><li>此 `segmentMembership` 對象包括在激活資料流中映射的段，在資格鑑定或段退出事件後，配置檔案的狀態已更改。 請注意，如果設定檔符合資格的其他未對應區段屬於相同區段，則這些區段可能是目的地匯出的一部分 [合併策略](/help/profile/merge-policies/overview.md) 作為激活資料流中映射的段。 </li><li>中的所有身分 `identityMap` 也包含物件(Experience Platform目前不支援HTTP API目的地中的身分對應)。</li><li>目標匯出中僅包含對應的屬性。</li></ul> |

{style=&quot;table-layout:fixed&quot;}

例如，將此資料流視為HTTP目標，其中資料流中選擇了三個段，四個屬性映射到目標。

![HTTP API目標資料流](/help/destinations/assets/catalog/http/profile-export-example-dataflow.png)

匯出至目的地的設定檔可由符合以下條件之一或退出該條件的設定檔來決定 *三個已對應區段*. 不過，在資料匯出中， `segmentMembership` 物件(請參閱 [匯出的資料](#exported-data) )，則可能會顯示其他未映射的區段，如果該特定設定檔是其成員，且這些區段與觸發匯出的區段共用相同的合併原則。 如果設定檔符合 **DeLorean汽車的客戶** 區段，但亦為 **觀看「回到未來」** 電影和 **科幻迷** 區段，則另外兩個區段也會出現在 `segmentMembership` 資料導出的對象，即使這些對象未映射到資料流中，如果這些對象與共用相同的合併策略 **DeLorean汽車的客戶** 區段。

從設定檔屬性的觀點來看，對上述四個屬性所做的任何變更將決定目的地匯出，而設定檔上呈現的四個對應屬性中的任何一個將出現在資料匯出中。

## 歷史資料回填 {#historical-data-backfill}

將新區段新增至現有目的地，或建立新目的地並將區段對應至該目的地時，Experience Platform會將歷史區段資格資料匯出至目的地。 符合區段資格的設定檔 *befor* 區段已新增至目的地後，大約一小時內就會匯出至目的地。

## 匯出的資料 {#exported-data}

已導出 [!DNL Experience Platform] 資料登陸 [!DNL HTTP] 目的地。 例如，以下匯出包含符合特定區段資格的設定檔、是其他兩個區段的成員，並退出另一個區段。 匯出內容也包含設定檔屬性名、姓氏、出生日期和個人電子郵件地址。 此設定檔的身分為ECID和電子郵件。

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
         "status":"existing"
      },
      "947c1c46-008d-40b0-92ec-3af86eaf41c1":{
         "lastQualificationTime":"2021-08-25T23:37:33Z",
         "status":"existing"
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

以下是匯出資料的進一步範例，具體取決於您在連線目的地流程中為 **[!UICONTROL 包含區段名稱]** 和 **[!UICONTROL 包含區段時間戳記]** 選項：

+++ 以下資料匯出範例包含 `segmentMembership` 節

```json
"segmentMembership": {
        "ups": {
          "5b998cb9-9488-4ec3-8d95-fa8338ced490": {
            "lastQualificationTime": "2019-04-15T02:41:50+0000",
            "status": "existing",
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

+++ 以下資料匯出範例包含 `segmentMembership` 節

```json
"segmentMembership": {
        "ups": {
          "5b998cb9-9488-4ec3-8d95-fa8338ced490": {
            "lastQualificationTime": "2019-04-15T02:41:50+0000",
            "status": "existing",
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

在95%的時間內，Experience Platform會嘗試為成功發送的消息提供少於10分鐘的吞吐量延遲，每個資料流每秒的請求速率小於10,000個，以到達HTTP目的地。

如果對您的HTTP API目的地提出失敗請求，Experience Platform會儲存失敗的請求並重試兩次，以將請求傳送至端點。