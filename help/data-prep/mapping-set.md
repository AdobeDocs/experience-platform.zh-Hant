---
keywords: Experience Platform；首頁；映射器；對應集；對應；
solution: Experience Platform
title: 對應集概述
topic-legacy: overview
description: 了解如何搭配Adobe Experience Platform資料準備使用對應集。
source-git-commit: 97f803f649b2c42b0449a2f8f0cff370ed1aba93
workflow-type: tm+mt
source-wordcount: '959'
ht-degree: 0%

---


# 對應集概述

映射集是一組映射，可將資料從一個架構轉換到另一個架構。 本文檔提供如何構成映射集的資訊，包括輸入架構、輸出架構和映射。

## 快速入門

此概觀需要妥善了解下列Adobe Experience Platform元件：

- [資料準備](./home.md):資料準備可讓資料工程師將資料對應、轉換及驗證至Experience Data Model(XDM)。
- [資料流](../dataflows/home.md):資料流是跨平台移動資料的資料作業的表示。資料流可跨不同的服務進行配置，有助於將資料從源連接器移動到目標資料集、到[!DNL Identity]和[!DNL Profile]以及到[!DNL Destinations]。
- [[!DNL Adobe Experience Platform Data Ingestion]](../ingestion/home.md):資料可傳送至的方 [!DNL Experience Platform]法。
- [[!DNL Experience Data Model (XDM) System]](../xdm/home.md):組織客戶體驗資 [!DNL Experience Platform] 料的標準化架構。

## 映射集語法

映射集由ID、名稱、輸入架構、輸出架構和關聯映射的清單組成。

