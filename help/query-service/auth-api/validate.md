---
keywords: Experience Platform；安全性； ip存取；驗證； API指南；查詢服務； IP驗證
title: IP驗證端點
description: 瞭解如何使用IP驗證API端點來驗證查詢服務中沙箱的IP存取權。
role: Developer
exl-id: 4ce9ab1c-e333-4ed5-a430-43ffec36a46d
source-git-commit: bf696c8836407a2fea82e9078201cb1f5004bcf8
workflow-type: tm+mt
source-wordcount: '229'
ht-degree: 3%

---

# IP驗證端點

>[!AVAILABILITY]
>
>已購買Data Distiller附加元件的客戶可使用此功能。 如需詳細資訊，請聯絡您的 Adobe 代表。

使用IP驗證API端點來驗證是否允許指定的IP位址存取查詢服務中的指定沙箱。 此檢查會確認存取限制是否適用，或IP位址是否允許存取沙箱中的資料。

## 驗證IP以存取沙箱 {#validate-ip-for-sandbox-access}

使用IP驗證端點來檢查指定IP位址是否允許存取指定沙箱的資料。 如果沙箱未設定IP限制，則預設會允許所有IP位址。 如果存在IP或CIDR限制，此API會驗證指定的IP位址是否符合任何設定的範圍。

>[!NOTE]
>
>您可以使用&#x200B;**使用者權杖**&#x200B;或&#x200B;**服務權杖**&#x200B;來存取此端點。 不需要特定的角色需求。

**API格式**

```http
POST /security/validate/ip-access
```

**要求**

```shell
curl -X POST https://platform.adobe.io/data/foundation/query/security/validate/ip-access \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}' \
 -d '{
       "ipAddress": "197.2.0.2"
     }'
```

**回應**

成功的回應會傳回HTTP狀態200，並布林值指出是否允許IP。

>[!NOTE]
>
>如果允許提供的IP存取沙箱，回應中的`isAllowed`欄位會傳回`true`，否則會傳回`false`。 此API支援動態驗證存取並確保沙箱環境符合安全性規範。

```json
{
"isAllowed": true
}
```
