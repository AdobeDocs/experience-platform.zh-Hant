---
title: getIdentity
description: 取得訪客的身分而不傳送事件資料。
exl-id: 28b99f62-14c4-4e52-a5c7-9f6fe9852a87
source-git-commit: a884790aa48fb97eebe2421124fc5d5f76c8a79d
workflow-type: tm+mt
source-wordcount: '206'
ht-degree: 2%

---

# `getIdentity`

`getIdentity`命令可讓您在不傳送事件資料的情況下取得訪客ID。 當您執行`sendEvent`命令時，Web SDK會自動取得訪客的身分（如果尚未取得）。

如果您需要個別呼叫來產生訪客ID並傳送資料，可以使用此命令。

## 使用Web SDK標籤擴充功能取得身分

Web SDK標籤擴充功能不會透過標籤擴充功能UI提供此命令。 使用JavaScript程式庫語法來使用自訂程式碼編輯器。

## 使用Web SDK JavaScript資料庫取得身分

呼叫Web SDK的已設定執行個體時執行`getIdentity`命令。 設定此命令時，可以使用下列選項：

* **`namespaces`**：名稱空間陣列。 預設值為 `["ECID"]`。其他支援的值包括： `["CORE"]`、`null`、`undefined`。 您可以同時要求[!DNL ECID]和[!DNL CORE ID]。 範例：`"namespaces": ["ECID","CORE"]`。
* **`edgeConfigOverrides`**： [資料流設定覆寫物件](datastream-overrides.md)。

```js
alloy("getIdentity",{
  "namespaces": ["ECID","CORE"] //this command retrieves both ECID and CORE IDs.
});
```

## 回應物件

如果您決定使用此命令[處理回應](command-responses.md)，則回應物件中有以下屬性：

* **`identity.ECID`**：包含訪客ECID的字串。
* **`identity.CORE`**：包含訪客核心ID的字串。
* **`edge.regionID`**：整數，代表取得身分時瀏覽器點選的Edge Network區域。 它與舊版Audience Manager位置提示相同。
