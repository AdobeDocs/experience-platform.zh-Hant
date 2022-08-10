---
keywords: Experience Platform；首頁；熱門主題；資料質量；質量；支援的驗證；驗證；支援的驗證；
solution: Experience Platform
title: 資料質量
topic-legacy: overview
description: 以下文檔提供了Adobe Experience Platform中批處理和流接收支援的檢查和驗證行為的摘要。
exl-id: 7ef40859-235a-4759-9492-c63e5fd80c8e
source-git-commit: 7857b9a82dc1b5e12c9f8d757f6967b926124ec4
workflow-type: tm+mt
source-wordcount: '425'
ht-degree: 5%

---

# Adobe Experience Platform資料質量

Adobe Experience Platform為通過批處理或流式接收上傳的任何資料提供了明確定義的完整性、準確性和一致性保證。 以下文檔提供了支援的批處理和流式接收檢查和驗證行為的摘要 [!DNL Experience Platform]。

## 支援的檢查

|   | 批量攝取 | 流攝入 |
| ------ | --------------- | ------------------- |
| 資料類型檢查 | 是 | 是 |
| 枚舉檢查 | 是 | 是 |
| 範圍檢查（最小、最大） | 是 | 是 |
| 必填欄位檢查 | 是 | 是 |
| 模式檢查 | 無 | 是 |
| 格式檢查 | 無 | 是 |

## 支援的驗證行為

批處理和流式接收都通過移動不良資料以在中進行檢索和分析，防止了故障資料下游 [!DNL Data Lake]。 資料接收為批處理和流式處理接收提供了以下驗證。

### 批次擷取

對批接收執行以下驗證：

| 驗證區域 | 說明 |
| --------------- | ----------- |
| 方案 | 確保架構 **不** 空，包含對聯合架構的引用，如下所示： `"meta:immutableTags": ["union"]` |
| `identityField` | 確保定義了所有有效的身份描述符。 |
| `createdUser` | 確保允許接收批的用戶接收批。 |

### 串流擷取

對流接收執行以下驗證：

| 驗證區域 | 說明 |
| --------------- | ----------- |
| 方案 | 確保架構 **不** 空，包含對聯合架構的引用，如下所示： `"meta:immutableTags": ["union"]` |
| `identityField` | 確保定義了所有有效的身份描述符。 |
| JSON | 確保JSON有效。 |
| IMS組織 | 確保列出的IMS組織是有效組織。 |
| 源名稱 | 確保指定資料源的名稱。 |
| 資料集 | 確保已指定、啟用且未刪除資料集。 |
| 標頭 | 確保已指定標題且其有效。 |

有關如何 [!DNL Platform] 監視和驗證資料可在 [監視資料流文檔](./monitor-data-ingestion.md)。

## 標識值驗證

下表概述了必須遵循的現有規則，以確保成功驗證您的標識值。

| 命名空間 | 驗證規則 | 違反規則時的系統行為 |
| --- | --- | --- |
| ECID | <ul><li>ECID的標識值必須正好是38個字元。</li><li>ECID的標識值必須只包含數字。</li></ul> | <ul><li>如果ECID的標識值不是正好38個字元，則跳過記錄。</li><li>如果ECID的標識值包含非數字字元，則跳過記錄。</li></ul> |
| 非ECID | 標識值不能超過1024個字元。 | 如果標識值超過1024個字元，則跳過記錄。 |

有關 [!DNL Identity Service] 護欄，看 [[!DNL Identity Service] 護欄概述](../../identity-service/guardrails.md)。
