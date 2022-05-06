---
keywords: Experience Platform；首頁；熱門主題；資料準備；api指南；架構；
solution: Experience Platform
title: 架構API終結點
topic-legacy: schemas
description: 可以使用Adobe Experience PlatformAPI中的「/functions」終結點驗證映射表達式並列出可用的映射集函式。
exl-id: dc24bfb4-2d96-4757-a610-0c2ee960d41d
source-git-commit: 47a94b00e141b24203b01dc93834aee13aa6113c
workflow-type: tm+mt
source-wordcount: '210'
ht-degree: 2%

---

# 函式端點

映射集函式允許您在源架構和目標架構之間轉換資料。 您可以使用 `/languages/el` 終結點，以驗證表達式並獲取所有可用映射集函式的清單。

## 驗證表達式

您可以通過向以下對象發出POST請求來驗證當前表達式是否有效 `/languages/el/validate` 端點。

**API格式**

```
POST /languages/el/validate
```

**要求**

```shell
curl -X POST https://platform.adobe.io/data/foundation/conversion/languages/el/validate \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \ 
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '
  {
    "expression": "concat(\"Hi\", \",\", \"there\", \"!\")"
  }'
```

**回應**

成功的響應返回HTTP狀態200，其驗證狀態為表達式。

```json
{
    "validationStatus": "succeeded",
    "error": "none"
}
```

## 清單映射集函式

通過向Web站點發出GET請求，可以檢索所有可用映射集函式的清單 `/languages/el/functions` 端點。

**API格式**

```
GET /languages/el/functions
```

**要求**

```shell
curl -X GET https://platform.adobe.io/data/foundation/conversion/languages/el/functions \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \ 
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**回應**

成功的響應返回HTTP狀態200，其中包含所有可用映射集函式的清單。

>[!NOTE]
>
>此響應已被截斷為空間。

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

通過向 `/languages/el/operators` 端點。

**API格式**

```
GET /languages/el/operators
```

**要求**

```shell
curl -X GET https://platform.adobe.io/data/foundation/conversion/languages/el/operators \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \ 
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**回應**

成功的響應返回HTTP狀態200，其中包含所有可用映射集運算子的清單。

>[!NOTE]
>
>此響應已被截斷為空間。

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
