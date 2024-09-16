---
title: 內容安全性原則(CSP)支援
description: 瞭解將您的網站與Adobe Experience Platform中的標籤整合時，如何處理內容安全性原則(CSP)限制。
exl-id: 9232961e-bc15-47e1-aa6d-3eb9b865ac23
source-git-commit: a8b0282004dd57096dfc63a9adb82ad70d37495d
workflow-type: tm+mt
source-wordcount: '1074'
ht-degree: 58%

---

# 內容安全性原則(CSP)支援

>[!NOTE]
>
>Adobe Experience Platform Launch 已進行品牌重塑，現在是 Adobe Experience Platform 中的一套資料彙集技術。 因此，這些產品文件都推出多項幾術語變更。如需術語變更的彙整參考資料，請參閱以下[文件](../../term-updates.md)。

內容安全性原則 (CSP) 這項安全性功能有助於防止跨網站指令碼攻擊 (XSS)。瀏覽器遭到誘騙而執行似乎是來自信任的來源但其實是來自其他位置的惡意內容時，就會發生這種情況。 CSP 能讓瀏覽器 (代表使用者) 驗證指令碼是否的確來自信任的來源。

CSP 的實作方式為新增 `Content-Security-Policy` HTTP 標頭至您的伺服器回應，或在 HTML 檔案的 `<head>` 區段中新增已設定的 `<meta>` 元素。

