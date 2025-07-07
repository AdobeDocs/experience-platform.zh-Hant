---
title: 使用TTL管理Data Lake中的體驗事件資料集保留
description: 瞭解如何使用存留時間(TTL)設定和Adobe Experience Platform API，評估、設定和管理Data Lake中的體驗事件資料集保留。 本指南說明TTL資料列層級的有效期限如何支援資料保留原則、最佳化儲存效率，以及確保有效的資料生命週期管理。 此外，還提供使用案例和最佳實務，協助您有效套用TTL。
exl-id: d688d4d0-aa8b-4e93-a74c-f1a1089d2df0
source-git-commit: 65a132609bc30233ac9f7efbe1981d4f75f3acb9
workflow-type: tm+mt
source-wordcount: '2458'
ht-degree: 0%

---

# 使用TTL管理資料湖中的體驗事件資料集保留

高效的資料管理對於最佳效能、成本控制及資料完整性至關重要。 使用體驗事件資料集保留存留時間(TTL)強制執行列層級的有效期，自動從資料湖的資料集中移除過時的記錄，同時確保最佳儲存效率和資料關聯性。

本指南說明如何使用目錄服務API來評估、設定和管理TTL。 您將瞭解何時及為何套用TTL、如何使用API呼叫設定和更新TTL值，以及確保有效實施的最佳實務。

>[!IMPORTANT]
>
>TTL的設計目標是最佳化資料生命週期管理和儲存效率。 這不是合規性工具，也不應依賴法規要求。 法規遵循通常需要更廣泛的資料治理策略。

## 為何使用TTL進行列層級資料管理

隨著資料整合長，有效率的資料管理對於保留效能、控制成本以及維持資料相關性的重要性日益提高。 TTL型資料列層級資料到期會移除過時的記錄，自動進行資料清理，無需手動介入，以協助最佳化儲存空間並提升系統效率。

TTL在管理時效性資料時會很有用，因為這類資料會隨著時間推移而失去相關性。 如果您有以下需要，請考慮實作TTL：

- 自動移除過時的記錄，降低儲存成本。
- 將無關資料減至最少，以改善查詢效能。
- 僅保留相關資訊以維持資料衛生。
- 最佳化資料保留，以支援業務目標。

>[!NOTE]
>
>體驗事件資料集保留適用於儲存在Data Lake中的事件資料。 如果您在Real-Time Customer Data Platform中管理保留，請考慮搭配使用[體驗事件有效期](../../profile/event-expirations.md)和[假名設定檔有效期](../../profile/pseudonymous-profiles.md)以及資料湖保留設定。

使用TTL設定，根據許可權最佳化儲存空間。 雖然在Real-Time CDP中使用的設定檔存放區資料可能會被視為過時，並在30天後移除，但針對分析和資料Distiller使用案例，資料湖中的相同事件資料仍可在12至13個月內可用（或更久則根據權益）。

>[!TIP]
>
>權益是指由您的Adobe訂閱與授權合約所定義的儲存與保留配額。

### 行業範例 {#industry-example}

例如，考慮使用視訊串流服務來追蹤使用者互動，例如視訊檢視、搜尋和推薦。 雖然最近的參與資料對個人化至關重要，但較舊的活動記錄（例如一年前的互動）會失去相關性。 透過使用列層級的有效期，Experience Platform會自動移除過時的記錄，確保只有目前且有意義的資料才會用於分析和建議。

## 評估TTL適用性 {#evaluate-ttl-suitability}

在套用保留原則之前，請評估您的資料集是否適合列層級的有效期。 請考量下列事項：

- 一段時間的資料關聯性：較舊的資料是否提供價值，或是會過時？
- 對下遊程式的影響：移除資料是否會影響報表、分析或整合？
- 儲存成本與保留價值：舊資料的價值是否足以證明儲存資料的成本？

如果歷史記錄對長期分析或業務營運至關重要，則TTL可能不是正確的方法。 檢閱這些因素，可確保TTL符合您的資料保留需求，而不會對資料可用性造成負面影響。

## 設定TTL的最佳實務 {#best-practices}

