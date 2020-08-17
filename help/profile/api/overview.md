---
keywords: Experience Platform;profile;real-time customer profile;troubleshooting;API;unified profile;Unified Profile;unified;Profile;rtcp;enable profile;Enable profile
solution: Adobe Experience Platform
title: 即時客戶個人檔案API開發人員指南
topic: guide
description: 即時客戶個人檔案API包含多個端點，概述如下。
translation-type: tm+mt
source-git-commit: 04efbf63741ef39bbf0b22795be74087f1f7c595
workflow-type: tm+mt
source-wordcount: '806'
ht-degree: 0%

---


# [!DNL Real-time Customer Profile] API開發人員指南

[!DNL Real-time Customer Profile] 讓您在Adobe Experience Platform中全面瞭解每一位客戶。 [!DNL Profile] 可讓您將來自多個通道的零散客戶資料（例如線上、離線、CRM和第三方資料）整合為一個統一的檢視，為每個客戶互動提供可操作的時間戳記帳戶。

API包 [!DNL Real-time Customer Profile] 含多個端點，概述如下。 如需詳細資訊，請造訪個別端點指南，並參 [閱快速入門手冊](getting-started.md) ，以取得必要標題、讀取範例API呼叫等重要資訊。

若要檢視所有可用的端點和CRUD作業，請造 [訪即時客戶個人檔案API參考設定檔](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/real-time-customer-profile.yaml)。

如需在UI中使用資料 [!DNL Real-time Customer Profile] 的指南，請 [!DNL Experience Platform] 參閱描述檔使 [用指南](../ui/user-guide.md)。

## (Alpha)計算屬性 {#computed-attributes}

>[!IMPORTANT]
>
>計算屬性功能為alpha，並非所有使用者皆可使用。 檔案和功能可能會有所變更。

計算屬性可讓您根據其他值、計算和運算式自動計算欄位的值。 計算屬性在描述檔層級上運作，這表示您可以匯總所有記錄和事件的值。 每個計算屬性都包含一個運算式（或「規則」），可評估傳入的資料，並將產生的值儲存在描述檔屬性或事件中。 這些計算可協助您輕鬆回答與期限購買值、購買間隔時間或應用程式開啟次數等相關的問題，而不需在每次需要資訊時手動執行複雜的計算。 您可以使用端點建立、查看、編輯和刪除計算屬 `config/computedAttributes` 性。 要瞭解如何使用此端點，請訪問計算 [的屬性端點指南](computed-attributes.md)。

## 邊緣投影 {#edge-projections}

Adobe Experience Platform讓資料可輕鬆在戰略性位置的伺服器（稱為「邊緣」）上存取，讓客戶體驗即時個人化。 API [!DNL Real-time Customer Profile] 提供端點，讓您透過稱為「投影」的元件處理邊緣。 這包括確定應將哪些資料投影到每個邊的投影配置，以及定義投影路由位置的投影目標。 有關使用邊緣投影的詳細資訊，請造訪投影 [設定和目標端點指南](edge-projections.md)。

## 實體([!DNL Profile] 存取) {#entities}

透過Adobe Experience Platform，您可以使 [!DNL Real-time Customer Profile] 用REST風格的API或使用者介面存取資料。 若要瞭解如何使用API存取實體（更常稱為「設定檔」），請依照實體端點指南中 [的步驟](entities.md)。 若要使用 [!DNL Platform] UI存取描述檔，請參閱 [Profile使用指南](../ui/user-guide.md)。

## 匯出工作([!DNL Profile] 匯出) {#profile-export}

[!DNL Real-time Customer Profile] 資料可匯出至資料集以進一步處理，例如匯出受眾區段以進行啟動或描述檔屬性以進行報告。 讀者區段的匯出工作是 [!DNL Adobe Experience Platform Segmentation Service] API的一部分，請閱讀區 [段匯出工作端點指南](../../profile/api/export-jobs.md) ，以瞭解詳細資訊。 有關如何為配置檔案屬性建立和管理導出作業的逐步說明，請訪問導 [出作業端點指南](export-jobs.md)。

## 合併原則 {#merge-policies}

將多個來源的資料匯整在一起時 [!DNL Experience Platform][!DNL Platform] ，合併原則是用來判斷資料的優先順序，以及將哪些資料合併以建立個別客戶個人檔案的規則。 使用 [!DNL Real-time Customer Profile] API，您可以建立新的合併原則、管理現有原則，以及為組織設定預設的合併原則。 若要進一步瞭解如何使用API來使用合併原則，請造訪合 [並原則端點指南](merge-policies.md)。

有關使用 [!DNL Platform] UI使用合併策略的指南，請參 [閱合併策](../ui/merge-policies.md)略使用手冊。

## 預覽範例狀態([!DNL Profile] 預覽) {#profile-preview}

當為描述檔啟用的資料已收錄到Experience Platform中時，它會儲存在描述檔資料儲存區中。 隨著描述檔儲存區中記錄數的增加或減少，會執行範例工作，其中包含資料儲存區中有多少描述檔片段和合併的描述檔的相關資訊。 使用描述檔API，您可以預覽最新成功的範例，以及依資料集和身分命名空間來列出描述檔散發。 若要開始使用端點， `/profilepreviewstatus` 請參閱預覽 [範例狀態端點指南](preview-sample-status.md)。

## 描述檔系統工作 {#profile-system-jobs}

所吸收的 [!DNL Platform] 資料被儲存在 [!DNL Data Lake] 資料儲存 [!DNL Real-time Customer Profile] 器中。 有時可能需要從商店刪除資料集或批次， [!DNL Profile] 以移除您不再需要或錯誤新增的資料。 這需要使用API來建 [!DNL Profile System Job]立稱為「[!DNL delete request]」的，如有需要，也可加以修改、監視或刪除。 要瞭解如何使用 `/system/jobs` API中的端點處理刪除請求，請遵循配置式系統作業端點指 [!DNL Real-time Customer Profile] 南中概述的步驟 [](profile-system-jobs.md)。

## 下一步 {#next-steps}

若要開始使用 [!DNL Real-time Customer Profile] API進行呼叫，請閱讀 [快速入門手冊](getting-started.md) ，然後選取其中一個端點指南，以瞭解如何使用特定的 [!DNL Profile]相關端點。 若要使用 [!DNL Profile] UI處理資料 [!DNL Experience Platform] ，請參閱即時客 [戶個人檔案使用指南](../ui/user-guide.md)。