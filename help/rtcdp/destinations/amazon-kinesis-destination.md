---
title: Amazon Kinesis目標
seo-title: Amazon Kinesis目標
description: 建立到Amazon Kinesis儲存的即時出站連接，以便從Adobe Experience Platform流資料。
seo-description: 建立到Amazon Kinesis儲存的即時出站連接，以便從Adobe Experience Platform流資料。
translation-type: tm+mt
source-git-commit: a18f89531cf024f61b054b47a660bd26766bebf6
workflow-type: tm+mt
source-wordcount: '422'
ht-degree: 0%

---


# Amazon Kinesis目標

## 概述 {#overview}

Amazon [!DNL Kinesis Data Streams] Web Services提供的服務可讓您即時收集和處理大量資料記錄。

您可以建立儲存的即時出站連線， [!DNL Amazon Kinesis] 以從Adobe Experience Platform串流資料。

* 如需詳細資訊 [!DNL Amazon Kinesis]，請參閱 [Amazon檔案](https://docs.aws.amazon.com/streams/latest/dev/introduction.html)。
* 若要連線至使 [!DNL Amazon Kinesis] 用API呼叫，請參閱串 [流目標API教學課程]。
* 若要使用 [!DNL Amazon Kinesis] Adobe即時CDP使用者介面連線，請參閱以下各節。

![UI中的Amazon Kinesis](/help/rtcdp/destinations/assets/aws-kinesis-destination.png)


## 使用案例 {#use-cases}

通過使用Amazon Kinesis等流目標，您可以輕鬆地將高價值細分事件和相關的配置檔案屬性反饋到您選擇的系統中。

例如，潛在客戶下載了白皮書，使其符合「高轉換傾向」區段的資格。 通過將潛在客戶所屬的段映射到Amazon Kinesis目標，您將在Amazon Kinesis中收到此事件。 在這裡，您可以採用自行動手的方法，並在活動之上描述業務邏輯，因為您認為最適合企業IT系統。

## 連接目標 {#connect-destination}

如需如 [何連線至您的雲端儲存 ](/help/rtcdp/destinations/cloud-storage-destinations-workflow.md)空間目的地（包括支援的雲端儲存空間目的地）的指示，請參閱雲端儲存空間工作流程 [!DNL Amazon]。

對於目 [!DNL Amazon Kinesis] 標，請在建立目標工作流中輸入以下資訊：

### 在帳戶步驟中 {#account-step}

* **Amazon Web Services訪問密鑰和密鑰**: 在中 [!DNL Amazon Web Services]，生成訪問密鑰——秘密訪問密鑰對，以授予Adobe即時CDP對您帳戶的訪 [!DNL Amazon Kinesis] 問權。 請參閱 [Amazon Web Services檔案瞭解更多](https://docs.aws.amazon.com/IAM/latest/UserGuide/id_credentials_access-keys.html)。
* **地區**: 指出要 [!DNL Amazon Web Services] 將資料串流至的區域。

![帳戶步驟中的輸入欄位](/help/rtcdp/destinations/assets/aws-kinesis-account-step.png)

### 在驗證步驟中 {#authentication-step}

* **名稱**: 提供您與 [!DNL Amazon Kinesis]
* **說明**: 提供您與的連線說明 [!DNL Amazon Kinesis]。
* **stream**: 提供帳戶中現有資料流的名 [!DNL Amazon Kinesis] 稱。 Adobe即時CDP會將資料匯出至此串流。

![驗證步驟中的輸入欄位](/help/rtcdp/destinations/assets/aws-kinesis-authentication-step.png)

<!--

>[!IMPORTANT]
>
>Adobe Real-time CDP needs `write` permissions on the bucket object where the export files will be delivered.

-->

## 啟用區段 {#activate-segments}

如需 [區段啟動工作流程的相關資訊](/help/rtcdp/destinations/activate-destinations.md) ，請參閱啟用設定檔和區段至目的地。

## 匯出的資料 {#exported-data}

您匯出的Experience Platform資料會以JSON [!DNL Amazon Kinesis] 格式登入。 例如，包含退出特定區段之對象之雜湊電子郵件身分的事件可能如下所示：

```
{
   "segmentMembership":{
      "ups":{
         "7841ba61-23c1-4bb3-a495-00d695fe1e93":{
            "lastQualificationTime":"2020-03-03T21:24:39Z",
            "status":"exited"
         }
      }
   }
},
"identityMap":{
   "email_lc_sha256":[
      {
         "id":"655332b5fa2aea4498bf7a290cff017cb4"
      },
      {
         "id":"66baf76ef9de8b42df8903f00e0e3dc0b7"
      }
   ]
},
```



>[!MORELIKETHIS]
>
>* 連結到Amazon Kinesis API教程
>* [Azure事件集線器目標](/help/rtcdp/destinations/azure-event-hubs-destination.md)
>* [目標類型和類別](/help/rtcdp/destinations/destination-types.md)

