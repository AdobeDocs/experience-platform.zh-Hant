---
keywords: Experience Platform；配置檔案；即時客戶配置檔案；故障排除；API；統一配置檔案；統一配置檔案；配置檔案；rtcp；啟用配置檔案；啟用配置檔案
title: 即時客戶配置檔案API指南
description: 即時客戶配置檔案API允許開發人員瀏覽和使用配置檔案資料，包括查看配置檔案、建立和更新合併策略、導出或示例配置檔案資料以及刪除不再需要或錯誤添加的配置檔案資料。 請遵循本指南以了解如何使用 API 執行關鍵作業。
exl-id: ce39b95b-cff7-46cf-a14c-8203017c8826
source-git-commit: 9f00bff31f9e7d2da1294d3d1f24cba7870a4614
workflow-type: tm+mt
source-wordcount: '961'
ht-degree: 1%

---

# [!DNL Real-time Customer Profile] API指南

[!DNL Real-time Customer Profile] 使您能夠全面查看您在Adobe Experience Platform的每個客戶。 [!DNL Profile] 允許您將來自多個渠道（如線上、離線、CRM和第三方資料）的不同客戶資料整合到一個統一視圖中，為每個客戶交互提供一個可操作且時間戳記的帳戶。

的 [!DNL Real-time Customer Profile] API包括多個端點，如下所述。 請訪問各個端點指南以瞭解詳細資訊，並參閱 [入門指南](getting-started.md) 有關所需標頭、讀取示例API調用等的重要資訊。

要查看所有可用端點和CRUD操作，請訪問 [即時客戶配置檔案API參考瀏覽器](https://www.adobe.com/go/profile-apis-en)。

指南 [!DNL Real-time Customer Profile] 資料 [!DNL Experience Platform] UI，請參閱 [配置檔案使用手冊](../ui/user-guide.md)。

## (Alpha)計算屬性 {#computed-attributes}

>[!IMPORTANT]
>
>計算屬性功能位於Alpha中，並且不適用於所有用戶。 文檔和功能可能會更改。

計算屬性是用於將事件級資料聚合到配置檔案級屬性中的函式。 這些函式被自動計算，以便可以跨分段、激活和個性化使用。

每個計算屬性都包含一個表達式，即「規則」，用於計算傳入資料並將結果值儲存在配置檔案屬性中。 這些計算有助於您輕鬆回答與生命期購買值、購買間隔時間或應用程式數量等相關的問題，而無需在每次需要資訊時手動執行複雜的計算。 然後，可以在配置檔案中查看這些計算的屬性值，用於建立段，或通過許多不同的訪問模式訪問。

可以使用 `config/computedAttributes` 端點。 要瞭解如何使用計算屬性，請參閱 [計算屬性概述](../computed-attributes/overview.md)。 有關API操作，請訪問 [計算屬性API終結點指南](../computed-attributes/ca-api.md)。

## 邊緣投影 {#edge-projections}

Adobe Experience Platform通過使資料在戰略位置稱為「邊緣」的伺服器上輕鬆訪問，實現了客戶體驗的即時個性化。 的 [!DNL Real-time Customer Profile] API提供了通過稱為「投影」的元件處理邊的端點。 這包括確定應將哪些資料投影到每個邊緣的投影配置，以及定義投影路由位置的投影目標。 有關使用邊緣投影的詳細資訊，請訪問 [投影配置和目標端點指南](edge-projections.md)。

## 實體([!DNL Profile] 訪問) {#entities}

通過Adobe Experience Platform，你可以 [!DNL Real-time Customer Profile] 使用REST風格的API或用戶介面的資料。 要瞭解如何使用API訪問實體（通常稱為「配置檔案」），請遵循中介紹的步驟 [實體端點指南](entities.md)。 使用 [!DNL Platform] UI，請參閱 [配置檔案使用手冊](../ui/user-guide.md)。

## 導出作業([!DNL Profile] 導出) {#profile-export}

[!DNL Real-time Customer Profile] 資料可以導出到資料集以用於進一步處理，例如導出用於激活的受眾段或用於報告的配置檔案屬性。 導出受眾部分的作業是 [!DNL Adobe Experience Platform Segmentation Service] API，請閱讀 [分段導出作業終結點指南](../../profile/api/export-jobs.md) 來瞭解更多資訊。 有關如何建立和管理配置檔案屬性的導出作業的逐步說明，請訪問 [導出作業終結點指南](export-jobs.md)。

## 合併策略 {#merge-policies}

將來自多個源的資料放在一起 [!DNL Experience Platform]，合併策略是 [!DNL Platform] 用於確定資料的優先順序以及將組合哪些資料來建立單個客戶配置檔案。 使用 [!DNL Real-time Customer Profile] API，您可以建立新的合併策略、管理現有策略以及為組織設定預設合併策略。 要使用API使用合併策略，請訪問 [合併策略終結點指南](merge-policies.md)。

要瞭解有關合併策略及其在平台中的角色的詳細資訊，請首先閱讀 [合併策略概述](../merge-policies/overview.md)。

## 預覽示例狀態([!DNL Profile] 預覽) {#profile-preview}

當資料被接收到平台中時，將運行示例作業以更新配置檔案計數和其他與即時客戶配置檔案資料相關的度量。 此示例作業的結果可使用 `/previewsamplestatus` 端點，即時客戶配置檔案API的一部分。 此終結點還可用於按資料集和標識命名空間列出配置檔案分發，以及生成多個報告，以便能夠查看組織配置檔案儲存的組成。  開始使用 `/profilepreviewstatus` 端點，請參閱 [預覽示例狀態終結點指南](preview-sample-status.md)。

## 配置系統作業 {#profile-system-jobs}

接收到的啟用配置檔案的資料 [!DNL Platform] 儲存在 [!DNL Data Lake] 以及 [!DNL Real-time Customer Profile] 資料儲存。 有時可能需要從 [!DNL Profile] 儲存以刪除不再需要或錯誤添加的資料。 這要求使用API建立 [!DNL Profile System Job]，也稱為「[!DNL delete request]「 」，如果需要，可以修改、監視或刪除。 瞭解如何使用 `/system/jobs` 端點 [!DNL Real-time Customer Profile] API，按照中介紹的步驟操作 [profile system jobs endpoint buide（配置檔案系統作業終結點指南）](profile-system-jobs.md)。

## 更新配置檔案屬性 {#update-profile}

有時可能需要更新組織的配置檔案儲存中的資料。 例如，您可能需要更正記錄或更改屬性值。 這可以通過批處理接收來完成，並且需要使用upsert標籤配置啟用配置檔案的資料集。 有關如何配置資料集以進行屬性更新的詳細資訊，請參閱本教程以瞭解 [為配置檔案和upsert啟用資料集](../../catalog/datasets/enable-upsert.md)。

## 後續步驟 {#next-steps}

使用 [!DNL Real-time Customer Profile] API，讀取 [入門指南](getting-started.md) 然後選擇其中一個端點參考線以瞭解如何使用特定 [!DNL Profile] — 相關端點。 使用 [!DNL Profile] 使用 [!DNL Experience Platform] UI，請參閱 [即時客戶概要檔案使用手冊](../ui/user-guide.md)。
