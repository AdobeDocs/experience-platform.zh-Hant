---
title: 在資料收集中使用第一方裝置識別碼
description: 在傳送資料至Edge Network的Web實作中，設定第一方裝置ID (FPID)以提供持久身分。
source-git-commit: 696e5098ebf556bfc0fa4fc22ff637cb0835eee0
workflow-type: tm+mt
source-wordcount: '1905'
ht-degree: 0%

---

# 在資料收集中使用第一方裝置識別碼

Experience Platform Edge Network使用Experience Cloud ID (ECID)來識別網站訪客。 若要改善所擁有屬性的身分識別耐久性，您可以設定和管理您自己的裝置識別碼，稱為第一方裝置ID (FPID)。 Edge Network使用FPID為Adobe解決方案使用的ECID提供種子。

本頁假設您熟悉ECID和`identityMap`。 如需詳細資訊，請參閱資料彙集[中的](./overview.md)身分。

## 何時使用FPID {#when-to-use}

瀏覽器限制可能會縮短Adobe用來識別回訪訪客的Cookie有效期。 如果您需要在組織擁有和控制的網站上擁有更持久的身分識別，FPID可讓您管理自己的裝置識別碼，並使用它作為ECID的種子。

使用Web SDK （包括Web SDK標籤擴充功能）的Web實作支援FPID。 如果您的主要目標是在組織擁有的網域上更強大的身分持續性，或您想要擁有的網頁屬性上更佳的報告和個人化連續性，適合使用外掛程式。 它們也可讓您從控制的基礎架構中設定及管理第一方Cookie。

當您的主要目標是應用程式到網頁的移轉或跨多個網域的身分連續性時，FPID不是合適的工具。 若是這些案例，請參閱[行動裝置對網頁的身分共用](./mobile-to-web.md)和[跨網域共用](./cross-domain-sharing.md)。

使用FPID的好處包括：

* 擁有的屬性具有更強的持續性。
* 進一步控制裝置識別碼的產生和管理方式。
* 分析和個人化的持久基礎。

使用FPID的權衡包括：

* 比依賴預設身分行為更能履行實作責任。
* 跨伺服器端Cookie邏輯和資料收集設定的協調。
* 額外驗證，確認識別碼如預期般使用。

### 高階設定路徑

