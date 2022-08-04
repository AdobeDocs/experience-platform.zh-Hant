---
keywords: Experience Platform；主題；熱門主題；資料湖隱私；標識命名空間；隱私；資料湖
solution: Experience Platform
title: 資料湖中的隱私請求處理
topic-legacy: overview
description: Adobe Experience Platform Privacy Service處理客戶訪問、選擇不銷售或刪除其根據法律和組織隱私法規規定的個人資料的請求。 本文檔涵蓋與處理儲存在資料湖中的客戶資料的隱私請求相關的基本概念。
exl-id: c06b0a44-be1a-4938-9c3e-f5491a3dfc19
source-git-commit: 159a46fa227207bf161100e50bc286322ba2d00b
workflow-type: tm+mt
source-wordcount: '1428'
ht-degree: 1%

---

# 資料湖中的隱私請求處理

Adobe Experience Platform [!DNL Privacy Service] 處理客戶訪問請求、選擇不銷售或刪除其根據法律和組織隱私法規規定的個人資料。

本文檔涵蓋與處理儲存在資料湖中的客戶資料的隱私請求相關的基本概念。

>[!NOTE]
>
>本指南僅介紹如何對Experience Platform中的資料湖進行隱私請求。 如果您還計畫對即時客戶配置檔案資料儲存進行隱私請求，請參閱上的指南 [配置檔案的隱私請求處理](../profile/privacy.md) 除本教程外。
>
>有關如何對其他Adobe Experience Cloud應用程式發出隱私請求的步驟，請參閱 [Privacy Service文檔](../privacy-service/experience-cloud-apps.md)。

## 快速入門

建議您對以下內容有正確理解 [!DNL Experience Platform] 服務，然後閱讀本指南。

* [[!DNL Privacy Service]](../privacy-service/home.md):管理客戶跨Adobe Experience Cloud應用程式訪問、選擇退出銷售或刪除其個人資料的請求。
* [[!DNL Catalog Service]](home.md):資料位置和沿襲的記錄系統 [!DNL Experience Platform]。 提供可用於更新資料集元資料的API。
* [[!DNL Experience Data Model (XDM) System]](../xdm/home.md):標準化框架 [!DNL Experience Platform] 組織客戶體驗資料。
* [[!DNL Identity Service]](../identity-service/home.md):通過跨設備和系統橋接身份，解決客戶體驗資料碎片化帶來的根本難題。

## 瞭解標識命名空間 {#namespaces}

Adobe Experience Platform [!DNL Identity Service] 跨系統和設備橋接客戶身份資料。 [!DNL Identity Service] 使用標識命名空間將標識值與其源系統相關聯，從而為標識值提供上下文。 命名空間可以表示一個通用概念，如電子郵件地址（「電子郵件」），或將標識與特定應用程式(如Adobe Advertising CloudID(「AdCloud」)或Adobe TargetID(「TNTID」))關聯。

[!DNL Identity Service] 維護全局定義（標準）和用戶定義（自定義）標識命名空間的儲存。 標準命名空間適用於所有組織（例如，「電子郵件」和「ECID」），而您的組織也可以建立自定義命名空間以滿足其特定需求。

有關中標識命名空間的詳細資訊 [!DNL Experience Platform]，請參見 [標識命名空間概述](../identity-service/namespaces.md)。

## 向資料集添加標識資料

在為資料湖建立隱私請求時，必須為每個客戶提供有效的標識值（及其關聯的命名空間），以便找到其資料並相應地處理它。 因此，所有受隱私請求約束的資料集都必須在其關聯的XDM架構中包含標識描述符。

>[!NOTE]
>
>當前無法在隱私請求中處理任何基於方案且不支援身份描述符元資料（如臨時資料集）的資料集。

