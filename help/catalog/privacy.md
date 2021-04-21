---
keywords: Experience Platform;home；熱門主題；資料湖隱私；身份名稱空間；隱私；資料湖
solution: Experience Platform
title: 資料湖中的隱私權要求處理
topic-legacy: overview
description: Adobe Experience Platform Privacy Service公司處理客戶存取、選擇退出銷售或刪除其個人資料的要求，這些要求由法律和組織的隱私權法規規定。 本檔案涵蓋處理儲存在資料湖中之客戶資料之隱私權要求的相關基本概念。
exl-id: c06b0a44-be1a-4938-9c3e-f5491a3dfc19
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '1279'
ht-degree: 0%

---

# 在[!DNL Data Lake]中處理隱私權要求

Adobe Experience Platform[!DNL Privacy Service]會處理客戶存取、選擇退出銷售或刪除其個人資料的要求，如法律和組織隱私權規定所述。

本檔案涵蓋處理儲存在[!DNL Data Lake]中之客戶資料之隱私權要求的相關基本概念。

## 快速入門

建議您在閱讀本指南之前，先瞭解以下[!DNL Experience Platform]服務：

* [[!DNL Privacy Service]](../privacy-service/home.md):管理客戶在Adobe Experience Cloud應用程式中存取、選擇退出銷售或刪除其個人資料的要求。
* [[!DNL Catalog Service]](home.md):資料位置和世系的記錄系統 [!DNL Experience Platform]。提供可用來更新資料集中繼資料的API。
* [[!DNL Experience Data Model (XDM) System]](../xdm/home.md):組織客戶體驗資 [!DNL Experience Platform] 料的標準化架構。
* [[!DNL Identity Service]](../identity-service/home.md):透過跨裝置和系統橋接身分，解決客戶體驗資料分散所帶來的根本挑戰。

## 瞭解身份名稱空間{#namespaces}

Adobe Experience Platform[!DNL Identity Service]跨系統和設備橋接客戶身份資料。 [!DNL Identity Service] 使用身份名稱空間將身份值與其來源系統關聯，以提供上下文至身份值。命名空間可以代表一般概念，例如電子郵件地址（「電子郵件」），或將識別與特定應用程式(例如Adobe Advertising CloudID(「AdCloud」)或Adobe TargetID(「TNTID」))建立關聯。

[!DNL Identity Service] 維護全局定義（標準）和用戶定義（自定義）標識名稱空間的儲存。標準名稱空間適用於所有組織（例如「電子郵件」和「ECID」），而您的組織也可以建立自訂名稱空間以符合其特定需求。

有關[!DNL Experience Platform]中身份名稱空間的詳細資訊，請參閱[身份名稱空間概述](../identity-service/namespaces.md)。

## 向資料集添加身份資料

為[!DNL Data Lake]建立隱私權要求時，必須為每個個別客戶提供有效的識別值（及其關聯的名稱空間），以找出其資料並據以處理。 因此，所有受隱私請求約束的資料集都必須在其關聯的XDM模式中包含身份描述符。

>[!NOTE]
>
>目前無法在隱私權要求中處理任何以不支援身分描述子中繼資料（例如臨機資料集）的結構為基礎的資料集。

