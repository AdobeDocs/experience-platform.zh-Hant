---
description: 本頁面說明如何驗證及開始使用Adobe Experience Platform Destination SDK。 其中包含如何取得Adobe I/O驗證憑證、沙箱名稱及目的地編寫存取控制權限的指示。
title: 開始使用Destination SDK
exl-id: f22c37a8-202d-49ac-9af0-545dfa9af8fd
source-git-commit: 7c1d956e3b6a1314baa13fef823d73d42404516a
workflow-type: tm+mt
source-wordcount: '627'
ht-degree: 4%

---

# 快速入門

## 總覽 {#overview}

本頁面說明如何驗證及開始使用Adobe Experience Platform Destination SDK。 其中包含如何取得Adobe I/O驗證憑證、沙箱名稱及目的地編寫存取控制權限的指示。

## 術語 {#terminology}

本指南使用平台專屬概念，例如組織和沙箱。 請參閱 [Experience Platform字彙表](https://experienceleague.adobe.com/docs/experience-platform/landing/glossary.html) 和其他術語的定義。

## 獲取所需的身份驗證憑據 {#obtain-authentication-credentials}

Destination SDK使用 [Adobe I/O](https://www.adobe.io/) 驗證的網關。 若要對Destination SDK端點進行API呼叫，您必須在API呼叫中提供特定標題。 與AdobeExchange團隊合作，為您設定驗證 [Adobe Developer Console](https://developer.adobe.com/console).

若要成功呼叫Destination SDKAPI端點，請遵循 [Experience Platform驗證教學課程](https://experienceleague.adobe.com/docs/experience-platform/landing/platform-apis/api-authentication.html). 從「[產生API金鑰、組織ID和用戶端密碼](https://experienceleague.adobe.com/docs/experience-platform/landing/platform-apis/api-authentication.html#api-ims-secret)」步驟。 Adobe交換團隊將為您處理前述步驟。 完成驗證教學課程會提供Destination SDKAPI呼叫中每個必要標題的值，如下所示：

* `x-api-key: {API_KEY}`，也稱為用戶端ID
* `x-gw-ims-org-id: {ORG_ID}`，又稱為組織ID
* `Authorization: Bearer {ACCESS_TOKEN}`。存取權杖的到期時間為24小時（以毫秒為單位），因此您必須重新整理它。 若要重新整理存取權杖，請重複驗證教學課程中概述的步驟。

<!--

### Obtain `Authorization: Bearer {ACCESS_TOKEN}`

To obtain the `{ACCESS_TOKEN}`, you must generate a JWT token and exchange it for the access token. Follow the steps below:

1. Follow the instructions in the [Generate JWT section](https://www.adobe.io/apis/experienceplatform/console/docs.html#!AdobeDocs/adobeio-console/master/credentials.md) in the credentials guide.
2. Follow the instructions in [Step 3: try it](https://www.adobe.io/authentication/auth-methods.html#!AdobeDocs/adobeio-auth/master/AuthenticationOverview/ServiceAccountIntegration.md) in the Service account connection guide.

You now have the required authentication headers `x-api-key: {API_KEY}`, `x-gw-ims-org-id: {ORG_ID}`, and `Authorization: Bearer {ACCESS_TOKEN}`.

>[!NOTE]
>
>The access token has an expiration time of 24 hours, expressed in milliseconds, so you will have to refresh it. To refresh the access token, repeat the steps outlined in this section.

-->

## 目的地所有權和沙箱 {#destination-ownership}

Experience Platform中的所有資源都會隔離至特定的虛擬沙箱。 Destination SDK請求需要標頭，以指定操作進行的沙箱名稱：

* `x-sandbox-name: {SANDBOX_NAME}`

AdobeExchange團隊會提供您的沙箱名稱，您必須在呼叫Destination SDKAPI端點時使用該名稱。

## 基於角色的訪問控制(RBAC) {#rbac}

若要使用Destination SDKAPI端點，請參閱 [參考檔案](functionality/configuration-options.md)，您需要 **[!UICONTROL 目標編寫]** 存取控制權限。 與AdobeExchange團隊合作，在 [Adobe Admin Console](https://adminconsole.adobe.com/).

![目標編寫權限](./assets/destination-authoring-permission.png)

如需詳細資訊，請閱讀下列Experience Platform存取控制檔案：

* [管理產品設定檔的權限](/help/access-control/ui/permissions.md)
* [可用的Experience Platform](/help/access-control/home.md#permissions)
* [Adobe Admin Console檔案](https://helpx.adobe.com/tw/enterprise/using/admin-console.html)

## 其他考量事項 {#additional-considerations}

* 對於已產品化/公用目的地，您對目的地設定所做的任何變更（無論您是建立還是編輯目的地設定）都需由Adobe審核和核准。 您的變更只有在審核完成後才會反映在您的目的地中。 這不適用於僅供您使用的私人目的地。
* 只有屬於相同組織且可存取沙箱的使用者才能編輯目的地設定。

## 後續步驟 {#next-steps}

依照本文所述步驟操作，您可取得Adobe I/O的驗證憑證、沙箱名稱，以及目的地編寫存取控制權限。 接下來，您可以使用Destination SDK來設定目的地。

* 視您的目的地類型而定，請閱讀下列設定指南：

   * [使用Destination SDK來設定串流目的地](guides/configure-destination-instructions.md)
   * [使用Destination SDK配置基於檔案的目標](guides/configure-file-based-destination-instructions.md)

* 對於所有操作，請參閱 [Destination Authoring API檔案](https://www.adobe.io/experience-platform-apis/references/destination-authoring/).
* 使用 [Destination Authoring API Postman集合](https://github.com/adobe/experience-platform-postman-samples/blob/master/apis/experience-platform/Destination%20Authoring%20API.postman_collection.json) 使用Destination SDKAPI端點來設定您的目的地。 若要開始使用Postman，請參閱 [匯入環境和集合的步驟](https://learning.postman.com/docs/getting-started/importing-and-exporting-data/) 和 [建立Postman環境的影片指南](https://video.tv.adobe.com/v/28832).
