---
keywords: Experience Platform;profile;real-time customer profile;troubleshooting;API
solution: Adobe Experience Platform
title: 即時客戶個人檔案API開發人員指南
topic: guide
translation-type: tm+mt
source-git-commit: 8449681a7fd0fc5dccf4837a1e8e512f1e2f2601
workflow-type: tm+mt
source-wordcount: '954'
ht-degree: 0%

---


# 即時客戶個人檔案API開發人員指南

即時客戶個人檔案可讓您在Adobe Experience Platform中全面瞭解每個客戶。 個人檔案可讓您將來自多個通道（例如線上、離線、CRM和第三方資料）的分散客戶資料整合為一個統一的檢視，提供每個客戶互動的可操作的時間戳記帳戶。

## 快速入門 {#getting-started}

使用Real-time Customer Profile API，您可以對Profile資源執行基本的CRUD操作，如配置計算屬性、訪問實體、導出Profile資料以及刪除不需要的資料集或批。

使用本開發人員指南需要對使用描述檔資料時涉及的各種Adobe Experience Platform服務有良好的瞭解。 在開始使用即時客戶設定檔API之前，請先檢閱下列服務的檔案：

* [即時客戶個人檔案](../home.md): 根據來自多個來源的匯整資料，即時提供統一的客戶個人檔案。
* [Adobe Experience Platform Identity Service](../../identity-service/home.md): 跨裝置和系統橋接身分，以更全面地瞭解客戶及其行為。
* [Adobe Experience Platform細分服務](../../segmentation/home.md): 可讓您從即時客戶個人檔案資料建立受眾細分。
* [體驗資料模型(XDM)](../../xdm/home.md): 平台組織客戶體驗資料的標準化架構。
* [沙盒](../../sandboxes/home.md): Experience Platform提供虛擬沙盒，可將單一Platform實例分割為不同的虛擬環境，以協助開發和發展數位體驗應用程式。

以下各節提供您必須知道的其他資訊，以便成功呼叫描述檔API端點。

### 讀取範例API呼叫

即時客戶設定檔API檔案提供範例API呼叫，以示範如何正確格式化請求。 這些包括路徑、必要標題和正確格式化的請求負載。 也提供API回應中傳回的範例JSON。 如需範例API呼叫檔案中所用慣例的詳細資訊，請參閱「Experience Platform疑難排解指 [南」中有關如何讀取範例API呼叫的章節](../../landing/troubleshooting.md#how-do-i-format-an-api-request) 。

### 必要的標題

API檔案也要求您完成驗證教學課 [程](../../tutorials/authentication.md) ，才能成功呼叫平台端點。 完成驗證教學課程時，會針對Experience Platform API呼叫中的每個必要標題提供值，如下所示：

* 授權： 生產者 `{ACCESS_TOKEN}`
* x-api-key: `{API_KEY}`
* x-gw-ims-org-id: `{IMS_ORG}`

Experience Platform中的所有資源都隔離至特定的虛擬沙盒。 對平台API的請求需要一個標題，該標題指定要在中執行操作的沙盒名稱：

* x-sandbox-name: `{SANDBOX_NAME}`

如需平台中沙盒的詳細資訊，請參閱沙盒 [概觀檔案](../../sandboxes/home.md)。

請求正文中包含裝載的所有請求（例如POST、PUT和PATCH呼叫）都必須包含標 `Content-Type` 題。 在呼叫參數中提供每個呼叫的接受值。

## (Alpha)計算屬性

>[!IMPORTANT]
>計算屬性功能為alpha，並非所有使用者皆可使用。 檔案和功能可能會有所變更。

計算屬性可讓您根據其他值、計算和運算式自動計算欄位的值。 計算屬性在描述檔層級上運作，這表示您可以匯總所有記錄和事件的值。

每個計算屬性都包含一個運算式，即&#39;rule&#39;，可評估傳入的資料，並將產生的值儲存在描述檔屬性或事件中。 這些計算可協助您輕鬆回答與期限購買值、購買間隔時間或應用程式開啟次數等相關的問題，而不需在每次需要資訊時手動執行複雜的計算。

您可以使用端點建立、查看、編輯和刪除計算屬 `config/computedAttributes` 性。 若要瞭解如何使用這些端點，請造 [訪計算屬性子指南](computed-attributes.md)。

## 邊緣投影

Adobe Experience Platform讓資料可輕鬆在戰略性位置的伺服器（稱為「邊緣」）上存取，讓客戶體驗即時個人化。 即時客戶個人檔案API提供端點，以透過稱為「預測」的元件處理邊緣。 這包括確定應將哪些資料投影到每個邊的投影配置，以及定義投影路由位置的投影目標。

如需使用邊緣投影的詳細資訊，請造訪 [邊緣投影子指南](edge-projections.md)。

## 實體

透過Adobe Experience Platform，您可以使用REST風格的API或使用者介面存取即時客戶個人檔案資料。 若要瞭解如何使用API存取實體（更常稱為「設定檔」），請遵循實體子指南 [中的步驟](entities.md)。

## 合併原則

在Experience Platform中將多個來源的資料匯整在一起時，合併原則是平台用來決定資料的優先順序以及將哪些資料合併以建立個別客戶個人檔案的規則。

使用「即時客戶個人檔案API」，您可以建立新的合併原則、管理現有原則，以及為組織設定預設的合併原則。 若要進一步瞭解如何使用API來處理合併原則，請造 [訪合併原則子指南](merge-policies.md)。

有關使用平台UI使用合併策略的指南，請參閱合 [並策略使用手冊](../ui/merge-policies.md)。

## 描述檔系統工作

Data Lake和即時客戶個人檔案資料儲存中會儲存在Platform中。 有時可能需要從描述檔存放區刪除資料集或批次，以移除您不再需要或錯誤新增的資料。 這需要使用API來建立描述檔系統工作（稱為「刪除請求」），如有需要，也可加以修改、監視或刪除。

若要瞭解如何使用即時客戶描述檔 `/system/jobs` API中的端點處理刪除請求，請遵循描述檔系統作業子指 [南中概述的步驟](profile-system-jobs.md)。

## 後續步驟

若要開始使用即時客戶描述檔API進行呼叫，請選取其中一個子指南，以瞭解如何使用特定的描述檔相關端點。 若要進一步瞭解如何使用平台UI使用描述檔資料，請參 [閱即時客戶描述檔使用指南](../ui/user-guide.md)。