---
keywords: Experience Platform；首頁；熱門主題；清單沙箱
solution: Experience Platform
title: 沙盒類型API終結點
description: 通過向/sandboxTypes終結點發出GET請求，可以檢索組織支援的沙盒類型清單。
exl-id: eb5e1b44-37f5-4ed5-98f5-ac8db8792c7d
source-git-commit: 59dfa862388394a68630a7136dee8e8988d0368c
workflow-type: tm+mt
source-wordcount: '162'
ht-degree: 2%

---

# 沙盒類型終結點

您可以通過向以下站點發出GET請求來檢索組織支援的沙盒類型清單 `/sandboxTypes` 端點。

## 快速入門

本指南中使用的API終結點是 [[!DNL Sandbox] API](https://www.adobe.io/experience-platform-apis/references/sandbox)。 在繼續之前，請查看 [入門指南](./getting-started.md) 有關相關文檔的連結、閱讀本文檔中示例API調用的指南，以及有關成功調用任何Experience PlatformAPI所需標頭的重要資訊。

## 檢索支援的沙盒類型清單

您可以通過向以下站點發出GET請求來檢索組織支援的沙盒類型清單 `/sandboxTypes` 端點。

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
  -H 'x-gw-ims-org-id: {ORG_ID}' \
```

**回應**

成功的響應將返回您的組織支援的沙盒類型清單。

```json
{
    "sandboxTypes": [
        "production",
        "development"
    ]
}
```
