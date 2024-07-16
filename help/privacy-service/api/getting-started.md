---
title: 驗證並存取 Privacy Service API
description: 瞭解如何向Privacy ServiceAPI驗證以及如何解譯檔案中的範例API呼叫。
role: Developer
exl-id: c1d05e30-ef8f-4adf-87e0-1d6e3e9e9f9e
source-git-commit: c16ce1020670065ecc5415bc3e9ca428adbbd50c
workflow-type: tm+mt
source-wordcount: '851'
ht-degree: 5%

---

# 驗證並存取 Privacy Service API

本指南介紹您在嘗試呼叫Adobe Experience Platform Privacy Service API之前必須瞭解的核心概念。

## 先決條件 {#prerequisites}

本指南需要您實際瞭解[Privacy Service](../home.md)，以及它如何讓您跨Adobe Experience Cloud應用程式管理資料主體（客戶）的存取和刪除請求。

為了建立API的存取認證，您組織內的管理員之前必須設定要在Adobe Admin Console中Privacy Service的產品設定檔。 您指派給API整合的產品設定檔決定在存取Privacy Service功能時，該整合具有哪些許可權。 如需詳細資訊，請參閱[管理Privacy Service許可權](../permissions.md)指南。

## 收集所需標頭的值 {#gather-values-required-headers}

為了呼叫Privacy Service API，您必須先收集要用於必要標題的存取認證：

* `Authorization: Bearer {ACCESS_TOKEN}`
* `x-api-key: {API_KEY}`
* `x-gw-ims-org-id: {ORG_ID}`

這些值是使用[Adobe Developer Console](https://developer.adobe.com/console)產生。 您的`{ORG_ID}`和`{API_KEY}`只需要產生一次，並可在未來的API呼叫中重複使用。 不過，您的`{ACCESS_TOKEN}`是暫時性的，必須每24小時重新產生一次。

以下將詳細介紹產生這些值的步驟。

### 一次性設定 {#one-time-setup}

移至[Adobe Developer Console](https://developer.adobe.com/console)並使用您的Adobe ID登入。 接下來，請依照教學課程中概述的步驟，在Developer Console檔案中建立[空白專案](https://developer.adobe.com/developer-console/docs/guides/projects/projects-empty/)。

建立新專案後，請選取&#x200B;**[!UICONTROL 新增至專案]**，然後從下拉式功能表中選擇&#x200B;**[!UICONTROL API]**。

![從Developer Console中專案詳細資訊頁面的[!UICONTROL 新增至專案]下拉式清單中選取的API選項](../images/api/getting-started/add-api-button.png)

#### 選取Privacy ServiceAPI {#select-privacy-service-api}

**[!UICONTROL 新增API]**&#x200B;畫面會出現。 選取&#x200B;**[!UICONTROL Experience Cloud]**&#x200B;以縮小可用API清單的範圍，然後在選取&#x200B;**[!UICONTROL 下一步]**&#x200B;之前，選取&#x200B;**[!UICONTROL Privacy ServiceAPI]**&#x200B;的卡片。

![正在從可用API清單中選取Privacy ServiceAPI卡](../images/api/getting-started/add-privacy-service-api.png)

>[!TIP]
>
>選取&#x200B;**[!UICONTROL 檢視檔案]**&#x200B;選項，在個別瀏覽器視窗中瀏覽至完整的[Privacy ServiceAPI參考檔案](https://developer.adobe.com/experience-platform-apis/references/privacy-service/)。

接著，選取驗證型別以產生存取權杖並存取Privacy ServiceAPI。

>[!IMPORTANT]
>
>選取&#x200B;**[!UICONTROL OAuth伺服器對伺服器]**&#x200B;方法，因為這是日後唯一支援的方法。 **[!UICONTROL 服務帳戶(JWT)]**&#x200B;方法已過時。 雖然使用JWT驗證方法的整合功能在2025年1月1日之前將繼續運作，但Adobe強烈建議您在該日期之前將現有整合功能移轉至新的OAuth伺服器對伺服器方法。 在[!BADGE 已棄用]一節中取得詳細資訊{type=negative}[產生JSON Web權杖(JWT)](/help/landing/api-authentication.md#jwt)。

![選取Oauth伺服器對伺服器的驗證方法。](/help/privacy-service/images/api/getting-started/select-oauth-authentication.png)

#### 透過產品設定檔指派許可權 {#product-profiles}

最後一個設定步驟是選取此整合將繼承其許可權的產品設定檔。 如果您選取多個設定檔，其許可權集將會結合以進行整合。

>[!NOTE]
>
產品設定檔及其提供的精細許可權，由管理員透過Adobe Admin Console建立和管理。 如需詳細資訊，請參閱[Privacy Service許可權](../permissions.md)的指南。

完成後，選取&#x200B;**[!UICONTROL 儲存設定的API]**。

![儲存組態之前，從清單中選取單一產品設定檔](../images/api/getting-started/select-product-profiles.png)

將API新增至專案後，專案的&#x200B;**[!UICONTROL Privacy Service API]**&#x200B;頁面會顯示所有呼叫Privacy Service API時所需的下列認證：

* `{API_KEY}` （[!UICONTROL 使用者端識別碼]）
* `{ORG_ID}` （[!UICONTROL 組織識別碼]）

在Developer Console中新增API後的![整合資訊。](/help/privacy-service/images/api/getting-started/api-integration-information.png)

### 每個工作階段的驗證 {#authentication-each-session}

您必須收集的最終必要認證是您的`{ACCESS_TOKEN}`，用於授權標頭。 不像`{API_KEY}`和`{ORG_ID}`的值，每24小時必須產生一次新Token才能繼續使用API。

一般來說，產生存取權杖有兩個方法：

* [手動產生Token](#manual-token)以進行測試和開發。
* [自動產生API整合的權杖](#auto-token)。

#### 手動產生權杖 {#manual-token}

若要手動產生新的`{ACCESS_TOKEN}`，請瀏覽至&#x200B;**[!UICONTROL 認證]** > **[!UICONTROL OAuth伺服器對伺服器]**，然後選取&#x200B;**[!UICONTROL 產生存取權杖]**，如下所示。

![如何在Developer Console UI中產生存取權杖的熒幕錄製。](/help/privacy-service/images/api/getting-started/generate-access-token.gif)

會產生新的存取Token，並提供按鈕以將該Token複製到剪貼簿。 此值用於必要的[!DNL Authorization]標頭，且必須以`Bearer {ACCESS_TOKEN}`格式提供。

#### 自動化權杖產生 {#auto-token}

您也可以使用Postman環境和集合來產生存取權杖。 如需詳細資訊，請閱讀Experience PlatformAPI驗證指南中有關[使用Postman驗證和測試API呼叫](/help/landing/api-authentication.md#use-postman)的章節。

## 讀取範例 API 呼叫 {#read-sample-api-calls}

每個端點指南都提供API呼叫範例，示範如何格式化您的請求。 這些包括路徑、必要的標頭和正確格式化的請求承載。 此外，也提供 API 回應中傳回的範例 JSON。 如需檔案中所使用之範例API呼叫慣例的詳細資訊，請參閱Platform API快速入門手冊中[如何讀取範例API呼叫](../../landing/api-guide.md#sample-api)的相關章節。

## 後續步驟 {#next-steps}

現在您瞭解要使用哪些標頭，就可以開始呼叫Privacy Service API了。 選取其中一個端點指南以開始：

* [隱私權職位](./privacy-jobs.md)
* [同意](./consent.md)
