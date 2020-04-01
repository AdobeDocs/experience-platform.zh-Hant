---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: 驗證及存取Experience Platform API
topic: tutorial
translation-type: tm+mt
source-git-commit: fca15ebf87559b08dd09e63b5df5655b57ef5977

---


# 驗證及存取Experience Platform API

本檔案提供逐步教學課程，以存取Adobe Experience Platform開發人員帳戶，以呼叫Experience Platform API。

## 驗證以進行API呼叫

為了維護應用程式和使用者的安全性，對Adobe I/O API的所有要求都必須使用OAuth和JSON Web Token(JWT)等標準進行驗證和授權。 然後，JWT會與用戶端特定資訊一起使用，以產生您的個人存取Token。

本教學課程涵蓋透過建立存取Token來驗證的步驟，其流程圖如下：
![](images/authentication/authentication-flowchart.png)

## 必要條件

為了成功呼叫Experience Platform API，您需要下列項目：

* 可存取Adobe Experience Platform的IMS組織
* 已註冊的Adobe ID帳戶
* Admin Console管理員可將您新增為 **開發人****員和** 產品使用者。

以下各節將逐步說明建立Adobe ID並成為組織的開發人員和使用者的步驟。

### 建立Adobe ID

如果您沒有Adobe ID，可使用下列步驟建立Adobe ID:

