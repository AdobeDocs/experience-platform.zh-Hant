---
keywords: Experience Platform；首頁；熱門主題；AmazonKinesis；亞馬遜；Kinesis;kinesis
solution: Experience Platform
title: AmazonKinesis源連接器概述
description: 瞭解如何使用API或用戶介面將AmazonKinesis連接到Adobe Experience Platform。
exl-id: b71fc922-7722-4279-8fc6-e5d7735e1ebb
source-git-commit: 59dfa862388394a68630a7136dee8e8988d0368c
workflow-type: tm+mt
source-wordcount: '491'
ht-degree: 0%

---

# [!DNL Amazon Kinesis] 連接器

Adobe Experience Platform提供本地連接，如AWS, [!DNL Google Cloud Platform], [!DNL Azure]。 您可以將資料從這些系統中 [!DNL Platform]。

雲儲存源可以將您自己的資料 [!DNL Platform] 無需下載、格式化或上載。 所攝取的資料可以格式化為XDM JSON、XDM Parke或分隔。 流程的每個步驟都整合到「源」工作流中。 [!DNL Platform] 允許您從 [!DNL Amazon Kinesis] 即時。

>[!NOTE]
>
>比例因子 [!DNL Kinesis] 如果需要接收高容量資料，必須增加。 當前，您可以從 [!DNL Kinesis] 平台每秒有4000條記錄。 要擴展並接收更高的卷資料，請與Adobe代表聯繫。

## 先決條件

以下部分提供了在建立 [!DNL Kinesis] 源連接。

### 設定訪問策略

A [!DNL Kinesis] 流需要以下權限才能建立源連接：

- `GetShardIterator`
- `GetRecords`
- `DescribeStream`
- `ListStreams`

這些權限通過 [!DNL Kinesis] 控制台，在您輸入憑據並選擇資料流後，平台會檢查它。

下面的示例顯示建立 [!DNL Kinesis] 源連接。

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
| `kinesis:GetRecords` | 從特定偏移或分片ID獲取記錄所需的操作。 |
| `kinesis:DescribeStream` | 一個操作，它返回與包括分片映射的流有關的資訊，該資訊是生成分片ID所需的。 |
| `kinesis:ListStreams` | 列出可從UI中選擇的可用流所需的操作。 |

有關控制訪問的詳細資訊 [!DNL Kinesis] 資料流，請參閱以下 [[!DNL Kinesis] 文檔](https://docs.aws.amazon.com/streams/latest/dev/controlling-access.html)。

### 配置迭代器類型

[!DNL Kinesis] 支援以下迭代器類型，以允許您指定讀取資料的順序：

| 迭代器類型 | 說明 |
| ------------- | ----------- |
| `AT_SEQUENCE_NUMBER` | 從由特定序列號標識的位置開始讀取資料。 |
| `AFTER_SEQUENCE_NUMBER` | 在由特定序列號標識的位置之後讀取資料。 |
| `AT_TIMESTAMP` | 從由特定時間戳標識的位置開始讀取資料。 |
| `TRIM_HORIZON` | 從最舊的資料記錄開始讀取資料。 |
| `LATEST` | 從最近的資料記錄開始讀取資料。 |

A [!DNL Kinesis] 當前僅支援UI源 `TRIM_HORIZON`，而API同時支援 `TRIM_HORIZON` 和 `LATEST` 模式獲取資料。 平台用於的預設迭代器值 [!DNL Kinesis] 源 `TRIM_HORIZON`。

有關迭代器類型的詳細資訊，請參閱以下 [[!DNL Kinesis] 文檔](https://docs.aws.amazon.com/kinesis/latest/APIReference/API_GetShardIterator.html#API_GetShardIterator_RequestSyntax)。

## 連接 [!DNL Amazon Kinesis] 至 [!DNL Platform]

以下文檔提供了有關如何連接的資訊 [!DNL Amazon Kinesis] 至 [!DNL Platform] 使用API或用戶介面：

### 使用API

- [使用流服務API建立AmazonKinesis源連接](../../tutorials/api/create/cloud-storage/kinesis.md)
- [使用流服務API收集流資料](../../tutorials/api/collect/streaming.md)

### 使用UI

- [在UI中建立AmazonKinesis源連接](../../tutorials/ui/create/cloud-storage/kinesis.md)
- [在UI中為雲儲存連接配置資料流](../../tutorials/ui/dataflow/streaming/cloud-storage-streaming.md)
