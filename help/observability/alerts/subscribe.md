---
keywords: Experience Platform；首頁；熱門主題；日期範圍
title: 訂閱Adobe I/O事件通知
description: 本檔案提供如何訂閱Adobe Experience Platform服務Adobe I/O事件通知的步驟。 也提供了關於可用事件類型的參考資訊，以及指向如何解釋每個適用 [!DNL Platform] 服務的返回事件資料的進一步文檔的連結。
exl-id: c0ad7217-ce84-47b0-abf6-76bcf280f026
source-git-commit: 8c00fb98a213b578f6970c1e1978f0159f8f38df
workflow-type: tm+mt
source-wordcount: '773'
ht-degree: 1%

---

# 訂閱Adobe I/O事件通知

[!DNL Observability Insights] 可讓您訂閱與Adobe Experience Platform活動相關的Adobe I/O事件通知。這些事件會傳送至已設定的WebHook，以促進活動監控的有效自動化。

本檔案提供如何訂閱Adobe Experience Platform服務Adobe I/O事件通知的步驟。 還提供了有關可用事件類型的參考資訊，以及指向如何解釋每個適用[!DNL Platform]服務的返回事件資料的進一步文檔的連結。

## 快速入門

本檔案需要有效了解Webhook，以及如何將Webhook從一個應用程式連接到另一個應用程式。 如需Webhook的簡介，請參閱[[!DNL I/O Events] 檔案](https://www.adobe.io/apis/experienceplatform/events/docs.html#!adobedocs/adobeio-events/master/intro/webhook_docs_intro.md)。

## 建立網頁連結

要接收[!DNL I/O Event]通知，您必須通過指定唯一的Webhook URL作為事件註冊詳細資訊的一部分來註冊Webhook。

您可以使用所選用的用戶端來設定網頁連結。 若要在本教學課程中使用暫時的Webhook位址，請造訪[Webhook.site](https://webhook.site/)並複製提供的唯一URL。

![](../images/notifications/webhook-url.png)

在初始驗證過程中， [!DNL I/O Events]將GET請求中的`challenge`查詢參數發送到Webhook。 您必須設定Webhook，以在回應裝載中傳回此參數的值。 如果您使用Webhook.site，請在右上角選取&#x200B;**[!DNL Edit]**，然後在&#x200B;**[!DNL Response body]**&#x200B;下輸入`$request.query.challenge$`，再選取&#x200B;**[!DNL Save]**。

![](../images/notifications/response-challenge.png)

## 在Adobe開發人員控制台中建立新專案

前往[Adobe開發人員控制台](https://www.adobe.com/go/devs_console_ui)並使用您的Adobe ID登入。 接下來，請依照「Adobe開發人員控制台」檔案中[建立空白專案](https://www.adobe.io/apis/experienceplatform/console/docs.html#!AdobeDocs/adobeio-console/master/projects-empty.md)教學課程中概述的步驟操作。

## 訂閱事件

建立新專案後，請導覽至該專案的「概觀」畫面。 從此處，選擇&#x200B;**[!UICONTROL 添加事件]**。

![](../images/notifications/add-event-button.png)

隨即出現對話方塊，可讓您將事件提供者新增至專案：

* 如果您訂閱Experience Platform警報，請選擇&#x200B;**[!UICONTROL 平台通知]**
* 如果您訂閱Adobe Experience Platform [!DNL Privacy Service]通知，請選取&#x200B;**[!UICONTROL Privacy Service事件]**

選擇事件提供程式後，請選擇&#x200B;**[!UICONTROL Next]**。

![](../images/notifications/event-provider.png)

下一個畫面會顯示要訂閱的事件類型清單。 選擇要訂閱的事件，然後選擇&#x200B;**[!UICONTROL Next]**。

>[!NOTE]
>
>如果您不確定要訂閱您正在使用之服務的事件，請參閱服務專屬通知檔案：
>
>* [[!DNL Privacy Service] 通知](../../privacy-service/privacy-events.md)
* [[!DNL Data Ingestion] 通知](../../ingestion/quality/subscribe-events.md)
* [[!DNL Flow Service (sources)] 通知](../../sources/notifications.md)


![](../images/notifications/choose-event-subscriptions.png)

下一個畫面會提示您建立JSON Web Token(JWT)。 您可以選擇自動產生金鑰組，或上傳在終端機中產生的您自己的公開金鑰。

在本教學課程中，會遵循第一個選項。 選擇&#x200B;**[!UICONTROL 生成鍵對]**&#x200B;的選項框，然後在右下角選擇&#x200B;**[!UICONTROL 生成鍵對]**&#x200B;按鈕。

![](../images/notifications/generate-keypair.png)

當金鑰組產生時，瀏覽器會自動下載。 您必須自行儲存此檔案，因為此檔案不會保存在開發人員控制台中。

下一個畫面可讓您檢閱新產生的金鑰組詳細資訊。 選擇&#x200B;**[!UICONTROL Next]**&#x200B;以繼續。

![](../images/notifications/keypair-generated.png)

在下一個螢幕中，在[!UICONTROL 事件註冊詳細資訊]部分中提供事件註冊的名稱和說明。 最佳實務是建立獨特且可輕鬆識別的名稱，以便區分此事件註冊與相同專案中的其他活動。

![](../images/notifications/registration-details.png)

在[!UICONTROL 如何接收事件]區段下方的相同畫面中，您可以選擇設定如何接收事件。 **** Webhook可讓您提供自訂的Webhook位址以接收事件，而 **[!UICONTROL 執行]** 階段動作則可讓您使用Adobe I/O Runtime [執行相同操作](https://www.adobe.io/apis/experienceplatform/runtime/docs.html)。

在本教學課程中，選取&#x200B;**[!UICONTROL Webhook]**&#x200B;並提供您先前建立之Webhook的URL。 完成後，選擇&#x200B;**[!UICONTROL 保存配置的事件]**&#x200B;以完成事件註冊。

![](../images/notifications/receive-events.png)

新建立事件註冊的詳細資訊頁面隨即顯示，您可以在其中編輯其配置、查看接收的事件、執行調試跟蹤以及添加新的事件提供程式。

![](../images/notifications/registration-complete.png)

## 後續步驟

依照本教學課程，您已註冊網頁掛接以接收[!DNL Experience Platform]和/或[!DNL Privacy Service]的[!DNL I/O Event]通知。 如需可用事件的詳細資訊以及如何解讀每項服務的通知裝載，請參閱下列檔案：

* [[!DNL Privacy Service] 通知](../../privacy-service/privacy-events.md)
* [[!DNL Data Ingestion] 通知](../../ingestion/quality/subscribe-events.md)
* [[!DNL Flow Service] （來源）通知](../../sources/notifications.md)

有關如何監視[!DNL Experience Platform]和[!DNL Privacy Service]上的活動的詳細資訊，請參閱[[!DNL Observability Insights] 概述](../home.md)。
