---
keywords: Experience Platform;home;mapper;mapping set;mapping;
solution: Experience Platform
title: 映射集概述
topic: 概述
description: 瞭解如何搭配「Adobe Experience Platform資料準備」使用對應集。
translation-type: tm+mt
source-git-commit: 4c06f621eb6fba8daa6501d56255cddbbcfdbda2
workflow-type: tm+mt
source-wordcount: '960'
ht-degree: 0%

---


# 映射集概述

映射集是一組映射，用於將資料從一個模式轉換為另一個模式。 本文檔提供了映射集的構成方式，包括輸入模式、輸出模式和映射。

## 快速入門

本概覽需要對Adobe Experience Platform的下列組成部分有切實的瞭解：

- [資料準備](./home.md):資料準備可讓資料工程師將資料對應、轉換及驗證至Experience Data Model(XDM)。
- [資料流](../dataflows/home.md):資料流是跨平台移動資料的資料作業的表示。資料流是跨不同服務配置的，有助於將資料從源連接器移動到目標資料集、移動到[!DNL Identity]和[!DNL Profile]以及移動到[!DNL Destinations]。
- [[!DNL Adobe Experience Platform Data Ingestion]](../ingestion/home.md):可傳送資料的方法 [!DNL Experience Platform]。
- [[!DNL Experience Data Model (XDM) System]](../xdm/home.md):組織客戶體驗資 [!DNL Experience Platform] 料的標準化架構。

## 映射集語法

映射集由ID、名稱、輸入模式、輸出模式和關聯映射的清單組成。

下列JSON為典型對應集的範例：

```json
{
    "id" : "cbb0da769faa48fcb29e026a924ba29d",
    "name" : "Demo Mapping Set",
    "inputSchema" : {
        "id": "a167ff2947ff447ebd8bcf7ef6756232",
        "version": 0
    },
    "outputSchema": {
        "schemaRef": {
            "id": "https://ns.adobe.com/{TENANT_ID}/schemas/6dd1768be928c36d58ad4897219bb52d491671f966084bc0",
            "contentType": "application/vnd.adobe.xed-full+json;version=1"
        }
    },
    "mappings": [
        {
            "sourceType": "ATTRIBUTE",
            "source": "Id",
            "destination": "_id",
            "name" : "Id",
            "description" : "Identifier field"
        },
        {
            "sourceType": "ATTRIBUTE",
            "source": "FirstName",
            "destination": "person.name.firstName"
        },
        {
            "sourceType": "ATTRIBUTE",
            "source": "LastName",
            "destination": "person.name.lastName"
        }
    ]
}
```

