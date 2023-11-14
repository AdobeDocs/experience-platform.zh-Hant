---
description: 若要使用Destination SDK，合作夥伴公司必須符合本檔案所列的先決條件。
title: 整合必要條件
exl-id: 031af9f1-ce18-4056-bd53-199ce8b56be5
source-git-commit: c1ba465a8a866bd8bdc9a2b294ec5d894db81e11
workflow-type: tm+mt
source-wordcount: '198'
ht-degree: 0%

---

# 整合必要條件

若要使用Destination SDK，請確定您符合下列各節所列的技術和合作關係先決條件。

## 串流目的地的技術/ API必要條件 {#streaming-prerequisites}

1. 您有Adobe Experience Platform的REST API端點，可將下列型別的資料傳送至：
   * 對象會籍資訊；
   * 設定檔身分資訊；
   * （選用）個人檔案擴充的其他屬性。
2. 您的REST API端點支援基本、持有人權杖或OAuth 2.0驗證通訊協定。
3. （選用）您有對象建立/更新/刪除API或API端點，用於程式化中繼資料管理。

## 批次目的地的技術先決條件 {#batch-prerequisites}

1. 您的目的地位置託管於 [!DNL Amazon S3]， [!DNL Azure Blob]， [!DNL Azure Data Lake Storage]， [!DNL SFTP]， [!DNL Google Cloud]或私人 [!DNL Data Landing Zone]，您可在此處接收轉存為不Experience Platform的檔案。
2. 您的目標平台可以透過設定的格式內嵌檔案 [檔案格式選項](functionality/destination-server/file-formatting.md) 批次目的地的Destination SDK。
3. （選用）您有對象建立/擷取/更新/刪除([!DNL CRUD])程式化中繼資料管理的API或API端點。

## 合作關係必要條件 {#partnership-prerequisites}

如果您是想要使用Destination SDK的獨立軟體廠商(ISV)或系統整合商(SI)，請閱讀 [取得存取許可權區段](overview.md#get-access).
