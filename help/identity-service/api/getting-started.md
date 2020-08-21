---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: 快速入門
topic: API guide
translation-type: tm+mt
source-git-commit: bd9884a24c5301121f30090946ab24d9c394db1b
workflow-type: tm+mt
source-wordcount: '714'
ht-degree: 1%

---


# [!DNL Identity Service] API開發人員指南

Adobe Experience Platform可 [!DNL Identity Service] 在Adobe Experience Platform內管理跨裝置、跨通道和近乎即時的客戶身分識別。

## 快速入門

本指南需要有效瞭解Adobe Experience Platform的下列元件：

- [!DNL Identity Service](../home.md): 解決客戶個人檔案資料分散所帶來的根本挑戰。 它可跨裝置和系統橋接身分，讓客戶與您的品牌互動。
- [!DNL Real-time Customer Profile](../../profile/home.md): 根據來自多個來源的匯整資料，即時提供統一的消費者個人檔案。
- [!DNL Experience Data Model (XDM)](../../xdm/home.md): 組織客戶體驗資料 [!DNL Platform] 的標準化架構。

以下章節提供您必須知道或掌握的額外資訊，才能成功呼叫 [!DNL Identity Service] API。

### 讀取範例API呼叫

本指南提供範例API呼叫，以示範如何格式化您的請求。 這些包括路徑、必要標題和正確格式化的請求負載。 也提供API回應中傳回的範例JSON。 如需範例API呼叫檔案中所用慣例的詳細資訊，請參閱疑難排解指 [南中有關如何讀取範例API呼叫的](../../landing/troubleshooting.md#how-do-i-format-an-api-request)[!DNL Experience Platform] 章節。

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

### 基於區域的路由

API [!DNL Identity Service] 採用區域特定的端點，要求在請求路徑 `{REGION}` 中加入。 在IMS組織布建期間，會決定地區並儲存在IMS組織描述檔中。 使用每個端點的正確區域可確保使用 [!DNL Identity Service] API提出的所有請求都路由到適當的區域。

API目前支援兩個地 [!DNL Identity Service] 區： VA7和NLD2。

下表顯示了使用區域的示例路徑：

| 服務 | 地區： VA7 | 地區： NLD2 |
| ------ | -------- |--------- |
| [!DNL Identity Service] API | https://</span>platform-va7.adobe。</span>io/data/core/identity/{ENDPOINT} | https://</span>platform-nld2.adobe。</span>io/data/core/identity/{ENDPOINT} |
| [!DNL Identity Namespace] API | https://</span>platform-va7.adobe。</span>io/data/core/idnamespace/{ENDPOINT} | https://</span>platform-nld2.adobe。</span>io/data/core/idnamespace{ENDPOINT} |

>[!NOTE]
>
>未指定區域的請求可能導致呼叫路由到錯誤區域，或導致呼叫意外失敗。

如果您無法在IMS組織設定檔中找到地區，請聯絡您的系統管理員以取得支援。

## 使用 [!DNL Identity Service] API

這些服務中使用的身份參數可以用兩種方式之一表示； 複合或XID。

複合身份是包括ID值和命名空間的構造。 使用複合身份時，名稱空間可以由名稱(`namespace.code`)或ID(`namespace.id`)提供。

當身分持續存在時， [!DNL Identity Service] 會產生並指派ID給該身分，稱為原生ID或XID。 所有群集和映射API的變體在其請求和響應中都支援組合身份和XID。 其中一個參數是必要的- `xid` 或組合或 [`ns`&#x200B;`nsid`] 與使 `id` 用這些API。

為了限制回應中的負載，API會根據使用的身分建構類型來調整其回應。 也就是說，如果您傳遞XID，您的回應會有XID，如果您傳遞複合身分，則回應會遵循請求中使用的結構。

本文中的範例不涵蓋 [!DNL Identity Service] API的完整功能。 如需完整的API，請參閱 [Swagger API參考](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/id-service-api.yaml)。

>[!NOTE]
>
>在請求中使用原生XID時，傳回的所有身分都會以原生XID格式。 建議使用ID/namespace表單。 如需詳細資訊，請參閱有關 [取得XID以取得身分的章節](./create-custom-namespace.md)。

## 後續步驟

現在您已收集到必要的認證，您可以繼續閱讀其餘的開發人員指南。 每個區段都提供其端點的重要資訊，並示範執行CRUD作業的範例API呼叫。 每個呼叫都包含一般 **API格式**、顯示必要標題 **和正確格式化負載的範例請求，以及成功呼叫** 的範例回應 **** 。
