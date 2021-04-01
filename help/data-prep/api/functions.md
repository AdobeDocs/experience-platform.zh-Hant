---
keywords: Experience Platform;home；熱門主題；資料準備；api指南；方案；
solution: Experience Platform
title: 方案API端點
topic: 模式
description: '您可以使用Adobe Experience PlatformAPI中的「/functions」端點來驗證映射表達式並列出可用的映射集函式。 '
translation-type: tm+mt
source-git-commit: 60c80a73deb8c77f19d5963cc3319d46143fb4c3
workflow-type: tm+mt
source-wordcount: '211'
ht-degree: 2%

---


# 函式端點

映射集函式允許您在源方案和目標方案之間轉換資料。 您可以使用`/languages/el`端點來驗證您的運算式，並取得所有可用映射集函式的清單。

## 驗證運算式

您可以向`/languages/el/validate`端點發出POST請求，以驗證當前表達式是否有效。

**API格式**

```
POST /languages/el/validate
```

**請求**

```shell
curl -X POST https://platform.adobe.io/data/foundation/conversion/languages/el/validate \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \ 
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '
  {
    "expression": "concat(\"Hi\", \",\", \"there\", \"!\")"
  }'
```

**回應**

成功的回應會傳回HTTP狀態200，其驗證狀態為運算式。

```json
{
    "validationStatus": "succeeded",
    "error": "none"
}
```

## 清單映射集函式

通過向`/languages/el/functions`端點發出GET請求，可以檢索所有可用映射集函式的清單。

**API格式**

```
GET /languages/el/functions
```

**請求**

```shell
curl -X GET https://platform.adobe.io/data/foundation/conversion/languages/el/functions \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \ 
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**回應**

成功的響應返回HTTP狀態200，並返回所有可用映射集函式的清單。

>[!NOTE]
>
>此回應已針對空間截斷。

```json
[
    {
        "category": "Date / Time",
        "function": "date",
        "description": "Function that converts date string into a ZonedDateTime object.",
        "syntax": "ZonedDateTime date(String, String, ZonedDateTime)",
        "returns": "Returns the date object that is formatted in given format or a default date if the expression evaluates to a null date.",
        "returnType": "java.time.ZonedDateTime",
        "example": "",
        "result": "",
        "params": [],
        "since": 1
    },
    {
        "category": "Hierarchies - Arrays",
        "function": "first",
        "description": "Function to retrieve the first element of the given array.",
        "syntax": "T first(T...)",
        "returns": "The first element or null if the array is null or empty.",
        "returnType": "java.lang.Object",
        "example": "first(\"1\", \"2\", \"3\")",
        "result": "\"1\"",
        "params": [
            {
                "name": "values",
                "description": "Zero or more arguments",
                "type": "object",
                "dataType": "[Ljava.lang.Object;",
                "position": 1
            }
        ],
        "since": 1
    }
]
```

## 清單映射集運算子

通過向`/languages/el/operators`端點發出GET請求，可以檢索所有可用於映射集運算子的清單。

**API格式**

```
GET /languages/el/operators
```

**請求**

```shell
curl -X GET https://platform.adobe.io/data/foundation/conversion/languages/el/operators \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \ 
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**回應**

成功的回應會傳回HTTP狀態200，並列出所有可用的對應集運算子。

>[!NOTE]
>
>此回應已針對空間截斷。

```json
[
    {
        "operatorSymbol": "+",
        "methodName": "add",
        "numberOfOperands": 2,
        "description": "Simple arithmetic addition",
        "example": "1 + 2"
    },
    {
        "operatorSymbol": "/",
        "methodName": "divide",
        "numberOfOperands": 2,
        "description": "Simple arithmetic division",
        "example": "1 / 2"
    },
    {
        "operatorSymbol": "~",
        "methodName": "complement",
        "numberOfOperands": 1,
        "description": "The usual ~ operator is used, e.g.\n~33\n, ~0010 0001 = 1101 1110 = -34.",
        "example": "~44"
    },
    {
        "operatorSymbol": "-",
        "methodName": "negate",
        "numberOfOperands": 1,
        "description": "The unary - operator is used. For example\n-12",
        "example": "-12"
    },
    {
        "operatorSymbol": "!",
        "methodName": "not",
        "numberOfOperands": 1,
        "description": "The usual ! operator can be used as well as the word not, e.g.\n!cond1\nand\nnot cond1\nare equivalent",
        "example": "!cond1"
    }
]
```
