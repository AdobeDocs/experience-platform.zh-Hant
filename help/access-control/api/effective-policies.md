---
keywords: Experience Platform;home;popular topics;effective policies;access control api
solution: Experience Platform
title: 檢視有效的原則
topic: developer guide
description: Adobe Experience Platform中的存取控制功能可讓您使用Adobe Admin Console管理各種平台功能的角色和權限。 本檔案是如何使用Adobe Experience Platform的存取控制API來檢視有效政策的指南。
translation-type: tm+mt
source-git-commit: 481f093e52c8533d2919504051af9e63704a0f4a
workflow-type: tm+mt
source-wordcount: '309'
ht-degree: 1%

---


# 檢視有效的原則

若要檢視目前使用者的有效原則，請向API中的端點 `/acl/effective-policies` 提出POST要 [!DNL Access Control] 求。 您要擷取的權限和資源類型必須以陣列的形式提供在請求裝載中。 以下範例API呼叫中說明此點。

**API格式**

```http
POST /acl/effective-policies
```

**請求**

以下請求將檢索有關當前用戶的「[!UICONTROL Manage Datasets]」權限和對「[!UICONTROL Schemas]」資源類型的訪問權限的資訊。

```shell
curl -X POST \
  https://platform.adobe.io/data/foundation/access-control/acl/effective-policies \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '[
    "/permissions/manage-datasets",
    "/resource-types/schemas"
  ]'
```

>[!NOTE]
>
>有關可在裝載陣列中提供的權限和資源類型的完整清單，請參見關於接受的權限和 [資源類型的附錄部分](#accepted-permissions-and-resource-types)。

**回應**

成功的回應會傳回請求中提供之權限和資源類型的相關資訊。 回應包含目前使用者對於請求中指定之資源類型的作用中權限。 如果請求裝載中包含的任何權限對目前使用者有效，API會傳回具有應用程式磁碟(`*`)的權限，以指出該權限有效。 回應裝載中會忽略請求中提供對使用者未作用的任何權限。

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

本檔案說明如何呼叫 [!DNL Access Control] API，以傳回資源類型之作用中權限和相關原則的資訊。 有關訪問控制的詳細信 [!DNL Experience Platform]息，請參 [閱訪問控制概述](../home.md)。

## 附錄

本節提供使用API的補充 [!DNL Access Control] 資訊。

### 接受的權限和資源類型

以下是權限和資源類型的清單，您可以在POST請求到端點的裝載中加入這些權 `/acl/active-permissions` 限。

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
permissions/manage-schema-identities
permissions/manage-schema-relationships
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
