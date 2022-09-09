---
keywords: Experience Platform；快速入門；歸因ai；熱門主題
feature: Attribution AI
title: 開始使用Attribution AI
topic-legacy: Getting started
description: 下列指南需要了解使用Attribution AI時涉及的各種Adobe Experience Platform服務。 開始教學課程之前，請檢閱下列檔案。
exl-id: ab269c24-97ac-4da9-9b6c-7d2dde61f0dc
source-git-commit: a14f857f87482e1468211152976530c718d56e38
workflow-type: tm+mt
source-wordcount: '619'
ht-degree: 1%

---

# 開始使用Attribution AI

以下指南需要了解 [!DNL Adobe Experience Platform] 與使用Attribution AI相關的服務。 開始教學課程之前，請檢閱下列檔案：

- [Experience Data Model(XDM)系統概觀](../../xdm/home.md):XDM是可讓 [!DNL Adobe Experience Cloud]由Experience Platform提供技術支援，在正確的時間，透過正確的管道將正確的訊息傳送給正確的人員。 建置Experience Platform的方法 — XDM系統可操作Experience Data Model結構，以供Platform服務使用。
- [結構構成基本概念](../../xdm/schema/composition.md):本檔案介紹Experience Data Model(XDM)結構，以及合成結構以用於 [!DNL Adobe Experience Platform].
- [建立結構](../../xdm/tutorials/create-schema-ui.md):本教學課程涵蓋使用Experience Platform中的結構編輯器建立結構的步驟。

Attribution AI需要資料集才能符合消費者體驗事件(CEE)結構，此結構為 [Experience Data Model(XDM)](../../xdm/home.md) 架構欄位組。 請透過attributionai-support@adobe.com聯絡Adobe支援，以實作或變更此資料。 如果存在媒體支出資料，您可以進行進一步分析，如增加收入和ROI。 如果客戶設定檔資料可用，您可以進一步將評分歸因於客戶設定檔層級。

## 術語

- **轉換事件：** 客戶為指出目標（例如會議註冊）的里程碑而做的任何數位事件或數位互動。 其他範例包括付費轉換、免費帳戶註冊或特徵資格。

- **接觸點：** 客戶在邁向目標的路徑中執行的任何數位事件或數位互動。 例如購買前相關的行銷工作、顯示已檢視的廣告曝光次數以及付費搜尋點按次數。

## 下載Attribution AI分數

>[!NOTE]
>
>如果您不需要下載原始分數，可以略過此步驟，並繼續 [後續步驟](#next-steps).

下載Attribution AI分數是透過API呼叫的組合來完成。 若要呼叫Platform API，您必須先完成 [驗證教學課程](https://www.adobe.com/go/platform-api-authentication-en). 完成驗證教學課程後，所有Experience PlatformAPI呼叫中每個必要標題的值都會顯示，如下所示：

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

使用角色型存取控制時， **檢視Attribution AI** 和 **管理Attribution AI** 權限可授予對不同Attribution AI功能的存取。 此 **管理Attribution AI** 讓您 **建立**, **克隆**, **編輯**, **刪除**, **啟用**，或 **disable** 例項，而 **檢視Attribution AI** 讓您 **讀取** 或 **檢視** 它。 此 **建立**, **編輯** 和 **刪除** 動作會由稽核記錄檔記錄。

請參閱檔案以了解 [為訪問控制分配權限](../../../help/access-control/home.md) 或方法 [使用審核日誌來監視訪問和活動](../../../help/landing/governance-privacy-security/audit-logs/overview.md).

## 後續步驟 {#next-steps}

準備就緒並部署所有憑證和結構後，請先遵循 [Attribution AI介面指南](./user-guide.md). 本指南會逐步引導您建立執行個體，並提交以進行訓練和計分。
