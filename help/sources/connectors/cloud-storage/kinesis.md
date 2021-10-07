---
keywords: Experience Platform；首頁；熱門主題；Amazon Kinesis;amazon kinesis;Kinesis;kinesis
solution: Experience Platform
title: Amazon Kinesis Source Connector概述
topic-legacy: overview
description: 了解如何使用API或使用者介面將Amazon Kinesis連線至Adobe Experience Platform。
exl-id: b71fc922-7722-4279-8fc6-e5d7735e1ebb
source-git-commit: 481f72c5c630f6dbcbbfd3eee11c91787e780f3f
workflow-type: tm+mt
source-wordcount: '445'
ht-degree: 0%

---

# [!DNL Amazon Kinesis] 連接器

Adobe Experience Platform為AWS、[!DNL Google Cloud Platform]和[!DNL Azure]等雲端提供者提供原生連線。 您可以將資料從這些系統帶入[!DNL Platform]。

雲端儲存來源可將您自己的資料帶入[!DNL Platform]，而無需下載、格式化或上傳。 擷取的資料可格式化為XDM JSON、XDM Parquet或分隔字元。 流程的每個步驟都整合至來源工作流程中。 [!DNL Platform] 可讓您即時從匯 [!DNL Amazon Kinesis] 入資料。

## 先決條件

以下部分提供了建立[!DNL Kinesis]源連接前所需的先決條件設定的詳細資訊。

### 設定訪問策略

[!DNL Kinesis]資料流需要以下權限才能建立源連接：

- `GetShardIterator`
- `GetRecords`
- `DescribeStream`
- `ListStreams`

這些權限會透過[!DNL Kinesis]主控台排列，當您輸入憑證並選取資料流時，Platform會加以檢查。

下面的示例顯示建立[!DNL Kinesis]源連接所需的最低訪問權限。

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
| `kinesis:GetShardIterator` | 遍歷記錄所需的操作。 |
| `kinesis:GetRecords` | 從特定偏移或共用ID取得記錄所需的動作。 |
| `kinesis:DescribeStream` | 傳回關於資料流（包括共用地圖）的資訊的動作，這是產生共用ID所需的。 |
| `kinesis:ListStreams` | 列出可用資料流（您可從UI中選取）所需的動作。 |

有關控制[!DNL Kinesis]資料流訪問的詳細資訊，請參閱以下[[!DNL Kinesis] document](https://docs.aws.amazon.com/streams/latest/dev/controlling-access.html)。

### 配置迭代器類型

[!DNL Kinesis] 支援下列迭代器類型，以便指定資料讀取的順序：

| 迭代器類型 | 說明 |
| ------------- | ----------- |
| `AT_SEQUENCE_NUMBER` | 從由特定序號標識的位置開始讀取資料。 |
| `AFTER_SEQUENCE_NUMBER` | 從由特定序列號標識的位置開始讀取資料。 |
| `AT_TIMESTAMP` | 從由特定時間戳記識別的位置開始讀取資料。 |
| `TRIM_HORIZON` | 從最舊的資料記錄開始讀取資料。 |
| `LATEST` | 從最新資料記錄開始讀取資料。 |

[!DNL Kinesis] UI來源目前僅支援`TRIM_HORIZON`，而API同時支援`TRIM_HORIZON`和`LATEST`作為取得資料的模式。 Platform用於[!DNL Kinesis]源的預設迭代器值為`TRIM_HORIZON`。

有關迭代器類型的詳細資訊，請參閱以下[[!DNL Kinesis] document](https://docs.aws.amazon.com/kinesis/latest/APIReference/API_GetShardIterator.html#API_GetShardIterator_RequestSyntax)。

## 將[!DNL Amazon Kinesis]連接到[!DNL Platform]

以下檔案提供如何使用API或使用者介面將[!DNL Amazon Kinesis]連線至[!DNL Platform]的資訊：

### 使用API

- [使用流量服務API建立Amazon Kinesis來源連線](../../tutorials/api/create/cloud-storage/kinesis.md)
- [使用流量服務API收集串流資料](../../tutorials/api/collect/streaming.md)

### 使用UI

- [在UI中建立Amazon Kinesis來源連線](../../tutorials/ui/create/cloud-storage/kinesis.md)
- [在UI中為雲儲存連接配置資料流](../../tutorials/ui/dataflow/streaming/cloud-storage-streaming.md)
