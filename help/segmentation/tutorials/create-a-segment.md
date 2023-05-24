---
keywords: Experience Platform；首頁；熱門主題；段；段；段；建立段；分段；建立段；分段；分段；分段；分段服務；
solution: Experience Platform
title: 使用分段服務API建立段
type: Tutorial
description: 按照本教程學習如何使用Adobe Experience Platform分段服務API開發、test、預覽和保存段定義。
exl-id: 78684ae0-3721-4736-99f1-a7d1660dc849
source-git-commit: 59dfa862388394a68630a7136dee8e8988d0368c
workflow-type: tm+mt
source-wordcount: '948'
ht-degree: 1%

---

# 使用分段服務API建立段

本文檔提供了一個教程，用於使用 [[!DNL Adobe Experience Platform Segmentation Service API]](../api/getting-started.md)。

有關如何使用用戶介面構建段的資訊，請參閱 [段生成器指南](../ui/overview.md)。

## 快速入門

本教程需要對各種 [!DNL Adobe Experience Platform] 服務。 在開始本教程之前，請查看以下服務的文檔：

- [[!DNL Real-Time Customer Profile]](../../profile/home.md):基於來自多個源的聚合資料提供統一、即時的用戶配置檔案。
- [[!DNL Adobe Experience Platform Segmentation Service]](../home.md):允許您從即時客戶配置檔案資料構建受眾段。
- [[!DNL Experience Data Model (XDM)]](../../xdm/home.md):標準化框架 [!DNL Platform] 組織客戶體驗資料。 為最好地利用分段，請確保根據 [資料建模的最佳做法](../../xdm/schema/best-practices.md)。

以下各節提供了您需要瞭解的其他資訊，以便成功呼叫 [!DNL Platform] API。

### 讀取示例API調用

本教程提供了示例API調用，以演示如何格式化請求。 這些包括路徑、必需的標頭和正確格式化的請求負載。 還提供了API響應中返回的示例JSON。 有關示例API調用文檔中使用的約定的資訊，請參見上的 [如何讀取示例API調用](../../landing/troubleshooting.md#how-do-i-format-an-api-request) 的 [!DNL Experience Platform] 疑難解答指南。

### 收集所需標題的值

為了呼叫 [!DNL Platform] API，必須首先完成 [驗證教程](https://www.adobe.com/go/platform-api-authentication-en)。 完成身份驗證教程將提供所有中每個必需標頭的值 [!DNL Experience Platform] API調用，如下所示：

- 授權：持 `{ACCESS_TOKEN}`
- x-api-key: `{API_KEY}`
- x-gw-ims-org-id: `{ORG_ID}`

中的所有資源 [!DNL Experience Platform] 與特定虛擬沙箱隔離。 所有請求 [!DNL Platform] API需要一個標頭，該標頭指定操作將在以下位置進行的沙盒的名稱：

- x-sandbox-name: `{SANDBOX_NAME}`

>[!NOTE]
>
>有關中的沙箱的詳細資訊 [!DNL Platform]，請參見 [沙盒概述文檔](../../sandboxes/home.md)。

包含負載(POST、PUT、PATCH)的所有請求都需要附加的標頭：

- 內容類型：應用程式/json

## 制定段定義

分割的第一步是定義一個段，該段在稱為段定義的構造中表示。 段定義是封裝寫入的查詢的對象 [!DNL Profile Query Language] (PQL)。 此對象也稱為PQL謂詞。 PQL謂語基於與您提供給的任何記錄或時間序列資料相關的條件，為段定義規則 [!DNL Real-Time Customer Profile]。 查看 [PQL指南](../pql/overview.md) 的子菜單。

可通過向Web站點發出POST請求來建立新段定義 `/segment/definitions` 端點 [!DNL Segmentation] API。 以下示例概述了如何格式化定義請求，包括要成功定義段所需的資訊。

有關如何定義段的詳細說明，請閱讀 [段定義開發者指南](../api/segment-definitions.md#create)。

## 預估和預覽對象 {#estimate-and-preview-an-audience}

在開發段定義時，可以在 [!DNL Real-Time Customer Profile] 查看摘要級資訊，以幫助您隔離預期的受眾。 估計提供關於段定義的統計資訊，如預計受眾規模和置信區間。 預覽提供段定義的限定配置檔案的分頁清單，允許您將結果與預期結果進行比較。

通過估計和預覽受眾，您可以test和優化PQL謂語，直到它們產生可期望的結果，然後在更新的段定義中使用它們。

預覽或獲取段的估計需要兩個步驟：

1. [建立預覽作業](#create-a-preview-job)
2. [查看估計或預覽](#view-an-estimate-or-preview) 使用預覽作業的ID

### 如何生成估計

資料樣本用於評估段和估計合格配置檔案的數量。 每天早晨將新資料載入到記憶體（在12AM-2AM PT之間，即7-9AM UTC之間），並且使用當天的樣本資料來估計所有分段查詢。 因此，增加的任何新欄位或收集的額外資料將反映在次日的估計數中。

示例大小取決於配置檔案儲存中的實體總數。 下表顯示了這些示例大小：

| 配置檔案儲存中的實體 | 示例大小 |
| ------------------------- | ----------- |
| 不到100萬 | 完整資料集 |
| 1到2000萬 | 100萬 |
| 2000多萬 | 5% |

估計通常在10到15秒內完成，從粗略估計開始，隨著讀取更多記錄而細化。

### 建立預覽作業

通過向POST請求建立新預覽作業 `/preview` 端點。

有關建立預覽作業的詳細說明，請參閱 [預覽和估計端點指南](../api/previews-and-estimates.md#create-preview)。

### 查看估計或預覽

評估和預覽過程非同步運行，因為不同的查詢可能需要不同的時間來完成。 一旦啟動查詢，您就可以使用API調用來檢索(GET)估計或預覽的當前狀態。

使用 [!DNL Segmentation Service] API，可以通過預覽作業的ID查找其當前狀態。 如果狀態為「RESULT_READY」，則可以查看結果。 要查找預覽作業的當前狀態，請閱讀上的部分 [檢索預覽作業區](../api/previews-and-estimates.md#get-preview) 在預覽和估計端點指南中。 要查找評估作業的當前狀態，請閱讀上的部分 [檢索估計作業](../api/previews-and-estimates.md#get-estimate) 在預覽和估計端點指南中。


## 後續步驟

開發、測試和保存段定義後，您可以建立段作業，以使用 [!DNL Segmentation Service] API。 請參閱上的教程 [評估和訪問段結果](./evaluate-a-segment.md) 詳細的步驟。
