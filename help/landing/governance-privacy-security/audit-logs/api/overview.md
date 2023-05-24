---
title: 審計查詢API指南
description: 審核查詢是REST風格的API，它允許開發人員查看誰在Adobe Experience Platform執行了哪些操作。
exl-id: 9ed291c6-ff8b-4d9b-9fed-d1e3fa8f92fb
source-git-commit: c2c5778e0a3fff7f488ad7a672123c813cca59f1
workflow-type: tm+mt
source-wordcount: '175'
ht-degree: 1%

---

# [!DNL Audit Query] API指南

的 [!DNL Audit Query] API提供端點，允許您以寫程式方式檢索和監視各種Adobe Experience Platform功能的事件資料。 下面概述了端點。 請訪問 [入門指南](./getting-started.md) 有關所需標頭、讀取示例API調用等的重要資訊。

要查看所有可用端點和CRUD操作，請訪問 [[!DNL Audit Query] API交換器](https://www.adobe.io/experience-platform-apis/references/audit-query/)。

## 活動

審計事件提供了有關平台中用戶操作的見解，包括操作類型、日期和時間、執行該操作的用戶的電子郵件ID以及與Adobe Experience Platform各功能的操作類型相關的其他屬性。 要瞭解如何使用API檢索度量，請參閱 [事件終結點指南](./events.md)。

## 轉存

審計導出允許您通過指定要在負載中檢索的事件來檢索事件資料。 要瞭解如何使用API檢索度量，請參閱 [導出終結點指南](./export.md)。