1. 前往 [Adobe I/O Console](https://console.adobe.io)
2. 按一 **下建立新帳戶**
3. 完成註冊程式


### 成為組織Experience Platform的開發人員和使用者

在Adobe I/O上建立整合之前，您的帳戶必須擁有IMS組織中產品的開發人員權限。 有關Admin Console開發人員帳戶的詳細資訊，請參閱管理開發人 [員的支援](https://helpx.adobe.com/enterprise/using/manage-developers.html) 檔案。

**取得開發人員存取權**

請連絡您組織中的Admin Console管理員，以便使用 [Admin Console將您新增為組織產品的開發人員](https://adminconsole.adobe.com/)。

![](images/authentication/assign-developer.png)

管理員必須將您指派為開發人員，以至少指派一個產品設定檔繼續。

![](images/authentication/add-developer.png)

一旦您被指派為開發人員，您就擁有在 [Adobe I/O上建立整合的存取權限](https://console.adobe.io/)。 這些整合是從外部應用程式和服務到Adobe API的管道。

**取得使用者存取權**

您的Admin Console管理員也必須以使用者身分將您新增至產品。

![](images/authentication/assign-users.png)

與新增開發人員的程式類似，管理員必須指派您至少一個產品設定檔，才能繼續。

![](images/authentication/assign-user-details.png)


## 一次性設定

下列步驟只需執行一次：

* 登入Adobe I/O Console
* 建立整合
* 複製向下訪問值

一旦您擁有整合和存取值，您將可以在日後重複使用這些值進行驗證。 以下將詳細說明每個步驟。

### 登入Adobe I/O Console

前往 [Adobe I/O Console](https://console.adobe.io/) ，使用您的Adobe ID登入。

登入後，按一下畫面 **頂端的** 「整合」標籤。 整合是為所選IMS組織建立的服務帳戶。 您只能呼叫建立整合的IMS組織。

>[!NOTE]
>如果您的帳戶與多個組織相關聯，螢幕右上角的下拉式選單可讓您輕鬆地在它們之間切換。

### 建立整合

在「整 **合** 」頁面中，按一 **下「新增整合** 」以啟動程式。 此程式包含三個步驟：
* 選擇整合類型
* 選擇要與
* 新增整合詳細資訊、公開金鑰和產品設定檔

![](images/authentication/integrations.png)

#### 選擇整合類型

下一個畫面會詢問您是要存取API或接收近乎即時的事件。 選擇 **存取API** ，然後 **繼續**。

![](images/authentication/create-new-integration.png)

#### 選擇要與

如果您的帳戶與多個IMS組織關聯，您可以使用右上角的下拉式選單，在它們之間切換。 在 **** Adobe Experience Platform **下選擇Workshop** and **** Experience Platform API，以存取API。

![](images/authentication/integration-select-service.png)

按一 **下** 「繼續」，移至下一節。

#### 新增整合詳細資訊、公開金鑰和產品設定檔

下一個畫面會提示您填寫整合詳細資訊、輸入公開金鑰憑證，並選取產品設定檔。

![](images/authentication/integration-details.png)

首先，輸入您的整合詳細資訊。 接著，選取產品設定檔。 產品設定檔會授予您對屬於您在先前步驟中選取之服務之功能群組的精細存取權。

對於證書部分，必須生成證書：

**對於MacOS和Linux平台：**

開啟命令行並執行以下命令：

`openssl req -x509 -sha256 -nodes -days 365 -newkey rsa:2048 -keyout private.key -out certificate_pub.crt`


**針對Windows平台：**

1. 下載openssl用戶端以產生公用憑證(例如 [Openssl windows用戶端](https://bintray.com/vszakats/generic/download_file?file_path=openssl-1.1.1-win64-mingw.zip))

1. 解壓該資料夾並將其複製到C:/libs/位置。

1. 開啟命令行提示並執行以下命令：

   `set OPENSSL_CONF=C:/libs/openssl-1.1.1-win64-mingw/openssl.cnf`

   `cd C:/libs/openssl-1.1.1-win64-mingw/`

   `openssl req -x509 -sha256 -nodes -days 365 -newkey rsa:2048 -keyout private.key -out certificate_pub.crt`

您會收到類似下列的回應，提示您輸入有關您自己的資訊：

```
Generating a 2048 bit RSA private key
.................+++
.......................................+++
writing new private key to 'private.key'
-----
You are about to be asked to enter information that will be incorporated
into your certificate request.
What you are about to enter is what is called a Distinguished Name or a DN.
There are quite a few fields but you can leave some blank
For some fields there will be a default value,
If you enter '.', the field will be left blank.
-----
Country Name (2 letter code) []:
State or Province Name (full name) []:
Locality Name (eg, city) []:
Organization Name (eg, company) []:
Organizational Unit Name (eg, section) []:
Common Name (eg, fully qualified host name) []:
Email Address []:
```

輸入資訊後，將生成兩個檔案： `certificate_pub.crt` 和 `private.key`。

>[!NOTE]
>`certificate_pub.crt` 將於365天後到期。 通過更改上述命令中的值，可以使 `days` 期間變 `openssl` 長，但定期旋轉憑據是一種很好的安全做法。

將在 `private.key` 後一節中用於生成我們的JWT。

用 `certificate_pub.crt` 於建立API密鑰。 返回Adobe I/O Console，然後按一下「 **選取檔案** 」上傳 `certificate_pub.crt` 檔案。

按一 **下「建立整合** 」以完成程式。

### 複製向下存取值

建立整合後，您可以檢視其詳細資訊。 按一 **下「擷取用戶端密碼** 」，您的螢幕看起來會類似下列：

![](images/authentication/access-values.png)

複製的值(即 `{API KEY}`組 `{IMS ORG}` 織ID) `{CLIENT SECRET}` ，如下一步中將使用這些值。

## 每個會話的驗證

最後一步是產生您的 `{ACCESS_TOKEN}` API呼叫，用來驗證您的API呼叫。 存取Token必須包含在您對Adobe Experience Platform進行之每個API呼叫的「授權」標題中。 存取Token會在24小時後到期，之後必須產生新Token，才能繼續使用API。

### 建立JWT

在Adobe I/O Console的整合詳細資訊頁面中，導覽至 **JWT** 標籤：

![](images/authentication/generate-jwt.png)

該頁提示您輸入在上 `private.key` 一節中建立的。 開啟命令行以查看檔案的內 `private.key` 容：

```shell
cat private.key
```

您的輸出會如下所示：

```shell
-----BEGIN PRIVATE KEY-----
MIIEvAIBADANBgkqhkiG9w0BAQEFAASCBKYwggSiAgEAAoIBAQCYjPj18NrVlmrc
H+YUTuwWrlHTiPfkBGM0P1HbIOdwrlSTCmPhmaNNG5+mEiULJLWlrhQpx/7uQVNW
......
xbWgBWatJ2hUhU5/K2iFlNJBVXyNy7rN0XzOagLRJ1uS2CM6Hn3vBOqLbHRG4Pen
J1LvEocGunT12UJekLdEaQR4AKodIyjv5opvewrzxUZhVvUIIgeU5vUpg9smCXai
wPW5MQjmygodzCh7+eGLrg==
-----END PRIVATE KEY-----
```

複製整個輸出並將其貼上到文本欄位中，然後按一下「生 **成JWT」**。 複製生成的JWT以執行下一步。

![](images/authentication/generated-jwt.png)

### 產生存取Token

您可以透過cURL命令產生存取Token。 如果您未安裝cURL，則可使用安裝 `npm install curl`。 您可以在這裡閱讀更多有關cURL的 [資訊](https://curl.haxx.se/)

在安裝cURL後，您需要將下列命令中的欄位交換為您自己的 `{API_KEY}`、 `{CLIENT_SECRET}`和 `{JWT_TOKEN}`:

```SHELL
curl -X POST "https://ims-na1.adobelogin.com/ims/exchange/jwt/" \
  -F "client_id={API_KEY}" \
  -F "client_secret={CLIENT_SECRET}" \
  -F "jwt_token={JWT_TOKEN}"
```

如果成功，輸出結果將如下所示：

```JSON
{
  "token_type":"bearer",
  "access_token":"eyJ4NXUiOiJpbXNfbmExLXN0ZzEta2V5LT2VyIiwiYWxnIjoiUlMyNTYifQ.eyJpZCI6IjE1MjAzMDU0ODY5MDhfYzMwM2JkODMtMWE1My00YmRiLThhNjctMWDhhNDJiNTE1X3VlMSIsImNsaWVudF9pZCI6ImYwNjY2Y2M4ZGVhNzQ1MWNiYzQ2ZmI2MTVkMzY1YzU0IiwidXNlcl9pZCI6IjA0ODUzMkMwNUE5ODg2QUQwQTQ5NDEzOUB0ZWNoYWNjdC5hZG9iZS5jb20iLCJzdGF0ZSI6IntcInNlc3Npb25cIjpcImh0dHBzOi8vaW1zLW5hMS1zdGcxLmFkb2JlbG9naW4uY29tL2ltcy9zZXNzaW9uL3YxL05UZzJZemM1TVdFdFlXWTNaUzAwT1RWaUxUZ3lPVFl0WkdWbU5EUTVOelprT0dFeUxTMHdORGcxTXpKRPVGc0TmtGRU1FRTBPVFF4TXpsQWRHVmphR0ZqWTNRdVlXUnZZbVV1WTI5dFwifSIsInR5cGUiOiJhY2Nlc3NfdG9rZW4iLCJhcyI6Imltcy1uYTEtc3RnMSIsImZnIjoiU0hRUlJUQ0ZTWFJJTjdSQjVVQ09NQ0lBWVU9PT09PT0iLCJtb2kiOiJhNTYwOWQ5ZiIsImMiOiJMeksySTBuZ2F2M1BhWWIxV0J3d3FRPT0iLCJleHBpcmVzX2luIjoiODY0MDAwMDAiLCJzY29wZSI6Im9wZW5pZCxzZXNzaW9uLEFkb2JlSUQscmVhZF9vcmdhbml6YXRpb25zLGFkZGl0aW9uYWxfaW5mby5wcm9qZWN0ZWRQcm9kdWN0Q29udGV4dCIsImNyZWF0ZWRfYXQiOiIxNTIwMzA1NDg2OTA4In0.EBgpw0JyKVzbjIBmH6fHDZUvJpvNG8xf8HUHNCK2l-dnVJqXxdi0seOk_kjVodkIa3evC54V560N60vi_mzt7gef-g954VH6l3gFh6XQ7yqRJD2LMW7G1lhQGhga4hrQCnJlfSQoztvIp9hkar9Zcu-MYgyEB5UlwK3KtB3elu7vJGk35F3T9OnqVL4PFj0Ix6zcuN_4gikgQgmtoUjuXULinbtu9Bkmdf7so9FvhapUd5ZTUTTMrAfJ36gEOQPqsuzlu9oUQaYTAn8v4B9TgoS0Paslo6WIksc4f_rSVWsbO6_TSUqIOi0e_RyL6GkMBA1ELA-Dkgbs-jUdkw",
  "expires_in":86399947
}
```

您的存取Token是金鑰下的 `access_token` 值。 此存取Token `expires_in` 8639947毫秒（24小時）。 之後，您必須依照上述相同步驟產生新的存取Token。

您現在已準備好在Adobe Experience Platform中提出API要求！

### 測試存取代碼

若要測試您的存取Token是否有效，您可以嘗試進行下列API呼叫。 此呼叫會列出容器內的所有 `global` 類別：

>[!NOTE]
>`{API_KEY}` 並 `{IMS_ORG}` 參考您上述產生的值。

**請求**

```SHELL
curl -X GET https://platform.adobe.io/data/foundation/schemaregistry/global/classes \
  -H 'Accept: application/vnd.adobe.xed-id+json' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}'
```


如果您的回覆與下列所示類似，則表示您的回覆 `access_token` 有效且有效。 （此回應已針對空格截斷。）

**回應**

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