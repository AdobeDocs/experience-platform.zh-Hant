---
title: Web SDK安裝概述
description: 瞭解如何安裝Experience PlatformWeb SDK。
keywords: web sdk安裝；安裝web sdk；internet explorer；promise；npm套件
exl-id: b1de7ca1-d0d2-4661-a273-a1acf29afcd5
source-git-commit: f75dcfc945be2f45c1638bdd4d670288aef6e1e6
workflow-type: tm+mt
source-wordcount: '231'
ht-degree: 0%

---

# Web SDK安裝概述

使用Adobe Experience Platform Web SDK有三種支援的方法：

1. **[Web SDK標籤擴充功能](extension.md)**：Adobe建議使用此方法。 在您的網站上安裝標籤載入器，然後使用Adobe Experience Platform資料收集UI來設定您的實施。
1. **[Web SDK JavaScript程式庫](library.md)**：參考CDN託管的程式庫檔案，或使用您自己的基礎架構託管程式庫檔案。 呼叫網站程式碼中的程式庫。
1. **[npm](npm.md)**：使用NPM套件管理器在您的網站上安裝Web SDK。

## 先決條件

使用或安裝Web SDK前，您必須符合下列要求：

* 必須先設定Adobe Experience Platform中的架構。 這些設定包含任何必要的結構描述、身分和資料串流。
* 您必須設定正確的許可權才能存取適當的工具。 例如，如果您的組織決定使用標籤擴充功能，您必須具備存取資料收集UI的正確許可權。 另請參閱 [資料彙集許可權管理](https://experienceleague.adobe.com/docs/experience-platform/collection/permissions.html) 以取得詳細資訊。
* 建議使用第一方網域(CNAME)。 如果您已有Adobe Analytics的CNAME，可以使用該名稱。 在開發環境中測試不需要使用CNAME，但Adobe建議在發佈至生產環境之前先使用一個。 另請參閱 [第一方裝置ID](../identity/first-party-device-ids.md) 以取得詳細資訊。
