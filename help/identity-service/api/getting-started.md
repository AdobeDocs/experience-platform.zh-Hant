---
keywords: Experience Platform；首頁；熱門主題；身份服務api；身份服務開發者指南；區域
solution: Experience Platform
title: 《 Identity Service API指南》
description: Identity Service API允許開發人員使用Adobe Experience Platform的身份圖管理跨設備、跨通道和接近即時的客戶身份識別。 請遵循本指南以了解如何使用 API 執行關鍵作業。
exl-id: d612af38-4648-4c3e-8cfd-3f306c9370e1
source-git-commit: 81f48de908b274d836f551bec5693de13c5edaf1
workflow-type: tm+mt
source-wordcount: '764'
ht-degree: 3%

---

# [!DNL Identity Service] API指南

Adobe Experience Platform [!DNL Identity Service] 通過Adobe Experience Platform內的「身份圖」管理客戶的跨設備、跨通道和近即時身份識別。

## 快速入門

本指南要求對Adobe Experience Platform的下列組成部分有工作上的理解：

- [[!DNL Identity Service]](../home.md):解決客戶配置檔案資料碎片化帶來的基本難題。 它通過跨設備和系統橋接身份來做到這一點，在這些設備和系統中客戶與您的品牌進行互動。
- [[!DNL Real-Time Customer Profile]](../../profile/home.md):根據來自多個源的聚合資料即時提供統一的消費者配置檔案。
- [[!DNL Experience Data Model (XDM)]](../../xdm/home.md):標準化框架 [!DNL Platform] 組織客戶體驗資料。

以下各節提供了您需要瞭解或掌握的其他資訊，以便成功呼叫 [!DNL Identity Service] API。

### 讀取示例API調用

本指南提供了示例API調用，以演示如何格式化請求。 這些包括路徑、必需的標頭和正確格式化的請求負載。 還提供了API響應中返回的示例JSON。 有關示例API調用文檔中使用的約定的資訊，請參見上的 [如何讀取示例API調用](../../landing/troubleshooting.md#how-do-i-format-an-api-request) 的 [!DNL Experience Platform] 疑難解答指南。

### 收集所需標題的值

為了呼叫 [!DNL Platform] API，必須首先完成 [驗證教程](https://www.adobe.com/go/platform-api-authentication-en)。 完成身份驗證教程將提供所有中每個必需標頭的值 [!DNL Experience Platform] API調用，如下所示：

- 授權：持 `{ACCESS_TOKEN}`
- x-api-key: `{API_KEY}`
- x-gw-ims-org-id: `{ORG_ID}`

中的所有資源 [!DNL Experience Platform] 與特定虛擬沙箱隔離。 所有請求 [!DNL Platform] API需要一個標頭，該標頭指定操作將在以下位置進行的沙盒的名稱：

- x-sandbox-name: `{SANDBOX_NAME}`

>[!NOTE]
>
>有關中的沙箱的詳細資訊 [!DNL Platform]，請參見 [沙盒概述文檔](../../sandboxes/home.md)。

包含負載(POST、PUT、PATCH)的所有請求都需要附加的標頭：

- 內容類型：應用程式/json

### 基於區域的路由

的 [!DNL Identity Service] API採用區域特定的端點，需要包含 `{REGION}` 作為請求路徑的一部分。 在您組織的預配過程中，將確定一個區域並將其儲存在您的組織配置檔案中。 使用每個端點的正確區域可確保使用 [!DNL Identity Service] API被路由到相應區域。

目前有兩個區域受支援 [!DNL Identity Service] API:VA7和NLD2。

下表顯示了使用區域的示例路徑：

| 服務 | 區域：VA7 | 區域：NLD2 |
| ------ | -------- |--------- |
| [!DNL Identity Service] API | https://</span>va7.adobe平台。</span>io/data/core/identity/{ENDPOINT} | https://</span>platform-nld2.adobe。</span>io/data/core/identity/{ENDPOINT} |
| [!DNL Identity Namespace] API | https://</span>va7.adobe平台。</span>io/data/core/idnamespace/{ENDPOINT} | https://</span>platform-nld2.adobe。</span>io/data/core/idnamespace{ENDPOINT} |

>[!NOTE]
>
>未指定區域的請求可能會導致呼叫路由到不正確區域或導致呼叫意外失敗。

如果您無法在組織配置檔案中找到區域，請與系統管理員聯繫以獲得支援。

## 使用 [!DNL Identity Service] API

這些服務中使用的身份參數可以用兩種方式之一表示；複合或XID。

複合標識是包括ID值和命名空間的構造。 使用複合標識時，可以通過任一名稱(`namespace.code`)或ID(`namespace.id`)。

當身份被保留時， [!DNL Identity Service] 生成ID並為該標識指定ID，稱為本地ID或XID。 群集和映射API的所有變體在其請求和響應中都支援複合標識和XID。 需要參數之一 —  `xid` 或組合 [`ns` 或 `nsid`] 和 `id` 來使用這些API。

為限制響應中的負載，API將其響應調整為所使用的標識構造類型。 即，如果傳遞XID，您的響應將具有XID，如果傳遞複合標識，則響應將遵循請求中使用的結構。

本文檔中的示例未涵蓋 [!DNL Identity Service] API。 有關完整的API，請參見 [Swagger API參考](https://www.adobe.io/experience-platform-apis/references/identity-service)。

>[!NOTE]
>
>在請求中使用本機XID時，返回的所有標識都將採用本機XID格式。 建議使用ID/命名空間表單。 有關詳細資訊，請參閱 [獲取XID以獲取身份](./create-custom-namespace.md)。

## 後續步驟

現在，您已收集了所需的憑據，現在可以繼續閱讀開發人員指南的其餘部分。 每個部分都提供有關其端點的重要資訊，並演示用於執行CRUD操作的示例API調用。 每個調用都包括一般API格式、顯示所需標頭和正確格式化負載的示例請求，以及成功調用的示例響應。
