---
title: 沙箱工具套件API端點
description: 沙箱工具API中的/packages端點可讓您以程式設計方式管理Adobe Experience Platform中的套件。
exl-id: 46efee26-d897-4941-baf4-d5ca0b8311f0
source-git-commit: f81e15ccfd89e2d0cb450f596743341264187f52
workflow-type: tm+mt
source-wordcount: '1621'
ht-degree: 8%

---

# 套件端點

沙箱工具可讓您選取不同的成品（也稱為物件），並將其匯出至套件中。 套件可以包含單一成品或多個成品（例如資料集或結構描述）。 套件中包含的任何成品都必須來自相同沙箱。

沙箱工具API中的`/packages`端點可讓您以程式設計方式管理組織中的套件，包括發佈套件並將套件匯入沙箱。

## 建立套件 {#create}

您可以透過向`/packages`端點發出POST要求，同時提供封裝名稱和封裝型別的值，來建立多成品封裝。

**API格式**

```http
POST /packages/
```

**要求**

```shell
curl -X POST \
  https://platform.adobe.io/data/foundation/exim/packages \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d'{
      "name": "acme",
      "description": "Acme Business Group",
      "packageType": "PARTIAL",    
      "sourceSandbox": {
        "name": "acme-sandbox",
        "imsOrgId": "5C1328435BF324E90A49402A@AdobeOrg"
      },
      "expiry": "2023-05-20T20:05:10Z",
      "artifacts": [
        {
          "id": "27115daa-c92b-4f17-a077-d65ffeb0c525",
          "type": "PROFILE_SEGMENT",
          "title": "Acme Profile Segment"
        }      
      ]
  }'
```

| 屬性 | 說明 | 類型 | 必要 |
| --- | --- | --- | --- |
| `name` | 封裝的名稱。 | 字串 | 是 |
| `description` | 提供封裝詳細資訊的說明。 | 字串 | 無 |
| `packageType` | 封裝型別是&#x200B;**PARTIAL**，表示您在封裝中包含特定成品。 | 字串 | 是 |
| `sourceSandbox` | 套件的來源沙箱。 | 字串 | 無 |
| `expiry` | 定義封裝到期日期的時間戳記。 預設值是從建立日期算起的90天。 回應到期欄位將會是epoch UTC時間。 | 字串（UTC時間戳記格式） | 無 |
| `artifacts` | 要匯出至封裝的成品清單。 當`packageType`為`FULL`時，`artifacts`值應為&#x200B;**null**&#x200B;或&#x200B;**empty**。 | 陣列 | 無 |

**回應**

成功的回應會傳回您新建立的封裝。 回應包含對應的套件ID，以及其狀態、到期日和成品清單的資訊。

```json
{
    "id": "209f886b00444eac9bb5836fe32e7681",
    "version": 0,
    "createdDate": 1684475012105,
    "modifiedDate": 1684475012105,
    "createdBy": "{CREATED_BY}",
    "modifiedBy": "{MODIFIED_BY}",
    "tenantId": "c875b077162b40409c1327b16da99c1b",
    "requestId": "devxa54a6b56d04f46119d9e3cc006fcc1cb",
    "userId": "platform_exim",
    "name": "acme",
    "description": "Acme Business Group",
    "imsOrgId": "5C1328435BF324E90A49402A@AdobeOrg",     
    "sourceSandbox": {
        "name": "cjm-mr",
        "imsOrgId": "5C1328435BF324E90A49402A@AdobeOrg"
    },     
    "packageType": "PARTIAL",
    "expiry": 1684613110000,
    "status": "DRAFT",    
    "artifactsList": [
        {
            "id": "d8d8ed6d-696a-40bd-b4fe-ca053ec94e29",
            "type": "JOURNEY",
            "found": false,
            "count": 0
        }
    ]
}
```

## 更新套件 {#update}

您可以對`/packages`端點發出PUT要求，以更新套件。

### 將成品新增至封裝 {#add-artifacts}

若要新增成品至封裝，您必須提供`id`並包含`action`的&#x200B;**ADD**。

**API格式**

```http
PUT /packages/
```

**要求**

```shell
curl -X PUT \
  https://platform.adobe.io/data/foundation/exim/packages \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d'{
      "id": "6fa50baedd344a278129a87e68cc9dc7",
      "action": "ADD",
      "expiry": "2023-05-20T20:05:10Z", 
      "artifacts": [
        {
         "id": "d8d8ed6d-696a-40bd-b4fe-ca053ec94e29@1647559351683",
         "type": "JOURNEY"
        }      
      ]
  }'
```

