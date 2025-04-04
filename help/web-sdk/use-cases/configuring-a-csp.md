---
title: 設定CSP
seo-title: Configuring a CSP for Adobe Experience Platform Web SDK
description: 瞭解如何為Experience Platform Web SDK設定CSP
seo-description: Learn how to configure a CSP for the Experience Platform Web SDK
keywords: 設定；設定；SDK；邊緣；Web SDK；設定；內容；Web；裝置；環境；Web SDK設定；內容安全性原則；
exl-id: 661d0001-9e10-479e-84c1-80e58f0e9c0b
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '339'
ht-degree: 0%

---

# 設定CSP

[內容安全性原則](https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers/Content-Security-Policy) (CSP)是用來限制瀏覽器可以使用的資源。 CSP也可限制指令碼和樣式資源的功能。 Adobe Experience Platform Web SDK不需要CSP，但新增此CSP可減少攻擊面，以防止惡意攻擊。

CSP必須反映[!DNL Experience Platform Web SDK]的部署和設定方式。 下列CSP顯示SDK正常運作所需的變更。 視您的特定環境而定，可能需要其他CSP設定。

## 內容安全性原則範例

以下範例說明如何設定CSP。

### 允許存取邊緣網域

```
default-src 'self';
connect-src 'self' EDGE-DOMAIN
```

在上述範例中，`EDGE-DOMAIN`應該取代為第一方網域。 第一方網域是針對[edgeDomain](../commands/configure/edgedomain.md)設定所設定。 若尚未設定第一方網域，則應將`EDGE-DOMAIN`取代為`*.adobedc.net`。 如果使用[idMigrationEnabled](../commands/configure/idmigrationenabled.md)開啟訪客移轉，`connect-src`指示詞也需要包含`*.demdex.net`。

### 使用NONCE允許內嵌指令碼和樣式元素

[!DNL Experience Platform Web SDK]可以修改頁面內容，而且必須核准才能建立內嵌指令碼和樣式標籤。 若要完成此操作，Adobe建議對[default-src](https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers/Content-Security-Policy/default-src) CSP指示詞使用Nonce。 Nonce是伺服器產生的密碼編譯增強隨機權杖，每個唯一頁面檢視產生一次。

```
default-src 'nonce-SERVER-GENERATED-NONCE'
```

此外，需要將CSP Nonce新增為[!DNL Experience Platform Web SDK] [基底程式碼](../install/library.md)指令碼標籤的屬性。 然後，[!DNL Experience Platform Web SDK]會在將內嵌指令碼或樣式標籤新增至頁面時，使用該Nonce：

```
<script nonce="SERVER-GENERATED-NONCE">
  !function(n,o){o.forEach(function(o){n[o]||((n.__alloyNS=n.__alloyNS||
  []).push(o),n[o]=function(){var u=arguments;return new Promise(
  function(i,l){n[o].q.push([i,l,u])})},n[o].q=[])})}
  (window,["alloy"]);
</script>
```

如果未使用Nonce，則另一個選項是將`unsafe-inline`新增到`script-src`和`style-src` CSP指示詞：

```
script-src 'unsafe-inline'
style-src 'unsafe-inline'
```

>[!NOTE]
>
>Adobe會&#x200B;**不**&#x200B;建議指定`unsafe-inline`，因為它允許任何指令碼在頁面上執行，這會限制CSP的優點。

## 設定CSP以供應用程式內傳訊使用 {#in-app-messaging}

當您設定[網頁應用程式內傳訊](../personalization/web-in-app-messaging.md)時，您必須在CSP中包含下列指令：

```
default-src  blob:;
```
