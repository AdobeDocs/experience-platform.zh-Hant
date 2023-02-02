---
title: 自助來源（串流SDK）快速入門
description: 本檔案簡介您在嘗試使用自助來源（串流SDK）建立新來源之前，需要知道的先決條件資訊。
hide: true
hidefromtoc: true
source-git-commit: 7744fef9751212a40f8f20df52812d38130c42fc
workflow-type: tm+mt
source-wordcount: '534'
ht-degree: 0%

---

# 自助來源（串流SDK）快速入門

自助來源（串流SDK）可讓您整合自己的來源，將串流資料帶入Adobe Experience Platform。 本檔案簡介您在嘗試呼叫 [[!DNL Flow Service] API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/flow-service.yaml).

## 高級流程

在Experience Platform中配置源的逐步過程如下：

### 整合

* [為串流SDK建立新的連線規格](create.md).
* [使用新的連接規範ID更新流規範](update-flow-specs.md).
* [測試並提交您的串流來源](submit.md).

### 文件

* 要開始記錄源，請閱讀 [自助源建立文檔概述](../documentation/doc-overview.md).
* 閱讀指南 [使用GitHub網頁介面](../documentation/github.md) 以了解如何使用GitHub建立檔案的步驟。
* 閱讀指南 [使用文字編輯器](../documentation/text-editor.md) 以了解如何使用本機電腦建立檔案的步驟。
* [使用串流SDK API檔案範本，在API中記錄您的來源](streaming-template-api.md).
* [使用串流SDK UI檔案範本，在UI中記錄您的來源](streaming-template-ui.md).

您也可以下載下列檔案範本：

* [API檔案範本](../assets/streaming/streaming-template-api.zip)
* [UI檔案範本](../assets/streaming/streaming-template-ui.zip)

## 先決條件

>[!IMPORTANT]
>
>您與Experience Platform整合的來源必須能夠支援端點可訂閱的Webhook，以傳送更新。

若要使用自助來源（串流SDK），您必須確定可存取已布建Adobe Experience Platform來源的沙箱組織。

本指南也需要妥善了解下列Adobe Experience Platform元件：

* [來源](../../home.md):Experience Platform可讓您從各種來源擷取資料，同時使用Platform服務來建構、加標籤及增強傳入資料。
* [沙箱](../../../sandboxes/home.md):Experience Platform提供可將單一Platform執行個體分割成個別虛擬環境的虛擬沙箱，以協助開發及改進數位體驗應用程式。

## 讀取範例API呼叫

自助來源（串流SDK）和 [!DNL Flow Service] API檔案提供範例API呼叫，以示範如何設定請求格式。 這些功能包括路徑、必要標題和格式正確的請求裝載。 也提供API回應中傳回的範例JSON。 如需範例API呼叫檔案中所使用慣例的相關資訊，請參閱 [如何閱讀API呼叫範例](../../../landing/troubleshooting.md#how-do-i-format-an-api-request) Experience Platform疑難排解指南中。

## 收集必要標題的值

若要呼叫Platform API，您必須先完成 [驗證教學課程](https://www.adobe.com/go/platform-api-authentication-en). 完成驗證教學課程會提供所有 [!DNL Experience Platform] API呼叫，如下所示：

* `Authorization: Bearer {ACCESS_TOKEN}`
* `x-api-key: {API_KEY}`
* `x-gw-ims-org-id: {ORG_ID}`

Platform中的所有資源，包括 [!DNL Flow Service]，會與特定虛擬沙箱隔離。 對Platform API提出的所有請求都需要標題，以指定作業將在下列位置進行的沙箱名稱：

* `x-sandbox-name: {SANDBOX_NAME}`

>[!NOTE]
>
>如需Platform中沙箱的詳細資訊，請參閱 [沙箱檔案](../../../sandboxes/home.md).

所有包含裝載(POST、PUT、PATCH)的請求都需要額外的標題：

* `Content-Type: application/json`

## 後續步驟

若要開始使用自助來源（串流SDK）建立新來源，請參閱以下的教學課程： [建立新源](./create.md).
