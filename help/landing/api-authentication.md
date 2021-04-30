---
keywords: Experience Platform;home；熱門主題；驗證；訪問
solution: Experience Platform
title: 驗證和存取Experience PlatformAPI
topic-legacy: tutorial
type: Tutorial
description: 本文件逐步說明如何存取 Adobe Experience Platform 開發人員帳戶，進而呼叫 Experience Platform API。
exl-id: dfe8a7be-1b86-4d78-a27e-87e4ed8b3d42
translation-type: tm+mt
source-git-commit: ef00f50ea2cda2c173208075123b3fe2b2d7ecd4
workflow-type: tm+mt
source-wordcount: '1165'
ht-degree: 6%

---


# 驗證及存取 Experience Platform API

本文件逐步說明如何存取 Adobe Experience Platform 開發人員帳戶，進而呼叫 Experience Platform API。在本教學課程結束時，您將會產生下列所有平台API呼叫所需的認證：

* `{ACCESS_TOKEN}`
* `{API_KEY}`
* `{IMS_ORG}`

為了維護應用程式和使用者的安全性，對Adobe I/OAPI的所有要求都必須使用OAuth和JSON Web Token(JWT)等標準進行驗證和授權。 JWT與用戶端特定資訊一起使用，以產生您的個人存取Token。

本教學課程涵蓋如何收集驗證平台API呼叫所需的認證，如下列流程圖所述：

![](./images/api-authentication/authentication-flowchart.png)

## 先決條件

若要成功呼叫Experience PlatformAPI，您必須具備下列功能：

* 可存取Adobe Experience Platform的IMS組織。
* Admin Console管理員，可以將您新增為產品設定檔的開發人員和使用者。

您還必須有Adobe ID才能完成本教學課程。 如果您沒有Adobe ID，則可使用下列步驟建立一個：

