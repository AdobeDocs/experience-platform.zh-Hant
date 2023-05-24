---
title: 反應堆API中的秘密
description: 瞭解如何在Reactor API中配置機密以便在事件轉發中使用的基礎知識。
exl-id: 0298c0cd-9fba-4b54-86db-5d2d8f9ade54
source-git-commit: 88939d674c0002590939004e0235d3da8b072118
workflow-type: tm+mt
source-wordcount: '1232'
ht-degree: 1%

---

# 反應堆API中的秘密

在Reactor API中，機密是表示驗證憑據的資源。 在事件轉發中使用機密，以驗證到另一個系統以進行安全資料交換。 因此，只能在事件轉發屬性(其屬性 `platform` 屬性設定為 `edge`)。

當前有三種支援的機密類型，如 `type_of` 屬性：

| 密鑰類型 | 說明 |
| --- | --- |
| `token` | 表示兩個系統已知和理解的身份驗證令牌值的單個字串。 |
| `simple-http` | 分別包含用戶名和密碼的兩個字串屬性。 |
| `oauth2-client_credentials` | 包含多個屬性以支援 [OAuth](https://datatracker.ietf.org/doc/html/rfc6749) 驗證規範。 事件轉發要求您獲取所需資訊，然後在指定的時間間隔內為您處理這些令牌的續訂。 |

{style="table-layout:auto"}

本指南提供了如何配置機密以便在事件轉發中使用的高級概述。 有關如何管理Reactor API中的機密（包括機密結構的示例JSON）的詳細指導，請參閱 [機密端點指南](../endpoints/secrets.md)。

## 憑據

每個密碼都包含 `credentials` 保存其相應憑據值的屬性。 當 [在API中建立密鑰](../endpoints/secrets.md#create)，每種類型的機密具有不同的必需屬性，如以下各節所示：

* [`token`](#token)
* [&#39;simple&#39;http&#39;](#simple-http)
* [&#39;oauth2-client_credentials&#39;](#oauth2-client_credentials)
* [&#39;oauth2-google](#oauth2-google)

### `token` {#token}

帶有 `type_of` 值 `token` 只需在 `credentials`:

| 憑據屬性 | 資料類型 | 說明 |
| --- | --- | --- |
| `token` | 字串 | 目標系統理解的秘密令牌。 |

{style="table-layout:auto"}

令牌被儲存為靜態值，因此密鑰 `expires_at` 和 `refresh_at` 屬性設定為 `null` 當機密被建立時。

### `simple-http` {#simple-http}

帶有 `type_of` 值 `simple-http` 需要以下屬性 `credentials`:

| 憑據屬性 | 資料類型 | 說明 |
| --- | --- | --- |
| `username` | 字串 | 用戶名。 |
| `password` | 字串 | 密碼。 API響應中未包括此值。 |

{style="table-layout:auto"}

當建立秘密時，兩個屬性用BASE64編碼交換 `username:password`。 交換後，秘密 `expires_at` 和 `refresh_at` 屬性設定為 `null`。

### `oauth2-client_credentials` {#oauth2-client_credentials}

帶有 `type_of` 值 `oauth2-client_credentials` 需要以下屬性 `credentials`:

| 憑據屬性 | 資料類型 | 說明 |
| --- | --- | --- |
| `client_id` | 字串 | OAuth整合的客戶端ID。 |
| `client_secret` | 字串 | 用於OAuth整合的客戶機密鑰。 API響應中未包括此值。 |
| `token_url` | 字串 | OAuth整合的授權URL。 |
| `refresh_offset` | 整數 | *（可選）* 將刷新操作偏移的值（秒）。 如果建立密鑰時省略此屬性，則值將設定為 `14400` （4小時）。 |
| `options` | 物件 | *（可選）* 指定OAuth整合的其他選項：<ul><li>`scope`:表示 [OAuth 2.0範圍](https://oauth.net/2/scope/) 的雙曲餘切值。</li><li>`audience`:表示 [Auth0訪問令牌](https://auth0.com/docs/protocols/protocol-oauth2)。</li></ul> |

當 `oauth2-client_credentials` 機密已建立或更新， `client_id` 和 `client_secret` (可能 `options`)在POST請求中交換 `token_url`根據OAuth協定的客戶端憑據流。

>[!NOTE]
>
>期望授權服務響應體與OAuth協定相容。

如果授權服務響應 `200 OK` 和JSON響應主體，解析主體 `access_token` 被推到邊緣環境 `expires_in` 用於計算 `expires_at` 和 `refresh_at` 機密的屬性。 如果秘密上沒有環境關聯， `access_token` 被丟棄。

在以下條件下，憑據交換被視為成功：

* `expires_in` 大於 `28800` （8小時）。
* `refresh_offset` 小於的值 `expires_in` 減 `14400` （4小時）。 例如，如果 `expires_in` 是 `36000` （10小時） `refresh_offset` 是 `28800` （8小時），由於 `28800` 大於 `36000` - `14400` (`21600`)。

如果交換成功，則機密的狀態屬性將設定為 `succeeded` 和值 `expires_at` 和 `refresh_at` 設定：

* `expires_at` 是當前UTC時間加值 `expires_in`。
* `refresh_at` 是當前UTC時間加值 `expires_in`，減去的值 `refresh_offset`。 例如，如果 `expires_in` 是 `43200` （十二小時） `refresh_offset` 是 `14400` （四小時） `refresh_at` 屬性將設定為 `28800` （8小時）。

如果交易因任何原因失敗， `status_details` 屬性 `meta` 對象更新時會顯示相關資訊。

#### 刷新 `oauth2-client_credentials` 秘密

如果 `oauth2-client_credentials` 已將機密分配給環境，其狀態為 `succeeded` （已成功交換憑據），將自動在 `refresh_at`。

如果交換成功， `refresh_status` 屬性 `meta` 對象設定為 `succeeded` 同時 `expires_at`。 `refresh_at`, `activated_at` 更新。

如果交換失敗，將再嘗試三次操作，上次嘗試的時間不超過訪問令牌過期前的兩個小時。 如果所有嘗試都失敗， `refresh_status_details` 屬性 `meta` 對象更新及相關詳細資訊。

### `oauth2-google` {#oauth2-google}

帶有 `type_of` 值 `oauth2-google` 需要以下屬性 `credentials`:

| 憑據屬性 | 資料類型 | 說明 |
| --- | --- | --- |
| `scopes` | 陣列 | 列出用於驗證的Google產品作用域。 支援以下作用域：<ul><li>[Google廣告](https://developers.google.com/google-ads/api/docs/oauth/overview): `https://www.googleapis.com/auth/adwords`</li><li>[Google酒吧/小酒店](https://cloud.google.com/pubsub/docs/reference/service_apis_overview): `https://www.googleapis.com/auth/pubsub`</li></ul> |

建立 `oauth2-google` 機密，響應包括 `meta.authorization_url` 屬性。 必須將此URL複製並貼上到瀏覽器中，以完成Google驗證流。

#### 重新授權 `oauth2-google` 秘密

授權URL `oauth2-google` 密鑰在建立密碼後1小時過期(如 `meta.authorization_url_expires_at`)。 此後，必須重新授權該秘密，以便更新身份驗證過程。

請參閱 [機密端點指南](../endpoints/secrets.md#reauthorize) 有關如何重新授權的詳細資訊 `oauth2-google` 向反應器API發出PATCH請求，以保密。

## 環境關係

建立密碼時，必須指定 [環境](../endpoints/environments.md) 它會存在。 機密會立即部署到建立機密的環境中。

機密只能與一個環境關聯。 一旦建立了秘密與環境之間的關係，就無法從環境中清除秘密，並且不能將秘密與其他環境相關聯。

>[!NOTE]
>
>此規則的唯一例外是相關環境是否被刪除。 在這種情況下，關係被清除，機密可以分配給其他環境。

在成功交換機密的憑據後，為了使機密與環境關聯，交換對象(用於 `token`,Base64編碼的字串 `simple-http`，或的訪問令牌 `oauth2-client_credentials`)被安全地保存在環境中。

在環境中成功保存Exchange項目後，機密 `activated_at` 屬性設定為當前UTC時間，現在可以使用資料元素引用。 查看 [下一部分](#referencing-secrets) 的子菜單。

## 引用機密 {#referencing-secrets}

要引用機密，必須建立「」類型的資料元素[!UICONTROL 秘密]」(由 [[!UICONTROL 核心] 擴展](../../extensions/client/core/overview.md))。 配置此資料元素時，系統會提示您指明每個環境使用哪個機密。 然後，可以建立引用機密資料元素的規則，例如在HTTP調用的標頭內。

![機密資料元素](../../images/api/guides/secrets/data-element.png)

>[!NOTE]
>
>要向庫添加機密資料元素，必須至少有一個 `succeeded` 與正在其上構建庫的環境關聯的機密。 例如，如果庫的機密資料元素沒有 `succeeded` 為 [!UICONTROL 暫存密碼] 部分，嘗試在轉移環境中構建該庫將導致錯誤。

在運行時，將秘密資料元素替換為保存在環境上的相應秘密交換對象。

## 後續步驟

本指南介紹了在反應堆API中使用機密的基本原理。 有關如何使用API調用管理機密的詳細資訊，請參閱 [機密端點指南](../endpoints/secrets.md)。