| 屬性 | 說明 | 類型 | 強制 |
| --- | --- | --- | --- |
| `id` | 要更新之封裝的ID。 | 字串 | 是 |
| `action` | 若要將成品加入封裝中，動作值應該是&#x200B;**ADD**。 只有&#x200B;**PARTIAL**&#x200B;封裝型別支援此動作。 | 字串 | 是 |
| `artifacts` | 要新增到封裝中的成品清單。 如果清單為&#x200B;**null**&#x200B;或&#x200B;**empty**，則不會變更封裝。 成品在新增至封裝之前，會先去除重複專案。 如需支援的成品完整清單，請參閱下表。 | 陣列 | 無 |
| `expiry` | 定義封裝到期日期的時間戳記。 若承載中未指定到期，則預設值是從呼叫PUT API後的90天。 回應到期欄位將會是epoch UTC時間。 | 字串（UTC時間戳記格式） | 無 |

目前支援的成品型別如下。

| 成品 | 平台 | 物件 | 部分流量 | 完整沙箱 |
| --- | --- | --- | --- | --- |
| `JOURNEY` | Adobe Journey Optimizer | 歷程 | 是 | 無 |
| `ID_NAMESPACE` | 客戶資料平台 | 身分 | 是 | 是 |
| `REGISTRY_DATATYPE` | 客戶資料平台 | 資料類型 | 是 | 是 |
| `REGISTRY_CLASS` | 客戶資料平台 | 類別 | 是 | 是 |
| `REGISTRY_MIXIN` | 客戶資料平台 | 欄位群組 | 是 | 是 |
| `REGISTRY_SCHEMA` | 客戶資料平台 | 結構描述 | 是 | 是 |
| `CATALOG_DATASET` | 客戶資料平台 | 資料集 | 是 | 是 |
| `DULE_CONSENT_POLICY` | 客戶資料平台 | 同意和治理原則 | 是 | 是 |
| `PROFILE_SEGMENT` | 客戶資料平台 | 對象 | 是 | 是 |
| `FLOW` | 客戶資料平台 | 來源資料流 | 是 | 是 |

**回應**

成功的回應會傳回您更新的封裝。 回應包含對應的套件ID，以及其狀態、到期日和成品清單的資訊。

```json
{
    "id": "6fa50baedd344a278129a87e68cc9dc7",
    "version": 4,
    "createdDate": 1684235842000,
    "modifiedDate": 1684475861366,
    "createdBy": "{CREATED_BY}",
    "modifiedBy": "{MODIFIED_BY}",
    "tenantId": "c875b077162b40409c1327b16da99c1b",
    "name": "acme",
    "description": "Acme Business Group",
    "imsOrgId": "5C1328435BF324E90A49402A@AdobeOrg",     
    "sourceSandbox": {
        "name": "acme-sandbox",
        "imsOrgId": "5C1328435BF324E90A49402A@AdobeOrg"
    },     
    "packageType": "PARTIAL",
    "expiry": 1692251861352,
    "status": "DRAFT",    
    "artifactsList": [
        {
            "id": "d8d8ed6d-696a-40bd-b4fe-ca053ec94e29@1647559351683",
            "type": "JOURNEY",
            "found": false,
            "count": 0
        },
        {
            "id": "d8d8ed6d-696a-40bd-b4fe-ca053ec94e29",
            "type": "JOURNEY",
            "found": false,
            "count": 0
        }
    ]
}
```

### 從封裝中刪除成品 {#delete-artifacts}

若要從封裝中刪除成品，您必須為`action`提供`id`並包含&#x200B;**DELETE**。


**API格式**

```http
PUT /packages/
```

**要求**

```shell
curl -X PUT \
  https://platform.adobe.io/data/foundation/exim/packages \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d'{
      "id": "6fa50baedd344a278129a87e68cc9dc7",
      "action": "DELETE",
      "artifacts": [
        {
          "id": "d8d8ed6d-696a-40bd-b4fe-ca053ec94e29@1647559351683",
          "type": "JOURNEY"
        }      
      ]
  }'
```

| 屬性 | 說明 | 類型 | 強制 |
| --- | --- | --- | --- |
| `id` | 要更新之封裝的ID。 | 字串 | 是 |
| `action` | 若要從封裝中刪除成品，動作值應為&#x200B;**DELETE**。 只有&#x200B;**PARTIAL**&#x200B;封裝型別支援此動作。 | 字串 | 是 |
| `artifacts` | 要從封裝中刪除的成品清單。 如果清單為&#x200B;**null**&#x200B;或&#x200B;**empty**，則不會變更封裝。 | 陣列 | 無 |

**回應**

