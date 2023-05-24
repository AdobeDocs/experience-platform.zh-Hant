---
keywords: Experience Platform；首頁；熱門主題；源；連接器；源連接器；源sdk;sdk;SDK
solution: Experience Platform
title: 自助源入門（批處理SDK）
description: 本文檔介紹了在嘗試使用自助源（批處理SDK）建立新源之前需要瞭解的先決條件資訊。
exl-id: ba131442-ff20-4854-87fe-918aa313382d
source-git-commit: 2a5d545db18a5dd33c5ff2ac5c543ec35db4ca00
workflow-type: tm+mt
source-wordcount: '386'
ht-degree: 0%

---

# 自助源入門（批處理SDK）

自助源（批處理SDK）允許您整合您自己的基於REST的源，以將批處理資料帶到Adobe Experience Platform。 本文檔介紹了在嘗試呼叫至 [[!DNL Flow Service] API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/flow-service.yaml)。

## 先決條件

要使用自助源（批處理SDK），必須確保您有權訪問配置有Adobe Experience Platform源的組織沙盒。

本指南還要求對Adobe Experience Platform的下列組成部分有工作上的理解：

* [源](../../home.md):Experience Platform允許從各種源接收資料，同時讓您能夠使用平台服務構建、標籤和增強傳入資料。
* [沙箱](../../../sandboxes/home.md):Experience Platform提供虛擬沙箱，將單個平台實例分區為獨立的虛擬環境，以幫助開發和發展數字型驗應用程式。

## 讀取示例API調用

自助源(Batch SDK)和 [!DNL Flow Service] API文檔提供了示例API調用，以演示如何格式化請求。 這些包括路徑、必需的標頭和正確格式化的請求負載。 還提供了API響應中返回的示例JSON。 有關示例API調用文檔中使用的約定的資訊，請參見上的 [如何讀取示例API調用](../../../landing/troubleshooting.md#how-do-i-format-an-api-request) Experience Platform疑難解答指南。

## 收集所需標題的值

要調用平台API，必須先完成 [驗證教程](https://www.adobe.com/go/platform-api-authentication-en)。 完成身份驗證教程將提供所有中每個必需標頭的值 [!DNL Experience Platform] API調用，如下所示：

* `Authorization: Bearer {ACCESS_TOKEN}`
* `x-api-key: {API_KEY}`
* `x-gw-ims-org-id: {ORG_ID}`

平台中的所有資源，包括屬於 [!DNL Flow Service]，與特定虛擬沙箱隔離。 所有對平台API的請求都需要一個標頭，該標頭指定操作將在以下位置進行的沙盒的名稱：

* `x-sandbox-name: {SANDBOX_NAME}`

>[!NOTE]
>
>有關平台中沙箱的詳細資訊，請參閱 [沙盒文檔](../../../sandboxes/home.md)。

包含負載(POST、PUT、PATCH)的所有請求都需要附加的標頭：

* `Content-Type: application/json`

## 後續步驟

要開始使用自助源(Batch SDK)建立新源，請參閱上的教程 [建立新源](./create.md)。
