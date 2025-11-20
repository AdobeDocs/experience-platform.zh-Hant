---
keywords: 串流； HTTP目的地
title: HTTP API連線
description: 在Adobe Experience Platform中使用HTTP API目的地，將設定檔資料傳送至第三方HTTP端點，以執行您自己的分析，或針對從Experience Platform匯出的設定檔資料執行您可能需要的任何其他操作。
badgeUltimate: label="Ultimate" type="Positive"
exl-id: 165a8085-c8e6-4c9f-8033-f203522bb288
source-git-commit: 7502810ff329a31f2fdaf6797bc7672118555e6a
workflow-type: tm+mt
source-wordcount: '2752'
ht-degree: 7%

---

# HTTP API連線

## 概觀 {#overview}

>[!IMPORTANT]
>
> 此目的地僅供[Adobe Real-Time Customer Data Platform Ultimate](https://helpx.adobe.com/jp/legal/product-descriptions/real-time-customer-data-platform.html)客戶使用。

HTTP API目的地是[!DNL Adobe Experience Platform]串流目的地，可協助您將設定檔資料傳送至第三方HTTP端點。

若要將設定檔資料傳送至HTTP端點，您必須先在[中](#connect-destination)連線至目的地[!DNL Adobe Experience Platform]。

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
| ---------|----------|---------|
| 匯出類型 | **[!UICONTROL Profile-based]** | 您正在匯出區段的所有成員，以及所需的結構描述欄位（例如：電子郵件地址、電話號碼、姓氏），如[目的地啟用工作流程](../../ui/activate-segment-streaming-destinations.md#mapping)的對應畫面中所選。 |
| 匯出頻率 | **[!UICONTROL Streaming]** | 串流目的地是「永遠在線」的 API 連線。 一旦 Experience Platform 根據受眾評估更新個人檔案，連接器就會將更新傳送到目的地平台。 閱讀更多關於串流平台的[資訊](/help/destinations/destination-types.md#streaming-destinations)。 |

{style="table-layout:auto"}

## 先決條件 {#prerequisites}

若要使用HTTP API目的地將資料匯出Experience Platform，您必須符合下列先決條件：

* 您必須有支援REST API的HTTP端點。
* 您的HTTP端點必須支援Experience Platform設定檔結構描述。 HTTP API目的地不支援轉換至第三方裝載結構描述。 如需Experience Platform輸出結構描述的範例，請參閱[匯出的資料](#exported-data)區段。
* 你的 HTTP 端點必須支援標頭。
* 您的 HTTP 端點必須在 2 秒內回應，以確保資料處理正確並避免逾時錯誤。

>[!TIP]
>
> 你也可以使用 [Adobe Experience Platform Destination SDK](/help/destinations/destination-sdk/overview.md) 設定整合，並將 Experience Platform 設定檔資料傳送到 HTTP 端點。

## mTLS 協定支援與憑證 {#mtls-protocol-support}

您可以使用[!DNL Mutual Transport Layer Security] ([!DNL mTLS])來確保與您的HTTP API目的地連線的輸出連線中的增強安全性。

[!DNL mTLS]是相互驗證的端對端安全性方法，可確保共用資訊的雙方在共用資料之前，都是聲稱的身分。 與[!DNL mTLS]相比，[!DNL TLS]包含額外的步驟，其中伺服器也會要求使用者端的憑證，並在其結尾加以驗證。

如果您想要搭配[!DNL mTLS]個目的地使用[!DNL HTTP API]，您放入[目的地詳細資料](#destination-details)頁面的伺服器位址必須停用[!DNL TLS]通訊協定，而且只能啟用[!DNL mTLS]。 如果端點上仍啟用[!DNL TLS] 1.2通訊協定，則不會傳送使用者端驗證的憑證。 這表示若要搭配您的[!DNL mTLS]目的地使用[!DNL HTTP API]，您的「接收」伺服器端點必須是僅限[!DNL mTLS]啟用的連線端點。

### 擷取及檢查憑證詳細資料 {#certificate}

如果您想檢查憑證細節，如 [!DNL Common Name] （CN） 和 [!DNL Subject Alternative Names] （SAN）以進行額外的第三方驗證，請使用 API 取得憑證並從回應中擷取這些欄位。

更多資訊請參閱 [公開憑證端點文件](../../../data-governance/mtls-api/public-certificate-endpoint.md) 。

## IP 位址允許清單 {#ip-address-allowlist}

為了滿足客戶的安全與合規需求，Experience Platform 提供一份靜態 IP 清單，您可以允許 HTTP API 目的地的權限。 如需允許清單的完整IP清單，請參閱串流目的地的[IP位址允許清單](/help/destinations/catalog/streaming/ip-address-allow-list.md)。

## 支援的驗證型別 {#supported-authentication-types}

HTTP API目的地支援多種對HTTP端點的驗證型別：

* 沒有驗證的HTTP端點；
* 持有人權杖驗證；
* [OAuth 2.0 用戶端憑證的](https://www.oauth.com/oauth2-servers/access-tokens/client-credentials/) 認證方式包括 HTTP 請求的主體表單、 [!DNL client ID]、 [!DNL client secret]和 [!DNL grant type] ，如下範例所示。

```shell
curl --location --request POST '<YOUR_API_ENDPOINT>' \
--header 'Content-Type: application/x-www-form-urlencoded' \
--data-urlencode 'grant_type=client_credentials' \
--data-urlencode 'client_id=<CLIENT_ID>' \
--data-urlencode 'client_secret=<CLIENT_SECRET>'
```

* [OAuth 2.0 用戶端憑證](https://www.oauth.com/oauth2-servers/access-tokens/client-credentials/) ，具備基本授權，授權標頭包含 URL 編碼的 [!DNL client ID] [!DNL client secret]和 。

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
>若要連線到目的地，您需要&#x200B;**[!UICONTROL View Destinations]**&#x200B;和&#x200B;**[!UICONTROL Manage Destinations]** [存取控制許可權](/help/access-control/home.md#permissions)。 閱讀[存取控制總覽](/help/access-control/ui/overview.md)或連絡您的產品管理員以取得必要的許可權。

若要連線到此目的地，請依照[目的地組態教學課程](../../ui/connect-destination.md)中所述的步驟進行。 連線到這個目的地時，您必須提供下列資訊：

### 驗證資訊 {#authentication-information}

>[!CONTEXTUALHELP]
>id="platform_destinations_connect_http_clientcredentialstype"
>title="用戶端憑證類型"
>abstract="選取&#x200B;**內文表單已編碼**，以在要求的內文中包含用戶端 ID 和用戶端密碼，或選取&#x200B;**基本授權**，以在要求的內文中包含用戶端 ID 和用戶端密碼。檢視文件中的範例。"

#### 持有人權杖驗證 {#bearer-token-authentication}

如果您選取&#x200B;**[!UICONTROL Bearer token]**&#x200B;驗證型別以連線至您的HTTP端點，請輸入下列欄位並選取&#x200B;**[!UICONTROL Connect to destination]**：

![UI熒幕的影像，您可在此使用持有人權杖驗證連線至HTTP API目的地。](../../assets/catalog/http/http-api-authentication-bearer.png)

* **[!UICONTROL Bearer token]**：插入持有人權杖以驗證您的HTTP位置。

#### 無驗證 {#no-authentication}

如果您選取&#x200B;**[!UICONTROL None]**&#x200B;驗證型別以連線至您的HTTP端點：

![UI熒幕的影像，您可在其中使用無驗證連線至HTTP API目的地。](../../assets/catalog/http/http-api-authentication-none.png)

當您選取此驗證開啟時，您只需要選取&#x200B;**[!UICONTROL Connect to destination]**，即可建立與端點的連線。

#### OAuth 2密碼驗證 {#oauth-2-password-authentication}

如果您選取&#x200B;**[!UICONTROL OAuth 2 Password]**&#x200B;驗證型別以連線至您的HTTP端點，請輸入下列欄位並選取&#x200B;**[!UICONTROL Connect to destination]**：

![UI熒幕的影像，您可在此使用OAuth 2搭配密碼驗證連線至HTTP API目的地。](../../assets/catalog/http/http-api-authentication-oauth2-password.png)

* **[!UICONTROL Access Token URL]**：您發行存取權杖以及選擇性地重新整理權杖的URL。
* **[!UICONTROL Client ID]**：您的系統指派給Adobe Experience Platform的[!DNL client ID]。
* **[!UICONTROL Client Secret]**：您的系統指派給Adobe Experience Platform的[!DNL client secret]。
* **[!UICONTROL Username]**：存取您HTTP端點的使用者名稱。
* **[!UICONTROL Password]**：存取您HTTP端點的密碼。

#### OAuth 2使用者端憑證驗證 {#oauth-2-client-credentials-authentication}

如果您選取&#x200B;**[!UICONTROL OAuth 2 Client Credentials]**&#x200B;驗證型別以連線至您的HTTP端點，請輸入下列欄位並選取&#x200B;**[!UICONTROL Connect to destination]**：

![UI熒幕的影像，您可在此使用OAuth 2搭配使用者端憑證驗證連線至HTTP API目的地。](../../assets/catalog/http/http-api-authentication-oauth2-client-credentials.png)

>[!WARNING]
> 
>使用[!UICONTROL OAuth 2 Client Credentials]驗證時，[!UICONTROL Access Token URL]最多可以有一個查詢引數。 新增包含更多查詢引數的[!UICONTROL Access Token URL]可能會導致連線至端點時發生問題。

* **[!UICONTROL Access Token URL]**：您發行存取權杖以及選擇性地重新整理權杖的URL。
* **[!UICONTROL Client ID]**：您的系統指派給Adobe Experience Platform的[!DNL client ID]。
* **[!UICONTROL Client Secret]**：您的系統指派給Adobe Experience Platform的[!DNL client secret]。
* **[!UICONTROL Client Credentials Type]**：選取端點支援的OAuth2使用者端認證授權型別：
   * **[!UICONTROL Body Form Encoded]**： 在此情況下， [!DNL client ID] 和 [!DNL client secret] 包含 *在發送給你目的地的請求* 正文中。 舉例請參見 [支援的認證類型](#supported-authentication-types) 章節。
   * **[!UICONTROL Basic Authorization]**：在此情況下，[!DNL client ID]和[!DNL client secret]在經過base64編碼並傳送至您的目的地之後，會包含在&#x200B;*標頭`Authorization`中的*。 如需範例，請參閱[支援的驗證型別](#supported-authentication-types)區段。

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

![UI 畫面圖片，顯示 HTTP 目的地細節已完成欄位。](../../assets/catalog/http/http-api-destination-details.png)

* **[!UICONTROL Name]**：輸入一個你未來能認出這個目的地的名字。
* **[!UICONTROL Description]**&#x200B;輸入描述，幫助你未來辨識該目的地。
* **[!UICONTROL Headers]**：依照以下格式，輸入任何您想要包含在目的地呼叫中的自訂標頭： `header1:value1,header2:value2,...headerN:valueN`。
* **[!UICONTROL HTTP Endpoint]**：您要將設定檔資料傳送至的HTTP端點URL。
* **[!UICONTROL Query parameters]**：您可以選擇將查詢引數新增至HTTP端點URL。 將您使用的查詢參數格式化，類似這樣：`parameter1=value&parameter2=value`。
* **[!UICONTROL Include Segment Names]**：如果您希望資料匯出包含您正在匯出的對象名稱，請切換按鈕。 **注意**：區段名稱僅包含在映射到目的地的區段。 匯出中出現的未對應區段不包括`name`欄位。 關於選擇此選項的資料匯出範例，請參閱 [下方的「匯出資料](#exported-data) 」區塊。
* **[!UICONTROL Include Segment Timestamps]**： 切換：如果你希望資料匯出包含受眾建立與更新的時間戳，以及受眾映射到啟用目的地的時間戳。 關於選擇此選項的資料匯出範例，請參閱 [下方的「匯出資料](#exported-data) 」區塊。

### 啟用警示 {#enable-alerts}

您可以啟用警報以接收有關傳送到您目的地的資料流狀態的通知。 從清單中選取警報以訂閱接收有關資料流狀態的通知。 如需警示的詳細資訊，請參閱[使用UI訂閱目的地警示](../../ui/alerts.md)的指南。

當您完成提供目的地連線的詳細資訊時，請選取&#x200B;**[!UICONTROL Next]**。

## 啟動此目標的對象 {#activate}

>[!IMPORTANT]
> 
>* 若要啟用資料，您需要&#x200B;**[!UICONTROL View Destinations]**、**[!UICONTROL Activate Destinations]**、**[!UICONTROL View Profiles]**&#x200B;和&#x200B;**[!UICONTROL View Segments]** [存取控制許可權](/help/access-control/home.md#permissions)。 閱讀[存取控制總覽](/help/access-control/ui/overview.md)或連絡您的產品管理員以取得必要的許可權。
>* 匯出至HTTP API目的地時目前不支援[同意原則評估](/help/data-governance/enforcement/auto-enforcement.md#consent-policy-evaluation)。 [閱讀全文](/help/destinations/ui/activate-streaming-profile-destinations.md#consent-policy-evaluation)。

如需啟用此目的地對象的指示，請參閱[啟用串流設定檔匯出目的地的對象資料](../../ui/activate-streaming-profile-destinations.md)。

### 目的地屬性 {#attributes}

在[[!UICONTROL Select attributes]](../../ui/activate-streaming-profile-destinations.md#select-attributes)步驟中，Adobe建議您從[聯合結構描述](../../../profile/home.md#profile-fragments-and-union-schemas)中選取唯一識別碼。 選取唯一識別碼以及您要匯出至目的地的任何其他XDM欄位。

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
| <ul><li>對應的屬性和區段可作為目的地匯出的提示。 這表示如果設定檔的`segmentMembership`狀態變更為`realized`或`exiting`，或任何對應的屬性已更新，將會啟動目的地匯出。</li><li>由於身分目前無法對應至HTTP API目的地，因此特定設定檔上任何身分的變更也會決定目的地匯出專案。</li><li>屬性的變更定義為屬性上的任何更新，無論其是否為相同的值。 這表示即使值本身並未變更，屬性上的覆寫也會視為變更。</li></ul> | <ul><li>`segmentMembership`物件包含對映在啟動資料流中的區段，在資格或區段退出事件後，設定檔的狀態已針對該區段變更。 請注意，如果其他符合設定檔資格的未對應區段與啟動資料流中所對應的區段屬於同一個[合併原則](/help/profile/merge-policies/overview.md)，則這些區段可以是目的地匯出的一部分。<br> **重要**：啟用&#x200B;**[!UICONTROL Include Segment Names]**&#x200B;選項時，只有對應至目的地的區段才會包含區段名稱。 匯出中顯示的未對應區段不會包含`name`欄位，即使該選項已啟用亦然。 </li><li>`identityMap`物件中的所有身分也包括在內(Experience Platform目前不支援HTTP API目的地中的身分對應)。</li><li>目的地匯出僅包含對應的屬性。</li></ul> |

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

根據您在&#x200B;**[!UICONTROL Include Segment Names]**&#x200B;和&#x200B;**[!UICONTROL Include Segment Timestamps]**&#x200B;選項的連線目的地流程中選取的UI設定，以下是匯出資料的更多範例：

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
          },
          "354e086f-2e11-49a2-9e39-e5d9a76be683": {
            "lastQualificationTime": "2020-04-15T02:41:50+0000",
            "status": "realized"
          }
        }
      }
```

**注意**：在此範例中，第一個區段(`5b998cb9-9488-4ec3-8d95-fa8338ced490`)已對應到目的地，並包含`name`欄位。 第二個區段(`354e086f-2e11-49a2-9e39-e5d9a76be683`)未對應到目的地，而且不包含`name`欄位，即使已啟用&#x200B;**[!UICONTROL Include Segment Names]**&#x200B;選項也是如此。

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

## 限制與重試政策 {#limits-retry-policy}

在 95% 的時間裡，Experience Platform 嘗試提供每秒少於 10,000 次資料流 HTTP 目的地的訊息傳輸延遲，且每秒請求次數少於 10 分鐘。

若 HTTP API 目的地的請求失敗，Experience Platform 會儲存失敗的請求，並重試兩次將請求傳送到你的端點。

## 疑難排解 {#troubleshooting}

若要確保可靠的資料傳送並避免逾時問題，請依照[先決條件](#prerequisites)區段中的指定，確定您的HTTP端點在2秒內回應Experience Platform要求。 需要更長時間的回應會導致逾時錯誤。
