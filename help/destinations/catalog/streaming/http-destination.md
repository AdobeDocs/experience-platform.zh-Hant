---
keywords: 流；
title: HTTP API連接
description: Adobe Experience Platform的HTTP API目標允許您將配置檔案資料發送到第三方HTTP終結點。
exl-id: 165a8085-c8e6-4c9f-8033-f203522bb288
source-git-commit: f098df9df2baa971db44a6746949f021e212ae3e
workflow-type: tm+mt
source-wordcount: '833'
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

## 連接到目標 {#connect-destination}

要連接到此目標，請按照 [目標配置教程](../../ui/connect-destination.md)。

### 連接參數 {#parameters}

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

* 配置檔案更新是由映射到目標的至少一個段的段成員關係的改變觸發的。 例如，配置檔案已限定映射到目標的段之一或已退出映射到目標的段之一。
* 配置檔案更新是由 [身份映射](/help/xdm/field-groups/profile/identitymap.md)。 例如，已為映射到目標的段之一限定的配置檔案已在標識映射屬性中添加了新標識。
* 配置檔案更新是由至少一個映射到目標的屬性的屬性的更改觸發的。 例如，映射步驟中映射到目標的屬性之一被添加到配置檔案。

在上述所有情況下，只將發生相關更新的配置檔案導出到目標。 例如，如果映射到目標流的段有100個成員，並且有5個新配置檔案符合該段的條件，則向目標的導出是增量的，並且只包括5個新配置檔案。

請注意，無論更改位於何處，都會為配置檔案導出所有映射的屬性。 因此，在上面的示例中，即使屬性本身沒有更改，也會導出這五個新配置檔案的所有映射屬性。

## 導出的資料 {#exported-data}

已導出 [!DNL Experience Platform] 資料到達 [!DNL HTTP] JSON格式的目標。 例如，下面的導出包含符合特定段條件並退出另一個段的配置檔案，並包含配置檔案屬性的名、姓、出生日期和個人電子郵件地址。 此配置檔案的標識為ECID和電子郵件。

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
    "ups": {
      "7841ba61-23c1-4bb3-a495-00d3g5fe1e93": {
        "lastQualificationTime": "2020-05-25T21:24:39Z",
        "status": "exited"
      },
      "59bd2fkd-3c48-4b18-bf56-4f5c5e6967ae": {
        "lastQualificationTime": "2020-05-25T23:37:33Z",
        "status": "existing"
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
