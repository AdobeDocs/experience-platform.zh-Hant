---
title: 排序和篩選流程服務API中的回應
description: 本教學課程涵蓋使用流程服務API中的查詢引數排序和篩選的語法，包括一些進階使用案例。
exl-id: 029c3199-946e-4f89-ba7a-dac50cc40c09
source-git-commit: c7ff379b260edeef03f8b47f932ce9040eef3be2
workflow-type: tm+mt
source-wordcount: '863'
ht-degree: 2%

---

# 排序和篩選流程服務API中的回應

在中執行清單(GET)請求時 [流程服務API](https://www.adobe.io/experience-platform-apis/references/flow-service/)，您可使用查詢引數來排序和篩選回應。 本指南提供不同使用案例下如何使用這些引數的參考資料。

## 排序

您可以使用 `orderby` 查詢引數。 下列資源可在API中排序：

* [連線](https://www.adobe.io/experience-platform-apis/references/flow-service/#tag/Connections)
* [來源連線](https://www.adobe.io/experience-platform-apis/references/flow-service/#tag/Source-connections)
* [目標連線](https://www.adobe.io/experience-platform-apis/references/flow-service/#tag/Target-connections)
* [流程](https://www.adobe.io/experience-platform-apis/references/flow-service/#tag/Flows)
* [執行](https://www.adobe.io/experience-platform-apis/references/flow-service/#tag/Runs)

若要使用引數，您必須將其值設為排序所依據的特定屬性(例如， `?orderby=name`)。 您可以在值前面加上加號(`+`)作為遞增順序或減號(`-`)遞減排序。 如果未提供排序前置詞，清單預設會依遞增順序排序。

```http
GET /flows?orderby=name
GET /flows?orderby=-name
```

您也可以使用&quot;and&quot;符號(`&`)。

```http
GET /flows?property=state==enabled&orderby=createdAt
```

## 篩選

您可使用 `property` 使用索引鍵值運算式的引數。 例如， `?property=id==12345` 只傳回滿足以下條件的資源： `id` 屬性完全等於 `12345`.

只要已知屬性的有效路徑，篩選功能可一般套用至實體中的任何屬性。

>[!NOTE]
>
>如果屬性巢狀內嵌於陣列專案中，您必須附加方括弧(`[]`)至路徑中的陣列。 請參閱以下小節： [篩選陣列屬性](#arrays) 例如。

**傳回來源資料表名稱為的所有來源連線 `lead`：**

```http
GET /sourceConnections?property=params.tableName==lead
```

**傳回特定區段ID的所有流程：**

```http
GET /flows?property=transformations[].params.segmentSelectors.selectors[].value.id==5722a16f-5e1f-4732-91b6-3b03943f759a
```

### 組合篩選器

多個 `property` 篩選器必須以「和」字元(`&`)。 組合篩選器時會假設AND關係，這表示實體必須滿足所有篩選器，才能將其包含在回應中。

**傳回區段ID的所有已啟用流程：**

```http
GET /flows?property=transformations[].params.segmentSelectors.selectors[].value.id==5722a16f-5e1f-4732-91b6-3b03943f759a&property=state==enabled
```

### 篩選陣列屬性 {#arrays}

您可以藉由附加，根據陣列中專案的屬性進行篩選 `[]` 至陣列屬性的名稱。

**與特定來源連線相關聯的傳回流程：**

```http
GET /flows?property=sourceConnectionIds[]==9874984,6980696
```

**傳回含有特定選取器值ID之轉換的資料流：**

```http
GET /flows?property=transformations[].params.segmentSelectors.selectors[].value.id==5722a16f-5e1f-4732-91b6-3b03943f759a
```

**傳回來源連線，這些連線的欄具有特定的 `name` 值：**

```http
GET /sourceConnections?property=params.columns[].name==firstName
```

**透過篩選區段ID來查詢目的地的資料流執行ID：**

```http
GET /runs?property=metrics.recordSummary.targetSummaries[].entitySummaries[].id==segment:068d6e2c-b546-4c73-bfb7-9a9d33375659
```

### `count`

任何篩選查詢都可以附加 `count` 具有值的查詢引數 `true` 以傳回結果的計數。 API回應包含 `count` 其值代表已篩選專案總數的屬性。 此呼叫中未傳回實際篩選的專案。

**傳回系統中已啟用的資料流的計數：**

```http
GET /flows?property=state==enabled&count=true
```

上述查詢的回應如下所示：

```json
{
  "count": 95
}
```

### 可依資源篩選的屬性

根據您正在擷取的流程服務實體，可能會使用不同的屬性進行篩選。 下錶針對篩選使用案例中常用的每個資源，劃分根層級欄位。

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

## 使用案例 {#use-cases}

閱讀本節內容，瞭解如何使用篩選和排序功能傳回特定聯結器的相關資訊，或協助您偵錯問題的特定範例。 如果您想要Adobe新增任何其他使用案例，請使用 **[!UICONTROL 詳細的意見回饋選項]** ，以提交請求。

**篩選以僅傳回特定目的地的連線**

您可以使用篩選器來只將連線傳回某些目的地。 首先，查詢 `connectionSpecs` 端點如下：

```http
GET /connectionSpecs
```

接著，搜尋您想要的 `connectionSpec` 透過檢查 `name` 引數。 例如，搜尋Amazon Ads、Pega或SFTP，以此類推 `name` 引數。 對應的 `id` 是 `connectionSpec` 供您在下一個API呼叫中搜尋的依據。

例如，篩選您的目的地以僅傳回與Amazon S3連線的現有連線：

```http
GET /connections?property=connectionSpec.id==4890fc95-5a1f-4983-94bb-e060c08e3f81
```

**篩選以僅傳回資料流至目的地**

查詢時 `/flows` 端點不使用傳回所有來源和目的地資料流，而是您可以使用篩選器來僅傳回資料流到目的地。 若要這麼做，請使用 `isDestinationFlow` 作為查詢引數，如下所示：

```http
GET /flows?property=inheritedAttributes.properties.isDestinationFlow==true
```

**篩選以僅將資料流傳回特定來源或目的地**

您可以篩選資料流，以將資料流傳回特定目的地或僅從特定來源。 例如，篩選您的目的地以僅傳回與Amazon S3連線的現有連線：

```http
GET /flows?property=inheritedAttributes.targetConnections[].connectionSpec.id==4890fc95-5a1f-4983-94bb-e060c08e3f81
```

**篩選以取得特定時段內所有資料流執行**

您可以篩選資料流的資料流執行，以僅檢視特定時間間隔內的執行，如下所示：

```
GET /runs?property=flowId==<flow-id>&property=metrics.durationSummary.startedAtUTC>1593134665781&property=metrics.durationSummary.startedAtUTC<1653134665781
```

**篩選以僅傳回失敗的資料流**

為了進行偵錯，您可以篩選並檢視特定來源或目的地資料流的所有失敗資料流執行，如下所示：

```http
GET /runs?property=flowId==<flow-id>&property=metrics.statusSummary.status==Failed
```

## 後續步驟

本指南說明如何使用 `orderby` 和 `property` 查詢引數，用於排序和篩選流程服務API中的回應。 如需如何將API用於Platform中常見工作流程的逐步指南，請參閱 [來源](../../sources/home.md) 和 [目的地](../../destinations/home.md) 檔案。
