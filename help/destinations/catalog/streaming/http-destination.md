---
keywords: 串流； HTTP目的地
title: HTTP API連線
description: 在Adobe Experience Platform中使用HTTP API目的地，將設定檔資料傳送至第三方HTTP端點，以執行您自己的分析，或針對從Experience Platform匯出的設定檔資料執行您可能需要的任何其他操作。
badgeUltimate: label="Ultimate" type="Positive"
exl-id: 165a8085-c8e6-4c9f-8033-f203522bb288
source-git-commit: d78b7a06318dabff5dac763068ca7c21a5a86633
workflow-type: tm+mt
source-wordcount: '2692'
ht-degree: 8%

---

# HTTP API連線

## 概觀 {#overview}

>[!IMPORTANT]
>
> 此目的地僅供[Adobe Real-Time Customer Data Platform Ultimate](https://helpx.adobe.com/jp/legal/product-descriptions/real-time-customer-data-platform.html)客戶使用。

HTTP API目的地是[!DNL Adobe Experience Platform]串流目的地，可協助您將設定檔資料傳送至第三方HTTP端點。

若要將設定檔資料傳送至HTTP端點，您必須先在[!DNL Adobe Experience Platform]中[連線至目的地](#connect-destination)。

## 使用案例 {#use-cases}

HTTP API目的地可讓您將XDM設定檔資料和對象匯出至一般HTTP端點。 在那裡，您可以對從Experience Platform匯出的設定檔資料執行自己的分析或執行任何其他您可能需要的操作。

HTTP端點可以是客戶自己的系統或協力廠商解決方案。

## 支援的對象 {#supported-audiences}

本節說明您可以將哪些型別的對象匯出至此目的地。

| 對象來源 | 支援 | 說明 |
|---------|----------|----------|
| [!DNL Segmentation Service] | ✓ | 透過Experience Platform [細分服務](../../../segmentation/home.md)產生的對象。 |
| 自訂上傳 | ✓ | 對象[從CSV檔案匯入](../../../segmentation/ui/audience-portal.md#import-audience)至Experience Platform。 |

{style="table-layout:auto"}

## 匯出型別和頻率 {#export-type-frequency}

請參閱下表以取得目的地匯出型別和頻率的資訊。

| 項目 | 類型 | 附註 |
---------|----------|---------|
| 匯出類型 | **[!UICONTROL 以設定檔為基礎]** | 您正在匯出區段的所有成員，以及所需的結構描述欄位（例如：電子郵件地址、電話號碼、姓氏），如[目的地啟用工作流程](../../ui/activate-segment-streaming-destinations.md#mapping)的對應畫面中所選。 |
| 匯出頻率 | **[!UICONTROL 串流]** | 串流目的地是「一律開啟」的API型連線。 根據對象評估在Experience Platform中更新設定檔後，聯結器會立即將更新傳送至下游的目標平台。 深入瞭解[串流目的地](/help/destinations/destination-types.md#streaming-destinations)。 |

{style="table-layout:auto"}

## 先決條件 {#prerequisites}

若要使用HTTP API目的地將資料匯出Experience Platform，您必須符合下列先決條件：

* 您必須有支援REST API的HTTP端點。
* 您的HTTP端點必須支援Experience Platform設定檔結構描述。 HTTP API目的地不支援轉換至第三方裝載結構描述。 如需Experience Platform輸出結構描述的範例，請參閱[匯出的資料](#exported-data)區段。
* 您的HTTP端點必須支援標頭。

>[!TIP]
>
> 您也可以使用[Adobe Experience Platform Destination SDK](/help/destinations/destination-sdk/overview.md)來設定整合，並將Experience Platform設定檔資料傳送至HTTP端點。

## mTLS通訊協定支援和憑證 {#mtls-protocol-support}

您可以使用[!DNL Mutual Transport Layer Security] ([!DNL mTLS])來確保與您的HTTP API目的地連線的輸出連線中的增強安全性。

[!DNL mTLS]是相互驗證的端對端安全性方法，可確保共用資訊的雙方在共用資料之前，都是聲稱的身分。 與[!DNL TLS]相比，[!DNL mTLS]包含額外的步驟，其中伺服器也會要求使用者端的憑證，並在其結尾加以驗證。

如果您想要搭配[!DNL HTTP API]個目的地使用[!DNL mTLS]，您放入[目的地詳細資料](#destination-details)頁面的伺服器位址必須停用[!DNL TLS]通訊協定，而且只能啟用[!DNL mTLS]。 如果端點上仍啟用[!DNL TLS] 1.2通訊協定，則不會傳送使用者端驗證的憑證。 這表示若要搭配您的[!DNL HTTP API]目的地使用[!DNL mTLS]，您的「接收」伺服器端點必須是僅限[!DNL mTLS]啟用的連線端點。

### 擷取及檢查憑證詳細資料 {#certificate}

如果您要檢查[!DNL Common Name] (CN)和[!DNL Subject Alternative Names] (SAN)等憑證詳細資料以進行其他協力廠商驗證，請使用API來擷取憑證，並從回應中擷取這些欄位。

如需詳細資訊，請參閱[公用憑證端點檔案](../../../data-governance/mtls-api/public-certificate-endpoint.md)。

## IP位址允許清單 {#ip-address-allowlist}

為了滿足客戶的安全性和合規性要求，Experience Platform提供您可以允許列出HTTP API目的地的靜態IP清單。 如需允許清單的完整IP清單，請參閱串流目的地的[IP位址允許清單](/help/destinations/catalog/streaming/ip-address-allow-list.md)。

## 支援的驗證型別 {#supported-authentication-types}

HTTP API目的地支援多種對HTTP端點的驗證型別：

* 沒有驗證的HTTP端點；
* 持有人權杖驗證；
* [OAuth 2.0使用者端認證](https://www.oauth.com/oauth2-servers/access-tokens/client-credentials/)驗證內文表單，在HTTP要求內文中有[!DNL client ID]、[!DNL client secret]和[!DNL grant type]，如下列範例所示。

```shell
curl --location --request POST '<YOUR_API_ENDPOINT>' \
--header 'Content-Type: application/x-www-form-urlencoded' \
--data-urlencode 'grant_type=client_credentials' \
--data-urlencode 'client_id=<CLIENT_ID>' \
--data-urlencode 'client_secret=<CLIENT_SECRET>'
```

* [OAuth 2.0使用者端認證](https://www.oauth.com/oauth2-servers/access-tokens/client-credentials/)具有基本授權，授權標頭包含URL編碼的[!DNL client ID]和[!DNL client secret]。

```shell
curl --location --request POST 'https://some-api.com/token' \
--header 'Authorization: Basic base64(clientId:clientSecret)' \
--header 'Content-type: application/x-www-form-urlencoded; charset=UTF-8' \
--data-urlencode 'grant_type=client_credentials'
```

* [OAuth 2.0密碼授予](https://www.oauth.com/oauth2-servers/access-tokens/password-grant/)。

## 連線到目標 {#connect-destination}

>[!IMPORTANT]
> 
>若要連線到目的地，您需要&#x200B;**[!UICONTROL 檢視目的地]**&#x200B;和&#x200B;**[!UICONTROL 管理目的地]** [存取控制許可權](/help/access-control/home.md#permissions)。 閱讀[存取控制總覽](/help/access-control/ui/overview.md)或連絡您的產品管理員以取得必要的許可權。

若要連線到此目的地，請依照[目的地組態教學課程](../../ui/connect-destination.md)中所述的步驟進行。 連線到這個目的地時，您必須提供下列資訊：

### 驗證資訊 {#authentication-information}

>[!CONTEXTUALHELP]
>id="platform_destinations_connect_http_clientcredentialstype"
>title="用戶端憑證類型"
>abstract="選取&#x200B;**內文表單已編碼**，以在要求的內文中包含用戶端 ID 和用戶端密碼，或選取&#x200B;**基本授權**，以在要求的內文中包含用戶端 ID 和用戶端密碼。檢視文件中的範例。"

#### 持有人權杖驗證 {#bearer-token-authentication}

如果您選取&#x200B;**[!UICONTROL 持有人權杖]**&#x200B;驗證型別以連線至您的HTTP端點，請輸入下列欄位並選取&#x200B;**[!UICONTROL 連線至目的地]**：

![UI熒幕的影像，您可在此使用持有人權杖驗證連線至HTTP API目的地。](../../assets/catalog/http/http-api-authentication-bearer.png)

* **[!UICONTROL 持有人權杖]**：插入持有人權杖以驗證您的HTTP位置。

#### 無驗證 {#no-authentication}

如果您選取&#x200B;**[!UICONTROL 無]**&#x200B;驗證型別以連線至您的HTTP端點：

![UI熒幕的影像，您可在其中使用無驗證連線至HTTP API目的地。](../../assets/catalog/http/http-api-authentication-none.png)

當您選取這個驗證開啟時，您只需要選取&#x200B;**[!UICONTROL 連線到目的地]**，而且與端點的連線已經建立。

#### OAuth 2密碼驗證 {#oauth-2-password-authentication}

如果您選取&#x200B;**[!UICONTROL OAuth 2密碼]**&#x200B;驗證型別以連線至您的HTTP端點，請輸入下列欄位並選取&#x200B;**[!UICONTROL 連線至目的地]**：

![UI熒幕的影像，您可在此使用OAuth 2搭配密碼驗證連線至HTTP API目的地。](../../assets/catalog/http/http-api-authentication-oauth2-password.png)

* **[!UICONTROL 存取權杖URL]**：您那邊發行存取權杖的URL，並可選擇重新整理權杖。
* **[!UICONTROL 使用者端識別碼]**：您的系統指派給Adobe Experience Platform的[!DNL client ID]。
* **[!UICONTROL 使用者端密碼]**：您的系統指派給Adobe Experience Platform的[!DNL client secret]。
* **[!UICONTROL 使用者名稱]**：存取您HTTP端點的使用者名稱。
* **[!UICONTROL 密碼]**：存取您HTTP端點的密碼。

#### OAuth 2使用者端憑證驗證 {#oauth-2-client-credentials-authentication}

如果您選取&#x200B;**[!UICONTROL OAuth 2使用者端認證]**&#x200B;驗證型別以連線至您的HTTP端點，請輸入下列欄位並選取&#x200B;**[!UICONTROL 連線至目的地]**：

![UI熒幕的影像，您可在此使用OAuth 2搭配使用者端憑證驗證連線至HTTP API目的地。](../../assets/catalog/http/http-api-authentication-oauth2-client-credentials.png)

>[!WARNING]
> 
>使用[!UICONTROL OAuth 2使用者端認證]驗證時，[!UICONTROL 存取權杖URL]最多可以有一個查詢引數。 新增包含更多查詢引數的[!UICONTROL 存取權杖URL]可能會導致連線到端點時發生問題。

* **[!UICONTROL 存取權杖URL]**：您那邊發行存取權杖的URL，並可選擇重新整理權杖。
* **[!UICONTROL 使用者端識別碼]**：您的系統指派給Adobe Experience Platform的[!DNL client ID]。
* **[!UICONTROL 使用者端密碼]**：您的系統指派給Adobe Experience Platform的[!DNL client secret]。
* **[!UICONTROL 使用者端認證型別]**：選取端點支援的OAuth2使用者端認證授權型別：
   * **[!UICONTROL 已編碼的內文表單]**：在此案例中，[!DNL client ID]和[!DNL client secret]包含在傳送至您目的地的要求&#x200B;*內文中*。 如需範例，請參閱[支援的驗證型別](#supported-authentication-types)區段。
   * **[!UICONTROL 基本授權]**：在此情況下，[!DNL client ID]和[!DNL client secret]在經過base64編碼並傳送至您的目的地之後，會包含在`Authorization`標頭&#x200B;*中的*。 如需範例，請參閱[支援的驗證型別](#supported-authentication-types)區段。

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
>abstract="切換是否希望資料匯出包括您正在匯出的對象的名稱。檢視選取此選項時的資料匯出範例的文件。"

>[!CONTEXTUALHELP]
>id="platform_destinations_connect_http_includesegmenttimestamps"
>title="包括區段時間戳記"
>abstract="切換是否希望資料匯出包括建立和更新對象時的 UNIX 時間戳記，以及對象對應至啟動目的地時的 UNIX 時間戳記。檢視選取此選項時的資料匯出範例的文件。"

>[!CONTEXTUALHELP]
>id="platform_destinations_connect_http_queryparameters"
>title="查詢參數"
>abstract="或者，您可以將查詢參數新增到 HTTP 端點 URL。將您使用的查詢參數格式化，類似這樣：`parameter1=value&parameter2=value`。"

若要設定目的地的詳細資訊，請填寫下方的必填和選用欄位。 UI中欄位旁的星號表示該欄位為必填欄位。

![顯示HTTP目的地詳細資訊已完成欄位的UI畫面影像。](../../assets/catalog/http/http-api-destination-details.png)

* **[!UICONTROL 名稱]**：輸入您日後可辨識此目的地的名稱。
* **[!UICONTROL 描述]**：輸入有助於您日後識別此目的地的描述。
* **[!UICONTROL 標頭]**：依照以下格式，輸入任何要包含在目的地呼叫中的自訂標頭： `header1:value1,header2:value2,...headerN:valueN`。
* **[!UICONTROL HTTP端點]**：您要傳送設定檔資料的HTTP端點的URL。
* **[!UICONTROL 查詢引數]**：您可以選擇將查詢引數新增至HTTP端點URL。 將您使用的查詢參數格式化，類似這樣：`parameter1=value&parameter2=value`。
* **[!UICONTROL 包含區段名稱]**：如果要讓資料匯出包含您匯出的對象名稱，請切換選項。 如需選取此選項的資料匯出範例，請參閱下方的[匯出的資料](#exported-data)區段。
* **[!UICONTROL 包含區段時間戳記]**：若要讓資料匯出包含建立和更新對象時的UNIX時間戳記，以及對象對應至啟用目的地時的UNIX時間戳記，請切換此專案。 如需選取此選項的資料匯出範例，請參閱下方的[匯出的資料](#exported-data)區段。

### 啟用警示 {#enable-alerts}

您可以啟用警報以接收有關傳送到您目的地的資料流狀態的通知。 從清單中選取警報以訂閱接收有關資料流狀態的通知。 如需警示的詳細資訊，請參閱[使用UI訂閱目的地警示](../../ui/alerts.md)的指南。

當您完成提供目的地連線的詳細資訊後，請選取&#x200B;**[!UICONTROL 下一步]**。

## 啟動此目標的對象 {#activate}

>[!IMPORTANT]
> 
>* 若要啟用資料，您需要&#x200B;**[!UICONTROL 檢視目的地]**、**[!UICONTROL 啟用目的地]**、**[!UICONTROL 檢視設定檔]**&#x200B;和&#x200B;**[!UICONTROL 檢視區段]** [存取控制許可權](/help/access-control/home.md#permissions)。 閱讀[存取控制總覽](/help/access-control/ui/overview.md)或連絡您的產品管理員以取得必要的許可權。
>* 匯出至HTTP API目的地時目前不支援[同意原則評估](/help/data-governance/enforcement/auto-enforcement.md#consent-policy-evaluation)。 [閱讀全文](/help/destinations/ui/activate-streaming-profile-destinations.md#consent-policy-evaluation)。

如需啟用此目的地對象的指示，請參閱[啟用串流設定檔匯出目的地的對象資料](../../ui/activate-streaming-profile-destinations.md)。

### 目的地屬性 {#attributes}

在[[!UICONTROL 選取屬性]](../../ui/activate-streaming-profile-destinations.md#select-attributes)步驟中，Adobe建議您從[聯合結構描述](../../../profile/home.md#profile-fragments-and-union-schemas)中選取唯一識別碼。 選取唯一識別碼以及您要匯出至目的地的任何其他XDM欄位。

## 設定檔匯出行為 {#profile-export-behavior}

Experience Platform會最佳化HTTP API目的地的設定檔匯出行為，僅在對象資格或其他重大事件後發生設定檔的相關更新時，將資料匯出至API端點。 在下列情況下，設定檔會匯出至您的目的地：

* 設定檔更新是由對應至目的地的至少一個對象的對象成員資格變更所決定。 例如，設定檔已符合對應至目的地的其中一個對象的資格，或已退出對應至目的地的其中一個對象。
* 設定檔更新是由[身分對應](/help/xdm/field-groups/profile/identitymap.md)中的變更所決定。 例如，已符合對應至目的地之其中一個對象資格的設定檔，已在身分對應屬性中新增身分。
* 設定檔更新是由對應到目的地的至少一個屬性的變更所決定。 例如，會將對應步驟中對應至目的地的其中一個屬性新增至設定檔。

在上述所有情況下，只有已發生相關更新的設定檔才會匯出至您的目的地。 例如，如果對應至目的地流程的受眾有一百個成員，且有五個新設定檔符合區段的資格，則匯出至您的目的地的作業將以漸進方式進行，且僅包含五個新設定檔。

請注意，無論變更位於何處，所有對映屬性都會匯出為設定檔。 因此，在上述範例中，將會匯出這五個新設定檔的所有對應屬性，即使屬性本身並未變更亦然。

### 決定資料匯出的因素及匯出中包含的因素 {#what-determines-export-what-is-included}

關於為特定設定檔匯出的資料，請務必瞭解&#x200B;*決定匯出至您HTTP API目的地*&#x200B;的資料以及&#x200B;*匯出中包含哪些資料的兩個不同概念*。

| 決定目的地匯出的因素 | 目的地匯出包含的內容 |
|---------|----------|
| <ul><li>對應的屬性和受眾可作為目的地匯出的提示。 這表示如果任何對應的對象變更狀態（從`null`變更為`realized`或從`realized`變更為`exiting`）或更新任何對應的屬性，將會啟動目的地匯出。</li><li>由於身分目前無法對應至HTTP API目的地，因此特定設定檔上任何身分的變更也會決定目的地匯出專案。</li><li>屬性的變更定義為屬性上的任何更新，無論其是否為相同的值。 這表示即使值本身並未變更，屬性上的覆寫也會視為變更。</li></ul> | <ul><li>`segmentMembership`物件包含啟動資料流中對應的對象，在資格或對象退出事件後，設定檔的狀態已針對該對象變更。 請注意，如果其他未對應的對象與啟動資料流中對應的對象屬於同一個[合併原則](/help/profile/merge-policies/overview.md)，則符合設定檔資格的其他未對應對象可以屬於目的地匯出的一部分。 </li><li>`identityMap`物件中的所有身分也包括在內(Experience Platform目前不支援HTTP API目的地中的身分對應)。</li><li>目的地匯出僅包含對應的屬性。</li></ul> |

{style="table-layout:fixed"}

例如，將此資料流視為HTTP目的地，其中在資料流中選取了三個對象，且四個屬性對應至目的地。

![ HTTP API目的地資料流範例。](/help/destinations/assets/catalog/http/profile-export-example-dataflow.png)

設定檔匯出至目的地的方式，可由符合或結束&#x200B;*三個對應區段*&#x200B;之一的設定檔來決定。 不過，在資料匯出中，`segmentMembership`物件（請參閱下方的[匯出的資料](#exported-data)區段）可能會顯示其他未對應的對象，如果該特定設定檔為其成員，且這些對象與觸發匯出的對象共用相同的合併原則。 如果設定檔符合&#x200B;**擁有DeLorean Cars的客戶**&#x200B;區段的資格，但同時也是&#x200B;**觀看的「回到未來」**&#x200B;電影和&#x200B;**科幻迷**&#x200B;區段的成員，則其他這兩個對象也將出現在資料匯出的`segmentMembership`物件中，即使這些對象未對應到資料流中，前提是這些對象與&#x200B;**擁有DeLorean Cars的客戶**&#x200B;區段共用相同的合併原則。

從設定檔屬性的角度來看，對上述四個對應屬性所做的任何變更將決定目的地匯出，而且設定檔上存在的四個對應屬性中的任何一個都會出現在資料匯出中。

## 歷史資料回填 {#historical-data-backfill}

當您新增對象至現有目的地，或當您建立新目的地並將對象對應至該目的地時，Experience Platform會將歷史對象資格資料匯出至該目的地。 在&#x200B;*之前新增了對象到目的地的符合對象*&#x200B;資格的設定檔，大約會在一小時內匯出到目的地。

## 匯出的資料 {#exported-data}

您匯出的[!DNL Experience Platform]資料以JSON格式登陸您的[!DNL HTTP]目的地。 例如，下列匯出包含符合特定區段資格的設定檔、是另一個兩個區段的成員，且已退出另一個區段。 匯出也包含設定檔屬性的名字、姓氏、出生日期和個人電子郵件地址。 此設定檔的身分識別為ECID和電子郵件。

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

根據您在&#x200B;**[!UICONTROL 包含區段名稱]**&#x200B;和&#x200B;**[!UICONTROL 包含區段時間戳記]**&#x200B;選項的連線目的地流程中選取的UI設定，以下是匯出資料的更多範例：

+++ 下列資料匯出範例包含`segmentMembership`區段中的對象名稱

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

+++ 以下資料匯出範例包含`segmentMembership`區段中的對象時間戳記

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

## 限制和重試原則 {#limits-retry-policy}

在95%的時間中，Experience Platform會嘗試針對每個資料流向HTTP目的地的成功傳送訊息，以每秒少於10,000個要求的速率，提供少於10分鐘的輸送量延遲。

如果對您的HTTP API目的地的請求失敗，Experience Platform會儲存失敗的請求並重試兩次，以將請求傳送至您的端點。