| 屬性 | 說明 |
| -------- | ----------- |
| `id` | 映射集的唯一標識符。 |
| `name` | 映射集的名稱。 |
| `inputSchema` | 傳入資料的XDM模式。 |
| `outputSchema` | 將轉換輸入資料的XDM模式以符合。 |
| `mappings` | 源模式到目標模式的欄位到欄位映射的陣列。 |
| `sourceType` | 對於每個列出的映射，其`sourceType`屬性都指示要映射的源類型。 可以是`ATTRIBUTE`、`STATIC`或`EXPRESSION`之一： <ul><li> `ATTRIBUTE` 用於在源路徑中找到的任何值。 </li><li>`STATIC` 用於插入到目標路徑中的值。此值保持不變，不受源模式影響。</li><li> `EXPRESSION` 用於運算式，在執行時期中將會解析。可在[映射函式指南](./functions.md)中找到可用表達式的清單。</li> </ul> |
| `source` | 對於每個列出的映射，`source`屬性都指示要映射的欄位。 有關如何配置源的詳細資訊，請參閱[源部分](#sources)。 |
| `destination` | 對於每個列出的映射，`destination`屬性都指示欄位或欄位的路徑，從`source`欄位提取的值將放在該欄位。 有關如何配置目標的詳細資訊，請參閱[目標部分](#destination)。 |
| `mappings.name` | （*可選*）映射的名稱。 |
| `mappings.description` | （*可選*）映射的說明。 |

## 配置映射源

在映射中，`source`可以是欄位、表達式或靜態值。 根據給定的源類型，可以用多種方法提取值。

### 欄式資料中的欄位

在對應欄式資料（例如CSV檔案）中的欄位時，請使用`ATTRIBUTE`來源類型。 如果欄位名中包含`.`，請使用`\`轉義值。 以下是此映射的範例：

**範例CSV檔案：**

```csv
Full.Name, Email
John Smith, js@example.com
```

**範例映射**

```json
{
    "source": "Full.Name",
    "destination": "pi.name",
    "sourceType": "ATTRIBUTE"
}
```

**轉換的資料**

```json
{
    "pi": {
        "name": "John Smith"
    }
}
```

### 巢狀資料中的欄位

在對應巢狀資料（例如JSON檔案）中的欄位時，請使用`ATTRIBUTE`來源類型。 如果欄位名中包含`.`，請使用`\`轉義值。 以下是此映射的範例：

**範例JSON檔案**

```json
{
    "customerInfo": {
        "name": "John Smith",
        "email": "js@example.com"
    }
}
```

**範例映射**

```json
{
    "source": "customerInfo.name",
    "destination": "pi.name",
    "sourceType": "ATTRIBUTE"
}
```

**轉換的資料**

```json
{
    "pi": {
        "name": "John Smith"
    }
}
```

### 陣列中的欄位

在陣列內映射欄位時，可以使用索引來檢索特定值。 若要這麼做，請使用`ATTRIBUTE`來源類型和您要映射的值的索引。 以下是此映射的範例：

**範例JSON檔案**

```json
{
    "customerInfo": {
        "emails": [
            {
                "name": "John Smith",
                "email": "js@example.com"
            },
            {
                "name": "Jane Smith",
                "email": "jane@example.com"
            }
        ]
    }
}
```

**範例映射**

```json
{
    "source": "customerInfo.emails[0].email",
    "destination": "pi.email",
    "sourceType": "ATTRIBUTE"
}
```

**轉換的資料**

```json
{
    "pi": {
        "email": "js@example.com"
    }
}
```

### 陣列到陣列或對象到對象

使用`ATTRIBUTE`源類型，還可以直接將陣列映射到陣列或對象到對象。 以下是此映射的範例：

**範例JSON檔案**

```json
{
    "customerInfo": {
        "emails": [
            {
                "name": "John Smith",
                "email": "js@example.com"
            },
            {
                "name": "Jane Smith",
                "email": "jane@example.com"
            }
        ]
    }
}
```

**範例映射**

```json
{
    "source": "customerInfo.emails",
    "destination": "pi.emailList",
    "sourceType": "ATTRIBUTE"
}
```

**轉換的資料**

```json
{
    "pi": {
        "emailList": [
            {
                "name": "John Smith",
                "email": "js@example.com"
            },
            {
                "name": "Jane Smith",
                "email": "jane@example.com"
            }
        ]
    }
}
```

### 陣列上的迭代操作

使用`ATTRIBUTE`源類型，您可以反覆循環遍歷陣列，並使用通配符索引(`[*]`)將其映射到目標模式。 以下是此映射的範例：

**範例JSON檔案**

```json
{
    "customerInfo": {
        "emails": [
            {
                "name": "John Smith",
                "email": "js@example.com"
            },
            {
                "name": "Jane Smith",
                "email": "jane@example.com"
            }
        ]
    }
}
```

**範例映射**

```json
{
    "source": "customerInfo.emails[*].name",
    "destination": "pi[*].names",
    "sourceType": "ATTRIBUTE"
}
```

**轉換的資料**

```json
{
    "pi": [
        {
            "names": {
                "name": "John Smith"
            } 
        },
        {
            "names": {
                "name": "Jane Smith"
            }
        }
    ]
}
```

### 常數值

如果要映射常數或靜態值，請使用`STATIC`源類型。  使用`STATIC`源類型時，`source`表示要分配給`destination`的硬編碼值。 以下是此映射的範例：

**範例JSON檔案**

```json
{
    "name": "John Smith",
    "email": "js@example.com"
}
```

**範例映射**

```json
{
    "source": "CUSTOMER",
    "destination": "userType",
    "sourceType": "STATIC"
}
```

**轉換的資料**

```json
{
    "userType:": "CUSTOMER"
}
```

### 運算式

如果要映射表達式，請使用`EXPRESSION`源類型。 [映射函式指南](./functions.md)中可找到接受函式的清單。 使用`EXPRESSION`源類型時，`source`表示要解析的函式。 以下是此映射的範例：

**範例JSON檔案**

```json
{
    "firstName": "John",
    "lastName": "Smith",
    "email": "js@example.com"
}
```

**範例映射**

```json
{
    "source": "concat(upper(lastName), upper(firstName), now())",
    "destination": "pi.created",
    "sourceType": "EXPRESSION"
}
```

**轉換的資料**

```json
{
    "pi": {
        "created": "SMITHJOHNFri Sep 25 15:17:31 PDT 2020"
    }
}
```

## 配置映射目標

在映射中，`destination`是從`source`提取的值將插入的位置。

### 根級別的欄位

當您要將`source`值映射到已轉換資料的根級別時，請遵循以下示例：

**範例JSON檔案**

```json
{
    "customerInfo": {
        "name": "John Smith",
        "email": "js@example.com"
    }
}
```

**範例映射**

```json
{
    "source": "customerInfo.name",
    "destination": "name",
    "sourceType": "ATTRIBUTE"
}
```

**轉換的資料**

```json
{
    "name": "John Smith"
}
```

### 巢狀欄位

當您要將`source`值映射至轉換資料中的巢狀欄位時，請遵循下列範例：

**範例JSON檔案**

```json
{
    "name": "John Smith",
    "email": "js@example.com"
}
```

**範例映射**

```json
{
    "source": "name",
    "destination": "pi.name",
    "sourceType": "ATTRIBUTE"
}
```

**轉換的資料**

```json
{
    "pi": {
        "name": "John Smith"
    }
}
```

### 特定陣列索引處的欄位

當要將`source`值映射到已轉換資料中陣列中的特定索引時，請遵循以下示例：

**範例JSON檔案**

```json
{
    "customerInfo": {
        "name": "John Smith",
        "email": "js@example.com"
    }
}
```

**範例映射**

```json
{
    "source": "customerInfo.name",
    "destination": "piList[0]",
    "sourceType": "ATTRIBUTE"
}
```

**轉換的資料**

```json
{
    "piList": ["John Smith"]
}
```

### 迭代陣列操作

當您想要反覆循環使用陣列並將值映射至目標時，可以使用萬用字元索引(`[*]`)。 以下是此範例：

```json
{
    "customerInfo": {
        "emails": [
            {
                "name": "John Smith",
                "email": "js@example.com"
            },
            {
                "name": "Jane Smith",
                "email": "jane@example.com"
            }
        ]
    }
}
```

**範例映射**

```json
{
    "source": "customerInfo.emails[*].name",
    "destination": "pi[*].names",
    "sourceType": "ATTRIBUTE"
}
```

**轉換的資料**

```json
{
    "pi": [
        {
            "names": {
                "name": "John Smith"
            } 
        },
        {
            "names": {
                "name": "Jane Smith"
            }
        }
    ]
}
```

## 後續步驟

閱讀本檔案後，您現在應瞭解如何建構對應集，包括如何在對應集內設定個別對應。 有關其他資料準備功能的詳細資訊，請閱讀[資料準備概述](./home.md)。 要瞭解如何使用資料準備API中的映射集，請閱讀[資料準備開發人員指南](./api/overview.md)。