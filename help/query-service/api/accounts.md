---
keywords: Experience Platform；首頁；熱門主題；查詢服務；api指南；查詢服務；查詢服務；帳戶；
solution: Experience Platform
title: 帳戶API終結點
description: 您可以為永久性建立查詢服務帳戶。
exl-id: 1667f4a5-e6e5-41e9-8f9d-6d2c63c7d7d6
source-git-commit: fcd44aef026c1049ccdfe5896e6199d32b4d1114
workflow-type: tm+mt
source-wordcount: '494'
ht-degree: 4%

---

# 帳戶終結點

在Adobe Experience Platform查詢服務中，帳戶用於建立可與外部SQL客戶端一起使用的非過期憑據。 您可以使用 `/accounts` 查詢服務API中的終結點，允許您按程式建立、檢索、編輯和刪除查詢服務整合帳戶（也稱為技術帳戶）。

## 快速入門

本指南中使用的端點是Query Service API的一部分。 在繼續之前，請查看 [入門指南](./getting-started.md) 要成功調用API，您需要瞭解的重要資訊，包括必需的標頭以及如何讀取示例API調用。

## 建立帳戶

通過向Oracle Query提供POST請求，您可以建立查詢服務整合帳戶 `/accounts` 端點。

**API格式**

```http
POST /accounts
```

**要求**

以下請求將為您的組織建立新的查詢服務整合帳戶。

```shell
curl -X POST https://platform.adobe.io/data/foundation/queryauth/accounts \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'content-type: application/json' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '
{
    "accountName": "sampleName",
    "assignedToUser": "sample@example.com",
    "credential": "samplecredential",
    "description": "Sample description"
}'
```

| 屬性 | 說明 |
| -------- | ----------- |
| `accountName` | **必需** 查詢服務整合帳戶的名稱。 |
| `assignedToUser` | **必需** 將為其建立查詢服務整合帳戶的Adobe ID。 |
| `credential` | *（可選）* 用於查詢服務整合的憑據。 如果未指定，系統將自動為您生成憑據。 |
| `description` | *（可選）* 查詢服務整合帳戶的說明。 |

**回應**

成功的響應返回HTTP狀態200，其中包含新建立的查詢服務整合帳戶的詳細資訊。 您可以使用這些帳戶詳細資訊將查詢服務與外部客戶端連接。

```json
{
    "technicalAccountName": "2428A037-D963-47C2-A14D-CD816EFB0AA3@TECHACCT.ADOBE.COM",
    "technicalAccountId": "E09A0DFB5FDB25D90A494012",
    "credential": "samplecredential"
}
```

| 屬性 | 說明 |
| -------- | ----------- |
| `technicalAccountName` | 查詢服務整合帳戶的名稱。 |
| `technicalAccountId` | 查詢服務整合帳戶的ID。 這個和 `credential`，為您的帳戶編製密碼。 |
| `credential` | 查詢服務整合帳戶的憑據。 這個和 `technicalAccountId`，為您的帳戶編製密碼。 |

## 更新帳戶

您可以通過向查詢服務整合帳戶發出PUT請求來更新 `/accounts` 端點。

**API格式**

```http
POST /accounts/{ACCOUNT_ID}
```

| 參數 | 說明 |
| --------- | ----------- |
| `{ACCOUNT_ID}` | 要更新的查詢服務整合帳戶的ID。 |

**要求**

```shell
curl -X PUT https://platform.adobe.io/data/foundation/queryauth/accounts/E09A0DFB5FDB25D90A494012 \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}' \
 -d '
 {
     "accountName": "Updated account name",
     "assignedToUser": "sampleuser2@adobe.com",
     "credential": "UpdatedCredential",
     "description": "Updated description"
 }'
```

| 屬性 | 說明 |
| -------- | ----------- |
| `accountName` | *（可選）* 查詢服務整合帳戶的更新名稱。 |
| `assignedToUser` | *（可選）* 查詢服務整合帳戶連結到的更新的Adobe ID。 |
| `credential` | *（可選）* 查詢服務帳戶的更新憑據。 |
| `description` | *（可選）* 查詢服務整合帳戶的更新說明。 |

