---
title: 沙箱工具套件API端點
description: 沙箱工具API中的/packages端點可讓您以程式設計方式管理Adobe Experience Platform中的套件。
exl-id: 46efee26-d897-4941-baf4-d5ca0b8311f0
source-git-commit: 1d8c29178927c7ee3aceb0b68f97baeaefd9f695
workflow-type: tm+mt
source-wordcount: '2933'
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
| `sourceSandbox` | 套件的來源沙箱。 | 物件 | 無 |
| `expiry` | 定義封裝到期日期的時間戳記。 預設值是從建立日期算起的90天。 回應到期欄位將會是epoch UTC時間。 | 字串（UTC時間戳記格式） | 無 |
| `artifacts` | 要匯出至封裝的成品清單。 當`artifacts`為&#x200B;**時，**&#x200B;值應為&#x200B;**null**&#x200B;或`packageType`empty`FULL`。 | 陣列 | 無 |

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

使用沙箱工具API中的`/packages`端點來更新套件。

### 將成品新增至封裝 {#add-artifacts}

若要新增成品至封裝，您必須提供`id`並包含&#x200B;**的** ADD`action`。

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
| `expiry` | 定義封裝到期日期的時間戳記。 若裝載中未指定到期，預設值是從呼叫PUT API後的90天。 回應到期欄位將會是epoch UTC時間。 | 字串（UTC時間戳記格式） | 無 |

目前支援的成品型別如下。

| 成品 | 平台 | 物件 | 部分流量 | 完整沙箱 |
| --- | --- | --- | --- | --- |
| `JOURNEY` | Adobe Journey Optimizer | 歷程 | 是 | 無 |
| `ID_NAMESPACE` | 客戶資料平台 | 身分識別 | 是 | 是 |
| `REGISTRY_DATATYPE` | 客戶資料平台 | 資料類型 | 是 | 是 |
| `REGISTRY_CLASS` | 客戶資料平台 | 類別 | 是 | 是 |
| `REGISTRY_MIXIN` | 客戶資料平台 | 欄位群組 | 是 | 是 |
| `REGISTRY_SCHEMA` | 客戶資料平台 | 結構描述 | 是 | 是 |
| `CATALOG_DATASET` | 客戶資料平台 | 資料集 | 是 | 是 |
| `DULE_CONSENT_POLICY` | 客戶資料平台 | 同意和治理原則 | 是 | 是 |
| `PROFILE_SEGMENT` | 客戶資料平台 | 客群 | 是 | 是 |
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

若要從封裝中刪除成品，您必須為`id`提供&#x200B;**並包含** DELETE`action`。

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
| `action` | 若要從封裝中刪除成品，動作值應該是&#x200B;**DELETE**。 只有&#x200B;**PARTIAL**&#x200B;封裝型別支援此動作。 | 字串 | 是 |
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

若要更新封裝中的中繼資料欄位，您必須提供`id`並包含&#x200B;**的** UPDATE`action`。

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
| `sourceSandbox` | Source沙箱應屬於請求標頭中指定的相同組織。 | 物件 | 是 |

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

若要刪除套件，請向`/packages`端點發出DELETE要求，並指定您要刪除之套件的識別碼。

**API格式**

```http
DELETE /packages/{PACKAGE_ID}
```

| 參數 | 說明 |
| --- | --- |
| `{PACKAGE_ID}` | 您要刪除之套件的ID。 |

**要求**

下列要求會刪除識別碼為{PACKAGE_ID}的封裝。

```shell
curl -X DELETE \
  https://platform.adobe.io/data/foundation/exim/packages/{PACKAGE_ID} \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
```

**回應**

成功的回應會傳回一個原因，其中顯示已刪除的套件ID。

```json
{
    "reason": "Package d30e0424a37b46ada6a5cf37f47a86ff deleted"
}
```

## 發佈套件 {#publish}

為了啟用將套件匯入沙箱，您必須發佈它。 指定您要發佈的套件ID時，向`/packages`端點發出GET要求。

**API格式**

```http
GET /packages/{PACKAGE_ID}/export
```

| 參數 | 說明 |
| --- | --- |
| `{PACKAGE_ID}` | 您要發佈的套件ID。 |

**要求**

下列要求會發佈識別碼為{PACKAGE_ID}的封裝。

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/exim/packages/{PACKAGE_ID}\export \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
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
    "correlationId": "48effe5e-1bef-4250-9c71-23b93ef5d285",
    "jobId": "18abab44e25f40c284a4bd6e8f52fd29"
}
```

## 查詢封裝 {#look-up-package}

您可以透過向`/packages`端點發出GET請求來查詢個別套件，端點在請求路徑中包含套件的對應ID。

**API格式**

```http
GET /packages/{PACKAGE_ID}
```

| 參數 | 說明 |
| --- | --- |
| `{PACKAGE_ID}` | 您要查閱之套件的ID。 |

**要求**

下列要求會擷取{PACKAGE_ID}的資訊。

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/exim/packages/{PACKAGE_ID} \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
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

您可以透過向`/packages`端點發出GET請求來列出您組織中的所有套件。

**API格式**

```http
GET /packages/?{QUERY_PARAMS}
```

| 參數 | 說明 |
| --- | --- |
| `{QUERY_PARAMS}` | 篩選結果的選用查詢引數。 如需詳細資訊，請參閱[查詢引數](./appendix.md)的相關章節。 |

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
| `{PACKAGE_ID}` | 您要查閱之套件的ID。 |

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

+++檢視回應

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
    "correlationId": "48effe5e-1bef-4250-9c71-23b93ef5d285",
    "jobId": "18abab44e25f40c284a4bd6e8f52fd29"
}
```

## 列出所有相依物件 {#dependent-objects}

指定封裝的識別碼時，透過對`/packages`端點發出POST要求，列出封裝中匯出物件的所有相依物件。

**API格式**

```http
POST /packages/{PACKAGE_ID}/children
```

| 參數 | 說明 |
| --- | --- |
| `{PACKAGE_ID}` | 套件的ID。 |

**要求**

下列要求列出{PACKAGE_ID}的所有相依物件。

