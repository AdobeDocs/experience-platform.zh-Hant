---
keywords: Experience Platform；設定檔；即時客戶設定檔；疑難排解；API；整合式設定檔；整合式；設定檔；rtcp；啟用設定檔；啟用設定檔
title: 即時客戶設定檔API指南
description: 即時客戶設定檔API可讓開發人員探索和使用設定檔資料，包括檢視設定檔、建立和更新合併原則、匯出或範例設定檔資料，以及刪除不再需要或錯誤新增的設定檔資料。 請遵循本指南以了解如何使用 API 執行關鍵作業。
role: Developer
exl-id: ce39b95b-cff7-46cf-a14c-8203017c8826
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '862'
ht-degree: 2%

---

# [!DNL Real-Time Customer Profile] API指南

[!DNL Real-Time Customer Profile]可讓您在Adobe Experience Platform中檢視每個個別客戶的整體檢視。 [!DNL Profile]可讓您將來自多個管道（例如線上、離線、CRM和協力廠商資料）的不同客戶資料整合為統一的檢視，針對每個客戶互動提供可採取行動且附有時間戳記的帳戶。

[!DNL Real-Time Customer Profile] API包含多個端點，如下所述。 如需詳細資訊，請瀏覽個別端點指南，並參閱[快速入門手冊](getting-started.md)，以取得必要標頭、讀取範例API呼叫等重要資訊。

若要檢視所有可用的端點和CRUD作業，請造訪[即時客戶設定檔API參考swagger](https://www.adobe.com/go/profile-apis-en)。

如需在[!DNL Experience Platform] UI中使用[!DNL Real-Time Customer Profile]資料的指南，請參閱[設定檔使用者指南](../ui/user-guide.md)。

## 計算屬性 {#computed-attributes}

計算屬性是用來將事件層級資料彙總至設定檔層級屬性的函式。 這些函式會自動計算，以便用於區段、啟用和個人化。

每個計算屬性都包含運算式（或「規則」），可評估傳入的資料並將結果值儲存在設定檔屬性中。 這些計算可協助您輕鬆回答與期限購買價值、購買間隔時間或應用程式開啟次數相關的問題，而不需要您每次都需要手動執行複雜的計算。 然後可以在設定檔中檢視這些計算的屬性值，用來建立對象，或是透過許多不同的存取模式進行存取。

您可以使用`ca/attributes/`端點來建立、檢視、編輯和刪除計算屬性。 若要瞭解如何使用計算屬性，請參閱[計算屬性概述](../computed-attributes/overview.md)。 若為API作業，請造訪[計算屬性API端點指南](../computed-attributes/api.md)。

## 實體（[!DNL Profile]存取權） {#entities}

透過Adobe Experience Platform，您可以使用RESTful API或使用者介面存取[!DNL Real-Time Customer Profile]資料。 若要瞭解如何使用API存取實體（通常稱為「設定檔」），請依照[實體端點指南](entities.md)中概述的步驟操作。 若要使用[!DNL Experience Platform] UI存取設定檔，請參閱[設定檔使用手冊](../ui/user-guide.md)。

## 匯出工作（[!DNL Profile]匯出） {#profile-export}

可將[!DNL Real-Time Customer Profile]資料匯出至資料集以供進一步處理，例如匯出對象以供啟動或設定檔屬性以供報告。 對象的匯出作業是[!DNL Adobe Experience Platform Segmentation Service] API的一部分，請參閱[分段匯出作業端點指南](../../profile/api/export-jobs.md)以瞭解更多資訊。 如需如何建立和管理設定檔屬性之匯出工作的逐步指示，請造訪[匯出工作端點指南](export-jobs.md)。

## 合併原則 {#merge-policies}

將來自多個來源的資料彙集到[!DNL Experience Platform]中時，合併原則是[!DNL Experience Platform]用來決定資料優先順序的方式以及將合併哪些資料以建立個別客戶設定檔的規則。 使用[!DNL Real-Time Customer Profile] API，您可以建立新的合併原則、管理現有原則，並為您的組織設定預設合併原則。 若要使用API來使用合併原則，請造訪[合併原則端點指南](merge-policies.md)。

若要進一步瞭解合併原則及其在Experience Platform中的角色，請先閱讀[合併原則概觀](../merge-policies/overview.md)。

## 預覽樣本狀態（[!DNL Profile]預覽） {#profile-preview}

將資料內嵌至Experience Platform後，會執行範例工作以更新設定檔計數和其他即時客戶設定檔資料相關量度。 此範例工作的結果可以使用`/previewsamplestatus`端點（即時客戶設定檔API的一部分）進行檢視。 此端點也可用來根據資料集和身分名稱空間列出設定檔分佈，以及產生多個報表，以瞭解您組織設定檔存放區的構成。  若要開始使用`/profilepreviewstatus`端點，請參閱[預覽範例狀態端點指南](preview-sample-status.md)。

## 設定檔系統工作 {#profile-system-jobs}

擷取到[!DNL Experience Platform]的已啟用設定檔的資料儲存在[!DNL Data Lake]以及[!DNL Real-Time Customer Profile]資料存放區。 有時候，可能有必要從設定檔存放區中刪除與資料集相關聯的設定檔資料，以移除不再需要或錯誤新增的資料。 這需要使用API來建立[!DNL Profile System Job] （也稱為「[!DNL delete request]」），如有必要，可以修改、監視或刪除。 若要瞭解如何使用[!DNL Real-Time Customer Profile] API中的`/system/jobs`端點來處理刪除請求，請依照[設定檔系統作業端點指南](profile-system-jobs.md)中概述的步驟操作。

## 更新設定檔屬性 {#update-profile}

有時候，您可能需要更新組織設定檔存放區中的資料。 例如，您可能需要更正記錄或變更屬性值。 這可以透過批次擷取完成，並需要設定檔啟用的資料集設定為upsert標籤。 如需如何設定屬性更新資料集的詳細資訊，請參閱[啟用設定檔和更新插入](../../catalog/datasets/enable-upsert.md)資料集的教學課程。

## 後續步驟 {#next-steps}

若要開始使用[!DNL Real-Time Customer Profile] API進行呼叫，請閱讀[快速入門手冊](getting-started.md)，然後選取其中一個端點指南，以瞭解如何使用特定的[!DNL Profile]相關端點。 若要使用[!DNL Experience Platform] UI處理[!DNL Profile]資料，請參閱[即時客戶設定檔使用手冊](../ui/user-guide.md)。
