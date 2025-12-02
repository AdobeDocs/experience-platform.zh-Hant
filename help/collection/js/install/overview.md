---
title: Web SDK安裝概觀
description: 瞭解如何安裝Experience Platform Web SDK。
keywords: web sdk安裝；安裝web sdk；internet explorer；promise；npm套件
exl-id: b1de7ca1-d0d2-4661-a273-a1acf29afcd5
source-git-commit: a490c429047f5e5997d69f30a51e6b78debe2d5d
workflow-type: tm+mt
source-wordcount: '229'
ht-degree: 0%

---

# Web SDK安裝概觀

使用Adobe Experience Platform Web SDK有三種受支援的方式：

1. **[Web SDK標籤延伸模組](/help/tags/extensions/client/web-sdk/overview.md)**： Adobe建議使用此方法。 在您的網站上安裝標籤載入器，然後使用Adobe Experience Platform資料收集UI來設定您的實施。
1. **[網頁SDK JavaScript程式庫](library.md)**：參考CDN代管的程式庫檔案，或使用您自己的基礎架構代管程式庫檔案。 呼叫網站程式碼中的程式庫。
1. **[NPM](npm.md)**：使用NPM封裝管理員在您的網站上安裝Web SDK。

## 先決條件

使用或安裝Web SDK之前，您必須符合下列要求：

* 必須先設定Adobe Experience Platform中的架構。 這些設定包含任何必要的結構描述、身分和資料串流。
* 您必須設定正確的許可權才能存取適當的工具。 例如，如果您的組織決定使用標籤擴充功能，您必須具備存取資料收集UI的正確許可權。 如需詳細資訊，請參閱[資料彙集許可權](../../permissions.md)。
* 建議使用第一方網域(CNAME)。 如果您已有Adobe Analytics的CNAME，可以使用該名稱。 在開發環境中測試不需要使用CNAME，但Adobe建議在發佈至生產環境之前先使用一個CNAME。 如需詳細資訊，請參閱[第一方裝置識別碼](../../use-cases/identity/first-party-device-ids.md)。