**回應**

成功的響應返回HTTP狀態200，其中包含有關您最近更新的查詢服務整合帳戶的資訊。

```json
{
    "accountName": "Updated account name",
    "assignedToUser": "sampleuser2@adobe.com",
    "created": "2021-06-16T16:44:42.073Z",
    "createdBy": "3BF132EF5BC636C10A49400B@AdobeID",
    "credential": "UpdatedCredential",
    "description": "Updated description",
    "lastUpdated": "2021-08-03T23:47:46.588Z",
    "lastUpdatedBy": "3BF132EF5BC636C10A49400B@AdobeID",
    "technicalAccountName": "2428A037-D963-47C2-A14D-CD816EFB0AA3@TECHACCT.ADOBE.COM",
    "technicalAccountId": "E09A0DFB5FDB25D90A494012"
}
```

## 列出所有帳戶

您可以通過向以下站點發出GET請求來檢索所有查詢服務整合帳戶的清單 `/accounts` 端點。

**API格式**

```http
GET /accounts
```

**要求**

```shell
curl -X GET https://platform.adobe.io/foundation/queryauth/accounts \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**回應**

成功的響應返回HTTP狀態200，其中包含所有查詢服務整合帳戶的清單。

```json
{
    "accounts": [
        {
            "lastUpdated": "2021-06-16T18:07:49.581Z",
            "accountName": "Use for XQL testing of account creation",
            "description": "Local test",
            "assignedToUser": "platform-ui-automation@adobe.com",
            "technicalAccountName": "ADC7EB19-63B4-4B9F-A192-EBE3CD0C034E@TECHACCT.ADOBE.COM",
            "technicalAccountId": "38645A7360CA3DF30A49400F",
            "lastUpdatedBy": "3BF132EF5BC636C10A49400B@AdobeID",
            "createdBy": "3BF132EF5BC636C10A49400B@AdobeID",
            "created": "2021-06-16T18:07:49.581Z",
            "active": true
        },
        {
            "lastUpdated": "2021-06-16T16:44:42.073Z",
            "accountName": "Use for XQL testing of account creation",
            "description": " ",
            "assignedToUser": "platform-ui-automation@adobe.com",
            "technicalAccountName": "66E91FDD-4733-45E2-A312-D87580CFA55D@TECHACCT.ADOBE.COM",
            "technicalAccountId": "392202E060CA2A770A49420A",
            "lastUpdatedBy": "3BF132EF5BC636C10A49400B@AdobeID",
            "createdBy": "3BF132EF5BC636C10A49400B@AdobeID",
            "created": "2021-06-16T16:44:42.073Z",
            "active": true
        }
    ],
    "_page": {
        "count": 2,
        "next": "2021-06-16T16:44:42.073Z",
        "orderby": "-created",
        "property": "active==true",
        "start": "2021-06-16T18:07:49.581Z"
    },
    "_links": {
        "next": {
            "href": "https://platform.adobe.io/data/foundation/queryauth/accounts?orderby=-created&property=active==true&start=2021-06-16T16:44:42.073Z"
        },
        "prev": {
            "href": "https://platform.adobe.io/data/foundation/queryauth/accounts?orderby=-created&property=active==true&start=2021-06-16T18:07:49.581Z&isPrevLink=true"
        }
    },
    "version": 1
}
```

## 刪除帳戶

通過向Oracle Query提供DELETE請求，您可以刪除Query Service整合帳戶 `/accounts` 端點。

**API格式**

```http
DELETE /accounts/{ACCOUNT_ID}
```

| 參數 | 說明 |
| --------- | ----------- |
| `{ACCOUNT_ID}` | 要刪除的查詢服務整合帳戶的ID。 |

**要求**

```shell
curl -X DELETE https://platform.adobe.io/data/foundation/queryauth/accounts/E09A0DFB5FDB25D90A494012 \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**回應**

成功的響應返回HTTP狀態200，並顯示一條消息，指出帳戶已成功刪除。

```json
{
    "result": "Success"
}
```
