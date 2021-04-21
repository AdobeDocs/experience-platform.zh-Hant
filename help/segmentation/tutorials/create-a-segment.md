---
keywords: Experience Platform; home；熱門主題；segment;Segment;create segmentation;segmentation;create a segment; Segmentation Service;
solution: Experience Platform
title: 使用分段服務API建立分段
topic-legacy: tutorial
type: Tutorial
description: 請依照本教學課程學習如何使用Adobe Experience Platform區段服務API來開發、測試、預覽和儲存區段定義。
exl-id: 78684ae0-3721-4736-99f1-a7d1660dc849
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '924'
ht-degree: 0%

---

# 使用分段服務API建立區段

本檔案提供使用[[!DNL Adobe Experience Platform Segmentation Service API]](../api/getting-started.md)來開發、測試、預覽和儲存區段定義的教學課程。

如需如何使用使用者介面建立區段的詳細資訊，請參閱[區段產生器指南](../ui/overview.md)。

## 快速入門

本教學課程需要對建立觀眾區隔時涉及的各種[!DNL Adobe Experience Platform]服務有深入的瞭解。 在開始本教學課程之前，請先閱讀下列服務的檔案：

- [[!DNL Real-time Customer Profile]](../../profile/home.md):根據來自多個來源的匯整資料，提供統一、即時的消費者個人檔案。
- [[!DNL Adobe Experience Platform Segmentation Service]](../home.md):可讓您從即時客戶個人檔案資料建立受眾細分。
- [[!DNL Experience Data Model (XDM)]](../../xdm/home.md):組織客戶體驗資 [!DNL Platform] 料的標準化架構。

以下各節提供您必須知道的其他資訊，才能成功呼叫[!DNL Platform] API。

### 讀取範例API呼叫

本教學課程提供範例API呼叫，以示範如何設定請求的格式。 這些包括路徑、必要標題和正確格式化的請求負載。 也提供API回應中傳回的範例JSON。 如需範例API呼叫檔案中所用慣例的詳細資訊，請參閱[!DNL Experience Platform]疑難排解指南中[如何讀取範例API呼叫](../../landing/troubleshooting.md#how-do-i-format-an-api-request)一節。

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

## 開發區段定義

分段的第一步是定義分段，在稱為分段定義的構造中表示。 段定義是一個對象，用於封裝寫入[!DNL Profile Query Language](PQL)中的查詢。 此對象也稱為PQL謂語。 PQL謂語根據與您提供給[!DNL Real-time Customer Profile]的任何記錄或時間系列資料相關的條件定義段規則。 有關編寫PQL查詢的詳細資訊，請參見[ PQL指南](../pql/overview.md)。

您可以透過向[!DNL Segmentation] API中的`/segment/definitions`端點提出POST請求，建立新的區段定義。 下列範例概述如何設定定義請求的格式，包括成功定義區段所需的資訊。

有關如何定義區段的詳細說明，請閱讀[區段定義開發人員指南](../api/segment-definitions.md#create)。

## 預估並預覽觀眾{#estimate-and-preview-an-audience}

當您開發區段定義時，可使用[!DNL Real-time Customer Profile]中的估計和預覽工具來檢視摘要層級資訊，以協助您隔離預期的觀眾。 估計值提供區段定義的統計資訊，例如預計讀者大小和信賴區間。 預覽提供區段定義的合格設定檔分頁清單，讓您比較結果與預期結果。

透過估計和預覽受眾，您可以測試和最佳化PQL謂語，直到產生可預期的結果，然後在更新的區段定義中使用。

預覽或取得區段估計需要兩個步驟：

1. [建立預覽工作](#create-a-preview-job)
2. [使用預](#view-an-estimate-or-preview) 覽工作的ID檢視估計或預覽

### 如何產生估計

資料樣本可用來評估區段並估計符合資格的設定檔數目。 每天早上（12AM-2AM PT，即7-9AM UTC），新資料會載入記憶體中，所有區段查詢都會使用當天的樣本資料來估計。 因此，新增的欄位或收集的其他資料，都會反映在次日的估計值中。

範例大小取決於您描述檔商店中的實體總數。 下表列出了這些樣本大小：

| 描述檔儲存中的實體 | 樣本大小 |
| ------------------------- | ----------- |
| 不到100萬 | 完整資料集 |
| 1000萬到2000萬 | 100萬 |
| 超過2000萬 | 總共5% |

估計值一般會持續10-15秒，從粗略的估計開始，並隨著讀取更多記錄而調整。

### 建立預覽工作

您可以向`/preview`端點發出POST請求，以建立新的預覽作業。

有關建立預覽作業的詳細說明，請參閱[預覽和估計端點指南](../api/previews-and-estimates.md#create-preview)。

### 檢視估計或預覽

由於不同的查詢可能需要不同的時間才能完成，因此會以非同步方式執行估計和預覽程式。 一旦啟動查詢後，您就可以使用API呼叫來擷取(GET)估計或預覽的目前狀態。

使用[!DNL Segmentation Service] API，您可以透過預覽工作的ID來尋找其目前狀態。 如果狀態為&quot;RESULT_READY&quot;，則可以查看結果。 要查找預覽作業的當前狀態，請閱讀預覽和估計端點指南中有關檢索預覽作業部分[的部分。 ](../api/previews-and-estimates.md#get-preview)要查找估計作業的當前狀態，請閱讀預覽和估計端點指南中有關檢索估計作業[的部分。](../api/previews-and-estimates.md#get-estimate)


## 後續步驟

在您開發、測試和儲存區段定義後，就可以使用[!DNL Segmentation Service] API建立區段工作以建立觀眾。 有關如何完成此操作的詳細步驟，請參閱[評估和訪問段結果](./evaluate-a-segment.md)的教程。