```shell
curl -X POST \
  https://platform.adobe.io/data/foundation/exim/packages/{PACKAGE_ID}/children \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
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

您可以檢查您是否具有匯入套件成品的許可權，方法是在指定套件識別碼和目標沙箱名稱時，對`/packages`端點發出GET請求。

**API格式**

```http
GET /packages/preflight/{packageId}?targetSandbox=<sandbox_name
```

| 參數 | 說明 |
| --- | --- |
| `{PACKAGE_ID}` | 您要匯入的套件ID。 |

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

+++檢視回應

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
| `{QUERY_PARAMS}` | 篩選結果的選用查詢引數。 如需詳細資訊，請參閱[查詢引數](./appendix.md)的相關章節。 |

**要求**

下列請求列出所有成功的匯入工作。

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/exim/packages/jobs?property=requestType==IMPORT&property=jobStatus==SUCCESS&orderby=createdDate&start=0&limit=5 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
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

## 跨組織共用套件 {#org-linking}

沙箱工具API中的`/handshake`端點可讓您與其他組織合作以共用套件。

### 傳送共用要求 {#send-request}

透過向`/handshake/bulkCreate`端點發出POST請求，將請求傳送到目標夥伴組織以共用核准。 這是共用私人套件之前的必要專案。

**API格式**

```http
POST /handshake/bulkCreate
```

**要求**

下列請求會啟動目標夥伴組織與來源組織之間的共用核准。

```shell
curl -X POST \
  https://platform.adobe.io/data/foundation/exim/handshake/bulkCreate \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Accept: application/json' \
  -H 'Authorization: {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -d '{
      "targetIMSOrgIds":["acme@AdobeOrg"],
      "sourceIMSDetails":{
        "id":"acme@AdobeOrg",
        "name":"acme_org"
      } 
  }' 
```

| 屬性 | 說明 | 類型 | 必要 |
| --- | --- | --- | --- |
| `targetIMSOrgIds` | 要向其傳送共用請求的目標組織清單。 | 陣列 | 是 |
| `sourceIMSDetails` | 有關來源組織的詳細資料。 | 物件 | 是 |

**回應**

成功的回應會傳回關於共用請求的詳細資料。

```json
{
    "successfulRequests": {
        "acme@AdobeOrg": {
            "id": "{ID}",
            "version": 0,
            "createdDate": 1724938816798,
            "modifiedDate": 1724938816798,
            "createdBy": "{CREATED_BY}",
            "modifiedBy": "{MODIFIED_BY}",
            "sourceIMSOrgId": "{ORG_ID}",
            "targetIMSOrgId": "{TARGET_ID}",
            "sourceRegion": "va6",
            "sourceIMSOrgName": "{SOURCE_NAME}",
            "status": "APPROVAL_PENDING",
            "createdByName": "{CREATED_BY}",
            "modifiedByName": "{MODIFIED_BY}",
            "modifiedByIMSOrgId": "{ORG_ID}",
            "statusHistory": "[{\"actionTakenBy\":\"acme@98ff67fa661fdf6549420b.e\",\"actionTakenByName\":\"{NAME}\",\"actionTakenByImsOrgID\":\"{ORG_ID}\",\"action\":\"INITIATED\",\"actionTimeStamp\":1724938816885}]",
            "linkingId": "{LINKING_ID}"
        }
    },
    "failedRequests": {}
}
```

### 核准已接收的共用要求 {#approve-requests}

藉由對`/handshake/action`端點發出POST要求，核准來自目標夥伴組織的共用要求。 核准後，來源合作夥伴組織可以共用私人套件。

**API格式**

```http
POST /handshake/action
```

**請求**

下列要求會核准來自目標合作夥伴組織的共用要求。

```shell
curl -X POST  \
  https://platform.adobe.io/data/foundation/exim/handshake/action \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Accept: application/json' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -d '{
      "linkingID":"{LINKING_ID}",
      "status":"APPROVED",
      "reason":"Done",
      "targetIMSOrgDetails":{
          "id":"acme@AdobeOrg",
          "name":"acme",
          "region":"va7"
      }
  }'
```

| 屬性 | 說明 | 類型 | 必要 |
| --- | --- | --- | --- |
| `linkingID` | 您回應之共用要求的ID。 | 字串 | 是 |
| `status` | 正在對共用要求執行的動作。 可接受的值為`APPROVED`或`REJECTED`。 | 字串 | 是 |
| `reason` | 執行此動作的原因。 | 字串 | 是 |
| `targetIMSOrgDetails` | 目標組織的詳細資料，其中識別碼值應為目標組織的&#x200B;**識別碼**、名稱值應為目標組織的&#x200B;**NAME**，而區域值應為目標組織&#x200B;**REGION**。 | 物件 | 是 |

**回應**

成功的回應會傳回關於已核准共用要求的詳細資料。

```json
{
    "id": "{ID}",
    "version": 1,
    "createdDate": 1726737474000,
    "modifiedDate": 1726737541731,
    "createdBy": "{CREATED_BY}",
    "modifiedBy": "{MODIFIED_BY}",
    "sourceIMSOrgId": "{ORG_ID}",
    "targetIMSOrgId": "{TARGET_ID}",
    "sourceRegion": "va7",
    "targetRegion": "va7",
    "sourceOrgName": "{SOURCE_ORG}",
    "targetOrgName": "{TARGET_ORG}",
    "status": "APPROVED",
    "createdByName": "{CREATED_BY}",
    "modifiedByIMSOrgId": "{MODIFIED_BY}",
    "statusHistory": "[{\"actionTakenBy\":\"{ACTION_BY}\",\"actionTakenByName\":\"{NAME}\",\"actionTakenByImsOrgID\":\"acme@AdobeOrg\",\"action\":\"INITIATED\",\"actionTimeStamp\":1726737474450,\"reason\":null},{\"actionTakenBy\":null,\"actionTakenByName\":null,\"actionTakenByImsOrgID\":\"745F37C35E4B776E0A49421B@AdobeOrg\",\"action\":\"APPROVED\",\"actionTimeStamp\":1726737541818,\"reason\":\"Done\"}]",
    "linkingId": "{LINKING_ID}"
}
```

### 列出傳出/傳入的共用要求 {#outgoing-and-incoming-requests}

藉由對`handshake/list?property=status%3D%3DAPPROVED&requestType=INCOMING`端點發出GET要求，列出傳出和傳入的共用要求。

**API格式**

```http
GET handshake/list?property=status%3D%3DAPPROVED&requestType=INCOMING
```

| 參數 | 接受/預設值 |
| --- | --- |
| `property` | 指定要作為篩選依據的屬性，例如狀態。 狀態的可接受值為： `APPROVED`、`REJECTED`和`IN_PROGRESS`。 |
| `start` | 起始的預設值為`0`。 |
| `limit` | 限制的預設值為`20`。 |
| `orderBy` | 以遞增或遞減順序排序記錄。 |
| `requestType` | 接受`INCOMING`或`OUTGOING`。 |

**要求**

下列要求會傳回所有傳出與傳入的共用要求清單。

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/exim/handshake/list?property=status%3D%3DAPPROVED&requestType=INCOMING \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id:{ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Accept: application/json' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
```

