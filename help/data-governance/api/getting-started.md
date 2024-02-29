---
keywords: Experience Platform；首頁；熱門主題；DULE；dule
solution: Experience Platform
title: 開始使用原則服務API
description: 原則服務API可讓您建立和管理與Adobe Experience Platform資料控管相關的各種資源。 本檔案介紹嘗試呼叫原則服務API之前需要瞭解的核心概念。
role: Developer
exl-id: 5539976c-8433-45af-a147-2ab82ae308b2
source-git-commit: c16ce1020670065ecc5415bc3e9ca428adbbd50c
workflow-type: tm+mt
source-wordcount: '439'
ht-degree: 8%

---

# 開始使用 [!DNL Policy Service] API

此 [!DNL Policy Service] API可讓您建立和管理與Adobe Experience Platform資料控管相關的各種資源。 本檔案介紹嘗試呼叫 [!DNL Policy Service] API。

## 先決條件

使用開發人員指南需要實際瞭解各種 [!DNL Experience Platform] 與資料控管功能搭配使用的服務。 開始使用之前 [!DNL Policy Service API]，請檢閱以下服務的檔案：

* [資料控管](../home.md)：作為依據的框架 [!DNL Experience Platform] 強制資料使用規範。
* [[!DNL Experience Data Model (XDM) System]](../../xdm/home.md)：作為依據的標準化架構 [!DNL Experience Platform] 組織客戶體驗資料。
* [[!DNL Real-Time Customer Profile]](../../profile/home.md)：根據來自多個來源的彙總資料，提供統一的即時消費者個人檔案。
* [沙箱](../../sandboxes/home.md)： [!DNL Experience Platform] 提供分割單一區域的虛擬沙箱 [!DNL Platform] 將執行個體整合至個別的虛擬環境中，協助開發及改進數位體驗應用程式。

## 讀取範例 API 呼叫

此 [!DNL Policy Service] API檔案提供API呼叫範例，示範如何格式化您的請求。 這些包括路徑、必要的標頭和正確格式化的請求承載。 此外，也提供 API 回應中傳回的範例 JSON。 如需檔案中用於範例API呼叫的慣例相關資訊，請參閱以下章節： [如何讀取範例API呼叫](../../landing/troubleshooting.md#how-do-i-format-an-api-request) 在 [!DNL Experience Platform] 疑難排解指南。

## 必要的標頭

此API檔案也要求您完成 [驗證教學課程](https://www.adobe.com/go/platform-api-authentication-en) 以便成功呼叫 [!DNL Platform] 端點。 完成驗證教學課程，在中提供每個所需標題的值 [!DNL Experience Platform] API呼叫，如下所示：

* `Authorization: Bearer {ACCESS_TOKEN}`
* `x-api-key: {API_KEY}`
* `x-gw-ims-org-id: {ORG_ID}`

中的所有資源 [!DNL Experience Platform]包括屬於資料控管的，會隔離至特定的虛擬沙箱。 所有要求至 [!DNL Platform] API需要標頭，用以指定將進行作業的沙箱名稱：

* `x-sandbox-name: {SANDBOX_NAME}`

>[!NOTE]
>
>如需中沙箱的詳細資訊 [!DNL Platform]，請參閱 [沙箱概述檔案](../../sandboxes/home.md).

所有包含承載 (POST、PUT、PATCH) 的請求都需有額外的標頭：

* `Content-Type: application/json`

## 核心與自訂資源

在 [!DNL Policy Service] API，所有原則和行銷動作稱為 `core` 或 `custom` 資源。

`core` 資源是由Adobe定義及維護的資源，而 `custom` 資源是由您組織建立及維護的資源，因此是唯一的且僅供您的組織檢視。 因此，列出和查詢作業(`GET`)是唯一允許對執行的作業 `core` 資源，而列出、查詢及更新作業(`POST`， `PUT`， `PATCH`、和 `DELETE`)可用於 `custom` 資源。

## 後續步驟

若要開始使用原則服務API進行呼叫，請選取其中一個可用的端點指南。