以下是典型對應集的範例：

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
| `inputSchema` | 傳入資料的XDM架構。 |
| `outputSchema` | 將轉換輸入資料的XDM架構以符合。 |
| `mappings` | 從源架構到目標架構的欄位到欄位映射的陣列。 |
| `sourceType` | 對於每個列出的映射，其`sourceType`屬性指示要映射的源的類型。 可以是`ATTRIBUTE`、`STATIC`或`EXPRESSION`之一： <ul><li> `ATTRIBUTE` 用於在源路徑中找到的任何值。 </li><li>`STATIC` 會用於插入至目的地路徑的值。此值保持不變，不受源架構影響。</li><li> `EXPRESSION` 用於運算式，將在執行階段期間解析。可在[映射函式指南](./functions.md)中找到可用表達式的清單。</li> </ul> |
| `source` | 對於所列的每個映射，`source`屬性指示要映射的欄位。 有關如何配置源的更多資訊，請參見[sources部分](#sources)。 |
| `destination` | 對於所列的每個映射，`destination`屬性指示欄位或欄位路徑，從`source`欄位中提取的值將放置在該欄位中。 有關如何配置目標的詳細資訊，請參閱[目標部分](#destination)。 |
| `mappings.name` | （*選用*）對應的名稱。 |
| `mappings.description` | （*選用*）映射的說明。 |

## 配置映射源

在映射中，`source`可以是欄位、表達式或靜態值。 根據給定的源類型，可以以多種方式提取值。

### 欄位資料中的欄位

在欄位資料（例如CSV檔案）中對應欄位時，請使用`ATTRIBUTE`來源類型。 如果欄位名稱內包含`.`，請使用`\`來逸出值。 以下是此對應的範例：

**範例CSV檔案：**

```csv
Full.Name, Email
John Smith, js@example.com
```

**範例對應**

```json
{
    "source": "Full.Name",
    "destination": "pi.name",
    "sourceType": "ATTRIBUTE"
}
```

**轉換後的資料**

```json
{
    "pi": {
        "name": "John Smith"
    }
}
```

### 巢狀資料中的欄位

對應巢狀資料中的欄位時（例如JSON檔案），請使用`ATTRIBUTE`來源類型。 如果欄位名稱內包含`.`，請使用`\`來逸出值。 以下是此對應的範例：

**範例JSON檔案**

```json
{
    "customerInfo": {
        "name": "John Smith",
        "email": "js@example.com"
    }
}
```

**範例對應**

```json
{
    "source": "customerInfo.name",
    "destination": "pi.name",
    "sourceType": "ATTRIBUTE"
}
```

**轉換後的資料**

```json
{
    "pi": {
        "name": "John Smith"
    }
}
```

### 陣列內的欄位

在陣列內對應欄位時，您可以使用索引來擷取特定值。 要執行此操作，請使用`ATTRIBUTE`源類型和要映射的值的索引。 以下是此對應的範例：

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

**範例對應**

```json
{
    "source": "customerInfo.emails[0].email",
    "destination": "pi.email",
    "sourceType": "ATTRIBUTE"
}
```

**轉換後的資料**

```json
{
    "pi": {
        "email": "js@example.com"
    }
}
```

### 陣列到陣列或對象到對象

使用`ATTRIBUTE`源類型，還可以直接將陣列映射到陣列或對象到對象。 以下是此對應的範例：

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

**範例對應**

```json
{
    "source": "customerInfo.emails",
    "destination": "pi.emailList",
    "sourceType": "ATTRIBUTE"
}
```

**轉換後的資料**

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

使用`ATTRIBUTE`源類型，可以迭代地循環陣列，並使用通配符索引(`[*]`)將其映射到目標架構。 以下是此對應的範例：

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

**範例對應**

```json
{
    "source": "customerInfo.emails[*].name",
    "destination": "pi[*].names",
    "sourceType": "ATTRIBUTE"
}
```

**轉換後的資料**

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

如果要映射常數或靜態值，請使用`STATIC`源類型。  使用`STATIC`源類型時，`source`表示要分配給`destination`的硬編碼值。 以下是此對應的範例：

**範例JSON檔案**

```json
{
    "name": "John Smith",
    "email": "js@example.com"
}
```

**範例對應**

```json
{
    "source": "CUSTOMER",
    "destination": "userType",
    "sourceType": "STATIC"
}
```

**轉換後的資料**

```json
{
    "userType:": "CUSTOMER"
}
```

### 運算式

如果要映射表達式，請使用`EXPRESSION`源類型。 [映射函式指南](./functions.md)中可找到接受函式的清單。 使用`EXPRESSION`源類型時，`source`表示要解析的函式。 以下是此對應的範例：

**範例JSON檔案**

```json
{
    "firstName": "John",
    "lastName": "Smith",
    "email": "js@example.com"
}
```

**範例對應**

```json
{
    "source": "concat(upper(lastName), upper(firstName), now())",
    "destination": "pi.created",
    "sourceType": "EXPRESSION"
}
```

**轉換後的資料**

```json
{
    "pi": {
        "created": "SMITHJOHNFri Sep 25 15:17:31 PDT 2020"
    }
}
```

## 設定對應目的地

在映射中，`destination`是將插入從`source`中提取的值的位置。

### 根層級的欄位

如果要將`source`值映射到已轉換資料的根級別，請遵循以下示例：

**範例JSON檔案**

```json
{
    "customerInfo": {
        "name": "John Smith",
        "email": "js@example.com"
    }
}
```

**範例對應**

```json
{
    "source": "customerInfo.name",
    "destination": "name",
    "sourceType": "ATTRIBUTE"
}
```

**轉換後的資料**

```json
{
    "name": "John Smith"
}
```

### 巢狀欄位

如果要將`source`值映射到轉換後資料中的嵌套欄位，請遵循以下示例：

**範例JSON檔案**

```json
{
    "name": "John Smith",
    "email": "js@example.com"
}
```

**範例對應**

```json
{
    "source": "name",
    "destination": "pi.name",
    "sourceType": "ATTRIBUTE"
}
```

**轉換後的資料**

```json
{
    "pi": {
        "name": "John Smith"
    }
}
```

### 特定陣列索引處的欄位

如果要將`source`值映射到轉換資料中陣列中的特定索引，請遵循以下示例：

**範例JSON檔案**

```json
{
    "customerInfo": {
        "name": "John Smith",
        "email": "js@example.com"
    }
}
```

**範例對應**

```json
{
    "source": "customerInfo.name",
    "destination": "piList[0]",
    "sourceType": "ATTRIBUTE"
}
```

**轉換後的資料**

```json
{
    "piList": ["John Smith"]
}
```

### 迭代陣列操作

如果要反複循環陣列並將值映射到目標，則可以使用通配符索引(`[*]`)。 以下是此範例：

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

**範例對應**

```json
{
    "source": "customerInfo.emails[*].name",
    "destination": "pi[*].names",
    "sourceType": "ATTRIBUTE"
}
```

**轉換後的資料**

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

閱讀本檔案後，您現在應了解如何建構對應集，包括如何在對應集內設定個別對應。 有關其他資料準備功能的詳細資訊，請閱讀[資料準備概述](./home.md)。 要了解如何使用資料準備API中的映射集，請閱讀[資料準備開發人員指南](./api/overview.md)。