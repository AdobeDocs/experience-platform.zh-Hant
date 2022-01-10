---
keywords: Amazon Kinesis;kinesis目的地；kinesis
title: Amazon Kinesis連線
description: 建立與Amazon Kinesis儲存體的即時傳出連線，以串流來自Adobe Experience Platform的資料。
exl-id: b40117ef-6ad0-48a9-bbcb-97c6f6d1dce3
source-git-commit: ba338972be13c7afa6720bba3f0fc96d244b8f9f
workflow-type: tm+mt
source-wordcount: '835'
ht-degree: 1%

---

# （測試版） [!DNL Amazon Kinesis] 連接

## 總覽 {#overview}

>[!IMPORTANT]
>
>此 [!DNL Amazon Kinesis] Platform中的目的地目前為測試版。 文件和功能可能會有所變更。

此 [!DNL Kinesis Data Streams] 服務依據 [!DNL Amazon Web Services] 可讓您即時收集和處理大量資料記錄。

您可以建立與 [!DNL Amazon Kinesis] 儲存以從Adobe Experience Platform串流資料。

* 如需 [!DNL Amazon Kinesis]，請參閱 [Amazon檔案](https://docs.aws.amazon.com/streams/latest/dev/introduction.html).
* 連線至 [!DNL Amazon Kinesis] 以程式設計方式，請參閱 [串流目的地API教學課程](../../api/streaming-destinations.md).
* 連線至 [!DNL Amazon Kinesis] 使用Platform使用者介面，請參閱以下各節。

![Amazon Kinesis在UI中](../../assets/catalog/cloud-storage/amazon-kinesis/catalog.png)

## 使用案例 {#use-cases}

使用串流目的地，例如 [!DNL Amazon Kinesis]，您可以輕鬆將高價值細分事件和相關設定檔屬性饋送至您所選擇的系統。

例如，潛在客戶下載了白皮書，將其歸類為「高傾向轉換」區段。 通過映射潛在客戶所在的段 [!DNL Amazon Kinesis] 目的地，您會在 [!DNL Amazon Kinesis]. 在那裡，您可以採用自己動手做的方法，在活動之上描述業務邏輯，因為您認為最適合您的企業IT系統。

## 匯出類型 {#export-type}

**設定檔**  — 您要匯出區段的所有成員，以及所需的架構欄位(例如：電子郵件地址、電話號碼、姓氏)，如「選取屬性」畫面中所選 [對象啟用工作流程](../../ui/activate-streaming-profile-destinations.md#select-attributes).

## 必填 [!DNL Amazon Kinesis] 權限 {#required-kinesis-permission}

若要成功連線並將資料匯出至 [!DNL Amazon Kinesis] 串流，Experience Platform需要下列動作的權限：

* `kinesis:ListStreams`
* `kinesis:PutRecord`
* `kinesis:PutRecords`

這些權限會透過 [!DNL Kinesis] 在Platform使用者介面中設定Kinesis目的地後，Platform會檢查主控台和。

以下範例顯示成功將資料匯出至 [!DNL Kinesis] 目的地。

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

有關控制訪問的詳細資訊 [!DNL Kinesis] 資料流，請讀取以下內容 [[!DNL Kinesis] 檔案](https://docs.aws.amazon.com/streams/latest/dev/controlling-access.html).

## 連接到目標 {#connect}

若要連線至此目的地，請依照 [目的地設定教學課程](../../ui/connect-destination.md).

### 連線參數 {#parameters}

同時 [設定](../../ui/connect-destination.md) 此目的地時，您必須提供下列資訊：

* **[!DNL Amazon Web Services]訪問密鑰和密鑰**:在 [!DNL Amazon Web Services]，產生 `access key - secret access key` 配對，以授與 [!DNL Amazon Kinesis] 帳戶。 了解更多 [Amazon Web Services檔案](https://docs.aws.amazon.com/IAM/latest/UserGuide/id_credentials_access-keys.html).
* **地區**:指出 [!DNL Amazon Web Services] 資料流到的區域。
* **名稱**:提供連線的名稱 [!DNL Amazon Kinesis]
* **說明**:提供與 [!DNL Amazon Kinesis].
* **流**:提供您 [!DNL Amazon Kinesis] 帳戶。 Platform會將資料匯出至此資料流。

<!--

>[!IMPORTANT]
>
>Platform needs `write` permissions on the bucket object where the export files will be delivered.

-->

## 啟用此目的地的區段 {#activate}

請參閱 [對串流設定檔匯出目的地啟用受眾資料](../../ui/activate-streaming-profile-destinations.md) 以取得啟用受眾區段至此目的地的指示。

## 設定檔匯出行為 {#profile-export-behavior}

Experience Platform會最佳化設定檔匯出行為至您的Amazon Kinesis目的地，以僅在符合區段資格或其他重大事件後發生設定檔的相關更新時，將資料匯出至您的目的地。 設定檔會在下列情況下匯出至您的目的地：

* 至少有一個區段對應至目的地，區段成員資格有所變更，便觸發設定檔更新。 例如，設定檔已符合對應至目的地的其中一個區段資格，或已退出對應至目的地的其中一個區段。
* 設定檔更新是由 [身分圖](/help/xdm/field-groups/profile/identitymap.md). 例如，已符合其中一個對應至目的地區段資格的設定檔，已在「身分對應」屬性中新增身分識別。
* 設定檔更新是由至少一個已對應至目的地之屬性的屬性變更所觸發。 例如，對應步驟中對應至目的地的其中一個屬性會新增至設定檔。

在上述所有情況中，只有發生相關更新的設定檔會匯出至您的目的地。 例如，如果對應至目的地流程的區段有100個成員，且有5個新設定檔符合該區段的資格，則匯出至目的地的作業會是增量的，且僅包含5個新設定檔。

請注意，無論變更在何處，所有對應屬性都會針對設定檔匯出。 因此，在上述範例中，即使屬性本身未變更，這五個新設定檔的所有對應屬性也會匯出。

## 匯出的資料 {#exported-data}

已導出 [!DNL Experience Platform] 資料登陸 [!DNL Amazon Kinesis] 格式。 例如，下列匯出包含符合特定區段資格且已退出另一個區段的設定檔，並包含設定檔屬性名、姓氏、出生日期和個人電子郵件地址。 此設定檔的身分為ECID和電子郵件。

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



>[!MORELIKETHIS]
>
>* [連線至Amazon Kinesis並使用流量服務API啟用資料](../../api/streaming-destinations.md)
>* [Azure事件中心目標](./azure-event-hubs.md)
>* [目的地類型和類別](../../destination-types.md)

