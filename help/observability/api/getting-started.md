---
keywords: Experience Platform；首頁；熱門主題；日期範圍
solution: Experience Platform
title: 開始使用Observability Insights API
description: 「可觀察性深入分析API」可讓您擷取各種Adobe Experience Platform功能的量度資料。 本檔案介紹嘗試呼叫Observability Insights API之前需要瞭解的核心概念。
exl-id: 3b120bd6-155d-467e-b98e-05478f8a4cc5
source-git-commit: 5a14eb5938236fa7186d1a27f28cee15fe6558f6
workflow-type: tm+mt
source-wordcount: '250'
ht-degree: 18%

---

# 開始使用[!DNL Observability Insights] API

[!DNL Observability Insights] API可讓您擷取各種Adobe Experience Platform功能的量度資料。 本檔案提供嘗試呼叫[!DNL Observability Insights] API之前需要瞭解的核心概念簡介。

## 讀取範例 API 呼叫

[!DNL Observability Insights] API檔案提供範例API呼叫，示範如何格式化您的請求。 這些包括路徑、必要的標頭和正確格式化的請求承載。 此外，也提供 API 回應中傳回的範例 JSON。 如需檔案中所使用之範例API呼叫慣例的詳細資訊，請參閱[Experience Platform疑難排解指南](../../landing/troubleshooting.md)中有關如何讀取範例API呼叫的章節。

## 必要的標頭

若要呼叫[!DNL Platform] API，您必須先完成[驗證教學課程](https://www.adobe.com/go/platform-api-authentication-en)。 完成驗證教學課程會提供所有 [!DNL Experience Platform] API 呼叫中每個必要標頭的值，如下所示：

* `Authorization: Bearer {ACCESS_TOKEN}`
* `x-api-key: {API_KEY}`
* `x-gw-ims-org-id: {ORG_ID}`

[!DNL Experience Platform]中的所有資源都與特定的虛擬沙箱隔離。 對[!DNL Platform] API的所有請求都需要標頭，以指定將在其中執行作業的沙箱名稱。 如需[!DNL Platform]中沙箱的詳細資訊，請參閱[沙箱概觀檔案](../../sandboxes/home.md)。

* `x-sandbox-name: {SANDBOX_NAME}`

## 後續步驟

若要開始使用[!DNL Observability Insights] API進行呼叫，請繼續參閱[量度端點指南](./metrics.md)。
