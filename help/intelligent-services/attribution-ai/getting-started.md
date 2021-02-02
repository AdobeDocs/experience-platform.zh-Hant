---
keywords: Experience Platform；快速入門；歸因ai；熱門主題
solution: Experience Platform, Intelligent Services
title: Attribution AI快速入門
topic: Getting started
description: 以下指南需要瞭解使用Attribution AI時涉及的各種Adobe Experience Platform服務。 在開始教學課程之前，請先閱讀下列檔案。
translation-type: tm+mt
source-git-commit: ece2ae1eea8426813a95c18096c1b428acfd1a71
workflow-type: tm+mt
source-wordcount: '538'
ht-degree: 0%

---


# Attribution AI快速入門

以下指南需要瞭解使用Attribution AI時涉及的各種[!DNL Adobe Experience Platform]服務。 在開始教學課程之前，請先檢閱下列檔案：

- [體驗資料模型(XDM)系統概觀](../../xdm/home.md):XDM是基礎架構，可讓 [!DNL Adobe Experience Cloud]Experience Platform提供支援，讓您在適當的時間，透過適當的通道，向適當的人傳遞適當的訊息。Experience Platform的建立方法XDM System可操作Experience Data Model架構，供Platform服務使用。
- [架構構成基礎](../../xdm/schema/composition.md):本檔案提供Experience Data Model(XDM)架構的簡介，以及用於合成架構的建立區塊、原則和最佳實務 [!DNL Adobe Experience Platform]。
- [建立結構](../../xdm/tutorials/create-schema-ui.md):本教學課程涵蓋使用Experience Platform中的架構編輯器建立架構的步驟。

歸因AI要求資料集符合消費者體驗事件(CEE)架構，此架構是[體驗資料模型](../../xdm/home.md)(XDM)中的混音。 若要實作或變更此資料，請在attributionai-support@adobe.com與Adobe支援聯絡。 如果媒體支出資料已經存在，您可以做進一步分析，例如增加收入和投資報酬率。 如果客戶配置檔案資料可用，您可以進一步將信用歸因於客戶配置檔案層。

## 術語

- **轉換事件：** 客戶為指出目標（例如會議註冊）的里程碑而進行的任何數位事件或數位互動。其他範例包括付費轉換、免費帳戶註冊或特徵資格。

- **觸點：客** 戶在邁向目標的道路上所進行的任何數位事件或數位互動。範例包括購買前相關的行銷成果、顯示已檢視的廣告印象以及付費搜尋點按。

## 下載Attribution AI分數

>[!NOTE]
>
>如果您不需要下載原始分數，可以略過此步驟並繼續[後續步驟](#next-steps)。

下載Attribution AI分數是透過API呼叫的組合來完成。 若要呼叫平台API，您必須先完成[驗證教學課程](https://www.adobe.com/go/platform-api-authentication-en)。 完成驗證教學課程後，所有Experience Platform API呼叫中每個必要標題的值都會顯示在下方：

- 授權：載體`{ACCESS_TOKEN}`
- x-api-key:`{API_KEY}`
- x-gw-ims-org-id:`{IMS_ORG}`

Experience Platform中的所有資源都隔離至特定的虛擬沙盒。 所有對平台API的請求都需要一個標題，該標題會指定要在中執行的操作的沙盒名稱：

- x-sandbox-name:`{SANDBOX_NAME}`

>[!NOTE]
>
>如需平台中沙盒的詳細資訊，請參閱[沙盒概述檔案](../../sandboxes/home.md)。

### 讀取範例API呼叫

本指南提供範例API呼叫，以示範如何格式化您的請求。 這些包括路徑、必要標題和正確格式化的請求負載。 也提供API回應中傳回的範例JSON。 如需範例API呼叫檔案中所用慣例的詳細資訊，請參閱Experience Platform疑難排解指南中[如何讀取範例API呼叫](../../landing/troubleshooting.md)一節。

## 下一步 {#next-steps}

在您準備好並準備好所有憑證和結構描述後，請從[歸因AI使用者介面指南](./user-guide.md)開始。 本指南會逐步引導您建立執行個體，並送出以進行訓練和計分。