---
keywords: Experience Platform；首頁；熱門主題；日期範圍
solution: Experience Platform
title: 訂閱Adobe I/O事件通知
topic-legacy: developer guide
description: 本檔案提供如何訂閱Adobe Experience Platform服務Adobe I/O事件通知的步驟。 還提供了有關可用事件類型的參考資訊，以及關於如何解釋每個適用 [!DNL Platform] 服務的返回事件資料的進一步文檔的連結。
exl-id: c0ad7217-ce84-47b0-abf6-76bcf280f026
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '740'
ht-degree: 1%

---

# 訂閱Adobe I/O事件通知

[!DNL Observability Insights] 可讓您訂閱有關Adobe I/O活動的「活動」通知。這些事件會傳送至已設定的網頁掛接，以利活動監控的有效自動化。

本檔案提供如何訂閱Adobe Experience Platform服務Adobe I/O事件通知的步驟。 還提供了有關可用事件類型的參考資訊，以及有關如何解釋每個適用[!DNL Platform]服務返回事件資料的進一步文檔的連結。

## 快速入門

本檔案要求您瞭解Webhook，以及如何將Webhook從一個應用程式連接至另一個應用程式。 有關Webhook的簡介，請參閱[[!DNL I/O Events] documentation](https://www.adobe.io/apis/experienceplatform/events/docs.html#!adobedocs/adobeio-events/master/intro/webhook_docs_intro.md)。

## 建立網頁掛接

為了接收[!DNL I/O Event]通知，您必須指定唯一的網頁掛接URL作為事件註冊詳細資訊的一部分來註冊網頁掛接。

您可以使用您選擇的用戶端來設定網頁掛接。 若要在本教學課程中使用臨時Webhook位址，請造訪[Webhook.site](https://webhook.site/)並複製提供的唯一URL。

![](../images/notifications/webhook-url.png)

在初始驗證過程中，[!DNL I/O Events]將GET請求中的`challenge`查詢參數發送到webhook。 您必須設定網頁掛接，以在回應裝載中傳回此參數的值。 如果您使用Webhook.site，請在右上角選擇&#x200B;**[!DNL Edit]**，然後在&#x200B;**[!DNL Response body]**&#x200B;下輸入`$request.query.challenge$`，然後再選擇&#x200B;**[!DNL Save]**。

![](../images/notifications/response-challenge.png)

## 在Adobe開發人員主控台中建立新專案

前往[Adobe開發人員主控台](https://www.adobe.com/go/devs_console_ui)並使用您的Adobe ID登入。 接下來，請依照[教學課程中描述的步驟，在「Adobe開發人員主控台」檔案中建立空白專案](https://www.adobe.io/apis/experienceplatform/console/docs.html#!AdobeDocs/adobeio-console/master/projects-empty.md)。

## 訂閱事件

建立新專案後，請導覽至該專案的概述畫面。 從此處選擇&#x200B;**[!UICONTROL Add event]**。

![](../images/notifications/add-event-button.png)

此時會出現一個對話框，允許您向項目添加事件提供程式：

* 如果您要訂閱[!DNL Experience Platform]通知，請選擇&#x200B;**[!UICONTROL Platform notifications]**
* 如果您要訂閱Adobe Experience Platform[!DNL Privacy Service]通知，請選擇&#x200B;**[!UICONTROL Privacy Service Events]**

選擇事件提供者後，請選擇&#x200B;**[!UICONTROL Next]**。

![](../images/notifications/event-provider.png)

下一個畫面會顯示要訂閱的事件類型清單。 選擇要訂閱的事件，然後選擇&#x200B;**[!UICONTROL Next]**。

>[!NOTE]
>
>如果您不確定要訂閱服務的事件，請參閱服務特定通知檔案：
>
>* [[!DNL Privacy Service] 通知](../../privacy-service/privacy-events.md)
>* [[!DNL Data Ingestion] 通知](../../ingestion/quality/subscribe-events.md)
>* [[!DNL Flow Service (sources)] 通知](../../sources/notifications.md)


![](../images/notifications/choose-event-subscriptions.png)

下一個畫面會提示您建立JSON網頁Token(JWT)。 您可以選擇自動產生金鑰對，或上傳您在終端機中產生的公開金鑰。

在本教學課程中，會遵循第一個選項。 選擇&#x200B;**[!UICONTROL Generate a key pair]**&#x200B;的選項框，然後選擇右下角的&#x200B;**[!UICONTROL Generate keypair]**&#x200B;按鈕。

![](../images/notifications/generate-keypair.png)

當鍵對產生時，瀏覽器會自動下載它。 您必須自行儲存此檔案，因為它不會保存在Developer Console中。

下一個畫面可讓您檢視新產生的金鑰對的詳細資訊。 選擇&#x200B;**[!UICONTROL Next]**&#x200B;繼續。

![](../images/notifications/keypair-generated.png)

在下一個畫面中，在[!UICONTROL Event registration details]區段中提供事件註冊的名稱和說明。 最佳實務是建立獨特、可輕鬆辨識的名稱，以協助區隔此活動註冊與同一專案中的其他活動。

![](../images/notifications/registration-details.png)

在[!UICONTROL How to receive events]區段下方的相同畫面上，您可選擇設定接收事件的方式。 **[!UICONTROL Webhook]** 可讓您提供自訂網頁掛接位址以接收事件， **[!UICONTROL Runtime action]** 而您也可使用 [Adobe I/O Runtime](https://www.adobe.io/apis/experienceplatform/runtime/docs.html)。

在本教學課程中，請選取&#x200B;**[!UICONTROL Webhook]**&#x200B;並提供您先前建立之網頁掛接的URL。 完成後，選擇&#x200B;**[!UICONTROL Save configured events]**&#x200B;完成事件註冊。

![](../images/notifications/receive-events.png)

此時會顯示新建立事件註冊的詳細資訊頁面，您可在此處編輯其設定、檢閱收到的事件、執行除錯追蹤，以及新增事件提供者。

![](../images/notifications/registration-complete.png)

## 後續步驟

在本教學課程中，您已註冊網頁掛接，以接收[!DNL Experience Platform]和／或[!DNL Privacy Service]的[!DNL I/O Event]通知。 有關可用事件以及如何解釋每項服務的通知負載的詳細資訊，請參閱以下文檔：

* [[!DNL Privacy Service] 通知](../../privacy-service/privacy-events.md)
* [[!DNL Data Ingestion] 通知](../../ingestion/quality/subscribe-events.md)
* [[!DNL Flow Service (sources)] 通知](../../sources/notifications.md)

如需如何監控[!DNL Experience Platform]和[!DNL Privacy Service]上活動的詳細資訊，請參閱[[!DNL Observability Insights] overview](../home.md)。
