---
keywords: Experience Platform;profile;real-time customer profile;troubleshooting;API;enable profile;Enable profile
solution: Adobe Experience Platform
title: 新增資料至即時客戶個人檔案
topic: tutorial
description: 本教學課程概述將資料新增至即時客戶個人檔案的必要步驟。
translation-type: tm+mt
source-git-commit: bf99b08a1093a815687cc06372407949e170a0b3
workflow-type: tm+mt
source-wordcount: '368'
ht-degree: 0%

---


# 新增資料至 [!DNL Real-time Customer Profile]

本教學課程概述將資料新增至的必要步驟 [!DNL Real-time Customer Profile]。

## 為 [!DNL Real-time Customer Profile]

要被吸收到供 [!DNL Experience Platform] 使用的數 [!DNL Real-time Customer Profile] 據必須符合為 [!DNL Experience Data Model] 啟用的(XDM)模式 [!DNL Profile]。 要啟用配置檔案的架構，它必須實施或 [!DNL XDM Individual Profile] 類 [!DNL XDM ExperienceEvent] 別。

您可以啟用結構，以便 [!DNL Real-time Customer Profile] 使用 [!DNL Schema Registry] API或使 [!DNL Schema Editor] 用者介面。 若要開始，請依照教學課程， [使用API建立架構](../../xdm/tutorials/create-schema-api.md) ，或 [使用架構編輯器UI建立架構](../../xdm/tutorials/create-schema-ui.md)。

## 使用批次擷取新增資料

使用批次擷取上傳 [!DNL Platform] 到的所有資料都會上傳到個別的資料集。 在此資料可供使用之 [!DNL Real-time Customer Profile]前，必須特別設定相關資料集。 如需完整指示，請參閱設定描述 [檔和身分服務資料集的教學課程](dataset-configuration.md)。

設定資料集後，您就可以開始將資料擷取至資料集。 請參閱批次 [擷取開發人員指南](../../ingestion/batch-ingestion/api-overview.md) ，以取得如何上傳不同格式檔案的詳細步驟。

## 使用串流擷取功能新增資料

任何與啟用的XDM架構相容的串 [!DNL Profile]流收錄資料，都會自動新增或覆寫中的適當記錄 [!DNL Real-time Customer Profile]。 如果記錄中提供了多個身份，或使用了時間序列資料，則這些身份將在身份圖中映射，而不需要額外配置。 請參閱串流 [擷取開發人員指南](../../ingestion/tutorials/streaming-record-data.md) ，瞭解更多資訊。

## 確認上傳成功

第一次上傳資料至新資料集，或是作為新ETL或資料來源相關程式的一部分，建議您仔細檢查資料，以確保資料已正確上傳。

使用 [!DNL Real-time Customer Profile] Access API，您可以在批次資料載入資料集時擷取其中的資料。 如果您無法擷取任何預期的實體，您的資料集可能無法啟用 [!DNL Profile]。 確認資料集已啟用後，請確定您的來源資料格式和識別碼支援您的期望。

如需如何使用 [!DNL Real-time Customer Profile] API存取實體的詳細指示，請參閱實 [體端點指南](../api/entities.md)，亦稱為「[!DNL Profile Access] API」。