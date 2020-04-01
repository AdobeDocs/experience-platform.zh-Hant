---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: 訂閱隱私權事件
topic: privacy events
translation-type: tm+mt
source-git-commit: e4cd042722e13dafc32b059d75fca2dab828df60

---


# 訂閱隱私權事件

隱私權事件是Adobe Experience Platform Privacy Service提供的訊息，該服務運用傳送至已設定網頁掛接的Adobe I/O Events，以協助有效率的工作要求自動化。 它們可降低或免除輪詢隱私權服務API的需求，以檢查工作是否完成或工作流程中是否達到特定里程碑。

目前有四種與隱私作業請求生命週期相關的通知類型：

| 類型 | 說明 |
--- | ---
| 工作完成 | 所有Experience Cloud解決方案都已回報，工作的整體或全域狀態已標示為完整。 |
| 作業錯誤 | 一或多個解決方案在處理請求時報告錯誤。 |
| 產品完整 | 與此工作相關的解決方案之一已完成其工作。 |
| 產品錯誤 | 其中一個解決方案在處理請求時報告錯誤。 |

本檔案提供在Adobe I/O中設定隱私權服務通知整合的步驟。如需隱私權服務及其功能的高階概觀，請參閱隱私權 [服務概觀](home.md)。

## 快速入門

本教學課程使 **用ngrok**，這是一種軟體產品，可透過安全隧道讓本機伺服器連接至公共網際網路。 在開 [始本教學課程](https://ngrok.com/download) 之前，請先安裝ngrok，以便後續操作並建立本機電腦的Webhook。 本指南還要求您下載GIT儲存庫，其中包含寫入 [Node.js的簡單伺服器](https://nodejs.org/)。

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

在同一目錄和新命令行窗口中，鍵入以下命令：

```shell
ngrok http -bind-tls=true 3000
```

成功的輸出看起來類似下列：

![ngrok輸出](images/privacy-events/ngrok-output.png)

請注意 `Forwarding` URL(`https://e142b577.ngrok.io`)，因為這將用來識別您的網頁鈎子，進行下一步。

## 使用Adobe I/O Console建立新的整合

登入 [Adobe I/O Console](https://console.adobe.io) ，然後按一下「整 **合」標籤** 。 此時會 _出現_ 「整合」視窗。 在這裡，按一下「 **新增整合」**。

![在Adobe I/O Console中檢視整合](images/privacy-events/integrations.png)

此時 *將出現「建立新整合* 」窗口。 選 **取「接收近即時事件」**，然後按一 **下「繼續」**。

![建立新整合](images/privacy-events/new-integration.png)

下一個畫面提供選項，可讓您根據您的訂閱、權益和權限，建立與組織可用的不同事件、產品和服務的整合。 對於此整合，請選取「隱 **私服務事件**」，然後按一 **下「繼續**」。

![選擇隱私權事件](images/privacy-events/privacy-events.png)

此時 *會顯示「整合詳細資訊* 」表單，您必須提供整合的名稱和說明，以及公開金鑰憑證。

![整合詳細資訊](images/privacy-events/integration-details.png)

如果您沒有公用憑證，則可使用下列terminal命令產生公用憑證：

```shell
openssl req -x509 -sha256 -nodes -days 365 -newkey rsa:2048 -keyout private.key -out certificate_pub
```

生成證書後，將檔案拖放到「 **Public keys certificates** 」（公鑰證書）框中，或按一下「 **Select a File** 」（選擇檔案）瀏覽檔案目錄並直接選擇證書。

新增憑證後，會出現「事 *件註冊* 」選項。 按一 **下新增事件註冊**。

![新增事件註冊](images/privacy-events/add-event-registration.png)

對話方塊會展開以顯示其他控制項。 您可以在這裡選取所需的事件類型，並註冊網頁掛接。 輸入事件註冊的名稱、網頁掛接URL(您最 `Forwarding` 初建立網頁 [掛接時傳回的位址](#create-a-webhook-using-ngrok))，以及簡短說明。 最後，選取您要訂閱的事件類型，然後按一下「儲 **存**」。

![活動註冊表單](images/privacy-events/event-registration-form.png)

完成「事件註冊」表單後，按一 **下「建立整合** 」,I/O整合就會完成。

![建立整合](images/privacy-events/create-integration.png)

## 檢視事件資料

在您建立I/O整合和隱私權工作後，您就可以檢視該整合的任何接收通知。 從I/O Console的 **Integrations** （整合）標籤，導覽至您的整合，然後按一下 **View**。

![檢視整合](images/privacy-events/view-integration.png)

此時會顯示整合的詳細資訊頁面。 按一 **下事件** ，檢視整合的事件註冊。 找到「隱私權事件」註冊，然後按一 **下「檢視**」。

![檢視活動註冊](images/privacy-events/view-registration.png)

此時 *會出現「事件詳細資料* 」視窗，可讓您檢視註冊的詳細資訊、編輯其設定，或檢視自啟動網頁掛接後收到的實際事件。 您可以檢視事件詳細資訊，並導覽至「除錯追蹤 **」選項** 。

![除錯追蹤](images/privacy-events/debug-tracing.png)

「裝 **載** 」區段提供選取事件的詳細資訊，包括其事件類型(`"com.adobe.platform.gdpr.productcomplete"`)，如上例所強調。

## 後續步驟

您可以視需要重複上述步驟，為不同的網頁掛接位址新增整合。