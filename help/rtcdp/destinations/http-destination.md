---
keywords: streaming;
title: HTTP目的地是即時客戶資料平台目的地，可協助您將描述檔資料傳送至協力廠商HTTP端點。
seo-title: HTTP目的地是即時客戶資料平台目的地，可協助您將描述檔資料傳送至協力廠商HTTP端點。
description: HTTP目的地是即時客戶資料平台目的地，可協助您將描述檔資料傳送至協力廠商HTTP端點。
seo-description: HTTP目的地是即時客戶資料平台目的地，可協助您將描述檔資料傳送至協力廠商HTTP端點。
translation-type: tm+mt
source-git-commit: 6eabcd70b133051205b669253f280cb92c24412f
workflow-type: tm+mt
source-wordcount: '568'
ht-degree: 2%

---


# (Alpha)目 [!DNL HTTP] 標

>[!IMPORTANT]
>
>Adobe [!DNL HTTP] 即時CDP中的目標目前位於alpha。 文件和功能可能會有所變更。

## 概述 {#overview}

目 [!DNL HTTP] 標是串流目 [!DNL Real-time Customer Data Platform] 標，可協助您將描述檔資料傳送至協力廠商端 [!DNL HTTP] 點。

若要傳送描述檔資 [!DNL HTTP] 料至端點，您必須先連線至中的目標 [[!DNL Real-time Customer Data Platform]](#connect-destination)。

## 使用案例 {#use-cases}

目標 [!DNL HTTP] 對象是需要將XDM個人檔案資料和受眾細分匯出至一般端點的 [!DNL HTTP] 客戶。

[!DNL HTTP] 端點可以是客戶自己的系統或第三方解決方案。

## 連接到目標 {#connect-destination}

1. 在「連 **[!UICONTROL 接]** >目 **[!UICONTROL 標]**」中，選 [!DNL HTTP API]擇並選 **[!UICONTROL 擇配置]**。

   ![啟動HTTP目標](assets/activate-http-destination.png)

   >[!NOTE]
   >
   >如果此目標已存在連接，您可以在目標卡上看到 **[!UICONTROL 「激活]** 」按鈕。 有關「激活」( **[!UICONTROL Activate]** )和「配置」( **[!UICONTROL Configure]**)之間差異的詳細資訊，請參 [閱目標工作區文檔的「目錄](../destinations/destinations-workspace.md#catalog) 」(Catalog)部分。
   >
   >![啟動HTTP目標](assets/connect-http-destination.png)

2. 在「帳 [!UICONTROL 戶] 」步驟中，您需要定義HTTP端點連線詳細資訊。 選 **[!UICONTROL 擇新帳戶]** ，然後輸入要連接的HTTP端點的連接詳細資訊。
   * **[!UICONTROL httpEndpoint]**:您要 [!DNL URL] 將描述檔資料傳送至的HTTP端點的完整。
      * （可選）您可以將查詢參數添加 [!UICONTROL 到httpEndpoint][!DNL URL]。
   * **[!UICONTROL authEndpoint]**:用於驗 [!DNL URL] 證的HTTP端點的完 [!DNL OAuth2] 整。
   * **[!UICONTROL 用戶端ID]**:用戶 [!DNL clientID] 端認證中使用 [!DNL OAuth2] 的參數。
   * **[!UICONTROL 用戶端密碼]**:用戶 [!DNL clientSecret] 端認證中使用 [!DNL OAuth2] 的參數。

   >[!NOTE]
   >
   >目前 [!DNL OAuth2] 僅支援用戶端認證。

   ![HTTP端點連線](assets/connect-http-endpoint.png)
3. 按一 **[!UICONTROL 下「連線至目的地]**」。
4. 連接成功後，按一下「下 **[!UICONTROL 一步]**」。
5. 在「驗 [!UICONTROL 證] 」步驟中，輸入帳戶驗證憑證：
   * **[!UICONTROL 名稱]**:輸入您將來識別此目的地的名稱。
   * **[!UICONTROL 說明]**:輸入說明，以幫助您識別未來的目標。
   * **[!UICONTROL 自訂標題]**:輸入您想要納入目標呼叫的任何自訂標題，請遵循下列格式： `header1:value1,header2:value2,...headerN:valueN`.

      >[!IMPORTANT]
      >
      >目前的實作至少需要一個自訂標題。 此限制將在日後的更新中解決。
   ![HTTP驗證](assets/authentication-http-connection.png)

6. **[!UICONTROL 行銷使用案例]**:行銷使用案例會指出將資料匯出至目的地的方式。 您可以從Adobe定義的行銷使用案例中選擇，也可以建立自己的行銷使用案例。 有關行銷使用案例的詳細資訊，請參 [閱即時CDP中的資料治理頁](../privacy/data-governance-overview.md#destinations) 。 如需個別Adobe定義之行銷使用案例的詳細資訊，請參閱「資 [料使用政策」概觀](../../data-governance/policies/overview.md#core-actions)。
7. 按一 **[!UICONTROL 下建立目標]**。

## 啟用區段

如需 [區段啟動工作流程的相關資訊](activate-destinations.md#select-attributes) ，請參閱啟用設定檔和區段至目的地。

## 目標屬性

在「選 [[!UICONTROL 擇屬性]](activate-destinations.md#select-attributes) 」步驟中，當 [將區段啟動至](activate-destinations.md) 目標時，建議您從聯合架構中選取唯一 [!DNL HTTP] 識別碼 [](../../profile/home.md#profile-fragments-and-union-schemas)。 選擇要導出到目標的唯一標識符和任何其他XDM欄位。

## 匯出的資料 {#exported-data}

您匯出的 [!DNL Experience Platform] 資料會以JSON格 [!DNL HTTP] 式載入您的目的地。 例如，以下事件包含符合特定區段資格並退出其他區段之對象的電子郵件地址設定檔屬性。 此潛在客戶的身份是 [!DNL ECID] 電子郵件。

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
