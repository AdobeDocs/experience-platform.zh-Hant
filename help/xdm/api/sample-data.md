---
keywords: Experience Platform;home；熱門主題；api;API;XDM;XDM系統；體驗資料模型；體驗資料模型；資料模型；資料模型；示例資料；rpc;
solution: Experience Platform
title: 範例資料API端點
description: 方案註冊表API中的/sampledata端點允許您生成映射到任何現有XDM方案結構的示例資料。
topic: developer guide
translation-type: tm+mt
source-git-commit: 0727ffa0c72bcb6a85de1a13215b691b97889b70
workflow-type: tm+mt
source-wordcount: '321'
ht-degree: 1%

---


# 範例資料端點

為了將資料收錄至Adobe Experience Platform，資料的格式和結構必須符合現有的體驗資料模型(XDM)架構。 根據特定資料集的架構複雜性，很難判斷資料集在擷取時所需的確切資料形狀。

使用[!DNL Schema Registry] API中的`/sampledata`端點，您可以為任何先前建立的方案生成示例提取對象。

## 快速入門

本指南中使用的端點是[[!DNL Schema Registry] API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/schema-registry.yaml)的一部分。 在繼續之前，請先閱讀[快速入門手冊](./getting-started.md)，以取得相關檔案的連結、閱讀本檔案中範例API呼叫的指南，以及成功呼叫任何Experience PlatformAPI所需之必要標題的重要資訊。

示例資料端點是[!DNL Schema Registry]支援的遠程過程調用(RPC)的一部分。 與[!DNL Schema Registry] API中的其他端點不同，RPC端點不需要額外的標題，如`Accept`或`Content-Type`，也不使用`CONTAINER_ID`。 而必須改用`/rpc`命名空間，如下列API呼叫所示。

## 檢索模式的示例資料

通過在指向端點的GET請求路徑中指定方案的ID，可以檢索方案庫中任何方案的示例資料。

**API格式**

```http
GET /rpc/sampledata/{SCHEMA_ID}
```

| 參數 | 說明 |
| --- | --- |
| `{SCHEMA_ID}` | 要為其生成示例資料的方案的`meta:altId`或URL編碼的`$id`。 |

**請求**

以下請求會為忠誠度成員方案生成示例資料。

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/schemaregistry/rpc/sampledata/_{TENANT_ID}.schemas.533ca5da28087c44344810891b0f03d9 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**回應**

成功的響應返回指定方案的示例資料對象。

```json
{
    "@id": "/uri-reference",
    "_{TENANT_ID}": {
        "favoriteHotel": "string",
        "loyalty": {
            "loyaltyId": "string",
            "loyaltyLevel": "string",
            "loyaltyPoints": 4862,
            "memberSince": "2018-11-12T20:20:39+00:00"
        }
    },
    "repo:createDate": "2004-10-23T12:00:00-06:00",
    "repo:modifyDate": "2004-10-23T12:00:00-06:00",
    "xdm:createdByBatchID": "/uri-reference",
    "xdm:faxPhone": {
        "xdm:extension": "string",
        "xdm:number": "string",
        "xdm:primary": false,
        "xdm:status": "active",
        "xdm:statusReason": "string",
        "xdm:validity": "consistent"
    },
    "xdm:homeAddress": {
        "@id": "/uri-reference",
        "repo:createDate": "2004-10-23T12:00:00-06:00",
        "repo:modifyDate": "2004-10-23T12:00:00-06:00",
        "schema:description": "string",
        "schema:elevation": 31148.05,
        "schema:latitude": 29.25,
        "schema:longitude": -145.42,
        "xdm:city": "string",
        "xdm:country": "string",
        "xdm:countryCode": "US",
        "xdm:createdByBatchID": "/uri-reference",
        "xdm:dmaID": 1612,
        "xdm:label": "string",
        "xdm:lastVerifiedDate": "2018-01-12",
        "xdm:modifiedByBatchID": "/uri-reference",
        "xdm:msaID": 26375,
        "xdm:postOfficeBox": "string",
        "xdm:postalCode": "string",
        "xdm:primary": false,
        "xdm:region": "string",
        "xdm:repositoryCreatedBy": "string",
        "xdm:repositoryLastModifiedBy": "string",
        "xdm:state": "string",
        "xdm:stateProvince": "US-CA",
        "xdm:status": "active",
        "xdm:statusReason": "string",
        "xdm:street1": "string",
        "xdm:street2": "string",
        "xdm:street3": "string",
        "xdm:street4": "string"
    },
    "xdm:homePhone": {
        "xdm:extension": "string",
        "xdm:number": "string",
        "xdm:primary": false,
        "xdm:status": "active",
        "xdm:statusReason": "string",
        "xdm:validity": "consistent"
    },
    "xdm:identityMap": {
        "key": [
            {
                "xdm:authenticatedState": "ambiguous",
                "xdm:id": "string",
                "xdm:primary": false
            }
        ]
    },
    "xdm:mobilePhone": {
        "xdm:extension": "string",
        "xdm:number": "string",
        "xdm:primary": false,
        "xdm:status": "active",
        "xdm:statusReason": "string",
        "xdm:validity": "consistent"
    },
    "xdm:modifiedByBatchID": "/uri-reference",
    "xdm:person": {
        "xdm:birthDate": "2018-01-12",
        "xdm:birthDayAndMonth": "01-23",
        "xdm:birthYear": 6427,
        "xdm:gender": "not_specified",
        "xdm:maritalStatus": "not_specified",
        "xdm:name": {
            "xdm:courtesyTitle": "string",
            "xdm:firstName": "string",
            "xdm:fullName": "string",
            "xdm:lastName": "string",
            "xdm:middleName": "string",
            "xdm:suffix": "string"
        },
        "xdm:nationality": "US",
        "xdm:taxId": "string"
    },
    "xdm:personalEmail": {
        "xdm:address": "john.smith@abc.com",
        "xdm:label": "string",
        "xdm:primary": false,
        "xdm:status": "active",
        "xdm:statusReason": "string",
        "xdm:type": "unknown"
    },
    "xdm:repositoryCreatedBy": "string",
    "xdm:repositoryLastModifiedBy": "string"
}
```
