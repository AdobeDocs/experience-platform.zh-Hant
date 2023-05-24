---
title: 位置提示
description: 本文介紹了位置提示在邊緣網路伺服器API中如何工作，以便最終用戶請求始終可以路由到同一伺服器。
exl-id: 8cd2f8e2-2065-4b7e-8d35-4ed1a716f1b3
source-git-commit: 2c7a5f007189d897ed32302a2a80c1e16af6af80
workflow-type: tm+mt
source-wordcount: '414'
ht-degree: 0%

---

# 位置提示

## 總覽 {#overview}

的 [!DNL Adobe Experience Platform Edge Network] 使用多個全局分佈的伺服器，確保快速響應時間，而不管最終用戶位置如何。 它還使用基於DNS的路由來確保請求始終路由到最靠近最終用戶的邊緣網路位置。

如果最終用戶在會話過程中連接到VPN或在移動設備上切換網路類型，則邊緣網路請求通常可以路由到其他位置。 由於Adobe Experience Platform和Adobe Experience Cloud解決方案在邊緣網路上儲存最終用戶配置檔案資訊，因此伺服器之間的中間會話路由可能存在問題。

這就是位置提示的發揮點。

為確保最終用戶始終與包含其當前配置檔案資料的邊緣網路區域伺服器進行交互，位置提示功能確保向邊緣網路發出的所有請求都發送到第一次發出會話請求的同一伺服器。 這有助於用戶獲得一致的體驗，無論他們在會話過程中可能經歷哪種網路更改。

## 位置提示用法

位置提示包括在初始邊緣網路請求的響應中，以及所有後續請求中，如下例所示：

```json
{
   "payload":[
      {
         "scope":"EdgeNetwork",
         "hint":"or2",
         "ttlSeconds":1800
      }
   ],
   "type":"locationHint:result"
}
```

的 `EdgeNetwork` 作用域包含邊緣網路相應路由後續請求所需的所有相關資訊。 在對Edge網路的初始請求和每個後續請求的響應中，句柄中將存在一個類型為 `locationHint:result`。

與 `EdgeNetwork` 作用域可以包含以下值之一：

* `or2`
* `va6`
* `irl1`
* `ind1`
* `jpn3`
* `sgp3`
* `aus3`

**API格式**

為確保正確路由後續請求，請在基本路徑之間後續API調用的URL路徑中插入位置提示，通常 `ee`, `v2` API版本。

```http
POST 'https://edge.adobedc.net/ee/{LOCATION_HINT}/v2/interact?dataStreamId={DataStream_ID}'
```

## 在Cookie中儲存位置提示 {#storing-hints-in-cookies}

為確保邊緣網路返回的位置提示在會話期間持續存在，您可以將位置提示值與cookie生命期一起儲存在Cookie中 `ttlSeconds` 欄位（通常為1800秒）。

與大多數Cookie一樣，每次從邊緣網路發出響應時，應延長此Cookie的生存期。 要確保與Web SDK的最大相容性，請使用Cookie名稱 `kndctr_{IMSORG}_AdobeOrg_cluster`。 組織ID通常以 `@AdobeOrg`。 的 `@` 必須將值轉換為下划線，以確保cookie的格式正確。
