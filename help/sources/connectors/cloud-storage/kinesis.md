---
keywords: Experience Platform；首頁；熱門主題；Amazon Kinesis;amazon kinesis;Kinesis;kinesis
solution: Experience Platform
title: Amazon Kinesis Source Connector概述
description: 了解如何使用API或使用者介面將Amazon Kinesis連線至Adobe Experience Platform。
exl-id: b71fc922-7722-4279-8fc6-e5d7735e1ebb
source-git-commit: 59dfa862388394a68630a7136dee8e8988d0368c
workflow-type: tm+mt
source-wordcount: '491'
ht-degree: 0%

---

# [!DNL Amazon Kinesis] 連接器

Adobe Experience Platform為AWS等雲端提供者提供原生連線， [!DNL Google Cloud Platform]，和 [!DNL Azure]. 您可以將資料從這些系統帶入 [!DNL Platform].

雲端儲存來源可將您自己的資料帶入 [!DNL Platform] 而無須下載、格式化或上傳。 擷取的資料可格式化為XDM JSON、XDM Parquet或分隔字元。 流程的每個步驟都整合至來源工作流程中。 [!DNL Platform] 可讓您將資料 [!DNL Amazon Kinesis] 即時。

>[!NOTE]
>
>的比例因子 [!DNL Kinesis] 必須增加，才能內嵌大量資料。 目前，您可從 [!DNL Kinesis] 帳戶對Platform的影響是每秒4000條記錄。 若要放大並擷取較多數量的資料，請聯絡您的Adobe代表。

## 先決條件

以下章節提供建立之前所需先決條件設定的詳細資訊 [!DNL Kinesis] 源連接。

### 設定訪問策略

A [!DNL Kinesis] stream需要下列權限才能建立來源連線：

- `GetShardIterator`
- `GetRecords`
- `DescribeStream`
- `ListStreams`

這些權限會透過 [!DNL Kinesis] 輸入憑證並選取資料流後，Platform會核取主控台和。

以下範例顯示建立 [!DNL Kinesis] 源連接。

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

有關控制訪問的詳細資訊 [!DNL Kinesis] 資料流，請參閱下列 [[!DNL Kinesis] 檔案](https://docs.aws.amazon.com/streams/latest/dev/controlling-access.html).

### 配置迭代器類型

[!DNL Kinesis] 支援下列迭代器類型，以便指定資料讀取的順序：

| 迭代器類型 | 說明 |
| ------------- | ----------- |
| `AT_SEQUENCE_NUMBER` | 從由特定序號標識的位置開始讀取資料。 |
| `AFTER_SEQUENCE_NUMBER` | 從由特定序列號標識的位置開始讀取資料。 |
| `AT_TIMESTAMP` | 從由特定時間戳記識別的位置開始讀取資料。 |
| `TRIM_HORIZON` | 從最舊的資料記錄開始讀取資料。 |
| `LATEST` | 從最新資料記錄開始讀取資料。 |

A [!DNL Kinesis] UI來源目前僅支援 `TRIM_HORIZON`，而API支援兩者 `TRIM_HORIZON` 和 `LATEST` 作為取得資料的模式。 Platform用於 [!DNL Kinesis] 來源為 `TRIM_HORIZON`.

有關迭代器類型的詳細資訊，請參閱以下內容 [[!DNL Kinesis] 檔案](https://docs.aws.amazon.com/kinesis/latest/APIReference/API_GetShardIterator.html#API_GetShardIterator_RequestSyntax).

## Connect [!DNL Amazon Kinesis] to [!DNL Platform]

以下檔案提供如何連線的資訊 [!DNL Amazon Kinesis] to [!DNL Platform] 使用API或使用者介面：

### 使用API

- [使用流量服務API建立Amazon Kinesis來源連線](../../tutorials/api/create/cloud-storage/kinesis.md)
- [使用流量服務API收集串流資料](../../tutorials/api/collect/streaming.md)

### 使用UI

- [在UI中建立Amazon Kinesis來源連線](../../tutorials/ui/create/cloud-storage/kinesis.md)
- [在UI中為雲儲存連接配置資料流](../../tutorials/ui/dataflow/streaming/cloud-storage-streaming.md)
