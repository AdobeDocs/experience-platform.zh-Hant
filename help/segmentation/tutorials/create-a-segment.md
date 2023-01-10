---
keywords: Experience Platform；首頁；熱門主題；區段；區段；建立區段；區段；建立區段；區段；分段服務；
solution: Experience Platform
title: 使用分段服務API建立區段
type: Tutorial
description: 請依照本教學課程，了解如何使用Adobe Experience Platform區段服務API來開發、測試、預覽和儲存區段定義。
exl-id: 78684ae0-3721-4736-99f1-a7d1660dc849
source-git-commit: 59dfa862388394a68630a7136dee8e8988d0368c
workflow-type: tm+mt
source-wordcount: '948'
ht-degree: 0%

---

# 使用分段服務API建立區段

本檔案提供開發、測試、預覽和儲存區段定義的教學課程，使用 [[!DNL Adobe Experience Platform Segmentation Service API]](../api/getting-started.md).

如需如何使用使用者介面建立區段的詳細資訊，請參閱 [區段產生器指南](../ui/overview.md).

## 快速入門

本教學課程需要妥善了解 [!DNL Adobe Experience Platform] 與建立受眾區隔相關的服務。 開始本教學課程之前，請先檢閱下列服務的檔案：

- [[!DNL Real-Time Customer Profile]](../../profile/home.md):根據來自多個來源的匯總資料，提供統一的即時消費者設定檔。
- [[!DNL Adobe Experience Platform Segmentation Service]](../home.md):可讓您從即時客戶設定檔資料建立受眾區段。
- [[!DNL Experience Data Model (XDM)]](../../xdm/home.md):標準化框架 [!DNL Platform] 組織客戶體驗資料。 為了最能善用區段，請確定您的資料已根據 [資料模型最佳實務](../../xdm/schema/best-practices.md).

以下小節提供您需要知道的其他資訊，以便成功呼叫 [!DNL Platform] API。

### 讀取範例API呼叫

本教學課程提供範例API呼叫，以示範如何設定要求格式。 這些功能包括路徑、必要標題和格式正確的請求裝載。 也提供API回應中傳回的範例JSON。 如需範例API呼叫檔案中所使用慣例的相關資訊，請參閱 [如何閱讀API呼叫範例](../../landing/troubleshooting.md#how-do-i-format-an-api-request) 在 [!DNL Experience Platform] 疑難排解指南。

### 收集必要標題的值

若要對 [!DNL Platform] API，您必須先完成 [驗證教學課程](https://www.adobe.com/go/platform-api-authentication-en). 完成驗證教學課程會提供所有 [!DNL Experience Platform] API呼叫，如下所示：

- 授權：承載 `{ACCESS_TOKEN}`
- x-api-key: `{API_KEY}`
- x-gw-ims-org-id: `{ORG_ID}`

中的所有資源 [!DNL Experience Platform] 與特定虛擬沙箱隔離。 所有請求 [!DNL Platform] API需要標頭，以指定要在中執行操作的沙箱名稱：

- x-sandbox-name: `{SANDBOX_NAME}`

>[!NOTE]
>
>如需中沙箱的詳細資訊，請參閱 [!DNL Platform]，請參閱 [沙箱概述檔案](../../sandboxes/home.md).

所有包含裝載(POST、PUT、PATCH)的請求都需要額外的標題：

- 內容類型：application/json

## 開發區段定義

分段的第一步是定義區段，以稱為區段定義的結構表示。 區段定義是物件，用於封裝寫入 [!DNL Profile Query Language] (PQL)。 此對象也稱為PQL謂語。 PQL謂詞根據與提供給的任何記錄或時間序列資料相關的條件定義段的規則 [!DNL Real-Time Customer Profile]. 請參閱 [PQL指南](../pql/overview.md) 以了解有關寫入PQL查詢的詳細資訊。

您可以向 `/segment/definitions` 端點 [!DNL Segmentation] API。 下列範例概述如何設定定義要求的格式，包括為成功定義區段而需要哪些資訊。

如需定義區段的詳細說明，請參閱 [區段定義開發人員指南](../api/segment-definitions.md#create).

## 預估和預覽受眾 {#estimate-and-preview-an-audience}

當您開發區段定義時，可以在中使用預估和預覽工具 [!DNL Real-Time Customer Profile] 檢視摘要層級資訊，協助您確保隔離預期的對象。 預估值提供區段定義的統計資訊，例如預計的受眾規模和信賴區間。 預覽提供符合區段定義之設定檔的編頁清單，讓您能比較結果與預期的結果。

透過預估和預覽對象，您可以測試和最佳化PQL述詞，直到產生所需的結果，以便用於更新的區段定義。

預覽或取得區段預估值需要兩個步驟：

1. [建立預覽作業](#create-a-preview-job)
2. [檢視預估或預覽](#view-an-estimate-or-preview) 使用預覽作業的ID

### 如何產生估計

資料範例可用來評估區段，以及估計合格設定檔的數量。 每天早上都會將新資料載入記憶體（在12AM-2AM PT之間，即7AM-9AM UTC），所有分段查詢都會使用當天的範例資料來預估。 因此，新增的任何欄位或收集的其他資料，都會反映在次日的估計值中。

樣本大小取決於設定檔存放區中的整體數量。 下表顯示以下樣本大小：

| 設定檔存放區中的實體 | 樣本大小 |
| ------------------------- | ----------- |
| 不到100萬 | 完整資料集 |
| 1000至2000萬 | 100萬 |
| 2000多萬 | 總共5% |

估計通常會持續10到15秒，從粗略估計開始，並隨著讀取更多記錄而精簡。

### 建立預覽作業

您可以向 `/preview` 端點。

有關建立預覽作業的詳細說明，請參閱 [預覽和估計端點指南](../api/previews-and-estimates.md#create-preview).

### 檢視預估或預覽

預估和預覽程式會以非同步方式執行，因為不同的查詢可能需要不同的時間才能完成。 一旦查詢起始後，您可以使用API呼叫來擷取(GET)預估值的目前狀態或隨著查詢進行預覽。

使用 [!DNL Segmentation Service] API，您可以透過其ID來查詢預覽作業的目前狀態。 如果狀態為&quot;RESULT_READY&quot;，則可以查看結果。 要查找預覽作業的當前狀態，請閱讀 [檢索預覽作業部分](../api/previews-and-estimates.md#get-preview) 在預覽和估計端點指南中。 若要查找估計作業的當前狀態，請閱讀 [檢索估計作業](../api/previews-and-estimates.md#get-estimate) 在預覽和估計端點指南中。


## 後續步驟

開發、測試並儲存區段定義後，您就可以建立區段工作，以使用 [!DNL Segmentation Service] API。 請參閱 [評估和存取區段結果](./evaluate-a-segment.md) 以取得完成此作業的詳細步驟。
