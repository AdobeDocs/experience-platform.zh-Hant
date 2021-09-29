---
keywords: Experience Platform；設定檔；即時客戶設定檔；疑難排解；API；啟用設定檔；啟用設定檔
title: 新增資料至即時客戶個人檔案
topic-legacy: tutorial
type: Tutorial
description: 本教學課程概述將資料新增至即時客戶設定檔的必要步驟。
exl-id: c2df224b-bf3d-4994-aa3a-9e9f4a6a726c
source-git-commit: 3b34cf37182ae98545651a7b54f586df7d811f34
workflow-type: tm+mt
source-wordcount: '454'
ht-degree: 0%

---


# 將資料添加到[!DNL Real-time Customer Profile]

本教學課程概述將資料新增至[!DNL Real-time Customer Profile]所需的步驟。

## 為[!DNL Real-time Customer Profile]啟用架構

要內嵌到[!DNL Experience Platform]以供[!DNL Real-time Customer Profile]使用的資料必須符合為[!DNL Profile]啟用的[!DNL Experience Data Model](XDM)架構。 為了為Profile啟用架構，它必須實作[!DNL XDM Individual Profile]或[!DNL XDM ExperienceEvent]類。

您可以使用[!DNL Schema Registry] API或[!DNL Schema Editor]使用者介面，在[!DNL Real-time Customer Profile]中啟用架構以使用。 若要開始使用，請依照[使用API](../../xdm/tutorials/create-schema-api.md)或[使用架構編輯器UI](../../xdm/tutorials/create-schema-ui.md)建立架構的教學課程進行。

## 使用批次內嵌新增資料

使用批次內嵌上傳至[!DNL Platform]的所有資料都會上傳至個別資料集。 在[!DNL Real-time Customer Profile]可以使用此資料之前，必須特別配置相關資料集。 如需完整指示，請參閱[為設定設定檔與身分服務資料集的教學課程](dataset-configuration.md)。

設定資料集後，您就可以開始擷取資料。 如需如何上傳不同格式檔案的詳細步驟，請參閱[批次內嵌開發人員指南](../../ingestion/batch-ingestion/api-overview.md)。

## 使用串流內嵌來新增資料

任何符合[!DNL Profile]啟用的XDM架構的串流內嵌資料，都會自動新增或覆寫[!DNL Real-time Customer Profile]中的適當記錄。 如果記錄中提供多個身分，或使用時間序列資料，則這些身分將在身分圖中對應，無需額外設定。 請參閱[串流獲取開發人員指南](../../ingestion/tutorials/streaming-record-data.md)以深入了解。

## 確認上傳成功

第一次將資料上傳至新資料集時，或是在涉及新ETL或資料來源的程式中，建議您仔細檢查資料，以確保資料已正確上傳。

使用[!DNL Real-time Customer Profile]存取API，您可以在將批次資料載入資料集時擷取該資料。 如果您無法擷取任何預期的實體，您的資料集可能無法啟用[!DNL Profile]。 確認資料集已啟用後，請確定來源資料格式和識別碼支援您的期望。

有關如何使用[!DNL Real-time Customer Profile] API存取實體的詳細說明，請參閱[entitys端點指南](../api/entities.md)，也稱為「[!DNL Profile Access] API」。

## 更新設定檔存放區資料

有時候，您可能需要更新組織的設定檔存放區中的資料。 例如，您可能需要更正記錄或更改屬性值。 您可以透過批次或串流內嵌完成此操作，且需要已啟用設定檔的資料集搭配上新插入標籤。 有關如何配置資料集進行屬性更新的詳細資訊，請參閱[啟用資料集進行配置檔案和更新](../../catalog/datasets/enable-upsert.md)的教程。
