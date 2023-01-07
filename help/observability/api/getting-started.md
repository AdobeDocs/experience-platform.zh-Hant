---
keywords: Experience Platform；首頁；熱門主題；日期範圍
solution: Experience Platform
title: 可觀察性前瞻分析API快速入門
description: 可觀察性前瞻分析API可讓您擷取各種Adobe Experience Platform功能的量度資料。 本檔案介紹您在嘗試呼叫可觀察性前瞻分析API前，需要了解的核心概念。
exl-id: 3b120bd6-155d-467e-b98e-05478f8a4cc5
source-git-commit: 5a14eb5938236fa7186d1a27f28cee15fe6558f6
workflow-type: tm+mt
source-wordcount: '253'
ht-degree: 0%

---

# 開始使用 [!DNL Observability Insights] API

此 [!DNL Observability Insights] API可讓您擷取各種Adobe Experience Platform功能的量度資料。 本檔案簡介您在嘗試呼叫 [!DNL Observability Insights] API。

## 讀取範例API呼叫

此 [!DNL Observability Insights] API檔案提供範例API呼叫，以示範如何設定請求格式。 這些功能包括路徑、必要標題和格式正確的請求裝載。 也提供API回應中傳回的範例JSON。 如需範例API呼叫檔案中使用之慣例的資訊，請參閱 [Experience Platform疑難排解指南](../../landing/troubleshooting.md).

## 必要標題

若要對 [!DNL Platform] API，您必須先完成 [驗證教學課程](https://www.adobe.com/go/platform-api-authentication-en). 完成驗證教學課程會提供所有 [!DNL Experience Platform] API呼叫，如下所示：

* `Authorization: Bearer {ACCESS_TOKEN}`
* `x-api-key: {API_KEY}`
* `x-gw-ims-org-id: {ORG_ID}`

中的所有資源 [!DNL Experience Platform] 與特定虛擬沙箱隔離。 所有請求 [!DNL Platform] API需要標頭，以指定要進行操作的沙箱名稱。 如需中沙箱的詳細資訊，請參閱 [!DNL Platform]，請參閱 [沙箱概述檔案](../../sandboxes/home.md).

* `x-sandbox-name: {SANDBOX_NAME}`

## 後續步驟

若要開始使用進行呼叫 [!DNL Observability Insights] API，繼續前往 [metrics端點指南](./metrics.md).
