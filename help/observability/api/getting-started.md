---
keywords: Experience Platform；首頁；熱門主題；日期範圍
solution: Experience Platform
title: 可觀性洞察API快速入門
topic-legacy: developer guide
description: 可觀測性洞察API可讓您擷取各種Adobe Experience Platform功能的量度資料。 本檔案提供您在嘗試呼叫Oncerbility Insights API之前，需要瞭解的核心概念。
exl-id: 3b120bd6-155d-467e-b98e-05478f8a4cc5
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '253'
ht-degree: 0%

---

# [!DNL Observability Insights] API快速入門

[!DNL Observability Insights] API可讓您擷取各種Adobe Experience Platform功能的量度資料。 本檔案提供您在嘗試呼叫[!DNL Observability Insights] API之前，需要瞭解的核心概念的簡介。

## 讀取範例API呼叫

[!DNL Observability Insights] API檔案提供範例API呼叫，以示範如何格式化您的請求。 這些包括路徑、必要標題和正確格式化的請求負載。 也提供API回應中傳回的範例JSON。 如需範例API呼叫檔案中所用慣例的詳細資訊，請參閱[Experience Platform疑難排解指南](../../landing/troubleshooting.md)中有關如何讀取範例API呼叫的章節。

## 必要的標題

若要呼叫[!DNL Platform] API，您必須先完成[驗證教學課程](https://www.adobe.com/go/platform-api-authentication-en)。 完成驗證教學課程後，所有[!DNL Experience Platform] API呼叫中每個所需標題的值都會顯示在下面：

* `Authorization: Bearer {ACCESS_TOKEN}`
* `x-api-key: {API_KEY}`
* `x-gw-ims-org-id: {IMS_ORG}`

[!DNL Experience Platform]中的所有資源都隔離到特定的虛擬沙盒。 對[!DNL Platform] API的所有請求都需要一個標題，該標題指定要進行操作的沙盒的名稱。 如需[!DNL Platform]中沙盒的詳細資訊，請參閱[沙盒概述檔案](../../sandboxes/home.md)。

* `x-sandbox-name: {SANDBOX_NAME}`

## 後續步驟

若要開始使用[!DNL Observability Insights] API進行呼叫，請繼續[度量端點指南](./metrics.md)。
