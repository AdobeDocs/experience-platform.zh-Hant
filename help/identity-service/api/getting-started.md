---
keywords: Experience Platform；首頁；熱門主題；身份服務api；身份服務開發人員指南；地區
solution: Experience Platform
title: Identity Service API指南
topic: API guide
description: Identity Service API可讓開發人員使用Adobe Experience Platform的身分圖表，管理客戶的跨裝置、跨通道和近乎即時的身分識別。 請依照本指南，瞭解如何使用API執行關鍵作業。
translation-type: tm+mt
source-git-commit: 69c3106070e31377ea8571cd14dc33aa9b6f7037
workflow-type: tm+mt
source-wordcount: '773'
ht-degree: 0%

---


# [!DNL Identity Service] API指南

Adobe Experience Platform[!DNL Identity Service]管理跨裝置、跨通道和近乎即時的客戶識別，在Adobe Experience Platform稱為身份圖。

## 快速入門

本指南需要對Adobe Experience Platform的下列組成部分有切實的瞭解：

- [[!DNL Identity Service]](../home.md):解決客戶個人檔案資料分散所帶來的根本挑戰。它可跨裝置和系統橋接身分，讓客戶與您的品牌互動。
- [[!DNL Real-time Customer Profile]](../../profile/home.md):根據來自多個來源的匯整資料，即時提供統一的消費者個人檔案。
- [[!DNL Experience Data Model (XDM)]](../../xdm/home.md):組織客戶體驗資 [!DNL Platform] 料的標準化架構。

以下各節提供您必須知道或掌握的額外資訊，才能成功呼叫[!DNL Identity Service] API。

### 讀取範例API呼叫

本指南提供範例API呼叫，以示範如何格式化您的請求。 這些包括路徑、必要標題和正確格式化的請求負載。 也提供API回應中傳回的範例JSON。 如需範例API呼叫檔案中所用慣例的詳細資訊，請參閱[!DNL Experience Platform]疑難排解指南中[如何讀取範例API呼叫](../../landing/troubleshooting.md#how-do-i-format-an-api-request)一節。

### 收集必要標題的值

若要呼叫[!DNL Platform] API，您必須先完成[驗證教學課程](https://www.adobe.com/go/platform-api-authentication-en)。 完成驗證教學課程後，所有[!DNL Experience Platform] API呼叫中每個所需標題的值都會顯示在下面：

- 授權：載體`{ACCESS_TOKEN}`
- x-api-key:`{API_KEY}`
- x-gw-ims-org-id:`{IMS_ORG}`

[!DNL Experience Platform]中的所有資源都隔離到特定的虛擬沙盒。 對[!DNL Platform] API的所有請求都需要一個標題，該標題指定要在中執行操作的沙盒的名稱：

- x-sandbox-name:`{SANDBOX_NAME}`

>[!NOTE]
>
>如需[!DNL Platform]中沙盒的詳細資訊，請參閱[沙盒概述檔案](../../sandboxes/home.md)。

所有包含裝載(POST、PUT、PATCH)的請求都需要額外的標題：

- 內容類型：application/json

### 基於區域的路由

[!DNL Identity Service] API採用區域特定端點，要求在請求路徑中加入`{REGION}`。 在IMS組織布建期間，會決定地區並儲存在IMS組織描述檔中。 使用每個端點的正確區域可確保使用[!DNL Identity Service] API提出的所有請求都路由到適當的區域。

[!DNL Identity Service] API目前支援兩個地區：VA7和NLD2。

下表顯示了使用區域的示例路徑：

| 服務 | 地區：VA7 | 地區：NLD2 |
| ------ | -------- |--------- |
| [!DNL Identity Service] API | https://</span>platform-va7.adobe。</span>io/data/core/identity/{ENDPOINT} | https://</span>platform-nld2.adobe。</span>io/data/core/identity/{ENDPOINT} |
| [!DNL Identity Namespace] API | https://</span>platform-va7.adobe。</span>io/data/core/idnamespace/{ENDPOINT} | https://</span>platform-nld2.adobe。</span>io/data/core/idnamespace{ENDPOINT} |

>[!NOTE]
>
>未指定區域的請求可能導致呼叫路由到錯誤區域，或導致呼叫意外失敗。

如果您無法在IMS組織設定檔中找到地區，請聯絡您的系統管理員以取得支援。

## 使用[!DNL Identity Service] API

這些服務中使用的身份參數可以用兩種方式之一表示；複合或XID。

複合身份是包括ID值和命名空間的構造。 使用複合身份時，可以通過名稱(`namespace.code`)或ID(`namespace.id`)提供命名空間。

當身分持續存在時，[!DNL Identity Service]會產生ID並指派給該身分，稱為原生ID或XID。 所有群集和映射API的變體在其請求和響應中都支援組合身份和XID。 其中一個參數是必需的- `xid`或[`ns`或`nsid`]和`id`的組合才能使用這些API。

為了限制回應中的負載，API會根據使用的身分建構類型來調整其回應。 也就是說，如果您傳遞XID，您的回應會有XID，如果您傳遞複合身分，則回應會遵循請求中使用的結構。

本文中的範例不涵蓋[!DNL Identity Service] API的完整功能。 如需完整的API，請參閱[Swagger API參考](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/id-service-api.yaml)。

>[!NOTE]
>
>在請求中使用原生XID時，傳回的所有身分都會以原生XID格式。 建議使用ID/namespace表單。 如需詳細資訊，請參閱[取得身分識別的XID一節。](./create-custom-namespace.md)

## 後續步驟

現在您已收集到必要的認證，您可以繼續閱讀其餘的開發人員指南。 每個區段都提供其端點的重要資訊，並示範執行CRUD作業的範例API呼叫。 每個呼叫都包含一般API格式、顯示必要標題和正確格式化負載的範例要求，以及成功呼叫的範例回應。
