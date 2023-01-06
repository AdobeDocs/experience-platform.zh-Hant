---
keywords: Experience Platform；首頁；熱門主題；資料湖隱私權；身分命名空間；隱私權；資料湖
solution: Experience Platform
title: 資料湖的隱私權要求處理
description: Adobe Experience Platform Privacy Service會處理客戶要求存取、選擇退出銷售或刪除其個人資料（如法律和組織隱私權法規所規定）。 本檔案涵蓋與處理資料湖中儲存之客戶資料的隱私權要求相關的基本概念。
exl-id: c06b0a44-be1a-4938-9c3e-f5491a3dfc19
source-git-commit: 74867f56ee13430cbfd9083a916b7167a9a24c01
workflow-type: tm+mt
source-wordcount: '1428'
ht-degree: 1%

---

# 資料湖的隱私權要求處理

Adobe Experience Platform [!DNL Privacy Service] 處理客戶要求存取、選擇退出銷售或刪除法律和組織隱私權法規所規定之個人資料的請求。

本檔案涵蓋與處理資料湖中儲存之客戶資料的隱私權要求相關的基本概念。

>[!NOTE]
>
>本指南僅說明如何針對Experience Platform中的資料湖提出隱私權要求。 如果您也打算向即時客戶設定檔資料存放區提出隱私權要求，請參閱 [設定檔的隱私權要求處理](../profile/privacy.md) 除了本教學課程之外。
>
>如需如何為其他Adobe Experience Cloud應用程式提出隱私權要求的步驟，請參閱 [Privacy Service檔案](../privacy-service/experience-cloud-apps.md).

## 快速入門

建議您對下列事項有切實的了解 [!DNL Experience Platform] 服務，再閱讀本指南：

* [[!DNL Privacy Service]](../privacy-service/home.md):管理客戶在Adobe Experience Cloud應用程式中存取、選擇退出銷售或刪除其個人資料的請求。
* [[!DNL Catalog Service]](home.md):資料位置和內宗記錄系統 [!DNL Experience Platform]. 提供可用來更新資料集中繼資料的API。
* [[!DNL Experience Data Model (XDM) System]](../xdm/home.md):標準化框架 [!DNL Experience Platform] 組織客戶體驗資料。
* [[!DNL Identity Service]](../identity-service/home.md):通過跨裝置和系統橋接身分，解決客戶體驗資料分散帶來的根本難題。

## 了解身分識別命名空間 {#namespaces}

Adobe Experience Platform [!DNL Identity Service] 橋接跨系統和裝置的客戶身分資料。 [!DNL Identity Service] 使用身分識別命名空間，將身分識別值與來源系統關聯，以提供內容與身分識別值。 命名空間可代表一般概念，例如電子郵件地址（「電子郵件」），或將身分識別與特定應用程式建立關聯，例如Adobe Advertising Cloud ID(「AdCloud」)或Adobe Target ID(「TNTID」)。

[!DNL Identity Service] 維護全域定義（標準）和使用者定義（自訂）身分識別命名空間的存放區。 所有組織皆可使用標準命名空間（例如「電子郵件」和「ECID」），而您的組織也可以建立自訂命名空間，以符合其特定需求。

如需中身分識別命名空間的詳細資訊，請參閱 [!DNL Experience Platform]，請參閱 [身分命名空間概述](../identity-service/namespaces.md).

## 將身分資料新增至資料集

為資料湖建立隱私權要求時，必須為每個個別客戶提供有效的身分值（及其相關的命名空間），以便找到其資料並據以處理。 因此，所有受隱私權要求約束的資料集，都必須在其相關聯的XDM結構中包含身分描述元。

>[!NOTE]
>
>目前無法在隱私權要求中處理任何以結構為基礎但不支援身分描述元資料的資料集（例如臨機資料集）。

