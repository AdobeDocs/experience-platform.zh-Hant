---
title: 傳輸層安全性(TLS)資訊
description: 有關使用哪些TLS版本和密碼的資訊
exl-id: 04948cd8-6cf0-4159-a9d3-3130b97af106
source-git-commit: 236c5a11f40490fc7ee536358fb146027fe64545
workflow-type: tm+mt
source-wordcount: '201'
ht-degree: 15%

---

# 傳輸層安全性(TLS)資訊

>[!NOTE]
>
>Adobe Experience Platform Launch 已進行品牌重塑，現在是 Adobe Experience Platform 中的一套資料彙集技術。 因此，這些產品文件都推出多項幾術語變更。如需術語變更的彙整參考資料，請參閱[術語更新](../../term-updates.md)檔案。

傳輸層安全性(TLS)是一種密碼編譯通訊協定，可為透過網際網路在應用程式之間傳送的資料提供端對端安全性。 如需TLS的詳細資訊，請閱讀[TLS基本資訊](https://www.internetsociety.org/deploy360/tls/basics/)檔案。

Adobe Experience Platform中的標籤是標籤管理系統，專為動態載入網站指令碼而設計。 載入指令碼時，TLS會保護Adobe主機`assets.adobedtm.com`與您的網站之間的通訊。

有多種可用的TLS版本，且支援多種不同的加密。 並非所有版本和密碼都與部分版本相同，部分版本會被視為不如其他版本或較不安全。

## 支援的TLS版本和加密

Adobe主機選專案前支援下列TLS版本和加密：

```
PORT    STATE SERVICE
443/tcp open  https
| ssl-enum-ciphers:
|   TLSv1.2:
|     ciphers:
|       TLS_ECDHE_ECDSA_WITH_AES_256_GCM_SHA384 (secp256r1) - A
|       TLS_ECDHE_ECDSA_WITH_AES_128_GCM_SHA256 (secp256r1) - A
|       TLS_ECDHE_ECDSA_WITH_CHACHA20_POLY1305_SHA256 (secp256r1) - A
|       TLS_ECDHE_RSA_WITH_CHACHA20_POLY1305_SHA256 (secp256r1) - A
|       TLS_ECDHE_RSA_WITH_AES_256_GCM_SHA384 (secp256r1) - A
|       TLS_ECDHE_RSA_WITH_AES_128_GCM_SHA256 (secp256r1) - A
|     compressors:
|       NULL
|     cipher preference: server
|   TLSv1.3:
|     ciphers:
|       TLS_AKE_WITH_AES_128_GCM_SHA256 (secp256r1) - A
|       TLS_AKE_WITH_AES_256_GCM_SHA384 (secp256r1) - A
|       TLS_AKE_WITH_CHACHA20_POLY1305_SHA256 (secp256r1) - A
|     cipher preference: client
|_  least strength: A
```

### 自行託管

如果您[自行託管](../publishing/hosts/self-hosting-libraries.md)您的資料庫，則支援的TLS版本將由您自己的託管服務決定。
