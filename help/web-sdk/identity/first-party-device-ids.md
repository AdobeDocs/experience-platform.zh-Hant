---
title: Web SDK中的第一方裝置ID
description: 瞭解如何為Adobe Experience Platform Web SDK設定第一方裝置識別碼(FPID)。
exl-id: c3b17175-8a57-43c9-b8a0-b874fecca952
source-git-commit: 9f10d48357b7fb28dc54375a4d077d0a1961a746
workflow-type: tm+mt
source-wordcount: '1990'
ht-degree: 0%

---


# Web SDK中的第一方裝置ID

Adobe Experience Platform Web SDK會使用Cookie將[Adobe Experience Cloud ID (ECID)](https://experienceleague.adobe.com/docs/experience-platform/identity/ecid.html)指派給網站訪客，以追蹤使用者行為。 若要說明瀏覽器對Cookie有效期的限制，您可以選擇設定並管理您自己的裝置識別碼。 這些稱為第一方裝置ID (FPID)。

>[!NOTE]
>
>只有透過Platform Web SDK將資料傳送至PlatformEdge Network時，才能使用第一方裝置ID支援。

>[!IMPORTANT]
>
>第一方裝置識別碼與Web SDK中的[第三方Cookie](../../tags/extensions/client/web-sdk/web-sdk-extension-configuration.md#identity)功能不相容。
>您可以使用第一方裝置識別碼，或使用第三方Cookie，但無法同時使用這兩項功能。

本文介紹如何為Platform Web SDK實作設定第一方裝置ID。

## 先決條件

本指南假設您熟悉身分識別資料在Platform Web SDK中的運作方式，包括ECID和`identityMap`的角色。 如需詳細資訊，請參閱Web SDK](./overview.md)中[身分資料的概觀。

## 使用FPID

FPID會使用第一方Cookie來追蹤訪客。 使用使用DNS [A記錄](https://datatracker.ietf.org/doc/html/rfc1035) （適用於IPv4）或[AAAA記錄](https://datatracker.ietf.org/doc/html/rfc3596) （適用於IPv6）的伺服器(而非DNS CNAME或JavaScript程式碼)設定第一方Cookie時，其最有效。

>[!IMPORTANT]
>
>`A`或`AAAA`記錄僅支援設定和追蹤Cookie。 資料收集的主要方法是透過DNS CNAME。 換言之，FPID是使用A記錄或AAAA記錄設定，然後使用CNAME傳送至Adobe。
>
>[Adobe管理的憑證方案](https://experienceleague.adobe.com/docs/core-services/interface/administration/ec-cookies/cookies-first-party.html#adobe-managed-certificate-program)也仍支援第一方資料收集。

設定FPID Cookie後，就能在收集事件資料時擷取其值並傳送至Adobe。 收集的FPID會作為種子來產生ECID，這繼續是Adobe Experience Cloud應用程式中的主要識別碼。

若要將網站訪客的FPID傳送至PlatformEdge Network，您必須在該訪客的`identityMap`中加入FPID。 如需詳細資訊，請參閱本檔案後面關於[在`identityMap`](#identityMap)中使用FPID的章節。

### ID格式需求

平台Edge Network只接受符合[UUIDv4格式](https://datatracker.ietf.org/doc/html/rfc4122)的ID。 不採用UUIDv4格式的裝置ID將會遭到拒絕。

產生UUID幾乎都會產生不重複的隨機ID，而發生碰撞的機率極小。 UUIDv4不能使用IP位址或任何其他個人識別資訊(PII)進行內建。 UUID隨處可見，而且幾乎每種程式語言都能找到程式庫來產生它們。

## 在資料串流UI中設定第一方ID Cookie {#setting-cookie-datastreams}

您可以在資料串流UI中指定Cookie名稱（可容納[!DNL FPID]），而不需要讀取Cookie值並在身分對應中包含FPID。

>[!IMPORTANT]
>
>此功能需要您啟用[第一方資料收集](https://experienceleague.adobe.com/docs/core-services/interface/administration/ec-cookies/cookies-first-party.html?lang=en)。

如需如何設定資料串流的詳細資訊，請參閱[資料串流檔案](../../datastreams/configure.md)。

設定資料流時，請啟用&#x200B;**[!UICONTROL 第一方ID Cookie]**&#x200B;選項。 此設定可告知Edge Network在查詢第一方裝置識別碼時參考指定的Cookie，而不是在[身分對應](#identityMap)中查詢此值。

請參閱[第一方Cookie](https://experienceleague.adobe.com/docs/core-services/interface/administration/ec-cookies/cookies-first-party.html?lang=zh-Hant)的相關檔案，深入瞭解其如何使用Adobe Experience Cloud。

![顯示資料流設定的平台UI影像，其中強調第一方ID Cookie設定](../assets/first-party-id-datastreams.png)

啟用此設定時，您必須提供預期儲存ID的Cookie名稱。

使用第一方ID時，無法執行第三方ID同步。 協力廠商ID同步依賴於[!DNL Visitor ID]服務以及該服務產生的`UUID`。 使用第一方ID功能時，會產生ECID而不使用[!DNL Visitor ID]服務，因此無法同步第三方ID。

當您使用第一方ID時，由於Audience Manager合作夥伴ID同步主要是以`UUIDs`或`DIDs`為基礎，因此不支援在合作夥伴平台中針對啟用的Audience Manager功能。 從第一方ID衍生的ECID未連結至`UUID`，使其無法定址。

## 使用您自己的伺服器設定Cookie

使用您擁有的伺服器設定Cookie時，可以使用各種方法防止Cookie因瀏覽器原則而受到限制：

* 使用伺服器端指令碼語言產生Cookie
* 設定Cookie以回應對子網域或網站上的其他端點發出的API請求
* 使用CMS產生Cookie
* 使用CDN產生Cookie

>[!IMPORTANT]
>
>使用JavaScript的`document.cookie`方法設定的Cookie，幾乎永遠無法受到限制Cookie持續時間的瀏覽器原則的保護。

### 何時設定Cookie

最好在向Edge Network提出任何請求之前先設定FPID Cookie。 但是，在無法提供的情況下，仍會使用現有方法產生ECID，並在Cookie存在時當作主要識別碼。

假設ECID最終受到瀏覽器刪除原則影響，但FPID未受到影響，則FPID會在下次造訪時成為主要識別碼，並用於在後續每次造訪時設定ECID種子。

### 設定Cookie的有效期

在實作FPID功能時，應謹慎設定Cookie的有效期。 在決定此專案時，您應該考量貴組織營運所在的國家或地區，以及每個地區的法律和政策。

在此決定中，您可能會想要採用全公司的Cookie設定原則，或針對您營運所在地區設定中不同使用者的不同原則。

無論您為Cookie的初始過期時間選取的設定為何，都必須確保加入邏輯，以便在每次發生新的網站造訪時延長Cookie的過期時間。

## Cookie標幟的影響

有各種Cookie標幟會影響Cookie在不同瀏覽器中的處理方式：

* [&#39;HTTPOnly&#39;](#http-only)
* [&#39;安全&#39;](#secure)
* [&#39;SameSite&#39;](#same-site)

### `HTTPOnly` {#http-only}

無法使用使用者端指令碼存取使用`HTTPOnly`標幟設定的Cookie。 這表示如果您在設定FPID時設定`HTTPOnly`旗標，則必須使用伺服器端指令碼語言來讀取要包含在`identityMap`中的Cookie值。

如果您選擇讓PlatformEdge Network讀取FPID Cookie的值，設定`HTTPOnly`旗標可確保任何使用者端指令碼都無法存取該值，但不會對PlatformEdge Network讀取Cookie的能力產生任何負面影響。

>[!NOTE]
>
>使用`HTTPOnly`旗標並不會對可能限制Cookie存留期的Cookie原則造成影響。 不過，在設定和讀取FPID的值時，您仍應考慮這個問題。

### `Secure` {#secure}

以`Secure`屬性設定的Cookie僅會透過HTTPS通訊協定，以加密的要求傳送至伺服器。 使用此標幟有助於確保中間人攻擊者無法輕鬆存取Cookie的值。 可能的話，最好設定`Secure`旗標。

### `SameSite` {#same-site}

`SameSite`屬性可讓伺服器判斷Cookie是否隨跨網站要求傳送。 屬性可針對跨網站偽造攻擊提供某些保護。 存在三個可能的值： `Strict`、`Lax`和`None`。 請洽詢您的內部團隊，判斷適合您組織的設定。

如果未指定`SameSite`屬性，某些瀏覽器的預設設定現在是`SameSite=Lax`。

## 在`identityMap`中使用FPID {#identityMap}

以下是如何在`identityMap`中設定FPID的範例：

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

與其他身分型別一樣，您可以在`identityMap`中包含FPID與其他身分。 以下是已驗證CRM ID所包含的FPID範例：

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

啟用第一方資料收集時，如果FPID包含在Edge Network正在讀取的Cookie中，您應該僅擷取已驗證的CRM ID：

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

下列`identityMap`會導致Edge Network的錯誤回應，因為它遺失FPID的`primary`指標。 在`identityMap`中出現的最後一個ID必須標籤為`primary`。

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

在此情況下，Edge Network傳回的錯誤回應將類似於以下內容：

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

當ECID和FPID同時存在時，ECID會優先識別使用者。 這可確保當瀏覽器Cookie存放區中存在現有的ECID時，仍會是主要識別碼，且現有的訪客計數不會受影響。 對於現有使用者，在ECID過期或因瀏覽器原則或手動程式而被刪除之前，FPID不會成為主要身分。

身分會依下列順序排定優先順序：

1. `identityMap`中包含的ECID
1. ECID儲存在Cookie中
1. `identityMap`中包含的FPID
1. 儲存在Cookie中的FPID

## 移轉至第一方裝置ID

如果您要從先前的實作移轉至FPID，可能很難在低層級視覺化轉換內容。

為了協助說明此流程，請思考先前曾造訪過您網站的客戶的情況，以及FPID移轉對Adobe解決方案中識別該客戶的方式有何影響。

![圖表顯示客戶的ID值在移轉至FPID後如何在造訪之間更新](../assets/identity/tracking/visits.png)

>[!IMPORTANT]
>
>`ECID` Cookie一律優先於`FPID`。

| 造訪 | 說明 |
| --- | --- |
| 首次造訪 | 假設您尚未開始設定FPID Cookie。 [AMCV Cookie](https://experienceleague.adobe.com/docs/id-service/using/intro/cookies.html#section-c55af54828dc4cce89f6118655d694c8)中包含的ECID將是用來識別訪客的識別碼。 |
| 第二次造訪 | 已開始推出第一方裝置ID解決方案。 現有的ECID仍存在，且仍然是訪客身分識別的主要識別碼。 |
| 第三次造訪 | 在第二次和第三次造訪之間，已過了足夠的時間且由於瀏覽器原則已刪除ECID。 但是，由於FPID是使用DNS A記錄設定的，因此FPID會持續存在。 FPID現在會視為主要ID，並用來植入寫入一般使用者裝置的ECID。 在Adobe Experience Platform和Experience Cloud解決方案中，該使用者現在會被視為新訪客。 |
| 第四次瀏覽 | 在第三次和第四次造訪之間，已過了足夠的時間且由於瀏覽器原則已刪除ECID。 如同先前的造訪，FPID會因設定方式而持續存在。 這次會產生與上次造訪相同的ECID。 在整個Experience Platform和Experience Cloud解決方案中，使用者會被視為與上次造訪相同的使用者。 |
| 第五次瀏覽 | 在第四次和第五次造訪之間，使用者已清除其瀏覽器中的所有Cookie。 系統會產生新的FPID，並用來種子建立新的ECID。 在Adobe Experience Platform和Experience Cloud解決方案中，該使用者現在會被視為新訪客。 |

{style="table-layout:auto"}

## 常見問題集

以下是有關第一方裝置ID常見問題的解答清單。

### 植入ID和單純產生ID有何不同？

內建概念的獨特之處在於，傳遞至Adobe Experience Cloud的FPID會使用確定性演演算法轉換為ECID。 每次將相同的FPID傳送至Adobe Experience PlatformEdge Network時，相同的ECID則會從FPID內建而來。

### 何時應該產生第一方裝置識別碼？

若要減少訪客的潛在數量膨脹，應先產生FPID，再使用Web SDK提出第一個請求。 不過，如果您無法這麼做，系統仍會為該使用者產生ECID，並將該ECID當作主要識別碼使用。 產生的FPID不會成為主要識別碼，直到ECID不再存在為止。

### 哪些資料收集方法支援第一方裝置ID？

目前只有Web SDK支援FPID。

### FPID是否儲存在任何平台或Experience Cloud解決方案上？

一旦使用FPID來設定ECID的種子後，就會從`identityMap`中捨棄該FPID，並取代為已產生的ECID。 FPID不會儲存在任何Adobe Experience Platform或Experience Cloud解決方案中。
