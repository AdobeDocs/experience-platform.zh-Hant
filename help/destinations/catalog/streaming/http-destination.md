---
title: (Beta)HTTP API連接
keywords: 流；
description: Adobe Experience Platform的HTTP API目標允許您將配置檔案資料發送到第三方HTTP終結點。
exl-id: 165a8085-c8e6-4c9f-8033-f203522bb288
source-git-commit: c62117de27b150f072731c910bb0593ce1fca082
workflow-type: tm+mt
source-wordcount: '1560'
ht-degree: 1%

---

# (Beta)HTTP API連接

>[!IMPORTANT]
>
>平台中的HTTP API目標當前處於Beta中。 文件和功能可能會有所變更。

## 總覽 {#overview}

HTTP API目標是 [!DNL Adobe Experience Platform] 流目標，幫助您將配置檔案資料發送到第三方HTTP終結點。

要向HTTP終結點發送配置檔案資料，必須首先 [連接到目標](#connect-destination) 在 [!DNL Adobe Experience Platform]。

## 使用案例 {#use-cases}

HTTP目標針對需要將XDM配置檔案資料和訪問群體段導出到通用HTTP端點的客戶。

HTTP端點可以是客戶自己的系統或第三方解決方案。

## 導出類型和頻率 {#export-type-frequency}

有關目標導出類型和頻率的資訊，請參閱下表。

| 項目 | 類型 | 附註 |
---------|----------|---------|
| 導出類型 | **[!UICONTROL 基於配置檔案]** | 您正在導出段的所有成員以及所需的架構欄位(例如：電子郵件地址、電話號碼、姓氏)，在「選擇配置檔案屬性」螢幕中選擇 [目標激活工作流](../../ui/activate-batch-profile-destinations.md#select-attributes)。 |
| 導出頻率 | **[!UICONTROL 流]** | 流目標是基於API的「始終開啟」連接。 一旦基於段評估在Experience Platform中更新配置檔案，連接器就將更新下游發送到目標平台。 閱讀有關 [流目標](/help/destinations/destination-types.md#streaming-destinations)。 |

{style=&quot;table-layout:auto&quot;}

## 先決條件 {#prerequisites}

>[!IMPORTANT]
>
>如果您希望為公司啟用HTTP API目標測試功能，請與Adobe代表或Adobe客戶服務人員聯繫。

要使用HTTP API目標導出Experience Platform外的資料，必須滿足以下先決條件：

* 必須具有支援REST API的HTTP終結點。
* 您的HTTP終結點必須支援Experience Platform配置檔案架構。 HTTP API目標中不支援對第三方負載架構的轉換。 請參閱 [導出的資料](#exported-data) 的子節。
* HTTP終結點必須支援標頭。
* 您的HTTP終結點必須支援 [OAuth 2.0客戶端憑據](https://www.oauth.com/oauth2-servers/access-tokens/client-credentials/) 驗證。 當HTTP API目標處於測試階段時，此要求有效。
* 客戶端憑據需要包括在對終結點的POST請求正文中，如下例所示。

```shell
curl --location --request POST '<YOUR_API_ENDPOINT>' \
--header 'Content-Type: application/x-www-form-urlencoded' \
--data-urlencode 'grant_type=client_credentials' \
--data-urlencode 'client_id=<CLIENT_ID>' \
--data-urlencode 'client_secret=<CLIENT_SECRET>'
```

您還可以使用 [Adobe Experience Platform Destination SDK](/help/destinations/destination-sdk/overview.md) 設定整合併將Experience Platform配置檔案資料發送到HTTP終結點。

## IP地址允許清單 {#ip-address-allowlist}

為滿足客戶的安全性和合規性要求，Experience Platform提供了一個靜態IP清單，您可以允許列出該HTTP API目標。 請參閱 [流目標的IP地址允許清單](/help/destinations/catalog/streaming/ip-address-allow-list.md) 清單。

## 連接到目標 {#connect-destination}

要連接到此目標，請按照 [目標配置教程](../../ui/connect-destination.md)。

### 連接參數 {#parameters}

>[!CONTEXTUALHELP]
>id="platform_destinations_connect_http_clientcredentialstype"
>title="客戶端憑據類型"
>abstract="選擇 **體形編碼** 將客戶端ID和客戶端機密包含在請求正文中，或 **基本授權** 將客戶端ID和客戶端機密包含在授權標頭中。 查看文檔中的示例。"

>[!CONTEXTUALHELP]
>id="platform_destinations_connect_http_headers"
>title="標頭"
>abstract="按照以下格式輸入要包括在目標調用中的任何自定義標頭： `header1:value1,header2:value2,...headerN:valueN`"

>[!CONTEXTUALHELP]
>id="platform_destinations_connect_http_endpoint"
>title="HTTP終結點"
>abstract="要將配置檔案資料發送到的HTTP終結點的URL。"

>[!CONTEXTUALHELP]
>id="platform_destinations_connect_http_includesegmentnames"
>title="包括段名稱"
>abstract="如果希望資料導出包含要導出的段的名稱，則切換。 查看資料導出示例的文檔，並選中此選項。"

>[!CONTEXTUALHELP]
>id="platform_destinations_connect_http_includesegmenttimestamps"
>title="包括段時間戳"
>abstract="如果希望資料導出包括建立和更新段時的UNIX時間戳，以及將段映射到要激活的目標時的UNIX時間戳，則切換。 查看資料導出示例的文檔，並選中此選項。"

>[!CONTEXTUALHELP]
>id="platform_destinations_connect_http_queryparameters"
>title="查詢參數"
>abstract="也可以將查詢參數添加到HTTP終結點URL。 設定您使用的查詢參數的格式如下： `parameter1=value&parameter2=value`。"

同時 [設定](../../ui/connect-destination.md) 此目標，必須提供以下資訊：

* **[!UICONTROL http終結點]**:這樣 [!DNL URL] 要向其發送配置檔案資料的HTTP終結點。
   * （可選）您可以將查詢參數添加到 [!UICONTROL http終結點] [!DNL URL]。
* **[!UICONTROL auth終結點]**:這樣 [!DNL URL] 用於的HTTP終結點 [!DNL OAuth2] 驗證。
* **[!UICONTROL 客戶端ID]**:這樣 [!DNL clientID] 參數 [!DNL OAuth2] 客戶端憑據。
* **[!UICONTROL 客戶端密碼]**:這樣 [!DNL clientSecret] 參數 [!DNL OAuth2] 客戶端憑據。

   >[!NOTE]
   >
   >僅 [!DNL OAuth2] 當前支援客戶端憑據。

* **[!UICONTROL 名稱]**:輸入將來用於識別此目標的名稱。
* **[!UICONTROL 說明]**:輸入將幫助您在將來確定此目標的說明。
* **[!UICONTROL 自定義標題]**:按以下格式輸入要包括在目標調用中的任何自定義標頭： `header1:value1,header2:value2,...headerN:valueN`。

   >[!IMPORTANT]
   >
   >當前實現至少需要一個自定義頭。 此限制將在以後的更新中解決。

## 將段激活到此目標 {#activate}

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
| <ul><li>映射的屬性和段用作目標導出的提示。 這意味著，如果任何映射段更改狀態（從null更改為已實現或從已實現/現有更新為退出）或任何映射屬性被更新，則將啟動目標導出。</li><li>由於標識當前無法映射到HTTP API目標，因此給定配置檔案上任何標識的更改也會決定目標導出。</li><li>屬性的更改定義為屬性上的任何更新，無論其值是否相同。 這意味著，即使值本身未更改，屬性上的覆蓋也被視為更改。</li></ul> | <ul><li>所有段（具有最新成員身份狀態）都包含在 `segmentMembership` 的雙曲餘切值。</li><li>中的所有標識 `identityMap` 對象也包括在內(Experience Platform當前不支援HTTP API目標中的標識映射)。</li><li>目標導出中只包含映射的屬性。</li></ul> |

{style=&quot;table-layout:fixed&quot;

例如，將此資料流視為HTTP目標，其中在資料流中選擇了三個段，並將四個屬性映射到目標。

![HTTP API目標資料流](/help/destinations/assets/catalog/http/profile-export-example-dataflow.png)

導出到目標的配置檔案可由符合或退出其中一個配置檔案來確定 *三個映射段*。 但是，在資料導出中，在 `segmentMembership` 對象（請參見） [導出的資料](#exported-data) )中，如果特定配置檔案是其成員，則可能會顯示其他未映射的段。 如果配置檔案符合DeLorean Cars分部客戶的資格，但也是受觀看的「回到未來」電影和科幻片迷分部的成員，則另外兩個分部也將出現在 `segmentMembership` 資料導出的對象，即使這些對象未映射到資料流中。

從配置檔案屬性的視點來看，對上述四個屬性的任何更改都將確定目標導出，並且配置檔案上存在的四個映射屬性中的任何一個都將出現在資料導出中。

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
