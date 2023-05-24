---
title: Shopify流源
description: 瞭解如何建立源連接和資料流，以便將流資料從Shopify實例接收到Adobe Experience Platform
badge: β
exl-id: 4c83c08d-c744-4167-9e3b-ed9a995943f4
source-git-commit: feb05d5bddc4135c5fe14d3ec5d8fad62c5e2236
workflow-type: tm+mt
source-wordcount: '682'
ht-degree: 2%

---

# [!DNL Shopify Streaming]

>[!NOTE]
>
>的 [!DNL Shopify Streaming] 源為beta。 請閱讀 [源概述](../../home.md#terms-and-conditions) 的子菜單。

Adobe Experience Platform為從流應用程式接收資料提供支援。 對流提供商的支援包括 [!DNL Shopify]。

## 先決條件 {#prerequisites}

以下部分概述了在使用前要完成的先決條件步驟 [!DNL Shopify Streaming] 源。

您必須具有 [!DNL Shopify] 合作夥伴帳戶，以便連接到 [!DNL Shopify] API。 如果您尚沒有合作夥伴帳戶，請使用 [[!DNL Shopify] 合作夥伴儀表板](https://www.shopify.com/partners)。

### 建立應用程式

具有有效 [!DNL Shopify] 合作夥伴帳戶，您現在可以使用合作夥伴儀表板繼續並建立您的應用。 有關如何在中建立應用程式的全面步驟 [!DNL Shopify]，閱讀 [[!DNL Shopify] 入門指南](https://www.shopify.com/partners/blog/17056443-how-to-generate-a-shopify-api-token)。

建立應用後，檢索 **客戶端ID** 和 **客戶端機密** 從 **客戶端憑據** 頁籤 [!DNL Shopify] 合作夥伴儀表板。 在後續步驟中將使用客戶端ID和客戶端密碼來檢索您的授權代碼和訪問令牌。

### 檢索授權代碼

接下來，輸入域的 `myshopify.com` 瀏覽器中的URL以及定義API密鑰、作用域和重定向URI的查詢字串。

此URL的格式如下：

**API格式**

```http
https://{SHOP}.myshopify.com/admin/oauth/authorize?client_id={API_KEY}&scope={SCOPES}&redirect_uri={REDIRECT_URI}
```

| 參數 | 說明 |
| --- | --- |
| `shop` | 子域 `myshopify.com` URL。 |
| `api_key` | 您 [!DNL Shopify] 客戶端ID。 可從 **客戶端憑據** 頁籤 [!DNL Shopify] 合作夥伴儀表板。 |
| `scopes` | 要定義的訪問類型。 例如，可以將作用域設定為 `scope=write_orders,read_customers` 允許修改訂單和讀取客戶的權限。 |
| `redirect_uri` | 將生成訪問令牌的指令碼的URL。 |

**要求**

```http
https://connnectors-test.myshopify.com/admin/oauth/authorize?client_id=l6fiviermmzpram5i1spfub99shms3j9&scope=write_orders,read_customers&redirect_uri=https://acme.com
```

**回應**

成功的響應將返回重定向URL，包括生成訪問令牌所需的授權代碼。

```http
https://www.acme.com/?code=k6j2palgrbljja228ou8c20fmn7w41gz&hmac=68c9163f772eecbc8848c90f695bca0460899c125af897a6d2b0ebbd59d3a43b&shop=connnectors-test.myshopify.com&state=123456×tamp=1658305460
```

### 檢索訪問令牌

現在，您擁有了客戶端ID、客戶端密碼和授權代碼，您就可以檢索訪問令牌。 要檢索您的訪問令牌，請向域發出POST請求 `myshopify.com` 附加此URL時的URL [!DNL Shopify's] API終結點： `/admin/oauth/access_token`。

**API格式**

```https
POST /{SHOP}.myshopify.com/admin/oauth/access_token
```

**要求**

以下請求為您生成訪問令牌 [!DNL Shopify] 實例。

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

成功的響應將返回您的訪問令牌和權限作用域。

```json
{
  "access_token": "shpca_wjhifwfc91psjtldysxd6rqli371tx54",
  "scope": "write_orders,read_customers"
}
```

## 建立用於流式傳輸的Webhook [!DNL Shopify] 資料 {#webhook}

Webhooks允許應用程式與您的 [!DNL Shopify] 在商店中發生特定事件後執行操作。 對於流 [!DNL Shopify] 資料到Experience Platform,webhooks可用於定義http端點和訂閱主題。

**要求**

以下請求為您的 [!DNL Shopify Streaming] 資料。

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
| `webhook.address` | 發送流消息的http終結點。 |
| `webhook.topic` | Webhook訂閱的主題。 有關詳細資訊，請閱讀 [[!DNL Shopify] WebHook事件主題指南](https://shopify.dev/docs/api/admin-rest/2023-04/resources/webhook#event-topics)。 |
| `webhook.format` | 資料的格式。 |

**回應**

成功的響應將返回Webhook上的資訊，包括其對應的資訊 `id`、地址和其他元資料資訊。

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

以下是使用Webhook時可能遇到的已知限制的清單 [!DNL Shopify Streaming] 源。

* 不能保證您可以為同一資源安排不同主題的交付順序。 比如，有可能 `products/update` 網鈎在 `products/create` 網鈎。
* 您可以設定Webhook，以至少將Webhook事件傳送到端點。 這意味著端點可能多次接收同一事件。 通過比較 `X-Shopify-Webhook-Id` 標題。
* [!DNL Shopify] 將HTTP 2xx狀態響應視為成功通知。 任何其他狀態代碼響應都被視為失敗。 [!DNL Shopify] 為失敗的webhook通知提供重試機制。 如果有 **等待5秒後沒有響應**。 [!DNL Shopify] 重試連接 **19次** 在下一個過程中 **48小時**。 如果在重試期間結束時仍沒有響應，則 [!DNL Shopify] 刪除webhook。

## 後續步驟

以下教程提供了有關如何連接的步驟 [!DNL Shopify Streaming] 源到Experience Platform:

* [使用流服務API建立Shopify流源連接和資料流](../../tutorials/api/create/ecommerce/shopify-streaming.md)
* [在UI中建立Shopify流源連接和資料流](../../tutorials/ui/create/ecommerce/shopify-streaming.md)