本節將逐步說明將身分描述元新增至現有資料集的XDM架構的步驟。 如果您已有具有身分描述元的資料集，可以跳至 [下一節](#nested-maps).

>[!IMPORTANT]
>
>決定要設為身分的結構欄位時，請記住 [使用嵌套映射類型欄位的限制](#nested-maps).

將身分描述符新增至資料集架構有兩種方法：

* [使用UI](#identity-ui)
* [使用 API](#identity-api)

### 使用UI {#identity-ui}

在 [!DNL Experience Platform ]使用者介面、 **[!UICONTROL 結構]** 工作區可讓您編輯現有的XDM結構。 要向架構添加標識描述符，請從清單中選擇該架構，並按照 [將架構欄位設定為身分欄位](../xdm/tutorials/create-schema-ui.md#identity-field) 在 [!DNL Schema Editor] 教學課程。

在您將結構中的適當欄位設為身分欄位後，您可以繼續前往 [提交隱私權要求](#submit).

### 使用 API {#identity-api}

>[!NOTE]
>
>本節假設您知道資料集XDM架構的唯一URI ID值。 如果您不知道此值，可使用 [!DNL Catalog Service] API。 閱讀 [快速入門](./api/getting-started.md) 依照 [清單](./api/list-objects.md) 或 [查找](./api/look-up-object.md) [!DNL Catalog] 物件，以尋找資料集。 結構ID位於 `schemaRef.id`
>
>本節亦假設您知道如何呼叫結構註冊表API。 如需與使用API相關的重要資訊，包括了解您的 `{TENANT_ID}` 容器的概念，請參閱 [快速入門](../xdm/api/getting-started.md) 一節。

您可以向 `/descriptors` 端點 [!DNL Schema Registry] API。

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
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
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
| `xdm:sourceVersion` | 指定的XDM架構版本(於 `xdm:sourceSchema`. |
| `xdm:sourceProperty` | 應用描述符的架構欄位的路徑。 |
| `xdm:namespace` | 其中 [標準身分命名空間](../privacy-service/api/appendix.md#standard-namespaces) 確認 [!DNL Privacy Service]，或貴組織定義的自訂命名空間。 |
| `xdm:property` | 「xdm:id」或「xdm:code」，視下使用的命名空間而定 `xdm:namespace`. |
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
>本節說明如何設定資料湖的隱私權要求格式。 強烈建議您檢閱 [[!DNL Privacy Service] UI](../privacy-service/ui/overview.md) 或 [[!DNL Privacy Service] API](../privacy-service/api/getting-started.md) 說明檔案，以取得如何提交隱私權工作的完整步驟，包括如何在要求負載中正確格式化已提交的使用者身分資料。

以下章節概述如何使用 [!DNL Privacy Service] UI或API。

>[!IMPORTANT]
>
>無法保證隱私權要求完成所需的時間。 如果在資料湖內發生變更，而請求仍在處理中，也無法保證這些記錄是否已處理。

### 使用UI

在UI中建立工作請求時，請務必選取 **[!UICONTROL AEP Data Lake]** 在 **[!UICONTROL 產品]** 以便處理資料湖中儲存的資料作業。

![顯示隱私權請求建立對話方塊中選取之資料湖產品的影像](./images/privacy/product-value.png)

### 使用 API

在API中建立工作請求時，任何 `userIDs` 提供的必須使用特定 `namespace` 和 `type` 視其套用的資料存放區而定。 資料湖的ID必須使用 `unregistered` 為 `type` 值和 `namespace` 與 [隱私權標籤](#privacy-labels) 已新增至適用資料集的資料集。

此外， `include` 要求裝載的陣列必須包含要提出要求之不同資料存放區的產品值。 向資料湖提出請求時，陣列必須包含值 `aepDataLake`.

以下請求會使用未註冊的 `email_label` 命名空間。 也包含資料湖的產品值，位於 `include` 陣列：

```shell
curl -X POST \
  https://platform.adobe.io/data/core/privacy/jobs \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'Content-Type: application/json' \
  -d '{
    "companyContexts": [
      {
        "namespace": "imsOrgID",
        "value": "{ORG_ID}"
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

>[!IMPORTANT]
>
>Platform可處理所有 [沙箱](../sandboxes/home.md) 屬於您的組織。 因此，任何 `x-sandbox-name` 系統會忽略請求中包含的標題。

## 刪除請求處理

當 [!DNL Experience Platform] 從接收刪除請求 [!DNL Privacy Service], [!DNL Platform] 發送確認 [!DNL Privacy Service] 已收到請求，且受影響的資料已標示為刪除。 七天內會從資料湖中移除記錄。 在這七天期間，資料會遭軟性刪除，因此無法供任何使用者存取 [!DNL Platform] 服務。

如果您也包含 `ProfileService` 或 `identity` 在隱私權要求中，會個別處理其相關資料。 請參閱 [刪除設定檔的請求處理](../profile/privacy.md#delete) 以取得更多資訊。

## 後續步驟

閱讀本檔案後，您便了解處理資料湖隱私權要求的相關重要概念。 建議您繼續閱讀本指南中提供的檔案，以深入了解如何管理身分資料和建立隱私權工作。

請參閱 [即時客戶設定檔的隱私權要求處理](../profile/privacy.md) 的隱私權要求處理步驟 [!DNL Profile] 儲存。

## 附錄

以下章節包含在資料湖中處理隱私權要求的其他資訊。

### 標籤巢狀映射類型欄位 {#nested-maps}

請務必注意，有兩種巢狀映射類型欄位不支援隱私權標籤：

* 陣列類型欄位內的映射類型欄位
* 另一個映射類型欄位中的映射類型欄位

上述兩個範例中任何一個的隱私權工作處理最終都會失敗。 因此，建議您避免使用巢狀對應類型欄位來儲存私人客戶資料。 相關消費者ID應儲存為 `identityMap` 欄位（本身為對應類型欄位），用於記錄資料集，或 `endUserID` 時間系列資料集的欄位。
