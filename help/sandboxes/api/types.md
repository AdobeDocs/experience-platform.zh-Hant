---
keywords: Experience Platform；首頁；熱門主題；清單沙箱
solution: Experience Platform
title: 沙箱類型API端點
topic-legacy: developer guide
description: 您可以向/sandboxTypes端點提出GET要求，以擷取組織的支援沙箱類型清單。
exl-id: eb5e1b44-37f5-4ed5-98f5-ac8db8792c7d
source-git-commit: e644fe9a2faf8692617f6bbee2b91a52c323ff5d
workflow-type: tm+mt
source-wordcount: '166'
ht-degree: 2%

---

# 沙箱類型端點

您可以向`/sandboxTypes`端點提出GET請求，以擷取組織的支援沙箱類型清單。

## 快速入門

本指南中使用的API端點是[[!DNL Sandbox] API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/sandbox-api.yaml)的一部分。 繼續之前，請檢閱[快速入門手冊](./getting-started.md)，取得相關檔案的連結、閱讀本檔案中範例API呼叫的指南，以及成功呼叫任何Experience PlatformAPI所需的必要標頭的重要資訊。

## 擷取支援的沙箱類型清單

您可以向`/sandboxTypes`端點提出GET請求，以擷取組織的支援沙箱類型清單。

**API格式**

```http
GET /sandboxTypes
```

**要求**

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/sandbox-management/sandboxTypes \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
```

**回應**

成功的回應會傳回貴組織支援的沙箱類型清單。

```json
{
    "sandboxTypes": [
        "production",
        "development"
    ]
}
```
