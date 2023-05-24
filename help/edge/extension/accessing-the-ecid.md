---
title: 訪問ECID
description: 瞭解如何從資料準備或標籤中訪問Experience CloudID
exl-id: 8e63a873-d7b5-4c6c-b14d-3c3fbc82b62f
source-git-commit: dee04f2cdeb9057ac10e27a17f9db3f065712618
workflow-type: tm+mt
source-wordcount: '228'
ht-degree: 3%

---


# 訪問ECID

的 [!DNL Experience Cloud Identity (ECID)] 是在用戶訪問您的網站時分配給他們的永久標識符。 在某些情況下，您可能希望 [!DNL ECID] （例如，將其發送給第三方）。 另一個用例是設定 [!DNL ECID] 在自定義XDM欄位中，除了將其包含在標識映射中外。

您可以通過 [資料收集的資料準備](../datastreams/data-prep.md) （推薦）或通過標籤。

## 通過資料準備（首選方法）訪問ECID {#accessing-ecid-data-prep}

如果您希望在自定義XDM欄位中設定ECID，除了在標識映射中設定ECID外，還可以通過設定 `source` 到以下路徑：

```js
xdm.identityMap.ECID[0].id
```

然後，將目標設定為XDM路徑，其中欄位的類型為 `string`。

![](./assets/access-ecid-data-prep.png)

## 標記

如果您需要訪問 [!DNL ECID] 在客戶端，使用如下所述的標籤方法。

1. 確保已配置您的屬性 [規則元件排序](../../tags/ui/managing-resources/rules.md#sequencing) 啟用。
1. 建立新規則。
1. 添加 [!UICONTROL 已載入庫] 事件。
1. 添加 [!UICONTROL 自定義條件] 使用以下代碼對規則執行操作(假定為SDK實例配置的名稱為 `alloy`):

   ```js
    return alloy("getIdentity")
      .then(function(result) {
        _satellite.setVar("ECID", result.identity.ECID);
      });
   ```

1. 儲存規則。

然後，您就可以 [!DNL ECID] 在後續規則中使用 `%ECID%` 或 `_satellite.getVar("ECID")`，就像您訪問任何其他資料元素一樣。
