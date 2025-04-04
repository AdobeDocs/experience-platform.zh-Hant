---
keywords: Experience Platform；設定檔；即時客戶設定檔；疑難排解；API；啟用設定檔；啟用設定檔
title: 新增資料至即時客戶個人檔案
type: Tutorial
description: 本教學課程概述將資料新增至即時客戶個人檔案的必要步驟。
exl-id: c2df224b-bf3d-4994-aa3a-9e9f4a6a726c
source-git-commit: b48c24ac032cbf785a26a86b50a669d7fcae5d97
workflow-type: tm+mt
source-wordcount: '452'
ht-degree: 0%

---


# 新增資料至[!DNL Real-Time Customer Profile]

本教學課程概述新增資料至[!DNL Real-Time Customer Profile]的必要步驟。

## 為[!DNL Real-Time Customer Profile]啟用結構描述

擷取到[!DNL Experience Platform]以供[!DNL Real-Time Customer Profile]使用的資料必須符合為[!DNL Profile]啟用的[!DNL Experience Data Model] (XDM)結構描述。 若要為設定檔啟用結構描述，它必須實作[!DNL XDM Individual Profile]或[!DNL XDM ExperienceEvent]類別。

您可以使用[!DNL Schema Registry] API或[!DNL Schema Editor]使用者介面啟用結構描述以用於[!DNL Real-Time Customer Profile]。 若要開始使用，請按照下列教學課程進行：[使用API建立結構描述](../../xdm/tutorials/create-schema-api.md)，或[使用結構描述編輯器UI](../../xdm/tutorials/create-schema-ui.md)建立結構描述。

## 使用批次擷取新增資料

所有使用批次擷取上傳至[!DNL Experience Platform]的資料都會上傳至個別資料集。 必須明確設定相關資料集，[!DNL Real-Time Customer Profile]才能使用此資料。 如需完整的指示，請參閱[設定設定檔與身分識別服務的資料集](dataset-configuration.md)上的教學課程。

設定資料集後，您就可以開始將資料擷取至其中。 如需如何上傳不同格式檔案的詳細步驟，請參閱[批次擷取開發人員指南](../../ingestion/batch-ingestion/api-overview.md)。

## 使用串流擷取新增資料

任何符合已啟用[!DNL Profile]的XDM結構描述的資料流擷取資料，都會自動新增或覆寫[!DNL Real-Time Customer Profile]中的適當記錄。 如果記錄中提供了多個身分，或使用了時間序列資料，則這些身分將會在身分圖形中對應而不需要額外的設定。 請參閱[串流擷取開發人員指南](../../ingestion/tutorials/streaming-record-data.md)以瞭解更多資訊。

## 確認上傳成功

首次將資料上傳到新資料集時，或作為涉及新ETL或資料來源的程式的一部分，建議仔細檢查資料，以確保資料已正確上傳。

使用[!DNL Real-Time Customer Profile] Access API，您可以在批次資料載入資料集時擷取該資料。 如果您無法擷取任何您期望的實體，您的資料集可能無法啟用[!DNL Profile]。 確認您的資料集已啟用後，請確保來源資料格式和識別碼支援您的期望。

如需有關如何使用[!DNL Real-Time Customer Profile] API存取實體的詳細指示，請參閱[實體端點指南](../api/entities.md)，也稱為「[!DNL Profile Access] API」。

## 更新設定檔存放區資料

有時候，您可能需要更新組織設定檔存放區中的資料。 例如，您可能需要更正記錄或變更屬性值。 這可以透過批次擷取完成，並需要設定檔啟用的資料集設定為upsert標籤。 如需如何設定屬性更新資料集的詳細資訊，請參閱[啟用設定檔和更新插入](../../catalog/datasets/enable-upsert.md)資料集的教學課程。