>[!NOTE]
>
> 如需 CSP 的詳細資訊，請參閱 [MDN 網頁文件](https://developer.mozilla.org/zh-TW/docs/Web/HTTP/CSP)。

Adobe Experience Platform中的標籤是標籤管理系統，專為動態載入網站指令碼而設計。 預設 CSP 會因潛在安全性問題而封鎖這些動態載入的指令碼。本檔案說明如何設定CSP，以允許從標籤動態載入指令碼。

如果您希望標籤能與CSP搭配使用，有兩個主要難題需要克服：

* **標籤庫的來源必須受信任。**&#x200B;若不符合這項條件，瀏覽器就會封鎖標籤程式庫和其他必要的JavaScript檔案，使其無法在頁面上載入。
* **須允許內嵌指令碼。**&#x200B;若不符合這項條件，頁面會封鎖自訂程式碼動作，使自訂程式碼動作無法正常執行。

提高安全性需要代表內容建立者增加工作量。 如果您希望使用標籤並部署CSP，請解決這兩項問題，並妥善將其他指令碼標示為安全指令碼。 本文件的其餘部分說明如何實現此一目標。

## 將標籤新增為信任的來源

使用 CSP 時，您必須在 `Content-Security-Policy` 標頭的值中加入所有信任的網域。您必須為標籤提供的值會因您使用的託管型別而異。

### 自行託管

如果您是[自行託管](../publishing/hosts/self-hosting-libraries.md)程式庫，組建的來源可能是您自己的網域。您可以使用下列設定，指定主機網域為安全來源：

**HTTP 標頭**

```http
Content-Security-Policy: script-src 'self'
```

**HTML `<meta>` 標籤**

```html
<meta http-equiv="Content-Security-Policy" content="script-src 'self'">
```

### Adobe 管理託管

如果您使用 [Adobe 管理主機](../publishing/hosts/managed-by-adobe-host.md)，則會在 `assets.adobedtm.com` 維護您的組建。您應將`self`指定為安全網域，這樣就不會破壞已載入的任何指令碼，但您也需將`assets.adobedtm.com`列為安全專案，否則頁面不會載入您的標籤庫。 在這種情況下，請使用下列設定：

**HTTP 標頭**

```http
Content-Security-Policy: script-src 'self' assets.adobedtm.com
```

**HTML `<meta>` 標籤**


有一個非常重要的先決條件：您必須非同步載入標籤程式庫[](./asynchronous-deployment.md)。 無法同步載入標籤程式庫（這會導致主控台發生錯誤，且規則無法正確執行）。

```html
<meta http-equiv="Content-Security-Policy" content="script-src 'self' assets.adobedtm.com">
```

您應將 `self` 指定為安全網域，讓已載入的任何指令碼繼續運作，不過您也需將 `assets.adobedtm.com` 列為安全項目，否則頁面不會載入您的程式庫組建。

## 內嵌指令碼

CSP 預設不允許內嵌指令碼，因此必須手動設定以允許。您可透過兩種方法允許內嵌指令碼：

* [透過 Nonce 允許](#nonce) (安全性高)
* [允許所有內嵌指令碼](#unsafe-inline) (最不安全)

>[!NOTE]
>
>CSP規格有第三種方法，也就是使用雜湊的詳細資訊，但這種方法無法用於標籤等標籤管理系統。 如需有關搭配Platform中的標籤使用雜湊的限制的詳細資訊，請參閱[子資源完整性(SRI)指南](./sri.md)。

### 透過Nonce允許 {#nonce}

此方法涉及產生密碼編譯 Nonce，並將其新增至您的 CSP 和網站上的每個內嵌指令碼。瀏覽器收到指示要載入帶有 Nonce 的內嵌指令碼時，會比較 Nonce 值與 CSP 標頭中的值。如果相符，就會載入指令碼。每次載入新頁面時，此 Nonce 的值應該都會不同。

>[!IMPORTANT]
>
>若要使用此方法，您必須以非同步方式載入組建。同步載入組建時，此方法就沒有效，這會導致主控台錯誤和規則無法正確執行。如需詳細資訊，請參閱[非同步部署](./asynchronous-deployment.md)指南。

以下範例示範如何將 Adobe 管理主機的 Nonce 新增至 CSP 設定。如果您使用自行託管，則可排除 `assets.adobedtm.com`。

**HTTP 標頭**

```http
Content-Security-Policy: script-src 'self' assets.adobedtm.com 'nonce-2726c7f26c'
```

**HTML `<meta>` 標籤**

```html
<meta http-equiv="Content-Security-Policy" content="script-src 'self' assets.adobedtm.com 'nonce-2726c7f26c'">
```

設定標頭或HTML標籤後，您必須告訴標籤在載入內嵌指令碼時從何處尋找Nonce。 若要讓標籤在載入指令碼時使用Nonce，您必須：

1. 建立資料元素，以參照 Nonce 在資料層中的位置。
1. 設定核心擴充功能，並指定要使用的資料元素。
1. 發佈您的資料元素和核心擴充功能變更。

>[!NOTE]
>
>以上程序僅處理自訂程式碼載入作業，而不會處理自訂程式碼用途。如果內嵌指令碼包含不符合 CSP 的自訂程式碼，則會以 CSP 優先。例如，如果您使用自訂程式碼，透過將內嵌指令碼附加至DOM來執行載入作業，標籤就無法正確新增Nonce，導致該特定自訂程式碼動作無法正常運作。

### 允許所有內嵌指令碼 {#unsafe-inline}

如果 Nonce 方法不適用，您可以設定 CSP 允許所有內嵌指令碼。這是最不安全但最容易實作及維護的方法。

以下範例示範如何允許 CSP 標頭中的所有內嵌指令碼。

#### 自行託管

如果您使用自行託管，請使用下列設定：

**HTTP 標頭**

```http
Content-Security-Policy: script-src 'self' 'unsafe-inline'
```

**HTML `<meta>` 標籤**

```html
<meta http-equiv="Content-Security-Policy" content="script-src 'self' 'unsafe-inline'">
```

#### Adobe 管理託管

如果您使用 Adobe 管理託管，請使用下列設定：

**HTTP 標頭**

```http
Content-Security-Policy: script-src 'self' assets.adobedtm.com 'unsafe-inline'
```

**HTML `<meta>` 標籤**

```html
<meta http-equiv="Content-Security-Policy" content="script-src 'self' assets.adobedtm.com 'unsafe-inline'">
```

## 後續步驟

閱讀本檔案後，您現在應瞭解如何設定CSP標頭，以接受標籤程式庫檔案和內嵌指令碼。

您也可以選擇使用子資源完整性 (SRI) 當作額外的安全措施，驗證擷取的程式庫組建。不過，此功能與標籤等標籤管理系統搭配使用時有一些重大限制。 如需詳細資訊，請參閱Platform](./sri.md)中[SRI相容性的指南。