成功的回應會傳回您更新的封裝。 回應包含對應的套件ID，以及其狀態、到期日和成品清單的資訊。

```json
{
    "id": "6fa50baedd344a278129a87e68cc9dc7",
    "version": 5,
    "createdDate": 1684235842000,
    "modifiedDate": 1684478830416,
    "createdBy": "{CREATED_BY}",
    "modifiedBy": "{MODIFIED_BY}",
    "tenantId": "c875b077162b40409c1327b16da99c1b",
    "name": "acme",
    "description": "Acme Business Group",
    "imsOrgId": "5C1328435BF324E90A49402A@AdobeOrg",     
    "sourceSandbox": {
        "name": "acme-sandbox",
        "imsOrgId": "5C1328435BF324E90A49402A@AdobeOrg"
    },      
    "packageType": "PARTIAL",
    "expiry": 1692254830403,
    "status": "DRAFT",    
    "artifactsList": [
        {
            "id": "d8d8ed6d-696a-40bd-b4fe-ca053ec94e29",
            "type": "JOURNEY",
            "found": false,
            "count": 0
        }
    ]
}
```

### 更新封裝中的中繼資料欄位 {#update-metadata}

>[!NOTE]
>
>**UPDATE**&#x200B;動作用於更新封裝的封裝中繼資料欄位，而&#x200B;**無法**&#x200B;用於新增/刪除封裝的成品。

若要更新封裝中的中繼資料欄位，您必須提供`id`並包含`action`的&#x200B;**UPDATE**。

**API格式**

```http
PUT /packages/
```

**要求**

```shell
curl -X PUT \
  https://platform.adobe.io/data/foundation/exim/packages \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d'{
      "id": "6fa50baedd344a278129a87e68cc9dc7",
      "action": "UPDATE",
      "name": "acme",
      "description": "Acme Business Group",  
      "sourceSandbox": {
        "name": "acme-sandbox",
        "imsOrgId": "5C1328435BF324E90A49402A@AdobeOrg"
      }
  }'
```

| 屬性 | 說明 | 類型 | 強制 |
| --- | --- | --- | --- |
| `id` | 要更新之封裝的ID。 | 字串 | 是 |
| `action` | 若要更新封裝中的中繼資料欄位，動作值應該是&#x200B;**UPDATE**。 只有&#x200B;**PARTIAL**&#x200B;封裝型別支援此動作。 | 字串 | 是 |
| `name` | 封裝的更新名稱。 不允許重複套件名稱。 | 陣列 | 是 |
| `sourceSandbox` | Source沙箱應屬於請求標頭中指定的相同組織。 | 字串 | 是 |

**回應**

成功的回應會傳回您更新的封裝。 回應包含對應的套件ID，以及其說明、狀態、到期日和成品清單的資訊。

```json
{
    "id": "6fa50baedd344a278129a87e68cc9dc7",
    "version": 6,
    "createdDate": 1684235842000,
    "modifiedDate": 1684479094129,
    "createdBy": "{CREATED_BY}",
    "modifiedBy": "{MODIFIED_BY}",
    "tenantId": "c875b077162b40409c1327b16da99c1b",
    "name": "acme",
    "description": "Acme Business Group",
    "imsOrgId": "5C1328435BF324E90A49402A@AdobeOrg",    
    "sourceSandbox": {
        "name": "acme-sandbox",
        "imsOrgId": "5C1328435BF324E90A49402A@AdobeOrg"
    },
    "packageType": "PARTIAL",
    "expiry": 1692255094127,
    "status": "DRAFT",    
    "artifactsList": [
        {
            "id": "d8d8ed6d-696a-40bd-b4fe-ca053ec94e29",
            "type": "JOURNEY",
            "found": false,
            "count": 0
        }
    ]
}
```

## 刪除套裝 {#delete}

若要刪除封裝，請向`/packages`端點發出DELETE要求，並指定您要刪除之封裝的識別碼。

**API格式**

```http
DELETE /packages/{PACKAGE_ID}
```

| 參數 | 說明 |
| --- | --- |
| {PACKAGE_ID} | 您要刪除之套件的ID。 |

**要求**

下列要求會刪除識別碼為{PACKAGE_ID}的封裝。

```shell
curl -X DELETE \
  https://platform.adobe.io/data/foundation/exim/packages/{PACKAGE_ID} \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
```

**回應**

成功的回應會傳回一個原因，其中顯示已刪除的套件ID。

```json
{
    "reason": "Package d30e0424a37b46ada6a5cf37f47a86ff deleted"
}
```

## Publish a套件 {#publish}

