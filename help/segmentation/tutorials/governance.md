---
keywords: Experience Platform；主題；熱門主題；資料使用符合性；強制；強制資料使用符合性；分段服務；分段；分段；
solution: Experience Platform
title: 使用API強制受眾段的資料使用符合性
type: Tutorial
description: 本教程介紹了使用API為Real-Time Customer Profile受眾段強制實施資料使用合規性的步驟。
exl-id: 2299328c-d41a-4fdc-b7ed-72891569eaf2
source-git-commit: 59dfa862388394a68630a7136dee8e8988d0368c
workflow-type: tm+mt
source-wordcount: '1368'
ht-degree: 1%

---

# 使用API強制受眾段的資料使用符合性

本教程介紹了實施資料使用合規性的步驟 [!DNL Real-Time Customer Profile] 使用API的受眾段。

## 快速入門

本教程需要對以下元件進行有效的瞭解 [!DNL Adobe Experience Platform]:

- [[!DNL Real-Time Customer Profile]](../../profile/home.md): [!DNL Real-Time Customer Profile] 是泛型查找實體儲存，用於管理 [!DNL Experience Data Model (XDM)] 資料 [!DNL Platform]。 配置檔案將資料合併到各種企業資料資產中，並以統一的演示文稿提供對該資料的訪問。
   - [合併策略](../../profile/api/merge-policies.md):使用的規則 [!DNL Real-Time Customer Profile] 確定在特定條件下哪些資料可以合併到統一視圖中。 可以為資料治理目的配置合併策略。
- [[!DNL Segmentation]](../home.md):如何 [!DNL Real-Time Customer Profile] 將檔案庫中的一大群個體分成小組，這些小組具有相似的特點，並會對營銷策略做出類似的反應。
- [資料治理](../../data-governance/home.md):Data Governance使用以下元件為資料使用標籤和強制實施提供了基礎架構：
   - [資料使用標籤](../../data-governance/labels/user-guide.md):用於根據處理各自資料的敏感度級別描述資料集和欄位的標籤。
   - [資料使用策略](../../data-governance/policies/overview.md):指示允許對按特定資料使用標籤分類的資料執行哪些市場營銷操作的配置。
   - [策略執行](../../data-governance/enforcement/overview.md):允許您強制實施資料使用策略並防止構成策略違規的資料操作。
- [沙箱](../../sandboxes/home.md): [!DNL Experience Platform] 提供虛擬沙箱，將單個沙箱 [!DNL Platform] 實例到獨立的虛擬環境，以幫助開發和發展數字型驗應用程式。

以下各節提供了您需要瞭解的其他資訊，以便成功呼叫 [!DNL Platform] API。

### 讀取示例API調用

