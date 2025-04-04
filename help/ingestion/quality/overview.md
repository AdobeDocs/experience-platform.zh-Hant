---
keywords: Experience Platform；首頁；熱門主題；資料品質；品質；品質；支援的驗證；驗證；支援的驗證；
solution: Experience Platform
title: 資料品質
description: 以下檔案提供Adobe Experience Platform中批次和串流擷取支援的檢查和驗證行為摘要。
exl-id: 7ef40859-235a-4759-9492-c63e5fd80c8e
source-git-commit: b48c24ac032cbf785a26a86b50a669d7fcae5d97
workflow-type: tm+mt
source-wordcount: '427'
ht-degree: 5%

---

# Adobe Experience Platform的資料品質

Adobe Experience Platform針對透過批次或串流擷取上傳的任何資料，提供完整、準確及一致的明確定義保證。 下列檔案提供[!DNL Experience Platform]中批次和串流擷取支援的檢查和驗證行為摘要。

## 支援的檢查

|   | 批次擷取 | 串流擷取 |
| ------ | --------------- | ------------------- |
| 資料型別檢查 | 是 | 是 |
| 列舉檢查 | 是 | 是 |
| 範圍檢查（最小、最大） | 是 | 是 |
| 必填欄位檢查 | 是 | 是 |
| 圖樣檢查 | 無 | 是 |
| 格式檢查 | 無 | 是 |

## 支援的驗證行為

批次和串流擷取都會將不良資料移動到[!DNL Data Lake]中進行擷取和分析，以防止失敗的資料向下游傳送。 資料擷取針對批次和串流擷取提供下列驗證。

### 批次擷取

會針對批次擷取完成下列驗證：

| 驗證區域 | 說明 |
| --------------- | ----------- |
| 結構描述 | 確保結構描述是&#x200B;**非**&#x200B;空的，並包含對聯合結構描述的參考，如下所示： `"meta:immutableTags": ["union"]` |
| `identityField` | 請確定已定義所有有效的身分描述項。 |
| `createdUser` | 確保允許擷取批次的使用者擷取批次。 |

### 串流擷取

以下驗證會針對串流擷取完成：

| 驗證區域 | 說明 |
| --------------- | ----------- |
| 結構描述 | 確保結構描述是&#x200B;**非**&#x200B;空的，並包含對聯合結構描述的參考，如下所示： `"meta:immutableTags": ["union"]` |
| `identityField` | 請確定已定義所有有效的身分描述項。 |
| JSON | 確保JSON有效。 |
| 組織 | 確保列出的組織是有效的組織。 |
| 來源名稱 | 請確定已指定資料來源的名稱。 |
| 資料集 | 確保資料集已指定、啟用且未移除。 |
| 標頭 | 請確定標頭已指定且有效。 |

在[監視資料流程檔案](./monitor-data-ingestion.md)中可以找到[!DNL Experience Platform]如何監視及驗證資料的詳細資訊。

## 身分值驗證

下表概述您必須遵循的現有規則，以確保身分值成功驗證。

| 命名空間 | 驗證規則 | 違反規則時的系統行為 |
| --- | --- | --- |
| ECID | <ul><li>ECID的身分值必須剛好38個字元。</li><li>ECID的身分值必須僅由數字組成。</li></ul> | <ul><li>如果ECID的身分值不完全是38個字元，則會略過記錄。</li><li>如果ECID的身分值包含非數字字元，則會略過記錄。</li></ul> |
| 非ECID | 身分值不可超過1024個字元。 | 如果身分值超過1024個字元，則會略過記錄。 |

如需[!DNL Identity Service]護欄的詳細資訊，請參閱[[!DNL Identity Service] 護欄概觀](../../identity-service/guardrails.md)。