為了啟用將套件匯入沙箱，您必須發佈它。 指定您要發佈的封裝ID時，向`/packages`端點發出GET要求。

**API格式**

```http
GET /packages/{PACKAGE_ID}/export
```

| 參數 | 說明 |
| --- | --- |
| {PACKAGE_ID} | 您要發佈的套件ID。 |

**要求**

下列要求會發佈識別碼為{PACKAGE_ID}的封裝。

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/exim/packages/{PACKAGE_ID}\export \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
```

| 屬性 | 說明 | 類型 | 強制 |
| --- | --- | --- | --- |
| `expiryPeriod` | 這個使用者指定的時段會定義從發佈套件開始的套件到期日（以天為單位）。 此值不應為負數。<br>若未指定任何值，則預設值將從發佈日期算起90 （天）。 | 整數 | 無 |

**回應**

成功的回應會傳回已發佈的套件。

```json
{
    "name": "acme",
    "description": "Acme Business Group",
    "visibility": "TENANT",
    "sourceSandbox":
    {
        "name": "acme-sandbox",
        "imsOrgId": "5C1328435BF324E90A49402A@AdobeOrg"
    },
    "type": "PARTIAL",
    "correlationId": "48effe5e-1bef-4250-9c71-23b93ef5d285"
}
```

## 查詢封裝 {#look-up-package}

您可以向`/packages`端點發出GET要求，在要求路徑中包含封裝的對應ID，以查詢個別封裝。

**API格式**

```http
GET /packages/{PACKAGE_ID}
```

| 參數 | 說明 |
| --- | --- |
| {PACKAGE_ID} | 您要查閱之套件的ID。 |

**要求**

下列要求會擷取{PACKAGE_ID}的資訊。

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/exim/packages/{PACKAGE_ID} \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
```

**回應**

成功的回應會傳回查詢之封裝ID的詳細資料。 回應包括名稱、說明、發佈日期和到期日、封裝的來源沙箱以及成品清單。

```json
{
    "id": "8f585fad94d042cd82dbcba594108a41",
    "version": 2,
    "createdDate": 1685597784000,
    "modifiedDate": 1685597810000,
    "createdBy": "{CREATED_BY}",
    "modifiedBy": "{MODIFIED_BY}",
    "tenantId": "c875b077162b40409c1327b16da99c1b",
    "name": "acme",
    "description": "Acme Business Group",
    "imsOrgId": "5C1328435BF324E90A49402A@AdobeOrg",
    "packageType": "PARTIAL",
    "expiry": 1693373810000,
    "publishDate": 1685597810000,
    "status": "PUBLISHED",
    "artifactsList": [
        {
            "id": "f4f57771-2bd2-469a-9c13-8d803eeb6515",
            "type": "JOURNEY",
            "found": false,
            "count": 0
        },
        {
            "id": "7f4caca7-a477-400d-a41e-c4735f8e780d",
            "type": "JOURNEY",
            "found": false,
            "count": 0
        }
    ],
    "sourceSandbox": {
        "name": "acme-sandbox",
        "imsOrgId": "5C1328435BF324E90A49402A@AdobeOrg"
    }
}
```

## 列出封裝 {#list-packages}

您可以透過向`/packages`端點發出GET要求，列出您組織中的所有封裝。

**API格式**

```http
GET /packages/?{QUERY_PARAMS}
```

| 參數 | 說明 |
| --- | --- |
| {QUERY_PARAMS} | 篩選結果的選用查詢引數。 如需詳細資訊，請參閱[查詢引數](./appendix.md)的相關章節。 |

**要求**

