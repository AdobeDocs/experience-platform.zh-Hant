---
title: 自助來源快速入門(串流SDK)
description: 本文簡介在嘗試使用自助來源(串流SDK)建立新來源之前，需要知道的先決條件資訊。
exl-id: 6cc13279-ce0b-45bc-ad25-e2e6aafc2af0
badge: Beta
source-git-commit: 863889984e5e77770638eb984e129e720b3d4458
workflow-type: tm+mt
source-wordcount: '543'
ht-degree: 12%

---

# 自助來源快速入門(串流SDK)

>[!NOTE]
>
>自助來源串流SDK為測試版。 如需使用Beta版標籤來源的相關資訊，請參閱[來源概觀](../../home.md#terms-and-conditions)。

自助來源(串流SDK)可讓您整合自己的來源，將串流資料引進Adobe Experience Platform。 本檔案提供嘗試呼叫[[!DNL Flow Service] API](https://developer.adobe.com/experience-platform-apis/references/flow-service/)之前需要瞭解的核心概念簡介。

## 高階流程

以Experience Platform設定來源的逐步流程概述如下：

### 整合

* [建立串流SDK的新連線規格](create.md)。
* [使用新的連線規格ID](update-flow-specs.md)更新串流流程規格。
* [測試並提交您的串流來源](submit.md)。

### 文件

* 若要開始記錄您的來源，請閱讀建立自助來原始檔](../documentation/doc-overview.md)的[總覽。
* 閱讀[使用GitHub網頁介面](../documentation/github.md)的指南，以瞭解如何使用GitHub建立檔案的步驟。
* 閱讀[使用文字編輯器](../documentation/text-editor.md)的指南，瞭解如何使用本機電腦建立檔案的步驟。
* [使用串流SDK API檔案範本在API中記錄您的來源](streaming-template-api.md)。
* [使用串流SDK UI檔案範本在UI中記錄您的來源](streaming-template-ui.md)。

您也可以下載下列檔案範本：

* [API檔案範本](../assets/streaming/streaming-template-api.zip)
* [UI檔案範本](../assets/streaming/streaming-template-ui.zip)

## 先決條件

>[!IMPORTANT]
>
>您與Experience Platform整合的來源必須能夠支援端點可訂閱的webhook，以傳送更新。

若要使用自助來源(串流SDK)，您必須確保您有權存取以Adobe Experience Platform來源布建的沙箱組織。

本指南也需要您實際瞭解下列Adobe Experience Platform元件：

* [來源](../../home.md)：Experience Platform允許從各種來源擷取資料，同時讓您能夠使用Platform服務來建構、加標籤以及增強傳入的資料。
* [沙箱](../../../sandboxes/home.md)：Experience Platform提供的虛擬沙箱可將單一Platform執行個體分割成個別的虛擬環境，以利開發及改進數位體驗應用程式。

## 讀取範例 API 呼叫

自助來源(串流SDK)和[!DNL Flow Service] API檔案提供範例API呼叫，示範如何格式化您的請求。 這些包括路徑、必要的標頭和正確格式化的請求承載。 此外，也提供 API 回應中傳回的範例 JSON。 如需檔案中所使用之範例API呼叫慣例的詳細資訊，請參閱Experience Platform疑難排解指南中有關[如何讀取範例API呼叫](../../../landing/troubleshooting.md#how-do-i-format-an-api-request)的章節。

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

若要開始使用自助式來源(串流SDK)建立新來源，請參閱[建立新來源](./create.md)的相關教學課程。
