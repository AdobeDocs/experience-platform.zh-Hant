---
title: 驗證並存取 Privacy Service API
description: 瞭解如何向Privacy ServiceAPI驗證以及如何解譯檔案中的範例API呼叫。
exl-id: c1d05e30-ef8f-4adf-87e0-1d6e3e9e9f9e
source-git-commit: 2c8ac35e9bf72c91743714da1591c3414db5c5e9
workflow-type: tm+mt
source-wordcount: '862'
ht-degree: 7%

---

# 驗證並存取 Privacy Service API

本指南介紹您在嘗試呼叫Adobe Experience Platform Privacy Service API之前必須瞭解的核心概念。

## 先決條件 {#prerequisites}

本指南需要您實際瞭解 [Privacy Service](../home.md) 以及它如何讓您管理來自Adobe Experience Cloud應用程式中資料主體（客戶）的存取和刪除請求。

為了建立API的存取認證，您組織內的管理員之前必須設定要在Adobe Admin Console中Privacy Service的產品設定檔。 您指派給API整合的產品設定檔決定在存取Privacy Service功能時，該整合具有哪些許可權。 請參閱以下指南： [管理Privacy Service許可權](../permissions.md) 以取得詳細資訊。

## 收集所需標頭的值 {#gather-values-required-headers}

為了呼叫Privacy Service API，您必須先收集要用於必要標題的存取認證：

* `Authorization: Bearer {ACCESS_TOKEN}`
* `x-api-key: {API_KEY}`
* `x-gw-ims-org-id: {ORG_ID}`

這些值的產生方式 [Adobe Developer Console](https://developer.adobe.com/console). 您的 `{ORG_ID}` 和 `{API_KEY}` 只需產生一次，且可在未來API呼叫中重複使用。 不過，您的 `{ACCESS_TOKEN}` 是暫時性的，必須每24小時重新產生一次。

以下將詳細介紹產生這些值的步驟。

### 一次性設定 {#one-time-setup}

前往 [Adobe Developer Console](https://developer.adobe.com/console) 並使用您的Adobe ID登入。 接下來，請依照教學課程中概述的步驟進行 [建立空白專案](https://developer.adobe.com/developer-console/docs/guides/projects/projects-empty/) 在開發人員控制檯檔案中。

建立新專案後，選取 **[!UICONTROL 新增至專案]** 並選擇 **[!UICONTROL API]** 下拉式選單中的。

![正在從以下專案選取的API選項 [!UICONTROL 新增至專案] 開發人員控制檯中專案詳細資訊頁面的下拉式清單](../images/api/getting-started/add-api-button.png)

#### 選取Privacy ServiceAPI {#select-privacy-service-api}

此 **[!UICONTROL 新增API]** 畫面隨即顯示。 選取 **[!UICONTROL Experience Cloud]** 若要縮小可用API的清單，請選取的卡片 **[!UICONTROL PRIVACY SERVICE API]** 在選取之前 **[!UICONTROL 下一個]**.

![從可用API清單中選取的Privacy ServiceAPI卡](../images/api/getting-started/add-privacy-service-api.png)

>[!TIP]
>
>選取 **[!UICONTROL 檢視檔案]** 可在個別瀏覽器視窗中導覽以完成 [Privacy Service API參考檔案](https://developer.adobe.com/experience-platform-apis/references/privacy-service/).

接著，選取驗證型別以產生存取權杖並存取Privacy ServiceAPI。

>[!IMPORTANT]
>
>選取 **[!UICONTROL OAuth伺服器對伺服器]** 方法，因為這是唯一支援日後使用的方法。 此 **[!UICONTROL 服務帳戶(JWT)]** 方法已過時。 雖然使用JWT驗證方法的整合功能在2025年1月1日之前將繼續運作，但Adobe強烈建議您在該日期之前將現有整合功能移轉至新的OAuth伺服器對伺服器方法。 在區段中取得詳細資訊 [!BADGE 已棄用]{type=negative}[產生JSON Web權杖(JWT)](/help/landing/api-authentication.md#jwt).

![選取Oauth伺服器對伺服器的驗證方法。](/help/privacy-service/images/api/getting-started/select-oauth-authentication.png)

#### 透過產品設定檔指派許可權 {#product-profiles}

最後一個設定步驟是選取此整合將繼承其許可權的產品設定檔。 如果您選取多個設定檔，其許可權集將會結合以進行整合。

>[!NOTE]
>
產品設定檔及其提供的精細許可權，由管理員透過Adobe Admin Console建立和管理。 請參閱以下指南： [Privacy Service許可權](../permissions.md) 以取得詳細資訊。

完成後，選取 **[!UICONTROL 儲存已設定的API]**.

![在儲存設定之前，從清單中選取單一產品設定檔](../images/api/getting-started/select-product-profiles.png)

將API新增至專案後， **[!UICONTROL PRIVACY SERVICE API]** 專案的頁面會顯示所有Privacy ServiceAPI呼叫所需的下列認證：

* `{API_KEY}` ([!UICONTROL 使用者端ID])
* `{ORG_ID}` ([!UICONTROL 組織 ID])

![在開發人員控制檯中新增API後的整合資訊。](/help/privacy-service/images/api/getting-started/api-integration-information.png)

### 每個工作階段的驗證 {#authentication-each-session}

您必須收集的最終必要認證是 `{ACCESS_TOKEN}`，用於Authorization標頭。 不像 `{API_KEY}` 和 `{ORG_ID}`，必須每24小時產生新Token才能繼續使用API。

一般來說，產生存取權杖有兩個方法：

* [手動產生權杖](#manual-token) 以進行測試和開發。
* [自動化權杖產生](#auto-token) 用於API整合。

#### 手動產生權杖 {#manual-token}

若要手動產生新的 `{ACCESS_TOKEN}`，導覽至 **[!UICONTROL 認證]** > **[!UICONTROL OAuth伺服器對伺服器]** 並選取 **[!UICONTROL 產生存取權杖]**，如下所示。

![如何在開發人員控制檯UI中產生存取權杖的熒幕記錄。](/help/privacy-service/images/api/getting-started/generate-access-token.gif)

會產生新的存取Token，並提供按鈕以將該Token複製到剪貼簿。 此值用於必要的 [!DNL Authorization] 標題，且必須以格式提供 `Bearer {ACCESS_TOKEN}`.

#### 自動化權杖產生 {#auto-token}

您也可以使用Postman環境和集合來產生存取權杖。 如需詳細資訊，請閱讀以下章節： [使用Postman驗證及測試API呼叫](/help/landing/api-authentication.md#use-postman) 在Experience Platform API驗證指南中。

## 讀取範例 API 呼叫 {#read-sample-api-calls}

每個端點指南都提供API呼叫範例，示範如何格式化您的請求。 這些包括路徑、必要的標頭和正確格式化的請求承載。 此外，也提供 API 回應中傳回的範例 JSON。 如需檔案中用於範例API呼叫的慣例相關資訊，請參閱以下章節： [如何讀取範例API呼叫](../../landing/api-guide.md#sample-api) （位於平台API快速入門手冊中）。

## 後續步驟 {#next-steps}

現在您瞭解要使用哪些標頭，就可以開始呼叫Privacy Service API了。 選取其中一個端點指南以開始：

* [隱私權職位](./privacy-jobs.md)
* [同意](./consent.md)
