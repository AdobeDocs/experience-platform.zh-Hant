---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: 使用API搭配決策服務執行階段
topic: tutorial
translation-type: tm+mt
source-git-commit: bd9884a24c5301121f30090946ab24d9c394db1b
workflow-type: tm+mt
source-wordcount: '1985'
ht-degree: 0%

---


# 使用API搭配決策服務執行階段

本檔案提供使用Adobe Experience Platform API執行時期服務 [!DNL Decisioning Service] 的教學課程。

## 快速入門

本教學課程需要對決策中涉及的 [!DNL Experience Platform] 服務有深入的瞭解，並決定在客戶體驗期間要呈現的下一個最佳方案。 在開始本教學課程之前，請先閱讀以下檔案：

- [!DNL Decisioning Service](./../home.md): 提供新增和移除選件的架構，以及建立演算法，以在客戶體驗期間選擇最佳呈現。
- [!DNL Experience Data Model (XDM)](../../xdm/home.md): 平台組織客戶體驗資料的標準化架構。
- [!DNL Profile Query Language (PQL)](../../segmentation/pql/overview.md): PQL用於定義規則和篩選器。
- [使用API管理決策物件和規則](./entities.md): 在使用「決策服務」執行階段之前，您必須設定相關實體。

以下章節提供您必須知道的其他資訊，才能成功呼叫 [!DNL Platform] API。

### 讀取範例API呼叫