下列要求會根據{QUERY_PARAMS}擷取封裝資訊。

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/exim/packages/?property=status==DRAFT,PUBLISHED&property=createdDate>=2023-05-11T18:29:59.999Z&property=createdDate<=2023-05-16T18:29:59.999Z&start=0&orderby=-createdDate&limit=20 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
```

**回應**

成功的回應會傳回屬於您組織的封裝清單，包括名稱、狀態、到期日及成品清單等詳細資訊。

```json
{
    "totalElements": 109,
    "currentPage": 0,
    "totalPages": 6,
    "hasPreviousPage": false,
    "hasNextPage": true,
    "data": [
        {
            "id": "8f585fad94d042cd82dbcba594108a41",
            "version": 2,
            "createdDate": 1685597784000,
            "modifiedDate": 1685597810000,
            "createdBy": "{CREATED_BY}",
            "modifiedBy": "{MODIFIED_BY}",
            "tenantId": "c875b077162b40409c1327b16da99c1b",
            "name": "acme",
            "description": "Acme Business Group",
            "imsOrgId": "5C1328435BF324E90A49402A@AdobeOrg",
            "packageType": "PARTIAL",
            "expiry": 1693373810000,
            "publishDate": 1685597810000,
            "status": "PUBLISHED",
            "artifactsList": [
                {
                    "id": "f4f57771-2bd2-469a-9c13-8d803eeb6515",
                    "type": "JOURNEY",
                    "found": false,
                    "count": 0
                },
                {
                    "id": "7f4caca7-a477-400d-a41e-c4735f8e780d",
                    "type": "JOURNEY",
                    "found": false,
                    "count": 0
                }
            ],
            "sourceSandbox": {
                "name": "acme-sandbox",
                "imsOrgId": "5C1328435BF324E90A49402A@AdobeOrg"
            }
        },
        {
            "id": "0d7e427ce4cb4dc1b78e30ef61b125c1",
            "version": 2,
            "createdDate": 1685555213000,
            "modifiedDate": 1685555275000,
            "createdBy": "{CREATED_BY}",
            "modifiedBy": "{MODIFIED_BY}",
            "tenantId": "7d7d8bbe3c7c4a8ea701cc5e42c57aeb",
            "name": "acme",
            "description": "Acme Business Group",
            "imsOrgId": "5C1328435BF324E90A49402A@AdobeOrg",
            "packageType": "PARTIAL",
            "expiry": 1693331275000,
            "publishDate": 1685555275000,
            "status": "PUBLISHED",
            "artifactsList": [
                {
                    "id": "626a9669a9f5b818db270e95",
                    "type": "CATALOG_DATASET",
                    "found": false,
                    "count": 0
                }
            ],
            "sourceSandbox": {
                "name": "acme-sandbox",
                "imsOrgId": "5C1328435BF324E90A49402A@AdobeOrg"
            }
        }
    ]
}
```

## 匯入套件 {#import}

此端點用於在指定的目標沙箱中擷取衝突的物件。 衝突的物件代表類似物件，這些物件已經存在於目標沙箱中。

**API格式**

```http
GET /packages/{PACKAGE_ID}/import?targetSandbox=targetSandboxName
```

| 參數 | 說明 |
| --- | --- |
| {PACKAGE_ID} | 您要查閱之套件的ID。 |

**要求**

下列要求匯入{PACKAGE_ID}。

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/exim/packages/{PACKAGE_ID}/import?targetSandbox=targetSandboxName \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
```

**回應**

回應中會傳回衝突。 回應會將原始套件加上`alternatives`片段顯示為依排名排序的陣列。

檢視回應+++

