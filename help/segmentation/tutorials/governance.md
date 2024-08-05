---
solution: Experience Platform
title: 使用API強制對象區段遵守資料使用規範
type: Tutorial
description: 本教學課程涵蓋使用API強制資料使用法規遵循區段定義的步驟。
exl-id: 2299328c-d41a-4fdc-b7ed-72891569eaf2
source-git-commit: 914174de797d7d5f6c47769d75380c0ce5685ee2
workflow-type: tm+mt
source-wordcount: '1348'
ht-degree: 6%

---

# 使用API強制區段定義的資料使用合規性

本教學課程涵蓋使用API強制區段定義符合資料使用規範的步驟。

## 快速入門

此教學課程需要您實際瞭解[!DNL Adobe Experience Platform]的下列元件：

- [[!DNL Real-Time Customer Profile]](../../profile/home.md)： [!DNL Real-Time Customer Profile]是一般查詢實體存放區，用來管理[!DNL Platform]內的[!DNL Experience Data Model (XDM)]資料。 設定檔會合併各種企業資料資產的資料，並在統一的簡報中提供該資料的存取權。
   - [合併原則](../../profile/api/merge-policies.md)： [!DNL Real-Time Customer Profile]用來決定哪些資料可以在特定條件下合併到統一檢視中的規則。 您可以針對資料控管目的設定合併原則。
- [[!DNL Segmentation]](../home.md)： [!DNL Real-Time Customer Profile]如何將設定檔存放區中包含的大量個人群組劃分為具有類似特徵且會以類似方式回應行銷策略的較小群組。
- [資料控管](../../data-governance/home.md)：「資料控管」使用下列元件，提供資料使用標籤與強制實施的基礎結構：
   - [資料使用標籤](../../data-governance/labels/user-guide.md)：用來描述資料集和欄位的標籤，以處理其個別資料的敏感度等級。
   - [資料使用原則](../../data-governance/policies/overview.md)：指出對依特定資料使用標籤分類的資料允許哪些行銷動作的設定。
   - [原則執行](../../data-governance/enforcement/overview.md)：可讓您執行資料使用原則，並防止構成原則違規的資料作業。
- [沙箱](../../sandboxes/home.md)： [!DNL Experience Platform]提供可將單一[!DNL Platform]執行個體分割成個別虛擬環境的虛擬沙箱，以利開發及改進數位體驗應用程式。

下列章節提供您需瞭解的其他資訊，才能成功呼叫[!DNL Platform] API。

### 讀取範例 API 呼叫

