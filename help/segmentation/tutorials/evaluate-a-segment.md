---
keywords: Experience Platform；主題；熱門主題；段評估；分段服務；分段；分段；評估段；訪問段結果；評估和訪問段；
solution: Experience Platform
title: 評估和訪問段結果
type: Tutorial
description: 按照本教程學習如何使用Adobe Experience Platform分段服務API評估段和訪問段結果。
exl-id: 47702819-f5f8-49a8-a35d-034ecac4dd98
source-git-commit: fcd44aef026c1049ccdfe5896e6199d32b4d1114
workflow-type: tm+mt
source-wordcount: '1607'
ht-degree: 0%

---

# 評估和訪問段結果

本文檔提供了一個教程，用於評估段和使用 [[!DNL Segmentation API]](../api/getting-started.md)。

## 快速入門

本教程需要對各種 [!DNL Adobe Experience Platform] 服務。 在開始本教程之前，請查看以下服務的文檔：

- [[!DNL Real-Time Customer Profile]](../../profile/home.md):根據來自多個來源的聚合資料即時提供統一的客戶配置檔案。
- [[!DNL Adobe Experience Platform Segmentation Service]](../home.md):允許您從 [!DNL Real-Time Customer Profile] 資料。
- [[!DNL Experience Data Model (XDM)]](../../xdm/home.md):平台組織客戶體驗資料的標準化框架。 為最好地利用分段，請確保根據 [資料建模的最佳做法](../../xdm/schema/best-practices.md)。
- [沙箱](../../sandboxes/home.md): [!DNL Experience Platform] 提供虛擬沙箱，將單個沙箱 [!DNL Platform] 實例到獨立的虛擬環境，以幫助開發和發展數字型驗應用程式。

### 必需的標題

