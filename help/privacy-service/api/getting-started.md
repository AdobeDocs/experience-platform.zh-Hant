---
title: 開始使用Privacy ServiceAPI
description: 了解如何驗證Privacy ServiceAPI，以及如何解譯檔案中的範例API呼叫。
topic-legacy: developer guide
exl-id: c1d05e30-ef8f-4adf-87e0-1d6e3e9e9f9e
source-git-commit: 6dcbf2df46ba35104abd9c4e6412799e77c9c49f
workflow-type: tm+mt
source-wordcount: '669'
ht-degree: 0%

---

# 開始使用Privacy ServiceAPI

本指南提供您在嘗試呼叫Privacy ServiceAPI前所需了解的核心概念的簡介。

## 先決條件

本指南需要認真了解下列功能：

* [Adobe Experience Platform Privacy Service](../home.md):提供RESTful API和使用者介面，可讓您管理Adobe Experience Cloud應用程式中資料主體（客戶）的存取和刪除請求。

## 收集必要標題的值

若要呼叫Privacy ServiceAPI，您必須先收集要用於必要標題的存取憑證：

* `Authorization: Bearer {ACCESS_TOKEN}`
* `x-api-key: {API_KEY}`
* `x-gw-ims-org-id: {IMS_ORG}`

這包括在Adobe Admin Console中取得Adobe Experience Platform的開發人員權限，然後在Adobe開發人員控制台中產生憑證。

### 獲得開發人員的Experience Platform

若要取得開發人員的存取權 [!DNL Platform]，請遵循 [Experience Platform驗證教學課程](https://www.adobe.com/go/platform-api-authentication-en). 進入「在Adobe開發人員控制台中產生存取認證」步驟後，請返回本教學課程以產生Privacy Service專屬的認證。

### 生成訪問憑據

使用Adobe開發人員控制台，您必須產生下列三個存取憑證：

* `{IMS_ORG}`
* `{API_KEY}`
* `{ACCESS_TOKEN}`

您的 `{IMS_ORG}` 和 `{API_KEY}` 只需產生一次，即可在未來的API呼叫中重複使用。 不過，您的 `{ACCESS_TOKEN}` 是臨時的，必須每24小時重新生成一次。

以下詳細說明產生這些值的步驟。

#### 一次性設定

前往 [Adobe開發人員控制台](https://www.adobe.com/go/devs_console_ui) 並登入您的Adobe ID。 接下來，請依照 [建立空白專案](https://www.adobe.io/apis/experienceplatform/console/docs.html#!AdobeDocs/adobeio-console/master/projects-empty.md) (位於Adobe開發人員控制台檔案中)。

建立新專案後，請選取 **[!UICONTROL 新增API]** 在 **[!UICONTROL 專案概述]** 螢幕。

![](../images/api/getting-started/add-api-button.png)

此 **[!UICONTROL 新增API]** 畫面。 選擇 **[!UICONTROL Privacy ServiceAPI]** 從可用API清單中選取 **[!UICONTROL 下一個]**.

![](../images/api/getting-started/add-privacy-service-api.png)

此 **[!UICONTROL 設定API]** 畫面。 選取要 **[!UICONTROL 產生金鑰組]**，然後選取 **[!UICONTROL 產生鍵對]** 在右下角。

![](../images/api/getting-started/generate-key-pair.png)

系統會自動產生金鑰組，而包含私密金鑰和公開憑證的ZIP檔案會下載至您的本機電腦（以便稍後步驟使用）。 選擇 **[!UICONTROL 儲存已設定的API]** 以完成設定。

![](../images/api/getting-started/key-pair-generated.png)

將API新增至專案後，專案頁面會重新顯示在 **Privacy ServiceAPI概述** 頁面。 從這裡，向下捲動至 **[!UICONTROL 服務帳戶(JWT)]** 區段，提供所有對Privacy ServiceAPI的呼叫中所需的下列存取憑證：

* **[!UICONTROL 用戶端ID]**:用戶端ID為必要 `{API_KEY}` for必須在x-api-key標題中提供。
* **[!UICONTROL 組織ID]**:組織ID為 `{IMS_ORG}` 必須用於x-gw-ims-org-id標題的值。

![](../images/api/getting-started/jwt-credentials.png)

#### 每個會話的驗證

您必須收集的最終必要憑證是 `{ACCESS_TOKEN}`，此資訊用於授權標題中。 不同於 `{API_KEY}` 和 `{IMS_ORG}`，則必須每24小時產生新代號，才能繼續使用 [!DNL Platform] API。

生成新 `{ACCESS_TOKEN}`，開啟先前下載的私密金鑰，並將其內容貼到旁邊的文字方塊中 **[!UICONTROL 產生存取權杖]** 選擇 **[!UICONTROL 產生代號]**.

![](../images/api/getting-started/paste-private-key.png)

系統會產生新的存取權杖，並提供將權杖複製到剪貼簿的按鈕。 此值用於所需的授權標頭，且必須以格式提供 `Bearer {ACCESS_TOKEN}`.

![](../images/api/getting-started/generated-access-token.png)

## 讀取範例API呼叫

本教學課程提供範例API呼叫，以示範如何設定要求格式。 這些功能包括路徑、必要標題和格式正確的請求裝載。 也提供API回應中傳回的範例JSON。 如需範例API呼叫檔案中所使用慣例的相關資訊，請參閱 [如何閱讀API呼叫範例](../../landing/api-guide.md#sample-api) 平台API快速入門手冊中的。

## 後續步驟

現在您已了解要使用的標題，可以開始呼叫Privacy ServiceAPI了。 選取要開始使用的端點指南之一：

* [隱私權工作](./privacy-jobs.md)
* [同意](./consent.md)
