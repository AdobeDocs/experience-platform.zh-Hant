---
keywords: Experience Platform；首頁；映射器；映射集；映射；
solution: Experience Platform
title: 映射集概述
description: 瞭解如何將映射集與Adobe Experience Platform資料準備一起使用。
exl-id: b45545b7-3ae7-400d-b6fd-b2cb76061093
source-git-commit: d39ae3a31405b907f330f5d54c91b95c0f999eee
workflow-type: tm+mt
source-wordcount: '959'
ht-degree: 0%

---

# 映射集概述

映射集是一組映射，用於將資料從一個模式轉換到另一個模式。 本文檔提供了如何構成映射集的資訊，包括輸入架構、輸出架構和映射。

## 快速入門

本概述要求對Adobe Experience Platform的下列組成部分進行工作理解：

- [資料準備](./home.md):資料準備允許資料工程師將資料映射到體驗資料模型(XDM)並驗證資料。
- [資料流](../dataflows/home.md):資料流是跨平台移動資料的資料作業的表示形式。 資料流是跨不同服務配置的，有助於將資料從源連接器移動到目標資料集 [!DNL Identity] 和 [!DNL Profile], [!DNL Destinations]。
- [[!DNL Adobe Experience Platform Data Ingestion]](../ingestion/home.md):資料可通過以下方法發送 [!DNL Experience Platform]。
- [[!DNL Experience Data Model (XDM) System]](../xdm/home.md):標準化框架 [!DNL Experience Platform] 組織客戶體驗資料。

## 映射集語法

映射集由ID、名稱、輸入模式、輸出模式和關聯映射的清單組成。

以下JSON是典型映射集的示例：

