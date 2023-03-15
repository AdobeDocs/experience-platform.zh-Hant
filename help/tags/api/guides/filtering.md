---
title: 篩選Reactor API中的回應
description: 了解在Reactor API中列出資源時如何篩選結果。
exl-id: 8a91f3dd-4ead-4a10-abb1-e71acb0d73b6
source-git-commit: 47a94b00e141b24203b01dc93834aee13aa6113c
workflow-type: tm+mt
source-wordcount: '553'
ht-degree: 1%

---

# 篩選Reactor API中的回應

在Reactor API中使用清單(GET)端點時，您可能會發現有必要將傳回的結果限制為記錄子集。 為達此目的，API的許多清單端點都支援依特定屬性篩選的功能。 如果您想要改為對API進行結構化查詢，請參閱上的指南 [搜尋](./search.md).

## 篩選語法

下列範例說明如何為您的GET請求實作篩選。

**API格式**

若要篩選指定清單端點的回應，您必須提供 `filter` 請求路徑中的查詢參數。

>[!NOTE]
>
>以下範本使用方括弧(`[]`)和空格字元以利閱讀。 實際上，這些字元必須經過URI編碼，如 [RFC 3986](https://tools.ietf.org/html/rfc3986). 正確編碼的請求路徑範例如本指南稍後所示。
>
>請注意，如果篩選器的結構不正確，則不會套用任何篩選器，並會傳回完整的結果集。

```http
GET {ENDPOINT}?filter[{ATTRIBUTE_NAME}]={OPERATOR} {VALUE}
```

| 屬性 | 說明 |
| --- | --- |
| `{ENDPOINT}` | 支援篩選參數的Reactor API中的清單端點。 |
| `{ATTRIBUTE_NAME}` | 要按篩選結果的特定屬性的名稱。 請記住，不同的端點支援不同的篩選屬性。 請參閱參考指南，了解您正在使用的端點，以取得可用篩選屬性的清單。 |
| `{OPERATOR}` | 用於確定如何根據提供的結果評估結果的運算子 `{VALUE}`. 支援的運算子列於 [附錄](#supported-operators). |
| `{VALUE}` | 比較傳回結果的值。 比較相等時，使用 `EQ` 運算子，值必須是完全、區分大小寫的相符項目，才會包含在回應中。 |

{style="table-layout:auto"}

**要求**

下列範例要求會套用需要程式庫的篩選器，以擷取已發佈程式庫的清單 `state` 屬性等於 `published`.

在URI編碼之前，請求路徑中此篩選器的語法看起來類似於以下內容：

`https://reactor.adobe.io/properties/PR906238a59bbf4262bcedba248f483600/libraries?filter[state]=EQ published`

路徑和查詢參數經過URI編碼後，即可用於API請求，如下所示：

```shell
curl -X GET \
  https://reactor.adobe.io/properties/PR906238a59bbf4262bcedba248f483600/libraries?filter%5Bstate%5D=EQ%20published \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}'
```

## 篩選多個值 {#multiple-values}

若要依單一屬性的多個值進行篩選，請以逗號分隔的清單提供值。

```http
GET {ENDPOINT}?filter[{ATTRIBUTE_NAME}]={OPERATOR} {VALUE_1},{VALUE_2}
```

## 使用多個篩選器

若要套用多個屬性的篩選器，請提供 `filter` 參數。 參數必須以&amp;符號分隔(`&`)字元。

```http
GET {ENDPOINT}?filter[{ATTRIBUTE_NAME_1}]={OPERATOR} {VALUE}&filter[{ATTRIBUTE_NAME_2}]={OPERATOR} {VALUE}
```

>[!NOTE]
>
>如果您在同一請求的多個篩選器中指定相同的屬性，則只會套用該屬性最後提供的篩選器。

## 附錄

下節包含在Reactor API中使用篩選器的其他資訊。

### 支援的篩選運算子 {#operators}

下表列出了支援的篩選參數運算子值。 請記得，根據您要篩選的屬性，並非所有可用的篩選運算子都適用，例如對字串屬性使用「小於」或「大於」運算子。

| 運算子 | 說明 |
| --- | --- |
| `EQ` | 屬性必須等於提供的值。 |
| `NOT` | 屬性不得等於提供的值。 |
| `LT` | 屬性必須小於提供的值。 |
| `GT` | 屬性必須大於提供的值。 |
| `BETWEEN` | 屬性必須落在指定的值範圍內。 使用此運算子時， [兩個值](#multiple-values) 必須提供，以指出所需範圍的最小值和最大值。 |
| `CONTAINS` | 屬性必須包含提供的值，例如字串屬性內的字元集。 |
