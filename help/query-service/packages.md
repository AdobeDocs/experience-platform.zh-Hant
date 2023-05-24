---
title: 查詢服務包
description: 以下文檔概述了可用於查詢服務的功能和產品包，並突出顯示了即席查詢和批處理查詢之間的差異。
exl-id: ba472d9e-afe6-423d-9abd-13ecea43f04f
source-git-commit: cde7c99291ec34be811ecf3c85d12fad09bcc373
workflow-type: tm+mt
source-wordcount: '714'
ht-degree: 3%

---

# 查詢服務包

本文檔概述了Query Service中提供的不同類型的打包和查詢執行功能。

Adobe Experience Platform查詢服務可以根據可以執行的查詢模式分為兩個功能：

- **即席查詢** 是SQL查詢，用於探索所攝取的資料集，以用於驗證、驗證、實驗等。 這些查詢不會將資料寫回平台資料湖。
- **批處理查詢** 是SQL查詢，用於執行所攝取資料集的接收後處理。 這些查詢是清理、形狀、操作和豐富資料，其結果將寫回平台資料湖。 這些查詢可以作為批處理作業進行計畫、管理和監視。

查詢服務功能與以下產品和載入項一起打包：

- **基於平台的應用程式** (Adobe Real-time Customer Data Platform、Adobe Customer Journey Analytics和Adobe Journey Optimizer):從一開始就提供用於執行臨時查詢的查詢服務訪問，其中包含基於平台的應用程式的每個變體和層。
- **[!DNL Data Distiller]** (可與Adobe Real-Time CDP、Customer Journey Analytics和Adobe Journey Optimizer一起購買的附加包):提供了用於執行批處理查詢的查詢服務訪問權限 [!DNL Data Distiller]。

下表根據查詢服務的打包方式概括了關鍵的Query Service權利：

| 查詢服務權利 | 與基於平台的應用程式打包在一起 | 打包 [!DNL Data Distiller] |
|---|---|---|
| 支援的查詢模式 | 僅專用查詢 | 批處理查詢 |
| 支援的使用案例 | <ul><li>探&#x200B;索</li><li>資料發&#x200B;現</li><li>資料驗證</li><li>實驗</li></ul> | <ul><li>清潔</li><li>成形</li><li>操縱</li><li>豐富</li></ul> |
| 支援的語義 | <ul><li>SELECT查詢</li></ul> | <ul><li>CTAS和ITAS查詢</li></ul> |
| 最長執行時間 | 10 分鐘 | 24 小時 |
| 許可證度量 | **查詢用戶併發**: <ul><li>1個併發用戶(Real-Time CDP、Adobe Journey Optimizer&#x200B;)</li><li>5個併發用戶(Customer Journey Analytics&#x200B;)</li></ul> **查詢併發**: <ul><li>1個併發運行查詢(所有應用程式&#x200B;)</li></ul> **附加的即席查詢用戶包載入項** 可以購買以增加客戶授權的即席查詢權利。 <ul><li>每包增加5個併發用戶</li><li>每個包都有1個附加並行運行查詢</li></ul> | **計算小時數**: <ul><li>變數（根據客戶的應用程式權利確定範圍）</li></ul> **計算小時數** 是查詢服務引擎在執行批處理查詢時讀取、處理和將資料寫回資料湖所花費的時間量。 |
| 查詢執行介面 | <ul><li>查詢服務UI</li><li>第三方客戶端UI</li><li>[!DNL PostgresSQL] 客戶端UI</li></ul> | <ul><li>查詢UI </li><li>第三方客戶端UI</li><li>[!DNL PostgresSQL] 客戶端UI</li><li>REST API</li></ul> |
| 通過返回的查詢結果 | 客戶端UI | 儲存在資料湖中的派生資料集 |
| 結果限制 | <ul><li>查詢UI - 100行</li><li>第三方客戶 — 50,000</li><li>[!DNL PostgresSQL] 客戶端 — 50,000</li></ul> | <ul><li>查詢UI（沒有行上限）</li><li>第三方客戶端（行上限）</li><li>[!DNL PostgresSQL] 客戶端（沒有行上限）</li><li>REST API（沒有行上限）</li></ul> |
| 讀取資料集容量 | 是 | 是 |
| 寫入資料集容量 | 無 | 是 |
| 計畫能力 | 無 | 是 |
| 監視容量 | 是 | 是 |
| 查詢預警設定容量 | 無 | 是 |

{style="table-layout:auto"}

## 存取控制

Experience Platform的訪問控制通過 [Adobe Admin Console](https://adminconsole.adobe.com/) 其中，產品配置檔案將用戶與權限和沙箱連結。 查看 [訪問控制概述](../access-control/home.md) 的子菜單。

為了使用查詢服務， [!DNL Manage Queries] 必須在管理控制台中啟用權限。 此權限允許用戶執行即席和批處理查詢。 請求訪問產品配置檔案的詳細說明 [!DNL Manage Queries] 權限已在 [管理產品配置檔案的權限](../access-control/ui/permissions.md) 和 [管理產品配置檔案的用戶](../access-control/ui/users.md) 的子菜單。

購買 [!DNL Data Distiller] 附加， [!DNL Write Dataset] 必須授予權限。 此權限允許 [!DNL Data Distiller] 執行批處理查詢的用戶。

下表概述了 [!DNL Manage Queries] 權限：

| 權限 | 函數 |
|---|---|
| [!DNL Manage Queries] （沒有寫資料權限） | 提供執行即席查詢的訪問 |
| [!DNL Manage Queries] （具有寫資料權限） | 提供對執行批處理查詢的訪問 |

{style="table-layout:auto"}

## 沙盒支援

沙箱是單個Experience Platform實例中的虛擬分區。 每個平台實例支援多個生產和非生產沙盒，每個沙盒都維護自己的平台資源庫。 非生產沙箱允許您test功能、運行實驗和制定定制配置，而不影響生產沙箱。 有關沙箱的詳細資訊，請參閱 [箱概述](../sandboxes/home.md)。 所有查詢服務權利均在所有沙箱中共用

## 後續步驟

通過閱讀此文檔，您應更好地瞭解查詢服務中提供的不同打包類型和查詢執行功能。 要瞭解有關查詢服務（如已知的行業使用案例）的詳細資訊，請閱讀 [使用案例文檔](./use-cases/abandoned-browse.md)。 有關更多一般資訊，請訪問 [查詢服務概述](./home.md)。
