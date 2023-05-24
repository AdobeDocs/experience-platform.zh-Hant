---
title: 內容安全策略(CSP)支援
description: 瞭解如何在將您的網站與Adobe Experience Platform的標籤整合時處理內容安全策略(CSP)限制。
exl-id: 9232961e-bc15-47e1-aa6d-3eb9b865ac23
source-git-commit: a8b0282004dd57096dfc63a9adb82ad70d37495d
workflow-type: tm+mt
source-wordcount: '1080'
ht-degree: 57%

---

# 內容安全策略(CSP)支援

>[!NOTE]
>
>Adobe Experience Platform Launch已被改名為Adobe Experience Platform的一套資料收集技術。 因此，所有產品文件中出現了幾項術語變更。 如需術語變更的彙整參考資料，請參閱以下[文件](../../term-updates.md)。

內容安全性原則 (CSP) 這項安全性功能有助於防止跨網站指令碼攻擊 (XSS)。當瀏覽器被誘騙運行惡意內容時，就會發生這種情況，這些內容似乎來自受信任的源，但確實來自其他地方。 CSP 能讓瀏覽器 (代表使用者) 驗證指令碼是否的確來自信任的來源。

CSP 的實作方式為新增 `Content-Security-Policy` HTTP 標頭至您的伺服器回應，或在 HTML 檔案的 `<head>` 區段中新增已設定的 `<meta>` 元素。

>[!NOTE]
>
> 如需 CSP 的詳細資訊，請參閱 [MDN 網頁文件](https://developer.mozilla.org/zh-TW/docs/Web/HTTP/CSP)。

Adobe Experience Platform的標籤是一個標籤管理系統，旨在動態載入您網站上的指令碼。 預設 CSP 會因潛在安全性問題而封鎖這些動態載入的指令碼。本文檔提供有關如何配置CSP以允許從標籤動態載入指令碼的指導。

如果希望標籤與CSP配合使用，需要克服兩個主要挑戰：

* **必須信任標籤庫的源。** 如果不滿足此條件，則瀏覽器將阻止標籤庫和其他所需的JavaScript檔案，並且不會在頁面上載入。
* **須允許內嵌指令碼。**&#x200B;若不符合這項條件，頁面會封鎖自訂程式碼動作，使自訂程式碼動作無法正常執行。

提高安全性需要為內容建立者增加工作量。 如果要使用標籤並安裝CSP，則必須解決這兩個問題，而不要錯誤地將其他指令碼標籤為安全。 本文件的其餘部分說明如何實現此一目標。

## 將標籤添加為受信任的源

使用 CSP 時，您必須在 `Content-Security-Policy` 標頭的值中加入所有信任的網域。您必須為標籤提供的值將因所使用的宿主類型而異。

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

如果您使用 [Adobe 管理主機](../publishing/hosts/managed-by-adobe-host.md)，則會在 `assets.adobedtm.com` 維護您的組建。應指定 `self` 作為安全域，這樣您就不會中斷任何已載入的指令碼，但您還需要 `assets.adobedtm.com` 列為安全，否則不會在頁面上載入標籤庫。 在這種情況下，請使用下列設定：

**HTTP 標頭**

```http
Content-Security-Policy: script-src 'self' assets.adobedtm.com
```

**HTML `<meta>` 標籤**


有一個非常重要的先決條件：必須載入標籤庫 [非同步](./asynchronous-deployment.md)。 這不適用於同步載入標籤庫（這會導致控制台錯誤和規則無法正確執行）。

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
>CSP規範提供了第三個使用散列的選項的詳細資訊，但這種方法在標籤管理系統（如標籤）中是不可行的。 有關在平台中使用散列與標籤的限制的詳細資訊，請參見 [子資源完整性(SRI)指南](./sri.md)。

### 透過 Nonce 允許 {#nonce}

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

配置標頭或HTML標籤後，在載入內聯指令碼時必須告訴標籤查找nonce的位置。 要使標籤在載入指令碼時使用nonce，必須：

1. 建立資料元素，以參照 Nonce 在資料層中的位置。
1. 設定核心擴充功能，並指定要使用的資料元素。
1. 發佈您的資料元素和核心擴充功能變更。

>[!NOTE]
>
>以上程序僅處理自訂程式碼載入作業，而不會處理自訂程式碼用途。如果內嵌指令碼包含不符合 CSP 的自訂程式碼，則會以 CSP 優先。例如，如果使用自定義代碼通過將內聯指令碼附加到DOM來載入內聯指令碼，則標籤無法正確添加內聯指令碼，因此特定自定義代碼操作不會按預期方式工作。

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

通過閱讀本文檔，您現在應該瞭解如何配置CSP頭以接受標籤庫檔案和內嵌指令碼。

您也可以選擇使用子資源完整性 (SRI) 當作額外的安全措施，驗證擷取的程式庫組建。但是，此功能在與標籤等標籤管理系統一起使用時有一些主要限制。 請參閱上的指南 [平台中的SRI相容性](./sri.md) 的子菜單。
