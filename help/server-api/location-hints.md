---
title: 位置提示
description: 本文說明位置提示在邊緣網路伺服器API中如何運作，以便讓一般使用者要求一律路由至相同的伺服器。
exl-id: 8cd2f8e2-2065-4b7e-8d35-4ed1a716f1b3
source-git-commit: 80c527ab3c82e01fe19e5003e224d63e79b23bdc
workflow-type: tm+mt
source-wordcount: '415'
ht-degree: 0%

---

# 位置提示

## 總覽 {#overview}

此 [!DNL Adobe Experience Platform Edge Network] 使用多個全域分佈的伺服器，確保快速響應時間，而不管最終用戶的位置如何。 它還使用基於DNS的路由，以確保請求始終路由到最靠近最終用戶的邊緣網路位置。

如果終端使用者在工作階段期間連線至VPN，或在其行動裝置上切換網路類型，邊緣網路請求通常可路由至不同位置。 由於Adobe Experience Platform和Adobe Experience Cloud解決方案會將一般使用者設定檔資訊儲存在邊緣網路上，因此伺服器之間的中間工作階段路由可能會造成問題。

這就是位置提示發揮作用的地方。

為確保最終用戶始終與包含其當前配置檔案資料的邊緣網路區域伺服器交互，位置提示功能可確保向邊緣網路發出的所有請求都發送到發出會話第一個請求的同一伺服器。 無論使用者在工作階段中可能會經歷哪些網路變更，這都能協助使用者提供一致的體驗。

## 位置提示用法

初始邊緣網路請求的響應和所有後續請求都包含位置提示，如以下示例所示：

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

此 `EdgeNetwork` 作用域包含邊緣網路相應路由後續請求所需的所有相關資訊。 在對Edge網路的初始和每個後續請求的響應中，句柄中會有一個部分，其類型為 `locationHint:result`.

與 `EdgeNetwork` 作用域可以包含以下值之一：

* `or2`
* `va6`
* `irl1`
* `ind1`
* `jpn3`
* `sgp3`
* `aus3`

**API格式**

為確保後續請求正確路由，請在基礎路徑之間後續API呼叫的URL路徑中插入位置提示，通常為 `ee`，和 `v2` API版本。

```http
POST 'https://edge.adobedc.net/ee/{LOCATION_HINT}/v2/interact?dataStreamId={DataStream_ID}'
```

## 在Cookie中儲存位置提示 {#storing-hints-in-cookies}

若要確保邊緣網路傳回的位置提示在工作階段期間持續存在，您可以將位置提示值與Cookie期限(包含在 `ttlSeconds` 欄位（通常為1800秒）。

和大部分的Cookie一樣，每次有來自邊緣網路的回應時，您都應延長此Cookie的存留期。 若要確保與Web SDK的最大相容性，請使用Cookie名稱 `kndctr_{IMSORG}_AdobeOrg_cluster`. IMS組織ID的結尾通常為 `@AdobeOrg`. 此 `@` 值必須轉換為底線，才能確保cookie的格式正確。
