---
keywords: Experience Platform；設定檔；即時客戶設定檔；疑難排解；API；啟用設定檔；啟用設定檔
title: 新增資料至即時客戶個人檔案
topic-legacy: tutorial
type: Tutorial
description: 本教學課程概述將資料新增至即時客戶設定檔的必要步驟。
exl-id: c2df224b-bf3d-4994-aa3a-9e9f4a6a726c
source-git-commit: 34e0381d40f884cd92157d08385d889b1739845f
workflow-type: tm+mt
source-wordcount: '452'
ht-degree: 0%

---


# 新增資料至 [!DNL Real-Time Customer Profile]

本教學課程概述將資料新增至 [!DNL Real-Time Customer Profile].

## 為 [!DNL Real-Time Customer Profile]

擷取至的資料 [!DNL Experience Platform] 供使用 [!DNL Real-Time Customer Profile] 必須符合 [!DNL Experience Data Model] (XDM)已啟用 [!DNL Profile]. 若要為設定檔啟用結構，必須實作 [!DNL XDM Individual Profile] 或 [!DNL XDM ExperienceEvent] 類別。

您可以啟用結構以用於 [!DNL Real-Time Customer Profile] 使用 [!DNL Schema Registry] API或 [!DNL Schema Editor] 使用者介面。 若要開始使用，請遵循 [使用API建立結構](../../xdm/tutorials/create-schema-api.md) 或 [使用結構編輯器UI建立結構](../../xdm/tutorials/create-schema-ui.md).

## 使用批次內嵌新增資料

所有上傳至的資料 [!DNL Platform] 使用批次內嵌功能會上傳至個別資料集。 此資料可供使用之前 [!DNL Real-Time Customer Profile]，則必須明確設定相關資料集。 如需完整指示，請參閱 [設定設定檔與身分服務的資料集](dataset-configuration.md).

設定資料集後，您就可以開始擷取資料。 請參閱 [批次匯入開發人員指南](../../ingestion/batch-ingestion/api-overview.md) 以取得上傳不同格式檔案的詳細步驟。

## 使用串流內嵌來新增資料

符合 [!DNL Profile]-enabled XDM架構會自動新增或覆寫 [!DNL Real-Time Customer Profile]. 如果記錄中提供多個身分，或使用時間序列資料，則這些身分將在身分圖中對應，無需額外設定。 請參閱 [串流獲取開發人員指南](../../ingestion/tutorials/streaming-record-data.md) 了解更多。

## 確認上傳成功

第一次將資料上傳至新資料集時，或是在涉及新ETL或資料來源的程式中，建議您仔細檢查資料，以確保資料已正確上傳。

使用 [!DNL Real-Time Customer Profile] 存取API時，您可以在批次資料載入至資料集時加以擷取。 如果您無法擷取任何預期的實體，資料集可能無法啟用 [!DNL Profile]. 確認資料集已啟用後，請確定來源資料格式和識別碼支援您的期望。

有關如何使用 [!DNL Real-Time Customer Profile] API，請參閱 [entities endpoint guide（圖元端點指南）](../api/entities.md)，也稱為「[!DNL Profile Access] API」。

## 更新設定檔存放區資料

有時候，您可能需要更新組織的設定檔存放區中的資料。 例如，您可能需要更正記錄或更改屬性值。 您可以透過批次內嵌完成此操作，且需要已啟用設定檔的資料集搭配上新插入標籤。 如需如何設定資料集以進行屬性更新的詳細資訊，請參閱的教學課程 [啟用「設定檔」和「插入」的資料集](../../catalog/datasets/enable-upsert.md).
