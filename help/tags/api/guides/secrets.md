---
title: Reactor API的秘密
description: 瞭解如何在Reactor API中設定用於事件轉送的秘密的基礎知識。
exl-id: 0298c0cd-9fba-4b54-86db-5d2d8f9ade54
source-git-commit: 88939d674c0002590939004e0235d3da8b072118
workflow-type: tm+mt
source-wordcount: '1206'
ht-degree: 2%

---

# Reactor API的秘密

在Reactor API中，密碼是代表驗證認證的資源。 在事件轉送中使用密碼來驗證到另一個系統的安全資料交換。 因此，只能在事件轉送屬性（`platform`屬性設定為`edge`的屬性）中建立密碼。

`type_of`屬性中目前表示三種支援的密碼型別：

| 密碼型別 | 說明 |
| --- | --- |
| `token` | 代表兩個系統已知且瞭解的驗證Token值的單一字元字串。 |
| `simple-http` | 包含使用者名稱和密碼的兩個字串屬性。 |
| `oauth2-client_credentials` | 包含數個屬性以支援[OAuth](https://datatracker.ietf.org/doc/html/rfc6749)驗證規格。 事件轉送會要求您提供必要資訊，然後以指定間隔為您處理這些權杖的續約。 |

{style="table-layout:auto"}

本指南提供如何設定用於事件轉送的密碼的整體概觀。 如需有關如何在Reactor API中管理秘密的詳細指引，包括秘密結構的JSON範例，請參閱[秘密端點指南](../endpoints/secrets.md)。

## 認證

每個密碼都包含儲存其個別認證值的`credentials`屬性。 在[在API](../endpoints/secrets.md#create)中建立密碼時，每種型別的密碼都有不同的必要屬性，如以下小節所示：

* [&#39;token&#39;](#token)
* [&#39;simple-http&#39;](#simple-http)
* [&#39;oauth2-client_credentials&#39;](#oauth2-client_credentials)
* [&#39;oauth2-google&#39;](#oauth2-google)

### `token` {#token}

`type_of`值為`token`的密碼只需要`credentials`下的單一屬性：

| 認證屬性 | 資料類型 | 說明 |
| --- | --- | --- |
| `token` | 字串 | 目的地系統可識別的秘密權杖。 |

{style="table-layout:auto"}

權杖會儲存為靜態值，因此在建立密碼時，密碼的`expires_at`和`refresh_at`屬性會設定為`null`。

### `simple-http` {#simple-http}

`type_of`值為`simple-http`的密碼需要`credentials`下的下列屬性：

| 認證屬性 | 資料類型 | 說明 |
| --- | --- | --- |
| `username` | 字串 | 使用者名稱。 |
| `password` | 字串 | 密碼。 API回應中不包含此值。 |

{style="table-layout:auto"}

建立密碼時，兩個屬性會以`username:password`的BASE64編碼交換。 交換之後，密碼的`expires_at`和`refresh_at`屬性設定為`null`。

### `oauth2-client_credentials` {#oauth2-client_credentials}

`type_of`值為`oauth2-client_credentials`的密碼需要`credentials`下的下列屬性：

| 認證屬性 | 資料類型 | 說明 |
| --- | --- | --- |
| `client_id` | 字串 | OAuth整合的使用者端ID。 |
| `client_secret` | 字串 | OAuth整合的使用者端密碼。 API回應中不包含此值。 |
| `token_url` | 字串 | Oauth整合的授權URL。 |
| `refresh_offset` | 整數 | *（選擇性）*&#x200B;要位移重新整理作業的值（秒）。 如果在建立密碼時省略此屬性，則預設值會設為`14400` （4小時）。 |
| `options` | 物件 | *（選擇性）*&#x200B;指定OAuth整合的其他選項：<ul><li>`scope`：代表認證之[OAuth 2.0領域](https://oauth.net/2/scope/)的字串。</li><li>`audience`：代表[Auth0存取權杖](https://auth0.com/docs/protocols/protocol-oauth2)的字串。</li></ul> |

建立或更新`oauth2-client_credentials`密碼時，會根據OAuth通訊協定的「使用者端認證」流程，在POST要求中將`client_id`和`client_secret` （可能還有`options`）交換給`token_url`。

>[!NOTE]
>
>預期授權服務回應本文與OAuth通訊協定相容。

如果授權服務以`200 OK`和JSON回應本文回應，則會剖析本文並將`access_token`推送至邊緣環境，並使用`expires_in`計算密碼的`expires_at`和`refresh_at`屬性。 如果密碼上沒有環境關聯，則會捨棄`access_token`。

在以下條件下，憑證交換被視為成功：

* `expires_in`大於`28800` （8小時）。
* `refresh_offset`小於`expires_in`減去`14400`的值（四個小時）。 例如，如果`expires_in`是`36000` （十小時），而`refresh_offset`是`28800` （八小時），則交換會被視為失敗，因為`28800`大於`36000` - `14400` (`21600`)。

如果交換成功，密碼的狀態屬性會設為`succeeded`，且會設定`expires_at`與`refresh_at`的值：

* `expires_at`為目前的UTC時間加上`expires_in`的值。
* `refresh_at`為目前的UTC時間加上`expires_in`的值減去`refresh_offset`的值。 例如，如果`expires_in`是`43200` （十二小時），而`refresh_offset`是`14400` （四個小時），則`refresh_at`屬性會在目前的UTC時間之後設定為`28800` （八個小時）。

如果交換因任何原因失敗，`meta`物件中的`status_details`屬性會以相關資訊更新。

#### 正在重新整理`oauth2-client_credentials`密碼

如果已將`oauth2-client_credentials`密碼指派給環境且其狀態為`succeeded` （已成功交換認證），則會在`refresh_at`上自動執行新的交換。

如果交換成功，`meta`物件中的`refresh_status`屬性會設為`succeeded`，而`expires_at`、`refresh_at`和`activated_at`會相應地更新。

如果交換失敗，會再嘗試作業三次，最後一次嘗試的時間不超過存取權杖過期的兩小時。 如果所有嘗試都失敗，來自`meta`物件的`refresh_status_details`屬性會以相關詳細資料更新。

### `oauth2-google` {#oauth2-google}

`type_of`值為`oauth2-google`的密碼需要`credentials`下的下列屬性：

| 認證屬性 | 資料類型 | 說明 |
| --- | --- | --- |
| `scopes` | 陣列 | 列出用於驗證的Google產品範圍。 支援下列範圍：<ul><li>[Google廣告](https://developers.google.com/google-ads/api/docs/oauth/overview)： `https://www.googleapis.com/auth/adwords`</li><li>[Google Pub/Sub](https://cloud.google.com/pubsub/docs/reference/service_apis_overview)： `https://www.googleapis.com/auth/pubsub`</li></ul> |

建立`oauth2-google`密碼之後，回應會包含`meta.authorization_url`屬性。 您必須複製此URL並貼到瀏覽器中，才能完成Google驗證流程。

#### 重新授權`oauth2-google`密碼

`oauth2-google`密碼的授權URL會在密碼建立後一小時到期（如`meta.authorization_url_expires_at`所指示）。 在這之後，必須重新授權密碼才能更新驗證程式。

若要瞭解如何透過向Reactor API發出PATCH要求來重新授權`oauth2-google`密碼，請參閱[密碼端點指南](../endpoints/secrets.md#reauthorize)。

## 環境關係

建立密碼時，您必須指定密碼將存在的[環境](../endpoints/environments.md)。 秘密會立即部署到在其中建立它們的環境。

密碼只能與一個環境相關聯。 一旦秘密和環境之間的關係建立，就不能從環境中清除秘密，也不能將秘密與不同的環境相關聯。

>[!NOTE]
>
>此規則的唯一例外是刪除相關環境時。 在這種情況下，關係會被清除，且密碼可以指派給不同的環境。

成功交換密碼的認證之後，為了將密碼與環境相關聯，交換成品（`token`的權杖字串、`simple-http`的Base64編碼字串或`oauth2-client_credentials`的存取權杖）會安全地儲存在環境上。

成功在環境中儲存Exchange成品後，密碼的`activated_at`屬性會設定為目前的UTC時間，現在可以使用資料元素加以參照。 如需參考密碼的詳細資訊，請參閱[下一節](#referencing-secrets)。

## 引用機密 {#referencing-secrets}

為了參考機密，您必須在事件轉送屬性上建立&quot;[!UICONTROL 機密]&quot; （由[[!UICONTROL 核心]擴充功能](../../extensions/client/core/overview.md)提供）型別的資料元素。 設定此資料元素時，系統會提示您指出每個環境要使用的密碼。 然後，您可以建立參考機密資料元素的規則，例如HTTP呼叫的標頭內。

![機密資料元素](../../images/api/guides/secrets/data-element.png)

>[!NOTE]
>
>若要將機密資料元素新增至程式庫，您必須至少有一個`succeeded`機密與正在建立程式庫的環境相關聯。 例如，如果程式庫的機密資料元素沒有為[!UICONTROL 中繼機密]區段設定`succeeded`機密，則嘗試在中繼環境中建置該程式庫會導致錯誤。

在執行階段，秘密資料元素會由儲存在環境中的對應秘密交換成品取代。

## 後續步驟

本指南說明在Reactor API中處理機密的基礎知識。 如需有關如何使用API呼叫管理密碼的詳細資訊，請參閱[密碼端點指南](../endpoints/secrets.md)。
