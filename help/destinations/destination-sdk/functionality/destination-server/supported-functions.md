---
description: Experience PlatformDestination SDK使用Pebble模板，允許您將從Experience Platform導出的資料轉換為目標所需的格式。
title: 支援的轉換函式在Destination SDK
source-git-commit: ab87a2b7190a0365729ba7bad472fde7a489ec02
workflow-type: tm+mt
source-wordcount: '579'
ht-degree: 3%

---


# 支援的轉換函式在Destination SDK

Experience PlatformDestination SDK使用 [[!DNL Pebble] 模板](https://pebbletemplates.io/)，允許您將從Experience Platform導出的資料轉換為目標所需的格式。

Experience Platform [!DNL Pebble] 與提供的現成版本相比，實現有一些更改 [!DNL Pebble]。 此外，除了提供的 [!DNL Pebble],Adobe已建立了一些可與Destination SDK一起使用的附加函式。

>[!IMPORTANT]
>
>Destination SDK支援的所有參數名和值均 **區分大小寫**。 為避免區分大小寫錯誤，請完全按文檔所示使用參數名稱和值。

## 使用位置 {#where-to-use}

使用本頁下面列出的支援的函式 [建立消息轉換模板](../../testing-api/streaming-destinations/create-template.md) 將資料從Experience Platform導出到目標。

消息轉換模板用於 [目標伺服器配置](templating-specs.md) 流目標。

## 先決條件 {#prerequisites}

要瞭解此參考頁中的概念和功能，請閱讀 [消息格式](message-format.md) 的雙曲餘切值。 你得明白 [輪廓結構](message-format.md#profile-structure) 在Experience Platform中 [!DNL Pebble] 轉換和導出資料的模板。

在前進到下面介紹的功能之前，請查看一節中的模板示例 [使用模板語言進行身份、屬性和段成員身份轉換](message-format.md#using-templating)。 這裡的例子開始非常簡單並且複雜性增加。

## 支援 [!DNL Pebble] 函式 {#supported-functions}

從 [!DNL Pebble] 標籤部分，Destination SDK僅支援：

* [篩選](https://pebbletemplates.io/wiki/tag/filter/)
* [for](https://pebbletemplates.io/wiki/tag/for/)
* [如果](https://pebbletemplates.io/wiki/tag/if/)
* [set](https://pebbletemplates.io/wiki/tag/set/)

>[!TIP]
>
>使用 `for` 在循環時不同 *陣列* 或 *地圖* 中的元素。 在陣列中迭代時，可以直接獲取元素。 在遍歷映射時，將獲取每個具有鍵值對的映射項。
>
> * 對於陣列元素的示例，請考慮 [標識映射](message-format.md#identities) 命名空間，在此可以循環訪問元素 `identityMap.gaid`。 `identityMap.email`或類似。
> * 對於映射元素的示例，請考慮 [segmentMembership](message-format.md#segment-membership)。


從 [!DNL Pebble] filter部分，Destination SDK支援所有函式。 下面的示例說明 `date` 函式可在Destination SDK中使用。

從 [!DNL Pebble] 函式部分，Adobe *不* 支援 [範圍](https://pebbletemplates.io/wiki/function/range/) 的子菜單。

## 示例 `date` 函式 {#date-function}

以示例 [!DNL Pebble] 函式在Destination SDK中使用，請參見下面日期函式([Pebble文檔中的連結](https://pebbletemplates.io/wiki/filter/date/))用於轉換時間戳的格式。

### 使用案例

要更改 `lastQualificationTime` 預設時間戳 [ISO 8601](https://en.wikipedia.org/wiki/ISO_8601) 該Experience Platform導出到目標首選的另一個值的值。

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

## 通過Adobe添加的函式 {#functions-added-by-adobe}

除了由 [!DNL Pebble]，請參閱下面的Adobe建立的其他函式，這些函式可用於資料導出。

### `addedSegments` 和 `removedSegments` 函式 {#addedsegments-removedsegments-functions}

#### 使用案例

可以使用這些函式來獲取添加到配置檔案或從配置檔案中刪除的段的清單。

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

你現在知道 [!DNL Pebble] Destination SDK中支援函式，以及如何使用這些函式來調整導出資料的格式以滿足您的需要。 接下來，您應查看以下頁面：

* [建立和test消息轉換模板](../../testing-api/streaming-destinations/create-template.md)
* [呈現模板API操作](../../testing-api/streaming-destinations/render-template-api.md)
