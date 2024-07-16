---
title: 在Reactor API中篩選回應
description: 瞭解如何在Reactor API中列出資源時篩選結果。
exl-id: 8a91f3dd-4ead-4a10-abb1-e71acb0d73b6
source-git-commit: 47a94b00e141b24203b01dc93834aee13aa6113c
workflow-type: tm+mt
source-wordcount: '551'
ht-degree: 1%

---

# 在Reactor API中篩選回應

在Reactor API中使用清單(GET)端點時，您可能會發現有必要將傳回的結果限製為記錄子集。 為達此目的，許多API的清單端點都支援依特定屬性篩選的功能。 如果您想改對API進行結構化查詢，請參閱[搜尋](./search.md)指南。

## 篩選語法

以下範例說明如何為GET請求實作篩選器。

**API格式**

若要篩選指定清單端點的回應，您必須在要求路徑中提供`filter`查詢引數。

>[!NOTE]
>
>下面的範本使用方括弧(`[]`)和空格字元來達到可讀性。 實際上，這些字元必須是URI編碼，如[RFC 3986](https://tools.ietf.org/html/rfc3986)中所述。 本指南稍後會顯示正確編碼的請求路徑範例。
>
>請注意，如果篩選器的結構不正確，則不會套用任何篩選器並傳回完整結果集。

```http
GET {ENDPOINT}?filter[{ATTRIBUTE_NAME}]={OPERATOR} {VALUE}
```

| 屬性 | 說明 |
| --- | --- |
| `{ENDPOINT}` | Reactor API中支援篩選器引數的清單端點。 |
| `{ATTRIBUTE_NAME}` | 篩選結果所依據的特定屬性的名稱。 請記住，不同的端點支援不同的篩選屬性。 如需可用篩選屬性的清單，請參閱您使用之端點的參考指南。 |
| `{OPERATOR}` | 決定如何針對提供的`{VALUE}`評估結果的運運算元。 支援的運運算元列在[附錄區段](#supported-operators)中。 |
| `{VALUE}` | 用來比較傳回結果的值。 使用`EQ`運運算元比較相等時，值必須是完全相符且區分大小寫的相符專案，才能包含在回應中。 |

{style="table-layout:auto"}

**要求**

下列範例要求套用篩選器，要求程式庫的`state`屬性等於`published`，以擷取已發佈程式庫的清單。

在URI編碼之前，請求路徑中此篩選器的語法如下所示：

`https://reactor.adobe.io/properties/PR906238a59bbf4262bcedba248f483600/libraries?filter[state]=EQ published`

路徑和查詢引數完成URI編碼後，便可用於API請求，如下所示：

```shell
curl -X GET \
  https://reactor.adobe.io/properties/PR906238a59bbf4262bcedba248f483600/libraries?filter%5Bstate%5D=EQ%20published \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}'
```

## 篩選多個值 {#multiple-values}

若要依單一屬性的多個值篩選，請以逗號分隔清單的形式提供這些值。

```http
GET {ENDPOINT}?filter[{ATTRIBUTE_NAME}]={OPERATOR} {VALUE_1},{VALUE_2}
```

## 使用多個篩選器

若要套用多個屬性的篩選器，請為每個屬性提供`filter`引數。 引數必須以&amp;字元(`&`)分隔。

```http
GET {ENDPOINT}?filter[{ATTRIBUTE_NAME_1}]={OPERATOR} {VALUE}&filter[{ATTRIBUTE_NAME_2}]={OPERATOR} {VALUE}
```

>[!NOTE]
>
>如果您在相同要求的多個篩選條件中指定相同的屬性，則只會套用最後為該屬性提供的篩選條件。

## 附錄

下節包含在Reactor API中使用篩選器的其他資訊。

### 支援的篩選器運運算元 {#operators}

下表列出篩選引數支援的運運算元值。 請記住，根據您篩選依據的屬性，並非所有可用的篩選運運算元都適用，例如對字串屬性使用「小於」或「大於」運運算元。

| 運算子 | 說明 |
| --- | --- |
| `EQ` | 屬性必須等於提供的值。 |
| `NOT` | 屬性不得等於提供的值。 |
| `LT` | 屬性必須小於提供的值。 |
| `GT` | 屬性必須大於提供的值。 |
| `BETWEEN` | 屬性必須落在指定的值範圍內。 使用此運運算元時，必須提供[兩個值](#multiple-values)，以表示所需範圍的最小值和最大值。 |
| `CONTAINS` | 屬性必須包含提供的值，例如字串屬性中的一組字元。 |
