---
keywords: Experience Platform；首頁；熱門主題；API;API；沙箱；沙箱；沙箱；沙箱
solution: Experience Platform
title: 沙箱API指南附錄
description: 本檔案提供與使用沙箱API相關的補充資訊。
exl-id: 48ffea01-f1b4-48c6-a6f5-c321074023d3
source-git-commit: 59dfa862388394a68630a7136dee8e8988d0368c
workflow-type: tm+mt
source-wordcount: '124'
ht-degree: 1%

---

# 沙箱API指南附錄

本檔案提供與使用 [!DNL Sandbox] API。

## 使用查詢參數 {#query}

此 [[!DNL Sandbox] API](https://www.adobe.io/experience-platform-apis/references/sandbox) 列出沙箱時，支援使用查詢參數來篩選結果。

>[!NOTE]
>
>此 `limit` 和 `offset` 必須一起指定查詢參數。 如果您只指定一個，API會傳回錯誤。 如果指定無，預設限制為50，偏移為0。

| 參數 | 說明 |
| --- | --- |
| `limit` | 回應中要傳回的記錄數上限。 |
| `offset` | 從第一個記錄開始（偏移）回應清單的實體數。 |
