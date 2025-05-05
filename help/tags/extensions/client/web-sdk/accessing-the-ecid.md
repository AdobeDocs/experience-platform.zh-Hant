---
title: 存取ECID
description: 瞭解如何從「資料準備」或「標籤」存取Experience CloudID
exl-id: 8e63a873-d7b5-4c6c-b14d-3c3fbc82b62f
source-git-commit: e53ae6053a4b00e7e75242b95496c6795953005a
workflow-type: tm+mt
source-wordcount: '283'
ht-degree: 1%

---


# 存取ECID

[!DNL Experience Cloud Identity (ECID)]是指派給使用者造訪您網站時的持續性識別碼。 在某些情況下，您可能會偏好存取[!DNL ECID] （例如，將其傳送給第三方）。 除了在身分對應中設定[!DNL ECID]之外，另一個使用案例是在自訂XDM欄位中設定。

您可以透過[資料收集的資料準備](../../../../datastreams/data-prep.md) （建議）或標籤存取ECID。

## 透過「資料準備」存取ECID （偏好方法） {#accessing-ecid-data-prep}

此方法使用[資料彙集的資料準備](../../../../datastreams/data-prep.md)來設定`ECID`的自訂對應。

請參閱資料彙集[&#128279;](../../../../datastreams/data-prep.md)的資料準備檔案，瞭解如何使用此功能。

如果您打算在自訂XDM欄位中設定ECID，除了在身分對應中擁有它之外，您還可以透過將`source`設定為以下路徑來執行此操作：

```js
xdm.identityMap.ECID[0].id
```

然後，將目標設定為欄位型別為`string`的XDM路徑。

![](./assets/access-ecid-data-prep.png)

## 標記

如果您需要在使用者端存取[!DNL ECID]，請使用如下所述的標籤方法。

1. 確定您的屬性已設定為啟用[規則元件排序](../../../ui/managing-resources/rules.md#sequencing)。
1. 建立新規則。 此規則應僅用於擷取[!DNL ECID]，而不包含任何其他重要動作。
1. 將[!UICONTROL 載入的程式庫]事件新增至規則。
1. 使用下列程式碼將[!UICONTROL 自訂程式碼]動作新增至規則（假設您已為SDK執行個體設定的名稱為`alloy`，而且還沒有相同名稱的資料元素）：

   ```js
    return alloy("getIdentity")
      .then(function(result) {
        _satellite.setVar("ECID", result.identity.ECID);
      });
   ```

1. 儲存規則。

之後，您應該能夠使用`%ECID%`或`_satellite.getVar("ECID")`存取後續規則中的[!DNL ECID]，就像存取任何其他資料元素一樣。
