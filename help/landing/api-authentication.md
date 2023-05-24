---
keywords: Experience Platform；首頁；熱門主題；驗證；訪問
solution: Experience Platform
title: 驗證和訪問Experience PlatformAPI
type: Tutorial
description: 本文件逐步說明如何存取 Adobe Experience Platform 開發人員帳戶，進而呼叫 Experience Platform API。
exl-id: dfe8a7be-1b86-4d78-a27e-87e4ed8b3d42
source-git-commit: fa4786b081b46c8f3c0030282ae3900891fbd652
workflow-type: tm+mt
source-wordcount: '1581'
ht-degree: 6%

---


# 驗證及存取 Experience Platform API

本文件逐步說明如何存取 Adobe Experience Platform 開發人員帳戶，進而呼叫 Experience Platform API。在本教程結束時，您將生成所有平台API調用所需的以下憑據：

* `{ACCESS_TOKEN}`
* `{API_KEY}`
* `{ORG_ID}`

要維護應用程式和用戶的安全，必須使用OAuth和JSON Web令牌(JWT)等標準對Adobe I/OAPI的所有請求進行身份驗證和授權。 JWT與特定於客戶端的資訊一起使用，以生成您的個人訪問令牌。

本教程介紹如何收集驗證平台API調用所需的憑據，如下圖所示：

![](./images/api-authentication/authentication-flowchart.png)

## 先決條件

為了成功調用Experience PlatformAPI，必須具備以下條件：

* 一個能進入Adobe Experience Platform的組織。
* 能夠將您添加為產品配置檔案的開發人員和用戶的Admin Console管理員。

您還必須擁有一個Adobe ID才能完成本教程。 如果沒有Adobe ID，可以使用以下步驟建立一個：