本教程提供了示例API調用，以演示如何格式化請求。 這些包括路徑、必需的標頭和正確格式化的請求負載。 還提供了API響應中返回的示例JSON。 有關示例API調用文檔中使用的約定的資訊，請參見上的 [如何讀取示例API調用](../../landing/troubleshooting.md#how-do-i-format-an-api-request) 的 [!DNL Experience Platform] 疑難解答指南。

### 收集所需標題的值

為了呼叫 [!DNL Platform] API，必須首先完成 [驗證教程](https://www.adobe.com/go/platform-api-authentication-en)。 完成身份驗證教程將提供所有中每個必需標頭的值 [!DNL Experience Platform] API調用，如下所示：

- 授權：持 `{ACCESS_TOKEN}`
- x-api-key: `{API_KEY}`
- x-gw-ims-org-id: `{ORG_ID}`

中的所有資源 [!DNL Experience Platform] 與特定虛擬沙箱隔離。 所有請求 [!DNL Platform] API需要一個標頭，該標頭指定操作將在以下位置進行的沙盒的名稱：

- x-sandbox-name: `{SANDBOX_NAME}`

>[!NOTE]
>
>有關中的沙箱的詳細資訊 [!DNL Platform]，請參見 [沙盒概述文檔](../../sandboxes/home.md)。

包含負載(POST、PUT、PATCH)的所有請求都需要附加的標頭：

- 內容類型：應用程式/json

## 查找段定義的合併策略 {#merge-policy}

此工作流從訪問已知受眾段開始。 在中啟用的段 [!DNL Real-Time Customer Profile] 包含段定義中的合併策略ID。 此合併策略包含有關要包括在段中的資料集的資訊，這些資料集又包含任何適用的資料使用標籤。

使用 [!DNL Segmentation] API，可以按段定義的ID查找段定義以查找其關聯的合併策略。

**API格式**

```http
GET /segment/definitions/{SEGMENT_DEFINITION_ID}
```

| 屬性 | 說明 |
| -------- | ----------- |
| `{SEGMENT_DEFINITION_ID}` | 要查找的段定義的ID。 |

**要求**

```shell
curl -X GET \
  https://platform.adobe.io/data/core/ups/segment/definitions/24379cae-726a-4987-b7b9-79c32cddb5c1 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**回應**

成功的響應返回段定義的詳細資訊。

```json
{
    "id": "24379cae-726a-4987-b7b9-79c32cddb5c1",
    "schema": { 
        "name": "_xdm.context.profile"
    },
    "ttlInDays": 90,
    "imsOrgId": "{ORG_ID}",
    "name": "Cart abandons in CA",
    "description": "",
    "expression": {
        "type": "PQL", 
        "format": "pql/text", 
        "value": "homeAddress.countryISO = 'US'"
    },
    "mergePolicyId": "2b43d78d-0ad4-4c1e-ac2d-574c09b01119",
    "evaluationInfo": {
        "batch": {
            "enabled": true
        },
        "continuous": {
            "enabled": false
        },
        "synchronous": {
            "enabled": false
        }
    },
    "creationTime": 1556094486000,
    "updateEpoch": 1556094486000,
    "updateTime": 1556094486000
  }
}
```

| 屬性 | 說明 |
| -------- | ----------- |
| `mergePolicyId` | 用於段定義的合併策略的ID。 下一步將使用此選項。 |

## 從合併策略查找源資料集 {#datasets}

合併策略包含有關其源資料集的資訊，這些資訊又包含資料使用標籤。 您可以通過將合併策略ID在GET請求中提供給 [!DNL Profile] API。 有關合併策略的詳細資訊，請參閱 [合併策略終結點指南](../../profile/api/merge-policies.md)。

**API格式**

```http
GET /config/mergePolicies/{MERGE_POLICY_ID}
```

| 屬性 | 說明 |
| -------- | ----------- |
| `{MERGE_POLICY_ID}` | 在 [上一步](#merge-policy)。 |

**要求**

```shell
curl -X GET \
  https://platform.adobe.io/data/core/ups/config/mergePolicies/2b43d78d-0ad4-4c1e-ac2d-574c09b01119 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**回應**

成功的響應返回合併策略的詳細資訊。

```json
{
    "id": "2b43d78d-0ad4-4c1e-ac2d-574c09b01119",
    "imsOrgId": "{ORG_ID}",
    "schema": {
        "name": "_xdm.context.profile"
    },
    "version": 1,
    "identityGraph": {
        "type": "none"
    },
    "attributeMerge": {
        "type":"dataSetPrecedence", 
        "data": {
            "order": ["5b95b155419ec801e6eee780", "5b7c86968f7b6501e21ba9df"]
        }
    },
    "default": false,
    "updateEpoch": 1551127597
}
```

| 屬性 | 說明 |
| -------- | ----------- |
| `schema.name` | 與合併策略關聯的架構的名稱。 |
| `attributeMerge.type` | 合併策略的資料優先順序配置類型。 如果值為 `dataSetPrecedence`，與此合併策略關聯的資料集列在 `attributeMerge > data > order`。 如果值為 `timestampOrdered`，則與中引用的架構關聯的所有資料集 `schema.name` 合併策略使用。 |
| `attributeMerge.data.order` | 如果 `attributeMerge.type` 是 `dataSetPrecedence`，此屬性將是包含此合併策略使用的資料集ID的陣列。 這些ID將用於下一步。 |

## 評估資料集中的策略違規

>[!NOTE]
>
> 此步驟假定您至少有一個活動資料使用策略，該策略可阻止對包含特定標籤的資料執行特定的市場營銷操作。 如果您沒有任何適用於正在評估的資料集的使用策略，請遵循 [策略建立教程](../../data-governance/policies/create.md) 建立一個，然後繼續執行此步驟。

獲取合併策略的源資料集的ID後，可以使用 [策略服務API](https://www.adobe.io/experience-platform-apis/references/policy-service/) 根據特定的市場營銷操作評估這些資料集，以檢查資料使用策略違規。

要評估資料集，必須在POST請求路徑中提供市場營銷操作的名稱，同時在請求主體中提供資料集ID，如下例所示。

**API格式**

```http
POST /marketingActions/core/{MARKETING_ACTION_NAME}/constraints
POST /marketingActions/custom/{MARKETING_ACTION_NAME}/constraints
```

| 參數 | 說明 |
| --- | --- |
| `{MARKETING_ACTION_NAME}` | 與要評估資料集的資料使用策略關聯的市場營銷操作的名稱。 根據策略是由Adobe還是您的組織定義，您必須使用 `/marketingActions/core` 或 `/marketingActions/custom`的下界。 |

**要求**

以下請求test `exportToThirdParty` 針對在 [上一步](#datasets)。 請求負載是包含每個資料集的ID的陣列。

```shell
curl -X POST \
  https://platform.adobe.io/data/foundation/dulepolicy/marketingActions/custom/exportToThirdParty/constraints
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '[
    {
      "entityType": "dataSet",
      "entityId": "5b95b155419ec801e6eee780"
    },
    {
      "entityType": "dataSet",
      "entityId": "5b7c86968f7b6501e21ba9df"
    }
  ]'
```

| 屬性 | 說明 |
| --- | --- |
| `entityType` | 負載陣列中的每個項目必須指示要定義的實體類型。 對於此使用情形，值將始終為&quot;dataSet&quot;。 |
| `entityID` | 負載陣列中的每個項必須為資料集提供唯一ID。 |

**回應**

成功的響應返回市場營銷操作的URI、從提供的資料集收集的資料使用情況標籤，以及由於針對這些標籤測試操作而違反的任何資料使用情況策略的清單。 在本示例中，「將資料導出到第三方」策略如 `violatedPolicies` 陣列，指示市場營銷操作觸發了策略違規。

```json
{
  "timestamp": 1556324277895,
  "clientId": "{CLIENT_ID}",
  "userId": "{USER_ID}",
  "imsOrg": "{ORG_ID}",
  "marketingActionRef": "https://platform.adobe.io:443/data/foundation/dulepolicy/marketingActions/custom/exportToThirdParty",
  "duleLabels": [
    "C1",
    "C2",
    "C4",
    "C5"
  ],
  "discoveredLabels": [
    {
      "entityType": "dataSet",
      "entityId": "5b95b155419ec801e6eee780",
      "dataSetLabels": {
        "connection": {
          "labels": []
        },
        "dataSet": {
          "labels": [
            "C5"
          ]
        },
        "fields": [
          {
            "labels": [
              "C2",
            ],
            "path": "/properties/_customer"
          },
          {
            "labels": [
              "C5"
            ],
            "path": "/properties/geoUnit"
          },
          {
            "labels": [
              "C1"
            ],
            "path": "/properties/identityMap"
          }
        ]
      }
    },
    {
      "entityType": "dataSet",
      "entityId": "5b7c86968f7b6501e21ba9df",
      "dataSetLabels": {
        "connection": {
          "labels": []
        },
        "dataSet": {
          "labels": [
            "C5"
          ]
        },
        "fields": [
          {
            "labels": [
              "C5"
            ],
            "path": "/properties/createdByBatchID"
          },
          {
            "labels": [
              "C5"
            ],
            "path": "/properties/faxPhone"
          }
        ]
      }
    }
  ],
  "violatedPolicies": [
    {
      "name": "Export Data to Third Party",
      "status": "ENABLED",
      "marketingActionRefs": [
        "https://platform-stage.adobe.io:443/data/foundation/dulepolicy/marketingActions/custom/exportToThirdParty"
      ],
      "description": "Conditions under which data cannot be exported to a third party",
      "deny": {
        "operator": "OR",
        "operands": [
          {
            "label": "C1"
          },
          {
            "operator": "AND",
            "operands": [
              {
                "label": "C3"
              },
              {
                "label": "C7"
              }
            ]
          }
        ]
      },
      "imsOrg": "{ORG_ID}",
      "created": 1565651746693,
      "createdClient": "{CREATED_CLIENT}",
      "createdUser": "{CREATED_USER",
      "updated": 1565723012139,
      "updatedClient": "{UPDATED_CLIENT}",
      "updatedUser": "{UPDATED_USER}",
      "_links": {
        "self": {
          "href": "https://platform-stage.adobe.io/data/foundation/dulepolicy/policies/custom/5d51f322e553c814e67af1a3"
        }
      },
      "id": "5d51f322e553c814e67af1a3"
    }
  ]
}
```

| 屬性 | 說明 |
| --- | --- |
| `duleLabels` | 從所提供的資料集中提取的資料使用標籤的清單。 |
| `discoveredLabels` | 請求負載中提供的資料集清單，其中顯示了在每個負載中找到的資料集級別和欄位級別標籤。 |
| `violatedPolicies` | 列出測試市場營銷操作（在中指定）所違反的任何資料使用策略的陣列 `marketingActionRef`) `duleLabels`。 |

使用API響應中返回的資料，您可以在體驗應用程式內設定協定，以在發生策略違規時適當強制執行策略違規。

## 篩選資料欄位

如果您的受眾部分未通過評估，則可以通過下面概述的兩種方法之一調整該部分中包含的資料。

### 更新段定義的合併策略

更新段定義的合併策略將調整運行段作業時將包括的資料集和欄位。 請參閱 [更新現有合併策略](../../profile/api/merge-policies.md#update) 的子版本。

### 導出段時限制特定資料欄位

使用 [!DNL Segmentation] API，您可以使用 `fields` 的下界。 添加到此參數的任何資料欄位都將包括在導出中，而所有其他資料欄位將被排除。

請考慮具有名為「A」、「B」和「C」的資料欄位的段。 如果只希望導出欄位&quot;C&quot;，則 `fields` 參數將僅包含欄位「C」。 這樣，在導出段時將排除欄位&quot;A&quot;和&quot;B&quot;。

請參閱 [導出段](./evaluate-a-segment.md#export) 的子菜單。

## 後續步驟

通過學完本教程，您查找了與受眾段關聯的資料使用標籤，並針對特定的市場營銷操作測試了它們是否違反了策略。 有關中的資料治理的詳細資訊 [!DNL Experience Platform]，請閱讀概述 [資料治理](../../data-governance/home.md)。