```json
[
    {
        "artifact": {
            "id": "https://ns.adobe.com/cjmstage/schemas/20121c2110bb2c6a585baabe5f82994577da1f7d0628234c",
            "type": "REGISTRY_SCHEMA",
            "found": false,
            "count": 0,
            "messages": [
                {
                    "status": "FOUND",
                    "attempt": 1,
                    "message": "Found object with ID: https://ns.adobe.com/cjmstage/schemas/20121c2110bb2c6a585baabe5f82994577da1f7d0628234c"
                }
            ]
        },
        "suggestionList": [
            {
                "id": "https://ns.adobe.com/cjmstage/schemas/176f33f6a8ff6542de1256f8dc01cce4be1b3a68fd5f5bc5",
                "type": "REGISTRY_SCHEMA",
                "found": false,
                "count": 0,
                "title": "Dean Dataset 1 - adhoc schema - 1618950408870_1686403052050"
            },
            {
                "id": "https://ns.adobe.com/cjmstage/schemas/1b37c3403e4e12c7aa46ea9dfe380a9f2b72d4da9db62b46",
                "type": "REGISTRY_SCHEMA",
                "found": false,
                "count": 0,
                "title": "Dean Dataset 1 - adhoc schema - 1618950408870_1686218766627"
            }
        ],
        "parentID": "745F37C35E4B776E0A49421B@AdobeOrg::prod::REGISTRY_SCHEMA::https://ns.adobe.com/cjmstage/schemas/20121c2110bb2c6a585baabe5f82994577da1f7d0628234c"
    },
    {
        "artifact": {
            "id": "https://ns.adobe.com/cjmstage/classes/24c1525f4f06fae2d203c6b78e26ae479ec4541c2c0d6b26",
            "type": "REGISTRY_CLASS",
            "found": false,
            "count": 0,
            "messages": [
                {
                    "status": "FOUND",
                    "attempt": 1,
                    "message": "Found object with ID: https://ns.adobe.com/cjmstage/classes/24c1525f4f06fae2d203c6b78e26ae479ec4541c2c0d6b26"
                }
            ]
        },
        "suggestionList": [
            {
                "id": "https://ns.adobe.com/cjmstage/classes/1dd81d61cdaa89a89382d0a424db77494475bd1db3105feb",
                "type": "REGISTRY_CLASS",
                "found": false,
                "count": 0,
                "title": "Dean Dataset 1 - Adhoc class - 1618950408870_1686564843736"
            },
            {
                "id": "https://ns.adobe.com/cjmstage/classes/2511fb5396a630b2cd3d5d9e9b69d42ce66a4289db8ac917",
                "type": "REGISTRY_CLASS",
                "found": false,
                "count": 0,
                "title": "Dean Dataset 1 - Adhoc class - 1618950408870_1686408152916"
            }
        ],
        "parentID": "745F37C35E4B776E0A49421B@AdobeOrg::prod::REGISTRY_CLASS::https://ns.adobe.com/cjmstage/classes/24c1525f4f06fae2d203c6b78e26ae479ec4541c2c0d6b26"
    },
    {
        "artifact": {
            "id": "4d4c874ec3344d64bf8b3160e60ac78b",
            "type": "MAPPING_SET",
            "found": false,
            "count": 0,
            "messages": [
                {
                    "status": "FOUND",
                    "attempt": 1,
                    "message": "Found object with ID: 4d4c874ec3344d64bf8b3160e60ac78b"
                }
            ]
        },
        "suggestionList": [
            {
                "id": "6b49c959d77c48e9904f7616fe2e7848",
                "type": "MAPPING_SET",
                "found": false,
                "count": 0,
                "title": ""
            },
            {
                "id": "7b363da9e6704afb9716f57193d5246f",
                "type": "MAPPING_SET",
                "found": false,
                "count": 0,
                "title": ""
            },
            {
                "id": "93ca0b4f437c4eaf9f1986408679e965",
                "type": "MAPPING_SET",
                "found": false,
                "count": 0,
                "title": ""
            }
        ],
        "parentID": "745F37C35E4B776E0A49421B@AdobeOrg::prod::MAPPING_SET::4d4c874ec3344d64bf8b3160e60ac78b"
    }
]
```

+++

## 提交匯入 {#submit-import}

>[!NOTE]
>
>替代成品已經存在於目標沙箱中，這是解決衝突所固有的。

一旦您檢閱了衝突並透過向`/packages`端點發出POST請求提供了替代，即可提交封裝的匯入。 結果會以承載的形式提供，這會開始針對在承載中指定的目的地沙箱匯入作業。

承載也接受匯入工作的使用者指定工作名稱和說明。 如果無法使用使用者指定的名稱和說明，則會將封裝名稱和說明用於工作名稱和說明。

**API格式**

```http
POST /packages/import
```

**要求**

下列請求會擷取要匯入的套件。 裝載是替代的對應，如果專案存在，則索引鍵是套件提供的`artifactId`，替代值是值。 如果對應或承載為&#x200B;**empty**，則不會執行任何替代。

```shell
curl -X POST \
  https://platform.adobe.io/data/foundation/exim/packages/import/ \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d'{
       "id": "09484a599f5f4a5faa43986643964615",
       "name": "acme",
       "description": "Acme Business Group",
       "destinationSandbox": {
         "name": "cjm-mr",
         "imsOrgId": "5C1328435BF324E90A49402A@AdobeOrg"
     },
     "alternatives": {
       "https://ns.adobe.com/cjmstage/schemas/ac33bbd22eb4ad6656e1c7e12e9f520261fb39fd28a902a9": {
         "id": "https://ns.adobe.com/cjmstage/schemas/a3b935344685afad4e52c753161cf673ec23d4fb1b3e9ce",
         "type": "REGISTRY_SCHEMA"
       }
     }
  }'
```

| 屬性 | 說明 | 類型 | 強制 |
| --- | --- | --- | --- |
| `alternatives` | `alternatives`代表來源沙箱成品對應到現有目標沙箱成品。 由於成品已存在，匯入工作會避免在Target沙箱中建立這些成品。 | 字串 | 無 |

**回應**

```json
{
    "name": "acme",
    "description": "Acme Business Group",
    "visibility": "TENANT",
    "sourceSandbox":
    {
        "name": "acme-sandbox",
        "imsOrgId": "5C1328435BF324E90A49402A@AdobeOrg"
    },
    "destinationSandbox":
    {
        "name": "acme-sandbox",
        "imsOrgId": "5C1328435BF324E90A49402A@AdobeOrg"
    },
    "type": "PARTIAL",
    "correlationId": "48effe5e-1bef-4250-9c71-23b93ef5d285"
}
```

