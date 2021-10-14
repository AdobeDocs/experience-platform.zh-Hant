---
keywords: Experience Platform；快速入門；customer ai；熱門主題
solution: Experience Platform, Intelligent Services, Real-time Customer Data Platform
feature: Customer AI
title: Customer AI快速入門
topic-legacy: Getting started
description: 本指南提供範例API呼叫，以示範如何設定請求格式。 這些功能包括路徑、必要標題和格式正確的請求裝載。
exl-id: 90c9a83a-8e66-4239-b2d6-2049a6319b25
source-git-commit: c3320f040383980448135371ad9fae583cfca344
workflow-type: tm+mt
source-wordcount: '571'
ht-degree: 0%

---

# Customer AI快速入門

Customer AI的指南需要對使用Customer AI時涉及的各種平台服務有良好的了解。 開始之前，請查閱以下文檔：

- [Experience Data Model(XDM)系統概觀](../../xdm/home.md):XDM是基礎架構，可 [!DNL Adobe Experience Cloud]讓Experience Platform提供技術支援，在適當的時間，透過適當的管道向適當的人員傳遞適當的訊息。建置Experience Platform的方法 — XDM系統可操作Experience Data Model結構，以供Platform服務使用。
- [結構構成基本概念](../../xdm/schema/composition.md):本檔案簡介Experience Data Model(XDM)結構，以及合成結構以用於的結構、原則和最佳實 [!DNL Adobe Experience Platform]務。
- [建立結構](../../xdm/tutorials/create-schema-ui.md):本教學課程涵蓋使用Experience Platform中的結構編輯器建立結構的步驟。
- [即時客戶個人檔案概觀](../../rtcdp/overview.md):Real-time Customer Data Platform( [!DNL Adobe Experience Platform]Real-time CDP)以為基礎，可協助公司匯集已知和未知的資料，在客戶歷程中運用智慧決策功能啟動客戶設定檔。Real-time CDP結合了多個企業資料源，以即時建立統一的配置檔案，這些配置檔案可用於跨所有渠道和設備提供一對一的個性化客戶體驗。
- [區段服務概觀](../../segmentation/home.md):區段是定義設定檔存放區中一組設定檔子集所共用的特定屬性或行為的程式，以區分可行銷的一組人員和您的客戶群。例如，在名為「您忘記購買運動鞋嗎？」的電子郵件行銷活動中，您可能想要有過去30天內搜尋跑鞋，但未完成購買的所有使用者的對象。 使用不同的區段，您可以專注於不同的受眾，提供更自訂的行銷體驗。
- [區段產生器使用指南](../../segmentation/tutorials/create-a-segment.md):Platform可讓您輕鬆建立和存取區段，並使用不同的建置區塊來進一步分析區段的特徵。

## 下載Customer AI分數

>[!NOTE]
>
>如果您不需要下載原始分數，可以略過此步驟，並繼續參閱[設定指南](./user-guide/configure.md)。

您可透過API呼叫的組合來下載Customer AI分數。 若要呼叫Platform API，您必須先完成[authentication教學課程](https://www.adobe.com/go/platform-api-authentication-en)。 完成驗證教學課程後，所有Experience PlatformAPI呼叫中每個必要標題的值都會顯示，如下所示：

- 授權：承載`{ACCESS_TOKEN}`
- x-api-key: `{API_KEY}`
- x-gw-ims-org-id: `{IMS_ORG}`

Experience Platform中的所有資源都會隔離至特定的虛擬沙箱。 對Platform API提出的所有請求都需要標題，以指定作業將在下列位置進行的沙箱名稱：

- x-sandbox-name: `{SANDBOX_NAME}`

>[!NOTE]
>
>如需Platform中沙箱的詳細資訊，請參閱[沙箱概觀檔案](../../sandboxes/home.md)。

### 讀取範例API呼叫

本指南提供範例API呼叫，以示範如何設定請求格式。 這些功能包括路徑、必要標題和格式正確的請求裝載。 也提供API回應中傳回的範例JSON。 如需範例API呼叫檔案中所使用慣例的資訊，請參閱Experience Platform疑難排解指南中[如何讀取範例API呼叫](../../landing/troubleshooting.md)的區段。

## 後續步驟

完成上文檔中概述的步驟後，請訪問[Input and Output](./input-output.md)文檔。 本檔案簡要概述在Customer AI中使用和產生的資料類型。
