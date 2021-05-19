---
keywords: Experience Platform；配置檔案；即時客戶配置檔案；疑難排解；API；統一配置檔案；統一配置檔案；配置檔案；rtcp；啟用配置檔案；啟用配置檔案
title: 即時客戶個人檔案API指南
description: 即時客戶描述檔API可讓開發人員探索和使用描述檔資料，包括檢視描述檔、建立和更新合併原則、匯出或取樣描述檔資料，以及刪除不再需要或錯誤新增的描述檔資料。 請依照本指南，瞭解如何使用API執行關鍵作業。
exl-id: ce39b95b-cff7-46cf-a14c-8203017c8826
source-git-commit: 77bf6f4634987900bea1280290e8049120bb8856
workflow-type: tm+mt
source-wordcount: '894'
ht-degree: 0%

---

# [!DNL Real-time Customer Profile] API指南

[!DNL Real-time Customer Profile] 讓您全面瞭解Adobe Experience Platform地區的每位客戶。[!DNL Profile] 可讓您將來自多個通道的零散客戶資料（例如線上、離線、CRM和第三方資料）整合為一個統一的檢視，為每個客戶互動提供可操作的時間戳記帳戶。

[!DNL Real-time Customer Profile] API包含多個端點，如下所述。 如需詳細資訊，請造訪個別端點指南，並參閱[快速入門手冊](getting-started.md)，以取得必要標題、讀取範例API呼叫等重要資訊。

若要檢視所有可用端點和CRUD作業，請造訪[即時客戶個人資料API參考設定檔](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/real-time-customer-profile.yaml)。

有關在[!DNL Experience Platform] UI中使用[!DNL Real-time Customer Profile]資料的指南，請參閱[Profile使用手冊](../ui/user-guide.md)。

## (Alpha)計算屬性{#computed-attributes}

>[!IMPORTANT]
>
>計算屬性功能為alpha，並非所有使用者皆可使用。 檔案和功能可能會有所變更。

計算屬性是用於將事件級別資料聚合到配置檔案級別屬性的函式。 這些函式會自動計算，以便跨區段、啟動和個人化使用。

每個計算屬性都包含一個運算式（或「規則」），可評估傳入的資料並將產生的值儲存在描述檔屬性中。 這些計算可協助您輕鬆回答與期限購買值、購買間隔時間或應用程式開啟次數等相關的問題，而不需在每次需要資訊時手動執行複雜的計算。 然後，這些計算的屬性值可以在描述檔中檢視、用於建立區段，或透過許多不同的存取模式存取。

可以使用`config/computedAttributes`端點建立、查看、編輯和刪除計算屬性。 要瞭解如何使用計算屬性，請參閱[計算屬性概述](../computed-attributes/overview.md)。 有關API操作，請訪問[計算屬性API端點指南](../computed-attributes/ca-api.md)。

## 邊緣投影{#edge-projections}

Adobe Experience Platform讓資料可輕鬆在戰略性位置的伺服器（稱為「邊緣」）上存取，借以即時個人化客戶體驗。 [!DNL Real-time Customer Profile] API提供端點，以透過稱為「投影」的元件處理邊緣。 這包括確定應將哪些資料投影到每個邊的投影配置，以及定義投影路由位置的投影目標。 如需使用邊緣投影的詳細資訊，請造訪[投影組態和目標端點指南](edge-projections.md)。

## 實體（[!DNL Profile]存取） {#entities}

通過Adobe Experience Platform，您可以使用REST風格的API或用戶介面訪問[!DNL Real-time Customer Profile]資料。 要瞭解如何使用API訪問實體（更常稱為「配置式」），請遵循[實體端點指南](entities.md)中概述的步驟。 要使用[!DNL Platform] UI訪問配置檔案，請參閱[Profile使用手冊](../ui/user-guide.md)。

## 匯出工作（[!DNL Profile]匯出）{#profile-export}

[!DNL Real-time Customer Profile] 資料可匯出至資料集以進一步處理，例如匯出受眾區段以進行啟動或描述檔屬性以進行報告。讀者區段的匯出工作是[!DNL Adobe Experience Platform Segmentation Service] API的一部分，請閱讀[區段匯出工作端點指南](../../profile/api/export-jobs.md)以瞭解詳細資訊。 有關如何為配置檔案屬性建立和管理導出作業的逐步說明，請訪問[導出作業端點指南](export-jobs.md)。

## 合併策略{#merge-policies}

在[!DNL Experience Platform]中將多個來源的資料匯整在一起時，合併原則是[!DNL Platform]用來判斷資料的優先順序以及將哪些資料合併以建立個別客戶個人檔案的規則。 使用[!DNL Real-time Customer Profile] API，您可以建立新的合併原則、管理現有原則，以及為組織設定預設的合併原則。 要瞭解有關使用API使用合併策略的更多資訊，請訪問[合併策略端點指南](merge-policies.md)。

有關使用[!DNL Platform] UI使用合併策略的指南，請參閱[合併策略使用手冊](../ui/merge-policies.md)。

## 預覽範例狀態（[!DNL Profile]預覽）{#profile-preview}

當為「描述檔」啟用的資料被吸收到「Experience Platform」中時，它會儲存在「描述檔」資料儲存區中。 隨著描述檔儲存區中記錄數的增加或減少，會執行範例工作，其中包含資料儲存區中有多少描述檔片段和合併的描述檔的相關資訊。 使用描述檔API，您可以預覽最新成功的範例，以及依資料集和身分命名空間來列出描述檔散發。 要開始使用`/profilepreviewstatus`端點，請參閱[預覽示例狀態端點指南](preview-sample-status.md)。

## 配置式系統作業{#profile-system-jobs}

收錄在[!DNL Platform]中的啟用描述檔資料會儲存在[!DNL Data Lake]和[!DNL Real-time Customer Profile]資料儲存區中。 有時可能需要從[!DNL Profile]商店刪除資料集或批次，以移除您不再需要或錯誤新增的資料。 這需要使用API來建立[!DNL Profile System Job]（也稱為「[!DNL delete request]」），如有需要，可加以修改、監視或刪除。 要瞭解如何使用[!DNL Real-time Customer Profile] API中的`/system/jobs`端點處理刪除請求，請遵循[配置檔案系統作業端點指南](profile-system-jobs.md)中概述的步驟。

## 下一步 {#next-steps}

若要開始使用[!DNL Real-time Customer Profile] API進行呼叫，請閱讀[快速入門手冊](getting-started.md)，然後選取其中一個端點手冊，以瞭解如何使用特定的[!DNL Profile]相關端點。 若要使用[!DNL Experience Platform] UI處理[!DNL Profile]資料，請參閱[即時客戶資料使用指南](../ui/user-guide.md)。
