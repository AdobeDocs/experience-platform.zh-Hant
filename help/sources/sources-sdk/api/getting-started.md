---
keywords: Experience Platform；首頁；熱門主題；來源；聯結器；來源聯結器；來源sdk；sdk；SDK
solution: Experience Platform
title: 自助來源快速入門(批次SDK)
description: 本文介紹嘗試使用自助來源(批次SDK)建立新來源之前，需要知道的先決條件資訊。
exl-id: ba131442-ff20-4854-87fe-918aa313382d
source-git-commit: 863889984e5e77770638eb984e129e720b3d4458
workflow-type: tm+mt
source-wordcount: '375'
ht-degree: 17%

---

# 自助來源快速入門(批次SDK)

自助來源(批次SDK)可讓您整合自己的REST型來源，以將批次資料引進Adobe Experience Platform。 本檔案提供嘗試呼叫[[!DNL Flow Service] API](https://developer.adobe.com/experience-platform-apis/references/flow-service/)之前需要瞭解的核心概念簡介。

## 先決條件

若要使用自助式來源(批次SDK)，您必須確保您有權存取以Adobe Experience Platform來源布建的組織沙箱。

本指南也需要您實際瞭解下列Adobe Experience Platform元件：

* [來源](../../home.md)：Experience Platform允許從各種來源擷取資料，同時讓您能夠使用Platform服務來建構、加標籤以及增強傳入的資料。
* [沙箱](../../../sandboxes/home.md)：Experience Platform提供的虛擬沙箱可將單一Platform執行個體分割成個別的虛擬環境，以利開發及改進數位體驗應用程式。

## 讀取範例 API 呼叫

自助來源(批次SDK)和[!DNL Flow Service] API檔案提供範例API呼叫，示範如何格式化您的請求。 這些包括路徑、必要的標頭和正確格式化的請求承載。 此外，也提供 API 回應中傳回的範例 JSON。 如需檔案中所使用之範例API呼叫慣例的詳細資訊，請參閱Experience Platform疑難排解指南中有關[如何讀取範例API呼叫](../../../landing/troubleshooting.md#how-do-i-format-an-api-request)的章節。

## 收集所需標頭的值

若要呼叫Platform API，您必須先完成[驗證教學課程](https://www.adobe.com/go/platform-api-authentication-en)。 完成驗證教學課程會提供所有 [!DNL Experience Platform] API 呼叫中每個必要標頭的值，如下所示：

* `Authorization: Bearer {ACCESS_TOKEN}`
* `x-api-key: {API_KEY}`
* `x-gw-ims-org-id: {ORG_ID}`

Platform中的所有資源（包括屬於[!DNL Flow Service]的資源）都與特定的虛擬沙箱隔離。 對Platform API的所有請求都需要標頭，以指定將在其中進行操作的沙箱名稱：

* `x-sandbox-name: {SANDBOX_NAME}`

>[!NOTE]
>
>如需Platform中沙箱的詳細資訊，請參閱[沙箱檔案](../../../sandboxes/home.md)。

所有包含承載 (POST、PUT、PATCH) 的請求都需有額外的標頭：

* `Content-Type: application/json`

## 後續步驟

若要開始使用自助來源(批次SDK)建立新來源，請參閱[建立新來源](./create.md)的教學課程。