1. 前往[Adobe開發人員主控台](https://console.adobe.io)。
2. 選擇「**[!UICONTROL Create a new account]**」。
3. 完成註冊程式。

## 取得開發人員和使用者的Experience Platform存取權

在Adobe開發人員主控台上建立整合之前，您的帳戶必須擁有Adobe Admin ConsoleExperience Platform產品設定檔的開發人員和使用者權限。

### 取得開發人員存取權

請洽詢您組織中的[!DNL Admin Console]管理員，以便使用[[!DNL Admin Console]](https://adminconsole.adobe.com/)將您新增為Experience Platform產品設定檔的開發人員。 請參閱[!DNL Admin Console]檔案，以取得有關如何[管理產品設定檔的開發人員存取權的特定指示。](https://helpx.adobe.com/enterprise/admin-guide.html/enterprise/using/manage-developers.ug.html)

一旦您被指派為開發人員，就可以開始在[Adobe開發人員主控台](https://www.adobe.com/go/devs_console_ui)中建立整合。 這些整合是從外部應用程式與服務到AdobeAPI的管道。

### 取得使用者存取權

您的[!DNL Admin Console]管理員也必須以使用者身分將您新增至相同的產品設定檔。 如需詳細資訊，請參閱 [!DNL Admin Console]](https://helpx.adobe.com/enterprise/admin-guide.html/enterprise/using/user-groups.ug.html)中[管理使用者群組的指南。

## 產生API金鑰、IMS組織ID和用戶端密碼{#api-ims-secret}

>[!NOTE]
>
>如果您正在從[Privacy Service開發人員指南](../privacy-service/api/getting-started.md)中遵循本文檔，現在可返回該指南以生成[!DNL Privacy Service]的唯一訪問憑據。

在您透過[!DNL Admin Console]獲得開發人員和使用者對平台的存取權後，下一步是在Adobe開發人員主控台中產生您的`{IMS_ORG}`和`{API_KEY}`認證。 這些憑證只需產生一次，就可在日後的平台API呼叫中重複使用。

### 新增Experience Platform至專案

前往[Adobe開發人員主控台](https://www.adobe.com/go/devs_console_ui)並使用您的Adobe ID登入。 接下來，請依照[教學課程中描述的步驟，在「Adobe開發人員主控台」檔案中建立空白專案](https://www.adobe.io/apis/experienceplatform/console/docs.html#!AdobeDocs/adobeio-console/master/projects-empty.md)。

建立新專案後，請在&#x200B;**[!UICONTROL Project Overview]**&#x200B;畫面上選取&#x200B;**[!UICONTROL Add API]**。

![](./images/api-authentication/add-api.png)

出現&#x200B;**[!UICONTROL Add an API]**&#x200B;螢幕。 選擇Adobe Experience Platform的產品表徵圖，然後選擇&#x200B;**[!UICONTROL Experience Platform API]**，再選擇&#x200B;**[!UICONTROL Next]**。

![](./images/api-authentication/platform-api.png)

從這裡開始，請依照[教學課程中描述的步驟，使用服務帳戶(JWT)](https://www.adobe.io/apis/experienceplatform/console/docs.html#!AdobeDocs/adobeio-console/master/services-add-api-jwt.md)（從「設定API」步驟開始）將API新增至專案，以完成程式。

>[!IMPORTANT]
>
>在上述連結程式中，您的瀏覽器會在特定步驟中自動下載私密金鑰和相關的公開憑證。 請注意，此私密金鑰儲存在您的機器上的位置，因為本教學課程的後續步驟中需要此私密金鑰。

### 收集認證

將API新增至專案後，專案的&#x200B;**[!UICONTROL Experience Platform API]**&#x200B;頁面會顯示所有對Experience PlatformAPI的呼叫所需的下列認證：

* `{API_KEY}` ([!UICONTROL Client ID])
* `{IMS_ORG}` ([!UICONTROL Organization ID])

![](././images/api-authentication/api-key-ims-org.png)

除了上述認證外，您還需要生成的&#x200B;**[!UICONTROL Client Secret]**&#x200B;以用於將來的步驟。 選擇&#x200B;**[!UICONTROL Retrieve client secret]**&#x200B;以顯示值，然後複製該值以供日後使用。

![](././images/api-authentication/client-secret.png)

## 產生JSON Web Token(JWT){#jwt}

下一步是根據您的帳戶認證產生JSON Web Token(JWT)。 此值用於產生`{ACCESS_TOKEN}`憑證，以便用於平台API呼叫，此憑證必須每24小時重新產生一次。

在左側導覽中選取&#x200B;**[!UICONTROL Service Account (JWT)]**，然後選取&#x200B;**[!UICONTROL Generate JWT]**。

![](././images/api-authentication/generate-jwt.png)

在&#x200B;**[!UICONTROL Generate custom JWT]**&#x200B;下方的文字方塊中，貼上您在將平台API新增至服務帳戶時先前產生的私密金鑰內容。 然後，選擇&#x200B;**[!UICONTROL Generate Token]**。

![](././images/api-authentication/paste-key.png)

頁面會更新，以顯示產生的JWT，以及可讓您產生存取Token的範例cURL命令。 在本教學課程中，請選取&#x200B;**[!UICONTROL Generated JWT]**&#x200B;旁的&#x200B;**[!UICONTROL Copy]**，將Token複製到剪貼簿。

![](././images/api-authentication/copy-jwt.png)

## 產生存取Token

生成JWT後，可在API調用中使用它來生成`{ACCESS_TOKEN}`。 與`{API_KEY}`和`{IMS_ORG}`的值不同，必須每24小時產生一個新Token，才能繼續使用平台API。

**要求**

以下請求根據裝載中提供的憑據生成新的`{ACCESS_TOKEN}`。 此端點僅接受表單資料作為其有效負載，因此必須為其指定`multipart/form-data`的`Content-Type`標題。

```shell
curl -X POST https://ims-na1.adobelogin.com/ims/exchange/jwt \
  -H 'Content-Type: multipart/form-data' \
  -F 'client_id={API_KEY}' \
  -F 'client_secret={SECRET}' \
  -F 'jwt_token={JWT}'
```

| 屬性 | 說明 |
| --- | --- |
| `{API_KEY}` | 您在上一步驟[中擷取的`{API_KEY}`([!UICONTROL Client ID])。](#api-ims-secret) |
| `{SECRET}` | 您在上一步[中擷取的用戶端密碼](#api-ims-secret)。 |
| `{JWT}` | 您在上一步[中生成的JWT](#jwt)。 |

>[!NOTE]
>
>您可以使用相同的API金鑰、用戶端密碼和JWT，為每個作業產生新的存取Token。 這可讓您在應用程式中自動產生存取Token。

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
| `token_type` | 傳回的Token類型。 對於存取Token，此值一律為`bearer`。 |
| `access_token` | 生成的`{ACCESS_TOKEN}`。 所有平台API呼叫的`Authentication`標題中，必須填入前置詞`Bearer`的值。 |
| `expires_in` | 存取Token過期前的剩餘毫秒數。 一旦此值達到0，就必須產生新的存取Token，才能繼續使用平台API。 |

## 測試存取認證

收集完所有三個必要的認證後，您可以嘗試進行下列API呼叫。 此呼叫會列出您組織可用的所有標準[!DNL Experience Data Model](XDM)類別。

**要求**

```SHELL
curl -X GET https://platform.adobe.io/data/foundation/schemaregistry/global/classes \
  -H 'Accept: application/vnd.adobe.xed-id+json' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}'
```

**回應**

如果您的回覆與下方所示的類似，則您的認證有效且有效。 （此回應已針對空格截斷。）

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

## 使用Postman來驗證和測試API呼叫

[Postmanis是](https://www.postman.com/) 一種常用的工具，可讓開發人員探索和測試REST風格的API。本[中篇文章](https://medium.com/adobetech/using-postman-for-jwt-authentication-on-adobe-i-o-7573428ffe7f)說明如何設定Postman以自動執行JWT驗證，並使用它來使用平台API。

## 後續步驟

閱讀本檔案後，您已收集並成功測試了Platform API的存取認證。 您現在可以遵循[documentation](../landing/documentation/overview.md)中提供的範例API呼叫。

除了您在本教學課程中收集的驗證值之外，許多平台API也需要提供有效的`{SANDBOX_NAME}`作為標題。 如需詳細資訊，請參閱[沙盒概述](../sandboxes/home.md)。