---
keywords: Experience Platform;profile;real-time customer profile;troubleshooting;API
solution: Adobe Experience Platform
title: 新增資料至即時客戶個人檔案
topic: tutorial
translation-type: tm+mt
source-git-commit: 6d24637dc6cc282f98288b6416e4a3b7cebe42ea

---


# 新增資料至即時客戶個人檔案

本教學課程概述將資料新增至即時客戶個人檔案的必要步驟。

## 啟用即時客戶個人檔案的結構

即時客戶個人檔案所吸收的資料，必須符合為個人檔案啟用的體驗資料模型(XDM)架構。 為了啟用配置式架構，它必須實作XDM個別配置式或XDM ExperienceEvent類。

您可以使用方案註冊表API或方案編輯器用戶介面啟用方案以用於即時客戶概要檔案。 若要開始，請依照教學課程， [使用API建立架構](../../xdm/tutorials/create-schema-api.md) ，或 [使用架構編輯器UI建立架構](../../xdm/tutorials/create-schema-ui.md)。

## 使用批次擷取新增資料

使用批次擷取上傳至平台的所有資料都會上傳至個別資料集。 在即時客戶設定檔可使用此資料之前，必須特別設定相關資料集。 如需完整指示，請參閱設定描述 [檔和身分服務資料集的教學課程](dataset-configuration.md)。

設定資料集後，您就可以開始將資料擷取至資料集。 請參閱批次 [擷取開發人員指南](../../ingestion/batch-ingestion/api-overview.md) ，以取得如何上傳不同格式檔案的詳細步驟。

## 使用串流擷取功能新增資料

任何符合啟用描述檔的XDM架構的串流內嵌資料，都會自動新增或覆寫即時客戶描述檔中的適當記錄。 如果記錄中提供了多個身份，或使用了時間序列資料，則這些身份將在身份圖中映射，而不需要額外配置。 請參閱串流 [擷取開發人員指南](../../ingestion/tutorials/streaming-record-data.md) ，瞭解更多資訊。

## 確認上傳成功

第一次上傳資料至新資料集，或是作為新ETL或資料來源相關程式的一部分，建議您仔細檢查資料，以確保資料已正確上傳。

使用即時客戶描述檔存取API，您可以在批次資料載入資料集時擷取批次資料。 如果您無法擷取任何預期的實體，您的資料集可能無法啟用描述檔。 確認資料集已啟用後，請確定您的來源資料格式和識別碼支援您的期望。

有關如何使用即時客戶描述檔API存取實體的詳細說明，請參閱「實體」的 [子指南，亦稱為「描述檔存取API」](../api/entities.md)。