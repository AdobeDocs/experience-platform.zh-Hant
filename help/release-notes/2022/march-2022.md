---
title: Adobe Experience 平台發行說明
description: Adobe Experience Platform的最新發行說明。
source-git-commit: 9117fffc58786f05e8741d9695ddb551344b6cc7
workflow-type: tm+mt
source-wordcount: '652'
ht-degree: 7%

---

# Adobe Experience Platform 發行說明

**發行日期：2022 年 3 月 30 日**

Adobe Experience Platform的新功能：

- [審核日誌](#audit-logs)

Adobe Experience Platform 現有功能更新：

- [警報](#alerts)
- [體驗資料模型(XDM)](#xdm)
- [來源](#sources)

## 審核日誌 {#audit-logs}

Experience Platform允許您審計用戶活動中的各種服務和功能。 審計日誌提供了有關誰執行了什麼和何時執行的資訊。

**新功能**

| 功能 | 說明 |
| --- | --- |
| 資料集、架構、類、欄位組、資料類型、沙盒、目標、段、合併策略、計算屬性、產品配置檔案和帳戶的審核日誌(Adobe) | 這些資源由審計日誌記錄。 如果啟用該功能，則在活動發生時自動收集審計日誌。 您不需要手動啟用日誌收集。 |
| 導出審核日誌 | 審核日誌可以作為 `CSV` 或 `JSON` 的子菜單。 生成的檔案將直接保存到您的電腦。 |

{style=&quot;table-layout:auto&quot;}

有關平台中審核日誌的詳細資訊，請參閱 [審核日誌概述](../../landing/governance-privacy-security/audit-logs/overview.md)。

## 警報 {#alerts}

Experience Platform允許您訂閱各種平台活動的基於事件的警報。 您可以通過 [!UICONTROL 警報] 頁籤，並可以選擇在UI本身或通過電子郵件通知接收警報消息。

**已更新功能**

| 功能 | 說明 |
| --- | --- |
| 新警報規則 | 現在，兩個新警報規則可用於與資料接收相關的源。 請參閱 [警報規則](../../observability/alerts/rules.md) 的子菜單。 |

{style=&quot;table-layout:auto&quot;&quot;

有關平台中警報的詳細資訊，請參閱 [警報概述](../../observability/alerts/overview.md)。

## 體驗資料模型(XDM) {#xdm}

體驗資料模型(XDM)是一種開源規範，它為傳入Adobe Experience Platform的資料提供了通用的結構和定義（架構）。 通過遵守XDM標準，所有客戶體驗資料都可以納入到共同的表示形式中，以更快、更整合的方式提供見解。 您可以從客戶操作中獲得有價值的見解，通過細分市場定義客戶受眾，並將客戶屬性用於個性化目的。

**已更新功能**

| 功能 | 說明 |
| --- | --- |
| 添加或刪除架構的單個標準欄位 | 現在，通過架構編輯器UI，您可以將標準欄位組的部分添加到您的架構中，從而為您選擇包括的欄位提供了更大的靈活性，而無需從頭構建自定義資源。<br><br>現在，您還可以直接在架構結構中定義即席自定義域，並將它們分配給新的或現有的自定義域組，而無需事先建立或編輯域組。<br><br>請參閱上的指南 [在UI中建立和編輯架構](../../xdm/ui/resources/schemas.md) 的子菜單。 |

{style=&quot;table-layout:auto&quot;&quot;

有關平台中XDM的詳細資訊，請參見 [XDM系統概述](../../xdm/home.md)。

## 來源 {#sources}

Adobe Experience Platform可以從外部源接收資料，同時允許您使用平台服務來構建、標籤和增強資料。 您可以從多種來源(如Adobe應用程式、基於雲的儲存、第三方軟體和您的CRM系統)接收資料。

Experience Platform提供REST風格的API和互動式UI，讓您能夠輕鬆地為各種資料提供程式設定源連接。 通過這些源連接，您可以驗證並連接到外部儲存系統和CRM服務，設定接收運行時間，並管理資料接收吞吐量。

**已更新功能**

| 功能 | 說明 |
| --- | --- |
| 現在可用於B2B的新源 | 現在，您可以將平台上所有可用的源用於B2B使用案例。 查看 [源目錄](../../sources/home.md) 的子菜單。 |
| 全面提供新 [!DNL Oracle Eloqua] 源 | 您現在可以使用 [!DNL Oracle Eloqua] 源，以無縫地從 [!DNL Oracle Eloqua] 實例（帳戶、市場活動、聯繫人）到平台。 請參閱 [建立 [!DNL Oracle Eloqua] 源連接](../../sources/connectors/oracle-eloqua.md) 的子菜單。 |
| API增強功能 [!DNL Data Landing Zone] | 的 [!DNL Data Landing Zone] 現在，使用 [!DNL Flow Service] API。 請參閱 [建立 [!DNL Data Landing Zone] 源連接](../../sources/tutorials/api/create/cloud-storage/data-landing-zone.md) 的子菜單。 |

{style=&quot;table-layout:auto&quot;&quot;

要瞭解有關源的詳細資訊，請參閱 [源概述](../../sources/home.md)。
