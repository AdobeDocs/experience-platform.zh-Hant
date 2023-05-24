---
keywords: Experience Platform；配置檔案；即時客戶配置檔案；疑難解答；API；啟用配置檔案；啟用配置檔案
title: 將資料添加到即時客戶配置檔案
type: Tutorial
description: 本教程概述了向Real-Time Customer Profile添加資料所需的步驟。
exl-id: c2df224b-bf3d-4994-aa3a-9e9f4a6a726c
source-git-commit: 0f7ef438db5e7141197fb860a5814883d31ca545
workflow-type: tm+mt
source-wordcount: '452'
ht-degree: 0%

---


# 將資料添加到 [!DNL Real-Time Customer Profile]

本教程概括介紹了將資料添加到 [!DNL Real-Time Customer Profile]。

## 為 [!DNL Real-Time Customer Profile]

正在被攝入的資料 [!DNL Experience Platform] 供使用 [!DNL Real-Time Customer Profile] 必須符合 [!DNL Experience Data Model] 為 [!DNL Profile]。 要為配置檔案啟用架構，它必須實現 [!DNL XDM Individual Profile] 或 [!DNL XDM ExperienceEvent] 類。

可以啟用方案以用於 [!DNL Real-Time Customer Profile] 使用 [!DNL Schema Registry] API或 [!DNL Schema Editor] 用戶介面。 要開始，請按照 [使用API建立架構](../../xdm/tutorials/create-schema-api.md) 或 [使用架構編輯器UI建立架構](../../xdm/tutorials/create-schema-ui.md)。

## 使用批處理接收添加資料

所有資料上載到 [!DNL Platform] 將使用批處理攝取上傳到各個資料集。 在此資料可供使用之前 [!DNL Real-Time Customer Profile]，必須具體配置有關的資料集。 有關完整說明，請參見上的教程 [為配置檔案和身份服務配置資料集](dataset-configuration.md)。

資料集配置完畢後，可以開始將資料插入資料集。 查看 [批量攝取顯影劑指南](../../ingestion/batch-ingestion/api-overview.md) 有關如何以不同格式上載檔案的詳細步驟。

## 使用流式接收添加資料

任何符合流接收的資料 [!DNL Profile]-enabled XDM架構將自動在中添加或覆蓋相應的記錄 [!DNL Real-Time Customer Profile]。 如果在記錄中提供了多個標識，或使用了時間序列資料，則這些標識將在標識圖中映射，而無需額外配置。 查看 [流式接收開發人員指南](../../ingestion/tutorials/streaming-record-data.md) 來瞭解更多資訊。

## 確認上載成功

首次將資料上載到新資料集時，或作為涉及新ETL或資料源的進程的一部分，建議仔細檢查資料，以確保已正確上載資料。

使用 [!DNL Real-Time Customer Profile] 訪問API時，可以在批處理資料載入到資料集時檢索它。 如果無法檢索預期的任何實體，則可能未為 [!DNL Profile]。 確認已啟用資料集後，請確保源資料格式和標識符支援您的期望值。

有關如何使用 [!DNL Real-Time Customer Profile] API，請參閱 [實體端點指南](../api/entities.md)，也稱為「 」[!DNL Profile Access] API」。

## 更新配置檔案儲存資料

有時可能需要更新組織的配置檔案儲存中的資料。 例如，您可能需要更正記錄或更改屬性值。 這可以通過批處理接收來完成，並且需要使用upsert標籤配置啟用配置檔案的資料集。 有關如何配置資料集以進行屬性更新的詳細資訊，請參閱本教程以瞭解 [為配置檔案和upsert啟用資料集](../../catalog/datasets/enable-upsert.md)。
