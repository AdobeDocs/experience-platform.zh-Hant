---
keywords: Experience Platform；設定檔；即時客戶設定檔；疑難排解；API
title: Real-Time Customer Profile API快速入門
type: Documentation
description: 設定檔API快速入門手冊概述您需瞭解的主要概念和基本功能，才能使用即時客戶設定檔API端點，對設定檔資料執行基本CRUD作業。
role: Developer
exl-id: 7e30610a-a7e7-43ab-a45d-fd84ef6e36ef
source-git-commit: c16ce1020670065ecc5415bc3e9ca428adbbd50c
workflow-type: tm+mt
source-wordcount: '407'
ht-degree: 6%

---

# 開始使用[!DNL Real-Time Customer Profile] API {#getting-started}

使用即時客戶設定檔API端點，您可以對設定檔資料執行基本CRUD操作，例如設定計算屬性、存取實體、匯出設定檔資料，以及刪除不需要的資料集或批次。

使用開發人員指南需要實際瞭解使用[!DNL Profile]資料所涉及的各種Adobe Experience Platform服務。 開始使用[!DNL Real-Time Customer Profile] API之前，請檢閱下列服務的檔案：

* [[!DNL Real-Time Customer Profile]](../home.md)：根據來自多個來源的彙總資料，即時提供統一的客戶設定檔。
* [[!DNL Adobe Experience Platform Identity Service]](../../identity-service/home.md)：跨裝置和系統橋接身分，以更清楚瞭解您的客戶及其行為。
* [[!DNL Adobe Experience Platform Segmentation Service]](../../segmentation/home.md)：可讓您從即時客戶設定檔資料建立對象。
* [[!DNL Experience Data Model (XDM)]](../../xdm/home.md)： Platform用來組織客戶體驗資料的標準化架構。
* [[!DNL Sandboxes]](../../sandboxes/home.md)： [!DNL Experience Platform]提供的虛擬沙箱可將單一[!DNL Platform]執行個體分割成個別的虛擬環境，以利開發及改進數位體驗應用程式。

下列章節提供您需瞭解的其他資訊，才能成功呼叫[!DNL Profile] API端點。

## 讀取範例 API 呼叫

[!DNL Real-Time Customer Profile] API檔案提供範例API呼叫，示範如何正確格式化請求。 這些包括路徑、必要的標頭和正確格式化的請求承載。 此外，也提供 API 回應中傳回的範例 JSON。 如需檔案中所使用範例API呼叫慣例的詳細資訊，請參閱[!DNL Experience Platform]疑難排解指南中[如何讀取範例API呼叫](../../landing/troubleshooting.md#how-do-i-format-an-api-request)一節。

## 必要的標頭

API檔案也要求您完成[驗證教學課程](https://www.adobe.com/go/platform-api-authentication-en)，才能成功呼叫[!DNL Platform]端點。 完成驗證教學課程會提供[!DNL Experience Platform] API呼叫中每個必要標題的值，如下所示：

* `Authorization: Bearer {ACCESS_TOKEN}`
* `x-api-key: {API_KEY}`
* `x-gw-ims-org-id: {ORG_ID}`

[!DNL Experience Platform]中的所有資源都與特定的虛擬沙箱隔離。 對[!DNL Platform] API的請求需要一個標頭，該標頭會指定將在其中執行操作的沙箱的名稱：

* `x-sandbox-name: {SANDBOX_NAME}`

如需[!DNL Platform]中沙箱的詳細資訊，請參閱[沙箱概觀檔案](../../sandboxes/home.md)。

要求內文中具有裝載的所有要求(例如POST、PUT和PATCH呼叫)都必須包含`Content-Type`標頭。 呼叫引數中會提供每個呼叫專屬的接受值。

## 後續步驟

若要開始使用[!DNL Real-Time Customer Profile] API進行呼叫，請選取其中一個可用的端點指南。
