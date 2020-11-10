---
keywords: Experience Platform;home;popular topics;date range
solution: Experience Platform
title: 訂閱Adobe I/O事件通知
topic: developer guide
description: 本檔案提供如何訂閱Adobe Experience Platform服務之Adobe I/O事件通知的步驟。 還提供了有關可用事件類型的參考資訊，以及有關如何解釋每個應用程式服務返回事件資料的進一步文檔的 [!DNL Platform] 連結。
translation-type: tm+mt
source-git-commit: f86f7483e7e78edf106ddd34dc825389dadae26a
workflow-type: tm+mt
source-wordcount: '763'
ht-degree: 1%

---


# 訂閱Adobe I/O事件通知

[!DNL Observability Insights] 可讓您訂閱Adobe Experience Platform活動的Adobe I/O活動通知。 這些事件會傳送至已設定的網頁掛接，以利活動監控的有效自動化。

本檔案提供如何訂閱Adobe Experience Platform服務之Adobe I/O事件通知的步驟。 還提供了有關可用事件類型的參考資訊，以及關於如何解釋每個適用服務的返回事件資料的進一步文檔的鏈 [!DNL Platform] 接。

## 快速入門

本檔案要求您瞭解Webhook，以及如何將Webhook從一個應用程式連接至另一個應用程式。 請參閱文 [[!DNL I/O Events] 件](https://www.adobe.io/apis/experienceplatform/events/docs.html#!adobedocs/adobeio-events/master/intro/webhook_docs_intro.md) ，以取得網頁勾點簡介。

## 建立網頁掛接

為了接收通知， [!DNL I/O Event] 您必須在事件註冊詳細資訊中指定唯一的網頁掛接URL來註冊網頁掛接。

您可以使用您選擇的用戶端來設定網頁掛接。 若要在本教學課程中使用臨時Webhook位址，請造訪 [Webhook.site](https://webhook.site/) ，並複製所提供的唯一URL。

![](../images/notifications/webhook-url.png)

在初始驗證過程中， [!DNL I/O Events] 將GET請 `challenge` 求中的查詢參數發送到Webhook。 您必須設定網頁掛接，以在回應裝載中傳回此參數的值。 如果您使用Webhook.site，請在右上角 **[!DNL Edit]** 選取，然後在選取前 `$request.query.challenge$` 先 **[!DNL Response body]** 在下方輸入 **[!DNL Save]**。

![](../images/notifications/response-challenge.png)

## 在Adobe Developer Console中建立新專案

前往 [Adobe Developer Console](https://www.adobe.com/go/devs_console_ui) ，使用您的Adobe ID登入。 接著，請依照教學課程中說明的步驟， [在Adobe Developer Console檔案中建立空白的專案](https://www.adobe.io/apis/experienceplatform/console/docs.html#!AdobeDocs/adobeio-console/master/projects-empty.md) 。

## 訂閱事件

建立新專案後，請導覽至該專案的概述畫面。 在這裡，選擇「 **[!UICONTROL 添加事件」]**。

![](../images/notifications/add-event-button.png)

此時會出現一個對話框，允許您向項目添加事件提供程式：

* 如果您要訂閱通知，請選 [!DNL Experience Platform] 取「平台 **[!UICONTROL 通知」]**
* 如果您要訂閱Adobe Experience Platform通知，請選 [!DNL Privacy Service] 取「隱私 **[!UICONTROL 服務事件」]**

選擇事件提供者後，選擇「下 **[!UICONTROL 一步]**」。

![](../images/notifications/event-provider.png)

下一個畫面會顯示要訂閱的事件類型清單。 選擇您要訂閱的事件，然後選擇「下 **[!UICONTROL 一步]**」。

>[!NOTE]
>
>如果您不確定要訂閱服務的事件，請參閱服務特定通知檔案：
>
>* [[!DNL Privacy Service] 通知](../../privacy-service/privacy-events.md)
>* [[!DNL Data Ingestion] 通知](../../ingestion/quality/subscribe-events.md)
>* [[!DNL Flow Service (sources)] 通知](../../sources/notifications.md)


![](../images/notifications/choose-event-subscriptions.png)

下一個畫面會提示您建立JSON網頁Token(JWT)。 您可以選擇自動產生金鑰對，或上傳您在終端機中產生的公開金鑰。

在本教學課程中，會遵循第一個選項。 選擇「生成密鑰 **[!UICONTROL 對」的選項框]**，然後選擇右下角的「 **[!UICONTROL 生成密鑰對]** 」按鈕。

![](../images/notifications/generate-keypair.png)

當鍵對產生時，瀏覽器會自動下載它。 您必須自行儲存此檔案，因為它不會保存在Developer Console中。

下一個畫面可讓您檢視新產生的金鑰對的詳細資訊。 選擇 **[!UICONTROL 下一步]** ，繼續。

![](../images/notifications/keypair-generated.png)

在下一個畫面中，在「活動註冊詳細資訊」區段中提供活動註冊的 [!UICONTROL 名稱和說明] 。 最佳實務是建立獨特、可輕鬆辨識的名稱，以協助區隔此活動註冊與同一專案中的其他活動。

![](../images/notifications/registration-details.png)

在相同畫面的下方， [!UICONTROL How to receive events] section（如何接收事件），您可選擇設定如何接收事件。 **[!UICONTROL Webhook]** 可讓您提供自訂的Webhook位址以接收事件，而 **[!UICONTROL Runtime動作則可讓您使用]** Adobe I/O Runtime進行相同動作 [](https://www.adobe.io/apis/experienceplatform/runtime/docs.html)。

在本教學課程中，請選 **[!UICONTROL 取Webhook]** ，並提供您先前建立之Webhook的URL。 完成後，選擇「保 **[!UICONTROL 存配置的事件]** 」以完成事件註冊。

![](../images/notifications/receive-events.png)

此時會顯示新建立事件註冊的詳細資訊頁面，您可在此處編輯其設定、檢閱收到的事件、執行除錯追蹤，以及新增事件提供者。

![](../images/notifications/registration-complete.png)

## 後續步驟

遵循本教學課程，您已註冊網頁掛接，以接收 [!DNL I/O Event] 和／或 [!DNL Experience Platform] 通知 [!DNL Privacy Service]。 有關可用事件以及如何解釋每項服務的通知負載的詳細資訊，請參閱以下文檔：

* [[!DNL Privacy Service] 通知](../../privacy-service/privacy-events.md)
* [[!DNL Data Ingestion] 通知](../../ingestion/quality/subscribe-events.md)
* [[!DNL Flow Service (sources)] 通知](../../sources/notifications.md)

如需如何 [[!DNL Observability Insights] 監控和](../home.md) 「」上活動的詳細資訊，請參閱 [!DNL Experience Platform] 總覽 [!DNL Privacy Service]。