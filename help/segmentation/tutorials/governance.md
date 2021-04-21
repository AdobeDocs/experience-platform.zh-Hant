---
keywords: Experience Platform; home；熱門主題；資料使用合規性；強制；強制資料使用合規性；分段服務；分段；分段；
solution: Experience Platform
title: 使用API強制對象區段的資料使用符合性
topic-legacy: tutorial
type: Tutorial
description: 本教學課程涵蓋使用API強制「即時客戶個人檔案」受眾細分資料使用合規性的步驟。
exl-id: 2299328c-d41a-4fdc-b7ed-72891569eaf2
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '1362'
ht-degree: 1%

---

# 使用API強制觀眾區隔的資料使用符合性

本教學課程涵蓋使用API強制[!DNL Real-time Customer Profile]觀眾區段資料使用符合性的步驟。

## 快速入門

本教學課程需要對[!DNL Adobe Experience Platform]的下列元件有正確的理解：

- [[!DNL Real-time Customer Profile]](../../profile/home.md): [!DNL Real-time Customer Profile] 是一般查閱實體儲存區，用於管理內 [!DNL Experience Data Model (XDM)] 的資料 [!DNL Platform]。描述檔會合併各種企業資料資產的資料，並以統一的簡報來存取該資料。
   - [合併策略](../../profile/api/merge-policies.md):用於確定 [!DNL Real-time Customer Profile] 哪些資料可以在特定條件下合併到統一視圖中的規則。可以為[!DNL Data Governance]目的配置合併策略。
- [[!DNL Segmentation]](../home.md):如 [!DNL Real-time Customer Profile] 何將描述檔商店中的龐大個人群組分割為具有類似特性且回應類似行銷策略的較小群組。
- [[!DNL Data Governance]](../../data-governance/home.md): [!DNL Data Governance] 使用以下元件為資料使用標籤和強制實施提供基礎架構：
   - [資料使用標籤](../../data-governance/labels/user-guide.md):標籤用來描述資料集和欄位，以處理其個別資料的敏感度等級為準。
   - [資料使用原則](../../data-governance/policies/overview.md):指示允許針對依特定資料使用標籤分類之資料執行哪些行銷動作的設定。
   - [政策實施](../../data-governance/enforcement/overview.md):允許您強制實施資料使用策略並防止構成違反策略的資料操作。
- [沙盒](../../sandboxes/home.md): [!DNL Experience Platform] 提供虛擬沙盒，可將單一執行個體分 [!DNL Platform] 割為不同的虛擬環境，以協助開發和發展數位體驗應用程式。

以下各節提供您必須知道的其他資訊，才能成功呼叫[!DNL Platform] API。

### 讀取範例API呼叫

