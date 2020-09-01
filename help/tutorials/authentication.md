---
keywords: Experience Platform;home;popular topics;Authenticate;access
solution: Experience Platform
title: 驗證及存取Experience Platform API
topic: tutorial
description: '本檔案提供逐步教學課程，以存取Adobe Experience Platform開發人員帳戶，以呼叫Experience Platform API。 '
translation-type: tm+mt
source-git-commit: d3ece56d10b1940a5992906a65a50ffe2f7e4346
workflow-type: tm+mt
source-wordcount: '878'
ht-degree: 1%

---


# 驗證和存取 [!DNL Experience Platform] API

本檔案提供逐步教學課程，以存取Adobe Experience Platform開發人員帳戶，以便呼叫 [!DNL Experience Platform] API。

## 驗證以進行API呼叫

為了維護應用程式和使用者的安全性，對Adobe I/O API的所有要求都必須使用OAuth和JSON Web Token(JWT)等標準進行驗證和授權。 然後，JWT會與用戶端特定資訊一起使用，以產生您的個人存取Token。

本教學課程涵蓋透過建立存取Token來驗證的步驟，其流程圖如下：
![](images/authentication/authentication-flowchart.png)

## 必要條件

為了成功呼叫 [!DNL Experience Platform] API，您需要：

* 可存取Adobe Experience Platform的IMS組織
* 已註冊的Adobe ID帳戶
* Admin Console管理員可將您新增為 **開發人****員和** 產品使用者。

以下各節將逐步說明建立Adobe ID並成為組織的開發人員和使用者的步驟。

### 建立Adobe ID

如果您沒有Adobe ID，可使用下列步驟建立Adobe ID:

1. 前往 [Adobe Developer Console](https://console.adobe.io)
2. 按一 **[!UICONTROL 下建立新帳戶]**
3. 完成註冊程式

## 成為組織的開發人員 [!DNL Experience Platform] 和使用者

在Adobe I/O上建立整合之前，您的帳戶必須擁有IMS組織中產品的開發人員權限。 有關Admin Console開發人員帳戶的詳細資訊，請參閱管理開發人 [員的支援](https://helpx.adobe.com/tw/enterprise/using/manage-developers.html) 檔案。

**取得開發人員存取權**

請連絡 [!DNL Admin Console] 您組織中的管理員，以便使用「 [[!DNL管理控制台」將您新增為組織產品的開發人員](https://adminconsole.adobe.com/)。

![](images/authentication/assign-developer.png)

管理員必須將您指派為開發人員，以至少指派一個產品設定檔繼續。

![](images/authentication/add-developer.png)

一旦您被指派為開發人員，您就擁有在 [Adobe I/O上建立整合的存取權限](https://www.adobe.com/go/devs_console_ui)。 這些整合是從外部應用程式和服務到Adobe API的管道。

**取得使用者存取權**

您的 [!DNL Admin Console] 管理員也必須以使用者身分將您加入產品。

![](images/authentication/assign-users.png)

與新增開發人員的程式類似，管理員必須指派您至少一個產品設定檔，才能繼續。

![](images/authentication/assign-user-details.png)

## 在Adobe Developer Console中產生存取認證

>[!NOTE]
>
>如果您要從「隱私服務開發人員指南」中遵循本檔案 [，現在可以返回該指南，以產生唯一的存取憑證](../privacy-service/api/getting-started.md)[!DNL Privacy Service]。

使用Adobe Developer Console，您必須產生下列三種存取憑證：

* `{IMS_ORG}`
* `{API_KEY}`
* `{ACCESS_TOKEN}`

您 `{IMS_ORG}` 的 `{API_KEY}` API呼叫只需產生一次，就可重複使用 [!DNL Platform] 。 但是，您的 `{ACCESS_TOKEN}` 作業是暫時的，必須每24小時重新生一次。

這些步驟將在下面詳細介紹。

### 一次性設定

前往 [Adobe Developer Console](https://www.adobe.com/go/devs_console_ui) ，使用您的Adobe ID登入。 接著，請依照教學課程中說明的步驟， [在Adobe Developer Console檔案中建立空白的專案](https://www.adobe.io/apis/experienceplatform/console/docs.html#!AdobeDocs/adobeio-console/master/projects-empty.md) 。

建立新專案後，按一下「專 **[!UICONTROL 案概述」畫面上的]**_「新增API_ 」。

![](images/authentication/add-api-button.png)

出現 _「Add an API_ （添加API）」螢幕。 按一下Adobe Experience Platform的產品圖示，然後選取「 **[!UICONTROL Experience Platform API]** 」，再按 **[!UICONTROL 「Next」]**。

![](images/authentication/add-platform-api.png)

在您選取要新 [!DNL Experience Platform] 增至專案的API後，請依照教學課程中所述的步驟，使用服務帳戶( [JWT)](https://www.adobe.io/apis/experienceplatform/console/docs.html#!AdobeDocs/adobeio-console/master/services-add-api-jwt.md) （從「設定API」步驟開始）將API新增至專案，以完成程式。

將API新增至專案後，「專案概述 _」頁面會顯示所有對API的呼叫所需的_[!DNL Experience Platform] 下列憑證：

* `{API_KEY}` （用戶端ID）
* `{IMS_ORG}` (組織 ID)

![](./images/authentication/api-key-ims-org.png)

### 每個會話的驗證

您必須收集的最終必要憑證是您的 `{ACCESS_TOKEN}`。 與和的值不 `{API_KEY}` 同， `{IMS_ORG}`必須每24小時產生一個新的Token，才能繼續使用 [!DNL Platform] API。

若要產生新 `{ACCESS_TOKEN}`的Developer Console認證指南， [請依照步驟產生JWT Token](https://www.adobe.io/apis/experienceplatform/console/docs.html#!AdobeDocs/adobeio-console/master/credentials.md) 。

## 測試存取認證

收集完所有三個必要的認證後，您可以嘗試進行下列API呼叫。 此調用將列出 [!DNL Experience Data Model] 方案註冊表容器內的所有(XDM)類 `global` :

**API格式**

```http
GET /global/classes
```

**請求**

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

[Postman](https://www.getpostman.com/) 是使用REST風格API的常用工具。 此 [中篇貼文](https://medium.com/adobetech/using-postman-for-jwt-authentication-on-adobe-i-o-7573428ffe7f) ，說明如何設定郵遞員以自動執行JWT驗證，並使用它來使用Adobe Experience Platform API。

## 後續步驟

閱讀本檔案後，您已收集並成功測試API的存取認 [!DNL Platform] 證。 您現在可以遵循檔案中提供的範例API呼 [叫](../landing/documentation/overview.md)。

除了您在本教學課程中收集的驗證值外，許多 [!DNL Platform] API也需要提供有 `{SANDBOX_NAME}` 效的標頭。 如需詳細 [資訊，請參閱](../sandboxes/home.md) 「沙盒總覽」。