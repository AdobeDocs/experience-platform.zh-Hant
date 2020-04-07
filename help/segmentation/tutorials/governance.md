---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: 對受眾細分強制執行資料使用規範
topic: tutorial
translation-type: tm+mt
source-git-commit: f5bc9beb59e83b0411d98d901d5055122a124d07

---


# 使用API強制觀眾區隔的資料使用符合性

本教學課程涵蓋使用API強制「即時客戶個人檔案」受眾細分資料使用合規性的步驟。

## 快速入門

本教學課程需要對Adobe Experience Platform的下列元件有正確的認識：

- [即時客戶個人檔案](../../profile/home.md):即時客戶描述檔是一般查閱實體儲存，用於管理平台內的體驗資料模型(XDM)資料。 描述檔會合併各種企業資料資產的資料，並以統一的簡報來存取該資料。
   - [合併策略](../../profile/api/merge-policies.md):「即時客戶個人檔案」用來判斷哪些資料可在特定條件下合併為統一檢視的規則。 可以為「資料治理」目的配置合併策略。
- [區段](../home.md):即時客戶個人檔案如何將個人檔案存放區中包含的大量個人群組分割為具有類似特性且回應類似行銷策略的較小群組。
- [資料治理](../../data-governance/home.md):Data Governance使用下列元件為資料使用標籤和強制實施(DULE)提供了基礎架構：
   - [資料使用標籤](../../data-governance/labels/user-guide.md):標籤用來說明資料集和欄位，以處理其個別資料的敏感度等級為準。
   - [資料使用原則](../../data-governance/api/getting-started.md):指示允許針對依特定資料使用標籤分類之資料執行哪些行銷動作的設定。

以下章節提供您必須知道的其他資訊，才能成功呼叫平台API。

### 讀取範例API呼叫

