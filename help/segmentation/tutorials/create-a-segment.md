---
solution: Experience Platform
title: 使用區段服務API建立區段定義
type: Tutorial
description: 按照本教學課程瞭解如何使用Adobe Experience Platform Segmentation Service API開發、測試、預覽和儲存區段定義。
exl-id: 78684ae0-3721-4736-99f1-a7d1660dc849
source-git-commit: f6d700087241fb3a467934ae8e64d04f5c1d98fa
workflow-type: tm+mt
source-wordcount: '1067'
ht-degree: 6%

---

# 使用區段服務API建立區段定義

本檔案提供使用[[!DNL Adobe Experience Platform Segmentation Service API]](../api/getting-started.md)開發、測試、預覽及儲存區段定義的教學課程。

有關如何使用使用者介面建立區段定義的資訊，請參閱[區段產生器指南](../ui/segment-builder.md)。

## 快速入門

此教學課程需要您實際瞭解建立區段定義所涉及的各種[!DNL Adobe Experience Platform]服務。 在開始本教學課程之前，請先檢閱下列服務的檔案：

- [[!DNL Real-Time Customer Profile]](../../profile/home.md)：根據來自多個來源的彙總資料，提供統一的即時消費者設定檔。
- [[!DNL Adobe Experience Platform Segmentation Service]](../home.md)：可讓您使用區段定義或其他外部來源，從即時客戶設定檔資料建立對象。
- [[!DNL Experience Data Model (XDM)]](../../xdm/home.md)： [!DNL Experience Platform]用來組織客戶體驗資料的標準化架構。 若要充分利用「細分」，請確定您的資料已根據[資料模型最佳實務](../../xdm/schema/best-practices.md)被擷取為設定檔和事件。

下列章節提供您需瞭解的其他資訊，才能成功呼叫[!DNL Experience Platform] API。

### 讀取範例 API 呼叫

本教學課程提供範例API呼叫，示範如何格式化您的請求。 這些包括路徑、必要的標頭和正確格式化的請求承載。 此外，也提供 API 回應中傳回的範例 JSON。 如需檔案中所使用範例API呼叫慣例的詳細資訊，請參閱[!DNL Experience Platform]疑難排解指南中[如何讀取範例API呼叫](../../landing/troubleshooting.md#how-do-i-format-an-api-request)一節。

### 收集所需標頭的值

若要呼叫[!DNL Experience Platform] API，您必須先完成[驗證教學課程](https://www.adobe.com/go/platform-api-authentication-en)。 完成驗證教學課程會提供所有 [!DNL Experience Platform] API 呼叫中每個必要標頭的值，如下所示：

- 授權：持有人`{ACCESS_TOKEN}`
- x-api-key： `{API_KEY}`
- x-gw-ims-org-id： `{ORG_ID}`

[!DNL Experience Platform]中的所有資源都與特定的虛擬沙箱隔離。 對[!DNL Experience Platform] API的所有請求都需要標頭，以指定將在其中執行作業的沙箱名稱：

- x-sandbox-name： `{SANDBOX_NAME}`

>[!NOTE]
>
>如需[!DNL Experience Platform]中沙箱的詳細資訊，請參閱[沙箱概觀檔案](../../sandboxes/home.md)。

所有包含承載 (POST、PUT、PATCH) 的請求都需有額外的標頭：

- Content-Type： application/json

## 開發區段定義

區段的第一個步驟是定義區段定義。 區段定義是封裝以[!DNL Profile Query Language] (PQL)撰寫的查詢的物件。 此物件也稱為PQL述詞。 PQL述詞會根據與您提供給[!DNL Real-Time Customer Profile]的任何記錄或時間序列資料相關的條件，定義區段定義的規則。 請參閱[PQL指南](../pql/overview.md)，以取得有關寫入PQL查詢的詳細資訊。

您可以對[!DNL Segmentation] API中的`/segment/definitions`端點發出POST要求，以建立新的區段定義。 下列範例概述如何格式化定義要求，包括要成功定義區段定義所需的資訊。

如需如何定義區段定義的詳細說明，請參閱[區段定義開發人員指南](../api/segment-definitions.md#create)。

## 預估和預覽對象 {#estimate-and-preview-an-audience}

當您開發區段定義時，可以使用[!DNL Real-Time Customer Profile]中的預估和預覽工具來檢視摘要層級的資訊，以協助確保您隔離預期的對象。 預估可提供區段定義的統計資訊，例如預計對象人數和信賴區間。 預覽可提供符合區段定義之資格設定檔的編頁清單，讓您比較結果與預期。

透過估計和預覽對象，您可以測試和最佳化PQL述詞，直到產生理想的結果，然後可以在更新的區段定義中使用這些述詞。

預覽或取得區段定義的預估值需要兩個步驟：

1. [建立預覽工作](#create-a-preview-job)
2. [使用預覽作業識別碼檢視預估或預覽](#view-an-estimate-or-preview)

### 如何產生預估值

為即時客戶個人檔案啟用的資料會擷取到Experience Platform中，並儲存在個人檔案資料存放區中。 當將記錄擷取至設定檔存放區後，設定檔總數增加或減少超過5%，則會觸發取樣工作以更新計數。 如果設定檔計數未變更超過5%，則取樣工作每週都會自動執行。

範例的觸發方式取決於所使用的擷取型別：

- 對於串流資料工作流程，會每小時進行一次檢查，以判斷是否符合增加或減少5%的臨界值。 如果達到此臨界值，則會自動觸發範例工作以更新計數。
- 對於批次擷取，在成功將批次擷取到設定檔存放區後15分鐘內，如果符合5%增加或減少臨界值，則會執行工作以更新計數。 使用設定檔API，您可以預覽最新成功的範例作業，以及依資料集和身分名稱空間列出設定檔分佈。

範例大小取決於設定檔存放區中的實體總數。 下表顯示這些範例大小：

| 設定檔存放區中的實體 | 抽樣大小 |
| ------------------------- | ----------- |
| 少於100萬 | 完整資料集 |
| 100萬到2000萬 | 100萬 |
| 超過2000萬 | 總數的5% |

預估通常超過10至15秒，從粗略的估計開始，並隨著閱讀更多記錄而調整。

### 建立預覽工作

您可以對`/preview`端點發出POST要求，以建立新的預覽工作。

建立預覽工作的詳細指示可以在[預覽和估計端點指南](../api/previews-and-estimates.md#create-preview)中找到。

### 檢視預估或預覽

預估和預覽程式會以非同步方式執行，因為不同的查詢可能需要不同的時間長度才能完成。 一旦啟動查詢後，您就可以使用API呼叫來擷取(GET)目前的預估或預覽狀態。

使用[!DNL Segmentation Service] API，您可以依據預覽作業的ID來查詢其目前狀態。 如果狀態為「RESULT_READY」，則可以檢視結果。 若要查詢預覽工作的目前狀態，請閱讀預覽與預估端點指南中[擷取預覽工作區段](../api/previews-and-estimates.md#get-preview)的區段。 若要查詢預估工作的目前狀態，請閱讀預覽與預估端點指南中[擷取預估工作](../api/previews-and-estimates.md#get-estimate)一節。


## 後續步驟

開發、測試並儲存區段定義後，您就可以建立區段工作，以使用[!DNL Segmentation Service] API建立對象。 請參閱有關[評估和存取區段結果](./evaluate-a-segment.md)的教學課程，以瞭解如何完成此工作的詳細步驟。
