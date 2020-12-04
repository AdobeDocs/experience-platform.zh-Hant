---
keywords: Experience Platform;home;popular topics;date range
solution: Experience Platform
title: 可觀性洞察API快速入門
topic: developer guide
description: 可觀測性洞察API可讓您擷取各種Adobe Experience Platform功能的量度資料。 本檔案提供您在嘗試呼叫Oncerbility Insights API之前，需要瞭解的核心概念。
translation-type: tm+mt
source-git-commit: c5455dc0812b251483170ac19506d7c60ad4ecaa
workflow-type: tm+mt
source-wordcount: '242'
ht-degree: 0%

---


# Getting started with the [!DNL Observability Insights] API

API [!DNL Observability Insights] 可讓您擷取各種Adobe Experience Platform功能的量度資料。 本檔案提供您在嘗試呼叫 [!DNL Observability Insights] API之前，需要瞭解的核心概念。

## 讀取範例API呼叫

API文 [!DNL Observability Insights] 件提供範例API呼叫，以示範如何設定請求的格式。 這些包括路徑、必要標題和正確格式化的請求負載。 也提供API回應中傳回的範例JSON。 如需範例API呼叫檔案中所用慣例的詳細資訊，請參閱 [Experience Platform疑難排解指南中有關如何讀取範例API呼叫的章節](../../landing/troubleshooting.md)。

## 必要的標題

若要呼叫API，您必 [!DNL Platform] 須先完成驗證教 [學課程](../../tutorials/authentication.md)。 完成驗證教學課程後，將提供所有 [!DNL Experience Platform] API呼叫中每個必要標題的值，如下所示：

* `Authorization: Bearer {ACCESS_TOKEN}`
* `x-api-key: {API_KEY}`
* `x-gw-ims-org-id: {IMS_ORG}`

中的所有資 [!DNL Experience Platform] 源都與特定虛擬沙盒隔離。 對API的所 [!DNL Platform] 有請求都需要一個標題，該標題會指定要進行操作的沙盒名稱。 如需中沙盒的詳細資訊 [!DNL Platform]，請參閱沙 [盒概述檔案](../../sandboxes/home.md)。

* `x-sandbox-name: {SANDBOX_NAME}`

## 後續步驟

若要開始使用 [!DNL Observability Insights] API進行呼叫，請前往量度 [端點指南](./metrics.md)。