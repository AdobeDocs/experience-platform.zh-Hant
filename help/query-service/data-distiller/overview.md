---
title: 資料Distiller概述
description: 與您的授權權限相關的查詢服務資料的資料Distiller使用限制摘要。
source-git-commit: fa4fc154f57243250dec9bdf9557db13ef7768e8
workflow-type: tm+mt
source-wordcount: '553'
ht-degree: 0%

---

# 資料Distiller概觀

Data Distiller是套件，包含Adobe Experience Platform中的一部分功能。 透過Data Distiller，您可以在Query Service中執行批次查詢，針對即時客戶設定檔或分析使用案例，執行擷取後資料準備（例如清理、整形和操作）。 您使用Data Distiller的方式取決於您目前持續取得的下列其中一項授權：Adobe Real-time Customer Data Platform、Customer Journey Analytics和/或Adobe Journey Optimizer。

## 授權使用情況 {#license-usage}

請參閱 [資料Distiller授權使用檔案](./license-usage.md) 查看貴組織的查詢服務許可證使用情況的重要資訊。

## 範圍參數 {#scoping-parameters}

範圍參數是與您的授權容量所定義的建議使用案例範圍相關的使用限制。 若不使用附加元件，Data Distiller的範圍劃分參數如下：

* **計算小時數**:您可以使用PSQL或Query Service API來執行在任何沙箱（已排程或其他）中執行的批次查詢，以掃描和寫入資料。 這會根據授權合約的範圍界定程式，使用您每年分配的計算小時數。 所有沙箱中會累計總計計算小時數。
* **擷取的資料**:擷取至Adobe Experience Platform(可使用Data Distiller查詢)的資料受您目前對Adobe Real-time Customer Data Platform、Customer Journey Analytics和/或Adobe Journey Optimizer的授權中所述的限制所限。
* **資料湖儲存**:您目前取得的Adobe Real-time Customer Data Platform、Customer Journey Analytics和/或Adobe Journey Optimizer授權中提供的資料湖儲存空間，也可與Data Distiller搭配使用。 資料湖儲存是一項共用功能。
* **查詢服務用戶**:在您目前的Adobe Real-time Customer Data Platform、Customer Journey Analytics和/或Adobe Journey Optimizer授權中詳述的Query Service使用者人數，也可與Data Distiller搭配使用。 查詢服務使用者是共用功能。

## 護欄

請參閱 [查詢服務護欄](../guardrails.md) 有關與您的授權權限相關的查詢服務資料預設使用限制的檔案。

## 靜態限制

靜態限制是與Adobe Experience Platform啟動的功能界限相關的使用限制。 [有關Adobe Experience Platform Activation的詳細資訊](https://helpx.adobe.com/ca/legal/product-descriptions/adobe-experience-platform0.html) 可在Adobe幫助文檔中找到。 以下列出資料Distiller靜態限制的摘要，如需更完整的資訊，請參閱查詢服務護欄檔案。

* **批次查詢**:排程的批次查詢會在24小時後逾時。
* **查詢服務**:您可以將Query Service用於下列用途：
   * 執行SQL查詢以進行資料分析和擷取後資料準備（清除、整形和操作）。
   * 若要執行SQL查詢以建立統計量度以直接顯示在BI工具中。
   * 在Adobe Experience Platform中快速檢查資料。
* **報表API呼叫**:若要確保使用報告API在匯總資料上執行查詢，有足夠的資源可有效執行。 這包括可增強現有資料模型(例如Real-time Customer Data Platform提供的資料模型)的查詢。 報表API會為每個查詢指派併發槽，以追蹤資源利用率。 最多可同時使用4個報表API呼叫。 如果您透過BI工具存取報表API，且需要更多並行插槽，則需要BI伺服器。


