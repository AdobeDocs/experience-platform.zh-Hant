---
keywords: Experience Platform；首頁；熱門主題；AmazonKinesis;amazon kinesis;Kinesis;kinesis
solution: Experience Platform
title: AmazonKinesis源連接器概述
topic-legacy: overview
description: 瞭解如何使用API或使用者介面將AmazonKinesis與Adobe Experience Platform連線。
exl-id: b71fc922-7722-4279-8fc6-e5d7735e1ebb
translation-type: tm+mt
source-git-commit: af11bc966889be54fc27e02f3eee321519cef88f
workflow-type: tm+mt
source-wordcount: '497'
ht-degree: 0%

---

# [!DNL Amazon Kinesis] 連接器

Adobe Experience Platform為AWS、[!DNL Google Cloud Platform]和[!DNL Azure]等雲提供商提供本機連接。 您可以將這些系統中的資料導入[!DNL Platform]。

雲端儲存來源可將您自己的資料匯入[!DNL Platform]，而不需下載、格式化或上傳。 收錄的資料可格式化為XDM JSON、XDM Parce或分隔。 此程式的每個步驟都會整合至Sources工作流程中。 [!DNL Platform] 可讓您即時從資料 [!DNL Amazon Kinesis] 中匯入。

## IP位址允許清單

在使用來源連接器之前，必須將IP位址清單新增至允許清單。 若未將您地區專屬的IP位址新增至您的允許清單，在使用來源時可能會導致錯誤或效能不佳。 如需詳細資訊，請參閱[IP位址允許清單](../../ip-address-allow-list.md)頁面。

## 先決條件

以下部分提供了在建立[!DNL Kinesis]源連接之前所需設定先決條件的詳細資訊。

### 設定訪問策略

[!DNL Kinesis]串流需要下列權限才能建立來源連線：

- `GetShardIterator`
- `GetRecords`
- `DescribeStream`
- `ListStreams`

這些權限會透過[!DNL Kinesis]主控台排列，在您輸入認證並選取資料流後，平台會加以檢查。

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
| `kinesis:GetRecords` | 從特定偏移或分片ID取得記錄所需的動作。 |
| `kinesis:DescribeStream` | 一種動作，可傳回有關串流的資訊，包括分片地圖，產生分片ID時需要此動作。 |
| `kinesis:ListStreams` | 列出可從UI中選取的可用串流所需的動作。 |

有關控制[!DNL Kinesis]資料流訪問的詳細資訊，請參見以下[[!DNL Kinesis] 文檔](https://docs.aws.amazon.com/streams/latest/dev/controlling-access.html)。

### 配置迭代器類型

[!DNL Kinesis] 支援以下迭代器類型，允許您指定資料的讀取順序：

| 迭代器類型 | 說明 |
| ------------- | ----------- |
| `AT_SEQUENCE_NUMBER` | 從由特定序列號標識的位置開始讀取資料。 |
| `AFTER_SEQUENCE_NUMBER` | 在由特定序列號標識的位置之後讀取資料。 |
| `AT_TIMESTAMP` | 從由特定時間戳標識的位置開始讀取資料。 |
| `TRIM_HORIZON` | 從最舊的資料記錄開始讀取資料。 |
| `LATEST` | 從最近的資料記錄開始讀取資料。 |

[!DNL Kinesis] UI來源目前僅支援`TRIM_HORIZON`，而API支援`TRIM_HORIZON`和`LATEST`兩種模式，以取得資料。 Platform用於[!DNL Kinesis]源的預設迭代器值為`TRIM_HORIZON`。

有關迭代器類型的詳細資訊，請參見以下[[!DNL Kinesis] document](https://docs.aws.amazon.com/kinesis/latest/APIReference/API_GetShardIterator.html#API_GetShardIterator_RequestSyntax)。

## 將[!DNL Amazon Kinesis]連接到[!DNL Platform]

下面的文檔提供了如何使用API或用戶介面將[!DNL Amazon Kinesis]連接到[!DNL Platform]的資訊：

### 使用API

- [使用Flow Service API建立AmazonKinesis來源連線](../../tutorials/api/create/cloud-storage/kinesis.md)
- [使用Flow Service API收集串流資料](../../tutorials/api/collect/streaming.md)

### 使用UI

- [在UI中建立AmazonKinesis源連接](../../tutorials/ui/create/cloud-storage/kinesis.md)
- [在UI中為雲端儲存區連線設定資料流](../../tutorials/ui/dataflow/streaming/cloud-storage-streaming.md)
