---
title: 在反應器API中篩選響應
description: 瞭解在Repartor API中列出資源時如何篩選結果。
exl-id: 8a91f3dd-4ead-4a10-abb1-e71acb0d73b6
source-git-commit: 47a94b00e141b24203b01dc93834aee13aa6113c
workflow-type: tm+mt
source-wordcount: '553'
ht-degree: 1%

---

# 在反應器API中篩選響應

在Reactor API中使用清單(GET)端點時，您可能會發現有必要將返回的結果限制為記錄的子集。 為此，許多API的清單端點都支援按特定屬性進行篩選的能力。 如果希望對API進行結構化查詢，請參閱上的指南 [搜索](./search.md)。

## 篩選語法

以下示例說明如何為您的GET請求實施篩選器。

**API格式**

要篩選給定清單終結點的響應，必須提供 `filter` 請求路徑中的查詢參數。

>[!NOTE]
>
>下面的模板使用方括弧(`[]`)和空格字元，以便閱讀。 實際上，這些字元必須是URI編碼的，如中所述 [RFC 3986](https://tools.ietf.org/html/rfc3986)。 本指南後面顯示了正確編碼的請求路徑示例。
>
>請注意，如果篩選器的結構不正確，則不應用篩選器，並返回完整的結果集。

```http
GET {ENDPOINT}?filter[{ATTRIBUTE_NAME}]={OPERATOR} {VALUE}
```

| 屬性 | 說明 |
| --- | --- |
| `{ENDPOINT}` | 支援篩選器參數的Reactor API中的清單終結點。 |
| `{ATTRIBUTE_NAME}` | 要按篩選結果的特定屬性的名稱。 請記住，不同的端點支援不同的篩選屬性。 有關您正在使用的端點的參考指南，請參閱可用過濾屬性清單。 |
| `{OPERATOR}` | 確定如何根據提供的結果評估結果的運算子 `{VALUE}`。 支援的運算子列於 [附錄部分](#supported-operators)。 |
| `{VALUE}` | 要將返回的結果與之進行比較的值。 當使用 `EQ` 運算子，該值必須精確且區分大小寫，才能包括在響應中。 |

{style="table-layout:auto"}

**要求**

下面的示例請求通過應用需要庫的篩選器來檢索已發佈庫的清單 `state` 屬性等於 `published`。

在URI編碼之前，請求路徑中此篩選器的語法如下所示：

`https://reactor.adobe.io/properties/PR906238a59bbf4262bcedba248f483600/libraries?filter[state]=EQ published`

一旦路徑和查詢參數已經URI編碼，就可以在API請求中使用，如下所示：

```shell
curl -X GET \
  https://reactor.adobe.io/properties/PR906238a59bbf4262bcedba248f483600/libraries?filter%5Bstate%5D=EQ%20published \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}'
```

## 對多個值進行篩選 {#multiple-values}

要按單個屬性的多個值進行篩選，請將這些值作為逗號分隔的清單提供。

```http
GET {ENDPOINT}?filter[{ATTRIBUTE_NAME}]={OPERATOR} {VALUE_1},{VALUE_2}
```

## 使用多個篩選器

要應用多個屬性的篩選器，請提供 `filter` 參數。 參數必須用和符分隔(`&`)字元。

```http
GET {ENDPOINT}?filter[{ATTRIBUTE_NAME_1}]={OPERATOR} {VALUE}&filter[{ATTRIBUTE_NAME_2}]={OPERATOR} {VALUE}
```

>[!NOTE]
>
>如果在同一請求上在多個篩選器中指定同一屬性，則將只應用該屬性的最後一個提供的篩選器。

## 附錄

以下部分包含有關在Reactor API中使用篩選器的其他資訊。

### 支援的篩選器運算子 {#operators}

下表列出了篩選器參數支援的運算子值。 請記住，根據篩選依據的屬性，並非所有可用的篩選器運算子都適用，例如對字串屬性使用「小於」或「大於」運算子。

| 運算子 | 說明 |
| --- | --- |
| `EQ` | 該屬性必須等於提供的值。 |
| `NOT` | 該屬性不能等於提供的值。 |
| `LT` | 該屬性必須小於提供的值。 |
| `GT` | 屬性必須大於提供的值。 |
| `BETWEEN` | 該屬性必須位於指定的值範圍內。 使用此運算子時， [兩個值](#multiple-values) 必須提供以指示所需範圍的最小值和最大值。 |
| `CONTAINS` | 該屬性必須包含提供的值，如字串屬性中的一組字元。 |