選取正確的TTL值，以確保您的體驗事件資料集保留原則可平衡資料保留、儲存效率和分析需求。 太短的TTL可能會導致資料遺失，而太長的TTL可能會增加儲存成本及不必要的資料累積。 考量資料被存取的頻率以及資料的相關性維持多久，確保TTL符合資料集的用途。

下表根據資料集型別和使用模式提供常見的TTL建議：

| 資料集型別 | 建議的TTL | 典型使用案例 |
|-----------------------------|------------------------|-------------------|
| 經常存取的資料集 | 30-90天 | 使用者參與記錄、網站點按資料流資料、短期行銷活動績效資料。 |
| 封存資料集 | 1年以上 | 財務交易記錄、合規性資料、長期趨勢分析、機器學習訓練資料集。 |
| 應用程式管理的資料集 | 最長13個月 | 系統管理的資料集有預先定義的TTL限制，這些限制會自動強制以遵守系統施加的限制。 |
| 客戶管理的資料集 | 30天 — 最大TTL | 透過UI、API或Data Distiller建立的資料集。 TTL必須至少為30天，並且必須在定義的最大TTL範圍內。 |

請定期檢閱TTL設定，以確保其持續符合您的儲存原則、分析需求及業務需求。

### 設定TTL時的主要考量事項 {#key-considerations}

請遵循下列最佳實務，以確保TTL設定符合您的資料保留策略：

- 定期稽核TTL變更。 每次TTL更新都會觸發稽核事件。 使用稽核記錄來追蹤TTL修改，以符合法規、資料控管和疑難排解目的。
- 如果資料必須無限期保留，請停用TTL。 若要停用TTL，請將`ttlValue`設定為`null`。 如此可防止自動過期，並永久保留所有記錄。 進行此變更前，請先考量儲存空間的影響。

## TTL的限制 {#limitations}

使用TTL時，請注意下列限制：

- 使用TTL的&#x200B;**體驗事件資料集保留套用至資料列層級的有效期**，而非資料集刪除。 TTL會根據定義的保留期移除記錄，但不會刪除整個資料集。 若要移除資料集，請使用[資料集到期端點](../../hygiene/api/dataset-expiration.md)或手動刪除。
- **TTL設定保持使用中狀態，直到明確停用**。 在您停用此設定之前，它一直有效。 停用TTL會停止過期，並確保資料集中的所有記錄都會保留。
- **TTL不是規範工具**。 雖然TTL可以最佳化儲存與生命週期管理，但您必須實作更廣泛的治理策略，以確保法規遵循性。

## 在套用TTL之前分析資料集大小和關聯性 {#analyze-dataset-size}

在套用TTL之前，請使用查詢來分析資料集大小和關聯性。 執行目標查詢（例如計算特定日期範圍內的記錄數）以預覽各種TTL值的影響。 然後使用此資訊來選擇最佳保留期間，以平衡資料公用程式與成本效益。

![在體驗事件資料集上實作TTL的視覺化工作流程。 步驟包括：評估資料期限和移除的影響、使用查詢驗證TTL設定、透過目錄服務API設定TTL，以及持續監視TTL影響並進行調整。](../images/datasets/dataset-retention-ttl-guide/manage-experience-event-dataset-retention-in-the-data-lake.png)

執行目標查詢可協助判斷在不同TTL設定下會保留或移除多少資料。 例如，下列SQL查詢會計算過去30天內建立的記錄數：

```sql
SELECT COUNT(1) FROM [datasetName] WHERE timestamp > date_sub(now(), INTERVAL 30 DAY);
```

針對不同的時間間隔執行類似的查詢有助於驗證TTL設定，並確保它們在儲存效率和資料可存取性之間取得平衡。

## 開始使用TTL管理

您必須先瞭解如何正確格式化請求，才能使用目錄服務API評估、設定及管理體驗事件資料集保留。 這包括瞭解API路徑、提供必要的標頭以及格式化要求承載。 如需此重要資訊，請參閱[目錄服務API快速入門手冊](../api/getting-started.md)。