## 列出所有相依物件 {#dependent-objects}

指定封裝識別碼時，藉由向`/packages`端點發出POST要求，列出封裝中匯出物件的所有相依物件。

**API格式**

```http
POST /packages/{PACKAGE_ID}/children
```

| 參數 | 說明 |
| --- | --- |
| {PACKAGE_ID} | 套件的ID。 |

**要求**

下列要求列出{PACKAGE_ID}的所有相依物件。

```shell
curl -X POST \
  https://platform.adobe.io/data/foundation/exim/packages/{PACKAGE_ID}/import?targetSandbox=targetSandboxName \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -d'[
      {
        "id": "4d4c874ec3344d64bf8b3160e60ac78b",
        "type": "MAPPING_SET"
      },
      {
        "id": "https://ns.adobe.com/cjmstage/schemas/20121c2110bb2c6a585baabe5f82994577da1f7d0628234c",
        "type": "REGISTRY_SCHEMA"
      },
      {
        "id": "https://ns.adobe.com/cjmstage/classes/24c1525f4f06fae2d203c6b78e26ae479ec4541c2c0d6b26",
        "type": "REGISTRY_CLASS"
      }
  ]'
```

**回應**

成功的回應會傳回物件的子項清單。

```json
[
    {
        "id": "4d4c874ec3344d64bf8b3160e60ac78b",
        "title": "4d4c874ec3344d64bf8b3160e60ac78b",
        "type": "MAPPING_SET",
        "children": [
            {
                "id": "https://ns.adobe.com/cjmstage/schemas/20121c2110bb2c6a585baabe5f82994577da1f7d0628234c",
                "title": "Dean Dataset 1 - adhoc schema - 1618950408870",
                "type": "REGISTRY_SCHEMA"
            }
        ]
    },
    {
        "id": "https://ns.adobe.com/cjmstage/schemas/20121c2110bb2c6a585baabe5f82994577da1f7d0628234c",
        "title": "Dean Dataset 1 - adhoc schema - 1618950408870",
        "type": "REGISTRY_SCHEMA",
        "children": [
            {
                "id": "https://ns.adobe.com/cjmstage/classes/24c1525f4f06fae2d203c6b78e26ae479ec4541c2c0d6b26",
                "title": "Dean Dataset 1 - Adhoc class - 1618950408870",
                "type": "REGISTRY_CLASS"
            }
        ]
    },
    {
        "id": "https://ns.adobe.com/cjmstage/classes/24c1525f4f06fae2d203c6b78e26ae479ec4541c2c0d6b26",
        "title": "Dean Dataset 1 - Adhoc class - 1618950408870",
        "type": "REGISTRY_CLASS",
        "children": []
    }
]
```

## 檢查以角色為基礎的許可權，以匯入所有封裝成品 {#role-based-permissions}

您可以檢查您是否具有匯入套件成品的許可權，方法是在指定套件識別碼和目標沙箱名稱時，向`/packages`端點發出GET要求。

**API格式**

```http
GET /packages/preflight/{packageId}?targetSandbox=<sandbox_name
```

| 參數 | 說明 |
| --- | --- |
| {PACKAGE_ID} | 您要匯入的套件ID。 |

**要求**

