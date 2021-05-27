---
keywords: Experience Platform；首頁；熱門主題；資料湖隱私權；身分命名空間；隱私權；資料湖
solution: Experience Platform
title: 資料湖的隱私權要求處理
topic-legacy: overview
description: Adobe Experience Platform Privacy Service會處理客戶要求存取、選擇退出銷售或刪除其個人資料（如法律和組織隱私權法規所規定）。 本檔案涵蓋與處理資料湖中儲存之客戶資料的隱私權要求相關的基本概念。
exl-id: c06b0a44-be1a-4938-9c3e-f5491a3dfc19
source-git-commit: e94482532e0c5698cfe5e51ba260f89c67fa64f0
workflow-type: tm+mt
source-wordcount: '1351'
ht-degree: 1%

---

# [!DNL Data Lake]中的隱私權要求處理

Adobe Experience Platform [!DNL Privacy Service]會處理客戶存取、選擇退出銷售或刪除其個人資料的請求，如法律和組織隱私權法規所述。

本檔案涵蓋與處理儲存在[!DNL Data Lake]中之客戶資料的隱私權要求相關的基本概念。

>[!NOTE]
>
>本指南僅說明如何以Experience Platform形式向Data Lake提出隱私權要求。 如果您也打算為即時客戶設定檔資料存放區提出隱私權要求，除了本教學課程外，請參閱設定檔](../profile/privacy.md)隱私權要求處理的指南。[
>
>如需如何為其他Adobe Experience Cloud應用程式提出隱私權要求的步驟，請參閱[Privacy Service檔案](../privacy-service/experience-cloud-apps.md)。

## 快速入門

在閱讀本指南之前，建議您對以下[!DNL Experience Platform]服務有充分的了解：

* [[!DNL Privacy Service]](../privacy-service/home.md):管理客戶在Adobe Experience Cloud應用程式中存取、選擇退出銷售或刪除其個人資料的請求。
* [[!DNL Catalog Service]](home.md):記錄內資料位置和世系的系 [!DNL Experience Platform]統。提供可用來更新資料集中繼資料的API。
* [[!DNL Experience Data Model (XDM) System]](../xdm/home.md):組織客戶體驗資 [!DNL Experience Platform] 料的標準化架構。
* [[!DNL Identity Service]](../identity-service/home.md):通過跨裝置和系統橋接身分，解決客戶體驗資料分散帶來的根本難題。

## 了解身分識別命名空間 {#namespaces}

Adobe Experience Platform [!DNL Identity Service]橋接跨系統和裝置的客戶身分資料。 [!DNL Identity Service] 使用身分識別命名空間，將身分識別值與來源系統關聯，以提供內容與身分識別值。命名空間可代表一般概念，例如電子郵件地址（「電子郵件」），或將身分識別與特定應用程式建立關聯，例如Adobe Advertising Cloud ID(「AdCloud」)或Adobe Target ID(「TNTID」)。

[!DNL Identity Service] 維護全域定義（標準）和使用者定義（自訂）身分識別命名空間的存放區。所有組織皆可使用標準命名空間（例如「電子郵件」和「ECID」），而您的組織也可以建立自訂命名空間，以符合其特定需求。

如需[!DNL Experience Platform]中身分命名空間的詳細資訊，請參閱[身分命名空間概述](../identity-service/namespaces.md)。

## 將身分資料新增至資料集

為[!DNL Data Lake]建立隱私權要求時，必須為每個個別客戶提供有效的身分值（及其相關的命名空間），以便找到其資料並據以處理。 因此，所有受隱私權要求約束的資料集，都必須在其相關聯的XDM結構中包含身分描述元。

>[!NOTE]
>
>目前無法在隱私權要求中處理任何以結構為基礎但不支援身分描述元資料的資料集（例如臨機資料集）。

本節將逐步說明將身分描述元新增至現有資料集的XDM架構的步驟。 如果您已有具有身分描述元的資料集，可以跳到[下一節](#nested-maps)。

>[!IMPORTANT]
>
>在決定要將哪些架構欄位設為身分時，請記住使用巢狀映射類型欄位](#nested-maps)的[限制。

將身分描述符新增至資料集架構有兩種方法：

* [使用UI](#identity-ui)
* [使用 API](#identity-api)

### 使用UI {#identity-ui}

在[!DNL Experience Platform ]使用者介面中， **[!UICONTROL 結構]**&#x200B;工作區可讓您編輯現有的XDM結構。 要向架構添加標識描述符，請從清單中選擇架構，並按照[將架構欄位設定為[!DNL Schema Editor]教程中的標識欄位](../xdm/tutorials/create-schema-ui.md#identity-field)的步驟操作。

在您將架構內的適當欄位設為身分欄位後，即可繼續前往[提交隱私權要求](#submit)的下一節。

### 使用 API {#identity-api}

>[!NOTE]
>
>本節假設您知道資料集XDM架構的唯一URI ID值。 如果您不知道此值，可使用[!DNL Catalog Service] API來擷取該值。 閱讀開發人員指南的[getting started](./api/getting-started.md)一節後，請依照[listing](./api/list-objects.md)或[rooking](./api/look-up-object.md) [!DNL Catalog]物件中概述的步驟，尋找您的資料集。 可在`schemaRef.id`下找到架構ID
>
> 本節包含對Schema Registry API的呼叫。 如需與使用API相關的重要資訊，包括了解您的`{TENANT_ID}`以及容器的概念，請參閱開發人員指南的[快速入門](../xdm/api/getting-started.md)一節。

您可以向[!DNL Schema Registry] API中的`/descriptors`端點提出POST要求，將身分描述元新增至資料集的XDM架構。

**API格式**

```http
POST /descriptors
```

**要求**

以下請求在示例架構的「電子郵件地址」欄位中定義標識描述符。

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
| `@type` | 要建立的描述符的類型。 對於身分描述元，值必須是&quot;xdm:descriptorIdentity&quot;。 |
| `xdm:sourceSchema` | 資料集XDM架構的唯一URI ID。 |
| `xdm:sourceVersion` | `xdm:sourceSchema`中指定的XDM架構版本。 |
| `xdm:sourceProperty` | 應用描述符的架構欄位的路徑。 |
| `xdm:namespace` | 由[!DNL Privacy Service]識別的[標準身分命名空間之一](../privacy-service/api/appendix.md#standard-namespaces)，或由您的組織定義的自訂命名空間。 |
| `xdm:property` | 視`xdm:namespace`下使用的命名空間而定，可以是&quot;xdm:id&quot;或&quot;xdm:code&quot;。 |
| `xdm:isPrimary` | 選用的布林值。 若為true，表示欄位為主要身分。 結構只能包含一個主要身分。 若未包含，則預設為false。 |

**回應**

成功的響應返回HTTP狀態201（已建立）以及新建立描述符的詳細資訊。

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

>[!NOTE]
>
>本節說明如何設定[!DNL Data Lake]隱私權要求的格式。 強烈建議您檢閱[[!DNL Privacy Service] UI](../privacy-service/ui/overview.md)或[[!DNL Privacy Service] API](../privacy-service/api/getting-started.md)檔案，以取得如何提交隱私權工作的完整步驟，包括如何在要求負載中正確格式化已提交的使用者身分資料。

以下章節概述如何使用[!DNL Privacy Service] UI或API，為[!DNL Data Lake]提出隱私權要求。

>[!IMPORTANT]
>
>無法保證隱私權要求完成所需的時間。 如果在資料湖內發生變更，而請求仍在處理中，則無法保證會處理這些記錄。

### 使用UI

在UI中建立作業請求時，請務必在&#x200B;**[!UICONTROL Products]**&#x200B;下選取&#x200B;**[!UICONTROL AEP Data Lake]**&#x200B;和/或&#x200B;**[!UICONTROL Profile]**，以便分別處理儲存在[!DNL Data Lake]或[!DNL Real-time Customer Profile]中之資料的作業。

<img src="images/privacy/product-value.png" width="450"><br>

### 使用 API

在API中建立作業請求時，提供的任何`userIDs`都必鬚根據它們所套用的資料存放區使用特定的`namespace`和`type`。 [!DNL Data Lake]的ID必須對其`type`值使用「未註冊」，且`namespace`值與已新增至適用資料集的[隱私權標籤](#privacy-labels)中的一個值相符。

此外，請求裝載的`include`陣列必須包含對請求進行之不同資料存放區的產品值。 向[!DNL Data Lake]提出請求時，陣列必須包含值`aepDataLake`。

以下請求使用未註冊的「email_label」命名空間為[!DNL Data Lake]建立新的隱私權作業。 也包含`include`陣列中[!DNL Data Lake]的產品值：

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

當[!DNL Experience Platform]收到來自[!DNL Privacy Service]的刪除請求時， [!DNL Platform]向[!DNL Privacy Service]發送確認，確認已接收該請求，且受影響的資料已標籤為刪除。 之後，會在七天內從[!DNL Data Lake]中移除記錄。 在該七天期間，資料會遭軟刪除，因此任何[!DNL Platform]服務都無法存取。

在未來版本中，在實際刪除資料後， [!DNL Platform]將向[!DNL Privacy Service]發送確認。

## 後續步驟

閱讀本檔案後，您便了解處理[!DNL Data Lake]隱私權要求的相關重要概念。 建議您繼續閱讀本指南中提供的檔案，以深入了解如何管理身分資料和建立隱私權工作。

如需處理[!DNL Profile]商店隱私權要求的步驟，請參閱[即時客戶設定檔的隱私權要求處理相關檔案](../profile/privacy.md)。

## 附錄

以下章節包含處理[!DNL Data Lake]中隱私權要求的其他資訊。

### 標籤嵌套映射類型欄位{#nested-maps}

請務必注意，有兩種巢狀映射類型欄位不支援隱私權標籤：

* 陣列類型欄位內的映射類型欄位
* 另一個映射類型欄位中的映射類型欄位

上述兩個範例中任何一個的隱私權工作處理最終都會失敗。 因此，建議您避免使用巢狀對應類型欄位來儲存私人客戶資料。 對於記錄型資料集，相關消費者ID應儲存為`identityMap`欄位內的非映射資料類型（本身為映射類型欄位），或者對於時間序列型資料集，應將`endUserID`欄位儲存為。
