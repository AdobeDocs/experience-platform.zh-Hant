---
keywords: Experience Platform;home;popular topics;Sandbox;sandbox
solution: Experience Platform
title: 建立沙盒
topic: developer guide
description: 您可以向「/沙盒」端點發出POST請求，以建立新沙盒。
translation-type: tm+mt
source-git-commit: c081a7521be9715ca32d35504922a70767924fd7
workflow-type: tm+mt
source-wordcount: '151'
ht-degree: 2%

---


# 建立沙盒

您可以向端點提出POST請求，以建立新沙 `/sandboxes` 盒。

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
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
    "name": "dev-3",
    "title": "Development 3",
    "type": "development"
  }'
```

| 屬性 | 說明 |
| --- | --- |
| `name` | 在未來請求中用來存取沙盒的識別碼。 此值必須是唯一的，最佳實務是盡可能使其具有描述性。 不能包含任何空格或大寫字母。 |
| `title` | 用於平台使用者介面中顯示目的的可人讀名稱。 |
| `type` | 要建立的沙盒類型。 目前，組織只能建立「開發」類型的沙盒。 |

**回應**

成功的回應會傳回新建立沙盒的詳細資訊，顯示其 `state` 是「建立」。

```json
{
    "name": "dev-3",
    "title": "Development 3",
    "state": "creating",
    "type": "development",
    "region": "VA7"
}
```

>[!NOTE]
>
>沙盒需要大約15分鐘的時間才能由系統布建，之後它們 `state` 會變成「活動」或「失敗」。
