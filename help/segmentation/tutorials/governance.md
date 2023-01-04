---
keywords: Experience Platform；首頁；熱門主題；資料使用符合性；強制；資料使用符合性；分段服務；分段；分段；
solution: Experience Platform
title: 使用API對受眾區段強制執行資料使用量法規遵循
topic-legacy: tutorial
type: Tutorial
description: 本教學課程涵蓋使用API強制執行即時客戶設定檔受眾區段資料使用合規性的步驟。
exl-id: 2299328c-d41a-4fdc-b7ed-72891569eaf2
source-git-commit: 34e0381d40f884cd92157d08385d889b1739845f
workflow-type: tm+mt
source-wordcount: '1368'
ht-degree: 1%

---

# 使用API對受眾區段強制執行資料使用法規遵循

本教學課程涵蓋強制遵循 [!DNL Real-Time Customer Profile] 使用API的受眾區段。

## 快速入門

本教學課程需要妥善了解以下元件： [!DNL Adobe Experience Platform]:

- [[!DNL Real-Time Customer Profile]](../../profile/home.md): [!DNL Real-Time Customer Profile] 是一般查詢實體存放區，用於管理 [!DNL Experience Data Model (XDM)] 資料內 [!DNL Platform]. 設定檔會合併各種企業資料資產的資料，並以統一的簡報方式提供對該資料的存取。
   - [合併策略](../../profile/api/merge-policies.md):使用的規則 [!DNL Real-Time Customer Profile] 以決定在特定條件下可合併至統一檢視的資料。 可針對資料控管目的設定合併原則。
- [[!DNL Segmentation]](../home.md):如何 [!DNL Real-Time Customer Profile] 將設定檔存放區中包含的大量個人群組劃分為具有類似特徵且會回應類似行銷策略的較小群組。
- [資料控管](../../data-governance/home.md):資料控管使用下列元件，提供資料使用標籤和強制實作的基礎架構：
   - [資料使用量標籤](../../data-governance/labels/user-guide.md):以處理個別資料的敏感程度來說明資料集和欄位的標籤。
   - [資料使用原則](../../data-governance/policies/overview.md):指出可對依特定資料使用標籤分類的資料執行哪些行銷動作的設定。
   - [政策執行](../../data-governance/enforcement/overview.md):允許您強制實施資料使用策略並防止構成策略違規的資料操作。
- [沙箱](../../sandboxes/home.md): [!DNL Experience Platform] 提供可分割單一沙箱的虛擬沙箱 [!DNL Platform] 例項放入個別的虛擬環境，以協助開發及改進數位體驗應用程式。

以下小節提供您需要知道的其他資訊，以便成功呼叫 [!DNL Platform] API。

### 讀取範例API呼叫

