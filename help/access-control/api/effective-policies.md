---
keywords: Experience Platform；首頁；熱門主題；有效策略；訪問控制API
solution: Experience Platform
title: 有效策略API終結點
topic-legacy: developer guide
description: Adobe Experience Platform的訪問控制允許您使用Adobe Admin Console管理各種平台功能的角色和權限。 本文檔是有關如何使用Adobe Experience Platform的訪問控制API查看有效策略的指南。
exl-id: 555d73db-115d-4f4c-8bd2-b91477799591
source-git-commit: 47a94b00e141b24203b01dc93834aee13aa6113c
workflow-type: tm+mt
source-wordcount: '320'
ht-degree: 1%

---

# 有效策略終結點

要查看當前用戶的有效策略，請向 `/acl/effective-policies` 端點 [!DNL Access Control] API。 您要檢索的權限和資源類型必須以陣列的形式提供在請求負載中。 這在下面的示例API調用中演示。

**API格式**

```http
POST /acl/effective-policies
```

**要求**

以下請求檢索有關「 」的資訊[!UICONTROL 管理資料集]&quot;權限和對&quot;的訪問[!UICONTROL 模式]&quot;當前用戶的資源類型。

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
>有關可以在負載陣列中提供的權限和資源類型的完整清單，請參見上的附錄部分 [接受的權限和資源類型](#accepted-permissions-and-resource-types)。

**回應**

成功的響應返回有關請求中提供的權限和資源類型的資訊。 響應包括當前用戶對請求中指定的資源類型具有的活動權限。 如果請求負載中包含的任何權限對當前用戶處於活動狀態，則API將返回帶有一個空間磁碟(`*`)以指示權限處於活動狀態。 請求中提供的對用戶無效的任何權限都會從響應負載中省略。

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

本文檔介紹了如何致電 [!DNL Access Control] API，返回有關資源類型的活動權限和相關策略的資訊。 有關訪問控制的詳細資訊 [!DNL Experience Platform]，請參見 [訪問控制概述](../home.md)。

## 附錄

本節提供了使用 [!DNL Access Control] API。

### 接受的權限和資源類型

以下是權限和資源類型的清單，您可以在POST請求的負載中包括到 `/acl/active-permissions` 端點。

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