本教學課程提供範例API呼叫，以示範如何設定請求的格式。 這些包括路徑、必要標題和正確格式化的請求負載。 也提供API回應中傳回的範例JSON。 如需範例API呼叫檔案中所用慣例的詳細資訊，請參閱疑難排解指 [南中有關如何讀取範例API呼叫的](../../landing/troubleshooting.md#how-do-i-format-an-api-request)[!DNL Experience Platform] 章節。

### 收集必要標題的值

若要呼叫API，您必 [!DNL Platform] 須先完成驗證教 [學課程](../../tutorials/authentication.md)。 完成驗證教學課程後，將提供所有 [!DNL Experience Platform] API呼叫中每個必要標題的值，如下所示：

- 授權： 生產者 `{ACCESS_TOKEN}`
- x-api-key: `{API_KEY}`
- x-gw-ims-org-id: `{IMS_ORG}`

中的所有資 [!DNL Experience Platform] 源都與特定虛擬沙盒隔離。 對API的所 [!DNL Platform] 有請求都需要一個標題，該標題會指定要在中執行的操作的沙盒名稱：

- x-sandbox-name: `{SANDBOX_NAME}`

>[!NOTE]
>
>如需中沙盒的詳細資訊 [!DNL Platform]，請參閱沙 [盒概述檔案](../../tutorials/authentication.md)。

所有包含裝載(POST、PUT、PATCH)的請求都需要額外的標題：

- 內容類型： application/json

執行時期要求也需要：

- x-request-id: `{UUID}`

>[!NOTE]
>
>`UUID` 是UUID格式的字串，其全域唯一，且不得重複用於不同的API呼叫

[!DNL Decisioning Service] 由多個彼此相關的業務對象控制。 所有業務對象都儲存在 [!DNL Platform’s] 業務對象儲存庫XDM核心對象儲存庫中。 此儲存庫的一個主要功能是API與業務對象類型正交。 與其使用POST、GET、PUT、PATCH或DELETE API來指出其API端點中的資源類型，只有6個通用端點，但它們接受或返回在需要消除歧義時指示對象類型的參數。 方案必須在儲存庫中註冊，但除此之外，該儲存庫可用於一組開放式對象類型。

所有XDM核心對象儲存庫API的端點路徑以開頭 `https://platform.adobe.io/data/core/ode/`。

端點之後的第一個路徑元素是 `containerId`。 此標識符通過XDM核心對象儲存庫根端點獲得 `GET https://platform.adobe.io/data/core/xcore/`。

## 決策模型的編製

商業邏輯實體的啟動會自動且持續進行。 一旦在儲存庫中保存新選項並將其標籤為「已批准」，它將成為包含該組可用選項的候選選項。 一旦更新決策規則，規則集就會重新組合併準備執行時期。 在此自動啟動步驟中，將評估由商業邏輯定義且不依賴執行時期內容的任何限制。 此啟動步驟的結果會傳送至快取，供執行階段使 [!DNL Decisioning Service] 用。

### 位置、篩選器和生命週期狀態的影響

選件會持續建立，其生命週期狀態會發生變更，否則可能會有新的內容呈現。 活動的選件篩選條件可能會變更，或可能比對或篩選已更新標籤集的選件。 此程式可以公平參與，而應用程式和服務需要知道所產生的活動候選集。 決策執行階段提供活動對選件API，可篩選未核准、不符合選件篩選或沒有活動參考之位置的表示法的選件。

**請求**

```shell
curl -X GET {DECISION_SERVICE_ENDPOINT_PATH}/{CONTAINER_ID}/offers?activityId={ACTIVITY_URI}' \
  -H 'Accept: application/vnd.adobe.xdm+json \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'x-request-id: {NEW_UUID}'
```

**回應**

參數可 `activityId` 以在URL中重複，而且在一個請求中最多可提供30種不同的活動參考。 此回應對於發現任何因設定而出現的意外情況非常有用，如下所示：

```json
{
  "xdm:activityOffers": [
    {
      "xdm:offerActivity": {
        "@id": "{ACTIVITY_URI}",
        "_links": {
          "self": {
            "href": "{repository_endpoint}/{CONTAINER_ID}/instances/{ACTIVITY_INSTANCE_ID}"
          }
        },
        "repo:etag": "1"
      },
      "xdm:offers": [
        {
          "@id": "{OFFER_URI_1}",
          "_links": {
            "self": {
              "href": "{REPOSITORY_ENDPOINT}/{CONTAINER_ID}/instances/{OFFER_INSTANCE_ID_1}"
            }
          },
          "repo:etag": "15"
        },
        {
          "@id": "{OFFER_URI_2}",
          "_links": {
            "self": {
              "href": "{REPOSITORY_ENDPOINT}/{CONTAINER_ID}/instances/{OFFER_INSTANCE_ID_2}"
            }
          },
          "repo:etag": "5"
        }
      ],
      "xdm:fallbackOffer": {
        "@id": "{FALLBACK_URI}",
        "_links": {
          "self": {
            "href": "{REPOSITORY_ENDPOINT}/{CONTAINER_ID}/instances/{FALLBACK_INSTANCE_ID}"
          }
        },
        "repo:etag": "2"
      }
    }
  ]
}
```

在物件更新時間和API回應反映活動與選件對應的時間之間，會有幾秒的延遲。 響應中會給出每個對象的修訂版本，以便客戶端可以檢查是否有對尚未反映的對象的更新。

### 診斷API和疑難排解

活動、選件和資格規則會編譯為決策服務執行階段使用的內部格式（執行階段選件目錄）。 編譯可以檢測在儲存對象和在XDM核心對象儲存庫中建立連結時未被執行的檢查捕獲的錯誤。

提供診斷API以獲取在該步驟中發生的任何編譯錯誤，並且在沒有錯誤的情況下獲取關於上次重新編譯規則和活動的資訊。

**請求**

```shell
curl -X GET {DECISION_SERVICE_ENDPOINT_PATH}/{CONTAINER_ID}/diagnostics \
  -H 'Accept: application/vnd.adobe.xdm+json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'x-request-id: {NEW_UUID}'
```

此API呼叫的唯一參數為 `containerId`。 結果會從所有已修改該容器中決策規則、選件、活動或選件篩選器的用戶端進行所有更新。 在更新物件的時間和編譯完成的時間之間，會有幾秒的延遲。 上次更新時間戳記和任何錯誤都會在回應診斷呼叫時傳回。

**回應**

```json
{
  "xdm:operations": {
    "xdm:offerCatalogUpdate": {
      "xdm:date": "2019-06-19T23:28:44.855Z",
      "xdm:errors": []
    },
    "xdm:activitiesUpdate": {
      "xdm:date": "2019-06-19T23:28:40.114Z",
      "xdm:errors": []
    }
  }
}
```

## 執行決策的REST API呼叫

REST API是在應用程式上執行的路由之一，以根據組織為其使用者設定的規則、模型和限制 [!DNL Platform] ，獲得下一個最佳體驗。 應用程式會傳送描述檔的其中一個身分（描述檔ID和識別名稱空間）, [!DNL Decisioning Service] 以尋找描述檔，並使用資訊來套用商業邏輯。 其他上下文資料可傳遞至請求，如果業務規則中已指定，則會納入資料中以做出決定。

應用程式可一次要求最多30個活動的決策，以取得更佳的效能。 活動的URI會在相同請求中傳遞。 REST API是同步的，如果沒有個人化選項符合限制，則會傳回所有這些活動的建議選項或備援選項。

有可能會有兩種不同的活動提供與其「最佳」相同的選項。 為避免重複合成的體驗，依預設，會 [!DNL Decisioning Service] 在相同請求中參考的活動之間進行仲裁。 仲裁意指，對於每項活動，都會考慮其前N個選項，但在這些活動中，不會多提議一次。 如果兩個活動有相同的排名最前選項，其中一個活動將被選為使用其次優或第三優等。 這些重複資料消除規則嘗試避免任何活動都必須使用其備援選項。

決策請求包含其POST請求主體的參數。 內文的格式為JSON標 `Content-Type` 題值 `application/vnd.adobe.xdm+json; schema="{REQUEST_SCHEMA_AND_VERSION}"`

目前支援的請求架構和版本為 `https://ns.adobe.com/experience/offer-management/decision-request;version=0.9`。 未來將會提供其他請求結構或版本。

**請求**

```shell
curl -X POST {DECISION_SERVICE_ENDPOINT_PATH}/{CONTAINER_ID}/decisions \
  -H 'Accept: application/json, application/problem+json \
  -H '
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'x-request-id: {NEW_UUID}' \
  -d '{
  "xdm:dryRun": {DRY_RUN_TRUE_FALSE},
  "xdm:validateContextData": {VALIDATE_CONTEXT_DATA_TRUE_FALSE},

  "xdm:offerActivities":[
    {
      "xdm:offerActivity": "{ACTIVITY_URI_1}"
    },
  ],
  "xdm:identityMap":{
    "{PROFILE_ID_NAMESPACE_CODE}":[
      {
        "xdm:id":"{PROFILE_ID}"
      }
    ]
  },
  "xdm:profileModel":"{PROFILE_MODEL}",
  "xdm:contextData": [
    {
      "@type": "{CONTEXT_DATASSCHEMA_ID}"
      "xdm:data": { JSON PROPERTIES OF CONTEXT ENTITY }
    }
  ] ,
  "xdm:allowDuplicatePropositions": {
    "xdm:acrossActivities": {DUPLICATE_OFFER_IDS_OF_TRUE_FALSE},
  }
}’
```

- **`xdm:dryRun`** -如果此可選屬性的值設定為true，則決策請求將遵守封閉約束，但實際上不會提取這些計數器，則預期呼叫者絕不會向概要檔案提出建議。 該 [!DNL Decisioning Service] 提案不會記錄為正式的XDM決策事件，也不會出現在報告資料集中。 此屬性的預設值為false，若省略屬性，則不會將決定視為測試執行，因此應向使用者呈現。
- **`xdm:validateContextData`** -此可選屬性可開啟或關閉上下文資料的驗證。 如果啟用了驗證，則對於每個提供的上下文資料項，將從XDM註冊表中提取模式(基於 `@type` 欄位)，並對該對 `xdm:data` 像進行驗證。

此架構的請求包含參照選件活動的URI陣列、描述檔識別和上下文資料項目陣列：

- **`xdm:offerActivities`** -此強制屬性是物件的陣列，每個項目都包含選件活動的相關資料。 選件活動具有下列屬性：
   - **`xdm:offerActivity`** -活動的唯一標識符(URI)。 這是選件活動 `@id` 的屬性值。
- **`xdm:identityMap`** -包含符合XDM架構之JSON物件的必要屬性 `https://ns.adobe.com/xdm/context/identitymap`。 該屬性定義映射，其中鍵是標識命名空間代碼，該值是給定命名空間中最終用戶標識符的清單。 如果是。
- **`xdm:contextData`** -可選屬性，包含對其架構的引用所描述的項目。 陣列中的每個上下文資料項都必須具有以下屬性：
   - **`@type`** -引用此項目中對象的XDM模式的必需屬性。
   - **`xdm:data`** -一個強制屬性，包含屬性中指定的每個XDM架構的對象 `@type` 屬性。

## 決策請求中的動態上下文資料

上節指出如何將XDM物件傳遞至決策請求。 以下是此類上下文物件陣列的範例：

```json
"xdm:contextData": [
  {
    "@type":" https://ns.adobe.com/{TENANT_ID_OF_ORG}/schemas/{NUMERIC_SCHEMA_ID};version=1",
    "xdm:data":{ 
      "{TENANT_ID_OF_ORG}": {
        "productDetails":{ 
          "xdm:gender":      "unisex",
          "xdm:fabrication": "leather",
          "xdm:category":    "wallets",
        }
      }
    }
  }
]
```

架構必須由您的組織構建。 要瞭解如何構建方案，請參閱方案編 [輯器教程](../../xdm/tutorials/create-schema-ui.md)。 您的架構將位於命名空間中 `https://ns.adobe.com/{TENANT_ID}/schemas`。

Schema Registry [API開發人員指南說明如何以程式方式存取結構](../../xdm/tutorials/create-schema-api.md) ，以及開發人員如何取得結構的租用戶ID和數值識別碼。 版本號是必需的，也由架構註冊表API提供。

由組織定義的架構通常具有名為的根屬性 `_{TENANT_ID}`，也稱為租用戶名稱空間字串。
請注意，從全域架構元件(例如_`https://ns.adobe.com/xdm/context/product` )使用的屬性有命名空間首碼 `xdm:`。 在這種情況下，組織定義的屬性 `productDetails` 是使用該資料類型構建的。 當租用戶屬性巢狀內嵌在以租用戶名稱空間命名的屬性中時，可全域使用的資料類型會使用保留首碼 `xdm:` 來避免屬性名稱衝突。

屬性中可列出多個資料 `xdm:contextData` 物件。 每個對象都必須通過屬性標識其 `@type` 類型。
上下文資料對象的值可用於PQL表達式中，例如在資格規則條件中。 上下文資料物件必須透過特殊路徑參考運算式來處理 `@{schemaId}`。 遵循此參考運算式的運算式是可存取資料物件屬性的規則路徑運算式：

```json
{
  "xdm:name": "Eligible for a free gender-specific item of interest",
  "xdm:condition": {
    "xdm:value":
      "gender in (\"female\",\"non-specific\")  
       and (
         select p from
           @{https://ns.adobe.com/{TENANT_ID}/schemas/{NUMERIC_SCHEMA_ID}}._{TENANT_ID}
         select e from xEvent 
            where e.type = \"productSearch\" 
              and e.category = p.category 
              and p.gender in (\"female\",\"unisex\")
       )",
    "xdm:format": "pql/text",
    "xdm:type": "PQL"
  }
}
```

在上述範例中，變 `p` 數會在標有 `@type` =的物件陣列上循環 `https://ns.adobe.com/{TENANT_ID}/schemas/{NUMERIC_SCHEMA_ID}}`。

請注意，PQL語法不在屬性名稱中使用前置詞。 根據預設，全域屬性只會參照而不含 `xdm:` 首碼。 您組織定義的屬性會巢狀內嵌在以租 **戶名稱空間** (在變數所指示的範例中 `{TENANT_ID}`)命名的其他屬性中。 為了能夠直接引用自定義屬性，變數將 `p` 綁定到引用其他嵌套屬性的路徑結果。

## 描述檔記錄的使用

描述檔和體驗事件實體的所有記錄都已在描述檔存放區中管理。 將一或多個描述檔識別碼傳遞至要求，這些識別碼的描述檔就會從商店中識別並查閱。 然後，該資料自動可用於由決策策略評估的決策規則和模型。

若要擷取描述檔和體驗記錄，會套用預設的合併原則。
請注意，在將描述檔記錄上傳至資料 [!DNL Platform] 表後，會有輕微的延遲，直到可以查找描述檔記錄為止。 透過串流API接收描述檔和體驗記錄時也是如此，只要幾秒後，資料才可用於評估決策規則，以評估描述檔和體驗事件資料。