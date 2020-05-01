---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: 資料湖中的隱私權要求處理
topic: overview
translation-type: tm+mt
source-git-commit: d3584202554baf46aad174d671084751e6557bbc

---


# 資料湖中的隱私權要求處理

Adobe Experience Platform隱私權服務會處理客戶存取、選擇退出銷售或刪除其個人資料的要求，並符合法律和組織的隱私權法規。

本檔案涵蓋處理儲存在資料湖中之客戶資料之隱私權要求的相關基本概念。

## 快速入門

建議您在閱讀本指南之前，先瞭解下列Experience Platform服務：

* [隱私權服務](../privacy-service/home.md): 管理客戶在Adobe Experience Cloud應用程式中存取、選擇退出銷售或刪除其個人資料的要求。
* [目錄服務](home.md): Experience Platform中資料位置和世系的記錄系統。 提供可用來更新資料集中繼資料的API。
* [體驗資料模型(XDM)系統](../xdm/home.md): Experience Platform組織客戶體驗資料的標準化架構。
* [身分服務](../identity-service/home.md): 透過跨裝置和系統橋接身分，解決客戶體驗資料分散所帶來的根本挑戰。

## 瞭解身分名稱空間 {#namespaces}

Adobe Experience Platform Identity Service可跨系統和裝置橋接客戶身分資料。 身分服務使用 **身分名稱空間** ，將身分值與其來源系統關聯，以提供其上下文。 命名空間可以代表一般概念，例如電子郵件地址（「電子郵件」），或將身分識別與特定應用程式(例如Adobe Advertising Cloud ID(「AdCloud」)或Adobe Target ID(「TNTID」))建立關聯。

Identity Service會維護全域定義（標準）和使用者定義（自訂）身分名稱空間的儲存。 標準名稱空間適用於所有組織（例如「電子郵件」和「ECID」），而您的組織也可以建立自訂名稱空間，以符合其特定需求。

如需Experience Platform中身分名稱空間的詳細資訊，請參閱身分 [名稱空間概觀](../identity-service/namespaces.md)。

## 向資料集添加身份資料

當建立資料湖的隱私權要求時，必須為每個個別客戶提供有效的身分值（及其相關的名稱空間），以找出其資料並據以處理。 因此，所有受隱私請求約束的資料集都必須在其關聯的XDM **模式中包含** 身份描述符。

>[!NOTE] 目前無法在隱私權要求中處理任何以不支援身分描述子中繼資料（例如臨機資料集）的結構為基礎的資料集。

