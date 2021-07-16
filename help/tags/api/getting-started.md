---
title: Reactor API快速入門
description: 了解如何開始使用Reactor API，包括產生必要存取憑證的步驟。
source-git-commit: 6a1728bd995137a7cd6dc79313762ae6e665d416
workflow-type: tm+mt
source-wordcount: '1070'
ht-degree: 1%

---

# Reactor API快速入門

若要使用[Reactor API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/reactor.yaml)，每個要求都必須包含下列驗證標題：

* `Authorization: Bearer {ACCESS_TOKEN}`
* `x-api-key: {API_KEY}`
* `x-gw-ims-org-id: {IMS_ORG}`

本指南說明如何使用Adobe開發人員控制台來收集這些標題的值，以便您開始呼叫Reactor API。

## 取得開發人員存取Adobe Experience Platform

您必須擁有開發人員存取Experience Platform的權限，才能產生Reactor API的驗證值。 若要取得開發人員存取權，請依照[Experience Platform驗證教學課程](http://www.adobe.com/go/platform-api-authentication-en)中的開始步驟操作。 進入「在Adobe開發人員控制台中產生存取認證」步驟後，請返回本教學課程，產生Reactor API專用的認證。

## 生成訪問憑據

使用Adobe開發人員控制台，您必須產生下列三個存取憑證：

* `{IMS_ORG}`
* `{API_KEY}`
* `{ACCESS_TOKEN}`

您的IMS組織ID(`{IMS_ORG}`)和API金鑰(`{API_KEY}`)可在初次產生後，於未來的API呼叫中重複使用。 不過，您的存取權杖(`{ACCESS_TOKEN}`)是暫時的，必須每24小時重新產生一次。

以下詳細說明產生這些值的步驟。

### 一次性設定

前往[Adobe開發人員控制台](https://www.adobe.com/go/devs_console_ui)並使用您的Adobe ID登入。 接下來，請依照開發人員控制台檔案中[建立空白專案](https://www.adobe.io/apis/experienceplatform/console/docs.html#!AdobeDocs/adobeio-console/master/projects-empty.md)教學課程中概述的步驟操作。

建立專案後，在&#x200B;**專案概述**&#x200B;畫面上選取&#x200B;**新增API**。

![](../images/api/getting-started/add-api-button.png)

出現「**新增API**」畫面。 在選擇&#x200B;**Next**&#x200B;之前，從可用API清單中選擇&#x200B;**Experience PlatformReactor API**。

![](../images/api/getting-started/add-launch-api.png)

在下一個畫面中，系統會提示您建立JSON Web Token(JWT)憑證，以產生新的鑰匙組或上傳您自己的公開金鑰。 在本教學課程中，選擇&#x200B;**生成鍵對**&#x200B;選項，然後在右下角選擇&#x200B;**生成鍵對**。

![](../images/api/getting-started/create-jwt.png)

下一個畫面會確認金鑰組已成功產生，而包含公開憑證和私密金鑰的壓縮資料夾會自動下載至您的電腦。 在後續步驟中需要此私密金鑰，才能產生存取權杖。

選擇&#x200B;**Next**&#x200B;以繼續。

![](../images/api/getting-started/keypair-generated.png)

下一個畫面會提示您選取一或多個產品設定檔，以與API整合建立關聯。

>[!NOTE]
>
>產品設定檔由貴組織透過Adobe Admin Console管理，並包含Adobe Experience Platform Launch中精細功能的特定權限集。 產品設定檔及其權限只能由組織內具有管理員權限的使用者管理。 如果您不確定要為API選取哪些產品設定檔，請聯絡管理員。

從清單中選取所需的產品設定檔，然後選取&#x200B;**儲存已設定的API**&#x200B;以完成API註冊。

![](../images/api/getting-started/select-product-profile.png)

將API新增至專案後，專案頁面會重新顯示在「Experience Platform反應器API」頁面上。 從此處，向下捲動至&#x200B;**服務帳戶(JWT)**&#x200B;區段，該區段提供所有對Reactor API的呼叫所需的下列存取憑證：

* **用戶端ID**:必須在標題中 `{API_KEY}` 提供用戶端 `x-api-key` ID。
* **組織ID**:組織ID是必 `{IMS_ORG}` 須用於標題的 `x-gw-ims-org-id` 值。

![](../images/api/getting-started/access-creds.png)

### 每個會話的驗證

現在您已有`{API_KEY}`和`{IMS_ORG}`值，最後一步就是產生`{ACCESS_TOKEN}`值。

>[!NOTE]
>
>這些代號會在24小時後過期。 如果您將此整合用於應用程式，最好以程式設計方式從應用程式內取得您的載體代號。

您有兩個選項可產生存取權杖，視您的使用案例而定：

* [手動產生代號](#manual)
* [以程式設計方式產生代號](#program)

#### 手動產生存取權杖 {#manual}

開啟先前在文字編輯器或瀏覽器中下載的私密金鑰，並複製其內容。 接著，導覽回開發人員控制台，並在選取&#x200B;**產生代號**&#x200B;前，將私密金鑰貼到專案「Reactor API」頁面的&#x200B;**產生存取代號**&#x200B;區段中。

![](../images/api/getting-started/paste-private-key.png)

系統會產生新的存取權杖，並提供將權杖複製到剪貼簿的按鈕。 此值用於所需的`Authorization`標頭，且必須以`Bearer {ACCESS_TOKEN}`格式提供。

![](../images/api/getting-started/token-generated.png)

#### 以程式設計方式產生存取權杖 {#program}

如果您將Launch整合用於應用程式，可以利用程式設計方式透過API請求產生存取權杖。 若要完成此操作，您必須取得下列值：

* 用戶端ID(`{API_KEY}`)
* 用戶端密碼(`{SECRET}`)
* JSON Web令牌(`{JWT}`)

您可從專案的主要頁面取得用戶端ID和機密，如上一步[所示。](#one-time-setup)

![](../images/api/getting-started/auto-access-creds.png)

若要取得JWT憑證，請導覽至左側導覽中的&#x200B;**服務帳戶(JWT)**，然後選取&#x200B;**產生JWT**&#x200B;標籤。 在此頁的&#x200B;**Generate custom JWT**&#x200B;下，將私密金鑰的內容貼到提供的文本框，然後選擇&#x200B;**Generate Token**。

![](../images/api/getting-started/generate-jwt.png)

產生的JWT在處理完成後會顯示在下方，並附上範例cURL命令，您可以視需要用來測試代號。 使用&#x200B;**複製**&#x200B;按鈕將代號複製到剪貼簿。

![](../images/api/getting-started/jwt-generated.png)

收集憑證後，您就可以將下方的API呼叫整合至您的應用程式，以程式設計方式產生存取權杖。

**要求**

請求必須傳送`multipart/form-data`裝載，並提供您的驗證憑證，如下所示：

```shell
curl -X POST \
  https://ims-na1.adobelogin.com/ims/exchange/jwt/ \
  -H 'Content-Type: multipart/form-data' \
  -F 'client_id={API_KEY}' \
  -F 'client_secret={SECRET}' \
  -F 'jwt_token={JWT}'
```

**回應**

成功的回應會傳回新的存取權杖，以及在其過期前剩餘的秒數。

```json
{
  "token_type": "bearer",
  "access_token": "{ACCESS_TOKEN}",
  "expires_in": 86399999
}
```

| 屬性 | 說明 |
| :-- | :-- |
| `access_token` | 新產生的存取權杖值。 此值用於所需的`Authorization`標頭，且必須以`Bearer {ACCESS_TOKEN}`格式提供。 |
| `expires_in` | 代號過期的剩餘時間（以毫秒為單位）。 代號過期後，必須產生新的代號。 |

{style=&quot;table-layout:auto&quot;}

## 後續步驟

依照本教學課程中的步驟，您應該會有`{IMS_ORG}`、`{API_KEY}`和`{ACCESS_TOKEN}`的有效值。 您現在可以在對Reactor API發出的簡單cURL要求中使用這些值，以測試這些值。

首先，嘗試對[列出所有公司](./endpoints/companies.md#list)進行API呼叫。

>[!NOTE]
>
>貴組織中可能沒有任何公司，在此情況下，回應將是HTTP狀態404（找不到）。 只要您未收到403（禁止）錯誤，您的存取憑證即有效且有效。

確認您的存取憑證正常運作後，請繼續探索其他API參考檔案，以了解API的許多功能。

## 其他資源

JWT程式庫和SDK:[https://jwt.io/](https://jwt.io/)

郵遞區號API開發：[https://www.postman.com/](https://www.postman.com/)
