---
keywords: Experience Platform；首頁；熱門主題；資料使用符合性；強制；資料使用符合性；分段服務；分段；分段；
solution: Experience Platform
title: 使用API對受眾區段強制執行資料使用量法規遵循
topic-legacy: tutorial
type: Tutorial
description: 本教學課程涵蓋使用API強制執行即時客戶設定檔受眾區段資料使用合規性的步驟。
exl-id: 2299328c-d41a-4fdc-b7ed-72891569eaf2
source-git-commit: 8133804076b1c0adf2eae5b748e86a35f3186d14
workflow-type: tm+mt
source-wordcount: '1358'
ht-degree: 1%

---

# 使用API對受眾區段強制執行資料使用法規遵循

本教學課程涵蓋使用API強制[!DNL Real-time Customer Profile]受眾區段符合資料使用情形的步驟。

## 快速入門

本教學課程需要認真了解[!DNL Adobe Experience Platform]的下列元件：

- [[!DNL Real-time Customer Profile]](../../profile/home.md): [!DNL Real-time Customer Profile] 是一般查詢實體存放區，可用來管理 [!DNL Experience Data Model (XDM)] 內的資 [!DNL Platform]料。設定檔會合併各種企業資料資產的資料，並以統一的簡報方式提供對該資料的存取。
   - [合併策略](../../profile/api/merge-policies.md):用於決定 [!DNL Real-time Customer Profile] 哪些資料可在特定條件下合併至統一檢視的規則。可以為[!DNL Data Governance]目的配置合併策略。
- [[!DNL Segmentation]](../home.md):如 [!DNL Real-time Customer Profile] 何將設定檔存放區中包含的大量個人群組，劃分為具有類似特徵且會對行銷策略採取類似回應的較小群組。
- [[!DNL Data Governance]](../../data-governance/home.md): [!DNL Data Governance] 使用以下元件提供資料使用標籤和強制實施的基礎架構：
   - [資料使用量標籤](../../data-governance/labels/user-guide.md):以處理個別資料的敏感程度來說明資料集和欄位的標籤。
   - [資料使用原則](../../data-governance/policies/overview.md):指出可對依特定資料使用標籤分類的資料執行哪些行銷動作的設定。
   - [政策執行](../../data-governance/enforcement/overview.md):允許您強制實施資料使用策略並防止構成策略違規的資料操作。
- [沙箱](../../sandboxes/home.md): [!DNL Experience Platform] 提供可將單一執行個體分割成個 [!DNL Platform] 別虛擬環境的虛擬沙箱，以協助開發及改進數位體驗應用程式。

以下各節提供您需要了解的其他資訊，以便成功呼叫[!DNL Platform] API。

### 讀取範例API呼叫

