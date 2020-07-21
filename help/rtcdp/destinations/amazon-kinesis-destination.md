---
title: Amazon Kinesis目標
seo-title: Amazon Kinesis目標
description: 建立到Amazon Kinesis儲存的即時出站連接，以便從Adobe Experience Platform流資料。
seo-description: 建立到Amazon Kinesis儲存的即時出站連接，以便從Adobe Experience Platform流資料。
translation-type: tm+mt
source-git-commit: b96286f6a06f0583b45343a513ee64f0025d79a7
workflow-type: tm+mt
source-wordcount: '442'
ht-degree: 2%

---


# （測試版）目 [!DNL Amazon Kinesis] 標


>[!IMPORTANT]
>
>Adobe [!DNL Amazon Kinesis] 即時CDP的目的地目前為beta版。 文件和功能可能會有所變更。

## 概述 {#overview}

該服 [!DNL Kinesis Data Streams] 務可 [!DNL Amazon Web Services] 讓您即時收集和處理大量資料記錄。

您可以建立儲存的即時出站連線， [!DNL Amazon Kinesis] 以從Adobe Experience Platform串流資料。

* 如需詳細資訊 [!DNL Amazon Kinesis]，請參閱 [Amazon檔案](https://docs.aws.amazon.com/streams/latest/dev/introduction.html)。
* 若要連線至使 [!DNL Amazon Kinesis] 用API呼叫，請參閱串 [流目標API教學課程](/help/rtcdp/destinations/streaming-destinations-api-tutorial.md)。
* 若要使用 [!DNL Amazon Kinesis] Adobe即時CDP使用者介面連線，請參閱以下各節。

![UI中的Amazon Kinesis](/help/rtcdp/destinations/assets/aws-kinesis-destination.png)


## 使用案例 {#use-cases}

透過使用串流目的地(例如 [!DNL Amazon Kinesis])，您可以輕鬆將高價值分段事件和相關的描述檔屬性饋送到您選擇的系統中。

例如，潛在客戶下載了白皮書，使其符合「高轉換傾向」區段的資格。 將潛在客戶所處的區段對應至目標， [!DNL Amazon Kinesis] 您就會收到此事件 [!DNL Amazon Kinesis]。 在這裡，您可以採用自行動手的方法，並在活動之上描述業務邏輯，因為您認為最適合企業IT系統。

## 連接目標 {#connect-destination}

如需如 [何連線至您的雲端儲存 ](/help/rtcdp/destinations/cloud-storage-destinations-workflow.md)空間目的地（包括支援的雲端儲存空間目的地）的指示，請參閱雲端儲存空間工作流程 [!DNL Amazon]。

對於目 [!DNL Amazon Kinesis] 標，請在建立目標工作流中輸入以下資訊：

### 在驗證步驟中 {#authentication-step}

* **[!DNL Amazon Web Services]訪問密鑰和密鑰&#x200B;**: 在中[!DNL Amazon Web Services]，生成訪問密鑰——秘密訪問密鑰對，以授予Adobe即時CDP對您帳戶的訪[!DNL Amazon Kinesis]問權。 請參閱[Amazon Web Services檔案瞭解更多](https://docs.aws.amazon.com/IAM/latest/UserGuide/id_credentials_access-keys.html)。
* **地區**: 指出要 [!DNL Amazon Web Services] 將資料串流至的區域。

![帳戶步驟中的輸入欄位](/help/rtcdp/destinations/assets/aws-kinesis-account-step.png)

### 在設定步驟中 {#setup-step}

* **名稱**: 提供您與 [!DNL Amazon Kinesis]
* **說明**: 提供您與的連線說明 [!DNL Amazon Kinesis]。
* **stream**: 提供帳戶中現有資料流的名 [!DNL Amazon Kinesis] 稱。 Adobe即時CDP會將資料匯出至此串流。

![驗證步驟中的輸入欄位](/help/rtcdp/destinations/assets/aws-kinesis-setup-step.png)

<!--

>[!IMPORTANT]
>
>Adobe Real-time CDP needs `write` permissions on the bucket object where the export files will be delivered.

-->

## 啟用區段 {#activate-segments}

如需 [區段啟動工作流程的相關資訊](/help/rtcdp/destinations/activate-destinations.md) ，請參閱啟用設定檔和區段至目的地。

## 匯出的資料 {#exported-data}

您匯出的 [!DNL Experience Platform] 資料會以JSON [!DNL Amazon Kinesis] 格式著陸。 例如，以下事件包含符合特定區段資格並退出其他區段之對象的電子郵件地址設定檔屬性。 此潛在客戶的身分是ECID和電子郵件。

```
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
>* [連接到Amazon Kinesis並使用API調用激活資料](/help/rtcdp/destinations/streaming-destinations-api-tutorial.md)
>* [Azure事件集線器目標](/help/rtcdp/destinations/azure-event-hubs-destination.md)
>* [目標類型和類別](/help/rtcdp/destinations/destination-types.md)

