---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: 使用API管理決策服務實體
topic: tutorial
translation-type: tm+mt
source-git-commit: bd9884a24c5301121f30090946ab24d9c394db1b
workflow-type: tm+mt
source-wordcount: '7207'
ht-degree: 0%

---


# 使用API管理決策物件和規則

本檔案提供使用Adobe Experience Platform API的商業實體 [!DNL Decisioning Service] 的教學課程。

本教學課程包含兩個部分：

- 第一部分介紹了用於管理業務對象的通用儲存庫 [API](#managing-repository-entities-using-apis)。 這些API通用性是，它們為任何類型的業務對象提供建立、讀取、更 **新** 、刪除和搜索功能。 介紹了API的一般模型，並說明了它與超文本應用語言(HAL)的關係。

- 第二部分應用有關儲存庫API [的知識](#creating-and-managing-offer-decisioning-entities-using-apis) ，重點介紹通過儲存庫API管理的業務實體。 在套用相同API時，管理活動和業務規則等兩個不同實體之間的唯一差異是請求和回應裝載，以及表示所管理物件類型的必要標題值。

## 快速入門

本教學課程需要有效瞭解服 [!DNL Experience Platform] 務和API慣例。 儲存 [!DNL Platform] 庫是由若干其他服務使用的服務， [!DNL Platform] 用於儲存業務對象和各種類型的元資料。 它提供安全而有彈性的方式來管理和查詢這些物件，以供數種執行時期服務使用。 就 [!DNL Decisioning Service] 是其中之一。 在開始本教學課程之前，請先閱讀以下檔案：

- [!DNL Experience Data Model (XDM)](../../xdm/home.md): 平台組織客戶體驗資料的標準化架構。
- [!DNL Decisioning Service](./../home.md): 說明「體驗決策」的概念和元件，尤其是「選件」決策。 說明在客戶體驗期間，選擇最佳呈現選項的策略。
- [!DNL Profile Query Language (PQL)](../../segmentation/pql/overview.md): PQL是一種功能強大的語言，可編寫XDM實例的表達式。 PQL用於定義決策規則。

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
>如需中沙盒的詳細資訊 [!DNL Platform]，請參閱沙 [盒概述檔案](../../sandboxes/home.md)。

所有包含裝載(POST、PUT、PATCH)的請求都需要額外的標題：

- 內容類型： application/json

## 資料庫API慣例

[!DNL Decisioning Service] 由多個彼此相關的業務對象控制。 所有業務對象都儲存在業務對 [!DNL Platform’s] 像儲存庫中。 此儲存庫的一個主要功能是API與業務對象類型正交。 與其使用POST、GET、PUT、PATCH或DELETE API來指出其API端點中的資源類型，只有6個通用端點，但它們接受或返回在需要消除歧義時指示對象類型的參數。 方案必須在儲存庫中註冊，但除此之外，該儲存庫可用於一組開放式對象類型。

除了上述標題外，用於建立、讀取、更新、刪除和查詢儲存庫對象的API還有以下約定：

- 所有儲存庫API的端點路徑以開頭 `https://platform.adobe.io/data/core/xcore/`。

API裝載格式會以或標 `Accept` 題協 `Content-Type` 商。 {FORMAT}依據 `Accept` 下表的特定儲存 `Content-Type``application/vnd.adobe.platform.xcore.{FORMAT}+json` 庫API請求或響應消息，{FORMAT}的值指示或標題中的消息格式。

| 格式變體 | 請求或回應實體的說明 |
| --- | --- |
| <br>後面跟一個參數 `schema={schemaId}` | 訊息包含JSON結構描述的例項，由格式參數結構描述所指示。 例項會包裝在JSON屬性中 `_instance`。 響應裝載中的其他頂級屬性指定可用於所有資源的儲存庫資訊。  符合HAL格式的消息具有包含HAL `_links` 格式引用的屬性。 |
| `patch.hal` | 訊息包含JSON PATCH裝載，假設要修補的例項符合HAL。 這表示不僅可修補例項本身的例項屬性，也可修補例項的HAL連結。 請注意，用戶端對哪些屬性可以更新有限制。 |
| `home.hal` | 訊息包含儲存庫之首頁檔案資源的JSON格式表示法。 |
| xdm.receipt | 訊息包含建立、更新（完整和修補程式）或刪除作業的JSON格式回應。 接收包含以ETag形式表示實例修訂的控制資料。 |

每個格式變 **體的使用** ，取決於特定的API:

| API | 內容類型標題 | 接受標題 |
| --- | --- | --- |
| 建立例項 <br/>建立容器 | `hal`<br/>with schema參數 | `xdm.receipt` |
| 更新<br/>InstanceUpdate容器 | `hal`<br/>with schema參數 | `xdm.receipt` |
| 修補程式實例 | `patch.hal` | `xdm.receipt` |
| 刪除例<br/>項刪除容器 | 不適用 | `xdm.receipt` |
| Read<br/>InstanceRead Container | 不適用 | `hal` with `schema` parameter |
| 清單例<br/>項清單容器 | 不適用 | `hal` 具有特殊參 `schema` 數 `https://ns.adobe.com/experience/xcore/hal/results` |
| 搜尋例項 | 不適用 | hal含特殊參 `schema` 數 `https://ns.adobe.com/experience/xcore/hal/results` |
| 讀取回購根 | 不適用 | `home.hal` |

對於容器建立、更新和讀取API，格式參數架構具有值 `https://ns.adobe.com/experience/xcore/container`。

`ContainerId` 是例項API的第一個路徑參數。 所有業務實體都位於稱為容器的容器中。 容器是隔離機制，可讓不同的顧慮分開。 資料庫實例API的第一個路徑元素是一般端點後的 `containerId`。 從呼叫者可存取的容器清單中取得識別碼。 例如，在容器中建立例項的API為 `POST https://platform.adobe.io/data/core/xcore/{containerId}/instances`。

可存取容器的清單是透過使用標準標題以HTTP GET請求呼叫儲存庫根端點&quot;/&quot;來取得。

## 管理容器存取

管理員可以將類似的承擔者、資源和存取權限分組至設定檔。 這可減輕管理負擔，而且 [Adobe的Admin Console UI也支援](https://adminconsole.adobe.com)。 您必須是組織中Adobe Experience Platform的產品管理員，才能建立個人檔案並指派使用者。

只要在單次步驟中建立符合特定權限的產品設定檔，然後將使用者新增至這些設定檔即可。 設定檔會當成已授與權限的群組，而該群組中每個實際使用者或技術使用者都會繼承這些權限。

### 列出使用者可存取的容器和整合

當管理員授與一般使用者的容器存取權或整合時，這些容器會顯示在儲存庫的「首頁」清單中。 該清單對於不同的用戶或整合可能不同，因為它是呼叫者可訪問的所有容器的子集。 容器清單可透過其與產品內容的關聯來篩選。 會呼叫篩選參數， `product` 並可加以重複。 如果給出多個產品上下文篩選器，則會傳回與任何給定產品上下文具有關聯的容器的合併。 請注意，單一容器可以關聯至多個產品內容。

容器的上 [!DNL Platform] 下文 [!DNL Decisioning Service] 目前為 `dma_offers`。

>[!NOTE]
>
>我們很快 [!DNL Platform Decisioning Containers] 就會改為 `acp`。 篩選是選用的，但篩選條件僅限篩 `dma_offers` 選條件需要在日後發行時進行編輯。 要準備此更改，客戶端不應使用篩選器，或應用兩個產品上下文作為其篩選器。

**請求**

```shell
curl -X GET {ENDPOINT_PATH}/?product=dma_offers&product=acp \ 
  -H 'Accept: application/vnd.adobe.platform.xcore.home.hal+json' \ 
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \ 
  -H 'x-api-key: {API_KEY}' \ 
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  _H 'x-sandbox-name: {SANDBOX_NAME}' \ 
  -H 'x-request-id: {NEW_UUID}' 
```

**回應**

```json
{ 
    "_embedded": { 
        "https://ns.adobe.com/experience/xcore/container": [ 
            { 
              "instanceId": "82d1f250-85b6-11e9-ac80-99ba4655b277", 
              "schemas": [ 
                "https://ns.adobe.com/experience/xcore/container;version=0.1" 
              ], 
              "productContexts": [ 
                "dma_offers" 
              ], 
              "repo:etag": 1, 
              "repo:createdDate": "2019-06-03T04:17:33.684Z", 
              "repo:lastModifiedDate": "2019-06-03T04:17:33.684Z", 
              "repo:createdBy": "CREATOR_ACCOUNT_ID", 
              "repo:lastModifiedBy": "LAST_UPDATE_ACCOUNT_ID", 
              "repo:createdByClientId": "CLIENT_ID_OR_API_KEY", 
              "repo:lastModifiedByClientId": "CLIENT_ID_OR_API_KEY", 
              "_instance": { 
                "repo:name": "My Organization's container", 
                "dataCenter": "VA7" 
              }, 
              "_links": { 
                "self": { 
                  "href": "/containers/82d1f250-85b6-11e9-ac80-99ba4655b277" 
                } 
              } 
            } 
        ] 
    }, 
    "_links": { 
        "self": { 
            "href": "/"  
        } 
    } 
}  
```

請注意 `instanceId` 結果項目中列出的項目。 它用作API中 `containerId` 的參數，以讀取和控制一般商業物件。

根據用戶的訪問權限，清單已被過濾，但可以通過屬性查詢進一步過濾。

## 管理實體的一般API

### 建立例項

用於在儲存庫中建立新實例的API採用 `containerId` 路徑參數，並使用方案參數標識標題中 `Content-Type` 的實例類型。

實例屬性是在屬性包裝的裝載中 `_instance` 提供。 例項屬性必須對具有指定結構描述識別碼的JSON結構描述有效。

HAL屬 `_links` 性必須存在，但可以為空。 這表示未定義此例項的自訂連結。

**請求**

```shell
curl -X POST {ENDPOINT_PATH}/{CONTAINER_ID}/instances \ 
  -H 'Content-Type: application/vnd.adobe.platform.xcore.hal+json; schema="{SCHEMA_ID}"' \  
  -H 'Accept: application/vnd.adobe.platform.xcore.xdm.receipt+json \ 
  -H 'x-api-key: {API_KEY}' \ 
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  _H 'x-sandbox-name: {SANDBOX_NAME}' \ 
  -H 'x-request-id: {NEW_UUID}' \ 
  -d '{ 
    "_instance": { 
        {JSON_PAYLOAD} 
    }, 
    "_links": { 
    } 
}' 
```

**回應**

```json
{ 
  "instanceId": "3684ceb0-8744-11e9-a989-89f60b24f6cc", 
  "@id": "GENERATED_URI", 
  "repo:etag": 1, 
  "repo:createdDate": "2019-06-05T03:44:25.343Z", 
  "repo:lastModifiedDate": "2019-06-05T03:44:25.343Z", 
  "repo:createdBy": "YOUR_TECHNICAL_ACCOUNT_ID", 
  "repo:lastModifiedBy": "YOUR_TECHNICAL_ACCOUNT_ID", 
  "repo:createdByClientId": "YOUR_API_KEY", 
  "repo:lastModifiedByClientId": "YOUR_API_KEY" 
}
```

回應包含剛建立之物件的instanceId。 此instanceId是不可變的，始終由儲存庫指派，並且全局唯一。 該值用作物理標識符。

此外，如果模式具有此類屬性，則在響應負載 `@id` 的屬性中返回通用資源標識符(URI)。 每個實例都應具有一個用作實例的URI和主鍵的屬性。 此識別碼被其他例項用來與新例項建立關係，包括跨不同類型。 在當前版本中，URI由儲存庫生成並包含在屬 `@id` 性中。 未來版本可能會放鬆此規則，並允許客戶管理自己的URI值，並為包含該值的屬性命名。

請注意，這些URI不是URL，無法提供直接擷取資源的方式。 為了指出這一點，URI的前置詞為不指定檢索協定的URI方案。 但是，URI可用來查閱具有查詢的例項。

REST回應會有一個「位置」標題，其中包含URL元件，可用來擷取剛建立的例項。 此元件是相對URI引用，需要應用於儲存庫的基本URI。 基本URI會在標題中傳 `Content-Base` 回。

屬 `repo:etag` 性指定實例的修訂。 此值可用於更新操作，以強制一致性。 HTTP標題可 `If-Match` 用來新增條件至PUT或PATCH API呼叫，以確保不會意外覆寫例項的其他變更。 每次 `repo:etag` 建立、讀取、更新、刪除和查詢呼叫時都會傳回值。 該值用作標頭中的值， ` If-Match` 根據 [RFC7232第3.1節](https://tools.ietf.org/html/rfc7232#section-3.1)。

其餘屬性會指出使用哪些帳戶和API金鑰來建立和上次修改例項。 由於此呼叫建立了例項，因此各自的值是請求的值。

### 依ID查閱例項

使用「建立」呼叫傳回之「位置」標題中的URL，應用程式就可以尋找例項。

**請求**

```shell
curl -X GET {ENDPOINT_PATH}/{CONTAINER_ID}/instances/{INSTANCE_ID} \ 
  -H 'Accept: *, application/vnd.adobe.platform.xcore.hal+json; schema="{SCHEMA_ID}" \ 
  -H 'x-api-key: {API_KEY}' \ 
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  _H 'x-sandbox-name: {SANDBOX_NAME}' \ 
  -H 'x-request-id: {NEW_UUID}'  
```

>[!NOTE]
>
>雖然應 `instanceId` 用程式會以路徑參數的形式提供，但應盡可能不要自行建立路徑，而應依循清單和搜尋作業所包含之例項的連結。 如需詳‎細資訊，請參閱‎6.4.4和6.4.6節。

**回應**

```json
{ 
  "instanceId": "ID_OF_THIS_INSTANCE", 
  "schemas": [ 
    "SCHEMA_ID_OF_INSTANCE" 
  ], 
  "repo:etag": 1, 
  "repo:createdDate": "2019-03-24T15:52:12.725Z", 
  "repo:lastModifiedDate": "2019-03-24T15:52:12.725Z", 
  "repo:createdBy": "CREATOR_ACCOUNT_ID", 
  "repo:lastModifiedBy": "LAST_UPDATE_ACCOUNT_ID", 
  "_instance": { 
    JSON_PROPERTIES_OF_THIS_INSTANCE 
  }, 
  "_links": { 
    "self": { 
      "name": "GENERATED_UNIQUE_LINK_NAME", 
      "href": "RELATIVE_URL_TO_INSTANCE" 
    } 
  } 
} 
```

例項的JSON屬性會包裝在屬性中，而其 `_instance` 他根層級屬性則包含例項的中繼資料。

資源也包含JSON結構描述ID的陣列。 此陣列指出此例項已驗證的JSON結構描述。

每個實例都包含與IANA註冊的自關係(如 [RFC5988所定義])相對應的關係類型自關的HAL連結。

**測試實例的較新修訂版本**

執行個 `eTag` 體的目前值會隨回應傳回，可讓用戶端針對執行個體發出條件式作業，以避免再次擷取相同的資源狀態，或避免覆寫稍後修訂版本的值，而不需用戶端知道。

查閱API可讓用戶端指定標 `If-None-Match` 頭參數。 請參閱此標準HTTP參數 [RFC2616的定義]。 用戶端指定的實體標籤值是它從更新、讀取、列出或搜尋API呼叫中，以最新回應接收的值。 請注意， `etag` 值應不透明於用戶端，且必須以字串的形式提供，並以引號括住。

**請求**

```shell
curl -X GET {ENDPOINT_PATH}/{CONTAINER_ID}/instances/{INSTANCE_ID} \ 
  -H 'Accept: *, application/vnd.adobe.platform.xcore.hal+json; schema="{SCHEMA_ID}" \ 
  -H 'If-None-Match: "{LAST_RECEIVED_ETAG}" \ 
  -H 'x-api-key: {API_KEY}' \ 
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  _H 'x-sandbox-name: {SANDBOX_NAME}' \ 
  -H 'x-request-id: {NEW_UUID}'  
```

當執行個體的上一個修訂版本是具有給定etag的修訂版本時，儲存庫API會以狀態304 Not Modified回應。

### 方案的清單實例——排序和分頁

用戶端將無法追蹤所建立的例項，因此無法透過其實體instanceId來存取。 使用讀取實例API將是例外。 客戶也不知道其他客戶已建立哪些實例。

更典型的存取模式是透過所有例項集進行頁面存取。

**請求**

```shell
curl -X GET {ENDPOINT_PATH}/{CONTAINER_ID}/instances?schema="{SCHEMA_ID}" \ 
  -H 'Accept: *, application/vnd.adobe.platform.xcore.hal+json; schema="https://ns.adobe.com/experience/xcore/hal/results" \ 
  -H 'x-api-key: {API_KEY}' \ 
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  _H 'x-sandbox-name: {SANDBOX_NAME}' \ 
  -H 'x-request-id: {NEW_UUID}'  
```

**回應**

回應取決於指定 `{schemaId}` 的。 例如，「https<span></span>://ns.adobe.com/experience/offer-management/offer-activity&amp;id=xcore:offer-activity:fa24f9e8fc15c73」的回應類似下列。

```json
{
"requestTime": "2019-06-28T06:54:05.606Z",
"_embedded": {
  "results": [],
  "total": 0,
  "count": 0
  },
  "_links": {
  "self": {
  "href": "/653da250-71b8-11e9-a3fe-9b1d0913f3ed/instances?schema=https://ns.adobe.com/experience/offer-management/offer-activity&id=xcore:offer-activity:fa24f9e8fc15c73",
"@type": "https://ns.adobe.com/experience/xcore/hal/results"
  }
  },
  "containerId": "653da250-71b8-11e9-a3fe-9b1d0913f3ed",
  "schemaNs": "https://ns.adobe.com/experience/offer-management/offer-activity;version=0.1"
}
```

>[!NOTE]
>
>結果包含給定方案或此清單第一頁的實例。 請注意，例項可以符合多個架構，因此可以出現在多個清單中。

頁面資源是瞬時的，是唯讀的； 無法更新或刪除。 該尋呼模型在延長的時間段內提供對大型清單子集的隨機訪問，而不維護任何每個客戶端狀態。

若要以此方式依頁面存取例項清單，必須能夠針對該例項清單列舉的項目定義穩定排序。 請注意，「穩定」並不表示例項會出現在預定頁面中。 事實上，當依據屬性P排序例項而形成頁面順序，且用戶端更新此屬性P時，另一用戶端可能會在透過清單分頁時在不同頁面上再次到達此例項。 換句話說，模型傾向於返回更新的結果。

但是，當排序順序基於不可修改的屬性時，「穩定」排序順序保證將到達在尋呼操作開始時存在的所有實例（除非它們在到達其尋呼時被刪除）。 當此排序順序位於單調增加的屬性上時，則也會到達在分頁操作開始後建立的例項。

客戶端可以提供其所需頁面大小的提示，但完全由儲存庫提供一個或多個實例以返回頁面。 為保證訂單穩定，服務必須從頁面中新增或移除項目，以便排序屬性的值在不同頁面邊界上不同。 如此，下一頁就不會再包含最後一頁的某些項目，或在最壞情況下，每個頁面上的相同項目會卡住。

分頁由下列參數控制：

- **`orderBy`**: 包含以逗號分隔、排序的屬性清單，依此清單排序例項清單。 第一個屬性用於主排序，第二個屬性用於解析主排序中的連結，依此類推。 當指定每個例項具有唯一值的屬性時，就不可能建立系結，而且每個項目之後都可能出現分頁符。 屬性的名稱可以前置詞有 `+` 以表示升序或 `-` 表示該屬性的降序。 如果屬性名稱未預先修正，則結果會依遞增順序排序。 如果 `orderBy` 未在請求中指定，則儲存庫將改用物理instanceId屬性。
- **`start`**: 客戶端使用start參數定義要檢索的頁。 開始參數會決定所要頁面的開始。 回應將包含以屬性值嚴格大於( `orderBy` 對於升序)或嚴格小於（對於降序）指定值的例項開始的例項。 未指定查詢參數時，它預設為在第一個可能的例項識別碼之前排序的instanceId值，因此，此值會從第一頁中忽略。
- **`limit`**: 指定正整數作為提示，指出指定請求應傳回的項目數上限。 實際響應尺寸可以更小或更大，因為受提供起動參數可靠操作的需要的限制

### 篩選清單

篩選清單結果是可能的，且與分頁機制無關。 篩選器只需略過清單順序中的例項，或明確要求僅包含滿足特定條件的例項。 客戶端可以請求屬性表達式作為篩選器，也可以指定URI清單作為實例的主鍵值。

- **`property`**: 包含屬性名稱路徑，後面接著比較運算子，後面接著值。 <br/>
傳回的例項清單包含運算式評估為true的例項。 例如，假設例項具有裝載屬性， `status` 且可能的值為 `draft`, `approved`則查詢參數只 `archived``deleted``property=_instance.status==approved` 會傳回已核准狀態的例項。 <br/>



**`id`**: 有時，清單需要依例項的URI來篩選。 查 `property` 詢參數可用來篩選一個例項，但若要取得多個例項，則可向請求提供URI清單。 參 `id` 數會重複，每個出現項都指定一個URI值， `id={URI_1}&id={URI_2},…` URI值必須經過URL編碼。`!=``<``~``~`****`cars``.*cars.*``.*``cars``~`<br/><br/>`property=repo:lastModifiedDate>=2019-02-23T16:30:00.000Z`<br/><br/>`property`<br/><br/>

- 分頁結果將作為特殊的mime類型返回 `application/vnd.adobe.platform.xcore.hal+json; schema="https://ns.adobe.com/experience/xcore/hal/results"`。`property``id``id={URI_1}&id={URI_2},…`

**請求**

**回應**

```shell
curl -X GET {ENDPOINT_PATH}/{CONTAINER_ID}/instances?schema="{SCHEMA_ID}"&orderby${ORDER_BY_PROPERTY_PATH}&property={TIMESTAMP_PROPERTY_PATH}>=2019-02-19T03:19:03.627Z&property${TIMESTAMP_PROPERTY_PATH}<=2019-06-19T03:19:03.627Z \ 
  -H 'Accept: *, application/vnd.adobe.platform.xcore.hal+json; schema="https://ns.adobe.com/experience/xcore/hal/results" \ 
  -H 'x-api-key: {API_KEY}' \ 
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  _H 'x-sandbox-name: {SANDBOX_NAME}' \ 
  -H 'x-request-id: {NEW_UUID}'  
```

**回應包含JSON屬性結果內的結果項目清單，旁邊是兩個屬性，這些屬性會指出此頁面上的結果數目，以及篩選清單中從剛傳回的頁面開始的項目總數。**

```json
{ 
  "requestTime": "2019-06-10T22:12:13.642Z", 
  "_embedded": { 
    "results": [ 
      { 
        "instanceId": "ID_OF_THIS_INSTANCE", 
        "schemas": [ 
          "SCHEMA_ID_OF_INSTANCE" 
        ], 
        "repo:etag": 1, 
        "repo:createdDate": "2019-04-19T03:19:03.627Z", 
        "repo:lastModifiedDate": "2019-04-19T03:19:03.627Z", 
        "repo:createdBy": "CREATOR_ACCOUNT_ID", 
        "repo:lastModifiedBy": "LAST_UPDATE_ACCOUNT_ID", 
        "_instance": { 
          JSON_PROPERTIES_OF_THIS_INSTANCE 
        }, 
        "_links": { 
          "self": { 
            "name": "GENERATED_UNIQUE_LINK_NAME", 
            "href": "RELATIVE_URL_TO_INSTANCE" 
          } 
        } 
      }, 
      { 
        "instanceId": "ID_OF_THIS_INSTANCE", 
        "schemas": [ 
          "SCHEMA_ID_OF_INSTANCE" 
        ], 
        "repo:etag": 1, 
        "repo:createdDate": "2019-04-19T20:30:31.361Z", 
        "repo:lastModifiedDate": "2019-04-19T20:30:31.361Z", 
        "repo:createdBy": "CREATOR_ACCOUNT_ID", 
        "repo:lastModifiedBy": "LAST_UPDATE_ACCOUNT_ID", 
        "_instance": { 
          JSON_PROPERTIES_OF_THIS_INSTANCE 
        }, 

        "_links": { 
          "self": { 
            "name": "GENERATED_UNIQUE_LINK_NAME", 
            "href": "RELATIVE_URL_TO_INSTANCE" 
          } 
        } 
      } 
    ], 
    "total": 2, 
    "count": 2 
  }, 
  "_links": { 
    "self": { 
      "href": "RELATIVE_URL_TO_THIS_RESULT" 
    } 
  }, 
  "containerId": "CONTAINER_ID_OF_THIS_LIST", 
  "schemaNs": "SCHEMA_ID_OF_INSTANCE_LIST" 
} 
```

全文搜尋與結構化查詢

### 如果客戶希望根據字串屬性中包含的術語提供更複雜的篩選條件和搜索實例，儲存庫會提供更強大的搜索API。

**請求**

**除了清單API中的分頁和篩選參數外，此API還允許客戶新增全文和布林查詢參數。**

```shell
curl -X GET {ENDPOINT_PATH}/{CONTAINER_ID}/queries/core/search?schema="{SCHEMA_ID}"&… \ 
  -H 'Accept: *, application/vnd.adobe.platform.xcore.hal+json; schema="https://ns.adobe.com/experience/xcore/hal/results" \ 
  -H 'x-api-key: {API_KEY}' \ 
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  _H 'x-sandbox-name: {SANDBOX_NAME}' \ 
  -H 'x-request-id: {NEW_UUID}'  
```

<!-- TODO: needs example response -->

全文搜尋由下列參數控制：

**`q`**: 包含以空格分隔的無序詞語清單，這些詞語在與例項的任何字串屬性相符之前，先加以標準化。 字串屬性會針對詞語進行分析，而且這些詞語也會標準化。 搜尋查詢會嘗試比對參數中指定的一或多個詞 `q` 語。 字元+、-、=和&amp;、 ||, >, &lt;,!,(,), {, }, [,],^, &quot;, ~, *, ?, :, /對於確定查詢字串中的字詞邊界有特殊含義，當出現在應與字元匹配的標籤中時，應使用反斜線進行逸出。 查詢字串可以用雙引號括住，以取得精確的字串比對，並逸出特殊字元。

- **`field`**: 如果搜尋詞只應與屬性的子集相符，則欄位參數可指出該屬性的路徑。 可以重複此參數，以指出應該與之匹配的多個屬性。`q`[]
- **`qop`**: 包含用於修改搜索的匹配行為的控制參數。 當參數設為且所有搜尋詞必須相符時，當參數不存在或其值設為或任一詞語可計算相符時。
- **`qop`**更新和修補實例

### 若要更新例項，用戶端可以一次覆寫完整的屬性清單，或使用JSON PATCH請求來控制個別屬性值，包括清單。

在這兩種情況下，請求的URL都會指定實體例項的路徑，在這兩種情況下，回應都會是JSON收據裝載，就像建立作業傳回 [的一樣](#create-instances)。 用戶端最好應使用 `Location` 其從先前此物件的API呼叫所收到的標頭或HAL連結，作為此API的完整URL路徑。 如果不可能，客戶端可以從和構建 `containerId` URL `instanceId`。

**請求** (PUT)`Location``containerId``instanceId`

**請求** （修補程式）

```shell
curl -X PUT {ENDPOINT_PATH}/{CONTAINER_ID}/instances/{INSTANCE_ID} \ 
  -H 'Content-Type: application/vnd.adobe.platform.xcore.hal+json; schema="{SCHEMA_ID}"' \  
  -H 'Accept: application/vnd.adobe.platform.xcore.xdm.receipt+json \ 
  -H 'x-api-key: {API_KEY}' \ 
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  _H 'x-sandbox-name: {SANDBOX_NAME}' \ 
  -H 'x-request-id: {NEW_UUID}'\ 
  -d '{ 
  "_instance": { 
    {JSON_PROPERTIES_OF_THIS_INSTANCE} 
  }, 
  "_links": { 
    {HAL_LINKS_OF_THIS_INSTANCE} 
  } 
}'  
```

**PATCH請求會應用這些指示，然後根據模式和與PUT請求相同的實體和參照完整性規則驗證生成的實體。**

```shell
curl -X PATCH {ENDPOINT_PATH}/{CONTAINER_ID}/instances/{INSTANCE_ID} \ 
  -H 'Content-Type: application/vnd.adobe.platform.xcore.patch.hal+json; schema="{SCHEMA_ID}"' \  
  -H 'Accept: application/vnd.adobe.platform.xcore.xdm.receipt+json \ 
  -H 'x-api-key: {API_KEY}' \ 
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  _H 'x-sandbox-name: {SANDBOX_NAME}' \ 
  -H 'x-request-id: {NEW_UUID}' \ 
  -d '[ 
  { 
    {JSON_PATCH_INSTRUCTIONS_FOR_THIS_INSTANCE} 
  } 
]'
```

**控制屬性值編輯**

**您可以使用下列註解，防止在建立和／或更新時設定屬性：**

**`"meta:usereditable"`**: 布爾值——當請求源自使用者代理（以使用者或技術帳戶存取Token來識別呼叫者）時，註解為的屬性不 `"meta:usereditable": false` 應出現在裝載中。 如果是，則它們不得具有與當前設定的值不同的值。 如果值不同，則更新請求或修補程式請求將被拒絕，狀態為422「不可處理實體」。

- **`"meta:immutable"`**: Boolean —— 設定注釋後， `"meta:immutable": true` 不能更改這些屬性。 這適用於來自使用者、技術帳戶整合或特殊服務的要求。
- **測試並行更新**`"meta:immutable": true`

有些情況下，多個客戶端嘗試並行更新實例。 該儲存庫在計算節點群集上操作，而不需要集中事務管理。 為避免一個客戶端同時寫入另一個客戶端編寫的實例，客戶端可以使用條件更新或修補程式請求。 通過在頭 `etag` 部指定字 `If-Match` 符串，儲存庫確保只有第一個請求成功，而使用相同值的其他客戶機的後續請求 `etag` 將失敗。 值隨 `etag` 著實例的每次修改而改變。 客戶端必須檢索實例以獲取最新 `etag` 值，然後，在嘗試更新的眾多客戶中，只有一個客戶端能夠使用該值成功。 其他客戶會收到409衝突訊息。

刪除例項`etag``If-Match``etag``etag``etag`

### 可以使用DELETE調用刪除實例。 用戶端最好將其 `Location` 從先前API呼叫中收到的標題或HAL連結當做完整的URL路徑。 如果不可能，客戶端可以從和物理 `containerId` 構造URL `instanceId`。

**請求**`instanceId`

**回應**

```shell
curl -X DELETE {ENDPOINT_PATH}/{CONTAINER_ID}/instances/{INSTANCE_ID} \ 
  -H 'Accept: application/vnd.adobe.platform.xcore.xdm.receipt+json \ 
  -H 'x-api-key: {API_KEY}' \ 
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  _H 'x-sandbox-name: {SANDBOX_NAME}' \ 
  -H 'x-request-id: {NEW_UUID}'  
```

在收到刪除請求時，儲存庫會檢查是否有任何其他實例（包括任何方案）仍引用要刪除的實例。 在分佈式、高可用性系統中，不能立即檢查參照完整性。 當定義了外鍵關係時，將非同步執行檢查。 這會導致對刪除請求結果的回應稍微延遲。 當執行這些檢查時，立即響應包括狀態202已接受和連結，用於檢查標題中刪除操作的結 `Location` 果。 然後，客戶應檢查該連結以取得結果。**

```json
{ 
  "instanceId": "3684ceb0-8744-11e9-a989-89f60b24f6cc", 
  "@id": "INSTANCE_URI", 
  "repo:etag": 1, 
  "repo:createdDate": "2019-06-05T03:44:25.343Z", 
  "repo:lastModifiedDate": "2019-06-05T03:44:25.343Z", 
  "repo:createdBy": "CREATOR_ACCOUNT_ID", 
  "repo:lastModifiedBy": "YOUR_TECHNICAL_ACCOUNT_ID", 
  "repo:createdByClientId": "CREATOR_API_KEY", 
  "repo:lastModifiedByClientId": "YOUR_API_KEY" 
} 
```

如果發現某個實例引用了要刪除的實例，則結果是刪除操作的拒絕。 如果未發現其他外鍵引用，則完成刪除。 如果結果尚未決定，則回應會指出在202年接受的另一個回應中，標題相同，並 `Location` 會要求客戶繼續檢查。 確定結果後，響應將指示狀態為200正確且響應的有效負載將包含原始刪除請求的結果。 請注意，200 Ok回應僅表示已知結果，回應主體將包含確認或拒絕刪除請求。

建立選件及其子元件`Location`

## 上節所述的API統一套用至所有類型的商業物件。 建立選件和活動之間的唯一差異，是標 `content-type` 題會注明JSON結構描述為符合結構描述之請求的JSON裝載。 因此，以下幾節只需關注這些方案及其之間的關係。

當使用內容類型的API `application/vnd.adobe.platform.xcore.hal+json; schema="{SCHEMA_ID}"`時，例項本身的屬性會內嵌 `_instance` 在有屬性的屬性中 `_links` 。 此格式將是所有實例的一般格式：

[!NOTE]`_instance``_links`

```json
{ 
  … ENVELOPE PROPERTIES 
  "_instance": { 
    INSTANCE PROPERTIES 
  }, 
  "_links": {
    HAL PROPERTIES 
  } 
}
```

>[!NOTE]為簡單起見，在所有JSON片段中，只會說明例項屬性，而且只有在需要時才會顯示封套屬性和_links區段。
>
>一般選件屬性

### 選件是一種決策選項，選件的JSON結構描述會繼承每個選項例項將擁有的標準選項屬性。

**`@id`** -每個選項的唯一標識符，它是主鍵，用於從其他對象引用該選項。 當建立實例時，將分配此屬性，該屬性是不可變的，且不可編輯。

- **`xdm:name`** -每個選項都有一個用於搜索和顯示的名稱。 名稱不是不可變的，不能用於唯一標識實例。 名稱可自由選取，但應在選件例項間具有唯一性。
- 如需 [完整的cURL語法](#updating-and-patching-instances) ，請參閱更新和修補例項。 參數 `schemaId` 必須是 `https://ns.adobe.com/experience/offer-management/personalized-offer` ，或 `https://ns.adobe.com/experience/offer-management/fallback-offer` 如果選件是後援選件。

```json
{ 
  "@id": "INSTANCE_URI",                         // meta:immutable=true, meta:usereditable=false 
  "xdm:name": "A name for the Decision Option",  // meta:immutable=false 
  "xdm:characteristics": { 
    properties specific to this instance         // property names can vary per instance 
  } 
}
```

每個選件例項都可以有一組選擇性屬性，這些屬性僅代表該例項。 不同選件可針對這些屬性使用不同的索引鍵，但值必須是字串。 這些屬性可用於決策和分段規則。 您也可以存取這些內容，以匯整決定的體驗，進一步自訂訊息。[](#updating-and-patching-instances)`schemaId``https://ns.adobe.com/experience/offer-management/personalized-offer``https://ns.adobe.com/experience/offer-management/fallback-offer`

優惠生命週期

### 有一個簡單的狀態轉換流，所有選項都將遵循。 他們從草案狀態開始，等他們準備好時，他們的狀態將設為批准。 當其結束日期過後，可將其移入封存狀態。 在該狀態下，通過將它們再次移入起草狀態，可以刪除或重複使用它們。

![](../images/entities/offer-lifecycle.png)

**`xdm:status`** -此屬性用於實例的生命週期管理。 此值代表工作流程狀態，用來指出選件是否仍在建置中（值=草稿）、執行階段通常可考慮（值=核准），或是不應再使用（值=封存）。

- 對實例執行簡單的PATCH操作通常用於僅操縱屬 `xdm:status` 性：

如需 [完整的cURL語法](#updating-and-patching-instances) ，請參閱更新和修補例項。 參數 `schemaId` 必須是 `https://ns.adobe.com/experience/offer-management/personalized-offer` ，或 `https://ns.adobe.com/experience/offer-management/fallback-offer` 如果選件是後援選件。

```json
[
  {
    "op":    "replace",
    "path":  "/_instance/xdm:status",
    "value": "approved" 
  }
]
```

表示和位置[](#updating-and-patching-instances)`schemaId``https://ns.adobe.com/experience/offer-management/personalized-offer``https://ns.adobe.com/experience/offer-management/fallback-offer`

### 選件是具有內容表示的決策選項。 當做出決定時，會選擇該選項，並使用其識別碼來取得需要提供之位置的內容或內容參考。 選件可以有多個表示法，但每個表示法都需要有不同的放置參照。 這可確保在給定位置時，可以明確確定表示。
在決策操作期間，與活動對象一起確定放置。 沒有以該位置作為參照的表示法的選件會自動從選擇清單中移除。

在將表示法新增至選件之前，放置例項必須存在。 這些例項會建立結構識別碼`https://ns.adobe.com/experience/offer-management/offer-placement`。

如需 [完整的cURL語法](#updating-and-patching-instances) ，請參閱更新和修補例項。 參數 `schemaId` 必須是 `https://ns.adobe.com/experience/offer-management/personalized-offer` ，或 `https://ns.adobe.com/experience/offer-management/fallback-offer` 如果選件是後援選件。

```json
{
  "xdm:name": "Kiosk Placement 1",
  "xdm:channel": "https://ns.adobe.com/xdm/channels/web",
  "xdm:componentType": 
     "https://ns.adobe.com/experience/offer-management/content-component-imagelink",
  "xdm:contentTypes": [
    "image/png", "image/png"
  ],
  "xdm:description": "Generic placeholder for offers in the Kiosk application. \nTechnical constraints: max width 530dpi, min width 480 dpi, aspect ratio 12:5. \nStylistic constraints: single background color with text block in complementary colors, \nNo magenta, please!"
} 
```

Placement **實例** 可具有以下屬性：`schemaId``https://ns.adobe.com/experience/offer-management/personalized-offer``https://ns.adobe.com/experience/offer-management/fallback-offer`

**`xdm:name`** -包含指定的位置名稱，以在人機互動和使用者介面中參照。**

- **`xdm:description`** -用於傳達在整體訊息傳遞中如何使用此位置內容的人類可讀意圖。 當傳送渠道定義新位置時，他們可以在此屬性中新增更多資訊，讓內容建立者可以據以建立或選擇內容。 這些指令不會正式解釋或執行。 這處房產只是表達意圖的場所。
- **`xdm:channel`** -渠道的URI。 頻道指出動態內容的傳送位置。 渠道限制不僅用於傳達將使用選件的位置，還用於判斷用於體驗的內容編輯器或驗證器。
- **`xdm:componentType`** -模型標識符，即URI，用於可在此位置描述的位置中顯示的內容。 元件類型包括： 影像連結、html或純文字。 每個元件類型可能暗示內容項目可能具有的一組特定屬性（模型）。 可以擴展元件類型清單。 有三個預先定義的元件類型值：
- `https://ns.adobe.com/experience/offer-management/content-component-imagelink`
   - `https://ns.adobe.com/experience/offer-management/content-component-text`
   - `https://ns.adobe.com/experience/offer-management/content-component-html`
   - **`xdm:contentTypes`**，此位置中預期元件的介質類型的約束。 一種元件類型（例如不同的影像格式）可能有多種媒體類型。
- **選件中** ，表示項目在陣列屬性中具有物件結構 `xdm:representations`。 每個項目都可以有下列屬性：

**`xdm:placement`** -此屬性包含對放置實例的引用。 當表示法新增至選件時，會檢查該值。 具有該URI的位置實例必須存在，且不能標籤為已刪除。 此外，還會執行檢查，以確保選件實例的放置參考值沒有兩個具有相同值的表示法。**`xdm:representations`

- **`xdm:components`** -內容元件是與特定選件表示法相關聯的片段。 這些片段稍後會用來構成使用者體驗。 請注意，決策服務本身並不構成完整的使用者體驗。 以下屬性是每個元件模型的一部分。
- **`@type`** -此屬性標識元件類型。 這個概念的另一個名稱是內容片段模型。 組 `@type` 件只是由組合最終用戶體驗的應用程式或服務定義的模型的URI。
   - **`repo:id`** -此屬性包含儲存資產的儲存庫中元件的主資源的全局唯一、不可變的標識符。`@type`
   - **`repo:name`** -此屬性包含儲存庫中資產的人工可讀名稱。 此名稱是用戶定義的，不保證是唯一的。
   - **`repo:resolveURL`** -此屬性包含一個唯一的資源定位器，用於讀取內容儲存庫中的資產。 這樣，在用戶端不瞭解要呼叫的API的情況下，取得資產會更輕鬆。 URL會傳回資產主要資源的位元組。
   - **`dc:format`** -此屬性來自Dublin Core Metadata Initiative。 該格式可用於確定顯示或操作該資源所需的軟體、硬體或其它設備。 建議的最佳實務是從受控辭彙中選取值（例如定義電腦媒體格式的網際網路媒體類型清單）。
   - **`dc:language`** -此屬性包含資源的語言或語言。 語言在IETF RFC 3066中定義的語言代碼中指定。
   - 屬性中表示了三種預定義的元件 `@type` 類型：

https<span></span>://ns.adobe.com/experience/offer-management/content-component-imagelink

- https<span></span>://ns.adobe.com/experience/offer-management/content-component-text
- https<span></span>://ns.adobe.com/experience/offer-management/content-component-html
- 視屬性的值而定， `@type` 將包 `xdm:components` 含其他屬性：

**`xdm:linkURL`** -當元件為影像連結時顯示。 此屬性將包含與影像關聯的連結，當使 `user-agent` 用者與選件內容互動時，該連結將導覽至該連結。`xdm:components`

- **`xdm:copyline`** -當元件是文本時使用。 除了參照文字資產（例如，對於可包含格式的長篇文字選件）外，短文字字串也可以直接儲存在xdm:copyline屬性中。`user-agent`
- **`xdm:copyline`**用戶端可以使用其他屬性來設定和評估上下文處理指示。 例如，「選件UI程式庫」用戶端會新增下列選用屬性，以更輕鬆地處理顯示：

在陣列中的每個項 `xdm:components` 目內，選件程式庫UI用戶端會新增下列屬性。 如果不瞭解對UI的影響，則不應刪除或處理這些屬性：

- **`offerui:previewThumbnail`** -此為選用屬性，選件程式庫UI會用來顯示資產的轉譯。 此轉譯與資產本身不同。 例如，內容可以是HTML，而轉譯是點陣圖影像，只顯示其近似值。 此（低品質）轉譯會顯示在選件的呈現區塊中。
   - **`offerui:previewThumbnail`**選件實例上的PATCH操作示例說明如何操作表示法：

如需 [完整的cURL語法](#updating-and-patching-instances) ，請參閱更新和修補例項。 參數 `schemaId` 必須是 `https://ns.adobe.com/experience/offer-management/personalized-offer` ，或 `https://ns.adobe.com/experience/offer-management/fallback-offer` 如果選件是後援選件。

```json
[
  {
    "op":    "add",
    "path":  "/_instance/xdm:representations/-",
    "value": {
      "xdm:placement": "xcore:offer-placement:e51944a87919861",
      "xdm:components": [
        {
          "xdm:copyline": "Get what you want!",
          "@type": "https://ns.adobe.com/experience/offer-management/content-component-text",
          "dc:format": "text/plain"
        }
      ]
    } 
  }
]' 
```

當尚未有屬性時，PATCH操作可能 `xdm:representations` 失敗。 在這種情況下，上述添加操作前面可能有一個建立陣列的添加操作， `xdm:representations` 或者單個添加操作直接設定陣列。
描述的結構和屬性用於所有選件類型、個人化選件以及備援選件。 以下兩節說明個人化選件各方面的限制與決策規則。`schemaId``https://ns.adobe.com/experience/offer-management/personalized-offer``https://ns.adobe.com/experience/offer-management/fallback-offer`

設定選件限制`xdm:representations``xdm:representations`

## 日曆限制

### 一般而言，決策選項可提供作為日曆限制的開始和結束日期和時間。 屬性嵌入在屬性中 `xdm:selectionConstraint`:

**`xdm:startDate`** -此屬性指示開始日期和時間。 該值是按RFC 3339規則格式化的字串，例如，此時間戳： 「2019-06-13T11:21:23.356Z」。
尚未到達其開始日期和時間的決策選項在決策中尚未被視為合格。

- **`xdm:endDate`** -此屬性指示結束日期和時間。 該值是按RFC 3339規則格式化的字串，例如，此時間戳： 「2019-07-13T11:00:00.000Z」已通過其結束日期和時間的決策選項在決策過程中不再被視為合格。
- **`xdm:endDate`**更改日曆約束可以通過以下PATCH調用完成：

如需 [完整的cURL語法](#updating-and-patching-instances) ，請參閱更新和修補例項。 參 `schemaId` 數必須 `https://ns.adobe.com/experience/offer-management/personalized-offer`。 備援選件沒有任何限制。

```json
[
  {
    "op":   "replace",
    "path": "/_instance/xdm:selectionConstraint",
    "value": {
      "xdm:startDate": "2019-06-13T00:00:00.000Z",
      "xdm:endDate":   "2019-07-13T00:00:00.000Z"
    } 
  }
]' 
```

封閉約束[](#updating-and-patching-instances)`schemaId``https://ns.adobe.com/experience/offer-management/personalized-offer`

### 封閉約束是定義封閉參數的決策選項中的元件。 封閉是一種過程，用於限制每個描述檔以及所有描述檔中可建議選項的次數。 屬性包含必須大於或等於1的整數值。 屬性嵌套在屬性內 `xdm:cappingConstraint`:

**`xdm:globalCap`** -全域上限是限制選件可整體建議的次數。

- **`xdm:profileCap`** -描述檔上限是對特定描述檔建議選件次數的限制。
- **`xdm:profileCap`**在個人化選件上設定或變更封頂限制，可透過下列PATCH呼叫完成：

如需 [完整的cURL語法](#updating-and-patching-instances) ，請參閱更新和修補例項。 參 `schemaId` 數必須 `https://ns.adobe.com/experience/offer-management/personalized-offer`。 備援選件沒有任何限制。

```json
[
  {
    "op":   "add",
    "path": "/_instance/xdm:cappingConstraint",
    "value": {
      "xdm:globalCap":  1000000,
      "xdm:profileCap": 5
    } 
  }
]' 
```

要刪除封閉值，操作&quot;add&quot;將替換為操作&quot;remove&quot;。 請注意，封閉值單獨存在，也可以單獨設定或移除。[](#updating-and-patching-instances)`schemaId``https://ns.adobe.com/experience/offer-management/personalized-offer`

資格限制

### 選件可在決策程式中有條件地選取。 當個人化選件參考資格規則時，規則條件必須評估為true，才能將選件物件視為指定的描述檔。 資格規則是獨立於決策選項而建立和管理的，同一規則可從多個個人化選件參考。

規則的參考內嵌在屬性中 `xdm:selectionConstraint`:

**`xdm:eligibilityRule`** -此屬性包含資格規則的參考。 該值是schema `@id` https://ns.adobe.com/experience/offer-management/eligibility-rule的實例。

- **`xdm:eligibilityRule`**添加和刪除規則也可以通過PATCH操作完成：`@id`

如需 [完整的cURL語法](#updating-and-patching-instances) ，請參閱更新和修補例項。 參 `schemaId` 數必須 `https://ns.adobe.com/experience/offer-management/personalized-offer`。 備援選件沒有任何限制。

```
[
  {
    "op":   "replace",
    "path": "/_instance/xdm:selectionConstraint/xdm:eligibilityRule",
    "value": "xcore:eligibility-rule:f84c6b33cc63c65" 
  }
]'
```

請注意，資格規則會與日曆約 `xdm:selectionConstraint` 束一起嵌入屬性中。 PATCH操作不應嘗試刪除整個 `SelectionConstraint` 屬性。`schemaId``https://ns.adobe.com/experience/offer-management/personalized-offer`

設定選件的優先順序`xdm:selectionConstraint``SelectionConstraint`

## 符合資格的決策選項將會被排名，以決定給定描述檔的最佳選項。 為了支援該排名，並在排名不能由另一個機制確定的情況下提供預設值，可以為每個個性化選件設定基本優先順序。
基本優先順序嵌入到屬性中 `xdm:rank`:

**`xdm:priority`** -此屬性代表在沒有已知描述檔特定排名順序的情況下，選取一個選件的預設順序。 如果比較優先順序值後，仍會系結兩個或兩個以上的個人化選件，則會隨機選擇一個選件，並用於選件提案中。 此屬性的值必須是大於或等於0的整數。

- **`xdm:priority`**通過以下PATCH調用可以調整基本優先順序：

如需 [完整的cURL語法](#updating-and-patching-instances) ，請參閱更新和修補例項。 參 `schemaId` 數必須 `https://ns.adobe.com/experience/offer-management/personalized-offer`。 備援選件沒有任何排名屬性。

```shell
curl -X PATCH {ENDPOINT_PATH}/{CONTAINER_ID}/instances/{INSTANCE_ID} \
  -H 'Content-Type: application/vnd.adobe.platform.xcore.patch.hal+json; schema="{SCHEMA_ID}"' \ 
  -H 'Accept: application/vnd.adobe.platform.xcore.xdm.receipt+json \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  _H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'x-request-id: {NEW_UUID}' \
  -d '[
  {
    "op":   "replace",
    "path": "/_instance/xdm:rank/xdm:priority",
    "value": 0 
  }
]'
```

管理決策規則[](#updating-and-patching-instances)`schemaId``https://ns.adobe.com/experience/offer-management/personalized-offer`

## 資格規則會保留評估的條件，以判斷特定決策選項是否符合指定描述檔的資格。 將規則附加至一或多個決策選項會隱式定義，對於此選項，規則必須評估為true，才能讓此使用者考慮該選項。 規則可包含描述檔屬性的測試、可評估與此描述檔的體驗事件相關的運算式，以及可包含傳遞至決策請求的上下文資料。 例如，條件可描述為：

「包括那些擁有精英地位、在過去6個月中曾三次坐過航班的個人，他們的航班號碼與目前的航班號相同。」

> 使用架構識別碼https://ns.adobe.com/experience/offer-management/eligibility-rule建立例項。 建 `_instance` 立或更新呼叫的屬性如下：

如需 [完整的cURL語法](#updating-and-patching-instances) ，請參閱更新和修補例項。 參 `schemaId` 數必須 `https://ns.adobe.com/experience/offer-management/eligibility-rule`。

```json
{
  "xdm:name": "Eligible for a free flight upgrade",
  "xdm:condition": {
    "xdm:value": 
      "membership.status = \"elite\" 
       and (select e from xEvent 
            where e.type = \"flight\" 
              and e.flightnumber = @{{SCHEMA_ID}}.flightnumber
              and (e.timestamp occurs <= 6 months before now).count() > 3
           )",
    "xdm:format": "pql/text",
    "xdm:type": "PQL"
  }
}
```

規則條件屬性中的值包含PQL運算式。 上下文資料是透過特殊路徑運算式@{schemaID}來參考。[](#updating-and-patching-instances)`schemaId``https://ns.adobe.com/experience/offer-management/eligibility-rule`

規則自然會與設定檔中的區 [!DNL Experience Platform] 段對齊，而規則通常只會透過測試描述檔屬性，重複使用區段的意 `segmentMembership` 圖。 屬 `segmentMembership` 性包含已評估的區段條件結果。 這可讓組織定義其網域特定對象一次、命名對象並評估條件一次。

管理選件集合[!DNL Experience Platform]`segmentMembership``segmentMembership`

## 建立標籤和標籤選件

### 選件可以組織在系列中，其中每個系列都定義要套用的篩選條件。 目前，系列中的篩選運算式可以有下列兩種表單之一：

選件 `@id` 的參數必須符合系列中選件識別碼清單中的一個參數。 此篩選器只是系列中選件的URI列舉。

1. 選件可以有標籤參考清單，而系列的篩選器則包含標籤清單。 在下列情況下，選件會出現在系列中：`@id`
2. a. 任何篩選標籤都符合選件的其中一個標籤\
   b. 所有篩選的標籤都符合選件的其中一個標籤\
   標籤是可連結至選件例項的簡單例項。 它們是獨立的例項，具有顯示它們的名稱。 此名稱在各執行個體間必須是唯一的，讓使用者介面中更容易顯示。

標籤物件可用於在決策選項（選件）中建立分類。 標籤可以由許多選件連結，而選件可以有許多標籤參考。 選件類別是參照與一組特定標籤例項相關的所有選件來建立。

標籤例項是使用架構識別碼https://ns.adobe.com/experience/offer-management/tag建立。 建 `_instance` 立或更新呼叫的屬性如下：

如需 [完整的cURL語法](#updating-and-patching-instances) ，請參閱更新和修補例項。 參 `schemaId` 數必須 `https://ns.adobe.com/experience/offer-management/tag`。

```json
{
  "xdm:name": "credit card"
} 
```

您可以使用標籤參考清單來建立選件例項，例如：[](#updating-and-patching-instances)`schemaId``https://ns.adobe.com/experience/offer-management/tag`


或者，選件可修補以變更其標籤清單：

```json
{
  "xdm:name": "ABC Bank Credit Card",
  "xdm:tags": [
    "xcore:tag:f66f67dbe6d6ee1",
    "xcore:tag:f2df943c428b6f7"
  ]
}
```

對於這兩種情況，請參 [閱更新和修補例項](#updating-and-patching-instances) ，以取得完整的cURL語法。 參 `schemaId` 數必須 `https://ns.adobe.com/experience/offer-management/personalized-offer`。

```json
[
  {
    "op":    "add",
    "path":  "/_instance/xdm:tags/-",
    "value": "xcore:tag:f66f677ad3c0ba7" 
  }
]' 
```

請注意， `xdm:tags` 屬性必須已存在，才能成功添加操作。 PATCH操作可以先添加array屬性，然後向該陣列添加標籤引用，實例中不存在標籤。](#updating-and-patching-instances)`schemaId``https://ns.adobe.com/experience/offer-management/personalized-offer`

定義選件系列的篩選`xdm:tags`

### 篩選例項是使用架構識別碼https://ns.adobe.com/experience/offer-management/offer-filter來建立。 建立 `_instance` 或更新呼叫的屬性可能如下所示：

如需 [完整的cURL語法](#updating-and-patching-instances) ，請參閱更新和修補例項。 參 `schemaId` 數必須 `https://ns.adobe.com/experience/offer-management/offer-filter`。

```json
{
  "xdm:name": "All Upgrade offers",
  "xdm:filterType": "allTags",
  "ids": [
    "xcore:tag:f66f67dbe6d6ee1",
    "xcore:tag:f66f677ad3c0ba7"
  ]
}
```

**`xdm:filterType`** -此屬性指出篩選是使用標籤設定，還是直接參照其ID的選件。 當篩選設定為使用標籤時，篩選類型可進一步指出所有標籤是否必須符合特定選件上的標籤，或任一指定標籤是否足以讓選件符合篩選條件。 此列舉屬性的有效值為：](#updating-and-patching-instances)`schemaId``https://ns.adobe.com/experience/offer-management/offer-filter`

- `offers`
   - `anyTags`
   - `allTags`
   - **`ids`** -屬性包含URI的陣列，這些URI是選件例項或標籤例項的參考，視值而定 `xdm:filterType`。 .
- 下列呼叫說明建立或 `_instance` 更新呼叫的屬性在選件被直接參考時的外觀：`xdm:filterType`

管理活動`_instance`

```json
{
  "xdm:name": "All Upgrade offers",
  "xdm:filterType": "offers",
  "ids": [
    "xcore:personalized-offer:f85e8298e53398d",
    "xcore:personalized-offer:f83a85c2bca3f1f",
    "xcore:personalized-offer:f9195bd412180b1",
    "xcore:personalized-offer:f67be37b6ad6ee6",
    "xcore:personalized-offer:f87bcc710ba6e93",
    "xcore:personalized-offer:f8855c30c0b20f8",
    "xcore:personalized-offer:f67bca7032d6ee5",
    "xcore:personalized-offer:f67bab756ed6ee4",
    "xcore:personalized-offer:f65281d506d6edf"
  ] 
} 
```

## 選件活動可用來控制決策程式。 它會指定套用至總庫存的選件篩選條件，以依主題／類別縮小選件，將庫存縮小至符合預留空間的選件的位置，並指定當組合的限制不符合所有可用的個人化選件（選件）時的備援選項。

活動實例是使用方案標識符建立的`https://ns.adobe.com/experience/offer-management/offer-activity`。 建 `_instance` 立或更新呼叫的屬性如下：

如需 [完整的cURL語法](#updating-and-patching-instances) ，請參閱更新和修補例項。 參 `schemaId` 數必須 `https://ns.adobe.com/experience/offer-management/offer-activity`。

```json
{
  "xdm:name": "Call center IVR Personalization",
  "xdm:startDate": "2019-03-01T05:59:59.999Z",
  "xdm:endDate":   "2019-12-27T00:00:00.000Z",
  "xdm:status":    "live",
  "xdm:placement": "xcore:offer-placement:f652486959731ff",
  "xdm:filter":    "xcore:offer-filter:f6998eb62ed6f15",
  "xdm:fallback":  "xcore:fallback-offer:f6529b31b3c0ba6"
}
```

**`xdm:name`** -此強制屬性包含活動名稱。 名稱會顯示在各種使用者介面中。](#updating-and-patching-instances)`schemaId``https://ns.adobe.com/experience/offer-management/offer-activity`

- **`xdm:status`** -此屬性用於實例的生命週期管理。 此值代表工作流程狀態，用於指出活動是否仍在建置中（值=草稿）、執行階段通常可考慮（值=即時），或是不應再使用（值=封存）。
- **`xdm:placement`** -強制屬性，包含對選件位置的參考，當做出決策時，選件位置會套用至庫存。 值是所使用之選`@id`件位置的URI()。
- **`xdm:filter`** -強制屬性，包含對選件篩選的參考，當在此活動中做出決策時，選件篩選會套用至庫存。 值是所使用之選`@id`件篩選器的URI()。
- **`xdm:fallback`** -包含備援選件參考的必備屬性。 當此活動的決策不符合任何個人化選件的資格時，會使用備援選件。 該值是備援選件`@id`例項的URI()。
- **`xdm:fallback`**管理備援選件`@id`

### 建立活動例項之前，必須有符合活動位置的備援選件。 備援選件例項是使用結構識別碼建立`https://ns.adobe.com/experience/offer-management/fallback-offer`。 建 `_instance` 立或更新呼叫的屬性包含與個人化選件相同的一般屬性，但不能有任何其他限制。

如需 [完整的cURL語法](#updating-and-patching-instances) ，請參閱更新和修補例項。 參 `schemaId` 數必須 `https://ns.adobe.com/experience/offer-management/fallback-offer`。

```json
{
  "xdm:name": "Default for Kiosk Placements",
  "xdm:status": "approved",
  "xdm:representations": [
    {
      "xdm:placement": "xcore:offer-placement:e91afcf81bad130"
      "xdm:components": [
        {
          "dc:language": ["en" ],
          "@type": "https://ns.adobe.com/experience/offer-management/content-component-html",
          "dc:format": "text/html"
        }
      ]
    }
  ]
}  
```

See [Updating and patching instances](#updating-and-patching-instances) for the full cURL syntax. The `schemaId` parameter must be `https://ns.adobe.com/experience/offer-management/fallback-offer`.

