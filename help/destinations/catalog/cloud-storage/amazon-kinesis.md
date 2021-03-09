---
keywords: AmazonKinesis；移動目標；
title: AmazonKinesis連接
description: 建立與AmazonKinesis儲存區的即時出站連線，以串流Adobe Experience Platform的資料。
translation-type: tm+mt
source-git-commit: 32cb198bcf2c142b50c4b7a60282f0c923be06b1
workflow-type: tm+mt
source-wordcount: '510'
ht-degree: 2%

---


# （測試版）[!DNL Amazon Kinesis]連線

>[!IMPORTANT]
>
>平台中的[!DNL Amazon Kinesis]目標當前處於測試階段。 文件和功能可能會有所變更。

[!DNL Kinesis Data Streams]服務由[!DNL Amazon Web Services]提供，可讓您即時收集和處理大量資料記錄。

您可以建立與[!DNL Amazon Kinesis]儲存空間的即時出站連線，以串流來自Adobe Experience Platform的資料。

* 有關[!DNL Amazon Kinesis]的更多資訊，請參見[Amazon文檔](https://docs.aws.amazon.com/streams/latest/dev/introduction.html)。
* 若要以程式設計方式連線至[!DNL Amazon Kinesis]，請參閱[串流目標API教學課程](../../api/streaming-destinations.md)。
* 要使用平台用戶介面連接到[!DNL Amazon Kinesis]，請參見以下各節。

![Amazon·Kinesis在UI中](../../assets/catalog/cloud-storage/amazon-kinesis/catalog.png)

## 使用案例 {#use-cases}

透過使用串流目標（例如[!DNL Amazon Kinesis]），您可以輕鬆將高價值區段事件和相關的描述檔屬性饋送到您選擇的系統中。

例如，潛在客戶下載了白皮書，使其符合「高轉換傾向」區段的資格。 通過將潛在客戶所屬的段映射到[!DNL Amazon Kinesis]目標，您將在[!DNL Amazon Kinesis]中收到此事件。 在這裡，您可以採用自行動手的方法，並在活動之上描述業務邏輯，因為您認為最適合企業IT系統。

## 導出類型{#export-type}

**基於描述檔** -您要匯出區段的所有成員，以及所要的架構欄位(例如：電子郵件地址、電話號碼、姓氏)，這是從目標啟動工作流程的「選取屬性」畫面 [中選擇的](../../ui/activate-destinations.md#select-attributes)。

## 連接目標{#connect-destination}

如需如何連線至您的雲端儲存目的地（包括[!DNL Amazon]支援的目的地）的指示，請參閱[雲端儲存目的地工作流程](./workflow.md)。

對於[!DNL Amazon Kinesis]目標，請在建立目標工作流中輸入以下資訊：

### 在驗證步驟{#authentication-step}中

* **[!DNL Amazon Web Services]訪問密鑰和密鑰**:在中 [!DNL Amazon Web Services]，產生一 `access key - secret access key` 對以授與您帳戶的平台存 [!DNL Amazon Kinesis] 取權。請參閱[Amazon網站服務檔案](https://docs.aws.amazon.com/IAM/latest/UserGuide/id_credentials_access-keys.html)瞭解更多資訊。
* **地區**:指出要 [!DNL Amazon Web Services] 將資料串流至的區域。

![帳戶步驟中的輸入欄位](../../assets/catalog/cloud-storage/amazon-kinesis/account.png)

### 在設定步驟{#setup-step}中

* **名稱**:提供您與  [!DNL Amazon Kinesis]
* **說明**:提供您與的連線說明 [!DNL Amazon Kinesis]。
* **stream**:提供帳戶中現有資料流的名 [!DNL Amazon Kinesis] 稱。平台會將資料匯出至此串流。
* **[!UICONTROL 行銷動作]**:行銷動作會指出將資料匯出至目的地的方式。您可以從Adobe定義的行銷動作中選擇，也可以建立自己的行銷動作。 如需行銷動作的詳細資訊，請參閱「Adobe Experience Platform的資料治理」頁面。 [](../../../data-governance/policies/overview.md)如需個別Adobe定義之行銷動作的詳細資訊，請參閱[資料使用政策概述](../../../data-governance/policies/overview.md)。

![驗證步驟中的輸入欄位](../../assets/catalog/cloud-storage/amazon-kinesis/setup.png)

<!--

>[!IMPORTANT]
>
>Platform needs `write` permissions on the bucket object where the export files will be delivered.

-->

## 啟用區段{#activate-segments}

如需區段啟動工作流程的相關資訊，請參閱[啟用設定檔和區段至目標](../../ui/activate-destinations.md)。

## 導出資料{#exported-data}

您匯出的[!DNL Experience Platform]資料會以JSON格式登入[!DNL Amazon Kinesis]。 例如，以下事件包含符合特定區段資格並退出其他區段之對象的電子郵件地址設定檔屬性。 此潛在客戶的身分是ECID和電子郵件。

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



>[!MORELIKETHIS]
>
>* [連線至AmazonKinesis，並使用Flow Service API啟動資料](../../api/streaming-destinations.md)
>* [Azure事件集線器目標](./azure-event-hubs.md)
>* [目標類型和類別](../../destination-types.md)

