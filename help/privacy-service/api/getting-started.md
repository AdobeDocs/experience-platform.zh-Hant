---
title: 開始使用Privacy ServiceAPI
description: 了解如何驗證Privacy ServiceAPI，以及如何解譯檔案中的範例API呼叫。
topic-legacy: developer guide
exl-id: c1d05e30-ef8f-4adf-87e0-1d6e3e9e9f9e
source-git-commit: 59dc28a84971dc8c21d633741cfe2dc1b44ea1a6
workflow-type: tm+mt
source-wordcount: '919'
ht-degree: 1%

---

# 開始使用Privacy ServiceAPI

本指南提供您在嘗試呼叫Adobe Experience Platform Privacy Service API之前所需了解的核心概念的簡介。

## 先決條件

本指南需要妥善了解 [Privacy Service](../home.md) 以及如何讓您管理Adobe Experience Cloud應用程式中資料主體（客戶）的存取和刪除請求。

若要建立API的存取憑證，您組織內的管理員必須先設定產品設定檔，才能在Adobe Admin Console內Privacy Service。 您指派給API整合的產品設定檔會決定整合在存取Privacy Service功能時具有的權限。 請參閱 [管理Privacy Service權限](../permissions.md) 以取得更多資訊。

## 收集必要標題的值

若要呼叫Privacy ServiceAPI，您必須先收集要用於必要標題的存取憑證：

* `Authorization: Bearer {ACCESS_TOKEN}`
* `x-api-key: {API_KEY}`
* `x-gw-ims-org-id: {ORG_ID}`

這些值是使用 [Adobe Developer Console](https://developer.adobe.com/console). 您的 `{ORG_ID}` 和 `{API_KEY}` 只需產生一次，即可在未來的API呼叫中重複使用。 不過，您的 `{ACCESS_TOKEN}` 是臨時的，必須每24小時重新生成一次。

以下詳細說明產生這些值的步驟。

### 一次性設定

前往 [Adobe Developer Console](https://developer.adobe.com/console) 並登入您的Adobe ID。 接下來，請依照 [建立空白專案](https://developer.adobe.com/developer-console/docs/guides/projects/projects-empty/) （位於開發人員控制台檔案中）。

建立新專案後，請選取 **[!UICONTROL 新增至專案]** 選擇 **[!UICONTROL API]** 從下拉式功能表。

![從 [!UICONTROL 新增至專案] 從開發人員控制台的專案詳細資訊頁面的下拉式清單](../images/api/getting-started/add-api-button.png)

#### 選取API並產生密鑰對 {#keypair}

此 **[!UICONTROL 新增API]** 畫面。 選擇 **[!UICONTROL Experience Cloud]** 若要縮小可用API的清單，請選取 **[!UICONTROL Privacy ServiceAPI]** 選擇 **[!UICONTROL 下一個]**.

![從可用API清單中選取的Privacy ServiceAPI卡](../images/api/getting-started/add-privacy-service-api.png)

此 **[!UICONTROL 設定API]** 畫面。 選取要 **[!UICONTROL 產生金鑰組]**，然後選取 **[!UICONTROL 產生鍵對]**.

![此 [!UICONTROL 產生金鑰組] 選項 [!UICONTROL 設定API] 螢幕](../images/api/getting-started/generate-key-pair.png)

系統會自動產生金鑰組，而瀏覽器會下載包含私密金鑰和公開憑證的ZIP檔案（以用於後續步驟）。 選擇 **[!UICONTROL 下一個]** 繼續。

![產生的鍵組（顯示在UI中），其值會由瀏覽器自動下載](../images/api/getting-started/key-pair-generated.png)

#### 透過產品設定檔指派權限 {#product-profiles}

最後的設定步驟是選取此整合將繼承其權限的產品設定檔。 如果您選取多個設定檔，系統會結合其權限集以進行整合。

>[!NOTE]
>
>產品設定檔及其提供的精細權限是由管理員透過Adobe Admin Console建立和管理。 請參閱 [Privacy Service權限](../permissions.md) 以取得更多資訊。

完成後，請選取 **[!UICONTROL 儲存已設定的API]**.

![儲存設定前，會從清單中選取單一產品設定檔](../images/api/getting-started/select-product-profiles.png)

將API新增至專案後，專案頁面會重新顯示在 **Privacy ServiceAPI概述** 頁面。 從這裡，向下捲動至 **[!UICONTROL 服務帳戶(JWT)]** 區段，提供所有對Privacy ServiceAPI的呼叫中所需的下列存取憑證：

* **[!UICONTROL 用戶端ID]**:用戶端ID為必要 `{API_KEY}` 必須在 `x-api-key` 頁首。
* **[!UICONTROL 組織ID]**:組織ID為 `{ORG_ID}` 值 `x-gw-ims-org-id` 頁首。

![設定API後，用戶端ID和組織ID值會顯示在專案概述頁面上](../images/api/getting-started/jwt-credentials.png)

### 每個會話的驗證

您必須收集的最終必要憑證是 `{ACCESS_TOKEN}`，此資訊用於授權標題中。 不同於 `{API_KEY}` 和 `{ORG_ID}`，則必須每24小時產生一個新代號，才能繼續使用API。

一般而言，有兩種方法可產生存取權杖：

* [手動產生代號](#manual-token) 用於測試和開發。
* [自動產生代號](#auto-token) 的API整合。

#### 手動產生代號 {#manual-token}

手動產生新 `{ACCESS_TOKEN}`，開啟先前下載的私密金鑰，並將其內容貼到旁邊的文字方塊中 **[!UICONTROL 產生存取權杖]** 選擇 **[!UICONTROL 產生代號]**.

![先前產生的存取權杖會貼至專案的「概觀」頁面上，並帶有 [!UICONTROL 產生代號] 按鈕](../images/api/getting-started/paste-private-key.png)

系統會產生新的存取權杖，並提供將權杖複製到剪貼簿的按鈕。 此值用於所需的授權標頭，且必須以格式提供 `Bearer {ACCESS_TOKEN}`.

![從UI複製的產生存取權杖](../images/api/getting-started/generated-access-token.png)

#### 自動產生代號 {#auto-token}

您可以透過POST要求AdobeIdentity Management服務(IMS)，傳送JSON網頁代號(JWT)，為自動化程式產生新的存取代號。 請參閱開發人員控制台檔案，位於 [JWT驗證](https://developer.adobe.com/developer-console/docs/guides/authentication/JWT/) 以取得詳細步驟。

## 讀取範例API呼叫

每個端點指南都提供範例API呼叫，以示範如何設定請求格式。 這些功能包括路徑、必要標題和格式正確的請求裝載。 也提供API回應中傳回的範例JSON。 如需範例API呼叫檔案中所使用慣例的相關資訊，請參閱 [如何閱讀API呼叫範例](../../landing/api-guide.md#sample-api) 平台API快速入門手冊中的。

## 後續步驟

現在您已了解要使用的標題，可以開始呼叫Privacy ServiceAPI了。 選取要開始使用的端點指南之一：

* [隱私權工作](./privacy-jobs.md)
* [同意](./consent.md)
