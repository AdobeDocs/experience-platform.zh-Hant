---
title: mbox3rdPartyId 的即時設定檔同步
description: 了解如何將mbox3rdPartyId與Adobe Experience Platform Web SDK搭配使用。
keywords: 個人化；目標；adobe target;renderDecisions;sendEvent;mbox3rdPartyId;
exl-id: 677d1054-0769-4ec6-811e-e02d4b247c2a
source-git-commit: fb0d8aedbb88aad8ed65592e0b706bd17840406b
workflow-type: tm+mt
source-wordcount: '161'
ht-degree: 9%

---

# 什麼是 `mbox3rdPartyId`

Adobe Target中的mbox3rdPartyId是您公司的訪客ID，例如您公司忠誠計畫的會員ID。

當訪客登入公司網站時，公司通常會建立ID，此ID會系結至訪客的帳戶、常客卡、會員編號或該公司的其他適用識別碼。 [了解更多](https://experienceleague.adobe.com/docs/target/using/audiences/visitor-profiles/3rd-party-id.html?lang=en#)


## 如何使用 `mbox3rdPartyId` 與Web SDK

### 步驟1:設定 `Target Third Party ID Namespace`

設定 `Target Third Party ID Namespace` 在 [資料流](../../datastreams/overview.md)，使用您要作為mbox第三方ID的ID命名空間。
[深入了解ID命名空間](https://experienceleague.adobe.com/docs/experience-platform/identity/namespaces.html?lang=zh-Hant)

![](assets/mbox3rdpartyid.png)

### 步驟2:傳送 `mbox3rdpartyId` 目標

傳送 `mbox3rdpartyId` 在 `sendEvent` 命令，使用您在步驟1中設定的ID命名空間。
[深入了解傳送ID](../../identity/overview.md#syncing-identities)

```javascript
alloy("sendEvent", {
  xdm: {
    "identityMap": {
      "ID_NAMESPACE": [ // Replace `ID_NAMESPACE` with the namespace you have configured in Step 1.
        {
          "id": "1234",
          "authenticatedState": "authenticated"
        }
      ]
    }
  }
});
```