本教學課程提供範例API呼叫，以示範如何設定要求格式。 這些功能包括路徑、必要標題和格式正確的請求裝載。 也提供API回應中傳回的範例JSON。 如需範例API呼叫檔案中所使用慣例的資訊，請參閱[!DNL Experience Platform]疑難排解指南中[如何讀取範例API呼叫](../../landing/troubleshooting.md#how-do-i-format-an-api-request)一節。

### 收集必要標題的值

若要呼叫[!DNL Platform] API，您必須先完成[authentication tutorial](https://www.adobe.com/go/platform-api-authentication-en)。 完成驗證教學課程後，將提供所有[!DNL Experience Platform] API呼叫中每個必要標題的值，如下所示：

- 授權：承載`{ACCESS_TOKEN}`
- x-api-key: `{API_KEY}`
- x-gw-ims-org-id: `{IMS_ORG}`

[!DNL Experience Platform]中的所有資源都與特定虛擬沙箱隔離。 對[!DNL Platform] API的所有請求都需要標題，以指定作業將在下列位置進行的沙箱名稱：

- x-sandbox-name: `{SANDBOX_NAME}`

>[!NOTE]
>
>如需[!DNL Platform]中沙箱的詳細資訊，請參閱[沙箱概觀檔案](../../sandboxes/home.md)。

所有包含裝載(POST、PUT、PATCH)的請求都需要額外的標題：

- 內容類型：application/json

## 查找段定義的合併策略 {#merge-policy}

此工作流程從存取已知的受眾區段開始。 在[!DNL Real-time Customer Profile]中啟用的段在其段定義中包含合併策略ID。 此合併原則包含要納入區段之資料集的相關資訊，而這些資料集又包含任何適用的資料使用標籤。

使用[!DNL Segmentation] API，您可以根據其ID查找段定義，以查找其關聯的合併策略。

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
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
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
| `mergePolicyId` | 用於段定義的合併策略的ID。 這會用於下一個步驟。 |

## 從合併策略中查找源資料集 {#datasets}

合併原則包含其來源資料集的相關資訊，而來源資料集又包含資料使用標籤。 您可以在GET請求中為[!DNL Profile] API提供合併策略ID，以查找合併策略的詳細資訊。 有關合併策略的詳細資訊，請參閱[merge策略終結點指南](../../profile/api/merge-policies.md)。

**API格式**

```http
GET /config/mergePolicies/{MERGE_POLICY_ID}
```

| 屬性 | 說明 |
| -------- | ----------- |
| `{MERGE_POLICY_ID}` | 在[上一步](#merge-policy)中獲得的合併策略的ID。 |

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

成功的響應返回合併策略的詳細資訊。

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
| `attributeMerge.type` | 合併策略的資料優先順序配置類型。 如果值為`dataSetPrecedence`，則與此合併策略關聯的資料集將列在`attributeMerge > data > order`下。 如果值為`timestampOrdered`，則合併策略將使用與`schema.name`中引用的架構關聯的所有資料集。 |
| `attributeMerge.data.order` | 如果`attributeMerge.type`為`dataSetPrecedence`，則此屬性將是一個陣列，其中包含此合併策略所使用資料集的ID。 這些ID會用於下一個步驟。 |

## 評估違反策略的資料集

>[!NOTE]
>
> 此步驟假設您至少有一個有效的資料使用原則，該原則可防止對包含特定標籤的資料執行特定行銷動作。 如果對要評估的資料集沒有任何適用的使用策略，請按照[策略建立教程](../../data-governance/policies/create.md)建立一個策略，然後繼續執行此步驟。

取得合併原則來源資料集的ID後，您就可以使用[Policy Service API](https://www.adobe.io/experience-platform-apis/references/policy-service/)，根據特定行銷動作評估這些資料集，以檢查資料使用原則違反情形。

若要評估資料集，您必須在POST請求的路徑中提供行銷動作的名稱，同時在請求內文中提供資料集ID，如下列範例所示。

**API格式**

```http
POST /marketingActions/core/{MARKETING_ACTION_NAME}/constraints
POST /marketingActions/custom/{MARKETING_ACTION_NAME}/constraints
```

| 參數 | 說明 |
| --- | --- |
| `{MARKETING_ACTION_NAME}` | 與您評估資料集時依據的資料使用政策相關聯的行銷動作名稱。 根據策略是由Adobe還是您的組織定義，您必須分別使用`/marketingActions/core`或`/marketingActions/custom`。 |

**要求**

下列請求會針對在[上一步驟](#datasets)中取得的資料集測試`exportToThirdParty`行銷動作。 要求裝載是包含每個資料集ID的陣列。

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
| `entityType` | 有效負載陣列中的每個項目必須指示要定義的實體類型。 在此使用案例中，值一律為「dataSet」。 |
| `entityID` | 裝載陣列中的每個項目都必須為資料集提供唯一ID。 |

**回應**

成功的回應會傳回行銷動作的URI、從提供的資料集收集的資料使用量標籤，以及因針對這些標籤測試動作而違反的任何資料使用策略清單。 在此示例中，`violatedPolicies`陣列中顯示了「將資料導出到第三方」策略，表明行銷操作觸發了策略違規。

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
| `duleLabels` | 從提供的資料集擷取的資料使用量標籤清單。 |
| `discoveredLabels` | 請求裝載中提供的資料集清單，顯示在每個資料集層級和欄位層級標籤。 |
| `violatedPolicies` | 列出針對提供的`duleLabels`測試行銷動作（在`marketingActionRef`中指定）而違反之任何資料使用原則的陣列。 |

使用API回應中傳回的資料，您可以在體驗應用程式中設定通訊協定，以在發生原則違規時適當強制執行。

## 篩選資料欄位

如果您的受眾區段未通過評估，您可以透過下列兩種方法之一調整區段中包含的資料。

### 更新段定義的合併策略

更新區段定義的合併原則，將會調整執行區段作業時將包含的資料集和欄位。 如需詳細資訊，請參閱API合併原則教學課程中[更新現有合併原則](../../profile/api/merge-policies.md#update)的相關章節。

### 匯出區段時限制特定資料欄位

使用[!DNL Segmentation] API將區段匯出至資料集時，您可以使用`fields`參數來篩選匯出中包含的資料。 新增至此參數的任何資料欄位都會包含在匯出中，而其他所有資料欄位則會排除。

請考量具有名為「A」、「B」和「C」之資料欄位的區段。 如果您只希望導出欄位&quot;C&quot;，則`fields`參數將僅包含欄位&quot;C&quot;。 如此一來，匯出區段時，將會排除欄位&quot;A&quot;和&quot;B&quot;。

如需詳細資訊，請參閱區段教學課程中關於[匯出區段](./evaluate-a-segment.md#export)的區段。

## 後續步驟

依照本教學課程，您已查找與對象區段相關聯的資料使用量標籤，並針對特定行銷動作測試這些標籤是否違反政策。 有關[!DNL Experience Platform]中[!DNL Data Governance]的詳細資訊，請閱讀[[!DNL Data Governance]](../../data-governance/home.md)的概述。
