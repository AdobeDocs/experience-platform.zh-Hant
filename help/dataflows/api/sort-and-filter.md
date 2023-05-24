---
title: 對流服務API中的響應進行排序和篩選
description: 本教程介紹使用Flow Service API中的查詢參數（包括一些高級使用案例）進行排序和篩選的語法。
exl-id: 029c3199-946e-4f89-ba7a-dac50cc40c09
source-git-commit: ef8db14b1eb7ea555135ac621a6c155ef920e89a
workflow-type: tm+mt
source-wordcount: '586'
ht-degree: 3%

---

# 對流服務API中的響應進行排序和篩選

在中執行清單(GET)請求時 [流服務API](https://www.adobe.io/experience-platform-apis/references/flow-service/)，您可以使用查詢參數對響應進行排序和篩選。 本指南提供了有關如何將這些參數用於不同使用情形的參考。

## 排序

可以使用 `orderby` 查詢參數。 可以在API中對以下資源進行排序：

* [連線](https://www.adobe.io/experience-platform-apis/references/flow-service/#tag/Connections)
* [源連接](https://www.adobe.io/experience-platform-apis/references/flow-service/#tag/Source-connections)
* [目標連接](https://www.adobe.io/experience-platform-apis/references/flow-service/#tag/Target-connections)
* [流](https://www.adobe.io/experience-platform-apis/references/flow-service/#tag/Flows)
* [運行](https://www.adobe.io/experience-platform-apis/references/flow-service/#tag/Runs)

要使用參數，必須將其值設定為要排序的特定屬性(例如， `?orderby=name`)。 可以用加號(`+`)，用於升序或減號(`-`)。 如果未提供排序前置詞，則預設情況下，清單按升序排序。

```http
GET /flows?orderby=name
GET /flows?orderby=-name
```

還可以使用「和」符號(`&`)。

```http
GET /flows?property=state==enabled&orderby=createdAt
```

## 篩選

可以使用 `property` 帶key-value表達式的參數。 比如說， `?property=id==12345` 僅返回資源 `id` 屬性等於 `12345`。

只要實體中任何屬性的有效路徑已知，過濾就可以通用地應用。

>[!NOTE]
>
>如果某個屬性嵌套在陣列項中，則必須附加方括弧(`[]`)到路徑中的陣列。 請參閱 [篩選陣列屬性](#arrays) 的上界。

**返回源表名稱為的所有源連接 `lead`:**

```http
GET /sourceConnections?property=params.tableName==lead
```

**返回特定段ID的所有流：**

```http
GET /flows?property=transformations[].params.segmentSelectors.selectors[].value.id==5722a16f-5e1f-4732-91b6-3b03943f759a
```

### 組合濾鏡

多重 `property` 如果篩選器以「和」字元分隔(`&`)。 組合濾鏡時假定為AND關係，這意味著實體必須滿足所有濾鏡才能包括在響應中。

**返回段ID的所有已啟用流：**

```http
GET /flows?property=transformations[].params.segmentSelectors.selectors[].value.id==5722a16f-5e1f-4732-91b6-3b03943f759a&property=state==enabled
```

### 篩選陣列屬性 {#arrays}

可以通過附加基於陣列中項的屬性進行篩選 `[]` 到陣列屬性的名稱。

**與特定源連接關聯的返回流：**

```http
GET /flows?property=sourceConnectionIds[]==9874984,6980696
```

**返回具有包含特定選擇器值ID的轉換的流：**

```http
GET /flows?property=transformations[].params.segmentSelectors.selectors[].value.id==5722a16f-5e1f-4732-91b6-3b03943f759a
```

**返回具有特定列的源連接 `name` 值：**

```http
GET /sourceConnections?property=params.columns[].name==firstName
```

**通過篩選段ID來查找目標的流運行ID:**

```http
GET /runs?property=metrics.recordSummary.targetSummaries[].entitySummaries[].id==segment:068d6e2c-b546-4c73-bfb7-9a9d33375659
```

### `count`

任何篩選查詢都可以附加 `count` 具有值的查詢參數 `true` 返回結果計數。 API響應包含 `count` 其值表示已篩選項總數的屬性。 此調用中不返回實際篩選的項。

**返回系統中已啟用的流計數：**

```http
GET /flows?property=state==enabled&count=true
```

對上述查詢的響應如下所示：

```json
{
  "count": 95
}
```

### 按資源可篩選的屬性

根據要檢索的流服務實體，可以使用不同的屬性進行篩選。 下表將列出篩選使用情形時常用的每個資源的根級別欄位。

**`connectionSpec`**

| 屬性 | 範例 |
| --- | --- |
| `id` | `/connectionSpecs?property=id==736873,9485095` |
| `name` | `/connectionSpecs?property=name==TestConn` |
| `providerId` | `/connectionSpecs?property=providerId==3897933` |
| `attributes.{ATTRIBUTE_NAME}` | `/connectionSpecs?property=attributes.sampleAttribute="abc"` |

{style="table-layout:auto"}

**`flowSpec`**

| 屬性 | 範例 |
| --- | --- |
| `id` | `/flowSpecs?property=id==736873,9485095` |
| `name` | `/flowSpecs?property=name==TestConn` |
| `providerId` | `/flowSpecs?property=providerId==3897933` |

{style="table-layout:auto"}

**`connection`**

| 屬性 | 範例 |
| --- | --- |
| `id` | `/connections?property=id==736873,9485095` |
| `name` | `/connections?property=name==TestConn` |
| `description` | `/connections?property=description==Test%20description` |
| `connectionSpec.id` | `/connections?property=connectionSpec.id==938903,849048` |
| `state` | `/connections?property=state==enabled` |

{style="table-layout:auto"}

**`sourceConnection`**

| 屬性 | 範例 |
| --- | --- |
| `id` | `/sourceConnections?property=id==736873,9485095` |
| `connectionSpec.id` | `/sourceConnections?property=connectionSpec.id==938903,849048` |
| `baseConnectionId` | `/sourceConnections?property=baseConnectionId==983908,4908095` |

{style="table-layout:auto"}

**`targetConnection`**

| 屬性 | 範例 |
| --- | --- |
| `id` | `/targetConnections?property=id==736873,9485095` |
| `connectionSpec.id` | `/targetConnections?property=connectionSpec.id==938903,849048` |
| `baseConnectionId` | `/targetConnections?property=baseConnectionId==983908,4908095` |

{style="table-layout:auto"}

**`flow`**

| 屬性 | 範例 |
| --- | --- |
| `id` | `/flows?property=id==736873,9485095` |
| `name` | `/flows?property=name==TestFlow` |
| `description` | `/flows?property=description==Test%20description` |
| `flowSpec.id` | `/flows?property=flowSpec.id==938903,849048` |
| `state` | `/flows?property=state==enabled` |
| `sourceConnectionIds` | `/flows?property=sourceConnectionIds[]==9874984,6980696` |
| `targetConnectionIds` | `/flows?property=targetConnectionIds[]==598590,690666` |

{style="table-layout:auto"}

**`run`**

| 屬性 | 範例 |
| --- | --- |
| `id` | `/runs?property=id==736873,9485095` |
| `flowId` | `/runs?property=flowId==8749844` |
| `state` | `/runs?property=state==inProgress` |

{style="table-layout:auto"}

## 後續步驟

本指南介紹如何使用 `orderby` 和 `property` 查詢參數以在流服務API中排序和篩選響應。 有關如何在平台中使用API來處理常用工作流的逐步指南，請參閱 [來源](../../sources/home.md) 和 [目的地](../../destinations/home.md) 文檔。
