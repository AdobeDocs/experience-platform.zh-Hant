---
keywords: Experience Platform;home；熱門主題；沙盒；沙盒
solution: Experience Platform
title: 在API中建立沙盒
topic: 開發人員指南
description: 您可以向「/沙盒」端點提出POST請求，以建立新沙盒。
translation-type: tm+mt
source-git-commit: ee2fb54ba59f22a1ace56a6afd78277baba5271e
workflow-type: tm+mt
source-wordcount: '306'
ht-degree: 2%

---


# 在API中建立沙盒

您可以向`/sandboxes`端點提出POST請求，以建立開發或生產沙盒。

## 建立開發沙盒

若要建立開發沙盒，請向`/sandboxes`端點提出POST要求，並為`type`屬性提供`development`值。

**API格式**

```http
POST /sandboxes
```

**請求**

下列請求會建立名為&quot;dev-3&quot;的新開發沙盒。

```shell
curl -X POST \
  https://platform.adobe.io/data/foundation/sandbox-management/sandboxes \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'Content-Type: application/json' \
  -d '{
    "name": "dev-3",
    "title": "Development 3",
    "type": "development"
  }'
```

| 屬性 | 說明 |
| --- | --- |
| `name` | 在未來請求中用來存取沙盒的識別碼。 此值必須是唯一的，最佳實務是盡可能使其具有描述性。 此值不能包含任何空格或特殊字元。 |
| `title` | 用於平台使用者介面中顯示目的的可人讀名稱。 |
| `type` | 要建立的沙盒類型。 `type`屬性的值可以是開發或生產。 |

**回應**

成功的回應會傳回新建立沙盒的詳細資料，顯示其`state`是「建立」。

```json
{
    "name": "dev-3",
    "title": "Development 3",
    "state": "creating",
    "type": "development",
    "region": "VA7"
}
```

## 建立生產沙盒

>[!NOTE]
>
>「多重製作沙盒」功能是beta版。

若要建立生產沙盒，請向`/sandboxes`端點提出POST請求，並為`type`屬性提供`production`值。

**API格式**

```http
POST /sandboxes
```

**請求**

下列請求會建立名為&quot;test-prod-sandbox&quot;的新生產沙盒。

```shell
curl -X POST \
  https://platform.adobe.io/data/foundation/sandbox-management/sandboxes \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'Content-Type: application/json' \
  -d '{
    "name": "test-prod-sandbox",
    "title": "Test Production Sandbox",
    "type": "production"
}'
```

| 屬性 | 說明 |
| --- | --- |
| `name` | 在未來請求中用來存取沙盒的識別碼。 此值必須是唯一的，最佳實務是盡可能使其具有描述性。 此值不能包含任何空格或特殊字元。 |
| `title` | 用於平台使用者介面中顯示目的的可人讀名稱。 |
| `type` | 要建立的沙盒類型。 `type`屬性的值可以是開發或生產。 |

**回應**

成功的回應會傳回新建立沙盒的詳細資料，顯示其`state`是「建立」。

```json
{
    "name": "test-production-sandbox",
    "title": "Test Production Sandbox",
    "state": "creating",
    "type": "production",
    "region": "VA7"
}
```
