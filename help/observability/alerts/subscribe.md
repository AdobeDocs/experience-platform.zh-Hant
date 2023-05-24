---
keywords: Experience Platform；首頁；熱門主題；日期範圍
title: 訂閱Adobe I/O事件通知
description: 本文檔提供了如何訂閱Adobe Experience Platform服務的Adobe I/O事件通知的步驟。 還提供了關於可用事件類型的參考資訊，以及指向關於如何解釋每個適用事件返回資料的進一步文檔的連結 [!DNL Platform] 服務。
feature: Alerts
exl-id: c0ad7217-ce84-47b0-abf6-76bcf280f026
source-git-commit: 0a4883cff4f8e04dd0dd62a9e01435fa302a9e54
workflow-type: tm+mt
source-wordcount: '771'
ht-degree: 1%

---

# 訂閱Adobe I/O事件通知

[!DNL Observability Insights] 允許您訂閱有關Adobe Experience Platform活動的Adobe I/O事件通知。 這些事件被發送到配置的webhook，以促進活動監控的高效自動化。

本文檔提供了如何訂閱Adobe Experience Platform服務的Adobe I/O事件通知的步驟。 還提供了關於可用事件類型的參考資訊，以及指向關於如何解釋每個適用事件返回資料的進一步文檔的連結 [!DNL Platform] 服務。

## 快速入門

本文檔要求瞭解Webhook以及如何將Webhook從一個應用程式連接到另一個應用程式。 請參閱 [[!DNL I/O Events] 文檔](https://www.adobe.io/apis/experienceplatform/events/docs.html#!adobedocs/adobeio-events/master/intro/webhook_docs_intro.md) 網鈎簡介。

## 建立網鈎

為了接收 [!DNL I/O Event] 通知，您必須通過指定唯一webhook URL作為事件註冊詳細資訊的一部分來註冊webhook。

可以使用您選擇的客戶端配置網路掛接。 要獲得用作本教程一部分的臨時Webhook地址，請訪問 [Webhook.site](https://webhook.site/) 並複製提供的唯一URL。

![](../images/notifications/webhook-url.png)

在初始驗證過程中， [!DNL I/O Events] 發送 `challenge` 向webhook請求GET中的查詢參數。 必須配置Webhook以在響應負載中返回此參數的值。 如果使用Webhook.site，請選擇 **[!DNL Edit]** 在右上角，然後輸入 `$request.query.challenge$` 在 **[!DNL Response body]** 選擇 **[!DNL Save]**。

![](../images/notifications/response-challenge.png)

## 在Adobe Developer控制台中建立新項目

轉到 [Adobe Developer控制台](https://www.adobe.com/go/devs_console_ui) 和你的Adobe ID登錄。 接下來，按照本教程中介紹的步驟操作 [建立空項目](https://developer.adobe.com/developer-console/docs/guides/projects/projects-empty/) 在Adobe Developer控制台文檔中。

## 訂閱事件

建立新項目後，導航到該項目的概述螢幕。 從此處，選擇 **[!UICONTROL 添加事件]**。

![](../images/notifications/add-event-button.png)

此時將顯示一個對話框，允許您向項目添加事件提供程式：

* 如果要訂閱Experience Platform警報，請選擇 **[!UICONTROL 平台通知]**
* 如果你訂閱Adobe Experience Platform [!DNL Privacy Service] 通知，選擇 **[!UICONTROL Privacy Service事件]**

選擇事件提供程式後，選擇 **[!UICONTROL 下一個]**。

![](../images/notifications/event-provider.png)

下一螢幕顯示要訂閱的事件類型清單。 選擇要訂閱的事件，然後選擇 **[!UICONTROL 下一個]**。

>[!NOTE]
>
>如果您不確定要訂閱您正在使用的服務的事件，請參閱以下文檔：
>
>* [平台通知](./rules.md)
>* [Privacy Service通知](../../privacy-service/privacy-events.md)


![](../images/notifications/choose-event-subscriptions.png)

下一個螢幕提示您建立JSON Web令牌(JWT)。 您可以選擇自動生成密鑰對，或上載在終端中生成的自己的公鑰。

在本教程中，將遵循第一個選項。 選擇 **[!UICONTROL 生成密鑰對]**，然後選擇 **[!UICONTROL 生成鍵對]** 按鈕。

![](../images/notifications/generate-keypair.png)

當密鑰對生成時，瀏覽器會自動下載該密鑰對。 您必須自己儲存此檔案，因為該檔案未保留在開發人員控制台中。

下一個螢幕允許您查看新生成的密鑰對的詳細資訊。 選取&#x200B;**[!UICONTROL 「下一步」]**&#x200B;以繼續。

![](../images/notifications/keypair-generated.png)

在下一螢幕中，為中的事件註冊提供名稱和說明 [!UICONTROL 事件註冊詳細資訊] 的子菜單。 最佳做法是建立一個唯一且易於識別的名稱，以幫助區分此事件註冊與同一項目上的其他項目。

![](../images/notifications/registration-details.png)

在同一螢幕下 [!UICONTROL 如何接收事件] 部分中，您可以選擇配置接收事件的方式。 **[!UICONTROL 網鈎]** 允許您提供自定義webhook地址以接收事件，而 **[!UICONTROL 運行時操作]** 允許您使用 [Adobe I/O Runtime](https://www.adobe.io/apis/experienceplatform/runtime/docs.html)。

對於本教程，請選擇 **[!UICONTROL 網鈎]** 並提供先前建立的webhook的URL。 完成後，選擇 **[!UICONTROL 保存已配置的事件]** 完成事件註冊。

![](../images/notifications/receive-events.png)

此時將顯示新建立的事件註冊的詳細資訊頁面，您可以在其中編輯其配置、查看接收的事件、執行調試跟蹤和添加新的事件提供程式。

![](../images/notifications/registration-complete.png)

## 後續步驟

按照本教程，您註冊了要接收 [!DNL I/O Event] 通知 [!DNL Experience Platform] 和/或 [!DNL Privacy Service]。 有關可用事件以及如何解釋每個服務的通知負載的詳細資訊，請參閱以下文檔：

* [[!DNL Privacy Service] 通知](../../privacy-service/privacy-events.md)
* [[!DNL Data Ingestion] 通知](../../ingestion/quality/subscribe-events.md)
* [[!DNL Flow Service] （源）通知](../../sources/notifications.md)

查看 [[!DNL Observability Insights] 概述](../home.md) 有關如何監視活動的詳細資訊，請參閱 [!DNL Experience Platform] 和 [!DNL Privacy Service]。
