---
keywords: Experience Platform;home；熱門主題；DULE;dule
solution: Experience Platform
title: 原則服務API快速入門
topic-legacy: developer guide
description: Policy Service API可讓您建立和管理與Adobe Experience Platform資料治理相關的各種資源。 本檔案提供您在嘗試呼叫Policy Service API之前，需要瞭解的核心概念的簡介。
exl-id: 5539976c-8433-45af-a147-2ab82ae308b2
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '438'
ht-degree: 0%

---

# [!DNL Policy Service] API快速入門

[!DNL Policy Service] API可讓您建立並管理與Adobe Experience Platform[!DNL Data Governance]相關的各種資源。 本檔案提供您在嘗試呼叫[!DNL Policy Service] API之前，需要瞭解的核心概念的簡介。

## 先決條件

使用開發人員指南需要對使用「資料治理」功能時涉及的各種[!DNL Experience Platform]服務有良好的瞭解。 在開始使用[!DNL Policy Service API]之前，請先閱讀以下服務的說明檔案：

* [[!DNL Data Governance]](../home.md):強制執行資料使 [!DNL Experience Platform] 用合規性的框架。
* [[!DNL Experience Data Model (XDM) System]](../../xdm/home.md):組織客戶體驗資 [!DNL Experience Platform] 料的標準化架構。
* [[!DNL Real-time Customer Profile]](../../profile/home.md):根據來自多個來源的匯整資料，提供統一、即時的消費者個人檔案。
* [沙盒](../../sandboxes/home.md): [!DNL Experience Platform] 提供虛擬沙盒，可將單一執行個體分 [!DNL Platform] 割為不同的虛擬環境，以協助開發和發展數位體驗應用程式。

## 讀取範例API呼叫

[!DNL Policy Service] API檔案提供範例API呼叫，以示範如何格式化您的請求。 這些包括路徑、必要標題和正確格式化的請求負載。 也提供API回應中傳回的範例JSON。 如需範例API呼叫檔案中所用慣例的詳細資訊，請參閱[!DNL Experience Platform]疑難排解指南中[如何讀取範例API呼叫](../../landing/troubleshooting.md#how-do-i-format-an-api-request)一節。

## 必要的標題

API檔案也要求您完成[驗證教學課程](https://www.adobe.com/go/platform-api-authentication-en)，才能成功呼叫[!DNL Platform]端點。 完成驗證教學課程可為[!DNL Experience Platform] API呼叫中的每個必要標題提供值，如下所示：

* `Authorization: Bearer {ACCESS_TOKEN}`
* `x-api-key: {API_KEY}`
* `x-gw-ims-org-id: {IMS_ORG}`

[!DNL Experience Platform]中的所有資源（包括屬於[!DNL Data Governance]的資源）都隔離到特定的虛擬沙盒。 對[!DNL Platform] API的所有請求都需要一個標題，該標題指定要在中執行操作的沙盒的名稱：

* `x-sandbox-name: {SANDBOX_NAME}`

>[!NOTE]
>
>如需[!DNL Platform]中沙盒的詳細資訊，請參閱[沙盒概述檔案](../../sandboxes/home.md)。

所有包含裝載(POST、PUT、PATCH)的請求都需要額外的標題：

* `Content-Type: application/json`

## 核心與自訂資源

在[!DNL Policy Service] API中，所有原則和行銷動作都稱為`core`或`custom`資源。

`core` 資源是由Adobe定義和維護的資源，而 `custom` 資源則是由您的組織建立和維護的資源，因此它們是唯一的，僅對您的IMS組織可見。因此，清單和查閱操作(`GET`)是`core`資源所允許的唯一操作，而清單、查閱和更新操作（`POST`、`PUT`、`PATCH`和`DELETE`）可用於`custom`資源。

## 後續步驟

若要開始使用Policy Service API進行呼叫，請選取其中一個可用的端點指南。
