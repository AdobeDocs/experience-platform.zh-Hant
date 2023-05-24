---
description: 要使用Destination SDK，合作夥伴公司必須滿足本文檔中列出的先決條件。
title: 整合先決條件
exl-id: 031af9f1-ce18-4056-bd53-199ce8b56be5
source-git-commit: 118ff85a9fceb8ee81dbafe2c381d365b813da29
workflow-type: tm+mt
source-wordcount: '198'
ht-degree: 0%

---

# 整合先決條件

要使用Destination SDK，請確保滿足以下各節中列出的技術和合作夥伴關係先決條件。

## 流目標的技術/API先決條件 {#streaming-prerequisites}

1. 您擁有Adobe Experience Platform的REST API終結點，可將以下類型的資料傳送到：
   * 會員資訊；
   * 配置式身份資訊；
   * （可選）配置檔案豐富的附加屬性。
2. 您的REST API終結點支援基本、承載令牌或OAuth 2.0身份驗證協定。
3. （可選）您具有用於寫程式元資料管理的段建立/更新/刪除API或API終結點。

## 批目標的技術先決條件 {#batch-prerequisites}

1. 您的目標位置托管在 [!DNL Amazon S3]。 [!DNL Azure Blob]。 [!DNL Azure Data Lake Storage]。 [!DNL SFTP]。 [!DNL Google Cloud]，或私有 [!DNL Data Landing Zone]中，您可以接收導出的檔案，而不是Experience Platform。
2. 目標平台可以以通過 [檔案格式選項](functionality/destination-server/file-formatting.md) Destination SDK。
3. （可選）您有段建立/檢索/更新/刪除([!DNL CRUD])API或API終結點，用於寫程式元資料管理。

## 夥伴關係先決條件 {#partnership-prerequisites}

如果您是希望使用Destination SDK的獨立軟體供應商(ISV)或系統整合商(SI)，請閱讀中的ISV和SI的合作夥伴要求 [獲取訪問部分](overview.md#get-access)。
