---
title: 排序和篩選流量服務API中的回應
description: 本教學課程涵蓋使用流量服務API中的查詢參數來排序和篩選的語法，包括一些進階使用案例。
source-git-commit: ccca81357bd7d7083abd3f395aa547c85ebf65fd
workflow-type: tm+mt
source-wordcount: '607'
ht-degree: 6%

---

# 排序和篩選流量服務API中的回應

在[流量服務API](https://www.adobe.io/experience-platform-apis/references/flow-service/)中執行清單(GET)請求時，您可以使用查詢參數來排序和篩選回應。 本指南提供如何針對不同使用案例使用這些參數的參考資料。

## 排序

您可以使用`orderby`查詢參數來排序回應。 可在API中排序下列資源：

* [連線](https://www.adobe.io/experience-platform-apis/references/flow-service/#tag/Connections)
* [源連接](https://www.adobe.io/experience-platform-apis/references/flow-service/#tag/Source-connections)
* [目標連線](https://www.adobe.io/experience-platform-apis/references/flow-service/#tag/Target-connections)
* [流量](https://www.adobe.io/experience-platform-apis/references/flow-service/#tag/Flows)
* [執行](https://www.adobe.io/experience-platform-apis/references/flow-service/#tag/Runs)

若要使用參數，必須將其值設定為您要排序的特定屬性（例如`?orderby=name`）。 您可以在值的開頭加上升順序的加號(`+`)，或以下降順序的加號(`-`)。 如果未提供排序前置詞，則清單預設會以升序排序。

```http
GET /flows?orderby=name
GET /flows?orderby=-name
```

您也可以使用&quot;and&quot;符號(`&`)，將排序參數與篩選參數結合。

```http
GET /flows?property=state==enabled&orderby=createdAt
```

## 篩選

您可以使用`property`參數搭配機碼值運算式來篩選回應。 例如， `?property=id==12345`僅傳回其`id`屬性恰好等於`12345`的資源。

只要已知該屬性的有效路徑，則可通常對實體中的任何屬性套用篩選。

>[!NOTE]
>
>如果屬性嵌套在陣列項中，則必須將方括弧(`[]`)附加到路徑中的陣列。 如需範例，請參閱[篩選陣列屬性的相關章節](#arrays)。

**返回源表名為的所有源連 `lead`接：**

```http
GET /sourceConnections?property=params.tableName==lead
```

**傳回特定區段ID的所有流量：**

```http
GET /flows?property=transformations[].params.segmentSelectors.selectors[].value.id==5722a16f-5e1f-4732-91b6-3b03943f759a
```

### 合併篩選器

若多個`property`篩選器以&quot;and&quot;字元(`&`)分隔，則可納入查詢中。 合併篩選器時會假設為AND關係，這表示實體必須滿足所有篩選器，才能將其納入回應中。

**傳回區段ID的所有已啟用流程：**

```http
GET /flows?property=transformations[].params.segmentSelectors.selectors[].value.id==5722a16f-5e1f-4732-91b6-3b03943f759a&property=state==enabled
```

### 篩選陣列屬性 {#arrays}

您可以將`[]`附加至陣列屬性的名稱，以根據陣列內項目的屬性進行篩選。

**與特定源連接關聯的返回流：**

```http
GET /flows?property=sourceConnectionIds[]==9874984,6980696
```

**具有包含特定選擇器值ID之轉換的傳回流：**

```http
GET /flows?property=transformations[].params.segmentSelectors.selectors[].value.id==5722a16f-5e1f-4732-91b6-3b03943f759a
```

**返回具有特定值的列的源 `name` 連接：**

```http
GET /sourceConnections?property=params.columns[].name==firstName
```

**依區段ID篩選，以查找目的地的流程執行ID:**

```http
GET /runs?property=metrics.recordSummary.targetSummaries[].entitySummaries[].id==segment:068d6e2c-b546-4c73-bfb7-9a9d33375659
```

### `count`

任何篩選查詢都可附加`count`查詢參數，其值為`true`，以傳回結果計數。 API回應包含`count`屬性，其值代表篩選項目總數的計數。 此呼叫不會傳回實際篩選的項目。

**返回系統中已啟用流的計數：**

```http
GET /flows?property=state==enabled&count=true
```

對上述查詢的回應如下所示：

```json
{
  "count": 95
}
```

### 可按資源篩選的屬性

根據要檢索的流服務實體，可以使用不同的屬性進行篩選。 下表劃分了篩選使用案例中常用的每個資源的根級別欄位。

**`connectionSpec`**

| 屬性 | 範例 |
| --- | --- |
| `id` | `/connectionSpecs?property=id==736873,9485095` |
| `name` | `/connectionSpecs?property=name==TestConn` |
| `providerId` | `/connectionSpecs?property=providerId==3897933` |
| `attributes.{ATTRIBUTE_NAME}` | `/connectionSpecs?property=attributes.sampleAttribute="abc"` |

{style=&quot;table-layout:auto&quot;}

**`flowSpec`**

| 屬性 | 範例 |
| --- | --- |
| `id` | `/flowSpecs?property=id==736873,9485095` |
| `name` | `/flowSpecs?property=name==TestConn` |
| `providerId` | `/flowSpecs?property=providerId==3897933` |

{style=&quot;table-layout:auto&quot;}

**`connection`**

| 屬性 | 範例 |
| --- | --- |
| `id` | `/connections?property=id==736873,9485095` |
| `name` | `/connections?property=name==TestConn` |
| `description` | `/connections?property=description==Test%20description` |
| `connectionSpec.id` | `/connections?property=connectionSpec.id==938903,849048` |
| `state` | `/connections?property=state==enabled` |

{style=&quot;table-layout:auto&quot;}

**`sourceConnection`**

| 屬性 | 範例 |
| --- | --- |
| `id` | `/sourceConnections?property=id==736873,9485095` |
| `connectionSpec.id` | `/sourceConnections?property=connectionSpec.id==938903,849048` |
| `baseConnectionId` | `/sourceConnections?property=baseConnectionId==983908,4908095` |

{style=&quot;table-layout:auto&quot;}

**`targetConnection`**

| 屬性 | 範例 |
| --- | --- |
| `id` | `/targetConnections?property=id==736873,9485095` |
| `connectionSpec.id` | `/targetConnections?property=connectionSpec.id==938903,849048` |
| `baseConnectionId` | `/targetConnections?property=baseConnectionId==983908,4908095` |

{style=&quot;table-layout:auto&quot;}

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

{style=&quot;table-layout:auto&quot;}

**`run`**

| 屬性 | 範例 |
| --- | --- |
| `id` | `/runs?property=id==736873,9485095` |
| `flowId` | `/runs?property=flowId==8749844` |
| `state` | `/runs?property=state==inProgress` |

{style=&quot;table-layout:auto&quot;}

## 後續步驟

本指南說明如何使用`orderby`和`property`查詢參數來排序和篩選流量服務API中的回應。 如需如何在Platform中使用API進行常見工作流程的逐步指南，請參閱[sources](../../sources/home.md)和[destinations](../../destinations/home.md)檔案中的API教學課程。
