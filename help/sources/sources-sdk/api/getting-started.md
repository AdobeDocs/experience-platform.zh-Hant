---
keywords: Experience Platform；首頁；熱門主題；來源；連接器；來源連接器；來源sdk;sdk; SDK
solution: Experience Platform
title: 來源SDK快速入門（測試版）
topic-legacy: developer guide
description: 本檔案簡介您在嘗試使用來源SDK建立新來源之前，需要知道的先決條件資訊。
hide: true
hidefromtoc: true
source-git-commit: d4b5b54be9fa2b430a3b45eded94a523b6bd4ef8
workflow-type: tm+mt
source-wordcount: '400'
ht-degree: 0%

---

# 來源SDK快速入門（測試版）

>[!IMPORTANT]
>
>Sources SDK目前仍在測試階段，而您的組織可能尚未取得存取權。 本檔案所述的功能可能會有所變更。

Sources SDK可讓您整合自己的REST型來源，將資料匯入Adobe Experience Platform。 本檔案簡介您在嘗試呼叫 [[!DNL Flow Service] API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/flow-service.yaml).

## 先決條件

若要使用來源SDK，您必須確保擁有布建有Adobe Experience Platform來源的IMS組織沙箱存取權。

本指南也需要妥善了解下列Adobe Experience Platform元件：

* [來源](../../home.md):Experience Platform可讓您從各種來源擷取資料，同時使用Platform服務來建構、加標籤及增強傳入資料。
* [沙箱](../../../sandboxes/home.md):Experience Platform提供可將單一Platform執行個體分割成個別虛擬環境的虛擬沙箱，以協助開發及改進數位體驗應用程式。

## 讀取範例API呼叫

來源SDK和 [!DNL Flow Service] API檔案提供範例API呼叫，以示範如何設定請求格式。 這些功能包括路徑、必要標題和格式正確的請求裝載。 也提供API回應中傳回的範例JSON。 如需範例API呼叫檔案中所使用慣例的相關資訊，請參閱 [如何閱讀API呼叫範例](../../../landing/troubleshooting.md#how-do-i-format-an-api-request) Experience Platform疑難排解指南中。

## 收集必要標題的值

若要呼叫Platform API，您必須先完成 [驗證教學課程](https://www.adobe.com/go/platform-api-authentication-en). 完成驗證教學課程會提供所有 [!DNL Experience Platform] API呼叫，如下所示：

* `Authorization: Bearer {ACCESS_TOKEN}`
* `x-api-key: {API_KEY}`
* `x-gw-ims-org-id: {IMS_ORG}`

Platform中的所有資源，包括 [!DNL Flow Service]，會與特定虛擬沙箱隔離。 對Platform API提出的所有請求都需要標題，以指定作業將在下列位置進行的沙箱名稱：

* `x-sandbox-name: {SANDBOX_NAME}`

>[!NOTE]
>
>如需Platform中沙箱的詳細資訊，請參閱 [沙箱檔案](../../../sandboxes/home.md).

所有包含裝載(POST、PUT、PATCH)的請求都需要額外的標題：

* `Content-Type: application/json`

## 後續步驟

若要開始使用Sources SDK建立新來源，請參閱以下主題的教學課程： [建立新源](./create.md).