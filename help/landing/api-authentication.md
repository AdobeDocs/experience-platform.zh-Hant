---
keywords: Experience Platform;home；熱門主題；驗證；訪問
solution: Experience Platform
title: 驗證和存取Experience PlatformAPI
topic-legacy: tutorial
type: Tutorial
description: 本文件逐步說明如何存取 Adobe Experience Platform 開發人員帳戶，進而呼叫 Experience Platform API。
exl-id: dfe8a7be-1b86-4d78-a27e-87e4ed8b3d42
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '896'
ht-degree: 4%

---

# 驗證並存取[!DNL Experience Platform] API

本檔案提供逐步教學課程，以存取Adobe Experience Platform開發人員帳戶，以呼叫[!DNL Experience Platform] API。

## 驗證以進行API呼叫

為了維護應用程式和使用者的安全性，對Adobe I/OAPI的所有要求都必須使用OAuth和JSON Web Token(JWT)等標準進行驗證和授權。 然後，JWT會與用戶端特定資訊一起使用，以產生您的個人存取Token。

本教學課程涵蓋透過建立存取Token來驗證的步驟，其流程圖如下：
![](images/api-authentication/authentication-flowchart.png)

## 先決條件

為了成功呼叫[!DNL Experience Platform] API，您需要：

* 可訪問Adobe Experience Platform的IMS組織
* 註冊的Adobe ID帳戶
* Admin Console管理員，可將您新增為產品的&#x200B;**開發人員**&#x200B;和&#x200B;**使用者**。

以下各節將逐步介紹建立Adobe ID並成為組織的開發人員和使用者的步驟。

### 建立Adobe ID

如果您沒有Adobe ID，則可使用下列步驟建立一個：

1. 前往[Adobe開發人員主控台](https://console.adobe.io)
2. 選擇 **[!UICONTROL create a new account]**
3. 完成註冊程式

## 成為組織[!DNL Experience Platform]的開發人員和使用者

在Adobe I/O上建立整合之前，您的帳戶必須擁有IMS組織中產品的開發人員權限。 有關Admin Console開發人員帳戶的詳細資訊，請參閱[支援檔案](https://helpx.adobe.com/tw/enterprise/using/manage-developers.html)中，以管理開發人員。

**取得開發人員存取權**

請洽詢您組織中的[!DNL Admin Console]管理員，以便使用[[!DNL Admin Console]](https://adminconsole.adobe.com/)新增您為您組織其中一項產品的開發人員。

![](images/api-authentication/assign-developer.png)

管理員必須將您指派為開發人員，以至少指派一個產品設定檔繼續。

![](images/api-authentication/add-developer.png)

一旦您被指派為開發人員，您將擁有在[Adobe I/O](https://www.adobe.com/go/devs_console_ui)上建立整合的存取權限。 這些整合是從外部應用程式與服務到AdobeAPI的管道。

**取得使用者存取權**

您的[!DNL Admin Console]管理員也必須以使用者身分將您新增至產品。

![](images/api-authentication/assign-users.png)

與新增開發人員的程式類似，管理員必須指派您至少一個產品設定檔，才能繼續。

![](images/api-authentication/assign-user-details.png)

## 在Adobe開發人員主控台中產生存取認證

>[!NOTE]
>
>如果您正在從[Privacy Service開發人員指南](../privacy-service/api/getting-started.md)中遵循本文檔，現在可返回該指南以生成[!DNL Privacy Service]的唯一訪問憑據。

使用Adobe開發人員主控台，您必須產生下列三種存取憑證：

* `{IMS_ORG}`
* `{API_KEY}`
* `{ACCESS_TOKEN}`

您的`{IMS_ORG}`和`{API_KEY}`只需產生一次，並可在未來的[!DNL Platform] API呼叫中重複使用。 但是，您的`{ACCESS_TOKEN}`是暫時的，必須每24小時重新產生一次。

這些步驟將在下面詳細介紹。

### 一次性設定

前往[Adobe開發人員主控台](https://www.adobe.com/go/devs_console_ui)並使用您的Adobe ID登入。 接下來，請依照[教學課程中描述的步驟，在「Adobe開發人員主控台」檔案中建立空白專案](https://www.adobe.io/apis/experienceplatform/console/docs.html#!AdobeDocs/adobeio-console/master/projects-empty.md)。

建立新專案後，請在&#x200B;**專案概述**&#x200B;畫面上選取&#x200B;**[!UICONTROL Add API]**。

![](images/api-authentication/add-api-button.png)

出現「**新增API**」畫面。 選擇Adobe Experience Platform的產品表徵圖，然後選擇&#x200B;**[!UICONTROL Experience Platform API]**，再選擇&#x200B;**[!UICONTROL Next]**。

![](images/api-authentication/add-platform-api.png)

選擇[!DNL Experience Platform]作為要添加到項目的API後，請按照[教程中介紹的使用服務帳戶(JWT)](https://www.adobe.io/apis/experienceplatform/console/docs.html#!AdobeDocs/adobeio-console/master/services-add-api-jwt.md)（從「配置API」步驟開始）將API添加到項目的步驟完成該過程。

將API新增至專案後，**專案概述**&#x200B;頁面會顯示所有對[!DNL Experience Platform] API的呼叫所需的下列憑證：

* `{API_KEY}` （用戶端ID）
* `{IMS_ORG}` (組織 ID)

![](./images/api-authentication/api-key-ims-org.png)

### 每個會話的驗證

您必須收集的最終必要憑證是您的`{ACCESS_TOKEN}`。 與`{API_KEY}`和`{IMS_ORG}`的值不同，必須每24小時產生一個新Token，才能繼續使用[!DNL Platform] API。

要生成新`{ACCESS_TOKEN}`，請按照「Developer Console」（開發人員控制台）憑據指南中的[生成JWT Token](https://www.adobe.io/apis/experienceplatform/console/docs.html#!AdobeDocs/adobeio-console/master/credentials.md)的步驟操作。

## 測試存取認證

收集完所有三個必要的認證後，您可以嘗試進行下列API呼叫。 此調用將列出方案註冊表`global`容器中的所有[!DNL Experience Data Model](XDM)類：

**API格式**

```http
GET /global/classes
```

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

## 使用Postman進行JWT驗證和API呼叫

[Postmanis](https://www.postman.com/) 是使用REST風格API的常用工具。此[中篇貼文](https://medium.com/adobetech/using-postman-for-jwt-authentication-on-adobe-i-o-7573428ffe7f)說明如何設定郵遞員以自動執行JWT驗證，並使用它使用Adobe Experience PlatformAPI。

## 後續步驟

閱讀本檔案後，您已收集並成功測試了[!DNL Platform] API的存取憑證。 您現在可以依照[平台API快速入門手冊](api-guide.md)中提供的範例進行。 本指南包含每個平台服務之API指南的連結，並提供其他資訊。 錯誤、Postman和JSON。

除了您在本教學課程中收集的驗證值之外，許多[!DNL Platform] API也需要提供有效的`{SANDBOX_NAME}`作為標題。 如需詳細資訊，請參閱[沙盒概述](../sandboxes/home.md)。
