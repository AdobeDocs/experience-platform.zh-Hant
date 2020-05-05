---
keywords: Experience Platform;getting started;attribution ai;popular topics
solution: Experience Platform
title: Attribution AI快速入門
topic: Getting started
translation-type: tm+mt
source-git-commit: 6161f5a9ca0df341272a96a8a19ce6c34f6d5d3e

---


# Attribution AI快速入門

以下指南需要瞭解使用Attribution AI時涉及的各種Adobe Experience Platform服務。 在開始教學課程之前，請先檢閱下列檔案：

- [體驗資料模型(XDM)系統概觀](../../xdm/home.md): XDM是基礎架構，可讓採用Experience Platform的Adobe Experience Cloud在適當的時機，透過適當的通道向適當的人傳遞適當的訊息。 Experience Platform的建立方法XDM System可操作Experience Data Model架構，供Platform服務使用。
- [架構構成基礎](../../xdm/schema/composition.md): 本檔案提供Experience Data Model(XDM)架構的簡介，以及構成Adobe Experience Platform中要使用之架構的建置區塊、原則和最佳實務。
- [建立結構](../../xdm/tutorials/create-schema-ui.md): 本教學課程涵蓋使用Experience Platform中的架構編輯器建立架構的步驟。

歸因AI需要資料集符合消費者體驗事件(CEE)架構，此架構是 [Experience Data Model](../../xdm/home.md) (XDM)中的混合項。 若要實作或變更此資料，請在attributionai-support@adobe.com與Adobe支援聯絡。 如果媒體支出資料已經存在，您可以做進一步分析，例如增加收入和投資報酬率。 如果客戶配置檔案資料可用，您可以進一步將信用歸因於客戶配置檔案層。

## 術語

- **轉換事件：** 客戶為指出邁向目標（例如會議註冊）的里程碑而進行的任何數位事件或數位互動。 其他範例包括付費轉換、免費帳戶註冊或特徵資格。

- **觸點：** 客戶在邁向目標的道路上所進行的任何數位事件或數位互動。 範例包括購買前相關的行銷成果、顯示已檢視的廣告印象以及付費搜尋點按。

## 下載Attribution AI分數

>[!NOTE] 如果您不需要下載原始分數，可以略過此步驟並繼續下 [一步](#next-steps)。

下載Attribution AI分數是透過API呼叫的組合來完成。 若要呼叫平台API，您必須先完成驗證教 [學課程](../../tutorials/authentication.md)。 完成驗證教學課程後，所有Experience Platform API呼叫中每個必要標題的值都會顯示在下方：

- 授權： 生產者 `{ACCESS_TOKEN}`
- x-api-key: `{API_KEY}`
- x-gw-ims-org-id: `{IMS_ORG}`

Experience Platform中的所有資源都隔離至特定的虛擬沙盒。 所有對平台API的請求都需要一個標題，該標題會指定要在中執行的操作的沙盒名稱：

- x-sandbox-name: `{SANDBOX_NAME}`

>[!NOTE] 如需平台中沙盒的詳細資訊，請參閱沙盒 [概觀檔案](../../sandboxes/home.md)。

### 讀取範例API呼叫

本指南提供範例API呼叫，以示範如何格式化您的請求。 這些包括路徑、必要標題和正確格式化的請求負載。 也提供API回應中傳回的範例JSON。 如需範例API呼叫檔案中所用慣例的詳細資訊，請參閱「Experience Platform疑難排解指 [南」中有關如何讀取範例API呼叫的章節](../../landing/troubleshooting.md) 。

## 下一步 {#next-steps}

當您準備好並準備好所有憑證和結構描述後，請從遵循 [Attribution AI使用者介面指南開始](./user-guide.md)。 本指南會逐步引導您建立執行個體，並送出以進行訓練和計分。