**回應**

成功的回應會傳回傳出和傳入共用要求及其詳細資訊的清單。

```json
{
    "totalElements": 1,
    "currentPage": 0,
    "totalPages": 1,
    "hasPreviousPage": false,
    "hasNextPage": false,
    "data": [
        {
            "id": "{ID}",
            "version": 1,
            "createdDate": 1724929446000,
            "modifiedDate": 1724929617000,
            "modifiedBy": "{MODIFIED_BY}",
            "sourceIMSOrgId": "{ORG_ID}",
            "targetIMSOrgId": "{TARGET_ID}",
            "sourceRegion": "va7",
            "targetRegion": "va6",
             "sourceOrgName": "{SOURCE_ORG}",
            "targetOrgName": "{TARGET_ORG}",
            "status": "APPROVED",
            "createdByName": "{CREATED_BY}",
            "modifiedByName": "{MODIFIED_BY}",
            "modifiedByIMSOrgId": "{MODIFIED_BY}",
            "statusHistory": "[{\"actionTakenBy\":\"{ACTION_BY}\",\"actionTakenByName\":\"{NAME}\",\"actionTakenByImsOrgID\":\"{ORG_ID}\",\"action\":\"INITIATED\",\"actionTimeStamp\":1724929442467,\"reason\":null},{\"actionTakenBy\":null,\"actionTakenByName\":\"{NAME}\",\"actionTakenByImsOrgID\":\"{ORG_ID}\",\"action\":\"APPROVED\",\"actionTimeStamp\":1724929617531,\"reason\":\"Done\"}]",
            "linkingId": "{LINKING_ID}"
        }
    ],
    "nextPage": null,
    "pageSize": null
}
```

## 傳輸封裝

使用沙箱工具API中的`/transfer`端點來擷取及建立新的封裝共用要求。

### 新共用要求 {#share-request}

擷取已發佈來源組織的套件，並透過向`/transfer`端點發出POST要求來與目標組織共用，同時提供套件ID和目標組織的ID。

**API格式**

```http
POST /transfer
```

**要求**

以下請求會擷取來源組織套件並將其與目標組織共用。

```shell
curl -X POST \
  https://platform.adobe.io/data/foundation/exim/transfer/ \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -d '{
      "packageId": "{PACKAGE_ID}",
      "targets": [
          {
              "imsOrgId": "{TARGET_IMS_ORG}"
          }
      ]
  }'
```

| 屬性 | 說明 | 類型 | 必要 |
| --- | --- | --- | --- |
| `packageId` | 您要共用的套件ID。 | 字串 | 是 |
| `targets` | 要共用給封裝的組織清單。 | 陣列 | 是 |

**回應**

成功的回應會傳回要求的封裝及其共用狀態的詳細資料。

```json
[
    {
        "id": "{ID}",
        "version": 0,
        "createdDate": 1726480559313,
        "modifiedDate": 1726480559313,
        "createdBy": "{CREATED_BY}",
        "modifiedBy": "{MODIFIED_BY}",
        "sourceIMSOrgId": "{ORG_ID}",
        "targetIMSOrgId": "{TARGET_ID}",
        "packageId": "{PACKAGE_ID}",
        "status": "PENDING",
        "initiatedBy": "acme@3ec9197a65a86f34494221.e",
        "requestType": "PRIVATE"
    }
]
```

### 依ID擷取共用要求 {#fetch-transfer-by-id}

在提供傳輸ID時，透過向`/transfer/{TRANSFER_ID}`端點發出GET要求來擷取共用要求的詳細資料。

**API格式**

```http
GET /transfer/{TRANSFER_ID}
```

| 參數 | 說明 |
| --- | --- |
| `{TRANSFER_ID}` | 您要擷取的傳輸ID。 |

**要求**

下列要求會擷取識別碼為{TRANSFER_ID}的傳輸。

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/exim/transfer/0c843180a64c445ca1beece339abc04b \
  -H 'x-api-key: {API__KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}'
```

**回應**

成功回應會傳回共用請求的詳細資料。

```json
{
    "id": "{ID}",
    "sourceIMSOrgId": "{ORG_ID}",
    "sourceOrgName": "{SOURCE_ORG}",
    "targetIMSOrgId": "{TARGET_ID}",
    "targetOrgName": "{TARGET_ORG}",
    "packageId": "{PACKAGE_ID}",
    "packageName": "{PACKAGE_NAME}",
    "status": "COMPLETED",
    "initiatedBy": "{INITIATED_BY}",
    "createdDate": 1724442856000,
    "requestType": "PRIVATE"
}
```

### 擷取共用清單 {#transfers-list}

向`/transfer/list?{QUERY_PARAMETERS}`端點發出GET要求，並視需要變更查詢引數，以擷取傳輸要求清單。

**API格式**

```http
GET `/transfer/list?{QUERY_PARAMETERS}`
```

| 參數 | 接受/預設值 |
| --- | --- |
| `property` | 指定要作為篩選依據的屬性，例如狀態。 狀態的可接受值為： `COMPLETED`、`PENDING`、`IN_PROGRESS`、`FAILED`。 |
| `start` | 起始的預設值為`0`。 |
| `limit` | 限制的預設值為`20`。 |
| `orderBy` | 排序只接受`createdDate`欄位。 |

**要求**

以下請求會從提供的搜尋引數中擷取傳輸請求清單。

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/exim/transfer/list?property=status==COMPLETED&start=0&limit=2&orderBy=-createdDate \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}'
```

**回應**

成功的回應會從提供的搜尋引數傳回所有傳輸要求的清單。

