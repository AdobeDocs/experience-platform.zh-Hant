---
keywords: Experience Platform；設定檔；即時客戶設定檔；疑難排解；API；統一設定檔；統一設定檔；統一；設定檔；rtcp；啟用設定檔；啟用設定檔
title: 即時客戶個人檔案API指南
description: 即時客戶設定檔API可讓開發人員探索及使用設定檔資料，包括檢視設定檔、建立和更新合併原則、匯出或範例設定檔資料，以及刪除不再需要或有錯誤新增的設定檔資料。 請依照本指南，了解如何使用API執行重要作業。
exl-id: ce39b95b-cff7-46cf-a14c-8203017c8826
source-git-commit: 1c2e4cd2b4070f3844a9848b5574e9d5b1688926
workflow-type: tm+mt
source-wordcount: '891'
ht-degree: 0%

---

# [!DNL Real-time Customer Profile] API指南

[!DNL Real-time Customer Profile] 可讓您全面了解Adobe Experience Platform中各個客戶的相關資訊。[!DNL Profile] 可讓您將來自多個管道的不同客戶資料（例如線上、離線、CRM和協力廠商資料）整合至統一檢視中，提供每個客戶互動的可操作、時間戳記帳戶。

[!DNL Real-time Customer Profile] API包含多個端點，如下所述。 如需詳細資訊，請造訪個別端點指南，並參閱[快速入門手冊](getting-started.md)，以取得必要標題、讀取範例API呼叫等的重要資訊。

若要檢視所有可用端點和CRUD作業，請造訪[即時客戶設定檔API參考Swagger](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/real-time-customer-profile.yaml)。

有關在[!DNL Experience Platform] UI中使用[!DNL Real-time Customer Profile]資料的指南，請參閱[設定檔使用手冊](../ui/user-guide.md)。

## (Alpha)計算屬性{#computed-attributes}

>[!IMPORTANT]
>
>計算屬性功能為Alpha值，不適用於所有用戶。 檔案和功能可能會有所變更。

計算屬性是用於將事件層級資料匯總到設定檔層級屬性的函式。 系統會自動計算這些函式，以便用於不同區段、啟動和個人化。

每個計算屬性都包含一個運算式（或「規則」），用於評估傳入的資料並將產生的值儲存在設定檔屬性中。 這些計算有助於您輕鬆回答與期限購買值、購買間時間或應用程式開啟數量等相關的問題，而無需您每次需要資訊時都手動執行複雜的計算。 然後，這些計算屬性值便可在設定檔中檢視、用於建立區段，或透過許多不同的存取模式存取。

可以使用`config/computedAttributes`端點建立、查看、編輯和刪除計算屬性。 若要了解如何使用計算屬性，請參閱[計算屬性概述](../computed-attributes/overview.md)。 有關API操作，請訪問[計算屬性API終結點指南](../computed-attributes/ca-api.md)。

## 邊緣投影{#edge-projections}

Adobe Experience Platform可讓資料在策略性位置的伺服器（稱為「邊緣」）上輕鬆存取，進而實現客戶體驗的即時個人化。 [!DNL Real-time Customer Profile] API提供端點，用於透過稱為「投影」的元件處理邊緣。 這包括用於確定應投影到每個邊緣的資料的投影配置，以及用於定義投影路由位置的投影目的地。 有關使用邊緣投影的詳細資訊，請訪問[投影配置和目標端點指南](edge-projections.md)。

## 實體（[!DNL Profile]訪問） {#entities}

您可以透過Adobe Experience Platform使用RESTful API或使用者介面存取[!DNL Real-time Customer Profile]資料。 若要了解如何使用API存取實體（通常稱為「設定檔」），請遵循[entities端點指南](entities.md)中概述的步驟。 若要使用[!DNL Platform] UI存取設定檔，請參閱[設定檔使用手冊](../ui/user-guide.md)。

## 導出作業（[!DNL Profile]導出）{#profile-export}

[!DNL Real-time Customer Profile] 資料可匯出至資料集以供進一步處理，例如匯出受眾區段以供啟用，或用來製作報表的設定檔屬性。對象區段的匯出工作屬於[!DNL Adobe Experience Platform Segmentation Service] API的一部分，請參閱[分段匯出工作端點指南](../../profile/api/export-jobs.md)以深入了解。 有關如何建立和管理配置檔案屬性的導出作業的逐步說明，請訪問[導出作業終結點指南](export-jobs.md)。

## 合併策略{#merge-policies}

在[!DNL Experience Platform]中將來自多個來源的資料集合在一起時，合併策略是[!DNL Platform]用於確定資料的優先順序以及將哪些資料合併以建立單個客戶配置檔案的規則。 使用[!DNL Real-time Customer Profile] API，您可以建立新的合併策略、管理現有策略，以及為組織設定預設的合併策略。 若要使用API使用合併策略，請訪問[合併策略終結點指南](merge-policies.md)。

若要進一步了解合併原則及其在Platform中的角色，請先閱讀[合併原則概述](../merge-policies/overview.md)開始。

## 預覽範例狀態（[!DNL Profile]預覽）{#profile-preview}

當為設定檔啟用的資料擷取至Experience Platform時，資料會儲存在設定檔資料存放區中。 隨著設定檔存放區中記錄數的增加或減少，會執行範例工作，其中包含關於資料存放區中有多少設定檔片段和合併的設定檔的資訊。 使用設定檔API，您可以預覽最新成功的範例，以及依資料集和身分命名空間列出設定檔分送。 若要開始使用`/profilepreviewstatus`端點，請參閱[預覽範例狀態端點指南](preview-sample-status.md)。

## 配置檔案系統作業{#profile-system-jobs}

內嵌至[!DNL Platform]的已啟用設定檔的資料會儲存在[!DNL Data Lake]和[!DNL Real-time Customer Profile]資料存放區中。 有時可能需要從[!DNL Profile]儲存區中刪除資料集或批次，以移除您不再需要或因錯誤新增的資料。 這需要使用API來建立[!DNL Profile System Job]（也稱為「[!DNL delete request]」），如有需要，可加以修改、監控或刪除。 若要了解如何使用[!DNL Real-time Customer Profile] API中的`/system/jobs`端點處理刪除請求，請遵循[設定檔系統作業端點指南](profile-system-jobs.md)中概述的步驟。

## 下一步 {#next-steps}

若要開始使用[!DNL Real-time Customer Profile] API進行呼叫，請閱讀[快速入門手冊](getting-started.md)，然後選取其中一個端點手冊，以了解如何使用特定的[!DNL Profile]相關端點。 若要使用[!DNL Experience Platform] UI處理[!DNL Profile]資料，請參閱[即時客戶設定檔使用手冊](../ui/user-guide.md)。
