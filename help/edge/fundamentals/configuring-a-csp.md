---
title: 配置CSP
seo-title: 為Adobe Experience Platform Web SDK設定CSP
description: 瞭解如何為Experience Platform Web SDK設定CSP
seo-description: 瞭解如何為Experience Platform Web SDK設定CSP
keywords: 配置；配置；SDK;edge;Web SDK;configure;context;web;device;environment;web sdk設定；內容安全策略；
translation-type: tm+mt
source-git-commit: 4f07d41197add406fbdd82caee5177a1ddaa7d7e
workflow-type: tm+mt
source-wordcount: '354'
ht-degree: 2%

---


# 配置CSP

[內容安全策略](https://developer.mozilla.org/zh-TW/docs/Web/HTTP/Headers/Content-Security-Policy)(CSP)用於限制瀏覽器允許使用的資源。 CSP也可以限制指令碼和樣式資源的功能。 Adobe Experience Platform Web SDK不需要CSP，但加入CSP可降低攻擊面，以防惡意攻擊。

CSP需要反映[!DNL Platform Web SDK]的部署和配置方式。 下列CSP說明SDK正常運作可能需要哪些變更。 視您的特定環境而定，可能需要其他CSP設定。

## 內容安全性原則範例

下列範例說明如何設定CSP。

### 允許存取邊緣網域

```
default-src 'self';
connect-src 'self' EDGE-DOMAIN
```

在上述範例中，`EDGE-DOMAIN`應以第一方網域取代。 第一方域被配置為[edgeDomain](configuring-the-sdk.md#edge-domain)設定。 如果尚未配置第一方域，應將`EDGE-DOMAIN`替換為`*.adobedc.net`。 如果使用[idMigrationEnabled](configuring-the-sdk.md#id-migration-enabled)開啟訪客移轉，則`connect-src`指令也必須包含`*.demdex.net`。

### 使用NONCE允許內嵌指令碼和樣式元素

[!DNL Platform Web SDK] 可修改頁面內容，且必須獲得核准才能建立內嵌指令碼和樣式標籤。為此，Adobe建議對[default-src](https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers/Content-Security-Policy/default-src) CSP指令使用nonce。 nonce是伺服器產生的加密強隨機Token，每個獨特頁面檢視產生一次。

```
default-src 'nonce-SERVER-GENERATED-NONCE'
```

此外，CSP nonce還需要作為屬性添加到[!DNL Platform Web SDK] [基本代碼](installing-the-sdk.md#adding-the-code)指令碼標籤中。 [!DNL Platform Web SDK] 將內嵌指令碼或樣式標籤新增至頁面時，將會使用該nonce:

```
<script nonce="SERVER-GENERATED-NONCE">
  !function(n,o){o.forEach(function(o){n[o]||((n.__alloyNS=n.__alloyNS||
  []).push(o),n[o]=function(){var u=arguments;return new Promise(
  function(i,l){n[o].q.push([i,l,u])})},n[o].q=[])})}
  (window,["alloy"]);
</script>
```

如果未使用nonce，則另一個選項是將`unsafe-inline`添加到`script-src`和`style-src` CSP指令：

```
script-src 'unsafe-inline'
style-src 'unsafe-inline'
```

>[!NOTE]
>
>Adobe建議您&#x200B;**not**&#x200B;指定`unsafe-inline`，因為它允許任何指令碼在頁面上執行，這限制了CSP的優點。
