---
title: 配置CSP
seo-title: Configuring a CSP for Adobe Experience Platform Web SDK
description: 瞭解如何為Experience PlatformWeb SDK配置CSP
seo-description: Learn how to configure a CSP for the Experience Platform Web SDK
keywords: 配置；配置；SDK；邊；Web SDK；配置；上下文；Web；設備；環境；Web sdk設定；內容安全策略；
exl-id: 661d0001-9e10-479e-84c1-80e58f0e9c0b
source-git-commit: 0085306a2f5172eb19590cc12bc9645278bd2b42
workflow-type: tm+mt
source-wordcount: '333'
ht-degree: 2%

---

# 配置CSP

A [內容安全策略](https://developer.mozilla.org/zh-TW/docs/Web/HTTP/Headers/Content-Security-Policy) (CSP)用於限制瀏覽器允許使用的資源。 CSP還可以限制指令碼和樣式資源的功能。 Adobe Experience PlatformWeb SDK不需要CSP，但添加一個CSP可以減少攻擊面，防止惡意攻擊。

CSP需要反映 [!DNL Platform Web SDK] 已部署和配置。 以下CSP顯示SDK正常運行可能需要哪些更改。 可能需要其他CSP設定，具體取決於您的具體環境。

## 內容安全策略示例

以下示例說明如何配置CSP。

### 允許訪問邊緣域

```
default-src 'self';
connect-src 'self' EDGE-DOMAIN
```

在上例中， `EDGE-DOMAIN` 應替換為第一方域。 為 [邊緣域](configuring-the-sdk.md#edge-domain) 的子菜單。 如果尚未配置第一方域， `EDGE-DOMAIN` 應替換為 `*.adobedc.net`。 如果啟用訪問者遷移，請使用 [idMigrationEnabled](configuring-the-sdk.md#id-migration-enabled)，也請參見Wiki頁。 `connect-src` 指令還需要包括 `*.demdex.net`。

### 使用NONCE允許內聯指令碼和樣式元素

[!DNL Platform Web SDK] 可以修改頁面內容，並且必須獲得批准才能建立內聯指令碼和樣式標籤。 為了實現此目的，Adobe建議使用 [預設](https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers/Content-Security-Policy/default-src) CSP指令。 nonce是伺服器生成的加密強隨機令牌，每個唯一頁面視圖生成一次。

```
default-src 'nonce-SERVER-GENERATED-NONCE'
```

此外，CSP nonce需要作為屬性添加到 [!DNL Platform Web SDK] [基本代碼](installing-the-sdk.md#adding-the-code) 指令碼標籤。 [!DNL Platform Web SDK] 然後將內嵌指令碼或樣式標籤添加到頁面時，將不會使用此選項：

```
<script nonce="SERVER-GENERATED-NONCE">
  !function(n,o){o.forEach(function(o){n[o]||((n.__alloyNS=n.__alloyNS||
  []).push(o),n[o]=function(){var u=arguments;return new Promise(
  function(i,l){n[o].q.push([i,l,u])})},n[o].q=[])})}
  (window,["alloy"]);
</script>
```

如果未使用nonce，則另一個選項是添加 `unsafe-inline` 到 `script-src` 和 `style-src` CSP指令：

```
script-src 'unsafe-inline'
style-src 'unsafe-inline'
```

>[!NOTE]
>
>Adobe **不** 建議指定 `unsafe-inline` 因為它允許任何指令碼在頁面上運行，這限制了CSP的優勢。
