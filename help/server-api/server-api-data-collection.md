---
title: 資料收集
description: 了解Adobe Experience Platform Edge Network Server API如何建構收集的資料。
source-git-commit: f52603f7e65ac553e00a2b632857561cd07ae441
workflow-type: tm+mt
source-wordcount: '131'
ht-degree: 5%

---


# 資料收集

此 [!DNL Server API] 提供兩種資料收集端點：

* [互動式資料收集端點](interactive-data-collection.md)，用於用戶端預期伺服器傳回回應時。 執行資料收集時，這些端點也可從其他邊緣網路服務傳回內容。
* [非互動式事件資料收集](non-interactive-data-collection.md)，用於預期不會從伺服器傳回任何回應時。 這些端點僅用於資料收集。

## `Event` 物件 {#event-object}

由 [!DNL Server API] 是在 `Event` 物件。 此物件的結構如下所述。

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
| `xdm` | 物件 | *必填*. 包含XDM格式資料的JSON物件，此格式與資料集結構描述相對應。 |
| `data` | 物件 | *可選*. 包含自由格式資料的JSON物件，可透過邊緣網路對應至XDM。 |

