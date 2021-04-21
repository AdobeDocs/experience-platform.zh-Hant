---
keywords: Experience Platform；快速入門；客戶ai；熱門主題
solution: Experience Platform, Intelligent Services, Real-time Customer Data Platform
title: 客戶AI快速入門
topic-legacy: Getting started
description: 本指南提供範例API呼叫，以示範如何格式化您的請求。 這些包括路徑、必要標題和正確格式化的請求負載。
exl-id: 90c9a83a-8e66-4239-b2d6-2049a6319b25
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '571'
ht-degree: 0%

---

# 客戶AI快速入門

客戶AI指南需要對使用客戶AI時涉及的各種平台服務有良好的瞭解。 開始之前，請先閱讀下列檔案：

- [體驗資料模型(XDM)系統概觀](../../xdm/home.md):XDM是基礎性的框架，可 [!DNL Adobe Experience Cloud]讓Experience Platform提供支援，在適當的時機，在適當的通道上向適當的人傳遞適當的訊息。建立Experience Platform的方法XDM System可操作Experience Data Model架構，供平台服務使用。
- [架構構成基礎](../../xdm/schema/composition.md):本檔案提供Experience Data Model(XDM)架構的簡介，以及用於合成架構的建立區塊、原則和最佳實務 [!DNL Adobe Experience Platform]。
- [建立結構](../../xdm/tutorials/create-schema-ui.md):本教程介紹使用Experience Platform中的架構編輯器建立架構的步驟。
- [即時客戶個人檔案總覽](../../rtcdp/overview.md):即時客 [!DNL Adobe Experience Platform]戶資料平台(Real-time CDP)以其為基礎，可協助公司將已知和未知的資料匯整在一起，在整個客戶歷程中運用智慧決策來啟動客戶個人檔案。即時CDP結合了多個企業資料源，以即時建立統一的配置檔案，可用於跨所有通道和設備提供一對一的個性化客戶體驗。
- [區段服務概觀](../../segmentation/home.md):區段是定義描述檔商店中描述檔子集所共用的特定屬性或行為，以區分適銷人員群組和客戶群的程式。例如，在名為「您忘記購買運動鞋嗎？」的電子郵件促銷活動中，您可能希望擁有在過去30天內搜尋跑鞋但未完成購買的所有使用者的觀眾。 使用不同的細分，您可以專注於不同的受眾，提供更自訂的行銷體驗。
- [區段產生器使用指南](../../segmentation/tutorials/create-a-segment.md):平台可讓您輕鬆建立和存取區段，並使用不同的建置區塊進一步描述區段。

## 下載客戶AI分數

>[!NOTE]
>
>如果您不需要下載原始分數，可以跳過此步驟並繼續[配置指南](./user-guide/configure.md)。

下載客戶AI分數是透過API呼叫的組合來完成。 若要呼叫平台API，您必須先完成[驗證教學課程](https://www.adobe.com/go/platform-api-authentication-en)。 完成驗證教學課程後，將提供所有Experience PlatformAPI呼叫中每個必要標題的值，如下所示：

- 授權：載體`{ACCESS_TOKEN}`
- x-api-key:`{API_KEY}`
- x-gw-ims-org-id:`{IMS_ORG}`

Experience Platform中的所有資源都隔離到特定的虛擬沙盒。 所有對平台API的請求都需要一個標題，該標題會指定要在中執行的操作的沙盒名稱：

- x-sandbox-name:`{SANDBOX_NAME}`

>[!NOTE]
>
>如需平台中沙盒的詳細資訊，請參閱[沙盒概述檔案](../../sandboxes/home.md)。

### 讀取範例API呼叫

本指南提供範例API呼叫，以示範如何格式化您的請求。 這些包括路徑、必要標題和正確格式化的請求負載。 也提供API回應中傳回的範例JSON。 如需範例API呼叫檔案中所用慣例的詳細資訊，請參閱Experience Platform疑難排解指南中[如何讀取範例API呼叫](../../landing/troubleshooting.md)一節。

## 後續步驟

完成上述文檔中的步驟後，請訪問[輸入和輸出](./input-output.md)文檔。 本檔案簡要概述客戶AI中使用和產生的資料類型。