```json
{
    "id": "cbb0da769faa48fcb29e026a924ba29d",
    "name": "Demo Mapping Set",
    "inputSchema": {
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
            "name": "Id",
            "description": "Identifier field"
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
| `outputSchema` | 將轉換輸入資料的XDM模式以符合。 |
| `mappings` | 從源架構到目標架構的欄位到欄位映射的陣列。 |
| `sourceType` | 對於每個列出的映射， `sourceType` attribute指示要映射的源的類型。 可以是 `ATTRIBUTE`。 `STATIC`或 `EXPRESSION`: <ul><li> `ATTRIBUTE` 用於源路徑中找到的任何值。 </li><li>`STATIC` 用於注入到目標路徑中的值。 此值保持不變，不受源架構的影響。</li><li> `EXPRESSION` 用於表達式，將在運行時解析該表達式。 可在 [映射函式指南](./functions.md)。</li> </ul> |
| `source` | 對於每個列出的映射， `source` attribute表示要映射的欄位。 有關如何配置源的詳細資訊，請參閱 [源節](#sources)。 |
| `destination` | 對於每個列出的映射， `destination` 屬性指示欄位或欄位的路徑，其中從 `source` 的下界。 有關如何配置目標的詳細資訊，請參閱 [目標部分](#destination)。 |
| `mappings.name` | (*可選*)映射的名稱。 |
| `mappings.description` | (*可選*)映射的說明。 |

## 配置映射源

在映射中， `source` 可以是欄位、表達式或靜態值。 根據給定的源類型，可以採用多種方式提取值。

### 列資料中的欄位

在列資料（如CSV檔案）中映射欄位時，使用 `ATTRIBUTE` 源類型。 如果欄位包含 `.` 在其名稱內使用 `\` 來轉義值。 以下是此映射的示例：

**示例CSV檔案：**

```csv
Full.Name, Email
John Smith, js@example.com
```

**示例映射**

```json
{
    "source": "Full.Name",
    "destination": "pi.name",
    "sourceType": "ATTRIBUTE"
}
```

**已轉換的資料**

```json
{
    "pi": {
        "name": "John Smith"
    }
}
```

### 嵌套資料中的欄位

在映射嵌套資料（如JSON檔案）中的欄位時，使用 `ATTRIBUTE` 源類型。 如果欄位包含 `.` 在其名稱內使用 `\` 來轉義值。 以下是此映射的示例：

**示例JSON檔案**

```json
{
    "customerInfo": {
        "name": "John Smith",
        "email": "js@example.com"
    }
}
```

**示例映射**

```json
{
    "source": "customerInfo.name",
    "destination": "pi.name",
    "sourceType": "ATTRIBUTE"
}
```

**已轉換的資料**

```json
{
    "pi": {
        "name": "John Smith"
    }
}
```

### 陣列中的欄位

映射陣列中的欄位時，可以使用索引檢索特定值。 要執行此操作，請使用 `ATTRIBUTE` 源類型和要映射的值的索引。 以下是此映射的示例：

**示例JSON檔案**

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

**示例映射**

```json
{
    "source": "customerInfo.emails[0].email",
    "destination": "pi.email",
    "sourceType": "ATTRIBUTE"
}
```

**已轉換的資料**

```json
{
    "pi": {
        "email": "js@example.com"
    }
}
```

### 陣列到陣列或對象到對象

使用 `ATTRIBUTE` 源類型中，還可以將陣列直接映射到陣列或對象到對象。 以下是此映射的示例：

**示例JSON檔案**

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

**示例映射**

```json
{
    "source": "customerInfo.emails",
    "destination": "pi.emailList",
    "sourceType": "ATTRIBUTE"
}
```

**已轉換的資料**

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

使用 `ATTRIBUTE` 源類型，您可以反複循環使用陣列，並使用通配符索引(`[*]`)。 以下是此映射的示例：

**示例JSON檔案**

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

**示例映射**

```json
{
    "source": "customerInfo.emails[*].name",
    "destination": "pi[*].names",
    "sourceType": "ATTRIBUTE"
}
```

**已轉換的資料**

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

如果要映射常數或靜態值，請使用 `STATIC` 源類型。  使用 `STATIC` 源類型， `source` 表示要分配給的硬編碼值 `destination`。 以下是此映射的示例：

**示例JSON檔案**

```json
{
    "name": "John Smith",
    "email": "js@example.com"
}
```

**示例映射**

```json
{
    "source": "CUSTOMER",
    "destination": "userType",
    "sourceType": "STATIC"
}
```

**已轉換的資料**

```json
{
    "userType:": "CUSTOMER"
}
```

### 表達式

如果要映射表達式，請使用 `EXPRESSION` 源類型。 可在 [映射函式指南](./functions.md)。 使用 `EXPRESSION` 源類型， `source` 表示要解析的函式。 以下是此映射的示例：

**示例JSON檔案**

```json
{
    "firstName": "John",
    "lastName": "Smith",
    "email": "js@example.com"
}
```

**示例映射**

```json
{
    "source": "concat(upper(lastName), upper(firstName), now())",
    "destination": "pi.created",
    "sourceType": "EXPRESSION"
}
```

**已轉換的資料**

```json
{
    "pi": {
        "created": "SMITHJOHNFri Sep 25 15:17:31 PDT 2020"
    }
}
```

## 配置映射目標

在映射中， `destination` 是從 `source` 的子菜單。

### 根級別的欄位

當要映射 `source` 值到已轉換資料的根級別，請遵循以下示例：

**示例JSON檔案**

```json
{
    "customerInfo": {
        "name": "John Smith",
        "email": "js@example.com"
    }
}
```

**示例映射**

```json
{
    "source": "customerInfo.name",
    "destination": "name",
    "sourceType": "ATTRIBUTE"
}
```

**已轉換的資料**

```json
{
    "name": "John Smith"
}
```

### 嵌套欄位

當要映射 `source` 值到已轉換資料中的嵌套欄位，請遵循以下示例：

**示例JSON檔案**

```json
{
    "name": "John Smith",
    "email": "js@example.com"
}
```

**示例映射**

```json
{
    "source": "name",
    "destination": "pi.name",
    "sourceType": "ATTRIBUTE"
}
```

**已轉換的資料**

```json
{
    "pi": {
        "name": "John Smith"
    }
}
```

### 特定陣列索引處的欄位

當要映射 `source` 值到已轉換資料中陣列中的特定索引，請遵循以下示例：

**示例JSON檔案**

```json
{
    "customerInfo": {
        "name": "John Smith",
        "email": "js@example.com"
    }
}
```

**示例映射**

```json
{
    "source": "customerInfo.name",
    "destination": "piList[0]",
    "sourceType": "ATTRIBUTE"
}
```

**已轉換的資料**

```json
{
    "piList": ["John Smith"]
}
```

### 迭代陣列操作

當要反複循環遍歷陣列並將值映射到目標時，可以使用通配符索引(`[*]`)。 下面可以看到此示例：

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

**示例映射**

```json
{
    "source": "customerInfo.emails[*].name",
    "destination": "pi[*].names",
    "sourceType": "ATTRIBUTE"
}
```

**已轉換的資料**

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

通過閱讀本文檔，您現在應該瞭解如何構建映射集，包括如何在映射集內配置單個映射。 有關其他資料準備功能的詳細資訊，請閱讀 [資料準備概述](./home.md)。 要瞭解如何在資料準備API中使用映射集，請閱讀 [資料準備開發人員指南](./api/overview.md)。