本節將逐步介紹將身份描述符添加到現有資料集的XDM模式的步驟。 如果您已有具有身分描述符的資料集，則可跳至下 [一節](#nested-maps)。

>[!IMPORTANT] 在決定要設定為身分的架構欄位時，請記住使 [用巢狀映射類型欄位的限制](#nested-maps)。

將身份描述符添加到資料集模式有兩種方法：

* [使用UI](#identity-ui)
* [使用API](#identity-api)

### 使用UI {#identity-ui}

在Experience Platform使用者介面中，工作區 _[!UICONTROL Schemas]_可讓您編輯現有的XDM結構。 要向方案添加標識描述符，請從清單中選擇方案，並遵循在方案編輯器教程[中將方案欄位設定為標識欄位的步驟](../xdm/tutorials/create-schema-ui.md#identity-field)。

在您將架構中的適當欄位設定為身分欄位後，您就可以繼續下一節的隱私權 [要求](#submit)。

### 使用API {#identity-api}

>[!NOTE] 本節假定您知道資料集的XDM架構的唯一URI ID值。 如果您不知道此值，可使用Catalog Service API來擷取該值。 閱讀開發人 [員指南的](./api/getting-started.md) 「快速入門」一節後，請依照中所述的步驟列 [出或](./api/list-objects.md) 尋找 [](./api/look-up-object.md) Catalog物件以尋找您的資料集。 可在 `schemaRef.id`
>
> 本節包含對方案註冊表API的調用。 如需有關使用API的重要資訊，包括瞭解您 `{TENANT_ID}` 的概念和容器概念，請參閱開 [發人員指南的](../xdm/api/getting-started.md) 「快速入門」一節。

通過向模式註冊表API中的端點發出POST請求，可以將身份描述符添加到資料集的XDM `/descriptors` 模式中。

**API格式**

```http
POST /descriptors
```

**請求**

以下請求在示例方案的「電子郵件地址」欄位上定義身份描述符。

```shell
curl -X POST \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/descriptors \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '
      {
        "@type": "xdm:descriptorIdentity",
        "xdm:sourceSchema": "https://ns.adobe.com/{TENANT_ID}/schemas/fbc52b243d04b5d4f41eaa72a8ba58be",
        "xdm:sourceVersion": 1,
        "xdm:sourceProperty": "/personalEmail/address",
        "xdm:namespace": "Email",
        "xdm:property": "xdm:code",
        "xdm:isPrimary": false
      }'
```

| 屬性 | 說明 |
| --- | --- |
| `@type` | 正在建立的描述符的類型。 對於身份描述符，值必須是&quot;xdm:descriptorIdentity&quot;。 |
| `xdm:sourceSchema` | 資料集XDM架構的唯一URI ID。 |
| `xdm:sourceVersion` | 中指定的XDM架構版本 `xdm:sourceSchema`。 |
| `xdm:sourceProperty` | 描述符要應用到的模式欄位的路徑。 |
| `xdm:namespace` | 隱私權服務 [可辨識的標準身分名稱空間](../privacy-service/api/appendix.md#standard-namespaces) ，或貴組織定義的自訂名稱空間。 |
| `xdm:property` | 視下方使用的命名空間而定，可選擇「xdm:id」或「xdm:code」 `xdm:namespace`。 |
| `xdm:isPrimary` | 選用的布林值。 若為true，則表示欄位為主要身分。 結構只能包含一個主要標識。 若未包含，則預設為false。 |

**回應**

成功的響應返回HTTP狀態201（已建立）和新建立的描述符的詳細資訊。

```json
{
  "@type": "xdm:descriptorIdentity",
  "xdm:sourceSchema": "https://ns.adobe.com/{TENANT_ID}/schemas/fbc52b243d04b5d4f41eaa72a8ba58be",
  "xdm:sourceVersion": 1,
  "xdm:sourceProperty": "/personalEmail/address",
  "xdm:namespace": "Email",
  "xdm:property": "xdm:code",
  "xdm:isPrimary": false,
  "meta:containerId": "tenant",
  "@id": "f3a1dfa38a4871cf4442a33074c1f9406a593407"
}
```

## 提交請求 {#submit}

>[!NOTE] 本節說明如何設定資料湖的隱私權要求的格式。 強烈建議您檢閱 [Privacy Service UI](../privacy-service/ui/overview.md) 或 [Privacy Service API](../privacy-service/api/getting-started.md) 檔案，以取得如何提交隱私權工作的完整步驟，包括如何在請求負載中正確格式化已提交的使用者身分資料。

下節將說明如何使用隱私權服務UI或API來提出資料湖的隱私權要求。

### 使用UI

在UI中建立工作請求時，請務必在 **Products下選取** AEP Data Lake **和／或** Profile __ ，以便分別處理儲存在Data Lake或Real-time Customer Profile中的資料的工作。

<img src="images/privacy/product-value.png" width="450"><br>

### 使用API

在API中建立工作請求時，所 `userIDs` 提供的任何作業請求都必須使用特 `namespace` 定 `type` 的作業請求，並視其套用的資料儲存區而定。 資料湖的ID必須使用「未註冊」作為其 `type` 值，且值 `namespace` 必須符合已新增至適用資料集的 [隱私權標籤](#privacy-labels) 。

此外，請求 `include` 裝載的陣列必須包含請求所針對之不同資料存放區的產品值。 向Data Lake請求時，陣列必須包含值&quot;aepDataLake&quot;。

下列請求會使用未註冊的「email_label」命名空間，為資料湖建立新的隱私權工作。 它還包括陣列中Data Lake的產品 `include` 值：

```shell
curl -X POST \
  https://platform.adobe.io/data/core/privacy/jobs \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -d '{
    "companyContexts": [
      {
        "namespace": "imsOrgID",
        "value": "{IMS_ORG}"
      }
    ],
    "users": [
      {
        "key": "user12345",
        "action": ["access","delete"],
        "userIDs": [
          {
            "namespace": "email_label",
            "value": "ajones@acme.com",
            "type": "unregistered"
          },
          {
            "namespace": "email_label",
            "value": "jdoe@example.com",
            "type": "unregistered"
          }
        ]
      }
    ],
    "include": ["aepDataLake"],
    "expandIds": false,
    "priority": "normal",
    "regulation": "ccpa"
}'
```

## 刪除請求處理

當Experience Platform收到來自隱私權服務的刪除要求時，平台會向隱私權服務傳送確認該要求已收到且受影響的資料已標示為刪除。 然後在七天內將記錄從資料湖中移除。 在該七天的時段內，資料會被軟刪除，因此無法由任何平台服務存取。

在未來版本中，平台會在實際刪除資料後傳送確認給隱私權服務。

## 後續步驟

閱讀本檔案後，您便瞭解處理資料湖的隱私權要求所涉及的重要概念。 建議您繼續閱讀本指南中提供的檔案，以加深您對如何管理身分資料和建立隱私權工作的瞭解。

如需處理描述檔 [商店的隱私權要求的步驟](../profile/privacy.md) ，請參閱即時客戶描述檔的隱私權要求處理檔案。

## 附錄

下節包含處理資料湖中隱私權要求的其他資訊。

### 標籤巢狀映射類型欄位 {#nested-maps}

請務必注意，有兩種巢狀映射類型欄位不支援隱私權標籤：

* 陣列類型欄位中的映射類型欄位
* 另一個映射類型欄位中的映射類型欄位

上述兩個範例中的任一範例的隱私權工作處理最終會失敗。 因此，建議您避免使用巢狀對應類型欄位來儲存私人客戶資料。 相關的使用者ID應儲存為記錄型資料集的欄位 `identityMap` （本身為映射類型欄位）內的非映射資料類型，或時間 `endUserID` 系列型資料集的欄位。