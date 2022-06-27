---
title: 資料收集
description: 瞭解Adobe Experience Platform邊緣網路伺服器API如何構建收集的資料。
source-git-commit: f52603f7e65ac553e00a2b632857561cd07ae441
workflow-type: tm+mt
source-wordcount: '131'
ht-degree: 5%

---


# 資料收集

的 [!DNL Server API] 提供了兩種類型的資料收集端點：

* [互動式資料收集終結點](interactive-data-collection.md)，當客戶端希望伺服器返迴響應時使用。 這些端點還可以在執行資料收集時從其他邊緣網路服務返回內容。
* [非互動式事件資料收集](non-interactive-data-collection.md)，在伺服器沒有響應時使用。 這些終結點僅用於資料收集。

## `Event` 對象 {#event-object}

由 [!DNL Server API] 在 `Event` 的雙曲餘切值。 此對象的結構如下所述。

```json
{
   "xdm":{
      "identityMap":{
         "Email_LC_SHA256":[
            {
               "id":"0c7e6a405862e402eb76a70f8a26fc732d07c32931e9fae9ab1582911d2e8a3b",
               "primary":true
            }
         ]
      },
      "eventType":"web.webpagedetails.pageViews",
      "web":{
         "webPageDetails":{
            "URL":"https://alloystore.dev/",
            "name":"home-demo-Home Page",
            "pageViews":{
               "value":1
            }
         }
      },
      "placeContext":{
         "localTime":"2021-08-09T17:09:20.859+03:00",
         "localTimezoneOffset":-180
      },
      "timestamp":"2021-08-09T14:09:20.859Z"
   },
   "data":{
      "prop1":"custom value",
      "var10":"search (organic)"
   }
}
```

| 屬性 | 類型 | 說明 |
| --- | --- | --- |
| `xdm` | 物件 | *必填*. JSON對象包含XDM格式的資料，與資料集架構相對應。 |
| `data` | 物件 | *可選*. 包含自由格式資料的JSON對象，可通過邊緣網路映射到XDM。 |

