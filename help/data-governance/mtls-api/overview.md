---
title: MTLS API指南
description: 瞭解如何使用mTLS服務API來安全地擷取及驗證Adobe所發行的公開憑證。
role: Developer
source-git-commit: f805d03ff2cd3a4f84ca8068023d83986f8bdfbb
workflow-type: tm+mt
source-wordcount: '196'
ht-degree: 1%

---

# MTLS服務API總覽

使用MTLS服務API可安全地擷取Adobe為您的組織應用程式發行的公開憑證。 此API可確保客戶與Adobe Experience Platform之間的資料交換通過驗證並加密，提供額外的安全層。 透過從外部驗證憑證的真實性，您可以增強信任度並保護敏感資訊。

## 公開憑證

公開憑證是在安全通訊中用來驗證伺服器或使用者端身分的數位檔案。 在mTLS服務API的上下文中，這些憑證可確保與Adobe Experience Platform的資料交換經過驗證和加密。 透過API擷取及驗證這些憑證可確認其真實性、增強資料交易的安全性和可信度並保護敏感資訊。 若要瞭解如何擷取您的公開憑證，請參閱[端點指南](./public-certificate-endpoint.md)以瞭解如何進行呼叫。

## 後續步驟

若要開始使用MTLS服務API進行呼叫，請閱讀[快速入門手冊](./getting-started.md)，以取得必要標頭的重要資訊、讀取範例API呼叫等等。
