---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: 訂閱隱私權事件
topic: privacy events
translation-type: tm+mt
source-git-commit: 1bb896f7629d7b71b94dd107eeda87701df99208
workflow-type: tm+mt
source-wordcount: '843'
ht-degree: 0%

---


# 訂閱 [!DNL Privacy Events]

[!DNL Privacy Events] 是Adobe Experience Platform提供的訊息，它運 [!DNL Privacy Service]用傳送至已設定網頁掛接的Adobe I/O事件，以協助有效率的工作要求自動化。 它們可降低或免除輪詢 [!DNL Privacy Service] API的需求，以檢查工作是否完成或工作流程中是否達到特定里程碑。

目前有四種與隱私作業請求生命週期相關的通知類型：

| 類型 | 說明 |
--- | ---
| 工作完成 | 所有 [!DNL Experience Cloud] 解決方案都已回報，作業的整體或全域狀態已標示為完成。 |
| 作業錯誤 | 一或多個解決方案在處理請求時報告錯誤。 |
| 產品完整 | 與此工作相關的解決方案之一已完成其工作。 |
| 產品錯誤 | 其中一個解決方案在處理請求時報告錯誤。 |

本檔案提供在Adobe I/O中設定通 [!DNL Privacy Service] 知整合的步驟。如需隱私權服務概觀 [!DNL Privacy Service] 及其功能的詳細 [資訊](home.md)。

## 快速入門

本教學課程使 **用ngrok**，這是一種軟體產品，可透過安全隧道讓本機伺服器連接至公共網際網路。 在開 [始本教學課程](https://ngrok.com/download) 之前，請先安裝ngrok，以便後續操作並建立本機電腦的網頁掛接。 本指南還要求您下載包含簡單 [Node.js伺服器的GIT儲存庫](https://nodejs.org/) 。

## 建立本地伺服器

您的Node.js伺服器必須傳 `challenge` 回請求傳送至根(`/`)端點的參數。 使用下列JavaScript `index.js` 設定您的檔案，以完成此作業：

```js
var express = require('express')
var app = express()

app.set('port', (process.env.PORT || 3000))
app.use(express.static(__dirname + '/public'))

app.get('/', function(request, response) {
  response.send(request.originalUrl.split('?challenge=')[1]);
})

app.listen(app.get('port'), function() {
  console.log("Node app is running at localhost:" + app.get('port'))
})
```

使用命令行，導航到Node.js伺服器的根目錄。 然後，鍵入以下命令：

1. `npm install`
1. `npm start`

這些命令安裝所有依賴項並初始化伺服器。 如果成功，您可在http://localhost:3000/找到您的伺服器。

## 使用ngrok建立網頁掛接

開啟新的命令列視窗，並導覽至您先前安裝程式碼的目錄。 在此處鍵入以下命令：

```shell
./ngrok http -bind-tls=true 3000
```

成功的輸出看起來類似下列：

![ngrok輸出](images/privacy-events/ngrok-output.png)

請注意 `Forwarding` URL(`https://212d6cd2.ngrok.io`)，因為這將用來識別您的網頁鈎子，進行下一步。

## 在Adobe Developer Console中建立新專案

前往 [Adobe Developer Console](https://www.adobe.com/go/devs_console_ui) ，使用您的Adobe ID登入。 接著，請依照教學課程中說明的步驟， [在Adobe Developer Console檔案中建立空白的專案](https://www.adobe.io/apis/experienceplatform/console/docs.html#!AdobeDocs/adobeio-console/master/projects-empty.md) 。

## 新增隱私權事件至專案

在主控台中建立完新專案後，按一下「專案概 **[!UICONTROL 述」畫面上的]** 「新 _增事件_ 」。

![](./images/privacy-events/add-event-button.png)

此時將 _顯示「添加事件_ 」對話框。 選 **[!UICONTROL 擇Experience Cloud]** ，以篩選可用事件類型的清單，然後在按「下一步」前選 **[!UICONTROL 取「隱私服務事]** 件」 ****。

![](./images/privacy-events/add-privacy-events.png)

此時將 _顯示「配置事件_ 註冊」對話框。 選擇您要接收的事件，方法是選擇相應的複選框。 您選取的事件會顯示在左 **[!UICONTROL 欄的「訂閱事件]** 」下方。 When finished, click **[!UICONTROL Next]**.

![](./images/privacy-events/choose-subscriptions.png)

下一個畫面會提示您提供活動註冊的公開金鑰。 您可以選擇自動產生金鑰對，或上傳您在終端機中產生的公開金鑰。

在本教學課程中，會遵循第一個選項。 按一下「產生鍵 **[!UICONTROL 對」選項方塊]**，然後按一下右下角的「產 **[!UICONTROL 生鍵對]** 」按鈕。

![](./images/privacy-events/generate-key-value.png)

當鍵對產生時，瀏覽器會自動下載它。 您必須自行儲存此檔案，因為它不會保存在Developer Console中。

下一個畫面可讓您檢視新產生的金鑰對的詳細資訊。 按一 **[!UICONTROL 下]** 「下一步」繼續。

![](./images/privacy-events/keypair-generated.png)

在下一個畫面中，提供事件註冊的名稱和說明。 最佳實務是建立獨特、可輕鬆辨識的名稱，以協助區隔此活動註冊與同一專案中的其他活動。

![](./images/privacy-events/event-details.png)

在同一螢幕的下方，您會獲得兩個選項來設定如何接收事件。 選 **[!UICONTROL 取Webhook]** ，並提供您 `Forwarding` 先前在Webhook URL下建立之網頁掛接的 **[!UICONTROL URL]**。 接著，在按一下「儲存已設定的事件」以完成事件註冊之前，請選取您偏好的傳送樣式( **[!UICONTROL 單一或批次]** )。

![](./images/privacy-events/webhook-details.png)

專案的詳細資訊頁面會重新顯示，並 [!DNL Privacy Events] 顯示在左 **[!UICONTROL 側導覽]** 的「事件」下方。

## 檢視事件資料

在您已註冊專 [!DNL Privacy Events] 案和隱私權工作後，您就可以檢視該註冊的任何收到通知。 從「開 **[!UICONTROL 發人員控制台]** 」的「專案」標籤中，從清單中選取您的專案，以開啟「產 _品概述」頁面_ 。 在這裡，從左側導 **[!UICONTROL 覽中選取]** 「隱私權事件」。

![](./images/privacy-events/events-left-nav.png)

此時會 _顯示「註冊詳細資訊_ 」標籤，讓您檢視註冊的詳細資訊、編輯其設定，或檢視啟動網頁掛接後收到的實際事件。

![](./images/privacy-events/registration-details.png)

按一下「 **[!UICONTROL 除錯追蹤]** 」標籤，以檢視已接收事件的清單。 按一下列出的事件以檢視其詳細資訊。

![](images/privacy-events/debug-tracing.png)

「裝 **[!UICONTROL 載]** 」區段提供選取事件的詳細資訊，包括其事件類型(`com.adobe.platform.gdpr.productcomplete`)，如上例所強調。

## 後續步驟

您可以視需要重複上述步驟，為不同的網頁掛接位址新增整合。