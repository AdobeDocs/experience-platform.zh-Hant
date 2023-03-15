---
title: 稽核查詢API指南
description: 「稽核查詢」是RESTful API，可讓開發人員查看誰在Adobe Experience Platform中執行了哪些動作。
exl-id: 9ed291c6-ff8b-4d9b-9fed-d1e3fa8f92fb
source-git-commit: c2c5778e0a3fff7f488ad7a672123c813cca59f1
workflow-type: tm+mt
source-wordcount: '175'
ht-degree: 1%

---

# [!DNL Audit Query] API指南

此 [!DNL Audit Query] API提供的端點可讓您以程式設計方式擷取和監控各種Adobe Experience Platform功能的事件資料。 這些端點概述如下。 請造訪 [快速入門手冊](./getting-started.md) 如需必要標題、讀取範例API呼叫等的重要資訊。

若要檢視所有可用端點和CRUD作業，請造訪 [[!DNL Audit Query] API Swagger](https://www.adobe.io/experience-platform-apis/references/audit-query/).

## 活動

稽核事件可提供Platform中使用者動作的深入分析，包括動作類型、日期和時間、執行動作之使用者的電子郵件ID，以及Adobe Experience Platform中各種功能之動作類型的其他相關屬性。 若要了解如何使用API擷取量度，請參閱 [events endpoint指南](./events.md).

## 轉存

稽核匯出可讓您指定要在裝載中擷取的事件，以擷取事件資料。 若要了解如何使用API擷取量度，請參閱 [匯出端點指南](./export.md).
