---
title: 在Web SDK中使用第一方裝置ID
description: 瞭解如何在Adobe Experience Platform Web SDK中設定第一方裝置識別碼(FPID)。
exl-id: c3b17175-8a57-43c9-b8a0-b874fecca952
source-git-commit: c7be2fff2cd94677b745e6ed095454bc46f8a37b
workflow-type: tm+mt
source-wordcount: '2181'
ht-degree: 0%

---


# 在Web SDK中使用第一方裝置ID

Adobe Experience Platform Web SDK會使用Cookie將[Adobe Experience Cloud ID (ECID)](https://experienceleague.adobe.com/docs/experience-platform/identity/ecid.html)指派給網站訪客，以追蹤使用者行為。 若要解除瀏覽器對Cookie有效期的限制，您可以設定並管理您自己的裝置識別碼，稱為第一方裝置ID (FPID)。

>[!NOTE]
>
>只有透過Web SDK將資料傳送至Experience Platform Edge Network時，才能使用第一方裝置ID支援。

>[!IMPORTANT]
>
>第一方裝置ID與Web SDK中的[第三方Cookie](../../tags/extensions/client/web-sdk/web-sdk-extension-configuration.md#identity)功能不相容。 您可以使用第一方裝置識別碼或第三方Cookie，但不可同時使用兩者。

## 先決條件 {#prerequisites}

開始之前，請確定您已熟悉身分識別資料在Web SDK中的運作方式，包括ECID和`identityMap`。 如需詳細資訊，請參閱網頁SDK](./overview.md)中[身分資料的概觀。

## 第一方裝置ID格式需求 {#formatting-requirements}

Edge Network只接受符合[UUIDv4格式](https://datatracker.ietf.org/doc/html/rfc4122)的ID。 不採用UUIDv4格式的裝置ID將會遭到拒絕。

* [!DNL UUIDs]是唯一的且隨機的，發生衝突的可能性微乎其微。
* [!DNL UUIDv4]無法使用IP位址或任何其他個人識別資訊(PII)進行內建。
* 用於產生[!DNL UUIDs]的程式庫可供各種程式語言使用。

## 使用您自己的伺服器設定[!DNL FPID] Cookie {#set-cookie-server}

透過您自己的伺服器設定Cookie時，您可以使用各種方法防止Cookie因瀏覽器原則而受到限制：

* 使用伺服器端指令碼語言產生Cookie
* 設定Cookie以回應對子網域或網站上的其他端點發出的API請求
* 使用[!DNL CMS]產生Cookie
* 使用[!DNL CDN]產生Cookie

此外，您應該一律在您的網域的`A`記錄下設定FPID Cookie。

>[!IMPORTANT]
>
>使用JavaScript的`document.cookie`方法設定的Cookie，幾乎永遠無法受到限制Cookie持續時間的瀏覽器原則的保護。

### 何時設定Cookie {#when-to-set-cookie}

最好在向Edge Network提出任何請求之前先設定[!DNL FPID] Cookie。 但是，在不可能的情況下，仍會使用現有方法產生[!DNL ECID]，並只要Cookie存在，就當作主要識別碼。

假設[!DNL ECID]最終受到瀏覽器刪除原則影響，但[!DNL FPID]未受到影響，則[!DNL FPID]將成為下次造訪的主要識別碼，並用於在每次後續造訪時設定[!DNL ECID]的種子。

### 設定Cookie的有效期 {#set-expiration}

當您實作[!DNL FPID]功能時，應謹慎設定Cookie的到期日。 在決定此專案時，您應該考量貴組織營運所在的國家或地區，以及每個地區的法律和政策。

在此決定中，您可能會想要採用全公司的Cookie設定原則，或針對您營運所在地區設定中不同使用者的不同原則。

無論您為Cookie的初始過期時間選取的設定為何，都必須確保加入邏輯，以便在每次發生新的網站造訪時延長Cookie的過期時間。

## Cookie標幟的影響 {#cookie-flag-impact}

有各種Cookie標幟會影響Cookie在不同瀏覽器中的處理方式：

* [&#39;HTTPOnly&#39;](#http-only)
* [&#39;安全&#39;](#secure)
* [&#39;SameSite&#39;](#same-site)

### `HTTPOnly` {#http-only}

無法使用使用者端指令碼存取使用`HTTPOnly`標幟設定的Cookie。 這表示如果您在設定[!DNL FPID]時設定`HTTPOnly`旗標，則必須使用伺服器端指令碼語言來讀取要包含在`identityMap`中的Cookie值。

如果您選擇讓Edge Network讀取[!DNL FPID] Cookie的值，設定`HTTPOnly`旗標可確保任何使用者端指令碼都無法存取該值，但不會對Edge Network讀取Cookie的能力產生任何負面影響。

>[!NOTE]
>
>使用`HTTPOnly`旗標並不會對可能限制Cookie存留期的Cookie原則造成影響。 不過，當您設定和讀取[!DNL FPID]的值時，還是應該考慮這個問題。

### `Secure` {#secure}

以`Secure`屬性設定的Cookie只會以加密的要求透過[!DNL HTTPS]通訊協定傳送至伺服器。 使用此標幟有助於確保中間人攻擊者無法輕鬆存取Cookie的值。 可能的話，最好設定`Secure`旗標。

### `SameSite` {#same-site}

`SameSite`屬性可讓伺服器判斷Cookie是否隨跨網站要求傳送。 屬性可針對跨網站偽造攻擊提供某些保護。 存在三個可能的值： `Strict`、`Lax`和`None`。 請洽詢您的內部團隊，判斷適合您組織的設定。

如果未指定`SameSite`屬性，某些瀏覽器的預設設定現在是`SameSite=Lax`。

## ID階層 {#id-hierarchy}

當[!DNL ECID]和[!DNL FPID]同時存在時，[!DNL ECID]會優先識別使用者。 這可確保當瀏覽器Cookie存放區中存在現有的[!DNL ECID]時，仍會是主要識別碼，且現有的訪客計數不會受到影響。 對於現有的使用者，[!DNL FPID]在[!DNL ECID]過期或因瀏覽器原則或手動程式而被刪除之前，不會成為主要身分。

身分會依下列順序排定優先順序：

1. [!DNL ECID]包含在`identityMap`中
1. [!DNL ECID]儲存在Cookie中
1. [!DNL FPID]包含在`identityMap`中
1. [!DNL FPID]儲存在Cookie中


## 移轉至第一方裝置ID {#migrating-to-fpid}

如果您要從先前的實施移轉至第一方裝置ID，可能很難在低層級視覺化轉換內容。

為了協助說明此程式，請思考先前曾造訪過您網站的客戶的案例，以及[!DNL FPID]移轉對Adobe解決方案中識別該客戶的方式有何影響。

![圖表顯示客戶的ID值在移轉至FPID後如何在造訪之間更新](../assets/identity/tracking/visits.png)

>[!IMPORTANT]
>
>`ECID` Cookie一律優先於`FPID`。

| 造訪 | 說明 |
| --- | --- |
| 首次造訪 | 假設您尚未開始設定[!DNL FPID] Cookie。 [AMCV Cookie](https://experienceleague.adobe.com/docs/id-service/using/intro/cookies.html#section-c55af54828dc4cce89f6118655d694c8)中包含的[!DNL ECID]將是用來識別訪客的識別碼。 |
| 第二次造訪 | [!DNL FPID]解決方案的轉出已開始。 現有的[!DNL ECID]仍然存在，並且仍然是訪客識別的主要識別碼。 |
| 第三次造訪 | 在第二次和第三次造訪之間，已經過了足夠的時間且由於瀏覽器原則已刪除[!DNL ECID]。 但是，由於[!DNL FPID]是使用[!DNL DNS] [!DNL A]記錄設定的，因此[!DNL FPID]會持續存在。 [!DNL FPID]現在被視為主要ID，並用來設定寫入一般使用者裝置的[!DNL ECID]的種子。 在Adobe Experience Platform和Experience Cloud解決方案中，該使用者現在會被視為新訪客。 |
| 第四次瀏覽 | 在第三次和第四次造訪之間，已過了足夠的時間因瀏覽器原則而刪除[!DNL ECID]。 和上次造訪一樣，[!DNL FPID]會因設定方式而保留。 這次產生與上次造訪相同的[!DNL ECID]。 在整個Experience Platform和Experience Cloud解決方案中，使用者會被視為與上次造訪相同的使用者。 |
| 第五次瀏覽 | 在第四次和第五次造訪之間，使用者已清除其瀏覽器中的所有Cookie。 已產生新的[!DNL FPID]，並用來設定建立新[!DNL ECID]的種子。 在Adobe Experience Platform和Experience Cloud解決方案中，該使用者現在會被視為新訪客。 |

{style="table-layout:auto"}

## 使用第一方裝置ID (FPID) {#using-fpid}

第一方裝置ID ([!DNL FPIDs])會使用第一方Cookie來追蹤訪客。 使用使用DNS [A記錄](https://datatracker.ietf.org/doc/html/rfc1035) （適用於IPv4）或[AAAA記錄](https://datatracker.ietf.org/doc/html/rfc3596) （適用於IPv6）的伺服器（而非DNS [!DNL CNAME]或[!DNL JavaScript]程式碼）設定第一方Cookie時，其最有效。

>[!IMPORTANT]
>
>[!DNL A]或[!DNL AAAA]記錄僅支援設定和追蹤Cookie。 資料收集的主要方法是透過[!DNL DNS CNAME]。 使用[!DNL A]或[!DNL AAAA]記錄設定[!DNL FPIDs]，並使用[!DNL CNAME]傳送至Adobe。
>
>第一方資料收集也支援[Adobe管理的憑證方案](https://experienceleague.adobe.com/docs/core-services/interface/administration/ec-cookies/cookies-first-party.html#adobe-managed-certificate-program)。

設定[!DNL FPID] Cookie後，便可在收集事件資料時擷取其值並傳送至Adobe。 收集的[!DNL FPIDs]用於產生[!DNL ECIDs]，這是Adobe Experience Cloud應用程式中的主要識別碼。

您可以透過兩種方式使用[!DNL FPIDs]：

* **[方法1](#setting-cookie-datastreams)**：為您的Web SDK呼叫設定[!DNL CNAME]，並在資料流設定中包含[!DNL FPID] Cookie的名稱。
* **[方法2](#identityMap)**：在身分對應中包含[!DNL FPID]。 如需詳細資訊，請參閱本檔案中有關[在`identityMap`](#identityMap)中使用FPID的下一節。

### 方法1：設定網頁SDK呼叫的CNAME，並在資料流中設定第一方ID Cookie {#setting-cookie-datastreams}

若要從您自己的網域設定[!DNL FPID] Cookie，您必須為網頁SDK呼叫設定您自己的[!DNL CNAME] （正式名稱），然後在資料流設定中啟用[!DNL First Party ID Cookie]功能。

**步驟 1.設定Web SDK部署網域**&#x200B;的CNAME

DNS中的[!DNL CNAME]記錄可讓您建立從某個網域名稱到另一個網域名稱的別名。 這可讓第三方服務看起來像是您自己的網域的一部分，因此其Cookie看起來像是第一方Cookie。

**範例**

假設您要在網站`mywebsite.com`上實作Web SDK。 網頁SDK會將資料傳送至Edge Network至`edge.adobedc.net`網域。

| 不含[!DNL CNAME] | 與[!DNL CNAME] |
|---------|----------|
| <ul><li>您的網站`mywebsite.com`使用Web SDK網域`edge.adobedc.net`傳送資料給Edge Network。</li><li>由`edge.adobedc.net`設定的Cookie被視為協力廠商Cookie，因為它們並非來自您的`mywebsite.com`網域。 根據您的使用者瀏覽器，第三方Cookie可能會遭到封鎖，且您的資料無法送達Edge Network。</li></ul> | <ul><li>您建立部署Web SDK的子網域，例如`metrics.mywebsite.com`。</li><li>您在DNS系統中設定[!DNL CNAME]記錄，使`metrics.mywebsite.com`指向`edge.adobedc.net`。</li><li>當您的網站透過`metrics.mywebsite.com`設定Cookie時，在瀏覽器中，它們將顯示為來自`mywebsite.com` （第一方）而非`edge.adobedc.net` （第三方）。 這能降低第一方ID Cookie遭到封鎖的可能性，確保資料收集作業更加準確。</li></ul> |

使用[!DNL CNAME]啟用第一方資料收集時，將會在對資料收集端點提出請求時傳送您網域的所有Cookie。

若要使用此功能，您必須將[!DNL FPID] Cookie設定在您網域的頂層，而非特定子網域。 如果您在子網域上設定它，Cookie值將不會傳送至Edge Network，且[!DNL FPID]解決方案將無法如預期運作。

>[!IMPORTANT]
>
>此功能需要您啟用[第一方資料收集](https://experienceleague.adobe.com/docs/core-services/interface/administration/ec-cookies/cookies-first-party.html?lang=en)。

**步驟 2.為您的資料流啟用**[!UICONTROL &#x200B;第一方ID Cookie ]**功能**

設定CNAME之後，您必須為資料流啟用&#x200B;**[!UICONTROL 第一方ID Cookie]**&#x200B;選項。 此設定可告知Edge Network在查詢第一方裝置ID時參考指定的Cookie，而不是在[身分對應](#identityMap)中查詢此值。

請參閱[資料流設定檔案](../../datastreams/configure.md#advanced-options)以瞭解如何設定資料流。

請參閱[第一方Cookie](https://experienceleague.adobe.com/docs/core-services/interface/administration/ec-cookies/cookies-first-party.html?lang=zh-Hant)的相關檔案，深入瞭解其如何使用Adobe Experience Cloud。

![顯示資料流設定的平台UI影像，其中強調第一方ID Cookie設定](../assets/first-party-id-datastreams.png)

啟用此設定時，您必須提供預期儲存[!DNL FPID]的Cookie名稱。

>[!NOTE]
>
>使用第一方ID時，無法執行第三方ID同步。 協力廠商ID同步依賴於[!DNL Visitor ID]服務以及該服務產生的`UUID`。 使用第一方ID功能時，會產生[!DNL ECID]而不使用[!DNL Visitor ID]服務，因此無法同步第三方ID。
><br> 使用第一方ID時，由於Audience Manager合作夥伴ID同步主要是以`UUIDs`或`DIDs`為基礎，因此不支援在合作夥伴平台中啟用的[Audience Manager](https://experienceleague.adobe.com/en/docs/audience-manager)功能。 衍生自第一方ID的[!DNL ECID]未連結至`UUID`，使其無法定址。

## 方法2：在`identityMap`中使用FPID {#identityMap}

除了將[!DNL FPID]儲存在您自己的Cookie中之外，您也可以透過身分對應將[!DNL FPID]傳送至Edge Network。

以下是如何在`identityMap`中設定[!DNL FPID]的範例：

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

與其他身分型別一樣，您可以在`identityMap`中包含[!DNL FPID]與其他身分。 以下是已驗證[!DNL CRM ID]所包含的[!DNL FPID]範例：

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
        "id": "email@mail.com",
        "authenticatedState": "authenticated",
        "primary": true
      }
    ]
  }
}
```

如果[!DNL FPID]包含在啟用第一方資料收集時Edge Network正在讀取的Cookie中，您應該僅擷取已驗證的[!DNL CRM ID]：

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

下列`identityMap`會導致Edge Network的錯誤回應，因為它遺失[!DNL FPID]的`primary`指標。 在`identityMap`中出現的最後一個ID必須標籤為`primary`。

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

## 常見問題集 {#faq}

以下是有關第一方裝置ID常見問題的解答清單。

### 植入ID和單純產生ID有何不同？

內建概念是唯一的，因為傳遞至Adobe Experience Cloud的[!DNL FPID]會使用確定性演演算法轉換為[!DNL ECID]。 每次將相同的[!DNL FPID]傳送至Edge Network時，相同的[!DNL ECID]都是從[!DNL FPID]內建的。

### 何時應該產生第一方裝置識別碼？

若要降低訪客可能的膨脹率，應先產生[!DNL FPID]，再使用網頁SDK提出您的第一個要求。 不過，如果您無法執行此動作，仍會為該使用者產生[!DNL ECID]，並將作為主要識別碼使用。 產生的[!DNL FPID]不會成為主要識別碼，直到[!DNL ECID]不再存在為止。

### 哪些資料收集方法支援第一方裝置ID？

目前只有Web SDK支援第一方裝置ID。

### 第一方裝置ID是否儲存在任何Platform或Experience Cloud解決方案上？

一旦使用[!DNL FPID]來植入[!DNL ECID]，就會從`identityMap`中捨棄該專案，並取代為已產生的[!DNL ECID]。 [!DNL FPID]未儲存在任何Adobe Experience Platform或Experience Cloud解決方案中。
