---
keywords: Experience Platform；配置；即時客戶配置；故障排除；API
title: 即時客戶配置檔案API入門
type: Documentation
description: 「配置檔案API入門」指南概述了使用即時客戶配置檔案API終結點對配置檔案資料執行基本CRUD操作時需要瞭解的關鍵概念和基本功能。
exl-id: 7e30610a-a7e7-43ab-a45d-fd84ef6e36ef
source-git-commit: 0f7ef438db5e7141197fb860a5814883d31ca545
workflow-type: tm+mt
source-wordcount: '411'
ht-degree: 0%

---

# 入門 [!DNL Real-Time Customer Profile] API {#getting-started}

使用Real-Time Customer Profile API終結點，您可以對Profile資料執行基本的CRUD操作，如配置計算屬性、訪問實體、導出配置檔案資料以及刪除不需要的資料集或批。

使用開發人員指南需要瞭解與 [!DNL Profile] 資料。 開始使用 [!DNL Real-Time Customer Profile] API，請查看以下服務的文檔：

* [[!DNL Real-Time Customer Profile]](../home.md):根據來自多個來源的聚合資料即時提供統一的客戶配置檔案。
* [[!DNL Adobe Experience Platform Identity Service]](../../identity-service/home.md):通過跨設備和系統橋接身份，更好地瞭解客戶及其行為。
* [[!DNL Adobe Experience Platform Segmentation Service]](../../segmentation/home.md):允許您從即時客戶配置檔案資料構建受眾段。
* [[!DNL Experience Data Model (XDM)]](../../xdm/home.md):平台組織客戶體驗資料的標準化框架。
* [[!DNL Sandboxes]](../../sandboxes/home.md): [!DNL Experience Platform] 提供虛擬沙箱，將單個沙箱 [!DNL Platform] 實例到獨立的虛擬環境，以幫助開發和發展數字型驗應用程式。

以下各節提供了您需要瞭解的其他資訊，以便成功撥打 [!DNL Profile] API終結點。

## 讀取示例API調用

的 [!DNL Real-Time Customer Profile] API文檔提供了示例API調用，以演示如何正確格式化請求。 這些包括路徑、必需的標頭和正確格式化的請求負載。 還提供了API響應中返回的示例JSON。 有關示例API調用文檔中使用的約定的資訊，請參見上的 [如何讀取示例API調用](../../landing/troubleshooting.md#how-do-i-format-an-api-request) 的 [!DNL Experience Platform] 疑難解答指南。

## 必需的標題

API文檔還要求您完成 [驗證教程](https://www.adobe.com/go/platform-api-authentication-en) 以便成功撥打 [!DNL Platform] 端點。 完成身份驗證教程將提供中每個必需標頭的值 [!DNL Experience Platform] API調用，如下所示：

* `Authorization: Bearer {ACCESS_TOKEN}`
* `x-api-key: {API_KEY}`
* `x-gw-ims-org-id: {ORG_ID}`

中的所有資源 [!DNL Experience Platform] 與特定虛擬沙箱隔離。 請求 [!DNL Platform] API需要一個標頭，該標頭指定操作將在以下位置進行的沙盒的名稱：

* `x-sandbox-name: {SANDBOX_NAME}`

有關中的沙箱的詳細資訊 [!DNL Platform]，請參見 [沙盒概述文檔](../../sandboxes/home.md)。

請求主體中具有負載的所有請求(如POST、PUT和PATCH呼叫)必須包括 `Content-Type` 標題。 在呼叫參數中提供特定於每個呼叫的接受值。

## 後續步驟

使用 [!DNL Real-Time Customer Profile] API，選擇可用的終結點指南之一。
