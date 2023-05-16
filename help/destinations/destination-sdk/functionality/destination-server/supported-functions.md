---
description: Experience PlatformDestination SDK使用Pebble模板，將從Experience Platform導出的資料轉換為目標所需的格式。
title: 支援的Destination SDK轉換函式
source-git-commit: ab87a2b7190a0365729ba7bad472fde7a489ec02
workflow-type: tm+mt
source-wordcount: '579'
ht-degree: 3%

---


# 支援的Destination SDK轉換函式

Experience PlatformDestination SDK使用 [[!DNL Pebble] 範本](https://pebbletemplates.io/)，可讓您將從Experience Platform匯出的資料轉換為目的地所需的格式。

Experience Platform [!DNL Pebble] 與提供的現成版本相比，實作有一些變更 [!DNL Pebble]. 此外，除了 [!DNL Pebble],Adobe已建立一些可搭配Destination SDK使用的額外函式。

>[!IMPORTANT]
>
>Destination SDK支援的所有參數名稱和值均為 **區分大小寫**. 為避免區分大小寫錯誤，請使用參數名稱和值，如說明檔案所示。

## 使用位置 {#where-to-use}

若 [建立訊息轉換範本](../../testing-api/streaming-destinations/create-template.md) 從Experience Platform匯出至目的地的資料。

訊息轉換範本用於 [目標伺服器配置](templating-specs.md) 用於串流目的地。

## 先決條件 {#prerequisites}

若要了解此參考頁面中的概念和功能，請閱讀 [訊息格式](message-format.md) 檔案。 您需要了解 [輪廓結構](message-format.md#profile-structure) 在Experience Platform中 [!DNL Pebble] 要轉換的範本和匯出的資料。

在前往下文說明的功能之前，請先檢閱區段中的範本範例 [使用範本語言進行身分、屬性和區段成員資格轉換](message-format.md#using-templating). 這裡的例子開始非常簡單，而且複雜性也在增加。

## 支援 [!DNL Pebble] 函式 {#supported-functions}

從 [!DNL Pebble] 標籤區段，Destination SDK僅支援：

* [篩選](https://pebbletemplates.io/wiki/tag/filter/)
* [for](https://pebbletemplates.io/wiki/tag/for/)
* [if](https://pebbletemplates.io/wiki/tag/if/)
* [set](https://pebbletemplates.io/wiki/tag/set/)

>[!TIP]
>
>使用 `for` 迭代時不同 *陣列* 或 *地圖* 範本中的元素。 當您逐一查看陣列時，可以直接取得元素。 當您逐一查看地圖時，會取得每個地圖項目，其中都有索引鍵值組。
>
> * 如需陣列元素的範例，請思考 [identityMap](message-format.md#identities) 命名空間，您可在其中反覆查看元素，例如 `identityMap.gaid`, `identityMap.email`、或類似。
> * 如需地圖元素的範例，請思考 [segmentMembership](message-format.md#segment-membership).


從 [!DNL Pebble] 篩選區段，Destination SDK支援所有功能。 以下進一步的範例說明 `date` 函式。

從 [!DNL Pebble] 函式部分，Adobe執行 *not* 支援 [範圍](https://pebbletemplates.io/wiki/function/range/) 函式。

## 範例，說明 `date` 函式。 {#date-function}

以示範 [!DNL Pebble] 函式用於Destination SDK中，請參閱下方的日期函式([Pebble檔案中的連結](https://pebbletemplates.io/wiki/filter/date/))來轉換時間戳記的格式。

### 使用案例

您想要變更 `lastQualificationTime` 預設時間戳記 [ISO 8601](https://en.wikipedia.org/wiki/ISO_8601) Experience Platform匯出至目的地所偏好的其他值的值。

### 範例

#### 輸入

```json
{
"lastQualificationTime": "2022-02-08T18:34:24.000+0000"
}
```

#### 格式

```java
{{ lastQualificationTime | date(existingFormat="yyyy-MM-dd'T'HH:mm:sss.SSSX", format="yyyy-MM-dd'T'HH:mm:ssX") }}
```

#### 輸出

```json
{
"lastQualificationTime": "2022-02-21T18:34:24Z"
}
```

## 依Adobe新增的函式 {#functions-added-by-adobe}

除了 [!DNL Pebble]，請參閱下方可供匯出資料的Adobe所建立的其他函式。

### `addedSegments` 和 `removedSegments` 函式 {#addedsegments-removedsegments-functions}

#### 使用案例

這些函式可用來取得已新增至設定檔或從設定檔移除的區段清單。

#### 範例

##### 輸入

```json
{
  "identityMap": {
    "myIdNamespace": [
      {
        "id": "external_id1"
      },
      {
        "id": "external_id2"
      }
    ]
  },
  "segmentMembership": {
    "ups": {
      "111111": {
        "lastQualificationTime": "2019-11-20T13:15:49Z",
        "status": "realized"
      },
      "222222": {
        "lastQualificationTime": "2019-11-20T13:15:49Z",
        "status": "exited"
      },
      "333333": {
        "lastQualificationTime": "2019-11-20T13:15:49Z",
        "status": "realized"
      }
    }
  }
}
```

##### 格式

```java
added: {% for s in addedSegments(segmentMembership.ups) %}<{{s.key}}>{% endfor %}; removed: {% for s in removedSegments(segmentMembership.ups) %}<{{s.key}}>{% endfor %}
```

##### 輸出

```json
added: <111111><333333>; removed: <222222>
```

<!--

### Added and removed segments filters {#added-and-removed-segmnts-filters}

#### Use case {#use-case}

These filters are similar to `addedSegments` and `removedSegments`, described above. The only difference is that they are implemented as filters as opposed to functions.

#### Example {#example}

##### Input {#input}

```json
{
  "identityMap": {
    "myIdNamespace": [
      {
        "id": "external_id1"
      },
      {
        "id": "external_id2"
      }
    ]
  },
  "segmentMembership": {
    "ups": {
      "111111": {
        "lastQualificationTime": "2019-11-20T13:15:49Z",
        "status": "realized"
      },
      "222222": {
        "lastQualificationTime": "2019-11-20T13:15:49Z",
        "status": "exited"
      },
      "333333": {
        "lastQualificationTime": "2019-11-20T13:15:49Z",
        "status": "realized"
      }
    }
  }
}
```

##### Format {#format}

```java
added: {% for s in input.profile.segmentMembership.ups | added %}<{{s.key}}>{% endfor %};|removed: {% for s in input.profile.segmentMembership.ups | removed %}<{{s.key}}>{% endfor %};
```

##### Output {#output}

```json
added: <111111><333333>;|removed: <222222>;
```

-->

## 後續步驟 {#next-steps}

你現在知道 [!DNL Pebble] Destination SDK支援函式，以及如何使用函式來調整匯出資料的格式，以符合您的需求。 接下來，您應檢閱下列頁面：

* [建立並測試訊息轉換範本](../../testing-api/streaming-destinations/create-template.md)
* [呈現範本API操作](../../testing-api/streaming-destinations/render-template-api.md)
