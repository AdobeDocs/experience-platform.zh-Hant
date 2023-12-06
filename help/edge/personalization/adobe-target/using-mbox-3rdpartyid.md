---
title: mbox3rdPartyId 的即時設定檔同步
description: 瞭解如何將mbox3rdPartyId與Adobe Experience Platform Web SDK搭配使用。
keywords: 個人化；target；adobe target；renderDecisions；sendEvent；mbox3rdPartyId；
exl-id: 677d1054-0769-4ec6-811e-e02d4b247c2a
source-git-commit: 3bf13c3f5ac0506ac88effc56ff68758deb5f566
workflow-type: tm+mt
source-wordcount: '156'
ht-degree: 5%

---

# 什麼是 `mbox3rdPartyId`

Adobe Target中的mbox3rdPartyId為公司的訪客ID，例如公司忠誠計畫的會員ID。

當訪客登入某個公司的網站時，該公司通常會建立ID，此ID會連結至該訪客的帳戶、熟客卡、會員編號或適用於該公司的其他識別碼。 [了解更多](https://experienceleague.adobe.com/docs/target/using/audiences/visitor-profiles/3rd-party-id.html#)


## 使用方式 `mbox3rdPartyId` 使用Web SDK

### 步驟1：設定 `Target Third Party ID Namespace`

設定 `Target Third Party ID Namespace` 在您的 [資料流](../../../datastreams/overview.md)，使用您想要用作mbox第三方ID的ID名稱空間。
[深入瞭解ID名稱空間](https://experienceleague.adobe.com/docs/experience-platform/identity/namespaces.html?lang=zh-Hant)

![顯示Target第三方ID名稱空間欄位的平台UI。](assets/mbox3rdpartyid.png)

### 步驟2：傳送 `mbox3rdpartyId` 至目標

傳送 `mbox3rdpartyId` 至目標位置 `sendEvent` 命令，使用您在步驟1中設定的ID名稱空間。
[進一步瞭解傳送ID](../../identity/overview.md#syncing-identities)

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
