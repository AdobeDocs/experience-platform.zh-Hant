---
description: 本頁說明如何驗證及開始使用Adobe Experience Platform Destination SDK。 其中包含如何取得Adobe I/O驗證憑證、沙箱名稱及目的地編寫存取控制權限的指示。
title: 目標SDK快速入門
source-git-commit: 19307fba8f722babe5b6d57e80735ffde00fc851
workflow-type: tm+mt
source-wordcount: '525'
ht-degree: 2%

---

# 快速入門

## 概覽 {#overview}

本頁說明如何驗證及開始使用Adobe Experience Platform Destination SDK。 其中包含如何取得Adobe I/O驗證憑證、沙箱名稱及目的地編寫存取控制權限的指示。

## 術語 {#terminology}

本指南使用平台專屬的概念，例如IMS組織和沙箱。 請參閱[Experience Platform字彙表](https://experienceleague.adobe.com/docs/experience-platform/landing/glossary.html)以了解這些字詞和其他字詞的定義。

## 獲取所需的身份驗證憑據 {#obtain-authentication-credentials}

目標SDK使用[Adobe I/O](https://www.adobe.io/)閘道進行驗證。 若要對目的地SDK端點進行API呼叫，您必須在API呼叫中提供特定標題。 與AdobeExchange團隊合作，為您設定[Adobe開發人員控制台](http://console.adobe.io/)的驗證。

若要成功呼叫目標SDK API端點，請遵循[Experience Platform驗證教學課程](https://experienceleague.adobe.com/docs/experience-platform/landing/platform-apis/api-authentication.html)。 從「[產生API金鑰、IMS組織ID和用戶端密碼](https://experienceleague.adobe.com/docs/experience-platform/landing/platform-apis/api-authentication.html#api-ims-secret)」步驟開始教學課程。 Adobe交換團隊將為您處理前述步驟。 完成驗證教學課程，可提供目標SDK API呼叫中每個必要標題的值，如下所示：

* `x-api-key: {API_KEY}`，也稱為用戶端ID
* `x-gw-ims-org-id: {IMS_ORG}`，又稱為組織ID
* `Authorization: Bearer {ACCESS_TOKEN}`。存取權杖的到期時間為24小時（以毫秒為單位），因此您必須重新整理它。 若要重新整理存取權杖，請重複驗證教學課程中概述的步驟。

<!--

### Obtain `Authorization: Bearer {ACCESS_TOKEN}`

To obtain the `{ACCESS_TOKEN}`, you must generate a JWT token and exchange it for the access token. Follow the steps below:

1. Follow the instructions in the [Generate JWT section](https://www.adobe.io/apis/experienceplatform/console/docs.html#!AdobeDocs/adobeio-console/master/credentials.md) in the credentials guide.
2. Follow the instructions in [Step 3: try it](https://www.adobe.io/authentication/auth-methods.html#!AdobeDocs/adobeio-auth/master/AuthenticationOverview/ServiceAccountIntegration.md) in the Service account connection guide.

You now have the required authentication headers `x-api-key: {API_KEY}`, `x-gw-ims-org-id: {IMS_ORG}`, and `Authorization: Bearer {ACCESS_TOKEN}`.

>[!NOTE]
>
>The access token has an expiration time of 24 hours, expressed in milliseconds, so you will have to refresh it. To refresh the access token, repeat the steps outlined in this section.

-->

## 目的地所有權和沙箱 {#destination-ownership}

Experience Platform中的所有資源都會隔離至特定的虛擬沙箱。 要求目標SDK時，必須要有標頭來指定操作進行之沙箱的名稱：

* `x-sandbox-name: {SANDBOX_NAME}`

AdobeExchange團隊會提供您的沙箱名稱，您必須在呼叫目標SDK API端點時使用該名稱。

## 基於角色的訪問控制(RBAC) {#rbac}

若要使用[參考檔案](./configuration-options.md)中所述的目標SDK API端點，您需要&#x200B;**[!UICONTROL 目標編寫]**&#x200B;存取控制權限。 與AdobeExchange團隊合作，在[Adobe Admin Console](https://adminconsole.adobe.com/)中取得指派給您的此權限。

![目標編寫權限](./assets/destination-authoring-permission.png)

如需詳細資訊，請閱讀下列Experience Platform存取控制檔案：

* [管理產品設定檔的權限](/help/access-control/ui/permissions.md)
* [可用的Experience Platform](/help/access-control/home.md#permissions)
* [Adobe Admin Console檔案](https://helpx.adobe.com/tw/enterprise/using/admin-console.html)

## 其他考量 {#additional-considerations}

* 您對目標設定所做的任何變更（無論您是建立還是編輯目標設定）都需由Adobe審核和核准。 您的變更只有在審核完成後才會反映在您的目的地中。
* 只有屬於相同組織且可存取沙箱的使用者才能編輯目的地設定。

## 後續步驟 {#next-steps}

依照本文所述步驟操作，您可取得Adobe I/O的驗證憑證、沙箱名稱，以及目的地編寫存取控制權限。 接下來，您可以使用目的地SDK來設定目的地。 請參閱[使用目標SDK來設定後續步驟的目標](./configure-destination-instructions.md) 。
