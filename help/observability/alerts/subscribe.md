---
keywords: Experience Platform；首頁；熱門主題；日期範圍
title: 訂閱Adobe I/O事件通知
description: 本檔案提供如何訂閱Adobe Experience Platform服務Adobe I/O事件通知的步驟。 也提供關於可用事件類型的參考資訊，以及如何解釋每個適用事件傳回資料的進一步檔案連結 [!DNL Platform] 服務。
feature: Alerts
exl-id: c0ad7217-ce84-47b0-abf6-76bcf280f026
source-git-commit: 0a4883cff4f8e04dd0dd62a9e01435fa302a9e54
workflow-type: tm+mt
source-wordcount: '771'
ht-degree: 1%

---

# 訂閱Adobe I/O事件通知

[!DNL Observability Insights] 可讓您訂閱與Adobe Experience Platform活動相關的Adobe I/O事件通知。 這些事件會傳送至已設定的WebHook，以促進活動監控的有效自動化。

本檔案提供如何訂閱Adobe Experience Platform服務Adobe I/O事件通知的步驟。 也提供關於可用事件類型的參考資訊，以及如何解釋每個適用事件傳回資料的進一步檔案連結 [!DNL Platform] 服務。

## 快速入門

本檔案需要有效了解Webhook，以及如何將Webhook從一個應用程式連接到另一個應用程式。 請參閱 [[!DNL I/O Events] 檔案](https://www.adobe.io/apis/experienceplatform/events/docs.html#!adobedocs/adobeio-events/master/intro/webhook_docs_intro.md) 了解webhook的簡介。

## 建立網頁連結

為了接收 [!DNL I/O Event] 通知，您必須在事件註冊詳細資訊中指定唯一的webhook URL，以註冊webhook。

您可以使用所選用的用戶端來設定網頁連結。 若要取得在本教學課程中使用的暫時Webhook位址，請造訪 [Webhook.site](https://webhook.site/) 並複製提供的唯一URL。

![](../images/notifications/webhook-url.png)

在初始驗證程式中， [!DNL I/O Events] 傳送 `challenge` 向webhook發出GET請求中的查詢參數。 您必須設定Webhook，以在回應裝載中傳回此參數的值。 如果您使用Webhook.site，請選取 **[!DNL Edit]** 在右上角，然後輸入 `$request.query.challenge$` 在 **[!DNL Response body]** 選擇 **[!DNL Save]**.

![](../images/notifications/response-challenge.png)

## 在Adobe Developer Console中建立新專案

前往 [Adobe Developer Console](https://www.adobe.com/go/devs_console_ui) 並登入您的Adobe ID。 接下來，請依照 [建立空白專案](https://developer.adobe.com/developer-console/docs/guides/projects/projects-empty/) 在Adobe Developer Console檔案中。

## 訂閱事件

建立新專案後，請導覽至該專案的「概觀」畫面。 從此處，選擇 **[!UICONTROL 新增事件]**.

![](../images/notifications/add-event-button.png)

隨即出現對話方塊，可讓您將事件提供者新增至專案：

* 如果您訂閱Experience Platform警報，請選取 **[!UICONTROL 平台通知]**
* 如果您訂閱Adobe Experience Platform [!DNL Privacy Service] 通知，請選取 **[!UICONTROL Privacy Service事件]**

選擇事件提供程式後，請選擇 **[!UICONTROL 下一個]**.

![](../images/notifications/event-provider.png)

下一個畫面會顯示要訂閱的事件類型清單。 選取您要訂閱的事件，然後選取 **[!UICONTROL 下一個]**.

>[!NOTE]
>
>如果您不確定要訂閱目前使用之服務的事件，請參閱下列檔案：
>
>* [平台通知](./rules.md)
>* [Privacy Service通知](../../privacy-service/privacy-events.md)


![](../images/notifications/choose-event-subscriptions.png)

下一個畫面會提示您建立JSON Web Token(JWT)。 您可以選擇自動產生金鑰組，或上傳在終端機中產生的您自己的公開金鑰。

在本教學課程中，會遵循第一個選項。 選取 **[!UICONTROL 產生金鑰組]**，然後選取 **[!UICONTROL 產生鍵對]** 按鈕。

![](../images/notifications/generate-keypair.png)

當金鑰組產生時，瀏覽器會自動下載。 您必須自行儲存此檔案，因為此檔案不會保存在開發人員控制台中。

下一個畫面可讓您檢閱新產生的金鑰組詳細資訊。 選取&#x200B;**[!UICONTROL 「下一步」]**&#x200B;以繼續。

![](../images/notifications/keypair-generated.png)

在下一個畫面中，提供中事件註冊的名稱和說明 [!UICONTROL 事件註冊詳細資訊] 區段。 最佳實務是建立獨特且可輕鬆識別的名稱，以便區分此事件註冊與相同專案中的其他活動。

![](../images/notifications/registration-details.png)

在同一螢幕的下方， [!UICONTROL 如何接收事件] 區段中，您可以選擇設定接收事件的方式。 **[!UICONTROL Webhook]** 可讓您提供自訂的網頁連結位址以接收事件，但 **[!UICONTROL 執行階段動作]** 可讓您使用 [Adobe I/O Runtime](https://www.adobe.io/apis/experienceplatform/runtime/docs.html).

在本教學課程中，請選取 **[!UICONTROL Webhook]** 並提供您先前建立之網頁連結的URL。 完成後，請選取 **[!UICONTROL 儲存已設定的事件]** 完成事件註冊。

![](../images/notifications/receive-events.png)

新建立事件註冊的詳細資訊頁面隨即顯示，您可以在其中編輯其配置、查看接收的事件、執行調試跟蹤以及添加新的事件提供程式。

![](../images/notifications/registration-complete.png)

## 後續步驟

依照本教學課程，您已註冊網頁掛接以接收 [!DNL I/O Event] 通知 [!DNL Experience Platform] 和/或 [!DNL Privacy Service]. 如需可用事件的詳細資訊以及如何解讀每項服務的通知裝載，請參閱下列檔案：

* [[!DNL Privacy Service] 通知](../../privacy-service/privacy-events.md)
* [[!DNL Data Ingestion] 通知](../../ingestion/quality/subscribe-events.md)
* [[!DNL Flow Service] （來源）通知](../../sources/notifications.md)

請參閱 [[!DNL Observability Insights] 概述](../home.md) 以取得如何監視活動的詳細資訊，請參閱 [!DNL Experience Platform] 和 [!DNL Privacy Service].
