---
keywords: 流；
title: HTTP連線
description: Adobe Experience Platform中的HTTP目的地可讓您將設定檔資料傳送至協力廠商HTTP端點。
exl-id: 165a8085-c8e6-4c9f-8033-f203522bb288
source-git-commit: 802b1844bec1e577e978da5d5a69de87278c04b9
workflow-type: tm+mt
source-wordcount: '361'
ht-degree: 3%

---

# (Alpha)[!DNL HTTP]連接

>[!IMPORTANT]
>
>Platform中的[!DNL HTTP]目標目前位於Alpha中。 文件和功能可能會有所變更。

## 概覽 {#overview}

[!DNL HTTP]目的地是[!DNL Adobe Experience Platform]串流目的地，可協助您將設定檔資料傳送至第三方[!DNL HTTP]端點。

若要將配置檔案資料發送到[!DNL HTTP]端點，必須先連接到[[!DNL Adobe Experience Platform]](#connect-destination)中的目標。

## 使用案例 {#use-cases}

[!DNL HTTP]目標會鎖定需要將XDM設定檔資料和對象區段匯出至一般[!DNL HTTP]端點的客戶。

[!DNL HTTP] 端點可以是客戶自己的系統或第三方解決方案。

## 連接到目標 {#connect}

要連接到此目標，請按照[目標配置教程](../ui/connect-destination.md)中所述的步驟操作。

### 連線參數 {#parameters}

在[設定](../ui/connect-destination.md)此目標時，您必須提供下列資訊：

* **[!UICONTROL httpEndpoint]**:您 [!DNL URL] 要將設定檔資料傳送至的HTTP端點。
   * 您可以選擇將查詢參數新增至[!UICONTROL httpEndpoint] [!DNL URL]。
* **[!UICONTROL authEndpoint]**:用 [!DNL URL] 於驗證的HTTP端 [!DNL OAuth2] 點。
* **[!UICONTROL 用戶端ID]**:用 [!DNL clientID] 戶端憑證中 [!DNL OAuth2] 使用的參數。
* **[!UICONTROL 用戶端密碼]**:用 [!DNL clientSecret] 戶端憑證中 [!DNL OAuth2] 使用的參數。

   >[!NOTE]
   >
   >當前僅支援[!DNL OAuth2]客戶端憑據。

* **[!UICONTROL 名稱]**:輸入一個名稱，以便您將來識別此目標。
* **[!UICONTROL 說明]**:輸入說明，以便您在未來識別此目的地。
* **[!UICONTROL 自訂標題]**:輸入您要納入目的地呼叫的任何自訂標題，請依照以下格式： `header1:value1,header2:value2,...headerN:valueN`.

   >[!IMPORTANT]
   >
   >目前的實作至少需要一個自訂標頭。 此限制將在日後的更新中解決。

## 啟用此目的地的區段 {#activate}

請參閱[將設定檔和區段啟用至目的地](../ui/activate-destinations.md#select-attributes) ，以取得將對象區段啟用至目的地的指示。

## 目標屬性 {#attributes}

在[[!UICONTROL 選擇屬性]](../ui/activate-destinations.md#select-attributes)步驟中，當[將區段](../ui/activate-destinations.md)激活到[!DNL HTTP]目標時，Adobe建議您從[聯合架構](../../profile/home.md#profile-fragments-and-union-schemas)中選擇唯一標識符。 選取唯一識別碼，以及您要匯出至目的地的任何其他XDM欄位。

## 匯出的資料 {#exported-data}

匯出的[!DNL Experience Platform]資料會以JSON格式將資料導入[!DNL HTTP]目的地。 例如，以下事件包含已符合特定區段資格並退出其他區段之對象的電子郵件地址設定檔屬性。 此潛在客戶的身分識別為[!DNL ECID]和電子郵件。

```json
{
  "person": {
    "email": "yourstruly@adobe.con"
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
