---
title: 查詢服務封裝
description: 以下檔案概述查詢服務可用功能和產品的包裝，並著重說明隨機查詢和批次查詢之間的差異。
exl-id: ba472d9e-afe6-423d-9abd-13ecea43f04f
source-git-commit: 47f02f6d1d4017dfe0fccddcd137487e064b3039
workflow-type: tm+mt
source-wordcount: '930'
ht-degree: 2%

---

# 查詢服務封裝

本檔案概述查詢服務中可用的不同型別封裝和查詢執行功能。

根據可以執行的查詢模式，Adobe Experience Platform查詢服務可以分成兩個功能：

- **臨時查詢** SQL查詢是用於探索用於驗證、驗證、實驗等擷取資料集的。 這些查詢不會將資料寫回Platform資料湖。
- **批次查詢** SQL查詢是否用於執行擷取資料集的擷取後處理。 這些查詢會清除、調整、操縱及擴充資料，且結果會回寫至Platform Data Lake。 這些查詢可以作為批次作業進行排程、管理和監視。

查詢服務功能會與下列產品和附加元件一起封裝：

- **平台式應用程式** (Adobe Real-time Customer Data Platform、Adobe Customer Journey Analytics和Adobe Journey Optimizer)：查詢服務存取權從一開始就會針對平台式應用程式的每個變數和層級提供，以執行臨時查詢。
- **[!DNL Data Distiller]** (可與Adobe Real-Time CDP、Customer Journey Analytics和Adobe Journey Optimizer一起購買的附加套件)：提供執行批次查詢的查詢服務存取權 [!DNL Data Distiller].

## 權益 {#entitlements}

下表根據封裝方式概述主要查詢服務權益：

| 查詢服務權益 | 與平台式應用程式封裝 | 已封裝 [!DNL Data Distiller] |
|---|---|---|
| 支援的查詢模式 | 僅限特定查詢 | 批次查詢 |
| 支援的使用案例 | <ul><li>探索&#x200B;</li><li>資料探索&#x200B;</li><li>資料驗證</li><li>實驗</li></ul> | <ul><li>清潔</li><li>塑形</li><li>操控</li><li>充實</li></ul> |
| 支援的語意 | <ul><li>選取查詢</li></ul> | <ul><li>CTAS和ITAS查詢</li></ul> |
| 最長執行時間 | 10 分鐘 | 24 小時 |
| 授權量度 | **查詢使用者並行**： <ul><li>1位同時使用者(Real-Time CDP、Adobe Journey Optimizer)&#x200B;</li><li>5位同時使用者(Customer Journey Analytics&#x200B;)</li></ul> **查詢並行**： <ul><li>1個並行執行查詢(所有應用程式&#x200B;)</li></ul> **其他Ad Hoc Query使用者套件附加元件** 可購買以增加客戶的授權特定查詢權益。 <ul><li>每包+5個額外的同時使用者</li><li>每包+1個額外的並行執行查詢</li></ul> | **計算時數**： <ul><li>變數（根據客戶的應用程式權益設定範圍）</li></ul> **計算時數** 是測量執行批次查詢時，查詢服務引擎讀取、處理資料以及將資料寫入資料湖所花費的時間。 |
| 加速查詢和報告使用 | 無 | 是 — 並行加速查詢可讓您從加速存放區讀取資料，並在您的儀表板中顯示。 也提供在加速存放區中儲存報告模型和資料集的專用權益。 |
| 資料湖儲存容量 | 您的總儲存許可權取決於您的平台應用程式授權。 例如，Real-Time CDP、AJO、CJA等。 | 是 — 提供額外的儲存權益，好讓您的資料Distiller使用案例原始和衍生資料集在七天資料到期日之後繼續儲存。<br>您的資料湖儲存容量是以TB為單位，取決於您購買的計算時數數量。 請檢視產品說明以取得更多詳細資料。 |
| 資料匯出允許 | 您的總匯出權益取決於您的平台式應用程式授權。 例如，Real-Time CDP、AJO、CJA等。 | 是 — 提供其他匯出權益，以允許匯出使用Data Distiller建立的衍生資料集。<br>您每年的資料匯出容量是以TB為單位，並且取決於您購買的計算時數數量。 如需更多詳細資訊，請檢視產品說明。 |
| 查詢執行介面 | <ul><li>查詢服務UI</li><li>協力廠商使用者端UI</li><li>[!DNL PostgresSQL] 使用者端UI</li></ul> | <ul><li>查詢服務UI </li><li>協力廠商使用者端UI</li><li>[!DNL PostgresSQL] 使用者端UI</li><li>REST API</li></ul> |
| 查詢結果傳回，透過 | 使用者端UI | 衍生資料集儲存在Data Lake中 |
| 結果限制 | <ul><li>查詢服務UI - 100列</li><li>協力廠商使用者端 — 50,000</li><li>[!DNL PostgresSQL] 使用者端 — 50,000</li></ul> | <ul><li>查詢服務UI — 輸出列數可以 [已使用UI設定進行設定](./ui/user-guide.md#result-count) 到50到500列。</li><li>協力廠商使用者端（列數沒有上限）</li><li>[!DNL PostgresSQL] 使用者端（列數沒有上限）</li><li>REST API （列數沒有上限）</li></ul> |
| 讀取資料集容量 | 是 | 是 |
| 寫入資料集容量 | 無 | 是 |
| 排程容量 | 無 | 是 |
| 監控容量 | 是 | 是 |
| 查詢警示設定容量 | 無 | 是 |

{style="table-layout:auto"}

## 存取控制 {#access-control}

Experience Platform的存取控制會透過 [Adobe Admin Console](https://adminconsole.adobe.com/) 產品設定檔將使用者與許可權和沙箱連結在一起。 請參閱 [存取控制總覽](../access-control/home.md) 以取得詳細資訊。

為了使用查詢服務， [!DNL Manage Queries] 必須在Admin Console中啟用許可權。 此許可權可讓使用者執行臨時和批次查詢。 請求存取產品設定檔的詳細說明 [!DNL Manage Queries] 已在中概述許可權 [管理產品設定檔的許可權](../access-control/ui/permissions.md) 和 [管理產品設定檔的使用者](../access-control/ui/users.md) 檔案。

購買後 [!DNL Data Distiller] 附加元件， [!DNL Write Dataset] 必須授與許可權。 此許可權允許 [!DNL Data Distiller] 執行批次查詢的使用者。

下表概述 [!DNL Manage Queries] 許可權：

| 權限 | 函數 |
|---|---|
| [!DNL Manage Queries] （沒有寫入資料許可權） | 提供執行特定查詢的存取權 |
| [!DNL Manage Queries] （具有寫入資料許可權） | 提供執行批次查詢的存取權 |

{style="table-layout:auto"}

## 沙箱支援 {#sandbox-support}

沙箱是單一Experience Platform執行個體中的虛擬分割區。 每個Platform執行個體支援多個生產和非生產沙箱，每個沙箱都維護自己的Platform資源庫。 非生產沙箱可讓您測試功能、執行實驗並進行自訂設定，而不會影響您的生產沙箱。 如需沙箱的詳細資訊，請參閱 [沙箱總覽](../sandboxes/home.md). 所有查詢服務許可權會在所有沙箱之間共用。

## 後續步驟

閱讀本檔案後，您應該能更清楚瞭解查詢服務中可用的不同封裝型別和查詢執行功能。 若要進一步瞭解查詢服務，例如知名的業界使用案例，請閱讀 [使用案例檔案](./use-cases/abandoned-browse.md). 如需一般資訊，請瀏覽 [查詢服務總覽](./home.md).
