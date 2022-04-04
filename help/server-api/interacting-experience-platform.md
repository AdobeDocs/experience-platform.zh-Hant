---
title: 與Adobe Experience Platform互動
description: 瞭解如何使用邊緣網路伺服器API與Adobe Experience Platform交互
seo-description: Learn how to use the Edge Network Server API to interact with Adobe Experience Platform
keywords: 資料採集；出口；分析；Adobe Experience Platform邊緣網路api;aep
exl-id: c49e40b7-9653-40f1-9db5-8941b20de8a3
source-git-commit: 422f859bef8faf292fd7e5fd8b6a8d31967421c1
workflow-type: tm+mt
source-wordcount: '71'
ht-degree: 1%

---

# 與Adobe Experience Platform互動

## 總覽 {#overview}

要啟用Experience Platform資料收集，必須首先 [配置資料流](../edge/fundamentals/datastreams.md) 將事件轉發到Experience Platform資料集。

配置後，資料流配置應包括 `com_adobe_experience_platform`，如下例所示：


```json
{
  // datastream config header

  "settings": {
    "com_adobe_experience_platform": {
      "sandboxName": "prod",
      "enabled": true,
      "datasets": {
        "event": {
          "xdmSchema": "https://ns.adobe.com/atag/schemas/35a31609b6d3242736751df469ade031",
          "datasetId": "5f67e6ad9501b0194b5aafb6"
        }
      }
    }

    // other settings
  }
}
```