```json
{
    "totalElements": 43,
    "currentPage": 0,
    "totalPages": 22,
    "hasPreviousPage": false,
    "hasNextPage": true,
    "data": [
        {
            "id": "{ID}",
            "sourceIMSOrgId": "{ORG_ID}",
            "sourceOrgName": "{SOURCE_ORG}",
            "targetIMSOrgId": "{TARGET_ID}",
            "targetOrgName": "{TARGET_ORG}",
            "packageId": "{PACKAGE_ID}",
            "packageName": "{PACKAGE_NAME}",
            "status": "COMPLETED",
            "initiatedBy": "{INITIATED_BY}",
            "completedTime": 1726129077000,
            "createdDate": 1726129062000,
            "requestType": "PRIVATE"
        },
        {
            "id": "{ID}",
            "sourceIMSOrgId": "{ORG_ID}",
            "sourceOrgName": "{SOURCE_ORG}",
            "targetIMSOrgId": "{TARGET_ID}",
            "targetOrgName": "{TARGET_ORG}",
            "packageId": "{PACKAGE_ID}",
            "packageName": "{PACKAGE_NAME}",
            "status": "COMPLETED",
            "initiatedBy": "{INITIATED_BY}",
            "completedTime": 1726066046000,
            "createdDate": 1726065936000,
            "requestType": "PRIVATE"
        }
    ],
    "nextPage": null,
    "pageSize": null
}
```

### 將套件可用性從私人更新為公開 {#update-availability}

透過向`/packages/update`端點發出GET要求，將套件從私用變更為公用。 依預設，會建立具有私人可用性的套件。

**API格式**

```http
PUT `/packages/update`
```

**要求**

以下請求會將套件的可用性從私人變更為公開。

```shell
curl -X PUT \
  https://platform.adobe.io/data/foundation/exim/packages \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-type: application/json' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -d '{
      "id":"{ID}",
      "action":"UPDATE",
      "packageVisibility":"PUBLIC"
  }'
```

| 屬性 | 說明 | 類型 | 必要 |
| --- | --- | --- | --- |
| `id` | 要更新的套件的ID。 | 字串 | 是 |
| `action` | 若要更新公開的可見度，動作值應該是&#x200B;**UPDATE**。 | 字串 | 是 |
| `packageVisbility` | 若要更新可見性，packageVisibility值應該是&#x200B;**PUBLIC**。 | 字串 | 是 |

**回應**

成功的回應會傳回封裝及其可見性的詳細資料。

```json
{
    "id": "{ID}",
    "version": 7,
    "createdDate": 1729624618000,
    "modifiedDate": 1729658596340,
    "createdBy": "{CREATED_BY}",
    "modifiedBy": "{MODIFIED_BY}",
    "name": "acme",
    "imsOrgId": "{ORG_ID}",
    "packageType": "PARTIAL",
    "expiry": 1737434596325,
    "status": "PUBLISH_FAILED",
    "packageVisibility": "PUBLIC",
    "artifactsList": [
        {
            "id": "{ID}",
            "type": "PROFILE_SEGMENT",
            "found": false,
            "count": 0,
            "title": "Acme Profile Segment"
        }
    ],
    "schemaMapping": {},
    "sourceSandbox": {
        "name": "acme-sandbox",
        "imsOrgId": "{ORG_ID}",
        "empty": false
    }
}
```

### 要求匯入公用套件 {#pull-public-package}

透過向`/transfer/pullRequest`端點發出POST要求，從具有公開可用性的來源組織匯入套件。

**API格式**

```http
POST /transfer/pullRequest
```

**要求**

下列請求將會匯入套件，並設定其公開可用性。

```shell
curl -X POST \
  https://platform.adobe.io/data/foundation/exim/transfer/pullRequest \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Accept: application/json' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -d '{
      "imsOrgId": "{ORG_ID}",
      "packageId": "{PACKAGE_ID}"
  }'
```

| 屬性 | 說明 | 類型 | 必要 |
| --- | --- | --- | --- |
| `imsOrgId` | 封裝來源組織的ID。 | 字串 | 是 |
| `packageId` | 要匯入的套件中的id。 | 字串 | 是 |

**回應**

成功的回應會傳回匯入之公用套件的詳細資料。

```json
{
    "id": "{ID}",
    "version": 0,
    "createdDate": 1729658890425,
    "modifiedDate": 1729658890425,
    "createdBy": "{CREATED_BY}",
    "modifiedBy": "{MODIFIED_BY}",
    "sourceIMSOrgId": "{ORG_ID}",
    "targetIMSOrgId": "{TARGET_ID}",
    "packageId": "{PACKAGE_ID}",
    "status": "PENDING",
    "initiatedBy": "{INITIATED_BY}",
    "pipelineMessageId": "{MESSAGE_ID}",
    "requestType": "PUBLIC"
}
```

### 列出公用套件 {#list-public-packages}

透過向`/transfer/list?{QUERY_PARAMS}`端點發出GET要求，擷取具有公開可見性的套件清單。

**API格式**

```http
GET /transfer/list?{QUERY_PARAMS}
```

| 參數 | 接受/預設值 |
| --- | --- |
| `property` | 指定要作為篩選依據的屬性，例如狀態。 狀態的可接受值為： `COMPLETED`和`FAILED`。 |
| `start` | 起始的預設值為`0`。 |
| `limit` | 限制的預設值為`20`。 |
| `orderBy` | 排序只接受`createdDate`欄位。 |
| `requestType` | 接受`PUBLIC`或`PRIVATE`。 |

**要求**

