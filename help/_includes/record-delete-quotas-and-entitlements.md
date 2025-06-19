---
source-git-commit: 1ab56cf2495238385d726277f6409d2e0c0cb017
workflow-type: tm+mt
source-wordcount: '364'
ht-degree: 3%

---
# 程式碼片段

## 配額與處理時間表 {#quotas}

記錄刪除請求受到每日和每月識別碼提交限制的約束，此限制取決於您組織的授權權益。 這些限制同時適用於UI和API型刪除請求。

>[!NOTE]
>
>您每天最多可以提交&#x200B;**1,000,000個識別碼**，但前提是剩餘的每月配額允許。 如果您的每月上限少於100萬，則每日提交內容不能超過該上限。

### 依產品的每月提交權利 {#quota-limits}

下表概述產品和權益層級的識別碼提交限制。 對於每種產品，每月上限是兩個值中較小者：固定的識別碼上限，或與授權資料量繫結的百分比型臨界值。

| 產品 | 權益說明 | 每月上限（以較小者為準） |
|----------|-------------------------|---------------------------------|
| Real-Time CDP或Adobe Journey Optimizer | 不含Privacy and Security Shield或Healthcare Shield附加元件 | 2,000,000個識別碼或可定址對象的5% |
| Real-Time CDP或Adobe Journey Optimizer | 搭配Privacy and Security Shield或Healthcare Shield附加元件 | 15,000,000個識別碼或10%的可定址對象 |
| Customer Journey Analytics | 不含Privacy and Security Shield或Healthcare Shield附加元件 | 每百萬個CJA權益列有2,000,000個識別碼或100個識別碼 |
| Customer Journey Analytics | 搭配Privacy and Security Shield或Healthcare Shield附加元件 | 每百萬個CJA權益列有15,000,000個識別碼或200個識別碼 |

>[!NOTE]
>
> 根據組織的實際可定址對象或CJA列權益，大多陣列織的每月限制會較低。

配額在每個日曆月的第一天重設。 未使用的配額&#x200B;**不會**&#x200B;延續。

>[!NOTE]
>
>配額是以貴組織針對&#x200B;**已提交識別碼**&#x200B;的每月授權為基礎。 系統護欄不會強制執行這些動作，但可加以監控和檢閱。
>
>記錄刪除是&#x200B;**共用服務**。 您的每月上限反映了Real-Time CDP、Adobe Journey Optimizer、Customer Journey Analytics和任何適用的Shield附加元件的最高權益。

### 處理識別碼提交的時間表 {#sla-processing-timelines}

提交後，記錄刪除請求會根據您的權益層級排入佇列並進行處理。

| 產品與權益說明 | 佇列持續時間 | 最大處理時間(SLA) |
|------------------------------------------------------------------------------------|---------------------|-------------------------------|
| 不含Privacy and Security Shield或Healthcare Shield附加元件 | 最多15天 | 30 天 |
| 搭配Privacy and Security Shield或Healthcare Shield附加元件 | 通常為24小時 | 15 天 |

如果您的組織需要更高的限制，請聯絡您的Adobe代表以要求軟體權利檔案審查。