本教學課程提供範例API呼叫，示範如何格式化您的請求。 這些包括路徑、必要的標頭和正確格式化的請求承載。 此外，也提供 API 回應中傳回的範例 JSON。 如需檔案中所使用範例API呼叫慣例的詳細資訊，請參閱[!DNL Experience Platform]疑難排解指南中[如何讀取範例API呼叫](../../landing/troubleshooting.md#how-do-i-format-an-api-request)一節。

### 收集所需標頭的值

若要呼叫[!DNL Platform] API，您必須先完成[驗證教學課程](https://www.adobe.com/go/platform-api-authentication-en)。 完成驗證教學課程會提供所有 [!DNL Experience Platform] API 呼叫中每個必要標頭的值，如下所示：

- 授權：持有人`{ACCESS_TOKEN}`
- x-api-key： `{API_KEY}`
- x-gw-ims-org-id： `{ORG_ID}`

[!DNL Experience Platform]中的所有資源都與特定的虛擬沙箱隔離。 對[!DNL Platform] API的所有請求都需要標頭，以指定將在其中執行作業的沙箱名稱：

- x-sandbox-name： `{SANDBOX_NAME}`

>[!NOTE]
>
>如需[!DNL Platform]中沙箱的詳細資訊，請參閱[沙箱概觀檔案](../../sandboxes/home.md)。

所有包含承載 (POST、PUT、PATCH) 的請求都需有額外的標頭：

- Content-Type： application/json

## 查詢區段定義的合併原則 {#merge-policy}

此工作流程從存取已知的區段定義開始。 啟用以在[!DNL Real-Time Customer Profile]中使用的區段定義，在其區段定義中包含合併原則ID。 此合併原則包含要將哪些資料集納入區段定義的資訊，而這些資料集又包含任何適用的資料使用標籤。

使用[!DNL Segmentation] API，您可以依其ID查詢區段定義，以尋找其相關聯的合併原則。

**API格式**

```http
GET /segment/definitions/{SEGMENT_DEFINITION_ID}
```

| 屬性 | 說明 |
| -------- | ----------- |
| `{SEGMENT_DEFINITION_ID}` | 您要查詢之區段定義的ID。 |

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

成功的回應會傳回區段定義的詳細資料。

```json
{
    "id": "24379cae-726a-4987-b7b9-79c32cddb5c1",
    "schema": { 
        "name": "_xdm.context.profile"
    },
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
| `mergePolicyId` | 用於區段定義的合併原則ID。 這將在下一個步驟中使用。 |

## 從合併原則尋找來源資料集 {#datasets}

合併原則包含其來源資料集的相關資訊，而來源資料集又包含資料使用標籤。 您可以在[!DNL Profile] API的GET要求中提供合併原則ID，以查詢合併原則的詳細資料。 您可以在[合併原則端點指南](../../profile/api/merge-policies.md)中找到有關合併原則的更多資訊。

**API格式**

```http
GET /config/mergePolicies/{MERGE_POLICY_ID}
```

| 屬性 | 說明 |
| -------- | ----------- |
| `{MERGE_POLICY_ID}` | 在[先前步驟](#merge-policy)中取得的合併原則識別碼。 |

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

成功的回應會傳回合併原則的詳細資料。

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
| `schema.name` | 與合併原則關聯的結構描述名稱。 |
| `attributeMerge.type` | 合併原則的資料優先順序設定型別。 如果值為`dataSetPrecedence`，則與此合併原則關聯的資料集將列在`attributeMerge > data > order`下。 如果值為`timestampOrdered`，則合併原則會使用與`schema.name`中參考的結構描述關聯的所有資料集。 |
| `attributeMerge.data.order` | 如果`attributeMerge.type`是`dataSetPrecedence`，則此屬性將是包含此合併原則所使用資料集ID的陣列。 這些ID會用於下一個步驟。 |

## 評估原則違規的資料集

>[!NOTE]
>
> 此步驟假設您至少有一個有效資料使用原則，可防止在包含特定標籤的資料上執行特定行銷動作。 如果您沒有所評估資料集的任何適用使用原則，請依照[原則建立教學課程](../../data-governance/policies/create.md)建立一個，然後再繼續此步驟。

取得合併原則來源資料集的ID後，您就可以使用[原則服務API](https://www.adobe.io/experience-platform-apis/references/policy-service/)來根據特定行銷動作評估這些資料集，以檢查資料使用原則是否違規。

若要評估資料集，您必須在POST請求的路徑中提供行銷動作的名稱，同時在請求內文中提供資料集ID，如下列範例所示。

**API格式**

```http
POST /marketingActions/core/{MARKETING_ACTION_NAME}/constraints
POST /marketingActions/custom/{MARKETING_ACTION_NAME}/constraints
```

| 參數 | 說明 |
| --- | --- |
| `{MARKETING_ACTION_NAME}` | 與您正在評估資料集的資料使用原則關聯的行銷動作名稱。 視原則是由Adobe或您的組織定義而定，您必須分別使用`/marketingActions/core`或`/marketingActions/custom`。 |

**要求**

下列要求會針對在[先前的步驟](#datasets)中取得的資料集，測試`exportToThirdParty`行銷動作。 請求承載是包含每個資料集ID的陣列。

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
| `entityType` | 承載陣列中的每個專案都必須指出正在定義的實體型別。 對於此使用案例，值將一律為「dataSet」。 |
| `entityID` | 承載陣列中的每個專案都必須提供資料集的唯一ID。 |

**回應**

成功的回應會傳回行銷動作的URI、從提供的資料集收集的資料使用標籤，以及針對這些標籤測試動作所違反的任何資料使用原則清單。 在此範例中，「將資料匯出至第三方」原則顯示在`violatedPolicies`陣列中，表示行銷動作觸發了原則違規。

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
| `duleLabels` | 從提供的資料集中擷取的資料使用標籤清單。 |
| `discoveredLabels` | 請求承載中提供的資料集清單，顯示可在每個資料集找到之資料集層級和欄位層級標籤。 |
| `violatedPolicies` | 陣列會針對提供的`duleLabels`列出測試行銷動作（在`marketingActionRef`中指定）所違反的任何資料使用原則。 |

您可以使用API回應中傳回的資料，在體驗應用程式中設定通訊協定，以便在發生原則違規時適當地強制執行。

## 篩選資料欄位

如果您的區段定義未通過評估，則您可透過下列兩種方法之一調整區段定義中包含的資料。

### 更新區段定義的合併原則

更新區段定義的合併原則將調整資料集和執行區段作業時要包含的欄位。 如需詳細資訊，請參閱API合併原則教學課程中有關[更新現有合併原則](../../profile/api/merge-policies.md#update)的章節。

### 匯出區段定義時限制特定資料欄位

使用[!DNL Segmentation] API將區段定義匯出至資料集時，您可以使用`fields`引數來篩選匯出中包含的資料。 所有新增至此引數的資料欄位都會包含在匯出中，而所有其他資料欄位則會被排除。

假設區段定義有名為「A」、「B」和「C」的資料欄位。 如果您只想匯出欄位「C」，則`fields`引數將會單獨包含欄位「C」。 如此一來，匯出區段定義時就會排除「A」和「B」欄位。

如需詳細資訊，請參閱分段教學課程中有關[匯出區段定義](./evaluate-a-segment.md#export)的章節。

## 後續步驟

依照本教學課程，您已查詢與區段定義相關聯的資料使用標籤，並測試它們是否違反特定行銷動作的原則。 如需[!DNL Experience Platform]中資料控管的詳細資訊，請閱讀[資料控管](../../data-governance/home.md)的概觀。
