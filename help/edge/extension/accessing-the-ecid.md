---
title: 存取ECID
description: 了解如何從資料準備或標籤存取Experience CloudID
exl-id: 8e63a873-d7b5-4c6c-b14d-3c3fbc82b62f
source-git-commit: dee04f2cdeb9057ac10e27a17f9db3f065712618
workflow-type: tm+mt
source-wordcount: '228'
ht-degree: 3%

---


# 存取ECID

此 [!DNL Experience Cloud Identity (ECID)] 是使用者造訪您的網站時，指派給使用者的永久識別碼。 在某些情況下，您可能偏好存取 [!DNL ECID] （例如傳送給第三方）。 另一個使用案例是設定 [!DNL ECID] 除了在「身分對應」中，還會顯示在自訂XDM欄位中。

您可以透過 [資料收集的資料準備](../datastreams/data-prep.md) （建議）或透過標籤。

## 透過資料準備（偏好方法）存取ECID {#accessing-ecid-data-prep}

如果您想在自訂XDM欄位中設定ECID，除了將ECID放在身分對應中，您還可以設定 `source` 至下列路徑：

```js
xdm.identityMap.ECID[0].id
```

然後，將目標設定為欄位類型的XDM路徑 `string`.

![](./assets/access-ecid-data-prep.png)

## 標記

如果您需要存取 [!DNL ECID] 在用戶端上，使用標籤方法，如下所述。

1. 確認屬性已設定 [規則元件排序](../../tags/ui/managing-resources/rules.md#sequencing) 已啟用。
1. 建立新規則。
1. 新增 [!UICONTROL 程式庫已載入] 事件。
1. 新增 [!UICONTROL 自訂條件] 動作至具有下列程式碼的規則(假設您為SDK例項設定的名稱為 `alloy`):

   ```js
    return alloy("getIdentity")
      .then(function(result) {
        _satellite.setVar("ECID", result.identity.ECID);
      });
   ```

1. 儲存規則。

之後，您應該就能存取 [!DNL ECID] 在後續規則中使用 `%ECID%` 或 `_satellite.getVar("ECID")`，就像您會存取任何其他資料元素一樣。
