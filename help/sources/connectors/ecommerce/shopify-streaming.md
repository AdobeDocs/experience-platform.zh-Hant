---
title: Shopify串流Source
description: 瞭解如何建立來源連線和資料流，以將來自您的Shopify執行個體的串流資料擷取到Adobe Experience Platform
badge: Beta
last-substantial-update: 2023-04-26T00:00:00Z
exl-id: ae991913-68b5-4bbb-b8a5-e566d67a4c1a
source-git-commit: b4334b4f73428f94f5a7e5088f98e2459afcaf3c
workflow-type: tm+mt
source-wordcount: '671'
ht-degree: 2%

---

# [!DNL Shopify Streaming]

>[!NOTE]
>
>[!DNL Shopify Streaming]來源是測試版。 如需使用Beta版標籤來源的相關資訊，請參閱[來源概觀](../../home.md#terms-and-conditions)。

Adobe Experience Platform支援從串流應用程式擷取資料。 對串流提供者的支援包括[!DNL Shopify]。

## 先決條件 {#prerequisites}

以下章節概述使用[!DNL Shopify Streaming]來源之前要完成的先決條件步驟。

您必須擁有有效的[!DNL Shopify]合作夥伴帳戶才能連線至[!DNL Shopify] API。 如果您還沒有合作夥伴帳戶，請使用[[!DNL Shopify] 合作夥伴儀表板](https://www.shopify.com/partners)進行註冊。

### 建立您的應用程式

使用有效的[!DNL Shopify]合作夥伴帳戶，您現在可以使用合作夥伴儀表板繼續並建立您的應用程式。 如需有關如何在[!DNL Shopify]中建立應用程式的完整步驟，請閱讀快速入門的[[!DNL Shopify] 指南](https://www.shopify.com/partners/blog/17056443-how-to-generate-a-shopify-api-token)。

建立您的應用程式後，請從[!DNL Shopify]合作夥伴儀表板的&#x200B;**使用者端認證**&#x200B;索引標籤中擷取您的&#x200B;**使用者端識別碼**&#x200B;和&#x200B;**使用者端密碼**。 使用者端ID和使用者端密碼將在後續步驟中使用，以擷取您的授權代碼和存取權杖。

### 擷取您的授權代碼

接下來，請在瀏覽器中輸入網域的`myshopify.com` URL，以及定義您的API金鑰、範圍和重新導向URI的查詢字串，以擷取您的授權代碼。

此URL的格式如下：

**API格式**

```http
https://{SHOP}.myshopify.com/admin/oauth/authorize?client_id={API_KEY}&scope={SCOPES}&redirect_uri={REDIRECT_URI}
```

| 參數 | 說明 |
| --- | --- |
| `shop` | 您的子網域`myshopify.com` URL。 |
| `api_key` | 您的[!DNL Shopify]使用者端識別碼。 您可以從[!DNL Shopify]合作夥伴儀表板的&#x200B;**使用者端認證**&#x200B;標籤擷取使用者端ID。 |
| `scopes` | 您要定義的存取權型別。 例如，您可以將範圍設定為`scope=write_orders,read_customers`，以允許修改訂單和讀取客戶的許可權。 |
| `redirect_uri` | 將會產生存取權杖的指令碼URL。 |

**要求**

```http
https://connnectors-test.myshopify.com/admin/oauth/authorize?client_id=l6fiviermmzpram5i1spfub99shms3j9&scope=write_orders,read_customers&redirect_uri=https://acme.com
```

**回應**

成功的回應會傳回您的重新導向URL，包括產生存取權杖所需的授權代碼。

```http
https://www.acme.com/?code=k6j2palgrbljja228ou8c20fmn7w41gz&hmac=68c9163f772eecbc8848c90f695bca0460899c125af897a6d2b0ebbd59d3a43b&shop=connnectors-test.myshopify.com&state=123456×tamp=1658305460
```

### 擷取您的存取權杖

現在您已取得使用者端ID、使用者端密碼和授權碼，您可以擷取存取權杖。 若要擷取您的存取Token，請在使用[!DNL Shopify's] API端點附加此URL時向網域的`myshopify.com` URL提出POST要求： `/admin/oauth/access_token`。

**API格式**

```https
POST /{SHOP}.myshopify.com/admin/oauth/access_token
```

**要求**

下列要求會產生您[!DNL Shopify]執行個體的存取權杖。

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

成功的回應會傳回您的存取權杖和許可權範圍。

```json
{
  "access_token": "shpca_wjhifwfc91psjtldysxd6rqli371tx54",
  "scope": "write_orders,read_customers"
}
```

## 建立webhook以串流[!DNL Shopify]資料 {#webhook}

Webhook可讓應用程式與您的[!DNL Shopify]資料保持同步，或在商店中發生特定事件後執行動作。 若要將[!DNL Shopify]資料串流至Experience Platform，webhook可用來定義http端點和訂閱的主題。

**要求**

以下請求會為您的[!DNL Shopify Streaming]資料建立webhook。

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
| `webhook.topic` | 您的webhook訂閱主題。 如需詳細資訊，請閱讀[[!DNL Shopify] webhook活動主題指南](https://shopify.dev/docs/api/admin-rest/2023-04/resources/webhook#event-topics)。 |
| `webhook.format` | 資料的格式。 |

**回應**

成功的回應會傳回您webhook上的資訊，包括其對應的`id`、位址和其他中繼資料資訊。

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

下列是將webhook與[!DNL Shopify Streaming]來源搭配使用時，您可能會遇到的已知限制清單。

* 並不保證您可以為相同資源安排不同主題的傳送順序。 例如，`products/update` webhook可能會在`products/create` webhook之前傳遞。
* 您可以設定webhook將webhook事件至少傳送一次到端點。 這表示端點可能會收到相同事件多次。 您可以將`X-Shopify-Webhook-Id`標頭與先前的事件做比較，以掃描重複的webhook事件。
* [!DNL Shopify]會將HTTP 2xx狀態回應視為成功通知。 任何其他狀態代碼回應均視為失敗。 [!DNL Shopify]為失敗的webhook通知提供重試機制。 如果等候5秒後&#x200B;**沒有回應**，[!DNL Shopify]會在接下來的&#x200B;**48小時**&#x200B;內重試連線&#x200B;**19次**。 如果重試期間結束時仍然沒有回應，則[!DNL Shopify]會刪除webhook。

## 後續步驟

下列教學課程提供如何使用API和UI將您的[!DNL Shopify Streaming]來源連線到Experience Platform的步驟：

* [使用Flow Service API建立Shopify串流來源連線和資料流](../../tutorials/api/create/ecommerce/shopify-streaming.md)
* [在UI中建立Shopify串流來源連線和資料流](../../tutorials/ui/create/ecommerce/shopify-streaming.md)
