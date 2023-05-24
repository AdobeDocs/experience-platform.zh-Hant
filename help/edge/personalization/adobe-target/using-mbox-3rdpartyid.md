---
title: mbox3rdPartyId 的即時設定檔同步
description: 瞭解如何在Adobe Experience PlatformWeb SDK中使用mbox3rdPartyId。
keywords: 個性化；目標；adobe目標；renderDecisions;sendEvent;mbox3rdPartyId;
exl-id: 677d1054-0769-4ec6-811e-e02d4b247c2a
source-git-commit: fb0d8aedbb88aad8ed65592e0b706bd17840406b
workflow-type: tm+mt
source-wordcount: '161'
ht-degree: 9%

---

# 什麼是 `mbox3rdPartyId`

Adobe Target的mbox3rdPartyId是您公司的訪問者ID，例如您公司的會員計畫的會員ID。

當訪問者登錄到公司的站點時，公司通常會建立一個與該公司的訪問者帳戶、會員卡、會員號碼或其他適用標識符相關的ID。 [了解更多](https://experienceleague.adobe.com/docs/target/using/audiences/visitor-profiles/3rd-party-id.html?lang=en#)


## 如何使用 `mbox3rdPartyId` Web SDK

### 步驟1:配置 `Target Third Party ID Namespace`

配置 `Target Third Party ID Namespace` 在 [資料流](../../datastreams/overview.md)，使用要用作mbox第三方ID的ID命名空間。
[瞭解有關ID命名空間的詳細資訊](https://experienceleague.adobe.com/docs/experience-platform/identity/namespaces.html?lang=zh-Hant)

![](assets/mbox3rdpartyid.png)

### 步驟2:發送 `mbox3rdpartyId` 目標

發送 `mbox3rdpartyId` 到 `sendEvent` 命令，使用您在步驟1中配置的ID命名空間。
[瞭解有關發送ID的詳細資訊](../../identity/overview.md#syncing-identities)

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
