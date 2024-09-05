---
title: Web SDK中的第一方裝置ID
description: 瞭解如何在Adobe Experience Platform Web SDK中設定第一方裝置識別碼(FPID)。
exl-id: c3b17175-8a57-43c9-b8a0-b874fecca952
source-git-commit: 1cb38e3eaa83f2ad0e7dffef185d5edaf5e6c38c
workflow-type: tm+mt
source-wordcount: '1904'
ht-degree: 0%

---


# Web SDK中的第一方裝置ID

Adobe Experience Platform Web SDK會使用Cookie將[Adobe Experience Cloud ID (ECID)](https://experienceleague.adobe.com/docs/experience-platform/identity/ecid.html)指派給網站訪客，以追蹤使用者行為。 若要說明瀏覽器對Cookie有效期的限制，您可以選擇設定並管理您自己的裝置識別碼。 這些稱為第一方裝置識別碼(`FPIDs`)。

>[!NOTE]
>
>只有在透過Web SDK傳送資料給Experience PlatformEdge Network時，才支援第一方裝置ID。

>[!IMPORTANT]
>
>第一方裝置識別碼與Web SDK中的[第三方Cookie](../../tags/extensions/client/web-sdk/web-sdk-extension-configuration.md#identity)功能不相容。
>您可以使用第一方裝置識別碼，或使用第三方Cookie，但無法同時使用這兩項功能。

本檔案說明如何為Web SDK實作設定第一方裝置ID。

## 先決條件

本指南假設您熟悉身分識別資料在Platform Web SDK中的運作方式，包括ECID和`identityMap`的角色。 如需詳細資訊，請參閱Web SDK](./overview.md)中[身分資料的概觀。

## 使用第一方裝置ID (FPID) {#using-fpid}

第一方裝置ID ([!DNL FPIDs])會使用第一方Cookie來追蹤訪客。 使用使用DNS [A記錄](https://datatracker.ietf.org/doc/html/rfc1035) （適用於IPv4）或[AAAA記錄](https://datatracker.ietf.org/doc/html/rfc3596) （適用於IPv6）的伺服器（而非DNS [!DNL CNAME]或[!DNL JavaScript]程式碼）設定第一方Cookie時，其最有效。

>[!IMPORTANT]
>
>[!DNL A]或[!DNL AAAA]記錄僅支援設定和追蹤Cookie。 資料收集的主要方法是透過[!DNL DNS] [!DNL CNAME]。 換句話說，[!DNL FPIDs]是使用[!DNL A]記錄或[!DNL AAAA]記錄所設定，然後使用[!DNL CNAME]傳送至Adobe。
>
>[Adobe管理的憑證方案](https://experienceleague.adobe.com/docs/core-services/interface/administration/ec-cookies/cookies-first-party.html#adobe-managed-certificate-program)也仍支援第一方資料收集。

設定[!DNL FPID] Cookie後，便可在收集事件資料時擷取其值並傳送至Adobe。 收集的[!DNL FPIDs]會作為產生[!DNL ECIDs]的種子使用，繼續成為Adobe Experience Cloud應用程式中的主要識別碼。

若要將網站訪客的[!DNL FPID]傳送至Edge Network，您必須在該訪客的`identityMap`中加入[!DNL FPID]。 如需詳細資訊，請參閱本檔案中有關[在`identityMap`](#identityMap)中使用FPID的下一節。

### 第一方裝置ID格式需求 {#formatting-requirements}

Edge Network只接受符合[UUIDv4格式](https://datatracker.ietf.org/doc/html/rfc4122)的[!DNL IDs]。 不採用[!DNL UUIDv4]格式的裝置ID將會遭到拒絕。

產生[!DNL UUID]幾乎都會產生唯一的隨機ID，發生衝突的可能性極小。 [!DNL UUIDv4]無法使用IP位址或任何其他個人識別資訊([!DNL PII])作為內建專案。 [!DNL UUIDs]隨處可見，幾乎可以找到每種程式語言產生它們的程式庫。

## 在資料串流UI中設定第一方ID Cookie {#setting-cookie-datastreams}

您可以在資料串流使用者介面中指定Cookie名稱，該介面可容納[!DNL FPID]，而不必讀取Cookie值並在身分對應中包含[!DNL FPID]。

>[!IMPORTANT]
>
>此功能需要您啟用[第一方資料收集](https://experienceleague.adobe.com/docs/core-services/interface/administration/ec-cookies/cookies-first-party.html?lang=en)。

如需如何設定資料串流的詳細資訊，請參閱[資料串流檔案](../../datastreams/configure.md)。

設定資料流時，請啟用&#x200B;**[!UICONTROL 第一方ID Cookie]**&#x200B;選項。 此設定可告知Edge Network在查詢第一方裝置識別碼時參考指定的Cookie，而不是在[身分對應](#identityMap)中查詢此值。

請參閱[第一方Cookie](https://experienceleague.adobe.com/docs/core-services/interface/administration/ec-cookies/cookies-first-party.html?lang=zh-Hant)的相關檔案，深入瞭解其如何使用Adobe Experience Cloud。

![顯示資料流設定的平台UI影像，其中強調第一方ID Cookie設定](../assets/first-party-id-datastreams.png)

啟用此設定時，您必須提供預期儲存ID的Cookie名稱。

使用第一方ID時，無法執行第三方ID同步。 協力廠商ID同步依賴於[!DNL Visitor ID]服務以及該服務產生的`UUID`。 使用第一方ID功能時，會產生[!DNL ECID]而不使用[!DNL Visitor ID]服務，因此無法同步第三方ID。

使用第一方ID時，由於Audience Manager合作夥伴ID同步主要以`UUIDs`或`DIDs`為基礎，因此不支援在合作夥伴平台中針對啟用的[Audience Manager](https://experienceleague.adobe.com/en/docs/audience-manager)功能。 衍生自第一方ID的[!DNL ECID]未連結至`UUID`，使其無法定址。

## 使用您自己的伺服器設定Cookie {#set-cookie-server}

使用您擁有的伺服器設定Cookie時，您可以使用各種方法防止Cookie因瀏覽器原則而受到限制：

* 使用伺服器端指令碼語言產生Cookie
* 設定Cookie以回應對子網域或網站上的其他端點發出的API請求
* 使用[!DNL CMS]產生Cookie
* 使用[!DNL CDN]產生Cookie

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

## 在`identityMap`中使用FPID {#identityMap}

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

## 常見問題集 {#faq}

以下是有關第一方裝置ID常見問題的解答清單。

### 植入ID和單純產生ID有何不同？

內建概念是唯一的，因為傳遞至Adobe Experience Cloud的[!DNL FPID]會使用確定性演演算法轉換為[!DNL ECID]。 每次將相同的[!DNL FPID]傳送至Edge Network時，相同的[!DNL ECID]都是從[!DNL FPID]內建的。

### 何時應該產生第一方裝置識別碼？

若要降低訪客的潛在數量膨脹，應先產生[!DNL FPID]，再使用Web SDK提出您的第一個請求。 不過，如果您無法執行此動作，仍會為該使用者產生[!DNL ECID]，並將作為主要識別碼使用。 產生的[!DNL FPID]不會成為主要識別碼，直到[!DNL ECID]不再存在為止。

### 哪些資料收集方法支援第一方裝置ID？

目前只有Web SDK支援第一方裝置ID。

### 第一方裝置ID是否儲存在任何平台或Experience Cloud解決方案上？

一旦使用[!DNL FPID]來植入[!DNL ECID]，就會從`identityMap`中捨棄該專案，並取代為已產生的[!DNL ECID]。 [!DNL FPID]未儲存在任何Adobe Experience Platform或Experience Cloud解決方案中。