本教學課程提供範例API呼叫，以示範如何設定要求格式。 這些功能包括路徑、必要標題和格式正確的請求裝載。 也提供API回應中傳回的範例JSON。 如需範例API呼叫檔案中所使用慣例的相關資訊，請參閱 [如何閱讀API呼叫範例](../../landing/troubleshooting.md#how-do-i-format-an-api-request) 在 [!DNL Experience Platform] 疑難排解指南。

### 收集必要標題的值

若要對 [!DNL Platform] API，您必須先完成 [驗證教學課程](https://www.adobe.com/go/platform-api-authentication-en). 完成驗證教學課程會提供所有 [!DNL Experience Platform] API呼叫，如下所示：

- 授權：承載 `{ACCESS_TOKEN}`
- x-api-key: `{API_KEY}`
- x-gw-ims-org-id: `{ORG_ID}`

中的所有資源 [!DNL Experience Platform] 與特定虛擬沙箱隔離。 所有請求 [!DNL Platform] API需要標頭，以指定要在中執行操作的沙箱名稱：

- x-sandbox-name: `{SANDBOX_NAME}`

>[!NOTE]
>
>如需中沙箱的詳細資訊，請參閱 [!DNL Platform]，請參閱 [沙箱概述檔案](../../sandboxes/home.md).

所有包含裝載(POST、PUT、PATCH)的請求都需要額外的標題：

- 內容類型：application/json

## 查找段定義的合併策略 {#merge-policy}

此工作流程從存取已知的受眾區段開始。 已啟用以用於 [!DNL Real-Time Customer Profile] 在其段定義中包含合併策略ID。 此合併原則包含要納入區段之資料集的相關資訊，而這些資料集又包含任何適用的資料使用標籤。

使用 [!DNL Segmentation] API，您可以根據其ID查找段定義，以查找其關聯的合併策略。

**API格式**

```http
GET /segment/definitions/{SEGMENT_DEFINITION_ID}
```

| 屬性 | 說明 |
| -------- | ----------- |
| `{SEGMENT_DEFINITION_ID}` | 您要查詢的區段定義ID。 |

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

成功的回應會傳回區段定義的詳細資訊。

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
| `mergePolicyId` | 用於段定義的合併策略的ID。 這會用於下一個步驟。 |

## 從合併策略中查找源資料集 {#datasets}

合併原則包含其來源資料集的相關資訊，而來源資料集又包含資料使用標籤。 您可以將合併策略ID提供給GET請求，以查找合併策略的詳細資訊 [!DNL Profile] API。 有關合併策略的詳細資訊，請參見 [合併策略終結點指南](../../profile/api/merge-policies.md).

**API格式**

```http
GET /config/mergePolicies/{MERGE_POLICY_ID}
```

| 屬性 | 說明 |
| -------- | ----------- |
| `{MERGE_POLICY_ID}` | 在 [上一步](#merge-policy). |

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
| `attributeMerge.type` | 合併策略的資料優先順序配置類型。 如果值為 `dataSetPrecedence`，則與此合併原則相關聯的資料集會列在 `attributeMerge > data > order`. 如果值為 `timestampOrdered`，則與中參考之結構關聯的所有資料集 `schema.name` 被合併策略使用。 |
| `attributeMerge.data.order` | 若 `attributeMerge.type` is `dataSetPrecedence`，此屬性將是一個陣列，內含此合併原則所使用資料集的ID。 這些ID會用於下一個步驟。 |

## 評估違反策略的資料集

>[!NOTE]
>
> 此步驟假設您至少有一個有效的資料使用原則，該原則可防止對包含特定標籤的資料執行特定行銷動作。 如果您對要評估的資料集沒有任何適用的使用原則，請遵循 [策略建立教程](../../data-governance/policies/create.md) 以先建立，然後再繼續此步驟。

取得合併原則來源資料集的ID後，即可使用 [策略服務API](https://www.adobe.io/experience-platform-apis/references/policy-service/) 根據特定行銷動作評估這些資料集，以檢查資料使用政策是否違反。

若要評估資料集，您必須在POST請求的路徑中提供行銷動作的名稱，同時在請求內文中提供資料集ID，如下列範例所示。

**API格式**

```http
POST /marketingActions/core/{MARKETING_ACTION_NAME}/constraints
POST /marketingActions/custom/{MARKETING_ACTION_NAME}/constraints
```

| 參數 | 說明 |
| --- | --- |
| `{MARKETING_ACTION_NAME}` | 與您評估資料集時依據的資料使用政策相關聯的行銷動作名稱。 根據策略是由Adobe還是貴組織定義，您必須使用 `/marketingActions/core` 或 `/marketingActions/custom`，分別為。 |

**要求**

下列要求會測試 `exportToThirdParty` 針對在 [上一步](#datasets). 要求裝載是包含每個資料集ID的陣列。

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
| `entityType` | 有效負載陣列中的每個項目必須指示要定義的實體類型。 在此使用案例中，值一律為「dataSet」。 |
| `entityID` | 裝載陣列中的每個項目都必須為資料集提供唯一ID。 |

**回應**

成功的回應會傳回行銷動作的URI、從提供的資料集收集的資料使用量標籤，以及因針對這些標籤測試動作而違反的任何資料使用策略清單。 在此範例中，「匯出資料至協力廠商」政策顯示於 `violatedPolicies` 陣列，表示行銷動作觸發了原則違反。

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
| `duleLabels` | 從提供的資料集擷取的資料使用量標籤清單。 |
| `discoveredLabels` | 請求裝載中提供的資料集清單，顯示在每個資料集層級和欄位層級標籤。 |
| `violatedPolicies` | 陣列，列出測試行銷動作(在 `marketingActionRef`) `duleLabels`. |

使用API回應中傳回的資料，您可以在體驗應用程式中設定通訊協定，以在發生原則違規時適當強制執行。

## 篩選資料欄位

如果您的受眾區段未通過評估，您可以透過下列兩種方法之一調整區段中包含的資料。

### 更新段定義的合併策略

更新區段定義的合併原則，將會調整執行區段作業時將包含的資料集和欄位。 請參閱 [更新現有合併策略](../../profile/api/merge-policies.md#update) 如需詳細資訊，請參閱API合併原則教學課程。

### 匯出區段時限制特定資料欄位

使用將區段匯出至資料集時 [!DNL Segmentation] API，您可以使用 `fields` 參數。 新增至此參數的任何資料欄位都會包含在匯出中，而其他所有資料欄位則會排除。

請考量具有名為「A」、「B」和「C」之資料欄位的區段。 如果您只想匯出欄位&quot;C&quot;，則 `fields` 參數將僅包含欄位&quot;C&quot;。 如此一來，匯出區段時，將會排除欄位&quot;A&quot;和&quot;B&quot;。

請參閱 [匯出區段](./evaluate-a-segment.md#export) 如需詳細資訊，請參閱區段教學課程。

## 後續步驟

依照本教學課程，您已查找與對象區段相關聯的資料使用量標籤，並針對特定行銷動作測試這些標籤是否違反政策。 如需資料控管的詳細資訊，請參閱 [!DNL Experience Platform]，請參閱的概觀 [資料控管](../../data-governance/home.md).
