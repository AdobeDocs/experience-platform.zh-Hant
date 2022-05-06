---
title: Privacy ServiceAPI入門
description: 瞭解如何驗證Privacy ServiceAPI以及如何解釋文檔中的示例API調用。
topic-legacy: developer guide
exl-id: c1d05e30-ef8f-4adf-87e0-1d6e3e9e9f9e
source-git-commit: 47a94b00e141b24203b01dc93834aee13aa6113c
workflow-type: tm+mt
source-wordcount: '669'
ht-degree: 0%

---

# Privacy ServiceAPI入門

本指南介紹在嘗試調用Privacy ServiceAPI之前需要瞭解的核心概念。

## 先決條件

本指南要求瞭解以下功能：

* [Adobe Experience Platform Privacy Service](../home.md):提供REST風格的API和用戶介面，允許您跨Adobe Experience Cloud應用程式管理對資料主題（客戶）的訪問和刪除請求。

## 收集所需標題的值

為了調用Privacy ServiceAPI，必須先收集要用於所需標頭的訪問憑據：

* `Authorization: Bearer {ACCESS_TOKEN}`
* `x-api-key: {API_KEY}`
* `x-gw-ims-org-id: {ORG_ID}`

這包括獲取Adobe Admin ConsoleAdobe Experience Platform的開發人員權限，然後在Adobe Developer控制台中生成憑據。

### 獲取開發人員對Experience Platform的訪問

獲取開發人員訪問權限 [!DNL Platform]，請執行 [Experience Platform驗證教程](https://www.adobe.com/go/platform-api-authentication-en)。 在您到達步驟「在Adobe Developer控制台中生成訪問憑據」後，返回本教程以生成特定於Privacy Service的憑據。

### 生成訪問憑據

使用Adobe Developer控制台，必須生成以下三種訪問憑據：

* `{ORG_ID}`
* `{API_KEY}`
* `{ACCESS_TOKEN}`

您 `{ORG_ID}` 和 `{API_KEY}` 只需生成一次，並可在將來的API調用中重用。 不過， `{ACCESS_TOKEN}` 是臨時的，必須每24小時再生一次。

以下詳細介紹了生成這些值的步驟。

#### 一次性設定

轉到 [Adobe開發人員控制台](https://www.adobe.com/go/devs_console_ui) 和你的Adobe ID登錄。 接下來，按照本教程中介紹的步驟操作 [建立空項目](https://www.adobe.io/apis/experienceplatform/console/docs.html#!AdobeDocs/adobeio-console/master/projects-empty.md) 在Adobe Developer控制台文檔中。

建立新項目後，選擇 **[!UICONTROL 添加API]** 的 **[!UICONTROL 項目概述]** 的上界。

![](../images/api/getting-started/add-api-button.png)

的 **[!UICONTROL 添加API]** 的上界。 選擇 **[!UICONTROL Privacy ServiceAPI]** 從可用API清單中選擇 **[!UICONTROL 下一個]**。

![](../images/api/getting-started/add-privacy-service-api.png)

的 **[!UICONTROL 配置API]** 的上界。 選擇要 **[!UICONTROL 生成密鑰對]**，然後選擇 **[!UICONTROL 生成鍵對]** 在右下角。

![](../images/api/getting-started/generate-key-pair.png)

將自動生成密鑰對，並將包含私鑰和公共證書的ZIP檔案下載到您的本地電腦（稍後將使用）。 選擇 **[!UICONTROL 保存已配置的API]** 完成配置。

![](../images/api/getting-started/key-pair-generated.png)

將API添加到項目後，項目頁面將重新出現在 **Privacy ServiceAPI概述** 的子菜單。 從此處向下滾動到 **[!UICONTROL 服務帳戶(JWT)]** 部分，該部分提供對Privacy ServiceAPI的所有調用中所需的以下訪問憑據：

* **[!UICONTROL 客戶端ID]**:客戶端ID是必需的 `{API_KEY}` 必須在x-api-key標頭中提供。
* **[!UICONTROL 組織ID]**:組織ID是 `{ORG_ID}` 必須在x-gw-ims-org-id頭中使用的值。

![](../images/api/getting-started/jwt-credentials.png)

#### 每個會話的身份驗證

您必須收集的最終所需憑據是 `{ACCESS_TOKEN}`，在「授權」標頭中使用。 與 `{API_KEY}` 和 `{ORG_ID}`，必須每24小時生成一個新令牌，以繼續使用 [!DNL Platform] API。

生成新 `{ACCESS_TOKEN}`，開啟以前下載的私鑰，並將其內容貼上到旁邊的文本框 **[!UICONTROL 生成訪問令牌]** 選擇 **[!UICONTROL 生成令牌]**。

![](../images/api/getting-started/paste-private-key.png)

將生成新的訪問令牌，並提供一個按鈕將令牌複製到剪貼簿。 此值用於所需的授權標頭，且必須以格式提供 `Bearer {ACCESS_TOKEN}`。

![](../images/api/getting-started/generated-access-token.png)

## 讀取示例API調用

本教程提供了示例API調用，以演示如何格式化請求。 這些包括路徑、必需的標頭和正確格式化的請求負載。 還提供了API響應中返回的示例JSON。 有關示例API調用文檔中使用的約定的資訊，請參見上的 [如何讀取示例API調用](../../landing/api-guide.md#sample-api) 的子版本。

## 後續步驟

現在，您瞭解要使用哪些標頭，就可以開始調用Privacy ServiceAPI。 選擇要開始的終結點參考線之一：

* [隱私作業](./privacy-jobs.md)
* [同意](./consent.md)
