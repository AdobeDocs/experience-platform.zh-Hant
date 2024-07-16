---
keywords: Experience Platform；首頁；熱門主題；API；API；XDM；XDM系統；體驗資料模型；體驗資料模型；資料模型；資料模型；結構描述登入；Schema登入；聯合；聯合；聯合；聯合；區段會籍；timeSeriesEvents；
solution: Experience Platform
title: 聯合API端點
description: 結構描述登入API中的/unions端點可讓您以程式設計方式管理體驗應用程式中的XDM聯合結構描述。
exl-id: d0ece235-72e8-49d9-856b-5dba44e16ee7
source-git-commit: 3da2e8f66f08a7bb9533795f7854ad583734911c
workflow-type: tm+mt
source-wordcount: '899'
ht-degree: 1%

---

# 聯合端點

聯合（或聯合檢視）是系統產生的唯讀結構描述，其彙總了共用相同類別（[!DNL XDM ExperienceEvent]或[!DNL XDM Individual Profile]）且已針對[[!DNL Real-Time Customer Profile]](../../profile/home.md)啟用的所有結構描述的欄位。

本文介紹在Schema Registry API中使用聯合的基本概念，包括各種操作的範例呼叫。 如需XDM中聯合的更多一般資訊，請參閱結構描述組合[基本概念中的聯合](../schema/composition.md#union)一節。

## 聯合結構描述欄位

[!DNL Schema Registry]會在聯合結構描述中自動包含三個索引鍵欄位： `identityMap`、`timeSeriesEvents`和`segmentMembership`。

### 身分對應

聯合結構描述的`identityMap`代表聯合關聯記錄結構描述中的已知身分。 身分對應會將身分割槽分給名稱空間輸入的不同陣列。 每個列出的身分識別本身都是包含唯一`id`值的物件。 如需詳細資訊，請參閱[Identity Service檔案](../../identity-service/home.md)。

### 時間序列事件

`timeSeriesEvents`陣列是與聯集關聯的記錄結構描述相關的時間序列事件清單。 將設定檔資料匯出至資料集時，每個記錄都會包含此陣列。 這對於各種使用案例非常有用，例如機器學習，其中模型需要設定檔的整個行為歷史記錄及其記錄屬性。

### 區段會籍地圖

`segmentMembership`對應會儲存評估區段定義的結果。 使用[分段API](https://www.adobe.io/experience-platform-apis/references/segmentation/)成功執行區段作業時，對應會更新。 `segmentMembership`也會儲存擷取至Platform的任何預先評估對象，以允許與其他解決方案(例如Adobe Audience Manager)整合。 如需詳細資訊，請參閱有關[使用API建立對象](../../segmentation/tutorials/create-a-segment.md)的教學課程。

## 擷取聯合清單 {#list}

當您在結構描述上設定`union`標籤時，[!DNL Schema Registry]會自動將結構描述新增到結構描述所依據之類別的聯合。 如果相關類別不存在聯集，則會自動建立新的聯集。 聯集的`$id`與其他[!DNL Schema Registry]資源的標準`$id`類似，唯一的差異是附加了兩個底線和單字「聯集」(`__union`)。

您可以透過向`/tenant/unions`端點發出GET要求來檢視可用的聯合清單。

**API格式**

```http
GET /tenant/unions
```

**要求**

```SHELL
curl -X GET \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/unions \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Accept: application/vnd.adobe.xed-id+json'
```

回應格式取決於請求中傳送的`Accept`標頭。 下列`Accept`標頭可用於列出聯合：

| `Accept`標題 | 說明 |
| --- | --- |
| `application/vnd.adobe.xed-id+json` | 傳回每個資源的簡短摘要。 這是列出資源的建議標頭。 （上限： 300） |
| `application/vnd.adobe.xed+json` | 傳回每個資源的完整JSON類別，包含原始`$ref`和`allOf`。 （上限： 300） |

{style="table-layout:auto"}

**回應**

成功的回應會在回應本文中傳回HTTP狀態200 （確定）和`results`陣列。 如果已定義聯合，則每個聯合的詳細資訊會作為陣列中的物件提供。 如果尚未定義聯合，仍會傳回HTTP狀態200 （確定），但`results`陣列將是空的。

```JSON
{
    "results": [
        {
            "title": "XDM Individual Profile",
            "$id": "https://ns.adobe.com/xdm/context/profile__union",
            "meta:altId": "_xdm.context.profile__union",
            "version": "1"
        },
        {
            "title": "Property",
            "$id": "https://ns.adobe.com/{TENANT_ID}/classes/19e1d8b5098a7a76e2c10a81cbc99590__union",
            "meta:altId": "_{TENANT_ID}.classes.19e1d8b5098a7a76e2c10a81cbc99590__union",
            "version": "1"
        }
    ]
}
```

## 查詢聯集 {#lookup}

您可以執行包含`$id`的GET要求來檢視特定的聯合，並且視Accept標頭而定，檢視聯合的部分或全部細節。

>[!NOTE]
>
>聯合查閱可使用`/unions`和`/schemas`端點來啟用它們，以便在[!DNL Profile]匯出至資料集時使用。

**API格式**

```http
GET /tenant/unions/{UNION_ID}
GET /tenant/schemas/{UNION_ID}
```

| 參數 | 說明 |
| --- | --- |
| `{UNION_ID}` | 您要查閱之聯合的URL編碼`$id` URI。 聯合結構描述的URI會附加「__union」。 |

{style="table-layout:auto"}

**要求**

```SHELL
curl -X GET \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/unions/https%3A%2F%2Fns.adobe.com%2Fxdm%2Fcontext%2Fprofile__union \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Accept: application/vnd.adobe.xed+json; version=1'
```

聯合查閱要求需要在Accept標頭中包含`version`。

下列Accept標頭可用於聯合結構描述查閱：

| 接受 | 說明 |
| -------|------------ |
| `application/vnd.adobe.xed+json; version=1` | 原始資料，含`$ref`和`allOf`。 包括標題和說明。 |
| `application/vnd.adobe.xed-full+json; version=1` | 已解決`$ref`屬性和`allOf`。 包括標題和說明。 |

{style="table-layout:auto"}

**回應**

成功的回應會傳回實作類別的所有結構描述的聯合檢視，這些類別的`$id`是在要求路徑中提供的。

回應格式取決於請求中傳送的Accept標頭。 實驗不同的Accept標頭，以比較回應並判斷哪個標頭最適合您的使用案例。

```JSON
{
    "type": "object",
    "description": "Union view of all schemas that extend https://ns.adobe.com/xdm/context/profile",
    "allOf": [
        {
            "$ref": "https://ns.adobe.com/xdm/context/profile"
        },
        {
            "$ref": "https://ns.adobe.com/xdm/context/profile-person-details"
        },
        {
            "$ref": "https://ns.adobe.com/{TENANT_ID}/mixins/477bb01d7125b015b4feba7bccc2e599"
        },
        {
            "$ref": "https://ns.adobe.com/xdm/context/profile-personal-details"
        }
    ],
    "meta:extends": [
        "https://ns.adobe.com/xdm/context/profile",
        "https://ns.adobe.com/xdm/data/record",
        "https://ns.adobe.com/xdm/context/identitymap",
        "https://ns.adobe.com/xdm/common/extensible",
        "https://ns.adobe.com/xdm/common/auditable",
        "https://ns.adobe.com/xdm/context/profile-person-details",
        "https://ns.adobe.com/{TENANT_ID}/mixins/477bb01d7125b015b4feba7bccc2e599",
        "https://ns.adobe.com/xdm/context/profile-personal-details"
    ],
    "title": "Union object for https://ns.adobe.com/xdm/context/profile",
    "$id": "https://ns.adobe.com/xdm/context/profile__union",
    "meta:containerId": "tenant",
    "meta:class": "https://ns.adobe.com/xdm/context/profile",
    "meta:altId": "_xdm.context.profile__union",
    "version": "1.0",
    "meta:resourceType": "unions",
    "meta:registryMetadata": {}
}
```

## 啟用聯合成員資格的結構描述 {#enable}

若要將結構描述加入其類別的聯合中，必須將`union`標籤新增到結構描述的`meta:immutableTags`屬性。 您可以發出PATCH要求，將單一字串值為`union`的`meta:immutableTags`陣列新增到有問題的結構描述中，藉此達成此目的。 如需詳細範例，請參閱[結構描述端點指南](./schemas.md#union)。

## 聯合中的清單結構描述 {#list-schemas}

若要檢視哪些結構描述是特定聯合的一部分，您可以對`/tenant/schemas`端點執行GET要求。 使用`property`查詢引數，您可以將回應設定為只傳回包含`meta:immutableTags`欄位和`meta:class`且等同於您正在存取其聯集的類別的結構描述。

**API格式**

```http
GET /tenant/schemas?property=meta:immutableTags==union&property=meta:class=={CLASS_ID}
```

| 參數 | 說明 |
| --- | --- |
| `{CLASS_ID}` | 您要列出其已啟用聯合的結構描述的類別的`$id`。 |

{style="table-layout:auto"}

**要求**

下列要求會擷取屬於[!DNL XDM Individual Profile]類別聯合之一部分的所有結構描述清單。

```SHELL
curl -X GET \
  'https://platform.adobe.io/data/foundation/schemaregistry/tenant/schemas?property=meta:immutableTags==union&property=meta:class==https://ns.adobe.com/xdm/context/profile' \
  -H 'Accept: application/vnd.adobe.xed-id+json' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

回應格式取決於請求中傳送的`Accept`標頭。 下列`Accept`標題可用於列出結構描述：

| `Accept`標題 | 說明 |
| --- | --- |
| `application/vnd.adobe.xed-id+json` | 傳回每個資源的簡短摘要。 這是列出資源的建議標頭。 （上限： 300） |
| `application/vnd.adobe.xed+json` | 傳回每個資源的完整JSON結構描述，包括原始`$ref`和`allOf`。 （上限： 300） |

{style="table-layout:auto"}

**回應**

成功的回應會傳回結構描述的篩選清單，其中只包含已針對聯合成員資格啟用的指定類別結構描述。 請記住，使用多個查詢引數時，會假設為AND關係。

```JSON
{
    "results": [
        {
            "title": "Schema 1",
            "$id": "https://ns.adobe.com/{TENANT_ID}/schemas/142afb78d8b368a5ba97a6cc8fc7e033",
            "meta:altId": "_{TENANT_ID}.schemas.142afb78d8b368a5ba97a6cc8fc7e033",
            "version": "1.2"
        },
        {
            "title": "Schema 2",
            "$id": "https://ns.adobe.com/{TENANT_ID}/schemas/e7297a6ddfc7812ab3a7b504a1ab98da",
            "meta:altId": "_{TENANT_ID}.schemas.e7297a6ddfc7812ab3a7b504a1ab98da",
            "version": "1.5"
        },
        {
            "title": "Schema 3",
            "$id": "https://ns.adobe.com/{TENANT_ID}/schemas/50f960bb810e99a21737254866a477bf",
            "meta:altId": "_{TENANT_ID}.schemas.50f960bb810e99a21737254866a477bf",
            "version": "1.2"
        },
        {
            "title": "Schema 4",
            "$id": "https://ns.adobe.com/{TENANT_ID}/schemas/a39655ca8ea3d5c1f36a463b45fccca8",
            "meta:altId": "_{TENANT_ID}.schemas.a39655ca8ea3d5c1f36a463b45fccca8",
            "version": "1.1"
        },
        {
            "title": "Schema 5",
            "$id": "https://ns.adobe.com/{TENANT_ID}/schemas/c063fac45c6d6285ef33b0e2af09f633",
            "meta:altId": "_{TENANT_ID}.schemas.c063fac45c6d6285ef33b0e2af09f633",
            "version": "1.2"
        },
        {
            "title": "Schema 6",
            "$id": "https://ns.adobe.com/{TENANT_ID}/schemas/dfebb19b93827b70bbad006137812537",
            "meta:altId": "_{TENANT_ID}.schemas.dfebb19b93827b70bbad006137812537",
            "version": "1.7"
        }
    ],
    "_links": {
        "global_schemas": {
            "href": "https://platform.adobe.io/data/foundation/schemaregistry/global/schemas?property=meta:immutableTags==union&property=meta:class==https://ns.adobe.com/xdm/context/profile"
        }
    }
}
```