本教學課程提供範例API呼叫，以示範如何設定請求的格式。 這些包括路徑、必要標題和正確格式化的請求負載。 也提供API回應中傳回的範例JSON。 如需範例API呼叫檔案中所用慣例的詳細資訊，請參閱[!DNL Experience Platform]疑難排解指南中[如何讀取範例API呼叫](../../landing/troubleshooting.md#how-do-i-format-an-api-request)一節。

### 收集必要標題的值

若要呼叫[!DNL Platform] API，您必須先完成[驗證教學課程](https://www.adobe.com/go/platform-api-authentication-en)。 完成驗證教學課程後，所有[!DNL Experience Platform] API呼叫中每個所需標題的值都會顯示在下面：

- 授權：載體`{ACCESS_TOKEN}`
- x-api-key:`{API_KEY}`
- x-gw-ims-org-id:`{IMS_ORG}`

[!DNL Experience Platform]中的所有資源都隔離到特定的虛擬沙盒。 對[!DNL Platform] API的所有請求都需要一個標題，該標題指定要在中執行操作的沙盒的名稱：

- x-sandbox-name:`{SANDBOX_NAME}`

>[!NOTE]
>
>如需[!DNL Platform]中沙盒的詳細資訊，請參閱[沙盒概述檔案](../../sandboxes/home.md)。

所有包含裝載(POST、PUT、PATCH)的請求都需要額外的標題：

- 內容類型：application/json

## 查找段定義{#merge-policy}的合併策略

此工作流程從存取已知觀眾區隔開始。 在[!DNL Real-time Customer Profile]中啟用的區段在其區段定義中包含合併原則ID。 此合併策略包含有關哪些資料集要包含在段中的資訊，這些資料集又包含任何適用的資料使用標籤。

使用[!DNL Segmentation] API，您可以依其ID來尋找區段定義，以尋找其相關的合併原則。

**API格式**

```http
GET /segment/definitions/{SEGMENT_DEFINITION_ID}
```

| 屬性 | 說明 |
| -------- | ----------- |
| `{SEGMENT_DEFINITION_ID}` | 您要尋找的區段定義ID。 |

**要求**

```shell
curl -X GET \
  https://platform.adobe.io/data/core/ups/segment/definitions/24379cae-726a-4987-b7b9-79c32cddb5c1 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**回應**

成功的回應會傳回區段定義的詳細資料。

```json
{
    "id": "24379cae-726a-4987-b7b9-79c32cddb5c1",
    "schema": { 
        "name": "_xdm.context.profile"
    },
    "ttlInDays": 90,
    "imsOrgId": "{IMS_ORG}",
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
| `mergePolicyId` | 用於區段定義的合併原則ID。 這將用於下一步。 |

## 從合併策略{#datasets}中查找源資料集

合併策略包含有關其源資料集的資訊，而源資料集又包含資料使用標籤。 您可以在[!DNL Profile] API的GET請求中提供合併原則ID，以查閱合併原則的詳細資訊。 有關合併策略的詳細資訊，請參閱[合併策略端點指南](../../profile/api/merge-policies.md)。

**API格式**

```http
GET /config/mergePolicies/{MERGE_POLICY_ID}
```

| 屬性 | 說明 |
| -------- | ----------- |
| `{MERGE_POLICY_ID}` | 在上一步[中獲得的合併策略的ID。](#merge-policy) |

**要求**

```shell
curl -X GET \
  https://platform.adobe.io/data/core/ups/config/mergePolicies/2b43d78d-0ad4-4c1e-ac2d-574c09b01119 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**回應**

成功的回應會傳回合併原則的詳細資訊。

```json
{
    "id": "2b43d78d-0ad4-4c1e-ac2d-574c09b01119",
    "imsOrgId": "{IMS_ORG}",
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
            "order" : ["5b95b155419ec801e6eee780", "5b7c86968f7b6501e21ba9df"]
        }
    },
    "default": false,
    "updateEpoch": 1551127597
}
```

| 屬性 | 說明 |
| -------- | ----------- |
| `schema.name` | 與合併策略關聯的架構的名稱。 |
| `attributeMerge.type` | 合併策略的資料優先順序配置類型。 如果值為`dataSetPrecedence`，則與此合併策略關聯的資料集列在`attributeMerge > data > order`下。 如果值為`timestampOrdered`，則合併策略將使用與`schema.name`中引用的模式關聯的所有資料集。 |
| `attributeMerge.data.order` | 如果`attributeMerge.type`是`dataSetPrecedence`，則此屬性將是包含此合併策略所使用資料集的ID的陣列。 這些ID會用於下一步驟。 |

## 評估資料集中的策略違規情況

>[!NOTE]
>
> 此步驟假設您至少有一個作用中的資料使用原則，可防止對包含特定標籤的資料執行特定行銷動作。 如果您沒有任何適用於評估資料集的使用策略，請遵循[策略建立教程](../../data-governance/policies/create.md)建立策略，然後繼續此步驟。

在您取得合併原則來源資料集的ID後，就可使用[原則服務API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/dule-policy-service.yaml)來評估這些資料集與特定行銷動作對應，以檢查資料使用原則違規情況。

若要評估資料集，您必須在POST請求的路徑中提供行銷動作的名稱，同時在請求內文中提供資料集ID，如下例所示。

**API格式**

```http
POST /marketingActions/core/{MARKETING_ACTION_NAME}/constraints
POST /marketingActions/custom/{MARKETING_ACTION_NAME}/constraints
```

| 參數 | 說明 |
| --- | --- |
| `{MARKETING_ACTION_NAME}` | 與您評估資料集依據的資料使用策略相關聯的行銷動作名稱。 根據策略是由Adobe還是由您的組織定義，您必須分別使用`/marketingActions/core`或`/marketingActions/custom`。 |

**要求**

下列請求會針對在上一步[中取得的資料集測試`exportToThirdParty`行銷動作。 ](#datasets)請求裝載是包含每個資料集ID的陣列。

```shell
curl -X POST \
  https://platform.adobe.io/data/foundation/dulepolicy/marketingActions/custom/exportToThirdParty/constraints
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
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
| `entityType` | 裝載陣列中的每個項目都必須指示要定義的實體類型。 在此使用案例中，值一律為&quot;dataSet&quot;。 |
| `entityID` | 裝載陣列中的每個項目都必須提供資料集的唯一ID。 |

**回應**

成功的回應會傳回行銷動作的URI、從提供的資料集收集的資料使用標籤，以及因測試這些標籤的動作而違反的任何資料使用原則清單。 在此範例中，`violatedPolicies`陣列中顯示「將資料匯出至第三方」原則，指出行銷動作觸發了原則違規。

```json
{
  "timestamp": 1556324277895,
  "clientId": "{CLIENT_ID}",
  "userId": "{USER_ID}",
  "imsOrg": "{IMS_ORG}",
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
      "imsOrg": "{IMS_ORG}",
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
| `duleLabels` | 從提供的資料集中提取的資料使用標籤清單。 |
| `discoveredLabels` | 請求裝載中提供的資料集清單，顯示每個資料集層級和欄位層級標籤。 |
| `violatedPolicies` | 列出任何違反資料使用原則的陣列，這些原則是根據提供的`duleLabels`測試行銷動作（在`marketingActionRef`中指定）。 |

使用API回應中傳回的資料，您可以在體驗應用程式中設定通訊協定，以便在發生違反原則的情況時適當強制執行。

## 篩選資料欄位

如果您的受眾細分未通過評估，您可以透過下列其中一種方法調整該細分中的資料。

### 更新區段定義的合併原則

更新區段定義的合併原則將會調整執行區段工作時將包含的資料集和欄位。 如需詳細資訊，請參閱API合併原則教學課程中有關更新現有合併原則的[一節。](../../profile/api/merge-policies.md#update)

### 匯出區段時限制特定資料欄位

使用[!DNL Segmentation] API將區段匯出至資料集時，您可以使用`fields`參數來篩選匯出中包含的資料。 新增至此參數的任何資料欄位都會包含在匯出中，而所有其他資料欄位則會被排除。

請考慮具有名為&quot;A&quot;、&quot;B&quot;和&quot;C&quot;的資料欄位的區段。 如果您只想匯出欄位&quot;C&quot;，則`fields`參數將僅包含欄位&quot;C&quot;。 執行此動作後，匯出區段時會排除欄位&quot;A&quot;和&quot;B&quot;。

如需詳細資訊，請參閱區段教學課程中有關匯出區段[的章節。](./evaluate-a-segment.md#export)

## 後續步驟

透過本教學課程，您已查找與觀眾區隔相關的資料使用標籤，並測試它們是否違反特定行銷動作的政策。 有關[!DNL Experience Platform]中[!DNL Data Governance]的更多資訊，請閱讀[[!DNL Data Governance]](../../data-governance/home.md)的概述。
