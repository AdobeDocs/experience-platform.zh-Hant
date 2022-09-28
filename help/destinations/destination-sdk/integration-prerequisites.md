---
description: 若要使用Destination SDK，合作夥伴公司必須符合本檔案所列的必要條件。
title: 整合必要條件
exl-id: 031af9f1-ce18-4056-bd53-199ce8b56be5
source-git-commit: d7c9623619e989a59d72aba74903ffc0e64e7d3c
workflow-type: tm+mt
source-wordcount: '0'
ht-degree: 0%

---

# 整合必要條件

若要使用Destination SDK，請確定您符合以下各節所列的技術和合作夥伴必要條件。

## 串流目的地的技術/ API必要條件 {#streaming-prerequisites}

1. 您有適用於Adobe Experience Platform的REST API端點，可將下列類型的資料傳送至：
   * 區段成員資格資訊；
   * 配置檔案身份資訊；
   * （選用）擴充設定檔的其他屬性。
2. 您的REST API端點支援API權杖承載驗證或OAuth 2.0驗證通訊協定。
3. （選用）您有區段建立/更新/刪除API或API端點，以便程式化中繼資料管理。

## 批次目的地的技術必要條件 {#batch-prerequisites}

1. 您有托管於的目的地位置 [!DNL Amazon S3], [!DNL Azure Blob], [!DNL Azure Data Lake Storage]、SFTP、 [!DNL Google Cloud]，或私人 [!DNL Data Landing Zone]，您可在此接收匯出的檔案。
2. 您的目的地平台可以內嵌透過 [檔案格式選項](/help/destinations/destination-sdk/server-and-file-configuration.md#file-configuration) Destination SDK。
3. （選用）您有區段建立/擷取/更新/刪除(CRUD)API或API端點，以管理程式化中繼資料。

## 合作夥伴先決條件 {#partnership-prerequisites}

如果您是希望使用Destination SDK的獨立軟體供應商(ISV)或系統整合商(SI)，請閱讀 [取得存取區段](./overview.md#get-access).
