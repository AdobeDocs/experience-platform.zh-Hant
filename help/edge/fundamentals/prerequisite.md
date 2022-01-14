---
title: 使用Adobe Experience Platform Web SDK的必要條件
description: 了解使用Adobe Experience Platform Web SDK的必要條件。
keywords: 第一方網域；CNAME；結構；建立結構；launch;aep web sdk擴充功能；擴充功能；組態ID；組態工具；資料元素；建立資料元素；XDM物件；sendEvent；傳送事件；
exl-id: 98ae69db-bc87-4ea3-b101-664ac53e7ae0
source-git-commit: 072e1968fa152454f4df6e88fcf7de5c03494030
workflow-type: tm+mt
source-wordcount: '396'
ht-degree: 2%

---

# 使用Adobe Experience Platform Web SDK的必要條件

若要使用Adobe Experience Platform Web SDK，您必須先：

- 已針對此功能布建您的組織。 如果您想要取得存取權，請填寫下列 [表單](http://adobe.ly/websdkaccess) 和Adobe會為您布建資料流和Adobe Experience Platform（如有需要）的存取權。 請注意，Adobe會為您提供必要的存取權，讓您以有限的方式與SDK搭配使用，不需額外付費。
- 建議啟用第一方網域(CNAME)。 如果您已有Adobe Analytics的CNAME，則應使用該CNAME。 在開發中進行測試沒有CNAME，但Adobe建議您先有CNAME，再投入生產。 雖然CNAME實作不會提供Cookie存留期的任何優點，但可防止特定廣告封鎖程式和較不常見的瀏覽器封鎖SDK請求。 在這些情況下，使用CNAME可能會防止使用這些工具的使用者中斷資料收集作業。

>[!IMPORTANT]
>
>**請注意，自11/10/20起，第一方CNAME實作的所有Safari瀏覽器和行動iOS裝置都有7天的到期日。**

- 如果您的網站已使用 [Experience CloudID服務](https://experienceleague.adobe.com/docs/experience-platform/edge/identity/overview.html) 在您的網站上(透過Adobe Experience Platform Launch中的訪客API或Experience CloudID服務擴充功能)，而且您想在移轉至Adobe Experience Platform Web SDK時繼續使用，則必須使用最新版的訪客API或Experience CloudID服務擴充功能。 請參閱 [ID移轉](https://experienceleague.adobe.com/docs/experience-platform/edge/identity/overview.html?lang=en#identity) 以取得更多資訊。

## 管理Adobe Experience Platform Web SDK的權限

若要開始使用Adobe Experience Platform，您必須擁有 [權限](https://experienceleague.adobe.com/docs/experience-platform/access-control/home.html?lang=zh-Hant) 來建立結構並管理身分。 您可在「資料模型」和「身分」類別中找到所需的最低權限。

![](../images/AEP-permission-categories.png)

在「資料模型」類別中，授予使用者「管理結構描述」和「檢視結構描述」權限。

![](../images/data-modeling-permissions.png)

在Identity Management類別中，授與使用者「管理身分識別命名空間」和「檢視身分識別命名空間」權限。

![](../images/identity-management-permissions.png)
