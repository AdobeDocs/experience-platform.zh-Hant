---
keywords: Experience Platform；首頁；熱門主題；資料品質；品質；支援的驗證；驗證；支援的驗證；
solution: Experience Platform
title: 資料品質
description: 以下檔案提供Adobe Experience Platform中批次和串流內嵌支援的檢查和驗證行為摘要。
exl-id: 7ef40859-235a-4759-9492-c63e5fd80c8e
source-git-commit: e802932dea38ebbca8de012a4d285eab691231be
workflow-type: tm+mt
source-wordcount: '425'
ht-degree: 5%

---

# Adobe Experience Platform中的資料品質

Adobe Experience Platform針對透過批次或串流內嵌上傳的任何資料，提供明確定義的完整性、正確性和一致性保證。 以下檔案提供中批次和串流內嵌支援的檢查和驗證行為摘要 [!DNL Experience Platform].

## 支援的檢查

|   | 批次內嵌 | 串流擷取 |
| ------ | --------------- | ------------------- |
| 資料類型檢查 | 是 | 是 |
| 枚舉檢查 | 是 | 是 |
| 範圍檢查（最小值、最大值） | 是 | 是 |
| 必填欄位檢查 | 是 | 是 |
| 圖樣檢查 | 無 | 是 |
| 格式檢查 | 無 | 是 |

## 支援的驗證行為

批次和串流內嵌都會移動不良資料，以便在 [!DNL Data Lake]. 資料內嵌提供下列批次和串流內嵌驗證。

### 批次擷取

系統會針對批次擷取執行下列驗證：

| 驗證區域 | 說明 |
| --------------- | ----------- |
| 方案 | 確保架構為 **not** empty ，並包含對union架構的引用，如下所示： `"meta:immutableTags": ["union"]` |
| `identityField` | 確保定義所有有效的身份描述符。 |
| `createdUser` | 確保已擷取批次的使用者可以擷取批次。 |

### 串流擷取

會針對串流擷取執行下列驗證：

| 驗證區域 | 說明 |
| --------------- | ----------- |
| 方案 | 確保架構為 **not** empty ，並包含對union架構的引用，如下所示： `"meta:immutableTags": ["union"]` |
| `identityField` | 確保定義所有有效的身份描述符。 |
| JSON | 確保JSON有效。 |
| IMS組織 | 確保列出的IMS組織是有效的組織。 |
| 源名稱 | 確保指定資料源的名稱。 |
| 資料集 | 確保指定、啟用和未移除資料集。 |
| 標頭 | 確保標頭已指定且有效。 |

有關如何 [!DNL Platform] 監控和驗證資料可在 [監控資料流檔案](./monitor-data-ingestion.md).

## 身分值驗證

下表概述您必須遵循的現有規則，以確保身分值的驗證成功。

| 命名空間 | 驗證規則 | 違反規則時的系統行為 |
| --- | --- | --- |
| ECID | <ul><li>ECID的身分值必須恰好為38個字元。</li><li>ECID的身分值只能由數字組成。</li></ul> | <ul><li>如果ECID的身分值不是確切的38個字元，則會略過記錄。</li><li>如果ECID的身分值包含非數字字元，系統會略過記錄。</li></ul> |
| 非ECID | 身分值不能超過1024個字元。 | 如果標識值超過1024個字元，則跳過該記錄。 |

如需 [!DNL Identity Service] 護欄，看 [[!DNL Identity Service] 護欄概述](../../identity-service/guardrails.md).
