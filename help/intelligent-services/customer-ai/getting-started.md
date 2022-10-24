---
keywords: Experience Platform；快速入門；customer ai；熱門主題
solution: Experience Platform, Real-time Customer Data Platform
feature: Customer AI
title: Customer AI快速入門
topic-legacy: Getting started
description: 本指南提供範例API呼叫，以示範如何設定請求格式。 這些功能包括路徑、必要標題和格式正確的請求裝載。
exl-id: 90c9a83a-8e66-4239-b2d6-2049a6319b25
source-git-commit: 14e3eff3ea2469023823a35ee1112568f5b5f4f7
workflow-type: tm+mt
source-wordcount: '652'
ht-degree: 1%

---

# Customer AI快速入門

Customer AI的指南需要對使用Customer AI時涉及的各種平台服務有良好的了解。 開始之前，請查閱以下文檔：

- [Experience Data Model(XDM)系統概觀](../../xdm/home.md):XDM是可讓 [!DNL Adobe Experience Cloud]由Experience Platform提供技術支援，在正確的時間，透過正確的管道將正確的訊息傳送給正確的人員。 建置Experience Platform的方法 — XDM系統可操作Experience Data Model結構，以供Platform服務使用。
- [結構構成基本概念](../../xdm/schema/composition.md):本檔案介紹Experience Data Model(XDM)結構，以及合成結構以用於 [!DNL Adobe Experience Platform].
- [建立結構](../../xdm/tutorials/create-schema-ui.md):本教學課程涵蓋使用Experience Platform中的結構編輯器建立結構的步驟。
- [即時客戶個人檔案概觀](../../rtcdp/overview.md):內建 [!DNL Adobe Experience Platform], Adobe Real-time Customer Data Platform(Real-Time CDP)可協助公司匯集已知和未知的資料，在客戶歷程中運用智慧決策功能啟用客戶設定檔。 Real-Time CDP結合多個企業資料來源，以即時建立統一的設定檔，以用於在所有管道和裝置上提供一對一的個人化客戶體驗。
- [區段服務概觀](../../segmentation/home.md):區段是定義設定檔存放區中一組設定檔子集所共用的特定屬性或行為的程式，以區分可行銷的一組人員和您的客戶群。 例如，在名為「您忘記購買運動鞋嗎？」的電子郵件行銷活動中，您可能想要有過去30天內搜尋跑鞋，但未完成購買的所有使用者的對象。 使用不同的區段，您可以專注於不同的受眾，提供更自訂的行銷體驗。
- [區段產生器使用手冊](../../segmentation/tutorials/create-a-segment.md):Platform可讓您輕鬆建立和存取區段，並使用不同的建置區塊來進一步分析區段的特徵。

## 下載Customer AI分數

>[!NOTE]
>
>如果您不需要下載原始分數，可以略過此步驟，並繼續 [配置指南](./user-guide/configure.md).

您可透過API呼叫的組合來下載Customer AI分數。 若要呼叫Platform API，您必須先完成 [驗證教學課程](https://www.adobe.com/go/platform-api-authentication-en). 完成驗證教學課程後，所有Experience PlatformAPI呼叫中每個必要標題的值都會顯示，如下所示：

- 授權：承載 `{ACCESS_TOKEN}`
- x-api-key: `{API_KEY}`
- x-gw-ims-org-id: `{ORG_ID}`

Experience Platform中的所有資源都會隔離至特定的虛擬沙箱。 對Platform API提出的所有請求都需要標題，以指定作業將在下列位置進行的沙箱名稱：

- x-sandbox-name: `{SANDBOX_NAME}`

>[!NOTE]
>
>如需Platform中沙箱的詳細資訊，請參閱 [沙箱概述檔案](../../sandboxes/home.md).

### 讀取範例API呼叫

本指南提供範例API呼叫，以示範如何設定請求格式。 這些功能包括路徑、必要標題和格式正確的請求裝載。 也提供API回應中傳回的範例JSON。 如需範例API呼叫檔案中所使用慣例的相關資訊，請參閱 [如何閱讀API呼叫範例](../../landing/troubleshooting.md) Experience Platform疑難排解指南中。

## 存取控制 {#access-control}

使用存取控制時， **檢視Customer AI** 和 **管理Customer AI** 權限可授予Customer AI不同功能的存取權。 此 **管理Customer AI** 權限可讓您 **建立**,**更新**, **刪除**, **啟用**，或 **disable** 例項，而 **檢視Customer AI** 可讓您閱讀或檢視。 此 **建立**, **更新** 和 **刪除** 動作會由稽核記錄檔記錄。

請參閱檔案以了解 [為訪問控制分配權限](../../../help/access-control/home.md) 或方法 [使用審核日誌來監視訪問和活動](../../../help/landing/governance-privacy-security/audit-logs/overview.md).

## 後續步驟

完成上述檔案中概述的步驟後，請造訪 [輸入和輸出](./input-output.md) 檔案。 本檔案簡要概述在Customer AI中使用和產生的資料類型。
