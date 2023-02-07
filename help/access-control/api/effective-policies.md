---
keywords: Experience Platform；首頁；熱門主題；有效原則；存取控制api
solution: Experience Platform
title: 有效策略API端點
description: 了解如何使用Adobe Experience Platform的存取控制API檢視有效的存取原則。
exl-id: 555d73db-115d-4f4c-8bd2-b91477799591
source-git-commit: 16d85a2a4ee8967fc701a3fe631c9daaba9c9d70
workflow-type: tm+mt
source-wordcount: '318'
ht-degree: 1%

---

# 有效策略終點

>[!NOTE]
>
>如果傳遞了使用者Token，則Token的使用者必須對請求的組織具有「組織管理員」角色。

要查看當前用戶的有效訪問控制策略，請向以下用戶發出POST請求： `/acl/effective-policies` 端點 [!DNL Access Control] API。 您要擷取的權限和資源類型必須以陣列的形式提供於要求裝載中。 以下範例API呼叫中已示範此問題。

**API格式**

```http
POST /acl/effective-policies
```

**要求**

下列請求會擷取「[!UICONTROL 管理資料集]&quot;權限和對&quot;[!UICONTROL 綱要]&quot;當前用戶的資源類型。

```shell
curl -X POST \
  https://platform.adobe.io/data/foundation/access-control/acl/effective-policies \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '[
    "/permissions/manage-datasets",
    "/resource-types/schemas"
  ]'
```

>[!NOTE]
>
>如需可在裝載陣列中提供的權限和資源類型的完整清單，請參閱 [接受的權限和資源類型](#accepted-permissions-and-resource-types).

**回應**

成功的回應會傳回要求中提供之權限和資源類型的相關資訊。 回應包含目前使用者對請求中指定的資源類型具有的作用中權限。 如果要求裝載中包含的任何權限對目前使用者有效，API會傳回具有特徵的權限(`*`)以指出權限處於作用中狀態。 回應裝載中會忽略要求中提供且對使用者非作用中的任何權限。

```json
{
    "policies": {
        "/resource-types/schemas": [
            "read",
            "write",
            "delete"
        ],
        "/permissions/manage-datasets": [
            "*"
        ]
    }
}
```

## 後續步驟

本檔案說明如何呼叫 [!DNL Access Control] API，可傳回資源類型之作用中權限和相關存取原則的資訊。 如需的存取控制的詳細資訊 [!DNL Experience Platform]，請參閱 [存取控制概觀](../home.md).

## 附錄

本節提供使用 [!DNL Access Control] API。

### 接受的權限和資源類型

以下是權限和資源類型的清單，您可以包含在POST要求對 `/acl/active-permissions` 端點。

**權限**

```plaintext
permissions/activate-destinations
permissions/evaluate-segments
permissions/execute-decisioning-activities
permissions/export-audience-for-segment
permissions/manage-datasets
permissions/manage-decisioning-activities
permissions/manage-decisioning-options
permissions/manage-destinations
permissions/manage-dsw
permissions/manage-dule-labels
permissions/manage-dule-policies
permissions/manage-identity-namespaces
permissions/manage-privacy-workflows
permissions/manage-profile-configs
permissions/manage-profiles
permissions/manage-queries
permissions/manage-schemas
permissions/manage-segments
permissions/manage-sources
permissions/reset-sandboxes
permissions/view-datasets
permissions/view-destinations
permissions/view-dule-labels
permissions/view-dule-policies
permissions/view-identity-namespaces
permissions/view-monitoring-dashboard
permissions/view-privacy-workflows
permissions/view-profile-configs
permissions/view-profiles
permissions/view-sandboxes
permissions/view-schemas
permissions/view-segments
permissions/view-sources
```

**資源類型**

```plaintext
resource-types/activation-associations
resource-types/activations
resource-types/activities
resource-types/analytics-source
resource-types/audience-manager-source
resource-types/bizible-source
resource-types/connection
resource-types/customer-attributes-source
resource-types/data-science-workspace
resource-types/dataset-preview
resource-types/datasets
resource-types/dule-label
resource-types/dule-policy
resource-types/enterprise-source
resource-types/identity-descriptor
resource-types/identity-namespaces
resource-types/launch-source
resource-types/marketing-action
resource-types/marketo-source
resource-types/monitoring
resource-types/offers
resource-types/placements
resource-types/privacy-consent
resource-types/privacy-content-delivery
resource-types/privacy-job
resource-types/profile-configs
resource-types/profile-datasets
resource-types/profiles
resource-types/query
resource-types/relationship-descriptor
resource-types/sandboxes
resource-types/schemas
resource-types/segment-jobs
resource-types/segments
resource-types/streaming-source
```