本教學課程提供範例API呼叫，以示範如何設定請求的格式。 這些包括路徑、必要標題和正確格式化的請求負載。 也提供API回應中傳回的範例JSON。 如需範例API呼叫檔案中所用慣例的詳細資訊，請參閱「Experience Platform疑難排解指 [南」中有關如何讀取範例API呼叫的章節](../../landing/troubleshooting.md#how-do-i-format-an-api-request) 。

### 收集必要標題的值

若要呼叫平台API，您必須先完成驗證教 [學課程](../../tutorials/authentication.md)。 完成驗證教學課程後，所有Experience Platform API呼叫中每個必要標題的值都會顯示在下方：

- 授權：生產者 `{ACCESS_TOKEN}`
- x-api-key: `{API_KEY}`
- x-gw-ims-org-id: `{IMS_ORG}`

Experience Platform中的所有資源都隔離至特定的虛擬沙盒。 所有對平台API的請求都需要一個標題，該標題會指定要在中執行的操作的沙盒名稱：

- x-sandbox-name: `{SANDBOX_NAME}`

>[!NOTE] 如需平台中沙盒的詳細資訊，請參閱沙盒 [概觀檔案](../../sandboxes/home.md)。

所有包含裝載(POST、PUT、PATCH)的請求都需要額外的標題：

- 內容類型：application/json

## 查閱區段定義的合併原則

此工作流程從存取已知觀眾區隔開始。 在即時客戶描述檔中啟用的區段在其區段定義中包含合併原則ID。 此合併策略包含有關哪些資料集要包含在段中的資訊，這些資料集又包含任何適用的資料使用標籤。

使用 [分段API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/segmentation.yaml)，您可以依其ID來查閱區段定義，以尋找其相關的合併原則。

**API格式**

```http
GET /segment/definitions/{SEGMENT_DEFINITION_ID}
```

| 屬性 | 說明 |
| -------- | ----------- |
| `{SEGMENT_DEFINITION_ID}` | 您要查閱的區段定義ID。 |

**請求**

```shell
curl -X GET \
  https://platform.adobe.io/data/core/ups/segment/definitions/24379cae-726a-4987-b7b9-79c32cddb5c1 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Reponse**

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

## 從合併策略中查找源資料集

合併策略包含有關其源資料集的資訊，這些資訊又包含DULE標籤。 您可以在GET請求中提供合併原則ID給描述檔API，以查閱合併原則的詳細資訊。

**API格式**

```http
GET /config/mergePolicies/{MERGE_POLICY_ID}
```

| 屬性 | 說明 |
| -------- | ----------- |
| `{MERGE_POLICY_ID}` | 在上一步驟中取得的合併原則 [ID](#lookup-a-merge-policy-for-a-segment-definition)。 |

**請求**

```shell
curl -X GET \
  https://platform.adobe.io/data/core/ups/config/mergePolicies/2b43d78d-0ad4-4c1e-ac2d-574c09b01119 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Reponse**

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
| `attributeMerge.type` | 合併策略的資料優先順序配置類型。 如果值為，則 `dataSetPrecedence`與此合併策略關聯的資料集列在下面 `attributeMerge > data > order`。 如果值為，則 `timestampOrdered`合併策略將使用與中引用的模式 `schema.name` 關聯的所有資料集。 |
| `attributeMerge.data.order` | 如果 `attributeMerge.type` 為， `dataSetPrecedence`則此屬性將是包含此合併策略所使用資料集的ID的陣列。 這些ID會用於下一步驟。 |

## 查閱來源資料集的資料使用標籤

收集合併策略的源資料集的ID後，可以使用這些ID查找為資料集本身配置的資料使用標籤及其中包含的任何特定資料欄位。

下列對 [](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/catalog.yaml) Catalog Service API的呼叫會在請求路徑中提供其ID，以擷取與單一資料集相關的資料使用標籤：

**API格式**

```http
GET /dataSets/{DATASET_ID}/dule
```

| 屬性 | 說明 |
| -------- | ----------- |
| `{DATASET_ID}` | 您要查閱其資料使用標籤的資料集ID。 |

**請求**

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/catalog/dataSets/5b95b155419ec801e6eee780/dule \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Reponse**

成功的響應返回與整個資料集相關聯的資料使用標籤清單，以及與源模式相關聯的任何特定資料欄位。

```json
{
    "connection": {},
    "dataset": {
        "identity": [],
        "contract": [
            "C3"
        ],
        "sensitive": [],
        "contracts": [
            "C3"
        ],
        "identifiability": [],
        "specialTypes": []
    },
    "fields": [],
    "schemaFields": [
        {
            "path": "/properties/personalEmail/properties/address",
            "identity": [
                "I1"
            ],
            "contract": [
                "C2",
                "C9"
            ],
            "sensitive": [],
            "contracts": [
                "C2",
                "C9"
            ],
            "identifiability": [
                "I1"
            ],
            "specialTypes": []
        }
    ]
}
```

| 屬性 | 說明 |
| -------- | ----------- |
| `dataset` | 包含整體套用至資料集之資料使用標籤的物件。 |
| `schemaFields` | 表示特定方案欄位的對象陣列，這些欄位具有應用於它們的資料使用標籤。 |
| `schemaFields.path` | 模式欄位的路徑，其資料使用標籤列在同一對象中。 |

## 篩選資料欄位

>[!NOTE] 此步驟為可選步驟。 如果您不想根據您在上一步驟尋找資料使用標籤時的發現來調整區段中包含的資料 [，則可跳至評估資料是否違反原則](#lookup-data-usage-labels-for-the-source-datasets)的最後步驟 [](#evaluate-data-for-policy-violations)。

如果您想要調整觀眾區隔中包含的資料，可以使用下列兩種方法之一：

### 更新區段定義的合併原則

更新區段定義的合併原則將會調整執行區段工作時將包含的資料集和欄位。 有關詳細資訊，請 [參閱合併策略教程中有關更新現有合併策略的章節](../../profile/api/merge-policies.md) 。

### 匯出區段時限制特定資料欄位

使用即時客戶描述檔API將區段匯出至資料集時，您可以使用參數來篩選匯出中包含的資 `fields` 料。 新增至此參數的任何資料欄位都會包含在匯出中，而所有其他資料欄位則會被排除。

請考慮具有名為&quot;A&quot;、&quot;B&quot;和&quot;C&quot;的資料欄位的區段。 如果您只想匯出欄位&quot;C&quot;，則參 `fields` 數將僅包含欄位&quot;C&quot;。 執行此動作後，匯出區段時會排除欄位&quot;A&quot;和&quot;B&quot;。

如需詳細資訊，請 [參閱區段教學課程](./evaluate-a-segment.md#export-a-segment) 中有關匯出區段的章節。

## 評估違反策略的資料

現在您已收集與受眾區段關聯的資料使用標籤，您可以針對行銷動作測試這些標籤，以評估是否有任何資料使用政策違規。 有關如何使用 [DULE Policy Service API執行策略評估的詳細步驟](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/dule-policy-service.yaml)，請參閱策略評估 [文檔](../../data-governance/enforcement/overview.md)。

## 後續步驟

透過本教學課程，您已查找與觀眾區隔相關的資料使用標籤，並測試它們是否違反特定行銷動作的政策。 如需Experience Platform中資料治理的詳細資訊，請參閱資 [料治理概觀](../../data-governance/home.md)。