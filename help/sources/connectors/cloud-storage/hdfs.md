---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: HDFS連接器
topic: overview
translation-type: tm+mt
source-git-commit: 340f5d0611e9e9eb4676018ee10c8a8aa08dbb2d
workflow-type: tm+mt
source-wordcount: '186'
ht-degree: 0%

---


# (Beta) [!DNL Apache] HDFS連接器

>[!NOTE]
>Apache HDFS連接器正在測試中。 如需使用 [測試版標籤連接器的詳細資訊](../../home.md#terms-and-conditions) ，請參閱來源概觀。

Adobe Experience Platform為AWS等雲端提供商提供原生連接 [!DNL Google Cloud Platform]功能 [!DNL Azure]，讓您能夠從這些系統中取得資料。 收錄的資料可格式化為JSON、鑲木地板或分隔字元。 雲端儲存空間供應商的支援包括 [!DNL Apache] HDFS。

## IP位址允許清單

在使用源連接器之前，必須將下列IP位址新增至允許清單。 若未將您地區專屬的IP位址新增至您的允許清單，在使用來源時可能會導致錯誤或效能不佳。

### 美國東部地區

- `20.41.2.0/23`
- `20.41.4.0/26`
- `20.44.17.80/28`
- `20.49.102.16/29`
- `40.70.148.160/28`
- `52.167.107.224/28`

### 西歐地區

- `13.69.67.192/28`
- `13.69.107.112/28`
- `13.69.112.128/28`
- `40.74.24.192/26`
- `40.74.26.0/23`
- `40.113.176.232/29`
- `52.236.187.112/28`

### 澳洲東部

- `13.70.74.144/28`
- `20.37.193.0/25`
- `20.37.193.128/26`
- `20.37.198.224/29`
- `40.79.163.80/28`
- `40.79.171.160/28`

以下檔案提供如何將 [!DNL Apache] HDFS連接至API或使 [!DNL Platform] 用者介面的資訊：

## 將 [!DNL Apache] HDFS連線至 [!DNL Platform] 使用API

- [使用Flow Service API建立HDFS連接器](../../tutorials/api/create/cloud-storage/hdfs.md)
- [使用Flow Service API探索雲端儲存系統](../../tutorials/api/explore/cloud-storage.md)
- [使用Flow Service API收集雲端儲存空間資料](../../tutorials/api/collect/cloud-storage.md)

## 將 [!DNL Apache] HDFS連 [!DNL Platform] 接至使用UI

- [在UI中建立Apache HDFS來源連接器](../../tutorials/ui/create/cloud-storage/hdfs.md)
- [在UI中為雲端儲存連接器設定資料流](../../tutorials/ui/dataflow/batch/cloud-storage.md)