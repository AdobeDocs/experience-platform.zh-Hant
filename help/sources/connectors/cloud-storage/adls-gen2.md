---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Azure Data Lake Storage Gen2連接器
topic: overview
translation-type: tm+mt
source-git-commit: 4d3899e8a91d15da7e40523a03285f3ccec27191
workflow-type: tm+mt
source-wordcount: '202'
ht-degree: 0%

---


# Azure Data Lake Storage Gen2連接器

Adobe Experience Platform為AWS等雲端提供商提供原生連接 [!DNL Google Cloud Platform]功能 [!DNL Azure]，讓您能夠從這些系統中取得資料。

雲端儲存來源可將您自己的資料匯入 [!DNL Platform] 其中，而不需下載、格式化或上傳。 收錄的資料可格式化為XDM JSON、XDM鑲木地板或分隔字元。 此程式的每個步驟都會整合至Sources工作流程中。 [!DNL Platform] 允許您從(ADLS-Gen2)批 [!DNL Azure Data Lake Storage Gen2] 次導入資料。

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

## 連線 [!DNL Azure Data Lake Storage Gen2] 至 [!DNL Platform]

以下檔案提供如何連線至使用API [!DNL Azure Data Lake Storage Gen2] 或使 [!DNL Platform] 用者介面的資訊：

### 使用API

- [使用Flow Service API建立ADLS-Gen2連接器](../../tutorials/api/create/cloud-storage/adls-gen2.md)
- [使用Flow Service API探索雲端儲存系統](../../tutorials/api/explore/cloud-storage.md)
- [使用Flow Service API收集雲端儲存空間資料](../../tutorials/api/collect/cloud-storage.md)

## 使用UI

- [在UI中建立ADLS-Gen2來源連接器](../../tutorials/ui/create/cloud-storage/adls-gen2.md)
- [在UI中為雲端儲存連接器設定資料流](../../tutorials/ui/dataflow/batch/cloud-storage.md)