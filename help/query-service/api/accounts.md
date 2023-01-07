---
keywords: Experience Platform；首頁；熱門主題；查詢服務；api指南；查詢服務；查詢服務帳戶；帳戶；
solution: Experience Platform
title: 帳戶API端點
description: 您可以為永久性建立查詢服務帳戶。
exl-id: 1667f4a5-e6e5-41e9-8f9d-6d2c63c7d7d6
source-git-commit: 58eadaaf461ecd9598f3f508fab0c192cf058916
workflow-type: tm+mt
source-wordcount: '495'
ht-degree: 4%

---

# 帳戶端點

在Adobe Experience Platform Query Service中，帳戶用於建立非到期憑證，以便與外部SQL用戶端搭配使用。 您可以使用 `/accounts` 端點，可讓您以程式設計方式建立、擷取、編輯和刪除查詢服務整合帳戶（也稱為技術帳戶）。

## 快速入門

本指南中使用的端點是查詢服務API的一部分。 繼續之前，請檢閱 [快速入門手冊](./getting-started.md) 若要成功對API進行呼叫，您必須知道的重要資訊，包括必要的標題以及如何讀取範例API呼叫。

## 建立帳戶

您可以向 `/accounts` 端點。

**API格式**

```http
POST /accounts
```

**要求**

下列請求會為您的IMS組織建立新的查詢服務整合帳戶。

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
| `accountName` | **必填** 查詢服務整合帳戶的名稱。 |
| `assignedToUser` | **必填** 將為其建立查詢服務整合帳戶的Adobe ID。 |
| `credential` | *（可選）* 用於查詢服務整合的憑據。 如果未指定，系統將自動為您生成憑據。 |
| `description` | *（可選）* 查詢服務整合帳戶的說明。 |

**回應**

成功的回應會傳回HTTP狀態200，並包含新建立之Query Service整合帳戶的詳細資訊。 您可以使用這些帳戶詳細資訊將Query Service與外部用戶端連結。

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
| `technicalAccountId` | 查詢服務整合帳戶的ID。 這個，連同 `credential`，合成您帳戶的密碼。 |
| `credential` | 查詢服務整合帳戶的憑據。 這個，連同 `technicalAccountId`，合成您帳戶的密碼。 |

## 更新帳戶

您可以向 `/accounts` 端點。

**API格式**

```http
POST /accounts/{ACCOUNT_ID}
```

| 參數 | 說明 |
| --------- | ----------- |
| `{ACCOUNT_ID}` | 要更新的查詢服務整合帳戶ID。 |

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
| `assignedToUser` | *（可選）* Query Service整合帳戶所連結的更新Adobe ID。 |
| `credential` | *（可選）* 查詢服務帳戶的更新憑證。 |
| `description` | *（可選）* 查詢服務整合帳戶的更新說明。 |

**回應**

成功的回應會傳回HTTP狀態200，並包含新更新之查詢服務整合帳戶的相關資訊。

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

您可以向 `/accounts` 端點。

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

成功的回應會傳回HTTP狀態200，並包含所有Query Service整合帳戶的清單。

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

您可以透過向 `/accounts` 端點。

**API格式**

```http
DELETE /accounts/{ACCOUNT_ID}
```

| 參數 | 說明 |
| --------- | ----------- |
| `{ACCOUNT_ID}` | 要刪除的查詢服務整合帳戶ID。 |

**要求**

```shell
curl -X DELETE https://platform.adobe.io/data/foundation/queryauth/accounts/E09A0DFB5FDB25D90A494012 \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**回應**

成功的回應會傳回HTTP狀態200，並顯示帳戶已成功刪除的訊息。

```json
{
    "result": "Success"
}
```
