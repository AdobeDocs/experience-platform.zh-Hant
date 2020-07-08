---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: DULE Policy Service API開發人員指南
topic: developer guide
translation-type: tm+mt
source-git-commit: bd9884a24c5301121f30090946ab24d9c394db1b
workflow-type: tm+mt
source-wordcount: '678'
ht-degree: 0%

---


# DULE [!DNL Policy Service] API開發人員指南

資料使用標籤與實施(DULE)是Adobe Experience Platform資料治理的核心機制。 DULE策略服務提供REST風格的API，允許您建立和管理資料使用策略，以確定可以針對已標籤有特定資料使用標籤的資料執行哪些行銷操作。

本檔案提供如何執行「原則服務API」中可用之關鍵作業的指示。 如果您尚未這麼做，請先檢閱資料管理概觀 [](../home.md) ，以熟悉DULE架構。 有關建立和實施DULE策略的逐步說明，請參見 [DULE策略教程](../policies/create.md)。

本檔案提供您在嘗試呼叫Policy Service API之前，需要瞭解的核心概念的簡介。

## DULE快速入門 [!DNL Policy Service]

開始使用之前，上的 [!DNL Policy Service]資料必 [!DNL Experience Platform] 須應用適當的DULE標籤。 有關將資料使用標籤應用於資料集和欄位的完整逐步說明，請參見 [DULE標籤使用手冊](../labels/user-guide.md)。

## 必要條件

本指南需要有效瞭解Adobe Experience Platform的下列元件：

* [資料治理](../home.md): 強制執行資料使用 [!DNL Experience Platform] 合規性的框架。
   * [DULE標籤](../labels/overview.md): 資料使用標籤會套用至「體驗資料模型」(XDM)資料欄位，指定資料存取限制。
* [體驗資料模型(XDM)系統](../../xdm/home.md): 組織客戶體驗資料 [!DNL Experience Platform] 的標準化架構。
* [即時客戶個人檔案](../../profile/home.md): 根據來自多個來源的匯整資料，提供統一、即時的消費者個人檔案。
* [沙盒](../../sandboxes/home.md): [!DNL Experience Platform] 提供虛擬沙盒，可將單一平台實例分割為獨立的虛擬環境，以協助開發和發展數位體驗應用程式。

## 讀取範例API呼叫

本指南提供範例API呼叫，以示範如何格式化您的請求。 這些包括路徑、必要標題和正確格式化的請求負載。 也提供API回應中傳回的範例JSON。 如需範例API呼叫檔案中所用慣例的詳細資訊，請參閱疑難排解指 [南中有關如何讀取範例API呼叫的](../../landing/troubleshooting.md#how-do-i-format-an-api-request)[!DNL Experience Platform] 章節。

## 收集必要標題的值

若要呼叫API，您必 [!DNL Platform] 須先完成驗證教 [學課程](../../tutorials/authentication.md)。 完成驗證教學課程後，將提供所有 [!DNL Experience Platform] API呼叫中每個必要標題的值，如下所示：

* 授權： 生產者 `{ACCESS_TOKEN}`
* x-api-key: `{API_KEY}`
* x-gw-ims-org-id: `{IMS_ORG}`

中的所有資 [!DNL Experience Platform]源(包括屬於這些資源 [!DNL Data Governance])都隔離到特定的虛擬沙盒。 對API的所 [!DNL Platform] 有請求都需要一個標題，該標題會指定要在中執行的操作的沙盒名稱：

* x-sandbox-name: `{SANDBOX_NAME}`

>[!NOTE]
>
>如需中沙盒的詳細資訊 [!DNL Platform]，請參閱沙 [盒概述檔案](../../sandboxes/home.md)。

所有包含裝載(POST、PUT、PATCH)的請求都需要額外的標題：

* 內容類型： application/json

## 核心與自訂資源

在 [!DNL Policy Service] API中，所有原則和行銷動作皆稱為 `core` 或資 `custom` 源。

資 `core` 源由Adobe定義和維護，而資源則由個別 `custom` 客戶建立和維護，因此，資源是獨一無二且僅對建立資源的IMS組織可見。 因此，清單和查閱作業(`GET`)是唯一允許對資源執行的作業 `core` ，而清單、查閱和更新作業(`POST`、 `PUT``PATCH`和 `DELETE`)則適用於資源 `custom` 。

## 策略狀態

資料使用原則可能有三種狀態： `DRAFT`、 `ENABLED`或 `DISABLED`。

預設情況下，只有「ENABLED」策略參與策略評估。

「DRAFT」策略也可以在策略評估中考慮，但只能通過設定查詢參數來考慮 `?includeDraft=true`。 有關策略評估的更多資訊，請參閱本文檔 [末尾的](../enforcement/overview.md) 「策略執行」一節。

## 行銷動作名稱 {#marketing-actions}

行銷動作名稱是行銷動作的唯一識別碼。 每個 `core` 行銷動作都有一個唯一名稱，可套用至所有IMS組織。 這些名稱由Adobe定義和維護。 同時，所有客戶定義的行銷動作(`custom` 資源)在您個別組織中都是獨一無二的，不會顯示或與其他IMS組織共用。

在API中使用行銷動作的步 [!DNL Policy Service] 驟，在本檔案稍後的「行 [銷動作](#marketing-actions) 」一節中有說明。

## 後續步驟

既然您已具備先決知識和認證，您就可以繼續閱讀本開發人員指南中提供的範例API呼叫：

* [行銷動作](marketing-actions.md)
* [策略](policies.md)