---
title: 存取ECID
description: 瞭解如何從「資料準備」或「標籤」存取Experience CloudID
exl-id: 8e63a873-d7b5-4c6c-b14d-3c3fbc82b62f
source-git-commit: e01dfcf3cccea589083a23171f4b8d9ecad58233
workflow-type: tm+mt
source-wordcount: '253'
ht-degree: 1%

---


# 存取ECID

此 [!DNL Experience Cloud Identity (ECID)] 是使用者造訪您的網站時，指派給使用者的持續性識別碼。 在某些情況下，您可能會偏好存取 [!DNL ECID] （例如，傳送給第三方）。 另一個使用案例是設定 [!DNL ECID] 在自訂XDM欄位中，身分對應中也會有。

您可透過以下方式存取ECID： [資料收集的資料準備](../../../../datastreams/data-prep.md) （建議）或透過標籤。

## 透過「資料準備」存取ECID （偏好方法） {#accessing-ecid-data-prep}

如果您想在自訂XDM欄位中設定ECID，除了在身分對應中擁有它之外，您還可以透過設定 `source` 至下列路徑：

```js
xdm.identityMap.ECID[0].id
```

然後，將目標設定為欄位屬於型別的XDM路徑 `string`.

![](./assets/access-ecid-data-prep.png)

## 標記

如果您需要存取 [!DNL ECID] 在使用者端，使用如下所述的標籤方法。

1. 確定您的屬性已設定為 [規則元件排序](../../../ui/managing-resources/rules.md#sequencing) 已啟用。
1. 建立新規則。 此規則應僅用於擷取 [!DNL ECID] 而不執行任何其他重要動作。
1. 新增 [!UICONTROL 程式庫已載入] 事件至規則。
1. 新增 [!UICONTROL 自訂程式碼] 對規則的動作，包含下列程式碼(假設您已為SDK執行個體設定的名稱為 `alloy` 而且還沒有相同名稱的資料元素)：

   ```js
    return alloy("getIdentity")
      .then(function(result) {
        _satellite.setVar("ECID", result.identity.ECID);
      });
   ```

1. 儲存規則。

之後，您應該能夠存取 [!DNL ECID] 在後續規則中，使用 `%ECID%` 或 `_satellite.getVar("ECID")`，就像存取任何其他資料元素一樣。
