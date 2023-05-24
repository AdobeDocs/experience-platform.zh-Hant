---
title: Privacy ServiceAPI入門
description: 瞭解如何驗證Privacy ServiceAPI以及如何解釋文檔中的示例API調用。
exl-id: c1d05e30-ef8f-4adf-87e0-1d6e3e9e9f9e
source-git-commit: 0f7ef438db5e7141197fb860a5814883d31ca545
workflow-type: tm+mt
source-wordcount: '919'
ht-degree: 1%

---

# Privacy ServiceAPI入門

本指南介紹在嘗試調用Adobe Experience Platform Privacy ServiceAPI之前需要瞭解的核心概念。

## 先決條件

本指南要求對 [Privacy Service](../home.md) 以及它如何允許您跨Adobe Experience Cloud應用程式管理訪問和刪除資料主題（客戶）的請求。

為了為API建立訪問憑據，您組織中的管理員以前必須設定產品配置檔案以在Adobe Admin Console內Privacy Service。 您分配給API整合的產品配置檔案確定整合在訪問Privacy Service權能時具有的權限。 請參閱上的指南 [管理Privacy Service權限](../permissions.md) 的子菜單。

## 收集所需標題的值

為了調用Privacy ServiceAPI，必須先收集要用於所需標頭的訪問憑據：

* `Authorization: Bearer {ACCESS_TOKEN}`
* `x-api-key: {API_KEY}`
* `x-gw-ims-org-id: {ORG_ID}`

這些值是使用 [Adobe Developer控制台](https://developer.adobe.com/console)。 您 `{ORG_ID}` 和 `{API_KEY}` 只需生成一次，並可在將來的API調用中重用。 不過， `{ACCESS_TOKEN}` 是臨時的，必須每24小時再生一次。

以下詳細介紹了生成這些值的步驟。

### 一次性設定

轉到 [Adobe Developer控制台](https://developer.adobe.com/console) 和你的Adobe ID登錄。 接下來，按照本教程中介紹的步驟操作 [建立空項目](https://developer.adobe.com/developer-console/docs/guides/projects/projects-empty/) 在Developer Console文檔中。

建立新項目後，選擇 **[!UICONTROL 添加到項目]** 選擇 **[!UICONTROL API]** 的下界。

![正在從 [!UICONTROL 添加到項目] 從Developer Console中的項目詳細資訊頁面中的下拉菜單](../images/api/getting-started/add-api-button.png)

#### 選擇API並生成密鑰對 {#keypair}

的 **[!UICONTROL 添加API]** 的上界。 選擇 **[!UICONTROL Experience Cloud]** 要縮小可用API清單的範圍，請選擇 **[!UICONTROL Privacy ServiceAPI]** 選擇 **[!UICONTROL 下一個]**。

![從可用API清單中選擇的Privacy ServiceAPI卡](../images/api/getting-started/add-privacy-service-api.png)

的 **[!UICONTROL 配置API]** 的上界。 選擇要 **[!UICONTROL 生成密鑰對]**，然後選擇 **[!UICONTROL 生成鍵對]**。

![的 [!UICONTROL 生成密鑰對] 選項 [!UICONTROL 配置API] 螢幕](../images/api/getting-started/generate-key-pair.png)

該密鑰對將自動生成，並且包含私鑰和公共證書的ZIP檔案將由瀏覽器下載（稍後的步驟中使用）。 選取&#x200B;**[!UICONTROL 「下一步」]**&#x200B;以繼續。

![在UI中顯示的生成鍵對，其值由瀏覽器自動下載](../images/api/getting-started/key-pair-generated.png)

#### 通過產品配置檔案分配權限 {#product-profiles}

最終的配置步驟是選擇此整合將從中繼承其權限的產品配置檔案。 如果選擇多個配置檔案，則它們的權限集將合併用於整合。

>[!NOTE]
>
>產品配置檔案及其提供的精細權限由管理員通過Adobe Admin Console建立和管理。 請參閱上的指南 [Privacy Service權限](../permissions.md) 的子菜單。

完成後，選擇 **[!UICONTROL 保存已配置的API]**。

![保存配置之前從清單中選擇的單個產品配置檔案](../images/api/getting-started/select-product-profiles.png)

將API添加到項目後，項目頁面將重新出現在 **Privacy ServiceAPI概述** 的子菜單。 從此處向下滾動到 **[!UICONTROL 服務帳戶(JWT)]** 部分，該部分提供對Privacy ServiceAPI的所有調用中所需的以下訪問憑據：

* **[!UICONTROL 客戶端ID]**:客戶端ID是必需的 `{API_KEY}` 必須在 `x-api-key` 標題。
* **[!UICONTROL 組織ID]**:組織ID是 `{ORG_ID}` 必須在 `x-gw-ims-org-id` 標題。

![配置API後，「客戶端ID」和「組織ID」值出現在項目概述頁上](../images/api/getting-started/jwt-credentials.png)

### 每個會話的身份驗證

您必須收集的最終所需憑據是 `{ACCESS_TOKEN}`，在「授權」標頭中使用。 與 `{API_KEY}` 和 `{ORG_ID}`，必須每24小時生成一個新令牌才能繼續使用API。

一般來說，有兩種方法生成訪問令牌：

* [手動生成令牌](#manual-token) 測試和開發。
* [自動生成令牌](#auto-token) 用於API整合。

#### 手動生成令牌 {#manual-token}

手動生成新 `{ACCESS_TOKEN}`，開啟以前下載的私鑰，並將其內容貼上到旁邊的文本框 **[!UICONTROL 生成訪問令牌]** 選擇 **[!UICONTROL 生成令牌]**。

![以前生成的訪問令牌將貼上到項目的概述頁面上， [!UICONTROL 生成令牌] 按鈕](../images/api/getting-started/paste-private-key.png)

將生成新的訪問令牌，並提供一個按鈕將令牌複製到剪貼簿。 此值用於所需的授權標頭，且必須以格式提供 `Bearer {ACCESS_TOKEN}`。

![從UI複製生成的訪問令牌](../images/api/getting-started/generated-access-token.png)

#### 自動生成令牌 {#auto-token}

通過向AdobeIdentity Management服務(IMS)的POST請求發送JSON Web令牌(JWT)，可以為自動化進程生成新的訪問令牌。 請參閱上的Developer Console文檔 [JWT驗證](https://developer.adobe.com/developer-console/docs/guides/authentication/JWT/) 的子菜單。

## 讀取示例API調用

每個端點指南都提供示例API調用，以演示如何格式化請求。 這些包括路徑、必需的標頭和正確格式化的請求負載。 還提供了API響應中返回的示例JSON。 有關示例API調用文檔中使用的約定的資訊，請參見上的 [如何讀取示例API調用](../../landing/api-guide.md#sample-api) 的子版本。

## 後續步驟

現在，您瞭解要使用哪些標頭，就可以開始調用Privacy ServiceAPI。 選擇要開始的終結點參考線之一：

* [隱私作業](./privacy-jobs.md)
* [同意](./consent.md)