1. 轉到 [Adobe Developer控制台](https://console.adobe.io)。
2. 選擇 **[!UICONTROL 建立新帳戶]**。
3. 完成註冊過程。

## 獲得開發人員和用戶訪問權以進行Experience Platform

在Adobe Developer控制台上建立整合之前，您的帳戶必須具有Adobe Admin ConsoleExperience Platform產品配置檔案的開發人員和用戶權限。

### 獲取開發人員訪問權限

聯繫 [!DNL Admin Console] 組織中的管理員，以將您作為開發人員添加到Experience Platform產品配置檔案中 [[!DNL Admin Console]](https://adminconsole.adobe.com/)。 查看 [!DNL Admin Console] 文檔，瞭解有關如何 [管理產品配置檔案的開發人員訪問](https://helpx.adobe.com/enterprise/admin-guide.html/enterprise/using/manage-developers.ug.html)。

一旦您被分配為開發人員，就可以開始在 [Adobe Developer控制台](https://www.adobe.com/go/devs_console_ui)。 這些整合是從外部應用和服務到AdobeAPI的管道。

### 獲取用戶訪問權限

您 [!DNL Admin Console] 管理員還必須將您作為用戶添加到同一產品配置檔案中。 請參閱上的指南 [管理用戶組 [!DNL Admin Console]](https://helpx.adobe.com/enterprise/admin-guide.html/enterprise/using/user-groups.ug.html) 的子菜單。

## 生成API密鑰、組織ID和客戶端密鑰 {#api-ims-secret}

>[!NOTE]
>
>如果您從 [Privacy ServiceAPI指南](../privacy-service/api/getting-started.md)，現在可以返回該指南以生成唯一的訪問憑據 [!DNL Privacy Service]。

在您獲得開發人員和用戶對平台的訪問權後， [!DNL Admin Console]，下一步是生成 `{ORG_ID}` 和 `{API_KEY}` Adobe Developer控制台中的憑據。 這些憑據只需生成一次，並可在以後的平台API調用中重用。

### 向項目添加Experience Platform

轉到 [Adobe Developer控制台](https://www.adobe.com/go/devs_console_ui) 和你的Adobe ID登錄。 接下來，按照本教程中介紹的步驟操作 [建立空項目](https://developer.adobe.com/developer-console/docs/guides/projects/projects-empty/) 在Adobe Developer控制台文檔中。

建立新項目後，選擇 **[!UICONTROL 添加API]** 的 **[!UICONTROL 項目概述]** 的上界。

![](./images/api-authentication/add-api.png)

的 **[!UICONTROL 添加API]** 的上界。 選擇Adobe Experience Platform的產品表徵圖，然後選擇 **[!UICONTROL Experience PlatformAPI]** 選擇 **[!UICONTROL 下一個]**。

![](./images/api-authentication/platform-api.png)

在此處，按照本教程中介紹的步驟操作 [使用服務帳戶(JWT)向項目添加API](https://www.adobe.io/apis/experienceplatform/console/docs.html#!AdobeDocs/adobeio-console/master/services-add-api-jwt.md) （從「配置API」步驟開始）以完成該過程。

>[!IMPORTANT]
>
>在上面連結的過程中，在某個步驟中，瀏覽器會自動下載私鑰和關聯的公共證書。 請注意，此私鑰儲存在您的電腦上的位置，因為在本教程的後續步驟中需要它。

### 收集憑據

API添加到項目後， **[!UICONTROL Experience PlatformAPI]** 項目的頁面顯示所有對Experience PlatformAPI的調用所需的以下憑據：

* `{API_KEY}` ([!UICONTROL 客戶端ID])
* `{ORG_ID}` ([!UICONTROL 組織 ID])

![](././images/api-authentication/api-key-ims-org.png)

除了上述憑據外，您還需要生成 **[!UICONTROL 客戶端密碼]** 以後的一步。 選擇 **[!UICONTROL 檢索客戶端密鑰]** 顯示值，然後複製以供以後使用。

![](././images/api-authentication/client-secret.png)

## 生成JSON Web令牌(JWT) {#jwt}

下一步是根據帳戶憑據生成JSON Web令牌(JWT)。 此值用於生成 `{ACCESS_TOKEN}` 用於平台API調用的憑據，必須每24小時重新生成一次。

>[!IMPORTANT]
>
>在本教程中，以下步驟概述了如何在開發人員控制台中生成JWT。 但是，這種生成方法只應用於測試和評估。
>
>為了經常使用，必須自動生成JWT。 有關如何以寫程式方式生成JWT的詳細資訊，請參見 [服務帳戶驗證指南](https://www.adobe.io/developer-console/docs/guides/authentication/JWT/) Adobe Developer。

選擇 **[!UICONTROL 服務帳戶(JWT)]** 在左側導航中，然後選擇 **[!UICONTROL 生成JWT]**。

![](././images/api-authentication/generate-jwt.png)

在下面提供的文本框中 **[!UICONTROL 生成自定義JWT]**，貼上在將平台API添加到服務帳戶時先前生成的私鑰的內容。 然後，選擇 **[!UICONTROL 生成令牌]**。

![](././images/api-authentication/paste-key.png)

頁面將更新以顯示生成的JWT，並附帶一個示例cURL命令，該命令允許您生成訪問令牌。 為本教程的目的，請選擇 **[!UICONTROL 複製]** 下 **[!UICONTROL 生成的JWT]** 將標籤複製到剪貼簿。

![](././images/api-authentication/copy-jwt.png)

## 生成訪問令牌

生成JWT後，可以在API調用中使用它來生成 `{ACCESS_TOKEN}`。 與 `{API_KEY}` 和 `{ORG_ID}`，必須每24小時生成一個新令牌才能繼續使用平台API。

**要求**

以下請求將生成新請求 `{ACCESS_TOKEN}` 基於負載中提供的憑據。 此終結點只接受表單資料作為其負載，因此必須為它提供 `Content-Type` 標題 `multipart/form-data`。

```shell
curl -X POST https://ims-na1.adobelogin.com/ims/exchange/jwt \
  -H 'Content-Type: multipart/form-data' \
  -F 'client_id={API_KEY}' \
  -F 'client_secret={SECRET}' \
  -F 'jwt_token={JWT}'
```

| 屬性 | 說明 |
| --- | --- |
| `{API_KEY}` | 的 `{API_KEY}` ([!UICONTROL 客戶端ID]) [上一步](#api-ims-secret)。 |
| `{SECRET}` | 您在中檢索到的客戶機密碼 [上一步](#api-ims-secret)。 |
| `{JWT}` | 您在 [上一步](#jwt)。 |

>[!NOTE]
>
>可以使用相同的API密鑰、客戶端密鑰和JWT為每個會話生成新的訪問令牌。 這允許您自動在應用程式中生成訪問令牌。

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
| `token_type` | 要返回的令牌的類型。 對於訪問令牌，此值始終 `bearer`。 |
| `access_token` | 生成的 `{ACCESS_TOKEN}`。 此值，前置詞為單詞 `Bearer`，作為 `Authentication` 所有平台API調用的標頭。 |
| `expires_in` | 在訪問令牌過期之前剩餘的毫秒數。 一旦此值達到0，則必須生成新的訪問令牌才能繼續使用平台API。 |

## Test訪問憑據

收集了所有三個所需憑據後，可嘗試進行以下API調用。 此呼叫列出所有標準 [!DNL Experience Data Model] (XDM)類可供您的組織使用。

**要求**

```SHELL
curl -X GET https://platform.adobe.io/data/foundation/schemaregistry/global/classes \
  -H 'Accept: application/vnd.adobe.xed-id+json' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}'
```

**回應**

如果您的響應與下面顯示的類似，則您的憑據有效且有效。 （此響應已被截斷為空間。）

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

## 使用Postman驗證和testAPI調用

[Postman](https://www.postman.com/) 是一種常用工具，可讓開發人員瀏覽和testREST風格的API。 此 [中柱](https://medium.com/adobetech/using-postman-for-jwt-authentication-on-adobe-i-o-7573428ffe7f) 介紹如何設定Postman以自動執行JWT驗證並使用它來使用平台API。

## 具有Experience Platform權限的開發人員和API訪問控制

>[!NOTE]
>
>只有系統管理員才能查看和管理權限中的API憑據。

在Adobe Developer控制台上建立整合之前，您的帳戶必須具有Adobe Admin ConsoleExperience Platform產品配置檔案的開發人員和用戶權限。

### 將開發人員添加到產品配置檔案

移至 [[!DNL Admin Console]](https://adminconsole.adobe.com/) 並使用您的 Adobe ID 登入。

選擇 **[!UICONTROL 產品]**，然後選擇 **[!UICONTROL Adobe Experience Platform]** 從產品清單中。

![產品清單Admin Console](././images/api-authentication/products.png)

從 **[!UICONTROL 產品配置檔案]** 頁籤 **[!UICONTROL AEP — 預設 — 所有用戶]**。 或者，使用搜索欄通過輸入名稱來搜索產品配置檔案。

![搜索產品配置檔案](././images/api-authentication/select-product-profile.png)

選擇 **[!UICONTROL 開發人員]** ，然後選擇 **[!UICONTROL 添加開發人員]**。

![從「開發人員」頁籤添加開發人員](././images/api-authentication/add-developer1.png)

輸入開發人員的 **[!UICONTROL 電子郵件或用戶名]**。 有效 [!UICONTROL 電子郵件或用戶名] 將顯示開發人員詳細資訊。 選取「**[!UICONTROL 儲存]**」。

![使用其電子郵件或用戶名添加開發人員](././images/api-authentication/add-developer-email.png)

已成功添加開發人員，並在 [!UICONTROL 開發人員] 頁籤。

![「開發人員」頁籤上列出的開發人員](././images/api-authentication/developer-added.png)

### 設定API

開發人員可以在Adobe Developer控制台的項目中添加和配置API。

選擇項目，然後選擇 **[!UICONTROL 添加API]**。

![向項目添加API](././images/api-authentication/add-api-project.png)

在 **[!UICONTROL 添加API]** 對話框 **[!UICONTROL Adobe Experience Platform]**，然後選擇 **[!UICONTROL Experience PlatformAPI]**。

![在Experience Platform中添加API](././images/api-authentication/add-api-platform.png)

在 **[!UICONTROL 配置API]** 螢幕，選擇 **[!UICONTROL AEP — 預設 — 所有用戶]**。

### 將API分配給角色

系統管理員可以將API分配給Experience PlatformUI中的角色。

選擇 **[!UICONTROL 權限]** 以及要將API添加到的角色。 選擇 **[!UICONTROL API憑據]** ，然後選擇 **[!UICONTROL 添加API憑據]**。

![選定角色中的API憑據頁籤](././images/api-authentication/api-credentials.png)

選擇要添加到角色的API，然後選擇 **[!UICONTROL 保存]**。

![可供選擇的API清單](././images/api-authentication/select-api.png)

您返回 [!UICONTROL API憑據] 的子菜單。

![帶有新添加的API的API憑據頁籤](././images/api-authentication/api-credentials-with-added-api.png)

## 後續步驟

通過閱讀此文檔，您已收集並成功測試了平台API的訪問憑據。 現在，您可以隨附在 [文檔](../landing/documentation/overview.md)。

除了在本教程中收集的驗證值之外，許多平台API還需要有效的 `{SANDBOX_NAME}` 作為標題提供。 如需詳細資訊，請參閱[沙箱概觀](../sandboxes/home.md)。