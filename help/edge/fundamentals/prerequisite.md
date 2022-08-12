---
title: 使用Adobe Experience PlatformWeb SDK的先決條件
description: 瞭解使用Adobe Experience PlatformWeb SDK的先決條件。
keywords: 第一方域；CNAME；架構；建立模式；啟動；aep web sdk擴展；擴展；配置ID；配置工具；資料元；建立資料元；XDM對象；sendEvent;send Event;
exl-id: 98ae69db-bc87-4ea3-b101-664ac53e7ae0
source-git-commit: 853c0a662592939c280c7e7ede8235d1b6155b2f
workflow-type: tm+mt
source-wordcount: '367'
ht-degree: 0%

---

# 使用Adobe Experience PlatformWeb SDK的先決條件

要使用Adobe Experience PlatformWeb SDK，必須首先：

- 已為您的組織設定此功能。 如果您想獲得訪問權限，請填寫以下內容 [表格](https://adobe.ly/websdkaccess) 而Adobe將為您提供對Datastreams和Adobe Experience Platform（如果需要）的訪問權限。 請注意，Adobe將為您提供必要的訪問權，讓您在SDK中以有限的方式使用，無需額外付費。
- 建議啟用第一方域(CNAME)。 如果你已經有Adobe Analytics的CNAME，你應該用那個。 在開發中進行測試沒有CNAME，但Adobe建議在您投入生產前先使用一個。 雖然CNAME實現在Cookie生存期方面沒有提供任何好處，但它可以阻止某些廣告攔截程式和不太常見的瀏覽器阻止SDK請求。 在這些情況下，使用CNAME可能會防止使用這些工具的用戶中斷資料收集。

>[!IMPORTANT]
>
>**請注意，自11/10/20起，第一方CNAME實施在所有Safari瀏覽器和移動iOS設備上都有7天的期限。**

- 如果您的網站已使用 [Experience CloudID服務](https://experienceleague.adobe.com/docs/experience-platform/edge/identity/overview.html) 在您的網站上(通過訪問者API或Adobe Experience Platform Launch內的Experience CloudID服務擴展)，並且您希望在遷移到Adobe Experience PlatformWeb SDK時繼續使用它，您必須使用訪問者API的最新版本或Experience CloudID服務擴展。 請參閱 [ID遷移](https://experienceleague.adobe.com/docs/experience-platform/edge/identity/overview.html?lang=en#identity) 的子菜單。

## 管理Adobe Experience PlatformWeb SDK的權限

要開始使用Adobe Experience PlatformWeb SDK，您需要配置適當的權限。 要瞭解有關如何設定配置的詳細資訊，請參閱上的文檔 [資料收集權限管理](https://experienceleague.adobe.com/docs/experience-platform/collection/permissions.html?lang=en)。
