---
title: Shopify流源
description: 了解如何建立來源連線和資料流，以將串流資料從Shopify執行個體內嵌至Adobe Experience Platform
badge: "Beta"
hidefromtoc: y
hide: y
source-git-commit: 279d8e307c8ca5a799a47c6f903b9a082d9cf034
workflow-type: tm+mt
source-wordcount: '682'
ht-degree: 2%

---

# [!DNL Shopify Streaming]

>[!NOTE]
>
>此 [!DNL Shopify Streaming] 來源為測試版。 請閱讀 [來源概觀](../../home.md#terms-and-conditions) 以取得使用測試版標籤來源的詳細資訊。

Adobe Experience Platform支援從串流應用程式擷取資料。 支援串流提供者包括 [!DNL Shopify].

## 先決條件 {#prerequisites}

以下章節概述使用前要完成的先決條件步驟 [!DNL Shopify Streaming] 來源。

您必須具備有效 [!DNL Shopify] 合作夥伴帳戶，以便連線至 [!DNL Shopify] API。 如果您尚未擁有合作夥伴帳戶，請使用 [[!DNL Shopify] 合作夥伴儀表板](https://www.shopify.com/partners).

### 建立您的應用程式

具有有效 [!DNL Shopify] 合作夥伴帳戶，您現在可以使用合作夥伴控制面板繼續並建立您的應用程式。 如需如何在中建立應用程式的完整步驟 [!DNL Shopify]，請閱讀 [[!DNL Shopify] 快速入門手冊](https://www.shopify.com/partners/blog/17056443-how-to-generate-a-shopify-api-token).

建立應用程式後，擷取您的 **用戶端ID** 和 **用戶密碼** 從 **客戶端憑據** 的 [!DNL Shopify] 合作夥伴控制面板。 用戶端ID和用戶端密碼將用於後續步驟，以擷取您的授權碼和存取權杖。

### 擷取授權代碼

接下來，輸入您網域的 `myshopify.com` 瀏覽器的URL，以及定義API金鑰、範圍和重新導向URI的查詢字串。

此URL的格式如下：

**API格式**

```http
https://{SHOP}.myshopify.com/admin/oauth/authorize?client_id={API_KEY}&scope={SCOPES}&redirect_uri={REDIRECT_URI}
```

| 參數 | 說明 |
| --- | --- |
| `shop` | 您的子網域 `myshopify.com` URL。 |
| `api_key` | 您的 [!DNL Shopify] 用戶端ID。 您可以從 **客戶端憑據** 的 [!DNL Shopify] 合作夥伴控制面板。 |
| `scopes` | 您要定義的存取類型。 例如，您可以將範圍設定為 `scope=write_orders,read_customers` 允許權限修改訂單和讀取客戶。 |
| `redirect_uri` | 將產生存取權杖的指令碼的URL。 |

**要求**

```http
https://connnectors-test.myshopify.com/admin/oauth/authorize?client_id=l6fiviermmzpram5i1spfub99shms3j9&scope=write_orders,read_customers&redirect_uri=https://acme.com
```

**回應**

成功的回應會傳回您的重新導向URL，包括產生存取權杖所需的授權碼。

```http
https://www.acme.com/?code=k6j2palgrbljja228ou8c20fmn7w41gz&hmac=68c9163f772eecbc8848c90f695bca0460899c125af897a6d2b0ebbd59d3a43b&shop=connnectors-test.myshopify.com&state=123456×tamp=1658305460
```

### 擷取您的存取權杖

現在您擁有用戶端ID、用戶端密碼和授權程式碼，便可擷取存取權杖。 若要擷取存取權杖，請對您網域的 `myshopify.com` 在附加此URL時使用 [!DNL Shopify's] API端點： `/admin/oauth/access_token`.

**API格式**

```https
POST /{SHOP}.myshopify.com/admin/oauth/access_token
```

**要求**

下列請求會為您的 [!DNL Shopify] 例項。

```shell
curl -X POST \
  'https://connnectors-test.myshopify.com/admin/oauth/access_token' \
  -H 'developer-token: {DEVELOPER_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'Cookie: _master_udr=xxx; request_method=POST'
  -d '{
    "client_id": "l6fiviermmzpram5i1spfub99shms3j9",
    "client_secret": "dajn3caxz9s7ti624ncyv_m4f60jnwi3ii3y3k",
    "code": "k6j2palgrbljja228ou8c20fmn7w41gz"
}'
```

**回應**

成功的回應會傳回您的存取權杖和權限範圍。

```json
{
  "access_token": "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",
  "scope": "write_orders,read_customers"
}
```

## 建立串流的網頁連結 [!DNL Shopify] 資料 {#webhook}

Webhook可讓應用程式與您的 [!DNL Shopify] 在商店中發生特定事件後執行資料或動作。 用於串流 [!DNL Shopify] 資料Experience Platform時，可使用webhook來定義http端點和訂閱主題。

**要求**

下列請求會為您的 [!DNL Shopify Streaming] 資料。

```shell
curl -X POST \
  'https://connnectors-test.myshopify.com/admin/api/2022-07/webhooks.json' \
  -H 'X-Shopify-Access-Token: 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' \
  -H 'Content-Type: application/json' \; request_method=POST' \
  -d '{
  "webhook": {
    "address": "https://dcs.adobedc.net/collection/9d411a24aa3c0a3eded92bac6c64d0da986ee7a8212f87168c5fb42d9ddc3227",
    "topic": "orders/create",
    "format": "json"
  }
}'
```

| 參數 | 說明 |
| --- | --- | 
| `webhook.address` | 傳送串流訊息的http端點。 |
| `webhook.topic` | 網頁連結訂閱的主題。 如需詳細資訊，請閱讀 [[!DNL Shopify] webhook事件主題指南](https://shopify.dev/docs/api/admin-rest/2023-04/resources/webhook#event-topics). |
| `webhook.format` | 資料的格式。 |

**回應**

成功的回應會傳回您網頁連結上的資訊，包括其對應的資訊 `id`、位址和其他中繼資料資訊。

```json
{
  "webhook": {
    "id": 1091138715786,
    "address": "https://dcs.adobedc.net/collection/9d411a24aa3c0a3eded92bac6c64d0da986ee7a8212f87168c5fb42d9ddc3227",
    "topic": "orders/create",
    "created_at": "2022-07-20T07:15:23-04:00",
    "updated_at": "2022-07-20T07:15:23-04:00",
    "format": "json",
    "fields": [],
    "metafield_namespaces": [],
    "api_version": "2021-10",
    "private_metafield_namespaces": []
  }
}
```

### 限制 {#limitations}

以下是使用Webhook與 [!DNL Shopify Streaming] 來源。

* 無法保證您可以針對相同資源安排不同主題的傳送順序。 例如，有可能 `products/update` 網頁鈎在 `products/create` 網頁鈎點。
* 您可以設定Webhook，以至少將Webhook事件傳送至端點一次。 這表示端點可能會多次收到相同的事件。 您可以比較 `X-Shopify-Webhook-Id` 標題至先前事件。
* [!DNL Shopify] 將HTTP 2xx狀態回應視為成功通知。 任何其他狀態代碼響應都被視為失敗。 [!DNL Shopify] 為失敗的webhook通知提供重試機制。 如果有 **等待5秒後無響應**, [!DNL Shopify] 重試連接 **19倍** 在下一個過程中 **48小時**. 如果重試期間結束時仍沒有響應，則 [!DNL Shopify] 刪除webhook。

## 後續步驟

下列教學課程提供如何連結您的 [!DNL Shopify Streaming] 來源Experience Platform:

* [使用流服務API建立Shopify流源連接和資料流](../../tutorials/api/create/ecommerce/shopify-streaming.md)
* [在UI中建立Shopify流源連接和資料流](../../tutorials/ui/create/ecommerce/shopify-streaming.md)