本教程還要求您完成 [驗證教程](https://www.adobe.com/go/platform-api-authentication-en) 以便成功撥打 [!DNL Platform] API。 完成身份驗證教程將提供所有中每個必需標頭的值 [!DNL Experience Platform] API調用，如下所示：

- 授權：持 `{ACCESS_TOKEN}`
- x-api-key: `{API_KEY}`
- x-gw-ims-org-id: `{ORG_ID}`

中的所有資源 [!DNL Experience Platform] 與特定虛擬沙箱隔離。 請求 [!DNL Platform] API需要一個標頭，該標頭指定操作將在以下位置進行的沙盒的名稱：

- x-sandbox-name: `{SANDBOX_NAME}`

>[!NOTE]
>
>有關中的沙箱的詳細資訊 [!DNL Platform]，請參見 [沙盒概述文檔](../../sandboxes/home.md)。

所有POST、PUT和PATCH請求都需要附加標頭：

- 內容類型：應用程式/json

## 評估段 {#evaluate-a-segment}

開發、測試和保存段定義後，您就可以通過計畫評估或按需評估來評估段。

[計畫評估](#scheduled-evaluation) （也稱為「計劃分段」）允許您建立在特定時間運行導出作業的循環計畫，但 [按需評估](#on-demand-evaluation) 包括建立段作業以立即構建受眾。 下面將介紹每個步驟。

如果尚未完成 [使用分段API建立段](./create-a-segment.md) 教程或使用 [段生成器](../ui/overview.md)，請在繼續本教程之前執行此操作。

## 計畫評估 {#scheduled-evaluation}

通過計畫評估，您的組織可以建立定期計畫以自動運行導出作業。

>[!NOTE]
>
>可以為最多五(5)個合併策略的沙箱啟用計畫評估 [!DNL XDM Individual Profile]。 如果您的組織有五個以上的合併策略 [!DNL XDM Individual Profile] 在單個沙箱環境中，您將無法使用計畫的評估。

### 建立計畫

通過向 `/config/schedules` 端點，您可以建立調度並包括應觸發調度的特定時間。

有關使用此終結點的詳細資訊，請參閱 [計畫終結點指南](../api/schedules.md#create)

### 啟用計畫

預設情況下，建立計畫時處於非活動狀態，除非 `state` 屬性設定為 `active` 在建立(POST)請求正文中。 您可以啟用計畫(設定 `state` 至 `active`)，向PATCH請求 `/config/schedules` 端點，並在路徑中包括調度的ID。

有關使用此終結點的詳細資訊，請參閱 [計畫終結點指南](../api/schedules.md#update-state)

### 更新計畫時間

通過向Web站點發出PATCH請求，可以更新計畫時間 `/config/schedules` 端點，並在路徑中包括調度的ID。

有關使用此終結點的詳細資訊，請參閱 [計畫終結點指南](../api/schedules.md#update-schedule)

## 按需評估

按需評估允許您建立段作業，以便隨時生成受眾段。 與計畫評估不同，這隻在請求時才會發生，而不是重複。

### 建立段任務

段作業是一個非同步過程，可按需建立訪問群體段。 它引用段定義以及控制如何 [!DNL Real-Time Customer Profile] 合併配置檔案片段中重疊的屬性。 當網段作業成功完成時，您可以收集有關網段的各種資訊，如處理過程中可能發生的任何錯誤以及受眾的最終大小。 每次要刷新當前符合段定義的受眾時，都需要運行段作業。

您可以通過向以下站點發出POST請求來建立新段任務 `/segment/jobs` 端點 [!DNL Real-Time Customer Profile] API。

有關使用此終結點的詳細資訊，請參閱 [段作業終結點指南](../api/segment-jobs.md#create)

### 查找段作業狀態

您可以使用 `id` 用於特定段作業以執行查找請求(GET)，以查看作業的當前狀態。

有關使用此終結點的詳細資訊，請參閱 [段作業終結點指南](../api/segment-jobs.md#get)

## 解釋段結果

成功運行段作業時， `segmentMembership` 將為段中包括的每個輪廓更新映射。 `segmentMembership` 還儲存所有被攝取到的預評估受眾片段 [!DNL Platform]，允許與其他解決方案整合，例如 [!DNL Adobe Audience Manager]。

以下示例顯示 `segmentMembership` 屬性與每個單獨配置檔案記錄類似：

```json
{
  "segmentMembership": {
    "UPS": {
      "04a81716-43d6-4e7a-a49c-f1d8b3129ba9": {
        "timestamp": "2018-04-26T15:52:25+00:00",
        "status": "realized"
      },
      "53cba6b2-a23b-454a-8069-fc41308f1c0f": {
        "lastQualificationTime": "2018-04-26T15:52:25+00:00",
        "status": "realized"
      }
    },
    "Email": {
      "abcd@adobe.com": {
        "lastQualificationTime": "2017-09-26T15:52:25+00:00",
        "status": "exited"
      }
    }
  }
}
```

| 屬性 | 說明 |
| -------- | ----------- |
| `lastQualificationTime` | 斷言段成員身份和配置檔案輸入或退出段的時間戳。 |
| `status` | 作為當前請求一部分的段參與狀態。 必須等於以下已知值之一： <ul><li>`realized`:實體符合段的條件。</li><li>`exited`:實體正在退出段。</li></ul> |

>[!NOTE]
>
>位於 `exited` 超過30天的狀態，根據 `lastQualificationTime`，將被刪除。

## 訪問段結果

可通過以下兩種方式之一訪問段作業的結果：您可以訪問單個配置檔案或將整個受眾導出到資料集。

以下各節將更詳細地概述這些選項。

## 查找配置檔案

如果您知道要訪問的特定配置檔案，則可以使用 [!DNL Real-Time Customer Profile] API。 有關訪問單個配置檔案的完整步驟，請參見 [使用配置檔案API訪問即時客戶配置檔案資料](../../profile/api/entities.md) 教程。

## 導出段 {#export}

分段作業成功完成後( `status` 屬性為「成功」)，您可以將受眾導出到資料集，在該資料集中可以訪問並對其執行操作。

要導出受眾，需要執行以下步驟：

- [建立目標資料集](#create-a-target-dataset)  — 建立資料集以容納受眾成員。
- [在資料集中生成受眾配置檔案](#generate-profiles)  — 根據段作業的結果，使用XDM個人配置檔案填充資料集。
- [監視導出進度](#monitor-export-progress)  — 檢查導出過程的當前進度。
- [讀取受眾資料](#next-steps)  — 檢索代表受眾成員的生成的XDM個人配置檔案。

### 建立目標資料集 {#create-dataset}

導出訪問群體時，必須先建立目標資料集。 必須正確配置資料集以確保導出成功。

關鍵注意事項之一是資料集所基於的架構(`schemaRef.id` 中)。 要導出段，資料集必須基於 [!DNL XDM Individual Profile Union Schema] (`https://ns.adobe.com/xdm/context/profile__union`)。 聯合架構是系統生成的只讀架構，它聚合共用同一類的架構的欄位，在本例中是XDM Individual Profile類。 有關聯合視圖架構的詳細資訊，請參閱 [方案註冊開發人員指南的「即時客戶概要檔案」部分](../../xdm/api/getting-started.md)。

建立必要資料集有兩種方法：

- **使用API:** 本教程中接下來的步驟概述了如何建立引用 [!DNL XDM Individual Profile Union Schema] 使用 [!DNL Catalog] API。
- **使用UI:** 使用 [!DNL Adobe Experience Platform] 用戶介面建立引用聯合模式的資料集，請按照 [UI教程](../ui/overview.md) 然後返回本教程，繼續執行 [生成觀眾配置檔案](#generate-profiles)。

如果已有相容的資料集並知道其ID，則可以直接執行該步驟 [生成觀眾配置檔案](#generate-profiles)。

**API格式**

```http
POST /dataSets
```

**要求**

以下請求建立新資料集，在負載中提供配置參數。

```shell
curl -X POST \
  https://platform.adobe.io/data/foundation/catalog/dataSets \
  -H 'Content-Type: application/json' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
    "name": "Segment Export",
    "schemaRef": {
        "id": "https://ns.adobe.com/xdm/context/profile__union",
        "contentType": "application/vnd.adobe.xed+json;version=1"
    }
}'
```

| 屬性 | 說明 |
| -------- | ----------- |
| `name` | 資料集的描述性名稱。 |
| `schemaRef.id` | 資料集將與之關聯的聯合視圖（架構）的ID。 |

**回應**

成功的響應返回包含新建立的資料集的只讀、系統生成的唯一ID的陣列。 要成功導出受眾成員，需要正確配置的資料集ID。

```json
[
  "@/datasets/5b020a27e7040801dedba61b"
] 
```

### 為受眾成員生成配置檔案 {#generate-profiles}

一旦您擁有了聯合持續資料集，就可以建立導出作業，通過向Web站點發出POST請求，將訪問群體成員持續到資料集 `/export/jobs` 端點 [!DNL Real-Time Customer Profile] API，並提供要導出的段的資料集ID和段資訊。

有關使用此終結點的詳細資訊，請參閱 [導出作業終結點指南](../api/export-jobs.md#create)

### 監視導出進度

作為導出作業流程，您可以通過嚮導出GET請求 `/export/jobs` 端點和包括 `id` 的子菜單。 導出作業一旦完成 `status` 欄位返回值「SUCCEEDED」。

有關使用此終結點的詳細資訊，請參閱 [導出作業終結點指南](../api/export-jobs.md#get)

## 後續步驟

成功完成導出後，您的資料可在 [!DNL Data Lake] 在 [!DNL Experience Platform]。 然後，您可以使用 [[!DNL Data Access API]](https://www.adobe.io/experience-platform-apis/references/data-access/) 使用 `batchId` 與導出關聯。 根據段的大小，資料可能以塊為單位，批可能由幾個檔案組成。

有關如何使用的逐步說明 [!DNL Data Access] 訪問和下載批處理檔案的API，請遵循 [資料存取教程](../../data-access/tutorials/dataset-data.md)。

您還可以使用 [!DNL Adobe Experience Platform Query Service]。 使用UI或REST風格的API, [!DNL Query Service] 允許您對內部資料寫入、驗證和運行查詢 [!DNL Data Lake]。

有關如何查詢受眾資料的詳細資訊，請查看 [[!DNL Query Service]](../../query-service/home.md)。
