---
title: 位置提示
description: 本文說明位置提示在Edge Network伺服器API中的運作方式，以便一般使用者請求可一律路由傳送到相同伺服器。
exl-id: 8cd2f8e2-2065-4b7e-8d35-4ed1a716f1b3
source-git-commit: 2c7a5f007189d897ed32302a2a80c1e16af6af80
workflow-type: tm+mt
source-wordcount: '415'
ht-degree: 0%

---

# 位置提示

## 概觀 {#overview}

[!DNL Adobe Experience Platform Edge Network]使用數個全域分散式伺服器，以確保快速回應時間，無論使用者位於何處。 它也會使用DNS型路由，確保要求一律路由至最接近使用者的Edge Network位置。

如果使用者在工作階段期間連線到VPN，或在其行動裝置上切換網路型別，Edge Network請求通常可以路由到其他位置。 伺服器之間的工作階段中間路由可能會產生問題，因為Adobe Experience Platform和Adobe Experience Cloud解決方案會將Edge Network上的使用者設定檔資訊儲存起來。

這是位置提示發揮作用的地方。

為確保一般使用者與包含其目前設定檔資料的Edge Network區域伺服器一律互動，位置提示功能可確保所有對Edge Network的請求都傳送至產生工作階段第一個請求的相同伺服器。 無論使用者在工作階段中可能會遇到哪些網路變更，這都能協助他們獲得一致的體驗。

## 位置提示使用

位置提示會包含在初始Edge Network請求的回應中，以及所有後續請求中，如以下範例所示：

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

`EdgeNetwork`範圍包含Edge Network據以路由後續請求所需的所有相關資訊。 在對Edge網路發出初始和每個後續要求的回應中，控制代碼中將有一個型別為`locationHint:result`的區段。

與`EdgeNetwork`範圍關聯的提示可包含下列其中一個值：

* `or2`
* `va6`
* `irl1`
* `ind1`
* `jpn3`
* `sgp3`
* `aus3`

**API格式**

為確保後續要求正確路由，請在基底路徑（通常是`ee`和`v2` API版本）之間後續API呼叫的URL路徑中插入位置提示。

```http
POST 'https://edge.adobedc.net/ee/{LOCATION_HINT}/v2/interact?dataStreamId={DataStream_ID}'
```

## 將位置提示儲存在Cookie中 {#storing-hints-in-cookies}

若要確保Edge Network傳回的位置提示在工作階段期間持續存在，您可以將位置提示值以及Cookie存留期儲存在`ttlSeconds`欄位中（通常為1800秒）。

和大多數Cookie一樣，每當Edge Network有回應時，都應延長此Cookie的生命週期。 若要確保與Web SDK的最大相容性，請使用Cookie名稱`kndctr_{IMSORG}_AdobeOrg_cluster`。 組織ID通常以`@AdobeOrg`結尾。 `@`值必須轉換為底線，以確保Cookie的格式正確。
