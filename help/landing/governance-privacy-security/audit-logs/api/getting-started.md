---
title: 審計查詢API入門
description: 審計查詢API允許您檢索各種Adobe Experience Platform功能的度量資料。 本文檔介紹了在嘗試調用審計查詢API之前需要瞭解的核心概念。
exl-id: 20eab0a8-98f7-4fee-8f91-88324e54ab18
source-git-commit: c2c5778e0a3fff7f488ad7a672123c813cca59f1
workflow-type: tm+mt
source-wordcount: '392'
ht-degree: 9%

---

# 審計查詢API入門

Adobe Experience Platform允許您以審計事件日誌的形式審計用戶活動中的各種服務和功能。 稽核記錄中所記錄的每個動作都包含中繼資料，其指出動作類型、日期和時間、執行動作之使用者的電子郵件 ID，以及與動作類型相關的其他屬性。

「審計查詢API」允許您以審計事件日誌的形式審計用戶活動中的各種服務和功能。 本文檔介紹了在嘗試調用審計查詢API之前需要瞭解的核心概念。

## 先決條件

要管理審計事件，您必須 **[!UICONTROL 查看用戶活動日誌]** 授予的訪問控制權限(在 [!UICONTROL 資料治理] )。 要瞭解如何管理平台功能的各個權限，請參閱 [訪問控制文檔](../../../../access-control/home.md)。

### 讀取示例API調用

本指南提供了示例API調用，以演示如何格式化請求。 這些包括路徑、必需的標頭和正確格式化的請求負載。 還提供了API響應中返回的示例JSON。 有關示例API調用文檔中使用的約定的資訊，請參見上的 [如何讀取示例API調用](../../../../landing/troubleshooting.md#how-do-i-format-an-api-request) Experience Platform疑難解答指南。

### 收集所需標題的值

本指南要求您完成 [驗證教程](https://www.adobe.com/go/platform-api-authentication-en) 以便成功調用平台API。 完成Experience Platform教程將提供所有驗證API調用中每個必需標頭的值，如下所示：

* 授權：持 `{ACCESS_TOKEN}`
* x-api-key: `{API_KEY}`
* x-gw-ims-org-id: `{ORG_ID}`

中的所有資源 [!DNL Experience Platform] 與特定虛擬沙箱隔離。 所有請求 [!DNL Platform] API需要一個標頭，該標頭指定操作將在中進行的沙盒的名稱。 有關中的沙箱的詳細資訊 [!DNL Platform]，請參見 [沙盒概述文檔](../../../../sandboxes/home.md)。

* `x-sandbox-name: {SANDBOX_NAME}`

包含負載(POST、PUT和PATCH)的所有請求都需要附加標頭：

* 內容類型：應用程式/json

## 後續步驟

使用 [!DNL Audit Query] API，請參閱 [事件終結點指南](./events.md) 和 [導出終結點指南](./export.md)。
