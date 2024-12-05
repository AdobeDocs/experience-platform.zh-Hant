---
keywords: Experience Platform；安全性；ip-access；QS-Auth；API指南；查詢服務；IP範圍
title: IP存取端點
description: 瞭解如何使用IP存取API端點在查詢服務中管理沙箱存取的IP範圍。
role: Developer
exl-id: fc15ab50-c125-4f00-a311-81fd41697c7d
source-git-commit: d0f4a295928b000b6091172800e453d79dc44e3a
workflow-type: tm+mt
source-wordcount: '422'
ht-degree: 3%

---

# IP存取端點

>[!AVAILABILITY]
>
>已購買Data Distiller附加元件的客戶可使用此功能。 如需詳細資訊，請聯絡您的 Adobe 代表。

若要保護指定查詢服務沙箱內資料存取的安全，請使用IP存取端點來管理允許的IP範圍。 您可以使用此API來擷取、設定或刪除與組織ID相關聯的IP範圍。

您可以使用IP存取API執行下列動作：

- **擷取所有IP範圍**
- **設定新的IP範圍**
- **刪除現有的IP範圍**

本檔案說明您可以從`/security/ip-access`端點提出和接收的請求和回應。

>[!NOTE]
>
>您必須有使用者權杖才能呼叫此API。 如需取得每個標頭所需值的詳細資訊，請參閱[快速入門手冊](./getting-started.md)。

## 擷取所有IP範圍 {#fetch-all-ip-ranges}

擷取針對您的沙箱設定的所有IP範圍清單。 如果未設定IP範圍，預設會允許所有IP，而且回應會在`allowedIpRanges`中傳回空白清單。

**API格式**

```http
GET /security/ip-access
```

**要求**

```shell
curl -X GET https://platform.adobe.io/data/foundation/queryauth/security/ip-access \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**回應**

成功的回應會傳回HTTP狀態200以及沙箱允許的IP範圍清單。

```json
{
  "imsOrg": "{ORG_ID}",
  "sandboxName": "prod",
  "channel": "data_distiller",
  "allowedIpRanges": [
    {"ipRange": "136.23.110.0/23", "description": "VPN-1 gateway IPs"},
    {"ipRange": "101.10.1.1"}
  ]
}
```

下表提供回應綱要特性的說明和範例：

| 屬性 | 說明 | 範例 |
|------------------|---------------------------------------------|-----------------------------------------------------------------------------------------------|
| `imsOrg` | 沙箱的組織ID。 | `{ORG_ID}` |
| `sandboxName` | 套用IP限制的沙箱名稱。 | `prod` |
| `channel` | IP限制的存取模式。 目前唯一接受的值為`data_distiller`。 此值表示IP限制套用至PSQL或JDBC連線。 | `data_distiller` |
| `allowedIpRanges` | CIDR或固定IP格式的允許IP清單。 每個專案都可以包含選擇性說明。 | `[{"ipRange": "136.23.110.0/23", "description": "VPN-1 gateway IPs"}]` |

>[!NOTE]
>
>`allowedIpRanges`欄位可以包含兩種IP規格：<br><ul><li>**CIDR**：用於定義IP範圍的標準CIDR標籤法（例如`"136.23.110.0/23"`）。</li><li>**固定IP**：個別存取許可權的單一IP （例如，`"101.10.1.1"`）。</li></ul>

## 設定新IP範圍

設定沙箱的新清單來覆寫現有的IP範圍。 此操作需要完整的IP範圍清單，包括任何保持不變的IP範圍。

**API格式**

```http
PUT /security/ip-access
```

**要求**

```shell
curl -X PUT https://platform.adobe.io/data/foundation/queryauth/security/ip-access \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}' \
 -d '{
     "ipRanges": [
       {"ipRange": "136.23.110.0/23", "description": "VPN-1 gateway IPs"},
       {"ipRange": "17.102.17.0/23", "description": "VPN-2 gateway IPs"},
       {"ipRange": "101.10.1.1"},
       {"ipRange": "163.77.30.9", "description": "Test server IP"}
     ]
   }'
```

**回應**

成功的回應會傳回HTTP狀態200以及新設定的IP範圍的詳細資訊。

```json
{
  "imsOrg": "{ORG_ID}",
  "sandboxName": "prod",
  "channel": "data_distiller",
  "allowedIpRanges": [
    {"ipRange": "136.23.110.0/23", "description": "VPN-1 gateway IPs"},
    {"ipRange": "17.102.17.0/23", "description": "VPN-2 gateway IPs"},
    {"ipRange": "101.10.1.1"},
    {"ipRange": "163.77.30.9", "description": "Test server IP"}
  ]
}
```

## 刪除IP範圍 {#delete-ip-ranges}

移除沙箱的所有已設定IP範圍。 此動作會刪除IP範圍並傳回已刪除的IP清單。

>[!NOTE]
>
>刪除操作會套用至組織(`imsOrg`) ID，並影響為沙箱設定的所有IP範圍。

**API格式**

```http
DELETE /security/ip-access
```

**要求**

```shell
curl -X DELETE https://platform.adobe.io/data/foundation/queryauth/security/ip-access \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**回應**

成功的回應會傳回HTTP狀態200以及已刪除之IP範圍的詳細資訊。

```json
{
  "imsOrg": "{ORG_ID}",
  "sandboxName": "prod",
  "channel": "data_distiller",
  "deletedIpRanges": [
    {"ipRange": "136.23.110.0/23", "description": "VPN-1 gateway IPs"},
    {"ipRange": "17.102.17.0/23", "description": "VPN-2 gateway IPs"},
    {"ipRange": "101.10.1.1"},
    {"ipRange": "163.77.30.9", "description": "Test server IP"}
  ]
}
```
