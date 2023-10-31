---
description: Experience PlatformDestination SDK使用Pebble範本，可讓您將從Experience Platform匯出的資料轉換為目的地所需的格式。
title: Destination SDK中支援的轉換函式
exl-id: 36f761c7-9d76-41fe-b05f-d4cad655ddd2
source-git-commit: b4334b4f73428f94f5a7e5088f98e2459afcaf3c
workflow-type: tm+mt
source-wordcount: '579'
ht-degree: 3%

---

# Destination SDK中支援的轉換函式

Experience PlatformDestination SDK使用 [[!DNL Pebble] 範本](https://pebbletemplates.io/)，可將從Experience Platform匯出的資料轉換為目的地所需的格式。

Experience Platform [!DNL Pebble] 與提供的現成可用版本相比，實作有一些變更 [!DNL Pebble]. 此外，除了提供的現成可用函式以外， [!DNL Pebble]，Adobe已建立一些可與Destination SDK搭配使用的其他函式。

>[!IMPORTANT]
>
>Destination SDK支援的所有引數名稱和值如下 **區分大小寫**. 為避免區分大小寫錯誤，請完全依照檔案中所示使用引數名稱和值。

## 使用位置 {#where-to-use}

使用本頁面下方所列的支援函式，當 [建立訊息轉換範本](../../testing-api/streaming-destinations/create-template.md) 適用於從Experience Platform匯出至目的地的資料。

訊息轉換範本用於 [目的地伺服器設定](templating-specs.md) 適用於串流目的地。

## 先決條件 {#prerequisites}

若要瞭解本參考頁面中的概念和函式，請閱讀 [訊息格式](message-format.md) 檔案優先。 您需要瞭解 [設定檔的結構](message-format.md#profile-structure) Experience Platform中，然後才能使用 [!DNL Pebble] 範本以轉換及匯出的資料。

繼續進行下面記錄的功能之前，請檢閱一節中的範本化範例 [使用範本語言進行身分、屬性和對象成員資格轉換](message-format.md#using-templating). 這裡的範例一開始非常簡單，複雜性也增加了。

## 支援 [!DNL Pebble] 函式 {#supported-functions}

從 [!DNL Pebble] 標籤區段，Destination SDK僅支援：

* [篩選](https://pebbletemplates.io/wiki/tag/filter/)
* [for](https://pebbletemplates.io/wiki/tag/for/)
* [如果](https://pebbletemplates.io/wiki/tag/if/)
* [set](https://pebbletemplates.io/wiki/tag/set/)

>[!TIP]
>
>使用 `for` 反複處理時不同 *陣列* 或 *地圖* 範本中的元素。 當反複處理陣列時，可以直接取得元素。 當反複檢視對映時，會取得每個對映專案，每個對映專案都有一個索引鍵/值組。
>
> * 如需陣列元素的範例，請思考陣列元素中的身分 [identityMap](message-format.md#identities) 名稱空間，您可以在此處循環檢視元素，例如 `identityMap.gaid`， `identityMap.email`或類似專案。
> * 如需對應元素的範例，請考慮 [區段會籍](message-format.md#segment-membership).

從 [!DNL Pebble] 篩選區段，Destination SDK支援所有函式。 以下進一步的範例說明如何 `date` 函式可在Destination SDK中使用。

從 [!DNL Pebble] 函式區段，Adobe會 *非* 支援 [範圍](https://pebbletemplates.io/wiki/function/range/) 函式。

## 範例： `date` 函式使用中 {#date-function}

以示範 [!DNL Pebble] 函式用於Destination SDK，請參閱下面的日期函式([Pebble檔案中的連結](https://pebbletemplates.io/wiki/filter/date/))來轉換時間戳記的格式。

### 使用案例

您想要變更 `lastQualificationTime` 來自預設值的時間戳記 [ISO 8601](https://en.wikipedia.org/wiki/ISO_8601) Experience Platform會匯出至目的地偏好之其他值的值。

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

## Adobe新增的函式 {#functions-added-by-adobe}

除了提供的現成可用函式之外， [!DNL Pebble]，請參閱下方的Adobe建立的其他函式，這些函式可用於資料匯出。

### `addedSegments` 和 `removedSegments` 函式 {#addedsegments-removedsegments-functions}

#### 使用案例

這些函式可用於取得新增到設定檔或從中移除的對象清單。

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

### Added and removed audiences filters {#added-and-removed-segmnts-filters}

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

您現在知道是哪個 [!DNL Pebble] Destination SDK支援函式，以及如何使用它們調整匯出資料的格式以符合您的需求。 接下來，請檢閱下列頁面：

* [建立及測試訊息轉換範本](../../testing-api/streaming-destinations/create-template.md)
* [轉譯器範本API作業](../../testing-api/streaming-destinations/render-template-api.md)
