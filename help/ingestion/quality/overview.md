---
keywords: Experience Platform;home；熱門主題；資料質量；質量；支援的驗證；支援的驗證；
solution: Experience Platform
title: 資料品質
topic-legacy: overview
description: 以下檔案摘要說明在Adobe Experience Platform支援的批次和串流擷取檢查與驗證行為。
exl-id: 7ef40859-235a-4759-9492-c63e5fd80c8e
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '317'
ht-degree: 6%

---

# Adobe Experience Platform的資料質量

Adobe Experience Platform為透過批次或串流擷取上傳的任何資料提供明確定義的完整性、正確性和一致性保證。 以下檔案提供[!DNL Experience Platform]中支援的批次和串流擷取檢查與驗證行為的摘要。

## 支援的檢查

|   | 批次擷取 | 串流擷取 |
| ------ | --------------- | ------------------- |
| 資料類型檢查 | 是 | 是 |
| 列舉檢查 | 是 | 是 |
| 範圍檢查（最小值、最大值） | 是 | 是 |
| 必填欄位檢查 | 是 | 是 |
| 模式檢查 | 無 | 是 |
| 格式檢查 | 無 | 是 |

## 支援的驗證行為

批處理和串流擷取功能都可在[!DNL Data Lake]中移動不良資料以擷取和分析，以防止失敗資料下游。 資料擷取提供下列批次和串流擷取驗證。

### 批次擷取

對批處理提取執行以下驗證：

| 驗證區域 | 說明 |
| --------------- | ----------- |
| 結構 | 確保架構為&#x200B;**not**&#x200B;空，並包含對聯合架構的引用，如下所示：`"meta:immutableTags": ["union"]` |
| `identityField` | 確保定義所有有效的身份描述符。 |
| `createdUser` | 確保接收批的用戶可以接收批。 |

### 串流擷取

對串流擷取執行下列驗證：

| 驗證區域 | 說明 |
| --------------- | ----------- |
| 結構 | 確保架構為&#x200B;**not**&#x200B;空，並包含對聯合架構的引用，如下所示：`"meta:immutableTags": ["union"]` |
| `identityField` | 確保定義所有有效的身份描述符。 |
| JSON | 確保JSON有效。 |
| IMS組織 | 確保列出的IMS組織為有效組織。 |
| 來源名稱 | 確保指定資料源的名稱。 |
| 資料集 | 確保指定、啟用和未刪除資料集。 |
| 標頭 | 確保標題已指定且有效。 |

有關[!DNL Platform]如何監視和驗證資料的詳細資訊，請參閱[監視資料流文檔](./monitor-data-ingestion.md)。
