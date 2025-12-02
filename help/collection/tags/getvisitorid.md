---
title: getVisitorId
description: 擷取Experience Cloud訪客ID服務標籤擴充功能例項。
source-git-commit: 434d6913ea391b127b4b52c8494730c496bbcfe2
workflow-type: tm+mt
source-wordcount: '194'
ht-degree: 0%

---

# `getVisitorId()`

`_satellite.getVisitorId()`方法會在您的標籤屬性[if](https://experienceleague.adobe.com/en/docs/id-service/using/home)中，傳回&#x200B;**Adobe Experience Cloud ID服務**&#x200B;的執行個體（您已安裝並發佈ID服務擴充功能）。 如果您想要直接存取訪客ID例項，以用於自訂程式碼區塊、進階資料元素設定或疑難排解訪客身分問題，此方法將有所幫助。

>[!IMPORTANT]
>
>此方法僅適用於包含獨立Experience Cloud ID服務標籤擴充功能的屬性。 不適用於網頁SDK標籤擴充功能中可用的隱含ID服務功能。 如果您需要使用Web SDK的隱含ID服務功能取得訪客身分識別，請參閱[`getIdentity`](/help/collection/js/commands/getidentity.md)命令。

如果您在已安裝並發佈ID服務擴充功能的情況下呼叫此方法，則會傳回與呼叫[`Visitor.getInstance()`](https://experienceleague.adobe.com/en/docs/id-service/using/id-service-api/methods/getinstance)方法後所取得物件類似的物件。 如果您在未安裝或未發佈ID服務擴充功能時呼叫此方法，則方法會傳回`null`。

```ts
_satellite.getVisitorId(): Visitor | null
```

## 可用的欄位和方法

請參閱Experience Cloud訪客ID服務檔案中的Experience Cloud ID服務[方法](https://experienceleague.adobe.com/en/docs/id-service/using/id-service-api/methods/get-set)，瞭解您可以使用哪些欄位和方法。

```js
// Retrieve a visitor's ECID
_satellite.getVisitorId().getMarketingCloudVisitorID();

// Retrieve a visitor's legacy Analytics ID
_satellite.getVisitorId().getAnalyticsVisitorID();

// Retrieve a visitor's Audience Manager blob for audience sharing
_satellite.getVisitorId().getAudienceManagerBlob();
```
