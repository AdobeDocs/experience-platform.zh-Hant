---
title: 查詢服務包
description: 以下檔案概述可用於Query Service的功能和產品套件，並強調臨機和批次查詢之間的差異。
source-git-commit: 3d2802ff5cdb359b28da23a05d1d6831cc273a52
workflow-type: tm+mt
source-wordcount: '718'
ht-degree: 3%

---

# 查詢服務包

本檔案概述Query Service中可用的不同類型封裝和查詢執行功能。

Adobe Experience Platform查詢服務可根據可執行的查詢模式，分為兩種功能：

- **臨機查詢** 是SQL查詢，用於探索擷取的資料集，以進行驗證、驗證、實驗等。 這些查詢不會將資料回寫至Platform資料湖。
- **批次查詢** 是SQL查詢，用於對擷取的資料集執行擷取後處理。 這些查詢會清理、塑造、操控及擴充資料，其結果會寫回Platform資料湖。 這些查詢可以作為批處理作業進行計畫、管理和監視。

查詢服務功能包含下列產品和附加元件：

- **基於平台的應用程式** (Real-time Customer Data Platform、Customer Journey Analytics和Adobe Journey Optimizer):從一開始就提供執行臨機查詢的查詢服務存取權，其中包含平台式應用程式的每個變異和層級。
- **[!DNL Data Distiller]** (可與Adobe Real-Time CDP、Customer Journey Analytics和Adobe Journey Optimizer一起購買的附加套件):提供用於執行批處理查詢的查詢服務訪問 [!DNL Data Distiller].

下表根據查詢服務的封裝方式概述了關鍵的查詢服務權限：

| 查詢服務權限 | 與基於平台的應用程式打包 | 封裝 [!DNL Data Distiller] |
|---|---|---|
| 支援的查詢模式 | 僅臨機查詢 | 批次查詢 |
| 支援的使用案例 | <ul><li>探&#x200B;索</li><li>資料探&#x200B;索</li><li>資料驗證</li><li>實驗</li></ul> | <ul><li>清潔</li><li>整形</li><li>操控</li><li>豐富</li></ul> |
| 支援語義 | <ul><li>選擇查詢</li></ul> | <ul><li>CTAS和ITAS查詢</li></ul> |
| 最大執行時間 | 10 分鐘 | 24 小時 |
| 授權量度 | **查詢用戶併發**: <ul><li>1名同時使用者(Real-time CDP, Adobe Journey Optimizer&#x200B;)</li><li>5個同時使用者(Customer Journey Analytics&#x200B;)</li></ul> **查詢併發**: <ul><li>1個併發運行查詢（所有應用程式）&#x200B;</li></ul> **其他臨機查詢使用者套件附加元件** 可購買，以增加客戶的授權臨機查詢權限。 <ul><li>每包多5個併發用戶</li><li>每個包附加1個併發運行查詢</li></ul> | **計算小時數**: <ul><li>變數（根據客戶的應用程式權限限定範圍）</li></ul> **計算小時數** 是查詢服務引擎在執行批次查詢時讀取、處理和將資料寫回資料湖所花費的時間量。 |
| 查詢執行介面 | <ul><li>查詢服務UI</li><li>第三方用戶端UI</li><li>[!DNL PostgresSQL] 用戶端UI</li></ul> | <ul><li>查詢UI </li><li>第三方用戶端UI</li><li>[!DNL PostgresSQL] 用戶端UI</li><li>REST API</li></ul> |
| 透過傳回的查詢結果 | 用戶端UI | 資料湖中儲存的衍生資料集 |
| 結果限制 | <ul><li>查詢UI - 100列</li><li>第三方客戶端 — 50,000</li><li>[!DNL PostgresSQL] 客戶端 — 50,000</li></ul> | <ul><li>查詢UI（沒有列上限）</li><li>第三方用戶端（無列上限）</li><li>[!DNL PostgresSQL] 用戶端（沒有列上限）</li><li>REST API（無列上限）</li></ul> |
| 讀取資料集容量 | 是 | 是 |
| 寫入資料集容量 | 無 | 是 |
| 計畫容量 | 無 | 是 |
| 監控容量 | 是 | 是 |
| 查詢警報設定容量 | 無 | 是 |

{style=&quot;table-layout:auto&quot;}

## 存取控制

Experience Platform的存取控制透過 [Adobe Admin Console](https://adminconsole.adobe.com/) 其中，產品設定檔會將使用者連結至權限和沙箱。 請參閱 [存取控制概觀](../access-control/home.md) 以取得更多資訊。

若要使用查詢服務， [!DNL Manage Queries] 必須在admin console中啟用權限。 此權限可讓使用者執行臨機和批次查詢。 要求存取產品設定檔的詳細指示 [!DNL Manage Queries] 權限已概述於 [管理產品設定檔的權限](../access-control/ui/permissions.md) 和 [管理產品設定檔的使用者](../access-control/ui/users.md) 檔案。

購買 [!DNL Data Distiller] 附加元件， [!DNL Write Dataset] 必須授予權限。 此權限允許 [!DNL Data Distiller] 用於執行批處理查詢的用戶。

下表概述 [!DNL Manage Queries] 權限：

| 權限 | 函數 |
|---|---|
| [!DNL Manage Queries] （無寫資料權限） | 提供執行臨機查詢的存取權 |
| [!DNL Manage Queries] （具有寫資料權限） | 提供執行批處理查詢的訪問 |

{style=&quot;table-layout:auto&quot;}

## 沙箱支援

沙箱是單一Experience Platform例項中的虛擬分區。 每個Platform例項都支援多種製作和非製作沙箱，每個沙箱都會維護其專屬的Platform資源程式庫。 非生產沙箱可讓您測試功能、執行實驗及進行自訂設定，而不會影響生產沙箱。 如需沙箱的詳細資訊，請參閱 [沙箱概述](../sandboxes/home.md). 所有查詢服務權限都會在所有沙箱間共用

## 後續步驟

閱讀本檔案後，您應更清楚了解Query Service中可用的不同封裝類型和查詢執行功能。 若要進一步了解Query Service，例如業界知名的使用案例，請參閱 [使用案例檔案](./use-cases/abandoned-browse.md). 如需更一般的資訊，請造訪 [查詢服務概述](./home.md).
