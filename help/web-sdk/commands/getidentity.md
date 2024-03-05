---
title: getIdentity
description: 取得訪客的身分而不傳送事件資料。
source-git-commit: 90493d179e620604337bda96cb3b7f5401ca4a81
workflow-type: tm+mt
source-wordcount: '190'
ht-degree: 2%

---

# `getIdentity`

此 `getIdentity` 命令可讓您在不傳送事件資料的情況下取得訪客ID。 當您執行 `sendEvent` 命令中，如果訪客的身分尚未出現，Web SDK就會自動取得該訪客的身分。

如果您需要個別呼叫來產生訪客ID並傳送資料，可以使用此命令。

## 使用Web SDK標籤擴充功能取得身分

Web SDK標籤擴充功能不會透過標籤擴充功能UI提供此命令。 使用JavaScript程式庫語法來使用自訂程式碼編輯器。

## 使用Web SDK JavaScript程式庫取得身分

執行 `getIdentity` 命令來呼叫Web SDK的已設定執行個體。 設定此命令時，可以使用下列選項：

* **`namespaces`**：名稱空間陣列。 預設值為 `["ECID"]`。有效值包括 `["ECID"]`， `null`，或 `undefined`.
* **`edgeConfigOverrides`**：一個 [資料流設定覆寫物件](datastream-overrides.md).

```js
alloy("getIdentity",{
  "namespaces": ["ECID"]
});
```

## 回應物件

如果您決定 [處理回應](command-responses.md) 使用此命令，回應物件中可以使用下列屬性：

* **`identity.ECID`**：包含訪客ECID的字串。
* **`edge.regionID`**：整數，代表瀏覽器在取得身分時點選的Edge Network區域。 它與舊版Audience Manager位置提示相同。
