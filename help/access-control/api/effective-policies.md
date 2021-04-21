---
keywords: Experience Platform；首頁；熱門主題；有效策略；訪問控制API
solution: Experience Platform
title: 有效策略API端點
topic-legacy: developer guide
description: Adobe Experience Platform的訪問控制允許您使用Adobe Admin Console來管理各種平台功能的角色和權限。 本檔案是如何使用Adobe Experience Platform的存取控制API來檢視有效政策的指南。
exl-id: 555d73db-115d-4f4c-8bd2-b91477799591
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '317'
ht-degree: 1%

---

# 有效的策略端點

要查看當前用戶的有效策略，請向[!DNL Access Control] API中的`/acl/effective-policies`端點發出POST請求。 您要擷取的權限和資源類型必須以陣列的形式提供在請求裝載中。 以下範例API呼叫中說明此點。

**API格式**

```http
POST /acl/effective-policies
```

**要求**

下列請求會擷取有關目前使用者之「[!UICONTROL Manage Datasets]」權限和「[!UICONTROL schemas]」資源類型存取權的資訊。

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
>有關可以在裝載陣列中提供的權限和資源類型的完整清單，請參見[接受的權限和資源類型](#accepted-permissions-and-resource-types)上的附錄部分。

**回應**

成功的回應會傳回請求中提供之權限和資源類型的相關資訊。 回應包含目前使用者對於請求中指定之資源類型的作用中權限。 如果請求裝載中包含的任何權限對於當前用戶處於活動狀態，則API返回具有應用程式盤(`*`)的權限，以指示該權限處於活動狀態。 回應裝載中會忽略請求中提供對使用者未作用的任何權限。

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

本檔案說明如何呼叫[!DNL Access Control] API，以傳回資源類型之作用中權限和相關原則的資訊。 有關[!DNL Experience Platform]的訪問控制的詳細資訊，請參閱[訪問控制概述](../home.md)。

## 附錄

本節提供使用[!DNL Access Control] API的補充資訊。

### 接受的權限和資源類型

以下是權限和資源類型的清單，您可以在`/acl/active-permissions`端點的POST請求的裝載中包括這些權限和資源類型。

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
