---
keywords: Experience Platform；首頁；對應程式；對應集；對應；
solution: Experience Platform
title: 對應集概述
description: 瞭解如何搭配Adobe Experience Platform資料準備使用對應集。
exl-id: b45545b7-3ae7-400d-b6fd-b2cb76061093
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '960'
ht-degree: 0%

---

# 對應集概述

對應集是一組對應，可將資料從一個結構描述轉換為另一個結構描述。 本檔案提供有關對應集如何構成的資訊，包括輸入結構描述、輸出結構描述和對應。

## 快速入門

此概覽需要深入瞭解下列Adobe Experience Platform元件：

- [資料準備](./home.md)：「資料準備」可讓資料工程師對應、轉換和驗證與Experience Data Model (XDM)之間的資料。
- [資料流](../dataflows/home.md)：資料流可呈現跨Experience Platform行動資料的資料作業。 資料流是跨不同服務設定的，有助於將資料從來源聯結器移至目標資料集、移至[!DNL Identity]和[!DNL Profile]以及移至[!DNL Destinations]。
- [[!DNL Adobe Experience Platform Data Ingestion]](../ingestion/home.md)：傳送資料給[!DNL Experience Platform]的方法。
- [[!DNL Experience Data Model (XDM) System]](../xdm/home.md)： [!DNL Experience Platform]用來組織客戶體驗資料的標準化架構。

## 對應集語法

對應集由ID、名稱、輸入結構描述、輸出結構描述和相關聯的對應清單組成。

以下JSON為典型對應集的範例：

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
| `id` | 對應集的唯一識別碼。 |
| `name` | 對應集的名稱。 |
| `inputSchema` | 傳入資料的XDM結構描述。 |
| `outputSchema` | 輸入資料將轉換為符合的XDM結構描述。 |
| `mappings` | 從來源結構描述到目的地結構描述的欄位對欄位對應陣列。 |
| `sourceType` | 對於每個列出的對應，其`sourceType`屬性會指出要對應的來源型別。 可以是`ATTRIBUTE`、`STATIC`或`EXPRESSION`其中之一： <ul><li> `ATTRIBUTE`用於來源路徑中找到的任何值。 </li><li>`STATIC`用於插入至目的地路徑的值。 此值會保持不變，不受來源結構描述的影響。</li><li> `EXPRESSION`用於運算式，將在執行階段進行解析。 可以在[對應函式指南](./functions.md)中找到可用運算式的清單。</li> </ul> |
| `source` | 對於每個列出的對應，`source`屬性會指出您要對應的欄位。 如需有關如何設定來源的詳細資訊，請參閱[來源概觀](../sources/home.md)。 |
| `destination` | 對於每個列出的對應，`destination`屬性會指出欄位，或是將放置從`source`欄位擷取之值的欄位路徑。 如需如何設定目的地的詳細資訊，請參閱[目的地概觀](../destinations/home.md)。 |
| `mappings.name` | （*選擇性*）對應的名稱。 |
| `mappings.description` | (*Optional*)對應的描述。 |

## 設定對應來源

在對映中，`source`可以是欄位、運算式或靜態值。 根據給定的來源型別，可以透過多種方式擷取值。

### 欄位資料中的欄位

在欄位資料（例如CSV檔案）中對應欄位時，請使用`ATTRIBUTE`來源型別。 如果欄位名稱中包含`.`，請使用`\`來逸出值。 此對應的範例可在以下找到：

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

**轉換的資料**

```json
{
    "pi": {
        "name": "John Smith"
    }
}
```

### 巢狀資料中的欄位

在巢狀資料（例如JSON檔案）中對應欄位時，請使用`ATTRIBUTE`來源型別。 如果欄位名稱中包含`.`，請使用`\`來逸出值。 此對應的範例可在以下找到：

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

**轉換的資料**

```json
{
    "pi": {
        "name": "John Smith"
    }
}
```

### 陣列中的欄位

對映陣列中的欄位時，您可以使用索引來擷取特定值。 若要這麼做，請使用`ATTRIBUTE`來源型別以及您要對應的值的索引。 此對應的範例可在以下找到：

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

**轉換的資料**

```json
{
    "pi": {
        "email": "js@example.com"
    }
}
```

### 陣列到陣列或物件到物件

使用`ATTRIBUTE`來源型別，您也可以直接將陣列對應至陣列，或將物件對應至物件。 此對應的範例可在以下找到：

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

### 陣列上的反複運算

使用`ATTRIBUTE`來源型別，您可以使用萬用字元索引(`[*]`)，重複地循環陣列並將它們對應到目標結構描述。 此對應的範例可在以下找到：

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

如果要對應常數或靜態值，請使用`STATIC`來源型別。  使用`STATIC`來源型別時，`source`代表您要指派給`destination`的硬式編碼值。 此對應的範例可在以下找到：

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

**轉換的資料**

```json
{
    "userType:": "CUSTOMER"
}
```

### 運算式

如果要對應運算式，請使用`EXPRESSION`來源型別。 可以在[對應函式指南](./functions.md)中找到接受的函式清單。 使用`EXPRESSION`來源型別時，`source`代表您要解析的函式。 此對應的範例可在以下找到：

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

**轉換的資料**

```json
{
    "pi": {
        "created": "SMITHJOHNFri Sep 25 15:17:31 PDT 2020"
    }
}
```

## 設定對應目的地

在對映中，`destination`是將從`source`擷取的值插入的位置。

### 根層級的欄位

當您想要將`source`值對應到轉換後資料的根層級時，請遵循下列範例：

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

**轉換的資料**

```json
{
    "name": "John Smith"
}
```

### 巢狀欄位

當您想要將`source`值對應到轉換資料中的巢狀欄位時，請遵循下列範例：

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

**轉換的資料**

```json
{
    "pi": {
        "name": "John Smith"
    }
}
```

### 位於特定陣列索引的欄位

當您想要將`source`值對應到轉換資料中陣列中的特定索引時，請遵循以下範例：

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

**轉換的資料**

```json
{
    "piList": ["John Smith"]
}
```

### 反複陣列操作

當您想要反複循環陣列並將值對應到目標時，可以使用萬用字元索引(`[*]`)。 其範例如下：

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

閱讀本檔案後，您現在應該瞭解對應集的建構方式，包括如何在對應集中設定個別對應。 如需其他資料準備功能的詳細資訊，請閱讀[資料準備總覽](./home.md)。 若要瞭解如何在資料準備API中使用對應集，請閱讀[資料準備開發人員指南](./api/overview.md)。
