---
keywords: Experience Platform；首頁；熱門主題；api;API；沙盒；沙盒；沙盒；沙盒
solution: Experience Platform
title: 沙盒API指南附錄
description: 本文檔提供與使用沙盒API相關的補充資訊。
exl-id: 48ffea01-f1b4-48c6-a6f5-c321074023d3
source-git-commit: 59dfa862388394a68630a7136dee8e8988d0368c
workflow-type: tm+mt
source-wordcount: '124'
ht-degree: 1%

---

# 沙盒API指南附錄

本文檔提供與與 [!DNL Sandbox] API。

## 使用查詢參數 {#query}

的 [[!DNL Sandbox] API](https://www.adobe.io/experience-platform-apis/references/sandbox) 支援在列出沙箱時使用查詢參數來頁面和篩選結果。

>[!NOTE]
>
>的 `limit` 和 `offset` 必須同時指定查詢參數。 如果僅指定一個，則API將返回錯誤。 如果指定無，則預設限制為50，偏移為0。

| 參數 | 說明 |
| --- | --- |
| `limit` | 響應中要返回的最大記錄數。 |
| `offset` | 從第一記錄開始（偏移）響應清單的實體數。 |
