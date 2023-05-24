---
title: 平台Web SDK中的第一方設備ID
description: 瞭解如何為Adobe Experience PlatformWeb SDK配置第一方設備ID(FPID)。
exl-id: c3b17175-8a57-43c9-b8a0-b874fecca952
source-git-commit: f5270d1d1b9697173bc60d16c94c54d001ae175a
workflow-type: tm+mt
source-wordcount: '1773'
ht-degree: 0%

---

# 平台Web SDK中的第一方設備ID

Adobe Experience PlatformWeb SDK分配 [Adobe Experience CloudID(ECID)](https://experienceleague.adobe.com/docs/experience-platform/identity/ecid.html?lang=en) 通過網站訪問者使用cookie，以跟蹤用戶行為。 要說明Cookie生命週期中的瀏覽器限制，可以選擇設定和管理自己的設備標識符。 這些被稱為第一方裝置 ID (FPID)。 

>[!NOTE]
>
>僅當通過平台Web SDK向平台邊緣網路發送資料時，第一方設備ID支援才可用。

本文檔介紹如何為平台Web SDK實現配置第一方設備ID。

## 先決條件

本指南假定您熟悉Platform Web SDK的標識資料工作方式，包括ECID和 `identityMap`。 請參閱 [Web SDK中的標識資料](./overview.md) 的子菜單。

## 使用FPID

FPID通過使用第一方餅乾跟蹤訪問者。 使用利用DNS的伺服器設定第一方Cookie時最有效 [記錄](https://datatracker.ietf.org/doc/html/rfc1035) （對於IPv4）或 [AAAA記錄](https://datatracker.ietf.org/doc/html/rfc3596) （對於IPv6），而不是DNS CNAME或JavaScript代碼。

>[!IMPORTANT]
>
>只支援記錄或AAAA記錄來設定和跟蹤Cookie。 資料收集的主要方法是通過DNS CNAME。 換句話說，使用A記錄或AAAA記錄來設定FPID，然後使用CNAME來發送到Adobe。
>
>的 [Adobe管理的證書程式](https://experienceleague.adobe.com/docs/core-services/interface/administration/ec-cookies/cookies-first-party.html#adobe-managed-certificate-program) 也支援第一方資料收集。

一旦設定了FPIDcookie，就可以讀取其值，並在收集事件資料時將其發送到Adobe。 收集的FPID用作種子來生成ECID,ECID繼續是Adobe Experience Cloud應用中的主要標識符。

要將網站訪問者的FPID發送到平台邊緣網路，必須在 `identityMap` 為那位訪客準備的。 請參閱本文檔稍後的部分， [在中使用FPID `identityMap`](#identityMap) 的子菜單。

### ID格式要求

平台邊緣網路僅接受符合 [UUIDv4格式](https://datatracker.ietf.org/doc/html/rfc4122)。 將拒絕不採用UUIDv4格式的設備ID。

生成UUID幾乎總會導致唯一的隨機ID，而發生衝突的概率可以忽略。 不能使用IP地址或任何其他個人識別資訊(PII)植入UUIDv4。 UUID無處不在，幾乎每種寫程式語言都可找到庫來生成它們。

## 使用您自己的伺服器設定Cookie

使用您擁有的伺服器設定cookie時，可以使用多種方法來防止由於瀏覽器策略而限制cookie:

* 使用伺服器端指令碼語言生成Cookie
* 設定Cookie以響應對站點上的子域或其他終結點發出的API請求
* 使用CMS生成Cookie
* 使用CDN生成Cookie

>[!IMPORTANT]
>
>使用JavaScript設定的Cookie `document.cookie` 方法幾乎永遠不會受到限制cookie持續時間的瀏覽器策略的保護。

### 何時設定Cookie

最好在向邊緣網路發出任何請求之前設定FPIDcookie。 但是，在不可能生成ECID的情況下，仍使用現有方法生成ECID，只要Cookie存在，它就充當主標識符。

假設ECID最終受到瀏覽器刪除策略的影響，但FPID不受影響，則FPID將在下次訪問時成為主標識符，並用於在每次後續訪問時對ECID進行種子化。

### 設定Cookie的到期日

設定Cookie的過期時間是實施FPID功能時應認真考慮的問題。 在做出此決定時，您應考慮您的組織所在國家或地區，以及這些地區中每個地區的法律和政策。

作為此決定的一部分，您可能希望採用公司範圍的Cookie設定策略，或者根據您操作的每個區域中的用戶的不同而採用不同的策略。

無論您為Cookie的初始到期選擇什麼設定，都必須確保在每次對站點進行新訪問時都包含延長Cookie到期的邏輯。

## Cookie標誌的影響

有多種cookie標誌影響不同瀏覽器對cookie的處理方式：

* [「HTTPOnly」](#http-only)
* [`Secure`](#secure)
* [`SameSite`](#same-site)

### `HTTPOnly` {#http-only}

使用 `HTTPOnly` 無法使用客戶端指令碼訪問標誌。 這意味著如果 `HTTPOnly` 標誌設定FPID時，必須使用伺服器端指令碼語言讀取要包含在 `identityMap`。

如果選擇讓平台邊緣網路讀取FPIDcookie的值，請設定 `HTTPOnly` 標誌將確保任何客戶端指令碼都無法訪問該值，但不會對平台邊緣網路讀取cookie的能力產生任何負面影響。

>[!NOTE]
>
>使用 `HTTPOnly` 標誌對可能限制cookie生存時間的cookie策略沒有影響。 但是，在設定和讀取FPID值時，您仍應考慮這一點。

### `Secure` {#secure}

使用 `Secure` 屬性僅通過HTTPS協定以加密請求發送到伺服器。 使用此標誌可以幫助確保中間人攻擊者無法輕鬆訪問cookie的值。 在可能的情況下，設定 `Secure` 。

### `SameSite` {#same-site}

的 `SameSite` 屬性允許伺服器確定是否隨跨站點請求一起發送cookie。 該屬性提供了一些防止跨站點偽造攻擊的保護。 存在三個可能的值： `Strict`。 `Lax` 和 `None`。 請咨詢您的內部團隊，以確定哪種設定適合您的組織。

否 `SameSite` 屬性已指定，現在某些瀏覽器的預設設定為 `SameSite=Lax`。

## 在中使用FPID `identityMap` {#identityMap}

下面是您如何在 `identityMap`:

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

與其他標識類型一樣，您可以將FPID與其他標識一起包含在 `identityMap`。 以下是已驗證的CRM ID所包含的FPID示例：

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

如果FPID包含在啟用第一方資料收集時邊緣網路正在讀取的cookie中，則您應僅捕獲經過驗證的CRM ID:

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

以下 `identityMap` 將導致邊緣網路錯誤響應，因為 `primary` FPID的指示器。 最後一個ID出現在 `identityMap` 必須標籤為 `primary`。

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

在這種情況下，「體驗邊緣」返回的錯誤響應類似於以下內容：

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

## ID層次結構

當ECID和FPID同時存在時，ECID將被優先化以識別用戶。 這將確保當瀏覽器cookie儲存中存在現有ECID時，它將繼續作為主標識符，並且現有訪問者計數不會受到影響。 對於現有用戶，在ECID過期或由於瀏覽器策略或手動進程而被刪除之前，FPID不會成為主標識。

標識按以下順序排列優先順序：

1. 包含在 `identityMap`
1. 儲存在Cookie中的ECID
1. 包含在 `identityMap`
1. 儲存在Cookie中的FPID

## 遷移到第一方設備ID

如果從以前的實現遷移到使用FPID ，則很難直觀地看到低級別的過渡情況。

為了幫助說明此過程，請考慮以前訪問過您的站點的客戶所參與的情形，以及FPID遷移對在Adobe解決方案中識別該客戶的方式將產生何種影響。

![示出在遷移到FPID後訪問期間如何更新客戶ID值的圖表](../assets/identity/tracking/visits.png)

| 造訪 | 說明 |
| --- | --- |
| 首次訪問 | 假設您尚未開始設定FPIDcookie。 包含在 [AMCV Cookie](https://experienceleague.adobe.com/docs/id-service/using/intro/cookies.html#section-c55af54828dc4cce89f6118655d694c8) 將是用於標識訪問者的標識符。 |
| 第二次訪問 | 已開始部署第一方設備ID解決方案。 現有ECID仍然存在，並繼續是訪問者標識的主要標識符。 |
| 第三次訪問 | 在第二次和第三次訪問之間，已經過足夠的時間，因為瀏覽器策略而刪除了ECID。 但是，由於FPID是使用DNS A記錄設定的，因此FPID仍然存在。 FPID現在被視為主ID，用於對寫入到最終用戶設備的ECID進行種子化。 用戶現在將被視為Adobe Experience Platform和Experience Cloud解決方案的新訪問者。 |
| 第四次訪問 | 在第三次和第四次訪問之間，已經過足夠的時間，因為瀏覽器策略而刪除了ECID。 與上次訪問一樣，FPID的設立方式也使它得以保留。 此時，將生成與上次訪問相同的ECID。 在整個Experience Platform和Experience Cloud解決方案中，用戶與上次訪問的用戶一樣。 |
| 第五次訪問 | 在第四次和第五次訪問之間，最終用戶清除了瀏覽器中的所有Cookie。 生成新FPID，並用於對新ECID的建立進行種子化。 用戶現在將被視為Adobe Experience Platform和Experience Cloud解決方案的新訪問者。 |

{style="table-layout:auto"}

## 常見問題集

以下是有關第一方設備ID的常見問題解答清單。

### 為ID設定種子與僅生成ID有何不同？

種子的概念是獨特的，因為傳遞給Adobe Experience Cloud的FPID是使用確定性算法轉換為ECID的。 每次向Adobe Experience Platform邊緣網路發送相同的FPID時，都會從FPID中植入相同的ECID。

### 何時應生成第一方設備ID?

為降低潛在訪客膨脹，應在使用平台Web SDK發出第一個請求之前生成FPID。 但是，如果您無法執行此操作，則仍將為該用戶生成ECID，並將用作主標識符。 生成的FPID在ECID不再存在之前不會成為主標識符。

### 哪些資料收集方法支援第一方設備ID?

目前只有平台Web SDK支援FPID。

### FPID是否儲存在任何平台或Experience Cloud解決方案中？

一旦FPID用於種子化ECID，它將從 `identityMap` 並替換為已生成的ECID。 FPID不儲存在任何Adobe Experience Platform或Experience Cloud解決方案中。
