---
keywords: Experience Platform;profile;real-time customer profile;troubleshooting;API
solution: Adobe Experience Platform
title: 即時客戶個人檔案API開發人員指南
topic: guide
translation-type: tm+mt
source-git-commit: c0b059d6654a98b74be5bc6a55f360c4dc2f216b
workflow-type: tm+mt
source-wordcount: '668'
ht-degree: 0%

---


# 即時客戶個人檔案API開發人員指南

即時客戶個人檔案可讓您在Adobe Experience Platform中全面瞭解每個客戶。 個人檔案可讓您將來自多個通道（例如線上、離線、CRM和第三方資料）的分散客戶資料整合為一個統一的檢視，提供每個客戶互動的可操作的時間戳記帳戶。

即時客戶個人檔案API包含多個端點，概述如下。 如需詳細資訊，請造訪個別端點指南，並參 [閱快速入門手冊](getting-started.md) ，以取得必要標題、讀取範例API呼叫等重要資訊。

若要檢視所有可用的端點和CRUD作業，請參閱即 [時客戶個人檔案API參考設定檔](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/real-time-customer-profile.yaml)。

## (Alpha)計算屬性

>[!IMPORTANT]
>
>
>計算屬性功能為alpha，並非所有使用者皆可使用。 檔案和功能可能會有所變更。

計算屬性可讓您根據其他值、計算和運算式自動計算欄位的值。 計算屬性在描述檔層級上運作，這表示您可以匯總所有記錄和事件的值。 每個計算屬性都包含一個運算式（或「規則」），可評估傳入的資料，並將產生的值儲存在描述檔屬性或事件中。 這些計算可協助您輕鬆回答與期限購買值、購買間隔時間或應用程式開啟次數等相關的問題，而不需在每次需要資訊時手動執行複雜的計算。 您可以使用端點建立、查看、編輯和刪除計算屬 `config/computedAttributes` 性。 要瞭解如何使用此端點，請訪問計算 [的屬性端點指南](computed-attributes.md)。

## 邊緣投影

Adobe Experience Platform讓資料可輕鬆在戰略性位置的伺服器（稱為「邊緣」）上存取，讓客戶體驗即時個人化。 即時客戶個人檔案API提供端點，以透過稱為「預測」的元件處理邊緣。 這包括確定應將哪些資料投影到每個邊的投影配置，以及定義投影路由位置的投影目標。 有關使用邊緣投影的詳細資訊，請造訪投影 [設定和目標端點指南](edge-projections.md)。

## 實體（描述檔存取） {#entities}

透過Adobe Experience Platform，您可以使用REST風格的API或使用者介面存取即時客戶個人檔案資料。 若要瞭解如何使用API存取實體（更常稱為「設定檔」），請依照實體端點指南中 [的步驟](entities.md)。 若要使用平台UI存取描述檔，請參閱「描述檔 [使用指南」](../ui/user-guide.md)。

## 合併原則

在Experience Platform中將多個來源的資料匯整在一起時，合併原則是平台用來決定資料的優先順序以及將哪些資料合併以建立個別客戶個人檔案的規則。 使用「即時客戶個人檔案API」，您可以建立新的合併原則、管理現有原則，以及為組織設定預設的合併原則。 若要進一步瞭解如何使用API來使用合併原則，請造訪合 [並原則端點指南](merge-policies.md)。

有關使用平台UI使用合併策略的指南，請參閱合 [並策略使用手冊](../ui/merge-policies.md)。

## 描述檔系統工作

Data Lake和即時客戶個人檔案資料儲存中會儲存在Platform中。 有時可能需要從描述檔存放區刪除資料集或批次，以移除您不再需要或錯誤新增的資料。 這需要使用API來建立描述檔系統工作（稱為「刪除請求」），如有需要，也可加以修改、監視或刪除。 要瞭解如何使用即時客戶配置檔案API中的 `/system/jobs` 端點處理刪除請求，請遵循配置檔案系統作業端點指 [南中概述的步驟](profile-system-jobs.md)。

## 後續步驟

若要開始使用即時客戶描述檔API進行呼叫，請閱讀快速入門手冊 [](getting-started.md) ，然後選取其中一個端點指南，以瞭解如何使用特定的描述檔相關端點。 若要進一步瞭解如何使用平台UI使用描述檔資料，請參 [閱即時客戶描述檔使用指南](../ui/user-guide.md)。