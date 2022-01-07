---
keywords: 流；
title: HTTP連線
description: Adobe Experience Platform中的HTTP API目的地可讓您將設定檔資料傳送至協力廠商HTTP端點。
exl-id: 165a8085-c8e6-4c9f-8033-f203522bb288
source-git-commit: 8d2c5ef477d4707be4c0da43ba1f672fac797604
workflow-type: tm+mt
source-wordcount: '633'
ht-degree: 1%

---

# （測試版） [!DNL HTTP] API連線

>[!IMPORTANT]
>
>此 [!DNL HTTP] Platform中的目的地目前為測試版。 文件和功能可能會有所變更。

## 總覽 {#overview}

此 [!DNL HTTP] API目的地是 [!DNL Adobe Experience Platform] 可協助您將設定檔資料傳送至協力廠商的串流目的地 [!DNL HTTP] 端點。

若要將設定檔資料傳送至 [!DNL HTTP] 端點，您必須先連線至 [[!DNL Adobe Experience Platform]](#connect-destination).

## 使用案例 {#use-cases}

此 [!DNL HTTP] 目標定位於需要將XDM設定檔資料和對象區段匯出為一般的客戶 [!DNL HTTP] 端點。

[!DNL HTTP] 端點可以是客戶自己的系統或第三方解決方案。

## 連接到目標 {#connect}

若要連線至此目的地，請依照 [目的地設定教學課程](../../ui/connect-destination.md).

### 連線參數 {#parameters}

同時 [設定](../../ui/connect-destination.md) 此目的地時，您必須提供下列資訊：

* **[!UICONTROL httpEndpoint]**:the [!DNL URL] HTTP端點，以便將設定檔資料傳送至該端點。
   * （可選）您可以將查詢參數新增至 [!UICONTROL httpEndpoint] [!DNL URL].
* **[!UICONTROL authEndpoint]**:the [!DNL URL] 用於的HTTP端點 [!DNL OAuth2] 驗證。
* **[!UICONTROL 用戶端ID]**:the [!DNL clientID] 參數 [!DNL OAuth2] 客戶端憑據。
* **[!UICONTROL 用戶端密碼]**:the [!DNL clientSecret] 參數 [!DNL OAuth2] 客戶端憑據。

   >[!NOTE]
   >
   >僅 [!DNL OAuth2] 當前支援客戶端憑據。

* **[!UICONTROL 名稱]**:輸入一個名稱，以便您將來識別此目標。
* **[!UICONTROL 說明]**:輸入說明，以便您在未來識別此目的地。
* **[!UICONTROL 自訂標題]**:輸入您要納入目的地呼叫的任何自訂標題，請依照以下格式： `header1:value1,header2:value2,...headerN:valueN`.

   >[!IMPORTANT]
   >
   >目前的實作至少需要一個自訂標頭。 此限制將在日後的更新中解決。

## 啟用此目的地的區段 {#activate}

請參閱 [對串流設定檔匯出目的地啟用受眾資料](../../ui/activate-streaming-profile-destinations.md) 以取得啟用受眾區段至此目的地的指示。

### 目標屬性 {#attributes}

在 [[!UICONTROL 選擇屬性]](../../ui/activate-streaming-profile-destinations.md#select-attributes) 步驟，Adobe建議您從 [聯合方案](../../../profile/home.md#profile-fragments-and-union-schemas). 選取唯一識別碼，以及您要匯出至目的地的任何其他XDM欄位。

## 設定檔匯出行為 {#profile-export-behavior}

Experience Platform會最佳化將設定檔匯出行為匯出至您的HTTP API目的地，以僅在符合區段資格或其他重大事件後發生設定檔的相關更新時，將資料匯出至API端點。 設定檔會在下列情況下匯出至您的目的地：

* 至少有一個區段對應至目的地，區段成員資格有所變更，便觸發設定檔更新。 例如，設定檔已符合對應至目的地的其中一個區段資格，或已退出對應至目的地的其中一個區段。
* 設定檔更新是由 [身分圖](/help/xdm/field-groups/profile/identitymap.md). 例如，已符合其中一個對應至目的地區段資格的設定檔，已在「身分對應」屬性中新增身分識別。
* 設定檔更新是由至少一個已對應至目的地之屬性的屬性變更所觸發。 例如，對應步驟中對應至目的地的其中一個屬性會新增至設定檔。

在上述所有情況中，只有發生相關更新的設定檔會匯出至您的目的地。 例如，如果對應至目的地流程的區段有100個成員，且有5個新設定檔符合該區段的資格，則匯出至目的地的作業會是增量的，且僅包含5個新設定檔。

請注意，無論變更在何處，所有對應屬性都會針對設定檔匯出。 因此，在上述範例中，即使屬性本身未變更，這五個新設定檔的所有對應屬性也會匯出。

## 匯出的資料 {#exported-data}

已導出 [!DNL Experience Platform] 資料登陸 [!DNL HTTP] 目的地。 例如，以下事件包含已符合特定區段資格並退出其他區段之對象的電子郵件地址設定檔屬性。 此潛在客戶的身份為 [!DNL ECID] 和電子郵件。

```json
{
  "person": {
    "email": "yourstruly@adobe.com"
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