>[!NOTE]
>
>本檔案說明列層級的有效期，此有效期會刪除資料集中的個別過期列，同時保持資料集本身不變。 這不適用於資料集有效期，因為到期日會移除整個資料集，並由另一個功能管理。 如需資料集層級的有效期，請參閱[資料集有效期API檔案](../../hygiene/api/dataset-expiration.md)。

### 檢查您的TTL限制 {#check-ttl-constraints}

使用資料衛生API `/ttl/{DATASET_ID}`端點協助規劃TTL設定。 此端點會傳回貴組織支援的最小TTL值和最大TTL值，以及資料集型別的建議值(`defaultValue`)。

如需詳細資訊，請參閱Adobe Developer [資料衛生API](https://developer.adobe.com/experience-platform-apis/references/data-hygiene/#operation/getTtl)檔案。

若要[檢查目前套用至資料集](#check-applied-ttl-values)的TTL，請改為向[目錄服務API](https://developer.adobe.com/experience-platform-apis/references/catalog/) `/dataSets/{DATASET_ID}`端點發出GET要求。

>[!TIP]
>
>目錄服務API的Experience Platform閘道URL和基本路徑為： `https://platform.adobe.io/data/foundation/catalog`。 資料衛生API的基本路徑為： `https://platform.adobe.io/data/core/hygiene`

**API格式**

```http
GET /ttl/{DATASET_ID}
```

| 參數 | 說明 |
| --- | --- |
| `{DATASET_ID}` | 系統產生的字串，可唯一識別資料集。 若要尋找資料集識別碼，請使用`/datasets`端點。 請參閱[清單目錄物件API指南](../api/list-objects.md)，取得篩選相關資料集回應的指示。 |

**要求**

以下請求會擷取貴組織特定資料集的TTL限制。

```shell
curl -X GET \
  'https://platform.adobe.io/data/foundation/catalog/ttl/{DATASET_ID}' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
  -H 'x-sandbox-id: {SANDBOX_ID}'
```

**回應**

成功的回應會根據您組織的權益，傳回建議、最大和最小TTL值，以及資料集的建議TTL (`defaultValue`)。 此`defaultValue`為建議的TTL期間，僅供指引使用。 除非您明確設定，否則不會套用它。 回應不包含任何可能已設定的自訂TTL值。 若要檢視資料集的目前TTL，請使用GET `/catalog/dataSets/{DATASET_ID}`端點。

+++選取以檢視回應

```json
{
  "extensions": {
    "adobe_lakeHouse": {
      "rowExpiration": {
        "defaultValue": "P12M",
        "maxValue": "P12M",
        "minValue": "P7D"
      }
    }
  }
}
```

+++

| 屬性 | 說明 |
|--------------|-------------|
| `defaultValue` | 為您的資料集建議的TTL值。 這個值是&#x200B;**不是**&#x200B;自動套用。 您必須明確設定TTL，才能使其生效。 |
| `maxValue` | 貴組織權益所允許的最長TTL期間。 一般而言，此期間為10年(`P10Y`)。 |
| `minValue` | 貴組織權益所允許的最短TTL期間。 此期間通常為30天(`P30D`)。 |

### 如何檢查套用的TTL值 {#check-applied-ttl-values}

若要檢查已套用至資料集的目前TTL值，請使用以下API呼叫：

```http
GET /dataSets/{DATASET_ID}
```

此呼叫傳回`ttlValue`區段中目前的`extensions.adobe_lakeHouse.rowExpiration` （如果已設定）。

**要求**

以下請求會擷取貴組織特定資料集的TTL值。

```shell
curl -X GET \
https://platform.adobe.io/data/foundation/catalog/dataSets/{DATASET_ID} \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**回應**

成功的回應包含`extensions`物件，其中包含套用至資料集的目前TTL組態。 為了簡短起見，下面的回應範例會遭截斷。

```json
{
    "{DATASET_ID}": {
        "name": "Acme Sales Data",
        "description": "This dataset contains sales transaction records for Acme Corporation.",
        "imsOrg": "{ORG_ID}",
        "sandboxId": "{SANDBOX_ID}",
        "extensions": {
            "adobe_lakeHouse": {
            "rowExpiration": {
                "ttlValue": "P3M",
            }
            }
        }
        ...
    }
}
```

### 設定或更新資料集的TTL {#set-update-ttl}

>[!IMPORTANT]
>
>TTL型列層級到期日只能套用至使用時間序列結構描述的事件資料集。 這包括以標準XDM ExperienceEvent類別以及擴充時間序列結構描述(`https://ns.adobe.com/xdm/data/time-series`)的自訂結構描述為基礎的資料集。
>
>在套用TTL之前，請使用結構描述登入API來檢查`meta:extends`屬性，以確認資料集的結構描述包含正確的延伸。 如需如何執行此動作的指引，請參閱[結構描述端點檔案](../../xdm/api/schemas.md#lookup)。

您可以設定新的TTL或使用相同的API方法更新現有的TTL，以設定體驗事件資料集保留。 使用PATCH要求至`/v2/datasets/{DATASET_ID}`端點以套用或調整TTL。

**API格式**

```http
PATCH /v2/datasets/{DATASET_ID}
```

| 參數 | 說明 |
| --- | --- |
| `{DATASET_ID}` | 您要更新TTL值的資料集ID。 |

**要求**

在下列範例中，`ttlValue`設定為`P3M`。 這表示超過三個月的記錄會自動刪除。 調整保留期間以符合您的業務需求（例如，`P6M`為六個月，`P12M`為一年）。

```shell
curl -X PATCH \
  'https://platform.adobe.io/data/foundation/catalog/v2/datasets/{DATASET_ID}' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -d '{
    "extensions": {
        "adobe_lakeHouse": {
            "rowExpiration": {
                "ttlValue": "P3M"  // A 3 month retention period
            }
        }
    }
}
```

| 屬性 | 說明 |
|----------------------------------|-------------|
| `rowExpiration.ttlValue` | 定義自動移除資料集中的記錄之前的持續時間。 使用ISO-8601週期格式（例如，`P3M`代表3個月，`P30D`代表30天）。 |

**回應**

成功的回應會傳回已更新資料集的參考，但不會明確包含TTL設定。 若要確認TTL設定，請進行後續的`GET /dataSets/{DATASET_ID}`要求。

```JSON
[
  "@/dataSets/{DATASET_ID}"
]
```

#### 範例情境 {#example-scenario}

考慮使用影片串流平台，該平台最初將TTL設定為三個月，以確保個人化有全新的參與資料。 不過，如果後續分析顯示較舊的互動仍可提供有價值的深入分析，則提出下列請求後，TTL可延長至6個月：

```shell
curl -X PATCH \
  'https://platform.adobe.io/data/foundation/catalog/v2/datasets/{DATASET_ID}' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -d '{
    "extensions": {
        "adobe_lakeHouse": {
            "rowExpiration": {
                "ttlValue": "P6M"  // Extend to 6 months
            }
        }
    }
}
```

## 資料集保留原則常見問題集 {#faqs}

此常見問題集涵蓋資料集保留工作、TTL變更的立即影響、復原選項，以及不同Platform服務的保留期間差異等實務問題。

### 我可以套用保留原則規則到哪些型別的資料集？

+++回答
您可以套用TTL型保留原則至任何使用時間序列行為的資料集。 這包括以標準XDM ExperienceEvent類別為基礎的資料集，以及用來擷取時間序列資料的自訂結構描述。

列層級的有效期需要下列技術條件：

- 結構描述在設計上必須用來擷取時間序列資料。
- 結構描述必須包含用於評估到期時間的時間戳記欄位。
- 資料集應儲存事件層級的資料，通常使用或擴充XDM ExperienceEvent類別。
- 資料集必須在目錄服務中註冊，因為TTL設定是透過`extensions.adobe_lakeHouse.rowExpiration`套用。
- TTL值必須使用ISO-8601期間格式（例如，`P30D`、`P6M`、`P1Y`）。
+++

### 資料集保留工作多久會從Data Lake服務中刪除資料？

+++回答
每30天會評估及處理資料集TTL，刪除所有過期的記錄。 如果事件在超過30天（擷取日期> 30天）前擷取至Experience Platform，且其事件日期超過定義的保留期間(TTL)，則會視為已過期。
+++

<!-- ### How soon will the Dataset Retention job delete data from Profile services?

+++Answer
Once a retention policy is set, existing events that already exceed the newly defined TTL are immediately deleted. Newer events remain until their timestamps surpass the retention period.

For example, if you apply a 30-day expiration policy on May 15th, the following occurs:

- New events receive a 30-day expiration as they are ingested.
- Existing events with a timestamp older than April 15th are immediately deleted.
- Existing events with a timestamp after April 15th are set to expire 30 days after their timestamp (for example, an event from April 18th would be deleted on May 18th).
+++ -->

### 我可以為資料湖和設定檔服務設定不同的保留原則嗎？

+++回答
可以，您可以為Data Lake和Profile服務設定不同的保留原則。 設定檔存放區的保留期間可能會短於或長於資料湖保留期間，具體取決於您組織的需求。
+++

### 如何檢查我目前的資料集使用情形？

+++回答
您可以在[!UICONTROL 資料集]詳細目錄工作區中，以個別量度的形式檢查資料湖和設定檔存放區的最新資料集存放大小。 排序欄以識別最大的資料集，並驗證保留原則是否已套用。

如需沙箱層級的使用量，請參閱授權使用量儀表板。 如需詳細資訊，請參閱[授權使用檔案](../../dashboards/guides/license-usage.md)。
+++

### 如何驗證資料保留工作是否成功？

+++回答
您可以在[資料集保留組態UI](./user-guide.md#data-retention-policy)或「資料詳細目錄」頁面中檢查上次資料保留作業的時間戳記，以驗證上次的資料保留作業。

或者，您可以向下列端點發出GET請求：

`GET https://platform.adobe.io/data/foundation/catalog/dataSets/{DATASET_ID}`

回應包含屬性`extensions.adobe_lakeHouse.rowExpiration.lastCompleted`，指出最近一次TTL作業完成時的Unix時間戳記（毫秒）。

歷史資料集使用量報告目前無法使用。
+++

### 我可以復原已刪除的資料嗎？

+++回答
否，一旦套用保留原則，任何超過保留期的資料都會永久刪除且無法復原。
+++

### 我可以在資料湖體驗事件資料集上設定的最低TTL是多少？

+++回答
資料湖體驗事件資料集的最低TTL為30天。 資料湖在初始擷取與處理期間充當處理備份與復原系統。 因此，資料必須在擷取之後在資料湖中保留至少30天，才能過期。
+++

### 如果需要保留某些Data Lake欄位的時間超過TTL原則所允許的時間，該怎麼辦？

+++回答
使用Data Distiller可保留超出資料集TTL的特定欄位，同時保持在您的使用率限制以內。 建立只定期將必要欄位寫入衍生資料集的工作。 此工作流程可確保遵循較短的TTL，同時保留重要資料以供長期使用。

如需詳細資訊，請參閱[使用SQL建立衍生資料集指南](../../query-service/data-distiller/derived-datasets/create-derived-datasets-with-sql.md)。
+++

## 後續步驟 {#next-steps}

現在您已瞭解如何管理列層級到期的TTL設定，請檢閱下列檔案以進一步瞭解TTL管理：

- 保留工作：瞭解如何使用[資料生命週期UI指南](../../hygiene/ui/dataset-expiration.md)，在Experience Platform UI中排程並自動化資料集有效期，或檢查資料集保留設定，以及驗證是否已刪除過期的記錄。
- [資料集過期API端點指南](../../hygiene/api/dataset-expiration.md)：探索如何刪除整個資料集，而不只是刪除資料列。 瞭解如何使用API排程、管理和自動化資料集到期日，以確保有效率的資料保留。
- [資料使用原則概觀](../../data-governance/policies/overview.md)：瞭解如何將您的資料保留策略與更廣泛的法規遵循要求及行銷使用限制保持一致。
