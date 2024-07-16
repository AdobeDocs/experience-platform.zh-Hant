---
description: Experience PlatformDestination SDK使用Pebble範本，可讓您將從Experience Platform匯出的資料轉換為目的地所需的格式。
title: Destination SDK中支援的轉換函式
exl-id: 36f761c7-9d76-41fe-b05f-d4cad655ddd2
source-git-commit: b4334b4f73428f94f5a7e5088f98e2459afcaf3c
workflow-type: tm+mt
source-wordcount: '552'
ht-degree: 2%

---

# Destination SDK中支援的轉換函式

Experience PlatformDestination SDK使用[[!DNL Pebble] 範本](https://pebbletemplates.io/)，可讓您將從Experience Platform匯出的資料轉換為目的地所需的格式。

與[!DNL Pebble]提供的現成版本相比，Experience Platform[!DNL Pebble]實作有一些變更。 此外，除了[!DNL Pebble]提供的現成函式外，Adobe已建立一些可與Destination SDK搭配使用的其他函式。

>[!IMPORTANT]
>
>Destination SDK支援的所有引數名稱和值都區分大小寫&#x200B;****。 為避免區分大小寫錯誤，請完全依照檔案中所示使用引數名稱和值。

## 使用位置 {#where-to-use}

當[為從Experience Platform匯出至目的地的資料建立訊息轉換範本](../../testing-api/streaming-destinations/create-template.md)時，請使用本頁下面列出的支援函式。

訊息轉換範本用於串流目的地的[目的地伺服器組態](templating-specs.md)。

## 先決條件 {#prerequisites}

若要瞭解此參考頁面中的概念和函式，請先閱讀[訊息格式](message-format.md)檔案。 您必須先瞭解Experience Platform中設定檔](message-format.md#profile-structure)的[結構，才能使用[!DNL Pebble]範本來轉換和匯出的資料。

在繼續使用下列功能之前，請先檢閱[使用範本語言進行身分、屬性和對象成員資格轉換](message-format.md#using-templating)一節中的範本範例。 這裡的範例一開始非常簡單，複雜性也增加了。

## 支援的[!DNL Pebble]函式 {#supported-functions}

從[!DNL Pebble]標籤區段，Destination SDK僅支援：

* [篩選器](https://pebbletemplates.io/wiki/tag/filter/)
* ](https://pebbletemplates.io/wiki/tag/for/)的[
* [if](https://pebbletemplates.io/wiki/tag/if/)
* [設定](https://pebbletemplates.io/wiki/tag/set/)

>[!TIP]
>
>反複處理範本中的&#x200B;*陣列*&#x200B;或&#x200B;*對應*&#x200B;元素時，使用`for`會不同。 當反複處理陣列時，可以直接取得元素。 當反複檢視對映時，會取得每個對映專案，每個對映專案都有一個索引鍵/值組。
>
> * 如需陣列元素的範例，請考慮[identityMap](message-format.md#identities)名稱空間中的身分，您可以在此重複執行元素，例如`identityMap.gaid`、`identityMap.email`或類似專案。
> * 如需對應元素的範例，請考慮[segmentMembership](message-format.md#segment-membership)。

從[!DNL Pebble]篩選區段，Destination SDK支援所有函式。 以下進一步的範例說明如何在Destination SDK中使用`date`函式。

從[!DNL Pebble]函式區段，Adobe *不*&#x200B;支援[範圍](https://pebbletemplates.io/wiki/function/range/)函式。

## 如何使用`date`函式的範例 {#date-function}

若要說明[!DNL Pebble]函式在Destination SDK中的使用方式，請參閱以下說明如何使用日期函式（[Pebble檔案](https://pebbletemplates.io/wiki/filter/date/)中的連結）來轉換時間戳記的格式。

### 使用實例

您想要將`lastQualificationTime`時間戳記從Experience Platform匯出的預設[ISO 8601](https://en.wikipedia.org/wiki/ISO_8601)值變更為您目的地偏好的其他值。

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

#### 匯出

```json
{
"lastQualificationTime": "2022-02-21T18:34:24Z"
}
```

## Adobe新增的函式 {#functions-added-by-adobe}

除了[!DNL Pebble]提供的現成函式之外，請參閱下方Adobe建立的其他函式，這些函式可用於資料匯出。

### `addedSegments`和`removedSegments`函式 {#addedsegments-removedsegments-functions}

#### 使用實例

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

##### 匯出

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

您現在知道Destination SDK支援哪些[!DNL Pebble]函式，以及如何使用它們來調整匯出資料的格式，以符合您的需求。 接下來，請檢閱下列頁面：

* [建立及測試訊息轉換範本](../../testing-api/streaming-destinations/create-template.md)
* [轉譯器範本API作業](../../testing-api/streaming-destinations/render-template-api.md)
