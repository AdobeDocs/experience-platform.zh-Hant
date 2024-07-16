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

# 開始使用[!DNL Policy Service] API

[!DNL Policy Service] API可讓您建立和管理與Adobe Experience Platform資料控管相關的各種資源。 本檔案提供嘗試呼叫[!DNL Policy Service] API之前需要瞭解的核心概念簡介。

## 先決條件

使用開發人員指南需要實際瞭解與使用資料控管功能有關的各種[!DNL Experience Platform]服務。 開始使用[!DNL Policy Service API]之前，請檢閱下列服務的檔案：

* [資料控管](../home.md)： [!DNL Experience Platform]強制資料使用規範所依據的架構。
* [[!DNL Experience Data Model (XDM) System]](../../xdm/home.md)： [!DNL Experience Platform]用來組織客戶體驗資料的標準化架構。
* [[!DNL Real-Time Customer Profile]](../../profile/home.md)：根據來自多個來源的彙總資料，提供統一的即時消費者設定檔。
* [沙箱](../../sandboxes/home.md)： [!DNL Experience Platform]提供可將單一[!DNL Platform]執行個體分割成個別虛擬環境的虛擬沙箱，以利開發及改進數位體驗應用程式。

## 讀取範例 API 呼叫

[!DNL Policy Service] API檔案提供範例API呼叫，示範如何格式化您的請求。 這些包括路徑、必要的標頭和正確格式化的請求承載。 此外，也提供 API 回應中傳回的範例 JSON。 如需檔案中所使用範例API呼叫慣例的詳細資訊，請參閱[!DNL Experience Platform]疑難排解指南中[如何讀取範例API呼叫](../../landing/troubleshooting.md#how-do-i-format-an-api-request)一節。

## 必要的標頭

API檔案也要求您完成[驗證教學課程](https://www.adobe.com/go/platform-api-authentication-en)，才能成功呼叫[!DNL Platform]端點。 完成驗證教學課程會提供[!DNL Experience Platform] API呼叫中每個必要標題的值，如下所示：

* `Authorization: Bearer {ACCESS_TOKEN}`
* `x-api-key: {API_KEY}`
* `x-gw-ims-org-id: {ORG_ID}`

[!DNL Experience Platform]中的所有資源（包括屬於資料控管的資源）都與特定的虛擬沙箱隔離。 對[!DNL Platform] API的所有請求都需要標頭，以指定將在其中執行作業的沙箱名稱：

* `x-sandbox-name: {SANDBOX_NAME}`

>[!NOTE]
>
>如需[!DNL Platform]中沙箱的詳細資訊，請參閱[沙箱概觀檔案](../../sandboxes/home.md)。

所有包含承載 (POST、PUT、PATCH) 的請求都需有額外的標頭：

* `Content-Type: application/json`

## 核心與自訂資源

在[!DNL Policy Service] API中，所有原則和行銷動作都稱為`core`或`custom`資源。

`core`資源是由Adobe定義及維護的資源，而`custom`資源是由您的組織建立及維護的資源，因此是唯一的且僅對您的組織可見。 因此，清單和查詢作業(`GET`)是唯一允許在`core`資源上執行的作業，而清單、查詢和更新作業（`POST`、`PUT`、`PATCH`和`DELETE`）則適用於`custom`資源。

## 後續步驟

若要開始使用原則服務API進行呼叫，請選取其中一個可用的端點指南。
