---
title: Platform Web SDK中的第一方裝置ID
description: 了解如何為Adobe Experience Platform Web SDK設定第一方裝置ID(FPID)。
exl-id: c3b17175-8a57-43c9-b8a0-b874fecca952
source-git-commit: f5270d1d1b9697173bc60d16c94c54d001ae175a
workflow-type: tm+mt
source-wordcount: '1773'
ht-degree: 0%

---

# Platform Web SDK中的第一方裝置ID

Adobe Experience Platform Web SDK指派 [Adobe Experience Cloud ID(ECID)](https://experienceleague.adobe.com/docs/experience-platform/identity/ecid.html?lang=en) 來追蹤使用者行為。 若要說明瀏覽器對Cookie存留期限的限制，您可以選擇設定並管理您自己的裝置識別碼。 這些被稱為第一方裝置 ID (FPID)。 

>[!NOTE]
>
>只有透過Platform Web SDK將資料傳送至Platform邊緣網路時，才支援第一方裝置ID。

本檔案說明如何為您的Platform Web SDK實作設定第一方裝置ID。

## 先決條件

本指南假設您熟悉身分資料在Platform Web SDK中的運作方式，包括ECID和 `identityMap`. 請參閱 [Web SDK中的身分資料](./overview.md) 以取得更多資訊。

## 使用FPID

FPID會透過第一方Cookie來追蹤訪客。 使用採用DNS的伺服器設定第一方Cookie時，最有效率 [記錄](https://datatracker.ietf.org/doc/html/rfc1035) （用於IPv4）或 [AAAA記錄](https://datatracker.ietf.org/doc/html/rfc3596) （適用於IPv6），而非DNS CNAME或JavaScript程式碼。

>[!IMPORTANT]
>
>記錄或AAAA記錄僅支援設定和追蹤Cookie。 資料收集的主要方法是透過DNS CNAME。 換言之，FPID是使用A記錄或AAAA記錄來設定，然後使用CNAME傳送至Adobe。
>
>此 [Adobe管理證書程式](https://experienceleague.adobe.com/docs/core-services/interface/administration/ec-cookies/cookies-first-party.html#adobe-managed-certificate-program) 第一方資料收集仍支援。

設定FPID Cookie後，即可擷取其值，並在收集事件資料時傳送至Adobe。 收集的FPID會作為種子來產生ECID，而ECID仍是Adobe Experience Cloud應用程式中的主要識別碼。

若要將網站訪客的FPID傳送至Platform Edge Network，您必須將FPID包含在 `identityMap` 的訪客。 請參閱本檔案稍後的章節，內容如下： [在 `identityMap`](#identityMap) 以取得更多資訊。

### ID格式需求

Platform Edge Network僅接受符合 [UUIDv4格式](https://datatracker.ietf.org/doc/html/rfc4122). 非UUIDv4格式的裝置ID將遭拒。

產生UUID幾乎一律會產生唯一的隨機ID，發生衝突的機率幾乎可忽略。 UUIDv4無法使用IP位址或任何其他個人識別資訊(PII)設定系統初始值。 UUID隨處可見，而且幾乎每個程式設計語言都能找到程式庫以產生它們。

## 使用您自己的伺服器設定Cookie

使用您擁有的伺服器設定Cookie時，可使用多種方法來防止Cookie因瀏覽器原則而受到限制：

* 使用伺服器端指令碼語言產生Cookie
* 針對向子網域或網站上的其他端點提出的API請求設定Cookie
* 使用CMS產生Cookie
* 使用CDN產生Cookie

>[!IMPORTANT]
>
>使用JavaScript設定的Cookie `document.cookie` 方法幾乎永遠不會受到限制Cookie持續時間的瀏覽器原則的保護。

### Cookie設定時機

最好先設定FPID Cookie，再向邊緣網路提出任何要求。 不過，在無法達成此目的的情況下，系統仍會使用現有方法產生ECID，只要Cookie存在，就會作為主要識別碼。

假設ECID最終受到瀏覽器刪除政策影響，但FPID未受影響，則FPID將成為下次造訪時的主要識別碼，並用於為後續每次造訪的ECID種子。

### 設定Cookie的有效期

設定Cookie的有效期是實作FPID功能時應謹慎考慮的事項。 做出此決定時，您應考量貴組織所在的國家/地區，以及每個地區的法律和政策。

在此決策中，您可能會想要採用公司範圍的Cookie設定政策，或是根據您營運所在地區的使用者而有所不同的政策。

無論您選擇何種設定來延長Cookie的初始有效期，您必須確定包含的邏輯會在每次新造訪網站時延長Cookie的有效期。

## Cookie標幟的影響

有多種Cookie旗標會影響不同瀏覽器對Cookie的處理方式：

* [&#39;HTTPOnly&#39;](#http-only)
* [`Secure`](#secure)
* [`SameSite`](#same-site)

### `HTTPOnly` {#http-only}

使用 `HTTPOnly` 無法使用用戶端指令碼來存取標幟。 這表示，若您將 `HTTPOnly` 標幟時，您必須運用伺服器端指令碼語言來讀取要包含在中的cookie值 `identityMap`.

如果您選擇讓Platform Edge Network讀取FPID Cookie的值，請設定 `HTTPOnly` 標幟可確保任何用戶端指令碼都無法存取值，但不會對平台邊緣網路讀取Cookie的能力造成任何負面影響。

>[!NOTE]
>
>使用 `HTTPOnly` 標幟不會影響可能限制cookie存留期的cookie原則。 不過，在設定及讀取FPID的值時，您仍應考量這一點。

### `Secure` {#secure}

以 `Secure` 屬性只會透過HTTPS通訊協定，以加密的要求傳送至伺服器。 使用此標幟有助於確保中間人攻擊者無法輕鬆存取Cookie的值。 如有可能，設定 `Secure` 標籤。

### `SameSite` {#same-site}

此 `SameSite` 屬性可讓伺服器判斷cookie是否隨跨網站請求傳送。 屬性可提供一些保護，以抵御跨網站偽造攻擊。 存在三個可能的值： `Strict`, `Lax` 和 `None`. 請洽詢您的內部團隊，以判斷哪個設定適合您的組織。

若否 `SameSite` 屬性時，某些瀏覽器的預設設定現在為預設設定 `SameSite=Lax`.

## 在中使用FPID `identityMap` {#identityMap}

以下範例說明如何在 `identityMap`:

```json
{
  "identityMap": {
    "FPID": [
      {
        "id": "123e4567-e89b-42d3-9456-426614174000",
        "authenticatedState": "ambiguous",
        "primary": true
      }
    ]
  }
}
```

如同其他身分類型，您可以在中納入FPID與其他身分 `identityMap`. 以下是已驗證CRM ID隨附的FPID範例：

```json
{
  "identityMap": {
    "FPID": [
      {
        "id": "123e4567-e89b-42d3-9456-426614174000",
        "authenticatedState": "ambiguous",
        "primary": true
      }
    ],
    "EMAIL": [
      {
        "id": "email@mail.com",
        "authenticatedState": "authenticated",
        "primary": true
      }
    ]
  }
}
```

如果第一方資料收集啟用時，邊緣網路所讀取的Cookie中包含FPID，則您應僅擷取已驗證的CRM ID:

```json
{
  "identityMap": {
    "EMAIL": [
      {
        "id": "email@mail.com",
        "authenticatedState": "authenticated",
        "primary": true
      }
    ]
  }
}
```

以下 `identityMap` 會導致邊緣網路發生錯誤回應，因為它缺少 `primary` FPID指示器。 最後， `identityMap` 必須標示為 `primary`.

```json
{
  "identityMap": {
    "FPID": [
      {
        "id": "123e4567-e89b-12d3-a456-426614174000",
        "authenticatedState": "ambiguous"
      }
    ],
    "EMAIL": [
      {
        "id": "email@mail.com",
        "authenticatedState": "authenticated"
      }
    ]
  }
}
```

在此情況下，Experience Edge傳回的錯誤回應會類似下列：

```json
{
    "type": "https://ns.adobe.com/aep/errors/EXEG-0306-400",
    "status": 400,
    "title": "No primary identity set in request (event)",
    "detail": "No primary identity found in the input event. Update the request accordingly to your schema and try again.",
    "report": {
        "requestId": "{REQUEST_ID}",
        "configId": "{CONFIG_ID}",
        "orgId": "{ORG_ID}"
    }
}
```

## ID階層

當ECID和FPID均存在時，系統會將ECID列為識別使用者的優先順序。 這可確保當瀏覽器Cookie存放區中存在現有ECID時，仍會是主要識別碼，而現有的訪客計數不會受到影響。 對於現有使用者，FPID要等到ECID過期或因瀏覽器原則或手動程式而遭到刪除後，才會成為主要身分識別。

身分識別會依下列順序排定優先順序：

1. 包含在 `identityMap`
1. 儲存在Cookie中的ECID
1. 包含於 `identityMap`
1. 儲存在Cookie中的FPID

## 移轉至第一方裝置ID

如果您使用先前實作的FPID移轉至，在低層很難將轉變的外觀視覺化。

為了說明此流程，請考量先前造訪過您網站的客戶所參與的案例，以及FPID移轉對於在Adobe解決方案中識別該客戶的方式有何影響。

![圖表顯示移轉至FPID後，客戶的ID值在兩次造訪之間如何更新](../assets/identity/tracking/visits.png)

| 造訪 | 說明 |
| --- | --- |
| 首次造訪 | 假設您尚未開始設定FPID Cookie。 包含於 [AMCV cookie](https://experienceleague.adobe.com/docs/id-service/using/intro/cookies.html#section-c55af54828dc4cce89f6118655d694c8) 將是用來識別訪客的識別碼。 |
| 第二次造訪 | 開始推出第一方裝置ID解決方案。 現有的ECID仍然存在，且仍是訪客識別的主要識別碼。 |
| 第三次瀏覽 | 在第二次和第三次瀏覽之間，已經過足夠的時間，ECID已因瀏覽器原則而刪除。 但是，由於FPID是使用DNS A記錄設定，因此FPID會持續存在。 FPID現在視為主要ID，用來為寫入使用者裝置的ECID種子。 在Adobe Experience Platform和Experience Cloud解決方案中，使用者現在會被視為新訪客。 |
| 第四次訪問 | 在第三次和第四次瀏覽之間，已經過足夠的時間，ECID已因瀏覽器原則而刪除。 與上次造訪一樣，FPID仍因其設定方式而存在。 這次會產生的ECID與上次造訪相同。 在整個Experience Platform和Experience Cloud解決方案中，使用者會與上次造訪的使用者相同。 |
| 第五次訪問 | 在第四次至第五次瀏覽之間，使用者清除了其瀏覽器中的所有Cookie。 會產生新的FPID，用來為建立新ECID的種子。 在Adobe Experience Platform和Experience Cloud解決方案中，使用者現在會被視為新訪客。 |

{style="table-layout:auto"}

## 常見問題集

以下是關於第一方裝置ID常見問題的解答清單。

### 設定ID種子與直接產生ID有何不同？

種子設定的概念很獨特，因為傳遞至Adobe Experience Cloud的FPID會使用確定性演算法轉換為ECID。 每次傳送相同的FPID至Adobe Experience Platform邊緣網路時，FPID中就會植入相同的ECID。

### 何時應產生第一方裝置ID?

為降低潛在訪客數量膨脹，您應在使用Platform Web SDK提出第一個要求前，先產生FPID。 不過，如果您無法這麼做，系統仍會為該使用者產生ECID，並將作為主要識別碼。 產生的FPID要等到ECID不再存在，才會成為主要識別碼。

### 哪些資料收集方法支援第一方裝置ID?

目前僅Platform Web SDK支援FPID。

### FPID是否儲存在任何平台或Experience Cloud解決方案上？

一旦使用FPID為ECID種子，系統會從 `identityMap` 並取代為已產生的ECID。 FPID不會儲存在任何Adobe Experience Platform或Experience Cloud解決方案中。