本節將逐步介紹將身份描述符添加到現有資料集的XDM模式的步驟。 如果您已有具有身分描述符的資料集，則可跳至[下一節](#nested-maps)。

>[!IMPORTANT]
>
>在決定要設定為身分的架構欄位時，請記住使用巢狀映射類型欄位](#nested-maps)的[限制。

將身份描述符添加到資料集模式有兩種方法：

* [使用UI](#identity-ui)
* [使用API](#identity-api)

### 使用UI {#identity-ui}

在[!DNL Experience Platform ]使用者介面中， **[!UICONTROL Schemas]**&#x200B;工作區可讓您編輯現有的XDM結構。 要向方案添加標識描述符，請從清單中選擇方案，並遵循[教程中將方案欄位設定為身份欄位[!DNL Schema Editor]的步驟。](../xdm/tutorials/create-schema-ui.md#identity-field)

在將架構中的相應欄位設定為身份欄位後，您可以繼續下一節有關[提交隱私請求](#submit)的內容。

### 使用API {#identity-api}

>[!NOTE]
>
>本節假定您知道資料集的XDM架構的唯一URI ID值。 如果您不知道此值，則可使用[!DNL Catalog Service] API來擷取該值。 閱讀開發人員指南的[getting started](./api/getting-started.md)一節後，請依照[列出](./api/list-objects.md)或[查找](./api/look-up-object.md) [!DNL Catalog]物件的步驟，尋找您的資料集。 可在`schemaRef.id`下找到架構ID
>
> 本節包含對方案註冊表API的調用。 如需有關使用API的重要資訊，包括瞭解您的`{TENANT_ID}`和容器概念，請參閱開發人員指南的[快速入門](../xdm/api/getting-started.md)一節。

通過向[!DNL Schema Registry] API中的`/descriptors`端點發出POST請求，可以將身份描述符添加到資料集的XDM模式。

**API格式**

```http
POST /descriptors
```

**要求**

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
| `xdm:sourceVersion` | `xdm:sourceSchema`中指定的XDM架構版本。 |
| `xdm:sourceProperty` | 描述符要應用到的模式欄位的路徑。 |
| `xdm:namespace` | [由[!DNL Privacy Service]識別的](../privacy-service/api/appendix.md#standard-namespaces)標準識別名稱空間，或由您的組織定義的自訂名稱空間。 |
| `xdm:property` | 根據`xdm:namespace`下使用的命名空間，可選擇&quot;xdm:id&quot;或&quot;xdm:code&quot;。 |
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

## 提交請求{#submit}

>[!NOTE]
>
>本節介紹如何格式化[!DNL Data Lake]的隱私權請求。 強烈建議您檢閱[[!DNL Privacy Service] UI](../privacy-service/ui/overview.md)或[[!DNL Privacy Service] API](../privacy-service/api/getting-started.md)檔案，以取得如何提交隱私權工作的完整步驟，包括如何在請求負載中正確格式化已提交的使用者身分資料。

下節概述如何使用[!DNL Privacy Service] UI或API，對[!DNL Data Lake]提出隱私權要求。

>[!IMPORTANT]
>
>無法保證隱私權要求完成所需的時間。 如果在請求仍在處理時在資料湖中發生變更，則無法保證是否處理這些記錄。

### 使用UI

在UI中建立作業請求時，請務必在&#x200B;**[!UICONTROL Products]**&#x200B;下選擇&#x200B;**[!UICONTROL AEP Data Lake]**&#x200B;和／或&#x200B;**[!UICONTROL Profile]**，以便分別處理儲存在[!DNL Data Lake]或[!DNL Real-time Customer Profile]中的資料的作業。

<img src="images/privacy/product-value.png" width="450"><br>

### 使用API

在API中建立工作請求時，所提供的任何`userIDs`必須使用特定的`namespace`和`type`，視其套用的資料儲存區而定。 [!DNL Data Lake]的ID必須對其`type`值使用「未註冊」，而`namespace`值必須與已新增至適用資料集的[隱私標籤](#privacy-labels)中的一個值相符。

此外，請求裝載的`include`陣列必須包含請求所針對之不同資料存放區的產品值。 向[!DNL Data Lake]發出請求時，陣列必須包含值`aepDataLake`。

以下請求使用未註冊的&quot;email_label&quot;命名空間為[!DNL Data Lake]建立一個新的隱私作業。 它還包含`include`陣列中[!DNL Data Lake]的產品值：

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

當[!DNL Experience Platform]收到[!DNL Privacy Service]的刪除請求時，[!DNL Platform]會向[!DNL Privacy Service]發送確認請求已接收且受影響的資料已標籤為刪除。 然後在7天內從[!DNL Data Lake]中移除記錄。 在該七天的時段內，資料會被軟刪除，因此無法由任何[!DNL Platform]服務存取。

在未來版本中，[!DNL Platform]會在實際刪除資料後傳送確認給[!DNL Privacy Service]。

## 後續步驟

閱讀本檔案後，您便瞭解處理[!DNL Data Lake]隱私權要求的重要概念。 建議您繼續閱讀本指南中提供的檔案，以加深您對如何管理身分資料和建立隱私權工作的瞭解。

如需處理[!DNL Profile]商店隱私權要求的步驟，請參閱「即時客戶設定檔」的[隱私權要求處理檔案。](../profile/privacy.md)

## 附錄

以下章節包含處理[!DNL Data Lake]中隱私權要求的其他資訊。

### 標籤嵌套的映射類型欄位{#nested-maps}

請務必注意，有兩種巢狀映射類型欄位不支援隱私權標籤：

* 陣列類型欄位中的映射類型欄位
* 另一個映射類型欄位中的映射類型欄位

上述兩個範例中的任一範例的隱私權工作處理最終會失敗。 因此，建議您避免使用巢狀對應類型欄位來儲存私人客戶資料。 相關的消費者ID應儲存為記錄型資料集的`identityMap`欄位（本身是映射類型欄位）中的非映射資料類型，或基於時間序列的資料集的`endUserID`欄位。
