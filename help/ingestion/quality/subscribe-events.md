---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: 訂閱資料擷取事件
topic: overview
translation-type: tm+mt
source-git-commit: 4817162fe2b7cbf4ae4c1ed325db2af31da5b5d3

---


# 資料擷取通知

將資料擷取至Adobe Experience Platform的程式由多個步驟組成。 一旦您識別需要擷取至平台的資料檔案，擷取程式就會開始，每個步驟都會連續進行，直到資料被成功擷取或失敗為止。 您可以使用 [Adobe Experience Platform Data Ingestion API或Experience Platform使用者介面來啟動擷取程式](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/ingest-api.yaml) 。

載入平台的資料必須經過多個步驟，才能到達其目的地、資料湖或即時客戶個人檔案資料儲存。 每個步驟都包括處理資料、驗證資料，然後儲存資料，再傳遞至下一步驟。 視所擷取的資料量而定，這可能會變成耗時的程式，而且程式總會因為驗證、語義或處理錯誤而失敗。 發生故障時，需要修正資料問題，然後必須使用修正的資料檔案重新啟動整個擷取程式。

為協助監控擷取程式，Experience Platform可讓您訂閱流程每個步驟所發佈的一組事件，並通知您所擷取資料的狀態和任何可能的失敗。

## 可用狀態通知事件

以下是可供訂閱的可用資料擷取狀態通知清單。

>[!NOTE] 所有資料擷取通知只提供一個事件主題。 為了區分不同的狀態，可以使用事件代碼。

| 平台服務 | 狀態 | 事件說明 | 事件代碼 |
| ---------------- | ------ | ----------------- | ---------- |
| 資料著陸 | success | 擷取——批次成功 | ing_load_success |
| 資料著陸 | 失敗 | 擷取——批次失敗 | ing_load_failure |
| 即時客戶個人檔案 | success | 配置檔案服務——資料載入批成功 | ps_load_success |
| 即時客戶個人檔案 | 失敗 | 配置檔案服務——資料載入批失敗 | ps_load_failure |
| 身分圖 | success | 身份圖——資料載入批成功 | ig_load_success |
| 身分圖 | 失敗 | 身份圖——資料載入批失敗 | ig_load_failure |

## 通知裝載方案

資料擷取通知事件模式是包含欄位和值的體驗資料模型(XDM)模式，提供有關所擷取資料狀態的詳細資訊。 請造訪公開的XDM GitHub回購網站，以檢視最新的通知 [裝載方案](https://github.com/adobe/xdm/blob/master/schemas/common/notifications/ingestion.schema.json)。

## 訂閱資料擷取狀態通知

透過 [Adobe I/O Events](https://www.adobe.io/apis/experienceplatform/events.html)，您可以使用Webhook訂閱多種通知類型。 若要進一步瞭解網頁勾選，以及如何使用網頁勾選訂閱Adobe I/O Events，請參 [閱「Adobe I/O Events Webhooks指南](https://www.adobe.io/apis/experienceplatform/events/docs.html#!adobedocs/adobeio-events/master/intro/webhook_docs_intro.md) 」。

### 使用Adobe I/O Console建立新的整合

登入 [Adobe I/O Console](https://console.adobe.io/home) ，然後按一下「整合 *」標籤，或按一下「快* 速開始 **** 」下的「建立整合」。 出現「 *整合* 」畫面時，按一下「 **新增整合** 」以建立新整合。

![建立新整合](../images/quality/subscribe-events/create_integration_start.png)

此時會 *出現「建立新整合* 」畫面。 選 **取「接收近即時事件」**，然後按一 **下「繼續」**。

![接收近即時事件](../images/quality/subscribe-events/create_integration_receive_events.png)

下一個畫面提供選項，可讓您根據您的訂閱、權益和權限，建立與組織可用的不同事件、產品和服務的整合。 對於此整合，請選取「 **Experience Platform** 」（體驗平台）下的「Platform notifications **」（平台通知），然後按一**&#x200B;下「Continue」（繼續）。

![選擇事件提供者](../images/quality/subscribe-events/create_integration_select_provider.png)

此時 *會顯示「整合詳細資訊* 」表單，您必須提供整合的名稱和說明，以及公開金鑰憑證。

如果您沒有公用憑證，則可使用下列命令在終端中產生一個憑證：

```shell
openssl req -x509 -sha256 -nodes -days 365 -newkey rsa:2048 -keyout private.key -out certificate_pub
```

生成證書後，將檔案拖放到「 **Public keys certificates** 」（公鑰證書）框中，或按一下「 **Select a File** 」（選擇檔案）瀏覽檔案目錄並直接選擇證書。

新增憑證後，會出現「事 *件註冊* 」選項。 按一 **下新增事件註冊**。

![整合詳細資訊](../images/quality/subscribe-events/create_integration_details.png)

「事 *件註冊詳細資訊* 」對話方塊會展開以顯示其他控制項。 您可以在這裡選取所需的事件類型，並註冊網頁掛接。 輸入事件註冊的名稱、網頁 *掛接URL（可選）*，以及簡短說明。 最後，選取您要訂閱的事件類型（資料擷取通知），然後按一下「儲 **存**」。

![選擇事件](../images/quality/subscribe-events/create_integration_select_event.png)

## 後續步驟

建立I/O整合後，您就可以檢視該整合的任何已接收通知。 如需如何追 [蹤事件的詳細指示，請參閱「追蹤Adobe I/O事件](https://www.adobe.io/apis/experienceplatform/events/docs.html#!adobedocs/adobeio-events/master/support/tracing.md) 」指南。
