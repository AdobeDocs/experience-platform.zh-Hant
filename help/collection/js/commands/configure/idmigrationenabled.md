---
title: idMigrationEnabled
description: 允許網頁SDK讀取AMCV Cookie。
exl-id: 33b9d645-0fbe-4fe4-8847-e6f9e78557b6
source-git-commit: 2e39a7809049c199d4778a0e17eb9e0f3b1d9775
workflow-type: tm+mt
source-wordcount: '176'
ht-degree: 0%

---

# `idMigrationEnabled`

`idMigrationEnabled`屬性可讓Web SDK讀取先前Adobe Experience Cloud實作所設定的AMCV Cookie。 如果您的組織將實作升級至Web SDK，此設定可讓您更順利轉換至目前的Adobe Experience Cloud ID服務。 此設定十分實用，可讓您在升級至網頁SDK時，不會看到不重複訪客大幅增加。

如果您的組織執行全新的網頁SDK實作，啟用此設定對資料收集或訪客身分識別沒有影響。 讓所有實施都啟用它沒有壞處。

執行`idMigrationEnabled`命令時設定`configure`布林值。 如果您在設定Web SDK時省略此屬性，其預設值為`true`。 如果您想要停用讀取由訪客API設定的AMCV Cookie的功能，請設定此屬性。 大部分的組織不需要設定此屬性。

```js
alloy("configure", {
  datastreamId: "ebebf826-a01f-4458-8cec-ef61de241c93",
  orgId: "ADB3LETTERSANDNUMBERS@AdobeOrg",
  idMigrationEnabled: false
});
```

## 使用網頁SDK標籤擴充功能啟用訪客ID移轉

可以使用[身分組態設定](/help/tags/extensions/client/web-sdk/configure/identity.md)，在Web SDK標籤擴充功能中設定這些設定。
