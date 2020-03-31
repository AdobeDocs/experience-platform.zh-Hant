---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: 資料擷取品質
topic: overview
translation-type: tm+mt
source-git-commit: 24df962656706d769a7034020d96a545e8f905ca

---


# Adobe Experience Platform中的資料品質

Adobe Experience Platform為透過批次或串流擷取上傳的任何資料，提供定義完善的保證，確保其完整性、正確性和一致性。 以下檔案提供Experience Platform中批次和串流擷取支援檢查與驗證行為的摘要。

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

批次和串流擷取功能都可在Data Lake中移動不良資料以擷取和分析，以防止失敗資料下游。 資料擷取提供下列批次和串流擷取驗證。

### 批次擷取

對批處理提取執行以下驗證：

| 驗證區域 | 說明 |
| --------------- | ----------- |
| 架構 | 確保架構不 **為空** ，並包含對聯合架構的引用，如下所示： `"meta:immutableTags": ["union"]` |
| `identityField` | 確保定義所有有效的身份描述符。 |
| `createdUser` | 確保接收批的用戶可以接收批。 |

### 串流擷取

對串流擷取執行下列驗證：

| 驗證區域 | 說明 |
| --------------- | ----------- |
| 架構 | 確保架構不 **為空** ，並包含對聯合架構的引用，如下所示： `"meta:immutableTags": ["union"]` |
| `identityField` | 確保定義所有有效的身份描述符。 |
| JSON | 確保JSON有效。 |
| IMS組織 | 確保列出的IMS組織為有效組織。 |
| 來源名稱 | 確保指定資料源的名稱。 |
| 資料集 | 確保指定、啟用和未刪除資料集。 |
| Header | 確保標題已指定且有效。 |

有關平台如何監控和驗證資料的詳細資訊，請參閱監控資 [料流檔案](./monitor-data-flows.md)。
