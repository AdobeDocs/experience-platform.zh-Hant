---
keywords: Experience Platform；首頁；熱門主題；API;API；沙箱；沙箱；沙箱；沙箱
solution: Experience Platform
title: 沙箱API指南附錄
description: 本檔案提供與使用沙箱API相關的補充資訊。
topic-legacy: developer guide
source-git-commit: f5ce7b7f09c624c53065757bb8a9b09f989dce0a
workflow-type: tm+mt
source-wordcount: '124'
ht-degree: 1%

---

# 沙箱API指南附錄

本檔案提供與使用[!DNL Sandbox] API相關的補充資訊。

## 使用查詢參數 {#query}

[[!DNL Sandbox] API](https://www.adobe.io/experience-platform-apis/references/sandbox)支援在列出沙箱時，使用查詢參數來篩選結果。

>[!NOTE]
>
>必須同時指定`limit`和`offset`查詢參數。 如果您只指定一個，API會傳回錯誤。 如果指定無，預設限制為50，偏移為0。

| 參數 | 說明 |
| --- | --- |
| `limit` | 回應中要傳回的記錄數上限。 |
| `offset` | 從第一個記錄開始（偏移）回應清單的實體數。 |
