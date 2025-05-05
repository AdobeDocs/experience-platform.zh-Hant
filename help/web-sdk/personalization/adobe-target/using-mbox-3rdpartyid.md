---
title: mbox3rdPartyId的即時設定檔同步
description: 瞭解如何搭配Adobe Experience Platform Web SDK使用mbox3rdPartyId。
keywords: 個人化；target；adobe target；renderDecisions；sendEvent；mbox3rdPartyId；
exl-id: 677d1054-0769-4ec6-811e-e02d4b247c2a
source-git-commit: fded2f25f76e396cd49702431fa40e8e4521ebf8
workflow-type: tm+mt
source-wordcount: '157'
ht-degree: 1%

---

# 什麼是`mbox3rdPartyId`

Adobe Target中的mbox3rdPartyId為公司的訪客ID，例如公司忠誠計畫的會員ID。

當訪客登入某個公司的網站時，該公司通常會建立ID，此ID會連結至該訪客的帳戶、熟客卡、會員編號或適用於該公司的其他識別碼。 [了解更多](https://experienceleague.adobe.com/docs/target/using/audiences/visitor-profiles/3rd-party-id.html?lang=zh-Hant#)


## 如何將`mbox3rdPartyId`與Web SDK一起使用

### 步驟1：設定`Target Third Party ID Namespace`

使用您要用作mbox第三方ID的ID名稱空間，在您的[資料流](../../../datastreams/overview.md)中設定`Target Third Party ID Namespace`。
[進一步瞭解ID名稱空間](https://experienceleague.adobe.com/docs/experience-platform/identity/namespaces.html?lang=zh-Hant)

![Experience Platform UI顯示Target協力廠商ID名稱空間欄位。](assets/mbox3rdpartyid.png)

### 步驟2：傳送`mbox3rdpartyId`至Target

使用您在步驟1中設定的ID名稱空間，在`sendEvent`命令中將`mbox3rdpartyId`傳送至Target。
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
