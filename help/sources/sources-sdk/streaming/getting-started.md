---
title: 自助源入門（流SDK）
description: 本文檔介紹了在嘗試使用自助源（Slef-Serve Sources，流式SDK）建立新源之前需要瞭解的先決條件資訊。
hide: true
hidefromtoc: true
exl-id: 6cc13279-ce0b-45bc-ad25-e2e6aafc2af0
source-git-commit: 05a7b73da610a30119b4719ae6b6d85f93cdc2ae
workflow-type: tm+mt
source-wordcount: '534'
ht-degree: 0%

---

# 自助源入門（流SDK）

自助源(Slefming SDK)允許您整合自己的源，將流資料帶到Adobe Experience Platform。 本文檔介紹了在嘗試呼叫至 [[!DNL Flow Service] API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/flow-service.yaml)。

## 高級流程

以下概述了在Experience Platform中配置源的逐步過程：

### 整合

* [為流式SDK建立新連接規範](create.md)。
* [使用新連接規範ID更新流規範](update-flow-specs.md)。
* [Test並提交流源](submit.md)。

### 文件

* 要開始記錄源，請閱讀 [建立自助源文檔概述](../documentation/doc-overview.md)。
* 閱讀上的指南 [使用GitHub Web介面](../documentation/github.md) 有關如何使用GitHub建立文檔的步驟。
* 閱讀上的指南 [使用文本編輯器](../documentation/text-editor.md) 有關如何使用本地電腦建立文檔的步驟。
* [使用Streaming SDK API文檔模板在API中記錄源](streaming-template-api.md)。
* [使用「流式SDK UI」文檔模板在UI中記錄源](streaming-template-ui.md)。

您還可以下載以下文檔模板：

* [API文檔模板](../assets/streaming/streaming-template-api.zip)
* [UI文檔模板](../assets/streaming/streaming-template-ui.zip)

## 先決條件

>[!IMPORTANT]
>
>您正在與Experience Platform整合的源必須能夠支援終結點可以訂閱到的Webhook以發送更新。

要使用自助源（流SDK），必須確保您有權訪問配置有Adobe Experience Platform源的沙盒組織。

本指南還要求對Adobe Experience Platform的下列組成部分有工作上的理解：

* [源](../../home.md):Experience Platform允許從各種源接收資料，同時讓您能夠使用平台服務構建、標籤和增強傳入資料。
* [沙箱](../../../sandboxes/home.md):Experience Platform提供虛擬沙箱，將單個平台實例分區為獨立的虛擬環境，以幫助開發和發展數字型驗應用程式。

## 讀取示例API調用

自助源（流SDK）和 [!DNL Flow Service] API文檔提供了示例API調用，以演示如何格式化請求。 這些包括路徑、必需的標頭和正確格式化的請求負載。 還提供了API響應中返回的示例JSON。 有關示例API調用文檔中使用的約定的資訊，請參見上的 [如何讀取示例API調用](../../../landing/troubleshooting.md#how-do-i-format-an-api-request) Experience Platform疑難解答指南。

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

要開始使用Self-Serve源(Streaming SDK)建立新源，請參閱上的教程 [建立新源](./create.md)。
