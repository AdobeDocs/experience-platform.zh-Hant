---
title: Amazon Kinesis Source聯結器總覽
description: 瞭解如何使用API或使用者介面將Amazon Kinesis連線至Adobe Experience Platform。
badgeUltimate: label="Ultimate" type="Positive"
exl-id: b71fc922-7722-4279-8fc6-e5d7735e1ebb
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '532'
ht-degree: 0%

---

# [!DNL Amazon Kinesis]來源

>[!IMPORTANT]
>
>- [!DNL Amazon Kinesis]來源可在來源目錄中提供給已購買Real-Time CDP Ultimate的使用者。
>
>- 您現在可以在Amazon Web Services (AWS)上執行Adobe Experience Platform時使用[!DNL Amazon Kinesis]來源。 目前有限數量的客戶可使用在AWS上執行的Experience Platform 。 若要進一步瞭解支援的Experience Platform基礎結構，請參閱[Experience Platform多雲端總覽](../../../landing/multi-cloud.md)。


Adobe Experience Platform為AWS、[!DNL Google Cloud Platform]和[!DNL Azure]等雲端提供者提供原生連線。 您可以將資料從這些系統帶入[!DNL Experience Platform]。

雲端儲存空間來源可以將您自己的資料帶入[!DNL Experience Platform]，而不需要下載、格式化或上傳。 內嵌的資料可以格式化為XDM JSON、XDM Parquet或分隔。 流程的每個步驟都會整合至來源工作流程。 [!DNL Experience Platform]可讓您即時從[!DNL Amazon Kinesis]匯入資料。

>[!NOTE]
>
>如果您需要擷取大量資料，必須增加[!DNL Kinesis]的縮放因數。 目前，您可以從[!DNL Kinesis]帳戶帶入Experience Platform的最大資料量為每秒4000筆記錄。 若要擴充並擷取較大量的資料，請聯絡您的Adobe代表。

## 先決條件

下節提供建立[!DNL Kinesis]來源連線之前所需先決條件設定的進一步資訊。

### 設定存取原則

[!DNL Kinesis]資料流需要下列許可權才能建立來源連線：

- `GetShardIterator`
- `GetRecords`
- `DescribeStream`
- `ListStreams`

這些許可權會透過[!DNL Kinesis]主控台進行排列，並在您輸入認證及選取資料流後，由Experience Platform檢查。

下列範例顯示建立[!DNL Kinesis]來源連線所需的最低存取許可權。

```json
{
    "Version": "2012-10-17",
    "Statement": [
        {
            "Effect": "Allow",
            "Action": [
                "kinesis:GetShardIterator",
                "kinesis:GetRecords",
                "kinesis:DescribeStream",
                "kinesis:ListStreams"
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
| `kinesis:GetShardIterator` | 需要透過記錄執行的動作。 |
| `kinesis:GetRecords` | 從特定位移或分片ID取得記錄所需的動作。 |
| `kinesis:DescribeStream` | 此動作會傳回有關串流的資訊，包括產生分片ID所需的分片對應。 |
| `kinesis:ListStreams` | 列出可從UI選取的可用串流所需的動作。 |

如需控制[!DNL Kinesis]資料串流存取權的詳細資訊，請參閱下列[[!DNL Kinesis] 檔案](https://docs.aws.amazon.com/streams/latest/dev/controlling-access.html)。

### 設定疊代器型別

[!DNL Kinesis]支援下列疊代器型別，可讓您指定讀取資料的順序：

| 迭代器型別 | 說明 |
| ------------- | ----------- |
| `AT_SEQUENCE_NUMBER` | 從由特定序號識別的位置開始讀取資料。 |
| `AFTER_SEQUENCE_NUMBER` | 從特定序號所識別的位置之後，開始讀取資料。 |
| `AT_TIMESTAMP` | 從由特定時間戳記所識別的位置開始讀取資料。 |
| `TRIM_HORIZON` | 從最舊的資料記錄開始讀取資料。 |
| `LATEST` | 從最近的資料記錄開始讀取資料。 |

[!DNL Kinesis] UI來源目前僅支援`TRIM_HORIZON`，而API同時支援`TRIM_HORIZON`和`LATEST`作為取得資料的模式。 Experience Platform用於[!DNL Kinesis]來源的預設疊代器值為`TRIM_HORIZON`。

如需疊代器型別的詳細資訊，請參閱下列[[!DNL Kinesis] 檔案](https://docs.aws.amazon.com/kinesis/latest/APIReference/API_GetShardIterator.html#API_GetShardIterator_RequestSyntax)。

## 將[!DNL Amazon Kinesis]連線至[!DNL Experience Platform]

以下檔案提供如何使用API或使用者介面將[!DNL Amazon Kinesis]連線到[!DNL Experience Platform]的資訊：

### 使用API

- [使用流量服務API建立Amazon Kinesis來源連線](../../tutorials/api/create/cloud-storage/kinesis.md)
- [使用流量服務API收集串流資料](../../tutorials/api/collect/streaming.md)

### 使用UI

- [在UI中建立Amazon Kinesis來源連線](../../tutorials/ui/create/cloud-storage/kinesis.md)
- [在UI中為雲端儲存空間連線設定資料流](../../tutorials/ui/dataflow/streaming/cloud-storage-streaming.md)
