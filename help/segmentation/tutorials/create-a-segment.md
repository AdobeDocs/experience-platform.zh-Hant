---
keywords: Experience Platform;home;popular topics;segment;Segment;create segment
solution: Experience Platform
title: 建立區段
topic: tutorial
description: 本檔案提供使用Adobe Experience Platform Segmentation Service API來開發、測試、預覽和儲存區段定義的教學課程。
translation-type: tm+mt
source-git-commit: a93b3a1980ca0f1d3a32257a923eb7ffc8896fd5
workflow-type: tm+mt
source-wordcount: '894'
ht-degree: 0%

---


# 建立區段

本檔案提供教學課程，以開發、測試、預覽和儲存使用的區段定義 [!DNL Adobe Experience Platform Segmentation Service API](../api/getting-started.md)。

如需如何使用使用者介面建立區段的詳細資訊，請參閱「區段產 [生器指南」](../ui/overview.md)。

## 快速入門

本教學課程需要對建立觀眾區隔時 [!DNL Adobe Experience Platform] 涉及的各種服務有充份的瞭解。 在開始本教學課程之前，請先閱讀下列服務的檔案：

- [!DNL Real-time Customer Profile](../../profile/home.md):根據來自多個來源的匯整資料，提供統一、即時的消費者個人檔案。
- [!DNL Adobe Experience Platform Segmentation Service](../home.md):可讓您從即時客戶個人檔案資料建立受眾細分。
- [!DNL Experience Data Model (XDM)](../../xdm/home.md):組織客戶體驗資料 [!DNL Platform] 的標準化架構。

以下章節提供您必須知道的其他資訊，才能成功呼叫 [!DNL Platform] API。

### 讀取範例API呼叫

本教學課程提供範例API呼叫，以示範如何設定請求的格式。 這些包括路徑、必要標題和正確格式化的請求負載。 也提供API回應中傳回的範例JSON。 如需範例API呼叫檔案中所用慣例的詳細資訊，請參閱疑難排解指 [南中有關如何讀取範例API呼叫的](../../landing/troubleshooting.md#how-do-i-format-an-api-request)[!DNL Experience Platform] 章節。

### 收集必要標題的值

若要呼叫API，您必 [!DNL Platform] 須先完成驗證教 [學課程](../../tutorials/authentication.md)。 完成驗證教學課程後，將提供所有 [!DNL Experience Platform] API呼叫中每個必要標題的值，如下所示：

- 授權：生產者 `{ACCESS_TOKEN}`
- x-api-key: `{API_KEY}`
- x-gw-ims-org-id: `{IMS_ORG}`

中的所有資 [!DNL Experience Platform] 源都與特定虛擬沙盒隔離。 對API的所 [!DNL Platform] 有請求都需要一個標題，該標題會指定要在中執行的操作的沙盒名稱：

- x-sandbox-name: `{SANDBOX_NAME}`

>[!NOTE]
>
>如需中沙盒的詳細資訊 [!DNL Platform]，請參閱沙 [盒概述檔案](../../sandboxes/home.md)。

所有包含裝載(POST、PUT、PATCH)的請求都需要額外的標題：

- 內容類型：application/json

## 開發區段定義

分段的第一步是定義分段，在稱為分段定義的構造中 **表示**。 段定義是一個對象，它封裝了寫入( [!DNL Profile Query Language] PQL)的查詢。 此對象也稱為 **PQL謂詞**。 PQL謂語根據與您提供給的任何記錄或時間序列資料相關的條件定義段規則 [!DNL Real-time Customer Profile]。 有關編寫 [PQL查詢的詳細資訊](../pql/overview.md) ，請參見PQL指南。

您可以透過對API中的端點提出POST請求，來建 `/segment/definitions` 立新的區段 [!DNL Segmentation] 定義。 下列範例概述如何設定定義請求的格式，包括成功定義區段所需的資訊。

如需如何定義區段的詳細說明，請閱讀區段定 [義開發人員指南](../api/segment-definitions.md#create)。

## 預估和預覽觀眾 {#estimate-and-preview-an-audience}

當您開發區段定義時，可以使用中的估計和預覽工具來檢 [!DNL Real-time Customer Profile] 視摘要層級的資訊，以協助您隔離預期的觀眾。 估計值提供區段定義的統計資訊，例如預計讀者大小和信賴區間。 預覽提供區段定義的合格設定檔分頁清單，讓您比較結果與預期結果。

透過估計和預覽受眾，您可以測試和最佳化PQL謂語，直到產生可預期的結果，然後在更新的區段定義中使用。

預覽或取得區段估計需要兩個步驟：

1. [建立預覽工作](#create-a-preview-job)
2. [使用預覽工作的ID](#view-an-estimate-or-preview) ，檢視估計值或預覽

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

您可以向端點發出POST請求，以建立新的預覽 `/preview` 作業。

有關建立預覽工作的詳細說明，請參閱預覽和估 [計端點指南](../api/previews-and-estimates.md#create-preview)。

### 檢視估計或預覽

由於不同的查詢可能需要不同的時間才能完成，因此估計和預覽進程會非同步運行。 一旦查詢啟動後，您就可以使用API呼叫來擷取(GET)估計或預覽的目前狀態。

使用 [!DNL Segmentation Service] API，您可以透過預覽工作的ID來尋找其目前狀態。 如果狀態為&quot;RESULT_READY&quot;，則可以查看結果。 若要查看預覽作業的當前狀態，請閱讀預覽和估計端 [點指南中有關檢索預覽作業部分](../api/previews-and-estimates.md#get-preview) 的章節。 要查找估計作業的當前狀態，請閱讀預覽和估計端 [點指南中有關檢索估計作業](../api/previews-and-estimates.md#get-estimate) 的部分。


## 後續步驟

在您開發、測試和儲存區段定義後，就可以建立區段工作，以使用 [!DNL Segmentation Service] API建立觀眾。 請參閱評估和存 [取區段結果的教學課程](./evaluate-a-segment.md) ，以取得如何完成此作業的詳細步驟。