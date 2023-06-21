---
keywords: Experience Platform；設定檔；即時客戶設定檔；疑難排解；API；統一設定檔；統一設定檔；統一；設定檔；rtcp；啟用設定檔；啟用設定檔
title: Real-Time Customer Profile API指南
description: 即時客戶設定檔API可讓開發人員探索和使用設定檔資料，包括檢視設定檔、建立和更新合併原則、匯出或範例設定檔資料，以及刪除不再需要或錯誤新增的設定檔資料。 請遵循本指南以了解如何使用 API 執行關鍵作業。
exl-id: ce39b95b-cff7-46cf-a14c-8203017c8826
source-git-commit: 3b4e1e793a610c9391b3718584a19bd11959e3be
workflow-type: tm+mt
source-wordcount: '963'
ht-degree: 1%

---

# [!DNL Real-Time Customer Profile] API指南

[!DNL Real-Time Customer Profile] 可讓您在Adobe Experience Platform中檢視每個個別客戶的整體檢視。 [!DNL Profile] 可讓您將來自多個管道（例如線上、離線、CRM和協力廠商資料）的不同客戶資料整合為統一的檢視，針對每個客戶互動提供可採取行動且附有時間戳記的帳戶。

此 [!DNL Real-Time Customer Profile] API包含多個端點，概述如下。 如需詳細資訊，請參閱個別端點指南，並參閱 [快速入門手冊](getting-started.md) 如需必要標題的重要資訊，請參閱範例API呼叫等。

若要檢視所有可用的端點和CRUD作業，請造訪 [即時客戶設定檔API參考Swagger](https://www.adobe.com/go/profile-apis-en).

使用指南 [!DNL Real-Time Customer Profile] 中的資料 [!DNL Experience Platform] UI，請參閱 [設定檔使用手冊](../ui/user-guide.md).

## [!BADGE Beta]{type=Informative}計算屬性 {#computed-attributes}

>[!IMPORTANT]
>
>計算屬性功能為測試版，並非所有使用者都可使用。 檔案和功能可能會有所變更。

計算屬性是用來將事件層級資料彙總到設定檔層級屬性的函式。 這些函式會自動計算，以便用於區段、啟用和個人化。

每個計算屬性都包含一個運算式（或「規則」），該運算式會評估傳入的資料並將產生的值儲存在設定檔屬性中。 這些計算可協助您輕鬆回答與期限購買值、購買間隔時間或應用程式開啟次數相關的問題，而不需要您每次都需要資訊時手動執行複雜的計算。 然後可以在設定檔中檢視這些計算的屬性值、用來建立區段，或透過許多不同的存取模式進行存取。

您可以使用建立、檢視、編輯和刪除計算屬性 `ca/attributes/` 端點。 若要瞭解如何使用計算屬性，請參閱 [計算屬性概觀](../computed-attributes/overview.md). 如需API作業的相關資訊，請造訪 [計算屬性API端點指南](../computed-attributes/api.md).

## 邊緣投影 {#edge-projections}

Adobe Experience Platform可讓位於策略性位置（稱為「邊緣」）的伺服器輕鬆存取資料，進而實現客戶體驗的即時個人化。 此 [!DNL Real-Time Customer Profile] API透過稱為「投影」的元件提供處理邊緣的端點。 這包括投影設定，以決定要將哪些資料投影到每個邊緣，以及投影目的地，以定義要路由投影的位置。 如需使用Edge投影的詳細資訊，請瀏覽 [投影設定和目的地端點指南](edge-projections.md).

## 實體([!DNL Profile] access) {#entities}

透過Adobe Experience Platform，您可以存取 [!DNL Real-Time Customer Profile] 使用RESTful API或使用者介面的資料。 若要瞭解如何使用API存取實體（通常稱為「設定檔」），請遵循以下說明的步驟 [實體端點指南](entities.md). 若要使用存取設定檔 [!DNL Platform] UI，請參閱 [設定檔使用手冊](../ui/user-guide.md).

## 匯出工作([!DNL Profile] export) {#profile-export}

[!DNL Real-Time Customer Profile] 資料可匯出至資料集以供進一步處理，例如匯出受眾區段以供啟用，或匯出設定檔屬性以供報告。 匯出對象區段的工作是 [!DNL Adobe Experience Platform Segmentation Service] API，請閱讀 [分段匯出作業端點指南](../../profile/api/export-jobs.md) 以深入瞭解。 如需如何建立和管理設定檔屬性的匯出工作的逐步指示，請造訪 [匯出作業端點指南](export-jobs.md).

## 合併原則 {#merge-policies}

將來自多個來源的資料彙集在一起時 [!DNL Experience Platform]，合併原則是指 [!DNL Platform] 使用來決定資料的優先順序以及將合併哪些資料以建立個別客戶設定檔。 使用 [!DNL Real-Time Customer Profile] API後，您可以建立新的合併原則、管理現有原則，並為您的組織設定預設合併原則。 若要使用API合併原則，請造訪 [合併原則端點指南](merge-policies.md).

若要進一步瞭解合併原則及其在Platform中的角色，請先閱讀 [合併原則概觀](../merge-policies/overview.md).

## 預覽範例狀態([!DNL Profile] 預覽) {#profile-preview}

將資料內嵌至Platform後，會執行範例工作以更新設定檔計數和其他即時客戶設定檔資料相關量度。 此範例工作的結果可以使用檢視 `/previewsamplestatus` 端點，即時客戶設定檔API的一部分。 此端點也可用來依資料集和身分名稱空間列出設定檔分佈，以及產生多個報表，以瞭解貴組織設定檔存放區的組成。  若要開始使用 `/profilepreviewstatus` 端點，請參閱 [預覽範例狀態端點指南](preview-sample-status.md).

## 設定檔系統工作 {#profile-system-jobs}

已擷取到的設定檔啟用資料 [!DNL Platform] 儲存在 [!DNL Data Lake] 以及 [!DNL Real-Time Customer Profile] 資料存放區。 有時候，可能有必要從刪除資料集或批次 [!DNL Profile] 以移除您不再需要或錯誤新增的資料。 這需要使用API來建立 [!DNL Profile System Job]，也稱為「[!DNL delete request]「」，可視需要修改、監視或刪除。 若要瞭解如何使用來處理刪除請求 `/system/jobs` 中的端點 [!DNL Real-Time Customer Profile] API，請依照以下範例中概述的步驟： [設定檔系統作業端點指南](profile-system-jobs.md).

## 更新設定檔屬性 {#update-profile}

有時候，您可能需要更新組織設定檔存放區中的資料。 例如，您可能需要更正記錄或變更屬性值。 這可以透過批次擷取完成，並需要設定檔啟用的資料集，以更新插入標籤。 如需如何設定屬性更新資料集的詳細資訊，請參閱的教學課程 [為設定檔和更新插入啟用資料集](../../catalog/datasets/enable-upsert.md).

## 後續步驟 {#next-steps}

若要開始使用進行呼叫 [!DNL Real-Time Customer Profile] API，請閱讀 [快速入門手冊](getting-started.md) 然後選取其中一個端點指南，以瞭解如何使用特定的 [!DNL Profile] — 相關端點。 使用方式 [!DNL Profile] 資料使用 [!DNL Experience Platform] UI，請參閱 [即時客戶設定檔使用手冊](../ui/user-guide.md).
