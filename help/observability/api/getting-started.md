---
keywords: Experience Platform；首頁；熱門主題；日期範圍
solution: Experience Platform
title: Oncebrity Insights API入門
description: Oncebrity Insights API允許您檢索各種Adobe Experience Platform功能的度量資料。 本文檔介紹了在嘗試調用Oncebrity Insights API之前需要瞭解的核心概念。
exl-id: 3b120bd6-155d-467e-b98e-05478f8a4cc5
source-git-commit: 5a14eb5938236fa7186d1a27f28cee15fe6558f6
workflow-type: tm+mt
source-wordcount: '253'
ht-degree: 0%

---

# 入門 [!DNL Observability Insights] API

的 [!DNL Observability Insights] API允許您檢索各種Adobe Experience Platform功能的度量資料。 本文檔介紹了在嘗試呼叫至 [!DNL Observability Insights] API。

## 讀取示例API調用

的 [!DNL Observability Insights] API文檔提供了示例API調用，以演示如何格式化請求。 這些包括路徑、必需的標頭和正確格式化的請求負載。 還提供了API響應中返回的示例JSON。 有關文檔中用於示例API調用的約定的資訊，請參閱中有關如何讀取示例API調用的部分 [Experience Platform故障排除指南](../../landing/troubleshooting.md)。

## 必需的標題

為了呼叫 [!DNL Platform] API，必須首先完成 [驗證教程](https://www.adobe.com/go/platform-api-authentication-en)。 完成身份驗證教程將提供所有中每個必需標頭的值 [!DNL Experience Platform] API調用，如下所示：

* `Authorization: Bearer {ACCESS_TOKEN}`
* `x-api-key: {API_KEY}`
* `x-gw-ims-org-id: {ORG_ID}`

中的所有資源 [!DNL Experience Platform] 與特定虛擬沙箱隔離。 所有請求 [!DNL Platform] API需要一個標頭，該標頭指定操作將在中進行的沙盒的名稱。 有關中的沙箱的詳細資訊 [!DNL Platform]，請參見 [沙盒概述文檔](../../sandboxes/home.md)。

* `x-sandbox-name: {SANDBOX_NAME}`

## 後續步驟

使用 [!DNL Observability Insights] API，繼續 [度量終結點指南](./metrics.md)。
