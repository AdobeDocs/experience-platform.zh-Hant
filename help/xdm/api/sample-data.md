---
keywords: Experience Platform；主題；熱門主題；api;API;XDM;XDM系統；經驗資料模型；經驗資料模型；資料模型；資料模型；示例資料；rpc;
solution: Experience Platform
title: 示例資料API終結點
description: 通過架構註冊表API中的/sampledata終結點，可以生成映射到任何現有XDM架構結構的示例資料。
topic-legacy: developer guide
exl-id: 424d33ca-0624-4891-bf83-044ac2861579
source-git-commit: 47a94b00e141b24203b01dc93834aee13aa6113c
workflow-type: tm+mt
source-wordcount: '318'
ht-degree: 2%

---

# 示例資料終結點

為了將資料導入Adobe Experience Platform，資料的格式和結構必須符合現有的經驗資料模型(XDM)架構。 根據特定資料集的模式的複雜性，很難確定資料集在攝取時期望的資料的確切形狀。

使用 `/sampledata` 端點 [!DNL Schema Registry] API，可以為任何先前建立的架構生成一個示例接收對象。

## 快速入門

本指南中使用的端點是 [[!DNL Schema Registry] API](https://www.adobe.io/experience-platform-apis/references/schema-registry/)。 在繼續之前，請查看 [入門指南](./getting-started.md) 有關相關文檔的連結、閱讀本文檔中示例API調用的指南，以及有關成功調用任何Experience PlatformAPI所需標頭的重要資訊。

示例資料終結點是遠程過程調用(RPC)的一部分，該調用由 [!DNL Schema Registry]。 不同於 [!DNL Schema Registry] API、RPC終結點不需要像 `Accept` 或 `Content-Type`，並且不使用 `CONTAINER_ID`。 相反，他們必須使用 `/rpc` 命名空間，如下面的API調用所示。

## 檢索架構的示例資料

通過在指向終結點的GET請求路徑中指定架構的ID，可以檢索架構庫中任何架構的示例資料。

**API格式**

```http
GET /rpc/sampledata/{SCHEMA_ID}
```

| 參數 | 說明 |
| --- | --- |
| `{SCHEMA_ID}` | 的 `meta:altId` 或URL編碼 `$id` 要為其生成示例資料的架構。 |

{style=&quot;table-layout:auto&quot;}

**要求**

以下請求為會員成員方案生成示例資料。

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/schemaregistry/rpc/sampledata/_{TENANT_ID}.schemas.533ca5da28087c44344810891b0f03d9 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**回應**

成功的響應返回指定架構的示例資料對象。

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
