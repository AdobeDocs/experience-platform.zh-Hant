---
keywords: Experience Platform；首頁；熱門主題；DULE;DULE
solution: Experience Platform
title: 策略服務API快速入門
topic-legacy: developer guide
description: Policy Service API允許您建立和管理與Adobe Experience Platform Data Governance相關的各種資源。 本文檔介紹了在嘗試調用策略服務API之前需要知道的核心概念。
exl-id: 5539976c-8433-45af-a147-2ab82ae308b2
source-git-commit: 34e0381d40f884cd92157d08385d889b1739845f
workflow-type: tm+mt
source-wordcount: '444'
ht-degree: 0%

---

# 開始使用 [!DNL Policy Service] API

此 [!DNL Policy Service] API可讓您建立及管理Adobe Experience Platform資料控管的各種資源。 本檔案簡介您在嘗試呼叫 [!DNL Policy Service] API。

## 先決條件

使用開發人員指南時，您必須妥善了解 [!DNL Experience Platform] 與資料控管功能搭配使用的服務。 開始使用之前 [!DNL Policy Service API]，請查閱以下服務的檔案：

* [資料控管](../home.md):框架 [!DNL Experience Platform] 強制資料使用合規性。
* [[!DNL Experience Data Model (XDM) System]](../../xdm/home.md):標準化框架 [!DNL Experience Platform] 組織客戶體驗資料。
* [[!DNL Real-Time Customer Profile]](../../profile/home.md):根據來自多個來源的匯總資料，提供統一的即時消費者設定檔。
* [沙箱](../../sandboxes/home.md): [!DNL Experience Platform] 提供可分割單一沙箱的虛擬沙箱 [!DNL Platform] 例項放入個別的虛擬環境，以協助開發及改進數位體驗應用程式。

## 讀取範例API呼叫

此 [!DNL Policy Service] API檔案提供範例API呼叫，以示範如何設定請求格式。 這些功能包括路徑、必要標題和格式正確的請求裝載。 也提供API回應中傳回的範例JSON。 如需範例API呼叫檔案中所使用慣例的相關資訊，請參閱 [如何閱讀API呼叫範例](../../landing/troubleshooting.md#how-do-i-format-an-api-request) 在 [!DNL Experience Platform] 疑難排解指南。

## 必要標題

API檔案也要求您完成 [驗證教學課程](https://www.adobe.com/go/platform-api-authentication-en) 以便成功呼叫 [!DNL Platform] 端點。 完成驗證教學課程，可提供 [!DNL Experience Platform] API呼叫，如下所示：

* `Authorization: Bearer {ACCESS_TOKEN}`
* `x-api-key: {API_KEY}`
* `x-gw-ims-org-id: {ORG_ID}`

中的所有資源 [!DNL Experience Platform]，包括屬於資料控管的，會隔離至特定的虛擬沙箱。 所有請求 [!DNL Platform] API需要標頭，以指定要在中執行操作的沙箱名稱：

* `x-sandbox-name: {SANDBOX_NAME}`

>[!NOTE]
>
>如需中沙箱的詳細資訊，請參閱 [!DNL Platform]，請參閱 [沙箱概述檔案](../../sandboxes/home.md).

所有包含裝載(POST、PUT、PATCH)的請求都需要額外的標題：

* `Content-Type: application/json`

## 核心與自訂資源

在 [!DNL Policy Service] API、所有原則和行銷動作皆可稱為 `core` 或 `custom` 資源。

`core` 資源是指由Adobe定義和維護的資源，然而 `custom` 資源是由您的組織建立和維護的資源，因此只有您的IMS組織可看見。 因此，請列出和查閱操作(`GET`)是 `core` 資源，則列出、查詢和更新操作(`POST`, `PUT`, `PATCH`，和 `DELETE`)可供 `custom` 資源。

## 後續步驟

要開始使用策略服務API進行調用，請選擇可用的終結點指南之一。
