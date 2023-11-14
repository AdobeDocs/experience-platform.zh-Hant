---
solution: Experience Platform
title: 驗證及存取Experience PlatformAPI
type: Tutorial
description: 本文件逐步說明如何存取 Adobe Experience Platform 開發人員帳戶，進而呼叫 Experience Platform API。
exl-id: dfe8a7be-1b86-4d78-a27e-87e4ed8b3d42
source-git-commit: f598c6dabe9296044055d8e961cf5177a655f5fa
workflow-type: tm+mt
source-wordcount: '2204'
ht-degree: 7%

---


# 驗證及存取 Experience Platform API

本文件逐步說明如何存取 Adobe Experience Platform 開發人員帳戶，進而呼叫 Experience Platform API。在本教學課程結束時，您將已產生或收集下列憑證，這些憑證需要作為所有Platform API呼叫中的標題：

* `{ACCESS_TOKEN}`
* `{API_KEY}`
* `{ORG_ID}`

>[!TIP]
>
>除了上述三個憑證外，許多Platform API也需要有效的 `{SANDBOX_NAME}` 提供為標題。 請參閱 [沙箱總覽](../sandboxes/home.md) 以取得有關沙箱和 [沙箱管理端點](/help/sandboxes/api/sandboxes.md#list) 說明檔案，以取得貴組織可用的沙箱清單相關資訊。

為了維護應用程式和使用者的安全性，對Experience Platform API的所有請求都必須使用OAuth等標準進行驗證和授權。

本教學課程涵蓋如何收集驗證Platform API呼叫所需的認證，如下方流程圖所述。 您可以在初始的一次性設定中收集大部分必要的認證。 然而，存取權杖必須每24小時重新整理一次。

![](./images/api-authentication/authentication-flowchart.png)

## 先決條件 {#prerequisites}

為了成功呼叫Experience Platform API，您必須具備下列條件：

* 有權存取Adobe Experience Platform的組織。
* 能夠新增您為產品設定檔的開發人員和使用者的Admin Console管理員。
* Experience Platform系統管理員，可授予您必要的屬性型存取控制項，以透過API在Experience Platform的不同部分執行讀取或寫入作業。

您也必須有Adobe ID才能完成本教學課程。 如果您沒有Adobe ID，可以使用下列步驟建立一個：

1. 前往 [Adobe Developer Console](https://console.adobe.io).
2. 選取 **[!UICONTROL 建立新帳戶]**.
3. 完成註冊程式。

## 取得Experience Platform的開發人員和使用者存取權 {#gain-developer-user-access}

在Adobe Developer Console上建立整合之前，您的帳戶必須擁有Adobe Admin Console中Experience Platform產品設定檔的開發人員和使用者許可權。

### 取得開發人員存取權 {#gain-developer-access}

聯絡 [!DNL Admin Console] 管理員的許可權，使用將您作為開發人員新增至Experience Platform產品設定檔 [[!DNL Admin Console]](https://adminconsole.adobe.com/). 請參閱 [!DNL Admin Console] 檔案，以取得關於如何 [管理產品設定檔的開發人員存取權](https://helpx.adobe.com/enterprise/admin-guide.html/enterprise/using/manage-developers.ug.html).

一旦指派您為開發人員，您就可以開始在中建立整合 [Adobe Developer Console](https://www.adobe.com/go/devs_console_ui). 這些整合是從外部應用程式和服務到Adobe API的管道。

### 取得使用者存取權 {#gain-user-access}

您的 [!DNL Admin Console] 管理員必須將您作為使用者新增到相同的產品設定檔。 透過使用者存取權，您可以在UI中檢視您執行的API作業的結果。

請參閱以下指南： [管理使用者群組 [!DNL Admin Console]](https://helpx.adobe.com/enterprise/admin-guide.html/enterprise/using/user-groups.ug.html) 以取得詳細資訊。

## 產生API金鑰（使用者端ID）和組織ID {#generate-credentials}

>[!NOTE]
>
>如果您要遵循此檔案，從 [Privacy Service API指南](../privacy-service/api/getting-started.md)，您現在可以返回該指南以產生 [!DNL Privacy Service].

在您透過取得開發人員和使用者的Platform存取權後 [!DNL Admin Console]，下一步是產生 `{ORG_ID}` 和 `{API_KEY}` Adobe Developer Console中的認證。 這些認證只需產生一次，並可在未來平台API呼叫中重複使用。

### 將Experience Platform新增至專案 {#add-platform-to-project}

前往 [Adobe Developer Console](https://www.adobe.com/go/devs_console_ui) 並使用您的Adobe ID登入。 接下來，請依照教學課程中概述的步驟進行 [建立空白專案](https://developer.adobe.com/developer-console/docs/guides/projects/projects-empty/) 在Adobe Developer Console檔案中。

建立新專案後，選取 **[!UICONTROL 新增API]** 於 **[!UICONTROL 專案概述]** 畫面。

>[!TIP]
>
>如果您已布建多個組織，請使用介面右上角的組織選擇器，以確保您位於所需的組織中。

![醒目提示新增API選項的開發人員控制檯畫面。](./images/api-authentication/add-api.png)

此 **[!UICONTROL 新增API]** 畫面隨即顯示。 選取Adobe Experience Platform的產品圖示，然後選擇 **[!UICONTROL EXPERIENCE PLATFORM API]** 在選取之前 **[!UICONTROL 下一個]**.

![選取「Experience PlatformAPI」。](./images/api-authentication/platform-api.png)

>[!TIP]
>
>選取 **[!UICONTROL 檢視檔案]** 可在個別瀏覽器視窗中導覽以完成 [Experience Platform API參考檔案](https://developer.adobe.com/experience-platform-apis/).

### 選取OAuth伺服器對伺服器驗證型別 {#select-oauth-server-to-server}

接著，選取驗證型別以產生存取權杖並存取Experience PlatformAPI。

>[!IMPORTANT]
>
>選取 **[!UICONTROL OAuth伺服器對伺服器]** 方法，因為這將是日後唯一支援的方法。 此 **[!UICONTROL 服務帳戶(JWT)]** 方法已過時。 雖然使用JWT驗證方法的整合功能在2025年1月1日之前將繼續運作，但Adobe強烈建議您在該日期之前將現有整合功能移轉至新的OAuth伺服器對伺服器方法。 在區段中取得詳細資訊 [!BADGE 已棄用]{type=negative}[產生JSON Web權杖(JWT)](#jwt).

![選取「Experience PlatformAPI」。](./images/api-authentication/oauth-authentication-method.png)

### 選取要整合的產品設定檔 {#select-product-profiles}

在 **[!UICONTROL 設定API]** 熒幕，選取 **[!UICONTROL AEP-Default-All-Users]**.

<!--
Your integration's service account will gain access to granular features through the product profiles selected here.

-->

>[!IMPORTANT]
>
若要存取Platform中的特定功能，您還需要系統管理員授予您必要的屬性型存取控制許可權。 閱讀本小節中的詳細資訊 [取得必要的屬性型存取控制許可權](#get-abac-permissions).

![選取要整合的產品設定檔。](./images/api-authentication/select-product-profiles.png)

選取 **[!UICONTROL 儲存已設定的API]** 當您準備好時。

以下的影片教學課程也提供上述步驟的逐步解說，以設定與Experience Platform API的整合：

>[!VIDEO](https://video.tv.adobe.com/v/28832/?learn=on)

### 收集認證 {#gather-credentials}

將API新增至專案後， **[!UICONTROL EXPERIENCE PLATFORM API]** 專案的頁面會顯示所有Experience PlatformAPI呼叫所需的下列認證：

![在Developer Console中新增API後的整合資訊。](./images/api-authentication/api-integration-information.png)

* `{API_KEY}` ([!UICONTROL 使用者端ID])
* `{ORG_ID}` ([!UICONTROL 組織 ID])

<!--

![](././images/api-authentication/api-key-ims-org.png)

<!--

In addition to the above credentials, you also need the generated **[!UICONTROL Client Secret]** for a future step. Select **[!UICONTROL Retrieve client secret]** to reveal the value, and then copy it for later use.

![](././images/api-authentication/client-secret.png)

-->

## 產生存取權杖 {#generate-access-token}

下一步是產生 `{ACCESS_TOKEN}` 用於平台API呼叫的認證。 不像 `{API_KEY}` 和 `{ORG_ID}`，必須每24小時產生一個新Token才能繼續使用Platform API。 選取 **[!UICONTROL 產生存取權杖]**，如下所示。

![顯示如何產生存取權杖](././images/api-authentication/generate-access-token.gif)

>[!TIP]
>
您也可以使用Postman環境和集合來產生存取權杖。 如需詳細資訊，請閱讀以下章節： [使用Postman驗證及測試API呼叫](#use-postman).

## [!BADGE 已棄用]{type=negative}產生JSON Web權杖(JWT) {#jwt}

>[!WARNING]
>
不建議使用產生存取權杖的JWT方法。 所有新的整合必須使用 [OAuth伺服器對伺服器驗證方法](#select-oauth-server-to-server). Adobe 也建議您將現有的整合移轉至 OAuth 方法。 請參閱下列重要檔案：
> 
* [應用程式從JWT移轉至OAuth的移轉指南](https://developer.adobe.com/developer-console/docs/guides/authentication/ServerToServerAuthentication/migration/)
* [OAuth 新舊應用程式的實施指南](https://developer.adobe.com/developer-console/docs/guides/authentication/ServerToServerAuthentication/implementation/)
* [使用OAuth伺服器對伺服器憑證方法的優勢](https://developer.adobe.com/developer-console/docs/guides/authentication/ServerToServerAuthentication/migration/#why-oauth-server-to-server-credentials)

+++ 檢視已棄用的資訊

下一步是根據您的帳戶憑證產生JSON Web權杖(JWT)。 此值用於產生 `{ACCESS_TOKEN}` 用於平台API呼叫的認證，必須每24小時重新產生一次。

>[!IMPORTANT]
>
在本教學課程中，以下步驟會概述如何在Developer Console中產生JWT。 不過，此產生方法只應用於測試和評估目的。
>
如要正常使用，必須自動產生JWT。 如需如何以程式設計方式產生JWT的詳細資訊，請參閱 [服務帳戶驗證指南](https://www.adobe.io/developer-console/docs/guides/authentication/JWT/) 在Adobe Developer上。

選取 **[!UICONTROL 服務帳戶(JWT)]** 在左側導覽中，然後選取 **[!UICONTROL 產生JWT]**.

![](././images/api-authentication/generate-jwt.png)

於下方提供的文字方塊中 **[!UICONTROL 產生自訂JWT]**，貼上您先前在將Platform API新增至服務帳戶時產生的私密金鑰內容。 然後，選取 **[!UICONTROL 產生Token]**.

![](././images/api-authentication/paste-key.png)

頁面會更新以顯示產生的JWT，以及可讓您產生存取權杖的範例cURL命令。 在本教學課程中，請選取 **[!UICONTROL 複製]** 旁邊 **[!UICONTROL 產生的JWT]** 以將Token複製到剪貼簿。

![](././images/api-authentication/copy-jwt.png)

**產生存取權杖**

產生JWT後，您可以在API呼叫中使用它來產生您的 `{ACCESS_TOKEN}`. 不像 `{API_KEY}` 和 `{ORG_ID}`，必須每24小時產生一個新Token才能繼續使用Platform API。

**要求**

以下請求會產生新的 `{ACCESS_TOKEN}` 根據承載中提供的認證。 此端點僅接受表單資料作為其裝載，因此必須給予它 `Content-Type` 頁首 `multipart/form-data`.

```shell
curl -X POST https://ims-na1.adobelogin.com/ims/exchange/jwt \
  -H 'Content-Type: multipart/form-data' \
  -F 'client_id={API_KEY}' \
  -F 'client_secret={SECRET}' \
  -F 'jwt_token={JWT}'
```

| 屬性 | 說明 |
| --- | --- |
| `{API_KEY}` | 此 `{API_KEY}` ([!UICONTROL 使用者端ID])中擷取到的值 [上一步](#api-ims-secret). |
| `{SECRET}` | 您在中擷取的使用者端密碼 [上一步](#api-ims-secret). |
| `{JWT}` | 您在中產生的JWT [上一步](#jwt). |

>[!NOTE]
>
您可以使用相同的API金鑰、使用者端密碼和JWT，為每個工作階段產生新的存取權杖。 這可讓您在應用程式中自動產生存取權杖。

**回應**

```json
{
  "token_type": "bearer",
  "access_token": "{ACCESS_TOKEN}",
  "expires_in": 86399992
}
```

| 屬性 | 說明 |
| --- | --- |
| `token_type` | 型別 of 正在傳回權杖。 若為存取權杖，此值一律為 `bearer`. |
| `access_token` | 產生的 `{ACCESS_TOKEN}`. 此值(前置詞為 `Bearer`，為必要項 `Authentication` 所有Platform API呼叫的標題。 |
| `expires_in` | 存取Token過期前的剩餘毫秒數。 此值達到0後，必須產生新的存取權杖才能繼續使用Platform API。 |

+++

## 測試存取認證 {#test-credentials}

收集完所有三個必要的認證（存取權杖、API金鑰和組織ID）後，您可以嘗試進行下列API呼叫。 此通話會列出所有標準 [!DNL Experience Data Model] (XDM)類別可供您的組織使用。 在中匯入並執行呼叫 [Postman](#use-postman).

>[!BEGINSHADEBOX]

**要求**

```SHELL
curl -X GET https://platform.adobe.io/data/foundation/schemaregistry/global/classes \
  -H 'Accept: application/vnd.adobe.xed-id+json' \
  -H 'Authorization: Bearer {{ACCESS_TOKEN}}' \
  -H 'x-api-key: {{API_KEY}}' \
  -H 'x-gw-ims-org-id: {{ORG_ID}}'
```

**回應**

如果您的回應與下方所示的回應類似，表示您的認證有效且運作正常。 （此回應已因空間而遭截斷。）

```JSON
{
  "results": [
    {
        "title": "XDM ExperienceEvent",
        "$id": "https://ns.adobe.com/xdm/context/experienceevent",
        "meta:altId": "_xdm.context.experienceevent",
        "version": "1"
    },
    {
        "title": "XDM Individual Profile",
        "$id": "https://ns.adobe.com/xdm/context/profile",
        "meta:altId": "_xdm.context.profile",
        "version": "1"
    }
  ]
}
```

>[!ENDSHADEBOX]

>[!IMPORTANT]
>
雖然上述呼叫足以測試您的存取認證，但請注意，您若沒有正確的屬性型存取控制許可權，將無法存取或修改數個資源。 請閱讀以下內容： **取得必要的屬性型存取控制許可權** 一節。

## 取得必要的屬性型存取控制許可權 {#get-abac-permissions}

若要存取或修改Experience Platform中的數個資源，您必須擁有適當的存取控制許可權。 系統管理員可授與您下列許可權： [您需要的許可權](/help/access-control/ui/permissions.md). 在本節中取得更多關於 [管理角色的API認證](/help/access-control/abac/ui/permissions.md#manage-api-credentials-for-role).

有關系統管理員如何授與所需許可權以透過API存取Platform資源的詳細資訊，也可在以下教學影片中取得：

>[!VIDEO](https://video.tv.adobe.com/v/28832/?learn=on&t=159)

## 使用Postman驗證及測試API呼叫 {#use-postman}

[Postman](https://www.postman.com/) 是常見的工具，可讓開發人員探索和測試RESTful API。 您可以使用Experience Platform Postman集合和環境來加速使用Experience Platform API。 深入瞭解 [在Experience Platform中使用Postman](/help/landing/postman.md) 以及開始使用集合和環境。

有關將Postman與Experience Platform集合和環境一起使用的詳細資訊，也可在以下影片教學課程中取得：

**下載並匯入Postman環境以搭配Experience Platform API使用**

>[!VIDEO](https://video.tv.adobe.com/v/28832/?learn=on&t=106)

**使用Postman集合來產生存取權杖**

下載 [Identity Management服務Postman集合](https://github.com/adobe/experience-platform-postman-samples/tree/master/apis/ims) 並觀看以下影片，瞭解如何產生存取權杖。

>[!VIDEO](https://video.tv.adobe.com/v/29698/?learn=on)

**下載Experience Platform API Postman集合併與API互動**

>[!VIDEO](https://video.tv.adobe.com/v/29704/?learn=on)

<!--
This [Medium post](https://medium.com/adobetech/using-postman-for-jwt-authentication-on-adobe-i-o-7573428ffe7f) describes how you can set up Postman to automatically perform JWT authentication and use it to consume Platform APIs.
-->

## 系統管理員：透過Experience Platform許可權授予開發人員和API存取控制 {#grant-developer-and-api-access-control}

>[!NOTE]
>
只有系統管理員才能在「許可權」中檢視和管理API認證。

在Adobe Developer Console上建立整合之前，您的帳戶必須擁有Adobe Admin Console中Experience Platform產品設定檔的開發人員和使用者許可權。

### 將開發人員新增至產品設定檔 {#add-developers-to-product-profile}

移至 [[!DNL Admin Console]](https://adminconsole.adobe.com/) 並使用您的 Adobe ID 登入。

選取 **[!UICONTROL 產品]**，然後選取 **[!UICONTROL Adobe Experience Platform]** 從產品清單中。

![Admin Console上的產品清單](././images/api-authentication/products.png)

從 **[!UICONTROL 產品設定檔]** 索引標籤，選取 **[!UICONTROL AEP-Default-All-Users]**. 或者，使用搜尋列透過輸入名稱來搜尋產品描述檔。

![搜尋產品設定檔](././images/api-authentication/select-product-profile.png)

選取 **[!UICONTROL 開發人員]** 索引標籤，然後選取 **[!UICONTROL 新增開發人員]**.

![從「開發人員」標籤新增開發人員](././images/api-authentication/add-developer1.png)

輸入開發人員的 **[!UICONTROL 電子郵件或使用者名稱]**. 有效的 [!UICONTROL 電子郵件或使用者名稱] 將顯示開發人員詳細資訊。 選取「**[!UICONTROL 儲存]**」。

![使用開發人員的電子郵件或使用者名稱新增開發人員](././images/api-authentication/add-developer-email.png)

已成功新增開發人員，並出現在 [!UICONTROL 開發人員] 標籤。

![「開發人員」標籤上列出的開發人員](././images/api-authentication/developer-added.png)

<!--

Commenting out this part since it duplicates information from the section Add Experience Platform to a project

### Set up an API

A developer can add and configure an API within a project in the Adobe Developer Console.

Select your project, then select **[!UICONTROL Add API]**.

![Add API to a project](././images/api-authentication/add-api-project.png)

In the **[!UICONTROL Add an API]** dialog box select **[!UICONTROL Adobe Experience Platform]**, then select **[!UICONTROL Experience Platform API]**.

![Add an API in Experience Platform](././images/api-authentication/add-api-platform.png)

In the **[!UICONTROL Configure API]** screen, select **[!UICONTROL AEP-Default-All-Users]**.

-->

### 將API指派給角色

系統管理員可以將API指派給Experience PlatformUI中的角色。

選取 **[!UICONTROL 許可權]** 以及您想要新增API的角色。 選取 **[!UICONTROL API認證]** 索引標籤，然後選取 **[!UICONTROL 新增API認證]**.

![所選角色中的API認證索引標籤](././images/api-authentication/api-credentials.png)

選取您要新增至角色的API，然後選取 **[!UICONTROL 儲存]**.

![可供選擇的API清單](././images/api-authentication/select-api.png)

您將返回 [!UICONTROL API認證] 索引標籤，其中列出新新增的API。

![使用新增API的API憑證標籤](././images/api-authentication/api-credentials-with-added-api.png)

## 其他資源 {#additional-resources}

請參閱以下連結的其他資源，以取得開始使用Experience PlatformAPI的更多說明

* [驗證及存取Experience PlatformAPI](https://experienceleague.adobe.com/docs/platform-learn/tutorials/platform-api-authentication.html?lang=zh-Hant) 視訊教學課程頁面
* [Identity Management服務Postman集合](https://github.com/adobe/experience-platform-postman-samples/tree/master/apis/ims) 用於產生存取權杖
* [Experience PlatformAPI Postman集合](https://github.com/adobe/experience-platform-postman-samples/tree/master/apis/experience-platform)

## 後續步驟 {#next-steps}

閱讀本檔案後，您已收集並成功測試您的Platform API存取認證。 您現在可以跟隨在整個中提供的範例API呼叫 [檔案](../landing/documentation/overview.md).

除了您在本教學課程中收集的驗證值之外，許多Platform API也需要有效的 `{SANDBOX_NAME}` 提供為標題。 如需詳細資訊，請參閱[沙箱概觀](../sandboxes/home.md)。