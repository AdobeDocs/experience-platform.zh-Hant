---
keywords: Experience Platform；配置檔案；即時客戶配置檔案；疑難排解；API；啟用配置檔案；啟用配置檔案
title: 新增資料至即時客戶個人檔案
topic-legacy: tutorial
type: Tutorial
description: 本教學課程概述將資料新增至即時客戶個人檔案的必要步驟。
exl-id: c2df224b-bf3d-4994-aa3a-9e9f4a6a726c
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '380'
ht-degree: 0%

---

# 將資料新增至[!DNL Real-time Customer Profile]

本教學課程概述將資料新增至[!DNL Real-time Customer Profile]的必要步驟。

## 為[!DNL Real-time Customer Profile]啟用模式

被收錄到[!DNL Experience Platform]以供[!DNL Real-time Customer Profile]使用的資料必須符合[!DNL Experience Data Model](XDM)架構，該架構已為[!DNL Profile]啟用。 要啟用配置式的架構，它必須實施[!DNL XDM Individual Profile]或[!DNL XDM ExperienceEvent]類。

您可以使用[!DNL Schema Registry] API或[!DNL Schema Editor]使用者介面，啟用架構以用於[!DNL Real-time Customer Profile]。 若要開始，請依照[使用API](../../xdm/tutorials/create-schema-api.md)或[使用架構編輯器UI](../../xdm/tutorials/create-schema-ui.md)建立架構的教學課程進行。

## 使用批次擷取新增資料

使用批次擷取上傳至[!DNL Platform]的所有資料都會上傳至個別的資料集。 在[!DNL Real-time Customer Profile]使用此資料之前，必須特別設定相關資料集。 有關完整說明，請參閱[為Profile and Identity Service](dataset-configuration.md)配置資料集的教程。

設定資料集後，您就可以開始將資料擷取至資料集。 請參閱[批次擷取開發人員指南](../../ingestion/batch-ingestion/api-overview.md)，以取得如何上傳不同格式檔案的詳細步驟。

## 使用串流擷取功能新增資料

任何與[!DNL Profile]啟用的XDM架構相容的串流內嵌資料，都會自動新增或覆寫[!DNL Real-time Customer Profile]中的適當記錄。 如果記錄中提供了多個身份，或使用了時間序列資料，則這些身份將在身份圖中映射，而不需要額外配置。 如需詳細資訊，請參閱[串流擷取開發人員指南](../../ingestion/tutorials/streaming-record-data.md)。

## 確認上傳成功

第一次上傳資料至新資料集，或是作為新ETL或資料來源相關程式的一部分，建議您仔細檢查資料，以確保資料已正確上傳。

使用[!DNL Real-time Customer Profile]存取API，您可以在批次資料載入資料集時擷取其中的資料。 如果您無法擷取任何預期的實體，您的資料集可能無法啟用[!DNL Profile]。 確認資料集已啟用後，請確定您的來源資料格式和識別碼支援您的期望。

有關如何使用[!DNL Real-time Customer Profile] API存取實體的詳細說明，請參閱[實體端點指南](../api/entities.md)，亦稱為&quot;[!DNL Profile Access] API&quot;。
