---
description: 本頁介紹如何驗證和開始使用Adobe Experience Platform Destination SDK。 它包括有關如何獲取Adobe I/O身份驗證憑據、沙盒名稱和目標創作訪問控制權限的說明。
title: Destination SDK入門
exl-id: f22c37a8-202d-49ac-9af0-545dfa9af8fd
source-git-commit: 7c1d956e3b6a1314baa13fef823d73d42404516a
workflow-type: tm+mt
source-wordcount: '627'
ht-degree: 4%

---

# 快速入門

## 總覽 {#overview}

本頁介紹如何驗證和開始使用Adobe Experience Platform Destination SDK。 它包括有關如何獲取Adobe I/O身份驗證憑據、沙盒名稱和目標創作訪問控制權限的說明。

## 術語 {#terminology}

本指南使用特定於平台的概念，如組織和沙箱。 咨詢 [Experience Platform辭彙表](https://experienceleague.adobe.com/docs/experience-platform/landing/glossary.html) 定義。

## 獲取所需的身份驗證憑據 {#obtain-authentication-credentials}

Destination SDK使用 [Adobe I/O](https://www.adobe.io/) 用於驗證的網關。 要對Destination SDK終結點進行API調用，必須在API調用中提供某些標頭。 與AdobeExchange團隊協作，為您設定 [Adobe Developer控制台](https://developer.adobe.com/console)。

要成功調用Destination SDKAPI終結點，請遵循 [Experience Platform驗證教程](https://experienceleague.adobe.com/docs/experience-platform/landing/platform-apis/api-authentication.html)。 從「」開始教程[生成API密鑰、組織ID和客戶端密鑰](https://experienceleague.adobe.com/docs/experience-platform/landing/platform-apis/api-authentication.html#api-ims-secret)的子菜單。 AdobeExchange團隊將為您處理前面的步驟。 完成Destination SDK教程將提供API調用中每個必需標頭的值，如下所示：

* `x-api-key: {API_KEY}`，也稱為客戶端ID
* `x-gw-ims-org-id: {ORG_ID}`，也稱為組織ID
* `Authorization: Bearer {ACCESS_TOKEN}`。訪問令牌的過期時間為24小時，以毫秒為單位，因此您必須刷新它。 要刷新訪問令牌，請重複驗證教程中介紹的步驟。

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

## 目標所有權和沙箱 {#destination-ownership}

Experience Platform中的所有資源都與特定的虛擬沙箱隔離。 Destination SDK請求要求標頭指定操作所在沙盒的名稱：

* `x-sandbox-name: {SANDBOX_NAME}`

AdobeExchange團隊為您提供沙盒名稱，您需要在對Destination SDKAPI終結點的調用中使用沙盒名稱。

## 基於角色的訪問控制(RBAC) {#rbac}

使用中介紹的Destination SDKAPI終結點 [參考文檔](functionality/configuration-options.md)你需要 **[!UICONTROL 目標創作]** 訪問控制權限。 與AdobeExchange團隊合作，以在 [Adobe Admin Console](https://adminconsole.adobe.com/)。

![目標創作權限](./assets/destination-authoring-permission.png)

有關詳細資訊，請閱讀以下Experience Platform訪問控制文檔：

* [管理產品配置檔案的權限](/help/access-control/ui/permissions.md)
* [可用的Experience Platform權限](/help/access-control/home.md#permissions)
* [Adobe Admin Console文檔](https://helpx.adobe.com/tw/enterprise/using/admin-console.html)

## 其他考量事項 {#additional-considerations}

* 對於已生產化/公共目標，您對目標配置所做的任何更改（無論您是建立還是編輯目標配置）都需要由Adobe審查和批准。 您所做的更改只有在審閱完成後才會反映在您的目標中。 這不適用於僅對您可用的私有目標。
* 只有屬於同一組織並有權訪問沙盒的用戶才能編輯目標配置。

## 後續步驟 {#next-steps}

按照本文中的步驟，您獲得了Adobe I/O的身份驗證憑據、沙盒名稱和目標創作訪問控制權限。 接下來，您可以使用Destination SDK設定目標。

* 根據目標類型，閱讀以下配置指南：

   * [使用Destination SDK配置流目標](guides/configure-destination-instructions.md)
   * [使用Destination SDK配置基於檔案的目標](guides/configure-file-based-destination-instructions.md)

* 有關所有操作，請參閱 [目標創作API文檔](https://www.adobe.io/experience-platform-apis/references/destination-authoring/)。
* 使用 [目標創作APIPostman集合](https://github.com/adobe/experience-platform-postman-samples/blob/master/apis/experience-platform/Destination%20Authoring%20API.postman_collection.json) 使用Destination SDKAPI終結點配置目標。 要開始使用Postman，請參閱 [導入環境和集合的步驟](https://learning.postman.com/docs/getting-started/importing-and-exporting-data/) 和 [建立Postman環境的視頻指南](https://video.tv.adobe.com/v/28832)。