本節將介紹向現有資料集的XDM架構中添加標識描述符的步驟。 如果已有帶有標識描述符的資料集，則可以跳到 [下一部分](#nested-maps)。

>[!IMPORTANT]
>
>在確定要設定為標識的架構欄位時，請記住 [使用嵌套映射類型欄位的限制](#nested-maps)。

向資料集模式添加標識描述符有兩種方法：

* [使用UI](#identity-ui)
* [使用 API](#identity-api)

### 使用UI {#identity-ui}

在 [!DNL Experience Platform ]用戶介面， **[!UICONTROL 架構]** 工作區允許您編輯現有XDM架構。 要向架構添加標識描述符，請從清單中選擇該架構，然後按照 [將架構欄位設定為標識欄位](../xdm/tutorials/create-schema-ui.md#identity-field) 的 [!DNL Schema Editor] 教程。

在將架構中的相應欄位設定為標識欄位後，可以繼續下一節。 [提交隱私請求](#submit)。

### 使用 API {#identity-api}

>[!NOTE]
>
>本節假定您知道資料集的XDM架構的唯一URI ID值。 如果不知道此值，則可以使用 [!DNL Catalog Service] API。 讀完 [開始](./api/getting-started.md) 的「Developer Guide（開發人員指南）」部分，按照中概述的步驟操作 [上市](./api/list-objects.md) 或 [查看](./api/look-up-object.md) [!DNL Catalog] 對象以查找您的資料集。 可以在以下位置找到架構ID `schemaRef.id`
>
>本節還假定您知道如何調用架構註冊表API。 有關使用API的重要資訊，包括瞭解您 `{TENANT_ID}` 和容器的概念，請參閱 [開始](../xdm/api/getting-started.md) 的下界。

可以通過向以下對象發出POST請求，將標識描述符添加到資料集的XDM架構 `/descriptors` 端點 [!DNL Schema Registry] API。

**API格式**

```http
POST /descriptors
```

**要求**

以下請求在示例架構的「電子郵件地址」欄位上定義標識描述符。

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
| `@type` | 正在建立的描述符的類型。 對於標識描述符，值必須為&quot;xdm:descriptorIdentity&quot;。 |
| `xdm:sourceSchema` | 資料集的XDM架構的唯一URI ID。 |
| `xdm:sourceVersion` | 中指定的XDM架構的版本 `xdm:sourceSchema`。 |
| `xdm:sourceProperty` | 描述符要應用到的架構欄位的路徑。 |
| `xdm:namespace` | 其中 [標準標識命名空間](../privacy-service/api/appendix.md#standard-namespaces) 確認 [!DNL Privacy Service]，或由您的組織定義的自定義命名空間。 |
| `xdm:property` | 「xdm:id」或「xdm:code」，具體取決於在 `xdm:namespace`。 |
| `xdm:isPrimary` | 可選布爾值。 如果為true，則表示該欄位是主標識。 架構只能包含一個主標識。 如果未包括，則預設為false。 |

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

>[!NOTE]
>
>本節介紹如何格式化資料湖的隱私請求。 強烈建議您查看 [[!DNL Privacy Service] UI](../privacy-service/ui/overview.md) 或 [[!DNL Privacy Service] API](../privacy-service/api/getting-started.md) 有關如何提交隱私作業的完整步驟的文檔，包括如何在請求負載中正確格式化已提交的用戶標識資料。

以下部分概述如何使用 [!DNL Privacy Service] UI或API。

>[!IMPORTANT]
>
>無法保證隱私請求完成所花的時間。 如果在請求仍在處理期間資料湖中發生更改，則也無法保證是否處理這些記錄。

### 使用UI

在UI中建立作業請求時，請確保選擇 **[!UICONTROL AEP資料湖]** 在 **[!UICONTROL 產品]** 以處理儲存在資料湖中的資料的作業。

![顯示在隱私請求建立對話框中選擇的資料湖產品的影像](./images/privacy/product-value.png)

### 使用 API

在API中建立作業請求時， `userIDs` 必須使用特定 `namespace` 和 `type` 取決於它們所應用的資料儲存。 資料湖的ID必須使用 `unregistered` 為 `type` 值和 `namespace` 與其匹配的值 [隱私標籤](#privacy-labels) 已添加到適用資料集。

另外， `include` 請求負載的陣列必須包括請求所針對的不同資料儲存的產品值。 在向資料湖請求時，陣列必須包括值 `aepDataLake`。

以下請求使用未註冊的資料湖建立新的隱私作業 `email_label` 命名空間。 還包括資料湖的產品價值。 `include` 陣列：

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
>平台處理跨所有 [沙箱](../sandboxes/home.md) 屬於您的組織。 因此， `x-sandbox-name` 系統將忽略請求中包含的標頭。

## 刪除請求處理

當 [!DNL Experience Platform] 從接收刪除請求 [!DNL Privacy Service]。 [!DNL Platform] 發送確認 [!DNL Privacy Service] 已接收請求並且已將受影響資料標籤為刪除。 然後，在七天內將記錄從資料庫中刪除。 在這七天的窗口期間，資料被軟刪除，因此無法由任何 [!DNL Platform] 服務。

如果還包括 `ProfileService` 或 `identity` 在隱私請求中，其關聯資料被單獨處理。 請參閱 [刪除配置檔案的請求處理](../profile/privacy.md#delete) 的子菜單。

## 後續步驟

通過閱讀本文檔，您已瞭解處理資料湖隱私請求所涉及的重要概念。 建議您繼續閱讀本指南中提供的文檔，以加深對如何管理身份資料和建立隱私作業的理解。

查看上的文檔 [即時客戶配置檔案的隱私請求處理](../profile/privacy.md) 有關處理隱私請求的步驟 [!DNL Profile] 商店。

## 附錄

以下部分包含處理資料湖中的隱私請求的附加資訊。

### 標籤嵌套的映射類型欄位 {#nested-maps}

請注意，有兩種嵌套的映射類型欄位不支援隱私標籤：

* 陣列類型欄位中的映射類型欄位
* 另一個映射類型欄位中的映射類型欄位

以上兩個示例中的任何一個的隱私作業處理最終都會失敗。 因此，建議避免使用嵌套的映射類型欄位來儲存私人客戶資料。 相關使用者ID應儲存為非映射資料類型 `identityMap` 欄位（本身是映射類型欄位），用於記錄資料集，或 `endUserID` 欄位。