1. 在您控制的基礎建設上產生並管理第一方裝置識別碼。
1. 設定您的實作，以從[第一方Cookie](#setting-cookie-datastreams)或[身分識別裝載](#identityMap)讀取該ID。
1. 驗證再度訪問的訪客會隨著時間在您擁有的屬性上保持一致的身分。

## FPID的運作方式 {#how-fpids-work}

傳遞至Adobe Experience Cloud的FPID會使用確定性演演算法轉換為ECID。 每次將相同的FPID傳送至Edge Network時，相同的ECID都會從FPID內建。 一旦使用FPID來設定ECID的種子後，就會從`identityMap`中將其捨棄，並取代為產生的ECID。 FPID不會儲存在Adobe Experience Platform或Experience Cloud解決方案中。

當ECID和FPID同時存在時，系統會一律使用ECID來先識別使用者。 此優先順序可確保在瀏覽器Cookie存放區中存在現有ECID時，保留其主要識別碼，且現有訪客計數不會增加風險。 對於現有使用者，在ECID過期或因瀏覽器原則或手動動作而遭到刪除之前，FPID不會成為主要身分。

身分會依下列順序排定優先順序：

1. `identityMap`中包含的ECID
1. ECID儲存在Cookie中
1. `identityMap`中包含的FPID
1. 儲存在Cookie中的FPID

## 產生並設定FPID Cookie {#set-fpid-cookie}

Edge Network只接受符合[UUIDv4格式](https://datatracker.ietf.org/doc/html/rfc4122)的ID。 不採用UUIDv4格式的裝置ID會遭到拒絕。

* UUID是唯一的且隨機的，發生碰撞的機率可以忽略不計。
* UUIDv4不能使用IP位址或任何其他個人識別資訊(PII)進行內建。
* 可用於產生各種UUID的程式庫。

### 伺服器端Cookie設定 {#set-cookie-server}

透過您自己的伺服器設定Cookie時，您可以使用各種方法來協助防止Cookie受到瀏覽器原則的限制：

* 使用伺服器端指令碼語言產生Cookie
* 設定Cookie以回應對子網域或網站上的其他端點發出的API請求
* 使用內容管理系統(CMS)產生Cookie
* 使用內容傳遞網路(CDN)產生Cookie

使用使用DNS [A記錄](https://datatracker.ietf.org/doc/html/rfc1035) （適用於IPv4）或[AAAA記錄](https://datatracker.ietf.org/doc/html/rfc3596) （適用於IPv6）的伺服器（與DNS `CNAME`或JavaScript程式碼相反）設定第一方Cookie時，其最有效。

>[!IMPORTANT]
>
>使用JavaScript的`document.cookie`方法（包括使用標籤方法[`cookie.set()`](../tags/cookie.md)）設定的Cookie，幾乎永遠不會受到限制Cookie持續時間的瀏覽器原則的保護。

請注意，`A`或`AAAA`記錄僅支援設定和追蹤Cookie。 資料收集的主要方法是透過DNS `CNAME`。 使用`A`或`AAAA`記錄設定FPID，並使用`CNAME`傳送至Adobe。 [Adobe-Managed Certificate Program](https://experienceleague.adobe.com/docs/core-services/interface/administration/ec-cookies/cookies-first-party.html#adobe-managed-certificate-program)可讓您設定資料收集的`CNAME`。

### 何時設定Cookie {#when-to-set-cookie}

理想情況下，在傳送資料至Edge Network之前，請先設定FPID Cookie。 如果您的實作在收集資料之前需要同意，請參閱[使用第一方裝置ID的同意](./consent.md#consent-with-fpids)，以取得協調FPID Cookie與您的同意流程的指引。 當您確定FPID可用來從第一個要求為ECID設定種子時，即可減少訪客數量膨脹。 在無法提供的情況下，仍會使用現有方法產生ECID，並在Cookie存在時作為主要識別碼。 產生的FPID不會成為主要識別碼，直到ECID不再存在為止。 假設ECID最終受到瀏覽器刪除原則影響，但FPID未受到影響，則FPID會在下次造訪時成為主要識別碼，並用於在後續每次造訪時設定ECID種子。

### 設定有效期 {#set-expiration}

Adobe建議您仔細考慮FPID Cookie的存留期。 請務必將貴組織的隱私權政策，以及貴組織營運所在國家或地區的法律和政策納入考量。 根據您組織的設定，您可以採用全公司的Cookie設定原則，或根據您營運所在每個地區設定中使用者的不同而採用的原則。 無論初始Cookie過期時間為何，請務必加入每次發生新網站造訪時都會延長過期時間的邏輯。

### Cookie標幟 {#cookie-flags}

有數種Cookie標幟會影響Cookie在不同瀏覽器中的處理方式：

* **`HTTPOnly`**：無法使用使用者端指令碼存取使用`HTTPOnly`旗標設定的Cookie。 這表示如果您在設定FPID時設定`HTTPOnly`旗標，則必須使用伺服器端指令碼語言來讀取要包含在`identityMap`中的Cookie值。 如果您選擇讓Edge Network讀取FPID Cookie的值，設定`HTTPOnly`旗標可確保使用者端指令碼無法存取該值，但不會對Edge Network讀取Cookie的能力造成負面影響。 使用`HTTPOnly`旗標不會影響可以限制Cookie存留期的Cookie原則。 不過，在設定和讀取FPID的值時，您還是要考慮這個問題。
* **`Secure`**：以`Secure`屬性設定的Cookie僅會透過HTTPS通訊協定，以加密的要求傳送至伺服器。 使用此標幟有助於確保中間人攻擊者無法輕鬆存取Cookie值。 可能的話，最好設定`Secure`旗標。
* **`SameSite`**： `SameSite`屬性可讓伺服器判斷Cookie是否隨跨網站要求傳送。 屬性可針對跨網站偽造攻擊提供某些保護。 存在三個可能的值： `Strict`、`Lax`和`None`。 請洽詢您的內部團隊，判斷適合您組織的設定。 如果未指定`SameSite`屬性，則某些瀏覽器的預設設定為`SameSite=Lax`。

## 將FPID傳送至Edge Network {#send-fpid}

您可透過兩種方式將FPID傳送至Edge Network：

* **[方法1](#setting-cookie-datastreams)**：為網頁SDK呼叫設定`CNAME`，並在資料流設定中包含FPID Cookie的名稱。
* **[方法2](#identityMap)**：在身分對應中包含FPID。

### 方法1：設定`CNAME`並在資料流中設定第一方ID Cookie {#setting-cookie-datastreams}

若要從您自己的網域設定FPID Cookie，您必須為網頁SDK呼叫設定您自己的`CNAME`，然後在資料流設定中啟用第一方ID Cookie功能。 DNS中的`CNAME`記錄可讓您建立從某個網域名稱到另一個網域名稱的別名。 此別名可讓第三方服務看起來像是您自己的網域的一部分，讓其Cookie看起來像是第一方Cookie。 當使用`CNAME`啟用第一方資料收集時，您網域的所有Cookie都會在對資料收集端點提出請求時傳送。

1. 使用Adobe建立要在您的組織中用於資料收集的`CNAME`記錄。 如需完整程式，請參閱[Adobe管理的憑證程式](https://experienceleague.adobe.com/en/docs/core-services/interface/data-collection/adobe-managed-cert)。
1. 啟用資料流中的&#x200B;**[!UICONTROL First Party ID Cookie]**&#x200B;選項。 此設定可告知Edge Network在查詢第一方裝置ID時參考指定的Cookie，而不是在身分對應中查詢值。 啟用此設定時，您必須提供預期儲存FPID的Cookie名稱。 如需詳細資訊，請參閱[建立和設定資料串流](/help/datastreams/configure.md#advanced-options)。

   ![顯示資料流設定的平台UI影像，其中強調第一方ID Cookie設定](/help/collection/js/assets/first-party-id-datastreams.png)

### 方法2：在`identityMap`中使用FPID {#identityMap}

除了將FPID儲存在您自己的Cookie中之外，您也可以透過身分對應將FPID傳送至Edge Network。

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

與其他身分型別一樣，您可以在`identityMap`中包含FPID與其他身分。 以下範例包含具有已驗證CRM ID的FPID：

```json
{
  "identityMap": {
    "FPID": [
      {
        "id": "123e4567-e89b-42d3-9456-426614174000",
        "authenticatedState": "ambiguous",
        "primary": false
      }
    ],
    "EMAIL": [
      {
        "id": "user@example.com",
        "authenticatedState": "authenticated",
        "primary": true
      }
    ]
  }
}
```

啟用第一方資料收集時，如果FPID包含在Edge Network正在讀取的Cookie中，請僅擷取已驗證的CRM ID：

```json
{
  "identityMap": {
    "EMAIL": [
      {
        "id": "user@example.com",
        "authenticatedState": "authenticated",
        "primary": true
      }
    ]
  }
}
```

下列`identityMap`導致來自Edge Network的錯誤回應，因為它遺失FPID的`primary`指標。 `identityMap`中至少有一個識別碼必須標示為`primary`。

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
        "id": "user@example.com",
        "authenticatedState": "authenticated"
      }
    ]
  }
}
```

## 移轉至FPID {#migrating-to-fpid}

如果您要從先前的實施移轉至第一方裝置ID，可能很難在低層級視覺化轉換內容。 為了協助說明此程式，請思考先前曾造訪過您網站的客戶案例，以及FPID移轉對Adobe解決方案中識別該客戶的方式有何影響。

![圖表顯示客戶的ID值在移轉至FPID後如何在造訪之間更新](/help/collection/js/assets/identity/tracking/visits.png)

| 造訪 | 說明 |
| --- | --- |
| 首次造訪 | 假設您尚未開始設定FPID Cookie。 [AMCV Cookie](https://experienceleague.adobe.com/docs/id-service/using/intro/cookies.html#section-c55af54828dc4cce89f6118655d694c8)中包含的ECID是用來識別訪客的識別碼。 |
| 第二次造訪 | 已開始推出FPID解決方案。 現有的ECID仍存在，且仍然是訪客身分識別的主要識別碼。 |
| 第三次造訪 | 在第二次和第三次造訪之間，已過了足夠的時間且由於瀏覽器原則已刪除ECID。 但是，由於FPID是使用DNS `A`記錄設定的，所以FPID會持續存在。 FPID現在會視為主要ID，並用來植入寫入一般使用者裝置的ECID。 使用者現在在Adobe Experience Platform和Experience Cloud解決方案中會被視為新訪客。 |
| 第四次瀏覽 | 在第三次和第四次造訪之間，已過了足夠的時間且由於瀏覽器原則已刪除ECID。 如同先前的造訪，FPID會因設定方式而持續存在。 這次會產生與上次造訪相同的ECID。 在整個Adobe Experience Platform和Experience Cloud解決方案中，使用者會被視為與上次造訪相同的使用者。 |
| 第五次瀏覽 | 在第四次和第五次造訪之間，使用者已清除瀏覽器中的所有Cookie。 系統會產生新的FPID，並用來種子建立新的ECID。 使用者現在在Adobe Experience Platform和Experience Cloud解決方案中會被視為新訪客。 |
