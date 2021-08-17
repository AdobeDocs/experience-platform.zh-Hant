---
keywords: Amazon Kinesis;kinesis目的地；kinesis
title: Amazon Kinesis連線
description: 建立與Amazon Kinesis儲存體的即時傳出連線，以串流來自Adobe Experience Platform的資料。
exl-id: b40117ef-6ad0-48a9-bbcb-97c6f6d1dce3
source-git-commit: 3aac1e7c7fe838201368379da8504efc8e316e1c
workflow-type: tm+mt
source-wordcount: '552'
ht-degree: 2%

---

# (Beta)[!DNL Amazon Kinesis]連接

## 概覽 {#overview}

>[!IMPORTANT]
>
>Platform中的[!DNL Amazon Kinesis]目標目前為測試版。 文件和功能可能會有所變更。

[!DNL Amazon Web Services]提供的[!DNL Kinesis Data Streams]服務允許您即時收集和處理大資料記錄流。

您可以建立與[!DNL Amazon Kinesis]儲存的即時傳出連線，以便串流來自Adobe Experience Platform的資料。

* 如需[!DNL Amazon Kinesis]的詳細資訊，請參閱[Amazon檔案](https://docs.aws.amazon.com/streams/latest/dev/introduction.html)。
* 若要以程式設計方式連線至[!DNL Amazon Kinesis]，請參閱[串流目的地API教學課程](../../api/streaming-destinations.md)。
* 若要使用Platform使用者介面連線至[!DNL Amazon Kinesis]，請參閱以下各節。

![Amazon Kinesis在UI中](../../assets/catalog/cloud-storage/amazon-kinesis/catalog.png)

## 使用案例 {#use-cases}

透過使用[!DNL Amazon Kinesis]等串流目的地，您可以輕鬆將高價值分段事件和相關設定檔屬性饋送至您所選擇的系統。

例如，潛在客戶下載了白皮書，將其歸類為「高傾向轉換」區段。 將潛在客戶所屬的區段對應至[!DNL Amazon Kinesis]目的地後，您會在[!DNL Amazon Kinesis]中收到此事件。 在那裡，您可以採用自己動手做的方法，在活動之上描述業務邏輯，因為您認為最適合您的企業IT系統。

## 匯出類型 {#export-type}

**以設定檔為基礎**  — 您要匯出區段的所有成員，以及所需的結構欄位(例如：電子郵件地址、電話號碼、姓氏)，從對象啟用工作流程的「選取屬性」畫面 [中選取](../../ui/activate-streaming-profile-destinations.md#select-attributes)。

## 必要的[!DNL Amazon Kinesis]權限 {#required-kinesis-permission}

若要成功將資料連線並匯出至[!DNL Amazon Kinesis]資料流，Experience Platform需要下列動作的權限：

* `kinesis:ListStreams`
* `kinesis:PutRecord`
* `kinesis:PutRecords`

這些權限會透過[!DNL Kinesis]主控台排列，當您在Platform使用者介面中設定Kinesis目的地時，Platform就會加以檢查。

以下示例顯示成功將資料導出到[!DNL Kinesis]目標所需的最低訪問權限。

```json
{
    "Version": "2012-10-17",
    "Statement": [
        {
            "Effect": "Allow",
            "Action": [
                "kinesis:ListStreams",
                "kinesis:PutRecord",
                "kinesis:PutRecords"
            ],
            "Resource": [
                "arn:aws:kinesis:us-east-2:901341027596:stream/*"
            ]
        }
    ]
}
```

| 屬性 | 說明 |
| -------- | ----------- |
| `kinesis:ListStreams` | 列出Amazon Kinesis資料流的動作。 |
| `kinesis:PutRecord` | 將單一資料記錄寫入Kinesis資料流的動作。 |
| `kinesis:PutRecords` | 在單一呼叫中將多個資料記錄寫入Kinesis資料流的動作。 |

有關控制[!DNL Kinesis]資料流訪問的詳細資訊，請閱讀以下[[!DNL Kinesis] document](https://docs.aws.amazon.com/streams/latest/dev/controlling-access.html)。

## 連接到目標 {#connect}

要連接到此目標，請按照[目標配置教程](../../ui/connect-destination.md)中所述的步驟操作。

### 連線參數 {#parameters}

在[設定](../../ui/connect-destination.md)此目標時，您必須提供下列資訊：

* **[!DNL Amazon Web Services]存取金鑰和機密金鑰**:在中 [!DNL Amazon Web Services]產生一組 `access key - secret access key` 以授與Platform對您帳戶的存 [!DNL Amazon Kinesis] 取權。如需詳細資訊，請參閱[Amazon網站服務檔案](https://docs.aws.amazon.com/IAM/latest/UserGuide/id_credentials_access-keys.html)。
* **地區**:指定要 [!DNL Amazon Web Services] 將資料流到哪個區域。
* **名稱**:提供連線的名稱  [!DNL Amazon Kinesis]
* **說明**:提供與的連線說明 [!DNL Amazon Kinesis]。
* **資料流**:提供帳戶中現有資料流的名 [!DNL Amazon Kinesis] 稱。Platform會將資料匯出至此資料流。

<!--

>[!IMPORTANT]
>
>Platform needs `write` permissions on the bucket object where the export files will be delivered.

-->

## 啟用此目的地的區段 {#activate}

請參閱[將受眾資料啟用至串流設定檔匯出目的地](../../ui/activate-streaming-profile-destinations.md) ，以取得關於將受眾區段啟用至此目的地的指示。

## 匯出的資料 {#exported-data}

您匯出的[!DNL Experience Platform]資料會以JSON格式連結至[!DNL Amazon Kinesis]。 例如，以下事件包含已符合特定區段資格並退出其他區段之對象的電子郵件地址設定檔屬性。 此潛在客戶的身分識別為ECID和電子郵件。

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
>* [連線至Amazon Kinesis並使用流量服務API啟用資料](../../api/streaming-destinations.md)
* [Azure事件中心目標](./azure-event-hubs.md)
* [目的地類型和類別](../../destination-types.md)