下列要求會檢查您對{PACKAGE_ID}和沙箱的許可權。

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/exim/packages/preflight/{PACKAGE_ID}?targetSandbox=<sandbox_name> \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
```

**回應**

成功的回應會傳回目標沙箱的資源許可權，包括所需的許可權清單、缺少許可權、成品型別，以及是否允許建立的決定。

檢視回應+++

```json
{
  "packageID": "b7bda68eb1214c86824f1d7204616e51",
  "targetSandboxName": "acme-sandbox",
  "permissionResponse": [
    {
      "artifactID": "4aca57b6-8b83-450b-a460-e8a07ca79a44",
      "requiredPermissions": {
        "resources": [
          {
            "palmResourceType": "Sandbox",
            "resourcePermissions": [
              "view"
            ]
          },
          {
            "palmResourceType": "Schema",
            "resourcePermissions": [
              "read"
            ]
          },
          {
            "palmResourceType": "ProfileConfig",
            "resourcePermissions": [
              "read"
            ]
          },
          {
            "palmResourceType": "Segment",
            "resourcePermissions": [
              "read",
              "write",
              "delete"
            ]
          },
          {
            "palmResourceType": "Composition",
            "resourcePermissions": [
              "read",
              "write",
              "delete"
            ]
          },
          {
            "palmResourceType": "Query",
            "resourcePermissions": [
              "write"
            ]
          },
          {
            "palmResourceType": "SegmentDashboard",
            "resourcePermissions": [
              "read"
            ]
          }
        ]
      },
      "missingPermissions": {
        "resources": []
      },
      "artifactType": "PROFILE_SEGMENT",
      "creationAllowed": true
    },
    {
      "artifactID": "36bb82bc-a00d-4d6b-a598-227d43e027c1",
      "requiredPermissions": {
        "resources": [
          {
            "palmResourceType": "Sandbox",
            "resourcePermissions": [
              "view"
            ]
          },
          {
            "palmResourceType": "ProfileConfig",
            "resourcePermissions": [
              "read",
              "write",
              "delete"
            ]
          },
          {
            "palmResourceType": "Dataset",
            "resourcePermissions": [
              "read"
            ]
          }
        ]
      },
      "missingPermissions": {
        "resources": [
          {
            "palmResourceType": "ProfileConfig",
            "resourcePermissions": [
              "write",
              "delete"
            ]
          },
          {
            "palmResourceType": "Dataset",
            "resourcePermissions": [
              "read"
            ]
          }
        ]
      },
      "artifactType": "PROFILE_MERGE",
      "creationAllowed": false
    }
  ]
}
```

+++

## 列出匯出/匯入工作 {#list-jobs}

您可以透過向`/packages`端點發出GET請求來列出目前的匯出/匯入作業。

**API格式**

```http
GET /packages/jobs?{QUERY_PARAMS}
```

| 參數 | 說明 |
| --- | --- |
| {QUERY_PARAMS} | 篩選結果的選用查詢引數。 如需詳細資訊，請參閱[查詢引數](./appendix.md)的相關章節。 |

**要求**

下列請求列出所有成功的匯入工作。

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/exim/packages/jobs?property=requestType==IMPORT&property=jobStatus==SUCCESS&orderby=createdDate&start=0&limit=5 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
```

**回應**

成功的回應會傳回所有成功的匯入作業。

```json
{
    "totalElements": 42,
    "currentPage": 0,
    "totalPages": 9,
    "hasPreviousPage": false,
    "hasNextPage": true,
    "data": [
        {
            "id": "3c1b92cf47a246d7bfbe6fd507c5d543",
            "name": "acme",
            "updated": 1685973675401,
            "created": 1685973675401,
            "jobType": "NEW",
            "packageType": "PARTIAL",
            "description": "Acme Business Group",
            "jobStatus": "SUCCESS",
            "visibility": "TENANT",
            "sourceSandBox": "acme-sandbox",
            "targetSandbox": "poc",
            "createdBy": "{CREATED_BY}"
        },
        {
            "id": "ead59d21405f4184a94dd786a1bf040d",
            "name": "acme1",
            "updated": 1685986367198,
            "created": 1685986367198,
            "jobType": "NEW",
            "packageType": "PARTIAL",
            "description": "Acme Business Group",
            "jobStatus": "SUCCESS",
            "visibility": "TENANT",
            "sourceSandBox": "acme-sandbox",
            "targetSandbox": "poc",
            "createdBy": "{CREATED_BY}"
        },
        {
            "id": "85ddaa3c2f6c475088167cde7a9d4326",
            "name": "acme2",
            "updated": 1686147692568,
            "created": 1686147692568,
            "jobType": "NEW",
            "packageType": "PARTIAL",
            "description": "Acme Business Group",
            "jobStatus": "SUCCESS",
            "visibility": "TENANT",
            "sourceSandBox": "acme-sandbox",
            "targetSandbox": "poc",
            "createdBy": "{CREATED_BY}"
        },
        {
            "id": "c49a4fcb31954cbd828ece1da096c8f5",
            "name": "acme3",
            "updated": 1686148007586,
            "created": 1686148007586,
            "jobType": "NEW",
            "packageType": "PARTIAL",
            "description": "Acme Business Group",
            "jobStatus": "SUCCESS",
            "visibility": "TENANT",
            "sourceSandBox": "acme-sandbox",
            "targetSandbox": "poc",
            "createdBy": "{CREATED_BY}"
        },
        {
            "id": "a3669315baed4cf2af49bf9ce90b8158",
            "name": "acme4",
            "updated": 1686148651910,
            "created": 1686148651910,
            "jobType": "NEW",
            "packageType": "PARTIAL",
            "description": "Acme Business Group",
            "jobStatus": "SUCCESS",
            "visibility": "TENANT",
            "sourceSandBox": "acme-sandbox",
            "targetSandbox": "poc",
            "createdBy": "{CREATED_BY}"
        }
    ]
}
```
