---
keywords: Experience Platform；首頁；熱門主題；資料湖隱私權；身分名稱空間；隱私權；資料湖
solution: Experience Platform
title: Data Lake中的隱私權請求處理
description: Adobe Experience Platform Privacy Service會根據法律和組織隱私權法規，處理客戶存取、選擇退出銷售或刪除其個人資料的請求。 本檔案說明與處理儲存在Data Lake中之客戶資料的隱私權請求相關的重要概念。
exl-id: c06b0a44-be1a-4938-9c3e-f5491a3dfc19
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '1430'
ht-degree: 1%

---

# 資料湖中的隱私權請求處理

Adobe Experience Platform [!DNL Privacy Service]會根據法律和組織隱私權法規的規定，處理客戶存取、選擇退出銷售或刪除其個人資料的請求。

本檔案說明與處理儲存在Data Lake中之客戶資料的隱私權請求相關的重要概念。

>[!NOTE]
>
>本指南僅涵蓋如何在Experience Platform中提出資料湖的隱私權請求。 如果您也打算向即時客戶設定檔資料存放區提出隱私權請求，除了本教學課程外，另請參閱有關為設定檔[&#128279;](../profile/privacy.md)處理隱私權請求的指南。
>
>如需如何對其他Adobe Experience Cloud應用程式提出隱私權要求的步驟，請參閱[Privacy Service檔案](../privacy-service/experience-cloud-apps.md)。

## 快速入門

在閱讀本指南之前，建議您實際瞭解下列[!DNL Experience Platform]服務：

* [[!DNL Privacy Service]](../privacy-service/home.md)：管理客戶透過Adobe Experience Cloud應用程式存取、選擇退出銷售或刪除其個人資料的請求。
* [[!DNL Catalog Service]](home.md)： [!DNL Experience Platform]內資料位置和歷程的記錄系統。 提供可用於更新資料集中繼資料的API。
* [[!DNL Experience Data Model (XDM) System]](../xdm/home.md)： [!DNL Experience Platform]用來組織客戶體驗資料的標準化架構。
* [[!DNL Identity Service]](../identity-service/home.md)：透過跨裝置和系統橋接身分，解決客戶體驗資料分散所造成的根本挑戰。

## 了解身分識別命名空間 {#namespaces}

Adobe Experience Platform [!DNL Identity Service]可跨系統和裝置橋接客戶身分資料。 [!DNL Identity Service]使用身分識別名稱空間，透過將身分識別值與其來源系統建立關聯來提供身分識別值的內容。 名稱空間可代表一般概念，例如電子郵件地址（「電子郵件」），或將身分與特定應用程式相關聯，例如Adobe Advertising Cloud ID (「AdCloud」)或Adobe Target ID (「TNTID」)。

[!DNL Identity Service]會維護全域定義（標準）和使用者定義（自訂）的身分名稱空間存放區。 標準名稱空間適用於所有組織（例如「Email」和「ECID」），而您的組織也可以建立自訂名稱空間以滿足其特定需求。

如需[!DNL Experience Platform]中識別名稱空間的詳細資訊，請參閱[識別名稱空間概觀](../identity-service/features/namespaces.md)。

## 將身分資料新增至資料集

為Data Lake建立隱私權要求時，必須為每位客戶提供有效的身分值（及其關聯的名稱空間），以便找到其資料並據以處理。 因此，所有遵循隱私權要求的資料集都必須在其相關聯的XDM結構描述中包含身分描述項。

>[!NOTE]
>
>任何以不支援身分描述項中繼資料的結構描述為基礎的資料集（例如臨時資料集），目前都無法在隱私權要求中處理。

本節逐步說明將身分描述項新增至現有資料集的XDM結構描述的步驟。 如果您已經有具有身分描述項的資料集，您可以跳至[下一節](#nested-maps)。

>[!IMPORTANT]
>
>在決定要將哪些結構描述欄位設定為身分時，請記得使用巢狀對應型別欄位的[限制](#nested-maps)。

將身分描述項新增到資料集結構描述的方法有兩種：

* [使用UI](#identity-ui)
* [使用 API](#identity-api)

### 使用UI {#identity-ui}

在[!DNL Experience Platform]使用者介面中，**[!UICONTROL 方案]**&#x200B;工作區可讓您編輯現有的XDM方案。 若要將身分描述項新增至結構描述，請從清單中選取結構描述，並按照[!DNL Schema Editor]教學課程中[將結構描述欄位設定為身分欄位](../xdm/tutorials/create-schema-ui.md#identity-field)的步驟操作。

一旦您在結構描述中將適當的欄位設定為身分欄位後，您就可以繼續進行[提交隱私權要求](#submit)的下一節。

### 使用 API {#identity-api}

>[!NOTE]
>
>本節假設您知道資料集XDM結構的唯一URI ID值。 如果您不知道此值，可以使用[!DNL Catalog Service] API擷取它。 閱讀開發人員指南的[快速入門](./api/getting-started.md)區段後，請依照中概述的步驟，針對[清單](./api/list-objects.md)或[查詢](./api/look-up-object.md) [!DNL Catalog]物件以尋找您的資料集。 結構描述ID可以在`schemaRef.id`下找到
>
>本節也假設您知道如何呼叫Schema Registry API。 如需與使用API相關的重要資訊，包括瞭解您的`{TENANT_ID}`和容器的概念，請參閱API指南的[快速入門](../xdm/api/getting-started.md)一節。

您可以對[!DNL Schema Registry] API中的`/descriptors`端點發出POST要求，藉此將身分描述項新增至資料集的XDM結構描述。

**API格式**

```http
POST /descriptors
```

**要求**

以下請求在範例結構描述中的「電子郵件地址」欄位上定義身分描述項。

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
| `@type` | 正在建立的描述項型別。 對於身分描述項，值必須是&quot;xdm：descriptorIdentity&quot;。 |
| `xdm:sourceSchema` | 資料集XDM結構的唯一URI ID。 |
| `xdm:sourceVersion` | 在`xdm:sourceSchema`中指定的XDM結構描述版本。 |
| `xdm:sourceProperty` | 要套用描述項的結構描述欄位路徑。 |
| `xdm:namespace` | [!DNL Privacy Service]可辨識的[標準身分名稱空間](../privacy-service/api/appendix.md#standard-namespaces)之一，或貴組織定義的自訂名稱空間。 |
| `xdm:property` | 「xdm：id」或「xdm：code」，取決於`xdm:namespace`下使用的名稱空間。 |
| `xdm:isPrimary` | 選用的布林值。 為true時，表示欄位是主要身分。 結構描述只能包含一個主要身分。 若未包含，則預設為false 。 |

**回應**

成功的回應會傳回HTTP狀態201 （已建立）和新建立之描述項的詳細資訊。

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
>本節說明如何格式化Data Lake的隱私權請求。 強烈建議您檢閱[[!DNL Privacy Service] UI](../privacy-service/ui/overview.md)或[[!DNL Privacy Service] API](../privacy-service/api/getting-started.md)檔案，以取得有關如何提交隱私權工作的完整步驟，包括如何在要求裝載中正確格式化提交的使用者身分資料。

以下章節概述如何使用[!DNL Privacy Service] UI或API向Data Lake提出隱私權請求。

>[!IMPORTANT]
>
>無法保證完成隱私權要求所需的時間。 如果變更發生在請求仍在處理期間的Data Lake內，則也無法保證這些記錄是否會處理。

### 使用UI

在UI中建立工作請求時，請務必在&#x200B;**[!UICONTROL 產品]**&#x200B;下選取&#x200B;**[!UICONTROL AEP Data Lake]**，以便處理儲存在Data Lake中之資料的工作。

![顯示隱私權請求建立對話方塊中選取之資料湖產品的影像](./images/privacy/product-value.png)

### 使用 API

在API中建立工作請求時，提供的任何`userIDs`都必須根據其套用的資料存放區使用特定的`namespace`和`type`。 資料湖的ID必須使用`unregistered`做為其`type`值，以及符合已新增至適用資料集之[隱私權標籤](#privacy-labels)的`namespace`值。

此外，請求承載的`include`陣列必須包含請求所針對的不同資料存放區的產品值。 向資料湖提出請求時，陣列必須包含值`aepDataLake`。

以下請求會使用未註冊的`email_label`名稱空間，為資料湖建立新的隱私權工作。 它也會包含`include`陣列中資料湖的產品值：

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
>Experience Platform會處理屬於您組織的所有[沙箱](../sandboxes/home.md)的隱私權請求。 因此，請求中包含的任何`x-sandbox-name`標頭都會被系統忽略。

## 正在處理刪除請求

當[!DNL Experience Platform]收到來自[!DNL Privacy Service]的刪除請求時，[!DNL Experience Platform]會傳送確認給[!DNL Privacy Service]，確認已收到該請求且受影響的資料已標示為刪除。 這些記錄接著會在七天內從資料湖中移除。 在這七天期間，資料會軟刪除，因此無法由任何[!DNL Experience Platform]服務存取。

如果您也將`ProfileService`或`identity`包含在隱私權請求中，則會分別處理其相關資料。 如需詳細資訊，請參閱有關設定檔[&#128279;](../profile/privacy.md#delete)的刪除請求處理的章節。

## 後續步驟

閱讀本檔案後，您便可瞭解處理Data Lake隱私權請求的重要概念。 建議您繼續閱讀本指南提供的檔案，以加深您對如何管理身分資料和建立隱私權工作的瞭解。

如需處理[!DNL Profile]存放區之隱私權要求的步驟，請參閱即時客戶設定檔[&#128279;](../profile/privacy.md)的隱私權要求處理檔案。

## 附錄

下節包含在Data Lake中處理隱私權請求的其他資訊。

### 標籤巢狀對應型別欄位 {#nested-maps}

請務必注意，有兩種巢狀對應型別欄位不支援隱私權標籤：

* 陣列型別欄位中的對應型別欄位
* 另一個對應型別欄位中的對應型別欄位

上述兩個範例的隱私權工作處理最終都將失敗。 因此，建議您避免使用巢狀對應型別欄位來儲存私人客戶資料。 對於以記錄為基礎的資料集，相關的消費者ID應該以非對應資料型別的形式儲存在`identityMap`欄位中（本身是對應型別欄位），或是以時間序列為基礎的資料集的`endUserID`欄位中。
