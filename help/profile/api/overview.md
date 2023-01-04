---
keywords: Experience Platform；設定檔；即時客戶設定檔；疑難排解；API；統一設定檔；統一設定檔；統一；設定檔；rtcp；啟用設定檔；啟用設定檔
title: 即時客戶個人檔案API指南
description: 即時客戶設定檔API可讓開發人員探索及使用設定檔資料，包括檢視設定檔、建立和更新合併原則、匯出或範例設定檔資料，以及刪除不再需要或有錯誤新增的設定檔資料。 請遵循本指南以了解如何使用 API 執行關鍵作業。
exl-id: ce39b95b-cff7-46cf-a14c-8203017c8826
source-git-commit: 34e0381d40f884cd92157d08385d889b1739845f
workflow-type: tm+mt
source-wordcount: '961'
ht-degree: 1%

---

# [!DNL Real-Time Customer Profile] API指南

[!DNL Real-Time Customer Profile] 可讓您全面了解Adobe Experience Platform中各個客戶的相關資訊。 [!DNL Profile] 可讓您將來自多個管道的不同客戶資料（例如線上、離線、CRM和協力廠商資料）整合至統一檢視中，提供每個客戶互動的可操作、時間戳記帳戶。

此 [!DNL Real-Time Customer Profile] API包含多個端點，如下所述。 如需詳細資訊，請參閱個別端點指南，並參閱 [快速入門手冊](getting-started.md) 如需必要標題、讀取範例API呼叫等的重要資訊。

若要檢視所有可用端點和CRUD作業，請造訪 [即時客戶設定檔API參考摘要](https://www.adobe.com/go/profile-apis-en).

使用指南 [!DNL Real-Time Customer Profile] 資料 [!DNL Experience Platform] UI，請參閱 [設定檔使用手冊](../ui/user-guide.md).

## (Alpha)計算屬性 {#computed-attributes}

>[!IMPORTANT]
>
>計算屬性功能為Alpha值，不適用於所有用戶。 檔案和功能可能會有所變更。

計算屬性是用於將事件層級資料匯總到設定檔層級屬性的函式。 系統會自動計算這些函式，以便用於不同區段、啟動和個人化。

每個計算屬性都包含一個運算式（或「規則」），用於評估傳入的資料並將產生的值儲存在設定檔屬性中。 這些計算有助於您輕鬆回答與期限購買值、購買間時間或應用程式開啟數量等相關的問題，而無需您每次需要資訊時都手動執行複雜的計算。 然後，這些計算屬性值便可在設定檔中檢視、用於建立區段，或透過許多不同的存取模式存取。

您可以使用 `config/computedAttributes` 端點。 若要了解如何使用計算屬性，請參閱 [計算屬性概述](../computed-attributes/overview.md). 若為API操作，請造訪 [計算屬性API端點指南](../computed-attributes/ca-api.md).

## 邊緣投影 {#edge-projections}

Adobe Experience Platform可讓資料在策略性位置的伺服器（稱為「邊緣」）上輕鬆存取，借此實現客戶體驗的即時個人化。 此 [!DNL Real-Time Customer Profile] API提供透過稱為「投影」的元件處理邊緣的端點。 這包括用於確定應投影到每個邊緣的資料的投影配置，以及用於定義投影路由位置的投影目的地。 如需使用邊緣投影的詳細資訊，請造訪 [投影設定和目的地端點指南](edge-projections.md).

## 實體([!DNL Profile] 存取) {#entities}

透過Adobe Experience Platform，您可以 [!DNL Real-Time Customer Profile] 使用RESTful API或使用者介面的資料。 若要了解如何使用API存取實體（通常稱為「設定檔」），請遵循 [entities endpoint guide（圖元端點指南）](entities.md). 若要使用 [!DNL Platform] UI，請參閱 [設定檔使用手冊](../ui/user-guide.md).

## 導出作業([!DNL Profile] 匯出) {#profile-export}

[!DNL Real-Time Customer Profile] 資料可匯出至資料集以供進一步處理，例如匯出受眾區段以供啟用，或用來製作報表的設定檔屬性。 對象區段的匯出工作屬於 [!DNL Adobe Experience Platform Segmentation Service] API，請閱讀 [細分匯出作業端點指南](../../profile/api/export-jobs.md) 了解更多。 有關如何建立和管理配置檔案屬性的導出作業的逐步說明，請訪問 [匯出作業端點指南](export-jobs.md).

## 合併策略 {#merge-policies}

將來自多個來源的資料匯整在 [!DNL Experience Platform]，合併策略是 [!DNL Platform] 用來決定資料的優先順序，以及將結合哪些資料以建立個別客戶設定檔。 使用 [!DNL Real-Time Customer Profile] API，您可以建立新的合併原則、管理現有原則，以及為組織設定預設的合併原則。 若要使用API處理合併原則，請造訪 [合併策略終結點指南](merge-policies.md).

若要進一步了解合併原則及其在Platform中的角色，請先閱讀 [合併策略概述](../merge-policies/overview.md).

## 預覽範例狀態([!DNL Profile] 預覽) {#profile-preview}

將資料內嵌至Platform時，會執行範例工作以更新設定檔計數和其他與即時客戶設定檔資料相關的量度。 此範例工作的結果可使用 `/previewsamplestatus` 端點，即時客戶設定檔API的一部分。 此端點也可用來列出資料集和身分命名空間的設定檔分配，以及產生多個報表，以便洞察組織的設定檔存放區組成。  若要開始使用 `/profilepreviewstatus` 端點，請參閱 [預覽範例狀態端點指南](preview-sample-status.md).

## 配置檔案系統作業 {#profile-system-jobs}

擷取至的已啟用設定檔資料 [!DNL Platform] 儲存於 [!DNL Data Lake] 以及 [!DNL Real-Time Customer Profile] 資料儲存。 有時候，您可能需要從 [!DNL Profile] 儲存，以移除您不再需要或有錯誤新增的資料。 這需要使用API來建立 [!DNL Profile System Job]，也稱為「[!DNL delete request]「 」，可以根據需要修改、監視或刪除。 若要了解如何使用 `/system/jobs` 端點 [!DNL Real-Time Customer Profile] API，請依照 [配置檔案系統作業終結點指南](profile-system-jobs.md).

## 更新設定檔屬性 {#update-profile}

有時候，您可能需要更新組織的設定檔存放區中的資料。 例如，您可能需要更正記錄或更改屬性值。 您可以透過批次內嵌完成此操作，且需要已啟用設定檔的資料集搭配上新插入標籤。 如需如何設定資料集以進行屬性更新的詳細資訊，請參閱的教學課程 [啟用「設定檔」和「插入」的資料集](../../catalog/datasets/enable-upsert.md).

## 後續步驟 {#next-steps}

若要開始使用進行呼叫 [!DNL Real-Time Customer Profile] API，請閱讀 [快速入門手冊](getting-started.md) 然後選取其中一個端點指南，以了解如何使用特定 [!DNL Profile] — 相關端點。 使用 [!DNL Profile] 資料使用 [!DNL Experience Platform] UI，請參閱 [即時客戶個人檔案使用手冊](../ui/user-guide.md).
