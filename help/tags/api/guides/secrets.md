---
title: Reactor API中的機密
description: 了解如何在Reactor API中設定機密，以用於事件轉送的基本知識。
exl-id: 0298c0cd-9fba-4b54-86db-5d2d8f9ade54
source-git-commit: 24e79c14268b9eab0e8286eb8cd1352c1dfcd1b6
workflow-type: tm+mt
source-wordcount: '1241'
ht-degree: 2%

---

# Reactor API中的機密

在Reactor API中，機密是代表驗證憑證的資源。 在事件轉發中使用機密來驗證到另一個系統以進行安全資料交換。 因此，只能在事件轉發屬性(其 `platform` 屬性設為 `edge`)。

目前有三種支援的機密類型表示於 `type_of` 屬性：

| 密碼類型 | 說明 |
| --- | --- |
| `token` | 一個字串，代表兩個系統都已知和理解的驗證令牌值。 |
| `simple-http` | 包含用戶名和密碼的兩個字串屬性。 |
| `oauth2-client_credentials` | 包含數個要支援的屬性 [OAuth](https://datatracker.ietf.org/doc/html/rfc6749) 驗證規格。 事件轉送會要求您取得所需資訊，然後以指定的間隔為您處理這些代號的續約。 |

{style=&quot;table-layout:auto&quot;}

本指南提供如何設定機密以用於事件轉送的概觀。 如需如何在Reactor API中管理機密的詳細指引，包括機密結構的範例JSON，請參閱 [secrets端點指南](../endpoints/secrets.md).

## 憑證

每個密碼包含 `credentials` 包含其相應憑據值的屬性。 當 [在API中建立機密](../endpoints/secrets.md#create)，每種機密類型都有不同的必要屬性，如下節所示：

* [`token`](#token)
* [&#39;simple-http&#39;](#simple-http)
* [&#39;oauth2-client_credentials&#39;](#oauth2-client_credentials)
* [&#39;oauth2-google&#39;](#oauth2-google)

### `token` {#token}

有 `type_of` 值 `token` 只需要下方的單一屬性 `credentials`:

| 憑據屬性 | 資料類型 | 說明 |
| --- | --- | --- |
| `token` | 字串 | 目的地系統所理解的機密代號。 |

{style=&quot;table-layout:auto&quot;}

代號會儲存為靜態值，因此會儲存機密 `expires_at` 和 `refresh_at` 屬性設為 `null` 密碼建立時。

### `simple-http` {#simple-http}

有 `type_of` 值 `simple-http` 需要下列屬性 `credentials`:

| 憑據屬性 | 資料類型 | 說明 |
| --- | --- | --- |
| `username` | 字串 | 使用者名稱。 |
| `password` | 字串 | 密碼。 API回應中未包含此值。 |

{style=&quot;table-layout:auto&quot;}

建立機密時，兩個屬性會以 `username:password`. 交換後，秘密 `expires_at` 和 `refresh_at` 屬性設為 `null`.

### `oauth2-client_credentials` {#oauth2-client_credentials}

有 `type_of` 值 `oauth2-client_credentials` 需要下列屬性 `credentials`:

| 憑據屬性 | 資料類型 | 說明 |
| --- | --- | --- |
| `client_id` | 字串 | OAuth整合的用戶端ID。 |
| `client_secret` | 字串 | OAuth整合的用戶端密碼。 API回應中未包含此值。 |
| `token_url` | 字串 | OAuth整合的授權URL。 |
| `refresh_offset` | 整數 | *（可選）* 用於偏移刷新操作的值（以秒為單位）。 如果在建立密碼時省略此屬性，則值會設為 `14400` （4小時）。 |
| `options` | 物件 | *（可選）* 指定OAuth整合的其他選項：<ul><li>`scope`:代表 [OAuth 2.0範圍](https://oauth.net/2/scope/) 來取得憑證。</li><li>`audience`:代表 [Auth0存取權杖](https://auth0.com/docs/protocols/protocol-oauth2).</li></ul> |

當 `oauth2-client_credentials` 密碼會建立或更新， `client_id` 和 `client_secret` (可能 `options`)會以POST要求來交換 `token_url`，根據OAuth通訊協定的用戶端認證流程。

>[!NOTE]
>
>預期授權服務響應主體與OAuth協定相容。

如果授權服務用 `200 OK` 和JSON回應內文，會剖析內文並 `access_token` 被推送至邊緣環境，且 `expires_in` 用於計算 `expires_at` 和 `refresh_at` 機密的屬性。 如果秘密上沒有環境關聯， `access_token` 會捨棄。

在以下條件下，認證交換被視為成功：

* `expires_in` 大於 `28800` （八小時）。
* `refresh_offset` 小於的值 `expires_in` 減號 `14400` （4小時）。 例如，若 `expires_in` is `36000` （10小時）, `refresh_offset` is `28800` （八小時），則會將交換視為失敗，因為 `28800` 大於 `36000` - `14400` (`21600`)。

如果交換成功，密碼的狀態屬性會設為 `succeeded` 和值 `expires_at` 和 `refresh_at` 已設定：

* `expires_at` 是目前的UTC時間加上 `expires_in`.
* `refresh_at` 是目前的UTC時間加上 `expires_in`，減去 `refresh_offset`. 例如，若 `expires_in` is `43200` （十二小時） `refresh_offset` is `14400` （4小時）, `refresh_at` 屬性會設為 `28800` （8小時）。

如果交易所因任何原因失敗， `status_details` 屬性 `meta` 物件更新，包含相關資訊。

#### 重新整理 `oauth2-client_credentials` 秘密

若 `oauth2-client_credentials` 已將機密指派給環境，且其狀態為 `succeeded` （已成功交換憑據），則會自動在 `refresh_at`.

如果交換成功，則 `refresh_status` 屬性 `meta` 物件設為 `succeeded` whel `expires_at`, `refresh_at`，和 `activated_at` 會據此更新。

如果交換失敗，則會再嘗試三次，上次嘗試的時間不超過存取權杖過期的兩小時。 如果所有嘗試都失敗， `refresh_status_details` 屬性 `meta` 物件更新，包含相關詳細資訊。

### `oauth2-google` {#oauth2-google}

有 `type_of` 值 `oauth2-google` 需要下列屬性 `credentials`:

| 憑據屬性 | 資料類型 | 說明 |
| --- | --- | --- |
| `scopes` | 陣列 | 列出用於驗證的Google產品範圍。 支援以下範圍：<ul><li>[Google Ads](https://developers.google.com/google-ads/api/docs/oauth/overview): `https://www.googleapis.com/auth/adwords`</li><li>[Google酒吧/小店](https://cloud.google.com/pubsub/docs/reference/service_apis_overview): `https://www.googleapis.com/auth/pubsub`</li></ul> |

建立 `oauth2-google` 機密，回應包含 `meta.authorization_url` 屬性。 您必須將此URL複製並貼到瀏覽器中，才能完成Google驗證流程。

#### 重新授權 `oauth2-google` 秘密

的授權URL `oauth2-google` 機密會在機密建立後一小時過期(如 `meta.authorization_url_expires_at`)。 此後，必須重新授權機密，才能續訂驗證程式。

請參閱 [secrets端點指南](../endpoints/secrets.md#reauthorize) 有關如何重新授權的詳細資訊 `oauth2-google` 向Reactor API提出PATCH要求以加密。

## 環境關係

建立機密時，您必須指定 [環境](../endpoints/environments.md) 它將存在。 系統會將機密立即部署至建立機密的環境。

機密只能與一個環境相關聯。 一旦建立機密與環境的關係，就無法從環境中清除機密，且機密無法與不同環境相關聯。

>[!NOTE]
>
>此規則的唯一例外是相關環境遭刪除。 在這種情況下，會清除關係，並將機密指派給不同的環境。

成功交換機密的憑證後，為了與環境相關聯的機密，交換工件(的代號字串 `token`,Base64編碼的字串 `simple-http`，或 `oauth2-client_credentials`)安全地儲存在環境中。

在環境上成功儲存交換工件後，機密的 `activated_at` 屬性設為目前的UTC時間，現在可使用資料元素參考。 請參閱 [下一節](#referencing-secrets) 以取得參考機密的詳細資訊。

## 引用機密 {#referencing-secrets}

若要參考機密，您必須建立「」類型的資料元素[!UICONTROL 機密]」(由 [[!UICONTROL 核心] 擴充功能](../../extensions/web/core/overview.md))。 設定此資料元素時，系統會提示您指出每個環境要使用的機密。 接著，您就可以建立參考機密資料元素的規則，例如在HTTP呼叫的標題內。

![機密資料元素](../../images/api/guides/secrets/data-element.png)

>[!NOTE]
>
>若要將機密資料元素新增至程式庫，您至少必須有一個 `succeeded` 與建置程式庫所在環境相關聯的機密。 例如，如果程式庫的機密資料元素沒有 `succeeded` 為配置的密碼 [!UICONTROL 測試密碼] 區段中，嘗試在測試環境中建置該程式庫會導致錯誤。

在運行時，將秘密資料元素替換為保存在環境上的相應秘密交換對象。

## 後續步驟

本指南說明在Reactor API中使用機密的基本知識。 如需如何使用API呼叫管理機密的詳細資訊，請參閱 [secrets端點指南](../endpoints/secrets.md).
