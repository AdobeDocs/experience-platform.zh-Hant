---
description: 本頁面說明如何驗證及開始使用Adobe Experience Platform Destination SDK。 其中包括如何取得Adobe I/O驗證認證、沙箱名稱和目的地編寫存取控制許可權的指示。
title: Destination SDK快速入門
exl-id: f22c37a8-202d-49ac-9af0-545dfa9af8fd
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '594'
ht-degree: 1%

---

# 快速入門

## 概觀 {#overview}

本頁面說明如何驗證及開始使用Adobe Experience Platform Destination SDK。 其中包括如何取得Adobe I/O驗證認證、沙箱名稱和目的地編寫存取控制許可權的指示。

## 術語 {#terminology}

本指南使用Experience Platform專屬的概念，例如組織和沙箱。 請參閱[Experience Platform字彙表](https://experienceleague.adobe.com/docs/experience-platform/landing/glossary.html)，瞭解這些字詞的定義。 請參閱[Destination SDK字彙表](/help/destinations/destination-sdk/glossary.md)，以取得與此功能直接相關的辭彙。

## 取得必要的驗證認證 {#obtain-authentication-credentials}

Destination SDK使用[Adobe I/O](https://www.adobe.io/)閘道進行驗證。 若要對Destination SDK端點進行API呼叫，您必須在API呼叫中提供某些標題。 與Adobe Exchange團隊合作，為您設定[Adobe Developer Console](https://developer.adobe.com/console)的驗證。

若要成功呼叫Destination SDK API端點，請依照[Experience Platform驗證教學課程](https://experienceleague.adobe.com/docs/experience-platform/landing/platform-apis/api-authentication.html?lang=zh-Hant)操作。 從[產生API金鑰、組織ID和使用者端密碼](https://experienceleague.adobe.com/docs/experience-platform/landing/platform-apis/api-authentication.html#api-ims-secret)步驟開始教學課程。 Adobe Exchange團隊將為您處理先前的步驟。 完成驗證教學課程，提供Destination SDK API呼叫中每個必要標題的值，如下所示：

* `x-api-key: {API_KEY}`，也稱為使用者端識別碼
* `x-gw-ims-org-id: {ORG_ID}`，也稱為組織識別碼
* `Authorization: Bearer {ACCESS_TOKEN}`。存取權杖的到期時間為24小時（以毫秒為單位），因此您必須重新整理。 若要重新整理存取Token，請重複驗證教學課程中概述的步驟。

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

## 目的地擁有權和沙箱 {#destination-ownership}

Experience Platform中的所有資源都會隔離至特定的虛擬沙箱。 向Destination SDK發出的請求需要標頭，以指定進行作業的沙箱名稱：

* `x-sandbox-name: {SANDBOX_NAME}`

Adobe Exchange團隊會提供您沙箱名稱，您必須在呼叫Destination SDK API端點時使用它。

## 角色型存取控制(RBAC) {#rbac}

若要使用[參考檔案](functionality/configuration-options.md)中說明的Destination SDK API端點，您需要&#x200B;**[!UICONTROL 目的地製作]**&#x200B;存取控制許可權。 與Adobe Exchange團隊合作，在[Adobe Admin Console](https://adminconsole.adobe.com/)中將此許可權指派給您。

![目的地編寫許可權](./assets/destination-authoring-permission.png)

如需詳細資訊，請閱讀下列Experience Platform存取控制檔案：

* [管理產品設定檔的許可權](/help/access-control/ui/permissions.md)
* [Experience Platform的可用許可權](/help/access-control/home.md#permissions)
* [Adobe Admin Console檔案](https://helpx.adobe.com/tw/enterprise/using/admin-console.html)

## 其他考量事項 {#additional-considerations}

* 針對產品化/公用目的地，無論您對目的地設定進行的任何變更（建立或編輯目的地設定）都需經過Adobe的檢閱和核准。 您的變更只有在檢閱完成後才會反映在您的目的地。 這不適用於只有您才能使用的私人目的地。
* 只有屬於相同組織且具有沙箱存取許可權的使用者才能編輯目的地設定。

## 後續步驟 {#next-steps}

依照本文的步驟操作，您已取得Adobe I/O的驗證認證、沙箱名稱和目的地編寫存取控制許可權。 接下來，您可以使用Destination SDK設定目的地。

* 根據您的目的地型別，閱讀下列設定指南：

   * [使用Destination SDK設定串流目的地](guides/configure-destination-instructions.md)
   * [使用Destination SDK設定以檔案為基礎的目的地](guides/configure-file-based-destination-instructions.md)

* 如需所有作業，請參閱[Destination Authoring API檔案](https://www.adobe.io/experience-platform-apis/references/destination-authoring/)。
* 使用[Destination Authoring API Postman集合](https://github.com/adobe/experience-platform-postman-samples/blob/master/apis/experience-platform/Destination%20Authoring%20API.postman_collection.json)，使用Destination SDK API端點設定您的目的地。 若要開始使用Postman，請參閱[匯入環境和集合的步驟](https://learning.postman.com/docs/getting-started/importing-and-exporting-data/)以及建立Postman環境的[影片指南](https://video.tv.adobe.com/v/28832)。