以下請求會擷取具有公開可用性的套件清單。

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/exim/transfer/list?property=status%3D%3DCOMPLETED%2CFAILED&requestType=PUBLIC&orderby=-createdDate \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Accept: application/json' \
  -H 'Authorization: {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
```

**回應**

成功的回應會傳回公用套件清單及其詳細資料。

+++檢視回應

```json
{
    "totalElements": 14,
    "currentPage": 0,
    "totalPages": 1,
    "hasPreviousPage": false,
    "hasNextPage": false,
    "data": [
        {
            "id": "{ID}",
            "sourceIMSOrgId": "{ORG_ID}",
            "sourceOrgName": "{SOURCE_NAME}",
            "targetIMSOrgId": "{TARGET_ID}",
            "targetOrgName": "{TARGET_ORG}",
            "packageId": "{PACKAGE_ID}",
            "packageName": "Public package demo",
            "status": "COMPLETED",
            "initiatedBy": "{INITIATED_BY}",
            "completedTime": 1729359318000,
            "createdDate": 1729359316000,
            "requestType": "PUBLIC"
        },
        {
            "id": "{ID}",
            "sourceIMSOrgId": "{ORG_ID}",
            "sourceOrgName": "{SOURCE_NAME}",
            "targetIMSOrgId": "{TARGET_ID}",
            "targetOrgName": "{TARGET_NAME}",
            "packageId": "{PACKAGE_ID}",
            "packageName": "Public package demo",
            "status": "COMPLETED",
            "initiatedBy": "{INITIATED_BY}",
            "completedTime": 1729359284000,
            "createdDate": 1729359283000,
            "requestType": "PUBLIC"
        },
        {
            "id": "{ID}",
            "sourceIMSOrgId": "{ORG_ID}",
            "sourceOrgName": "{SOURCE_NAME}",
            "targetIMSOrgId": "{TARGET_ID}",
            "targetOrgName": "{TARGET_NAME}",
            "packageId": "{PACKAGE_ID}",
            "packageName": "Test Private Flow Final",
            "status": "COMPLETED",
            "initiatedBy": "{INITIATED_BY}",
            "completedTime": 1729284462000,
            "createdDate": 1729275962000,
            "requestType": "PUBLIC"
        },
        {
            "id": "{ID}",
            "sourceIMSOrgId": "{ORG_ID}",
            "sourceOrgName": "{SOUCE_NAME}",
            "targetIMSOrgId": "{TARGET_ID}",
            "targetOrgName": "{TARGET_NAME}",
            "packageId": "{PACKAGE_ID}",
            "packageName": "Fest",
            "status": "FAILED",
            "initiatedBy": "{INITIATED_BY}",
            "completedTime": 1729284104000,
            "createdDate": 1729253854000,
            "requestType": "PUBLIC"
        },
        {
            "id": "{ID}",
            "sourceIMSOrgId": "{ORG_ID}",
            "sourceOrgName": "{SOURCE_NAME}",
            "targetIMSOrgId": "{TARGET_ID}",
            "targetOrgName": "{TARGET_NAME}",
            "packageId": "{PACKAGE_ID}",
            "packageName": "PublicPackageSharing",
            "status": "COMPLETED",
            "initiatedBy": "{INITIATED_BY}",
            "completedTime": 1729284835000,
            "createdDate": 1729253556000,
            "requestType": "PUBLIC"
        },
        {
            "id": "{ID}",
            "sourceIMSOrgId": "{ORG_ID}",
            "sourceOrgName": "{SOURCE_NAME}",
            "targetIMSOrgId": "{TARGET_ID}",
            "targetOrgName": "{TARGET_NAME}",
            "packageId": "{PACKAGE_ID}",
            "packageName": "PublicPackageSharing",
            "status": "COMPLETED",
            "initiatedBy": "{INITIATED_BY}",
            "completedTime": 1729284835000,
            "createdDate": 1729253556000,
            "requestType": "PUBLIC"
        },
        {
            "id": "{ID}",
            "sourceIMSOrgId": "{ORG_ID}",
            "sourceOrgName": "{SOURCE_NAME}",
            "targetIMSOrgId": "{TARGET_ID}",
            "targetOrgName": "{TARGET_NAME}",
            "packageId": "{PACKAGE_ID}",
            "packageName": "PublicPackageSharing",
            "status": "COMPLETED",
            "initiatedBy": "{INITIATED_BY}",
            "completedTime": 1729284835000,
            "createdDate": 1729253556000,
            "requestType": "PUBLIC"
        },
        {
            "id": "{ID}",
            "sourceIMSOrgId": "{ORG_ID}",
            "sourceOrgName": "{SOURCE_NAME}",
            "targetIMSOrgId": "{TARGET_ID}",
            "targetOrgName": "{TARGET_NAME}",
            "packageId": "{PACKAGE_ID}",
            "packageName": "Public Package Audit Test",
            "status": "COMPLETED",
            "initiatedBy": "{INITIATED_BY}",
            "completedTime": 1729284667000,
            "createdDate": 1729253421000,
            "requestType": "PUBLIC"
        },
        {
            "id": "{ID}",
            "sourceIMSOrgId": "{ORG_ID}",
            "sourceOrgName": "{SOURCE_NAME}",
            "targetIMSOrgId": "{TARGET_ID}",
            "targetOrgName": "{TARGET_NAME}",
            "packageId": "{PACKAGE_ID}",
            "packageName": "Public Package Audit Test",
            "status": "COMPLETED",
            "initiatedBy": "{INITIATED_BY}",
            "completedTime": 1729284957000,
            "createdDate": 1729253143000,
            "requestType": "PUBLIC"
        },
        {
            "id": "{ID}",
            "sourceIMSOrgId": "{ORG_ID}",
            "sourceOrgName": "{SOURCE_NAME}",
            "targetIMSOrgId": "{TARGET_ID}",
            "targetOrgName": "{TARGET_NAME}",
            "packageId": "{PACKAGE_ID}",
            "packageName": "Public Package Audit Test",
            "status": "COMPLETED",
            "initiatedBy": "{INITIATED_BY}",
            "completedTime": 1729284562000,
            "createdDate": 1729252975000,
            "requestType": "PUBLIC"
        },
        {
               "id": "{ID}",
            "sourceIMSOrgId": "{ORG_ID}",
            "sourceOrgName": "{SOURCE_NAME}",
            "targetIMSOrgId": "{TARGET_ID}",
            "targetOrgName": "{TARGET_NAME}",
            "packageId": "{PACKAGE_ID}",
            "packageName": "Private Package Test 1",
            "status": "COMPLETED",
            "initiatedBy": "{INITIATED_BY}",
            "completedTime": 1729284262000,
            "createdDate": 1729229755000,
            "requestType": "PUBLIC"
        },
        {
            "id": "{ID}",
            "sourceIMSOrgId": "{ORG_ID}",
            "sourceOrgName": "{SOURCE_NAME}",
            "targetIMSOrgId": "{TARGET_ID}",
            "targetOrgName": "{TARGET_NAME}",
            "packageId": "{PACKAGE_ID}",
            "packageName": "Demo Package 1016",
            "status": "COMPLETED",
            "initiatedBy": "{INITIATED_BY}",
            "completedTime": 1729284784000,
            "createdDate": 1729208888000,
            "requestType": "PUBLIC"
        },
        {
            "id": "{ID}",
            "sourceIMSOrgId": "{ORG_ID}",
            "sourceOrgName": "{SOURCE_NAME}",
            "targetIMSOrgId": "{TARGET_ID}",
            "targetOrgName": "{TARGET_NAME}",
            "packageId": "{PACKAGE_ID}",
            "packageName": "Public Package test 1",
            "status": "COMPLETED",
            "initiatedBy": "{INITIATED_BY}",
            "completedTime": 1729284934000,
            "createdDate": 1729153097000,
            "requestType": "PUBLIC"
        },
        {
            "id": "{ID}",
            "sourceIMSOrgId": "{ORG_ID}",
            "sourceOrgName": "{SOURCE_NAME}",
            "targetIMSOrgId": "{TARGET_ID}",
            "targetOrgName": "{TARGET_NAME}",
            "packageId": "{PACKAGE_ID}",
            "packageName": "Public Package test 1",
            "status": "COMPLETED",
            "initiatedBy": "{INITIATED_BY}",
            "completedTime": 1729284912000,
            "createdDate": 1729153043000,
            "requestType": "PUBLIC"
        }
    ],
    "nextPage": null,
    "pageSize": null
}
```

+++

## 複製封裝裝載(#package-payload)

您可以透過向`/packages/payload`端點發出GET請求，複製公用套件的裝載，端點在請求路徑中包含套件的對應ID。

**API格式**

```http
GET /packages/payload/{PACKAGE_ID}
```

| 參數 | 說明 |
| --- | --- |
| `{PACKAGE_ID}` | 您要複製的套件ID。 |

**要求**

下列要求會擷取ID為{PACKAGE_ID}的封裝裝載。

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/exim/packages/payload/{PACKAGE_ID} \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Accept: application/json' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
```

| 屬性 | 說明 | 類型 | 必要 |
| --- | --- | --- | --- |
| `imsOrdId` | 套件所屬組織的識別碼。 | 字串 | 是 |
| `packageId` | 您請求之裝載的套件識別碼。 | 字串 | 是 |

**回應**

成功的回應會傳回套件的裝載。

```json
{
    "imsOrgId": "{ORG_ID}",
    "packageId": "{PACKAGE_ID}"
}
```

## 移轉物件組態更新

使用沙箱工具API中的/packages端點來移轉物件設定更新。

### 更新作業(#update-operations)

提供套件ID，對`/packages/{packageId}/version/compare`端點發出POST要求，將指定的或最新版本的套件快照集與來源沙箱的目前狀態或先前匯入套件的目標沙箱進行比較。

***API格式***

```http
PATCH /packages/{packageId}/version/compare
```

| 屬性 | 說明 | 類型 | 必要 |
| --- | --- | --- | --- |
| `packageId` | 套件的ID。 | 字串 | 是 |

**要求**

```shell
curl -X POST \
  https://platform-stage.adobe.io/data/foundation/exim/packages/{PACKAGE_ID}/version/compare/ \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Accept: application/json' \
  -H 'Content-Type: application/json' \
  -d '{
      "triggerNew": true,
      "targetSandbox": "{SANDBOX_NAME}"
  }'
```

| 屬性 | 說明 | 類型 | 必要 |
| --- | --- | --- | --- |
| `triggerNew` | 此旗標可觸發新的差異計算工作，即使已有作用中或完成的工作存在。 | 布林值 | 無 |
| `targetSandbox` | 代表必須用來計算差異的目標沙箱名稱。 如果未指定，會將來源沙箱當作目標沙箱。 | 字串 | 無 |

**回應**

先前完成之工作的成功回應會傳回工作物件與先前計算的差異結果。 新完成的作業會傳回JobId。

+++檢視回應（已提交的工作）

```json
{
    "status": "OK",
    "type": "SUCCESS",
    "ajo": false,
    "message": "Job with ID: {JOB_ID}",
    "object": {
        "id": "c4b7d07ae4c646279e2070a31c50bd5c",
        "name": "Compute Job Package: {SNAPSHOT_ID}",
        "description": null,
        "visibility": "TENANT",
        "requestType": "VERSION",
        "expiry": 0,
        "snapshotId": "{SNAPSHOT_ID}",
        "packageVersion": 0,
        "createdTimestamp": 0,
        "modifiedTimestamp": 0,
        "type": "PARTIAL",
        "jobStatus": "SUCCESS",
        "jobType": "COMPUTE",
        "counter": 0,
        "imsOrgId": "{ORG_ID}",
        "sourceSandbox": {
            "name": "prod",
            "imsOrgId": "{ORG_ID}",
            "empty": false
        },
        "destinationSandbox": {
            "name": "amanda-1",
            "imsOrgId": "{ORG_ID}",
            "empty": false
        },
        "deltaPackageVersion": {
            "packageId": "{PACKAGE_ID}",
            "currentVersion": 0,
            "validated": false,
            "rootArtifacts": [
                {
                    "id": "https://ns.adobe.com/sandboxtoolingstage/schemas/355f461cbfb662fd0d12d06aeab34e206efcfa5d913604de",
                    "type": "REGISTRY_SCHEMA",
                    "found": false,
                    "count": 0
                }
            ],
            "eximGraphDelta": {
                "vertices": [],
                "pluginDeltas": [
                    {
                        "sourceArtifact": {
                            "id": "https://ns.adobe.com/sandboxtoolingstage/mixins/9fad8b185640a2db7daf9bb1295543ee8cb5965d80a21e8d",
                            "type": "REGISTRY_MIXIN",
                            "found": false,
                            "count": 0,
                            "title": "Custom FieldGroup 2"
                        },
                        "targetArtifact": {
                            "id": "https://ns.adobe.com/sandboxtoolingstage/mixins/b7fa3024777ef11b68c5121e937d8543677093f4f0e63a5f",
                            "type": "REGISTRY_MIXIN",
                            "found": false,
                            "count": 0,
                            "title": "Custom FieldGroup 2_1738766274074"
                        },
                        "changes": [
                            {
                                "op": "replace",
                                "path": "/title",
                                "oldValue": "Custom FieldGroup 2_1738766274074",
                                "newValue": "Custom FieldGroup 2"
                            },
                            {
                                "op": "replace",
                                "path": "/description",
                                "oldValue": "Description for furnished object",
                                "newValue": ""
                            }
                        ]
                    },
                    {
                        "sourceArtifact": {
                            "id": "https://ns.adobe.com/sandboxtoolingstage/mixins/304ac900943716c8bd99e6aaf6aa840aac91995729f1987f",
                            "type": "REGISTRY_MIXIN",
                            "found": false,
                            "count": 0,
                            "title": "Custom FieldGroup 4"
                        },
                        "targetArtifact": {
                            "id": "https://ns.adobe.com/sandboxtoolingstage/mixins/34c9add91cce4a40d68a0e715c9f0a16048871734f8c8b74",
                            "type": "REGISTRY_MIXIN",
                            "found": false,
                            "count": 0,
                            "title": "Custom FieldGroup 4_1738766274074"
                        },
                        "changes": [
                            {
                                "op": "replace",
                                "path": "/title",
                                "oldValue": "Custom FieldGroup 4_1738766274074",
                                "newValue": "Custom FieldGroup 4"
                            },
                            {
                                "op": "replace",
                                "path": "/description",
                                "oldValue": "Description for furnished object",
                                "newValue": ""
                            }
                        ]
                    }
                ]
            }
        },
        "importReplacementMap": {
            "https://ns.adobe.com/sandboxtoolingstage/mixins/9fad8b185640a2db7daf9bb1295543ee8cb5965d80a21e8d": "https://ns.adobe.com/sandboxtoolingstage/mixins/b7fa3024777ef11b68c5121e937d8543677093f4f0e63a5f",
            "5a45f8cd309d5ed5797be9a0af65e89152a51d57a6c74b52": "4ae041fa182d6faf2e7c56463399170d913138a7c5712909",
            "https://ns.adobe.com/sandboxtoolingstage/schemas/b2b7705e770a35341b8bc5ec5e3644d9c7387266777fe4ba": "https://ns.adobe.com/sandboxtoolingstage/schemas/838c4e21ad81543ac14238ac1756012f7f98f0e0bec6b425",
            "https://ns.adobe.com/sandboxtoolingstage/schemas/355f461cbfb662fd0d12d06aeab34e206efcfa5d913604de": "https://ns.adobe.com/sandboxtoolingstage/schemas/9a55692d527169d0239e126137a694ed9db2406c9bcbd06a",
            "8f45c79235c91e7f0c09af676a77d170a34b5ee0ad5de72c": "65d755cc3300674c3cfcec620c59876af07f046884afd359",
            "f04b8e461396ff426f8ba8dc5544f799bf287baa8e0fa5c": "b6fa821ada8cb97cac384f0b0354bbe74209ec97fb6a83a3",
            "https://ns.adobe.com/sandboxtoolingstage/mixins/304ac900943716c8bd99e6aaf6aa840aac91995729f1987f": "https://ns.adobe.com/sandboxtoolingstage/mixins/34c9add91cce4a40d68a0e715c9f0a16048871734f8c8b74",
            "c8304f3cb7986e8c9b613cd8d832125bd867fb4a5aedf67a": "4d21e9bf89ce0042b52d7d41ff177a7697d695e2617d1fc1"
        },
        "schemaFieldMappings": null
    }
}
```

+++

+++檢視回應（新提交的工作）

```json
{
    "status": "OK",
    "type": "SUCCESS",
    "ajo": false,
    "message": "Job with ID: {JOB_ID}",
    "object": {
        "id": "aa5cfacf35a8478c8cf44a675fab1c30 ",
        "name": "Compute Job Package: {SNAPSHOT_ID}",
        "description": null,
        "visibility": "TENANT",
        "requestType": "VERSION",
        "expiry": 0,
        "snapshotId": "{SNAPSHOT_ID}",
        "packageVersion": 0,
        "createdTimestamp": 0,
        "modifiedTimestamp": 0,
        "type": "PARTIAL",
        "jobStatus": "IN_PROGRESS",
        "jobType": "COMPUTE",
        "counter": 0,
        "imsOrgId": "{ORG_ID}",
        "sourceSandbox": {
            "name": "prod",
            "imsOrgId": "{ORG_ID}",
            "empty": false
        },
        "destinationSandbox": {
            "name": "amanda-1",
            "imsOrgId": "{ORG_ID}",
            "empty": false
        },
        "schemaFieldMappings": null
    }
}
```

+++

### 更新套件版本(#package-versioning)

提供套件ID，向`/packages/{packageId}/version/save`端點發出GET請求，使用每個物件的來源沙箱中最新快照集將套件升級為新版本。

***API格式***

```http
PATCH /packages/{packageId}/version/save
```

| 屬性 | 說明 | 類型 | 必要 |
| --- | --- | --- | --- |
| `packageId` | 套件的ID。 | 字串 | 是 |

**要求**

```shell
curl -X POST \
  https://platform-stage.adobe.io/data/foundation/exim/packages/{PACKAGE_ID}/version/save/ \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Accept: application/json' \
  -H 'Content-Type: application/json' \
```

**回應**

成功的回應會傳回版本升級的工作狀態。

```json
{
    "id": "3cec9bae662e43d9b9106fcbf7744a75",
    "name": "Version Job Package: {JOB_ID}",
    "description": null,
    "visibility": "TENANT",
    "requestType": "VERSION",
    "expiry": 0,
    "snapshotId": "{SNAPSHOT_ID}",
    "packageVersion": 2,
    "createdTimestamp": 0,
    "modifiedTimestamp": 0,
    "type": "PARTIAL",
    "jobStatus": "PENDING",
    "jobType": "UPGRADE",
    "counter": 0,
    "imsOrgId": "{ORG_ID}",
    "sourceSandbox": {
        "name": "prod",
        "imsOrgId": "{ORG_ID}",
        "empty": false
    },
    "destinationSandbox": {
        "name": "prod",
        "imsOrgId": "{ORG_ID}",
        "empty": false
    },
    "schemaFieldMappings": null
}
```

### 擷取套件版本記錄(#package-version-history)

透過向`/packages/{packageId}/history`端點發出GET請求並提供套件ID，擷取套件的版本設定歷史記錄，包括時間戳記和修飾元。

***API格式***

```http
PATCH /packages/{packageId}/history
```

| 屬性 | 說明 | 類型 | 必要 |
| --- | --- | --- | --- |
| `packageId` | 套件的ID。 | 字串 | 是 |

**要求**

```shell
curl -X POST \
  https://platform-stage.adobe.io/data/foundation/exim/packages/{PACKAGE_ID}/history/ \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Accept: application/json' \
  -H 'Content-Type: application/json' \
```

**回應**

成功的回應會傳回套件的版本記錄。

```json
[
    {
        "id": "cb68591a1ed941e191e7f52e33637a26",
        "version": 0,
        "createdDate": 1739516784000,
        "modifiedDate": 1739516784000,
        "createdBy": "{CREATED_BY}",
        "modifiedBy": "{MODIFIED_BY}",
        "imsOrgId": "{ORG_ID}",
        "packageVersion": 3
    },
    {
        "id": "e26189e6e4df476bb66c3fc3e66a1499",
        "version": 0,
        "createdDate": 1739343268000,
        "modifiedDate": 1739343268000,
        "createdBy": "{CREATED_BY}",
        "modifiedBy": "{MODIFIED_BY}",
        "imsOrgId": "{ORG_ID}",
        "packageVersion": 2
    },
    {
        "id": "11af34c0eee449ac84ef28c66d9383e3",
        "version": 0,
        "createdDate": 1739343073000,
        "modifiedDate": 1739343073000,
        "createdBy": "{CREATED_BY}",
        "modifiedBy": "{MODIFIED_BY}",
        "imsOrgId": "{ORG_ID}",
        "packageVersion": 1
    }
]
```

### 提交更新工作(#submit-update)

藉由提供套件ID向`/packages/{packageId}/import`端點發出PATCH要求，將新的更新推播至目標沙箱物件。

***API格式***

```http
PATCH /packages/{packageId}/import
```

| 屬性 | 說明 | 類型 | 必要 |
| --- | --- | --- | --- |
| `packageId` | 套件的ID。 | 字串 | 是 |

**要求**

```shell
curl -X POST \
  https://platform-stage.adobe.io/data/foundation/exim/packages/{PACKAGE_ID}/import/ \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Accept: application/json' \
  -H 'Content-Type: application/json' \
  -d '{
      "id": "50fd94f8072b4f248737a2b57b41058f",
      "name": "Test Update",
      "destinationSandbox": {
        "name": "test-sandbox-sbt",
        "imsOrgId": "{ORG_ID}"
      },
      "overwriteMappings": {
        "https://ns.adobe.com/sandboxtoolingstage/schemas/327a48c83a5359f8160420a00d5a07f0ba8631a1fd466f9e" : {
            "id" : "https://ns.adobe.com/sandboxtoolingstage/schemas/e346bb2cd7b26576cb51920d214aebbd42940a9bf94a75cd",
            "type" : "REGISTRY_SCHEMA"
        }
      }
  }'
```

**回應**

成功的回應會傳回更新的作業ID。

```json
{
    "id": "3cec9bae662e43d9b9106fcbf7744a75",
    "name": "Update Job Name",
    "description": "Update Job Description",
    "visibility": "TENANT",
    "requestType": "IMPORT",
    "expiry": 0,
    "snapshotId": "{SNAPSHOT_ID}",
    "packageVersion": 2,
    "createdTimestamp": 0,
    "modifiedTimestamp": 0,
    "type": "PARTIAL",
    "jobStatus": "PENDING",
    "jobType": "UPDATE",
    "counter": 0,
    "imsOrgId": "{ORG_ID}",
    "sourceSandbox": {
        "name": "prod",
        "imsOrgId": "{ORG_ID}",
        "empty": false
    },
    "destinationSandbox": {
        "name": "amanda-1",
        "imsOrgId": "{ORG_ID}",
        "empty": false
    },
    "schemaFieldMappings": null
}
```

### 停用套件(#disable-update)的更新和覆寫

透過向`/packages/{packageId}/?{QUERY_PARAMS}`端點發出GET請求，並提供套件ID，停用不支援這些套件的更新和覆寫。

***API格式***

```http
PATCH /packages/{packageId}?{QUERY_PARAMS}
```

| 屬性 | 說明 | 類型 | 必要 |
| --- | --- | --- | --- |
| `packageId` | 套件的ID。 | 字串 | 是 |
| {QUERY_PARAM} | getCapabilites查詢引數。 這應該設定為`true`或`false` | 布林值 | 是 |

**要求**

```shell
curl -X POST \
  https://platform-stage.adobe.io/data/foundation/exim/packages/{PACKAGE_ID}?getCapabilities=true'/ \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Accept: application/json' \
  -H 'Content-Type: application/json' \
```

**回應**

成功的回應會傳回套件功能的清單。

```json
{
    "id": "80230dde96574a828191144709bb9b51",
    "version": 3,
    "createdDate": 1749808582000,
    "modifiedDate": 1749808648000,
    "createdBy": "{CREATED_BY}",
    "modifiedBy": "{MODIFIED_BY}",
    "name": "Ankit_Primary_Descriptor_Test",
    "description": "RestPackage",
    "imsOrgId": "{ORG_ID}",
    "clientId": "usecasebuilder",
    "packageType": "PARTIAL",
    "expiry": 1757584598000,
    "publishDate": 1749808648000,
    "status": "PUBLISHED",
    "packageVisibility": "PRIVATE",
    "latestPackageVersion": 0,
    "packageAccessType": "TENANT",
    "artifactsList": [
        {
            "id": "https://ns.adobe.com/sandboxtoolingstage/schemas/1c767056056de64d8030380d1b9f570d26bc15501a1e0e95",
            "altId": null,
            "type": "REGISTRY_SCHEMA",
            "found": false,
            "count": 0
        }
    ],
    "schemaMapping": {},
    "sourceSandbox": {
        "name": "atul-sandbox",
        "imsOrgId": "{ORG_ID}",
        "empty": false
    },
    "packageCapabilities": {
        "capabilities": [
            "VERSIONABLE"
        ]
    }
}
```
