---
title: Adobe Experience Platform發行說明2022年3月
description: 2022年3月為Adobe Experience Platform發佈的說明。
exl-id: 0d499aa6-e25d-4d34-ad32-5e4ab361cba1
source-git-commit: 34e0381d40f884cd92157d08385d889b1739845f
workflow-type: tm+mt
source-wordcount: '1176'
ht-degree: 8%

---

# Adobe Experience Platform 發行說明

**發行日期：2022 年 3 月 30 日**

Adobe Experience Platform的新功能：

- [稽核記錄](#audit-logs)
- [Real-Time CDPB2B版相關帳戶](#related-accounts)

Adobe Experience Platform 現有功能更新：

- [警報](#alerts)
- [[!DNL Dashboards]](#dashboards)
- [資料收集](#data-collection)
- [[!DNL Query Service]](#query-service)
- [來源](#sources)

## 稽核記錄 {#audit-logs}

Experience Platform允許您審計用戶活動中的各種服務和功能。 審計日誌提供了有關誰執行了什麼和何時執行的資訊。

**新功能**

| 功能 | 說明 |
| --- | --- |
| 資料集、架構、類、欄位組、資料類型、沙盒、目標、段、合併策略、計算屬性、產品配置檔案和帳戶的審核日誌(Adobe) | 這些資源由審計日誌記錄。 如果啟用該功能，則在活動發生時自動收集審計日誌。 您無需手動啟用記錄收集。 |
| 導出審核日誌 | 審核日誌可以作為 `CSV` 或 `JSON` 的子菜單。 生成的檔案將直接保存到您的電腦。 |

{style="table-layout:auto"}

有關平台中審核日誌的詳細資訊，請參閱 [審核日誌概述](../../landing/governance-privacy-security/audit-logs/overview.md)。

## Real-Time CDPB2B版相關帳戶 {#related-accounts}

>[!NOTE]
>
>相關客戶功能僅適用於Real-Time CDPB2B版的客戶。

B2B企業通常將客戶資訊儲存在多個系統中，每個系統都只包含同一真實業務實體的部分甚至衝突資料。 這就帶來了一個巨大的挑戰，即要準確地瞭解客戶的情況，從而降低其B2B營銷和銷售工作的效率和效率。 隨著相關賬戶的發佈， [!DNL Real-Time CDP B2B] 現在顯示與您正在瀏覽的帳戶類似的帳戶清單。 您可以將相關帳戶包括在段定義中，以擴大範圍或在段中應用更寬的標準。

閱讀以下文檔頁中有關該功能的詳細資訊：

- [Real-Time CDPB2B版相關帳戶概述](../../rtcdp/b2b-ai-ml-services/related-accounts.md)
- [「帳戶配置檔案UI」指南中的「相關帳戶」頁籤](../../rtcdp/accounts/account-profile-ui-guide.md#related-accounts-tab)
- [如何在段定義中使用相關帳戶](../../rtcdp/segmentation/b2b.md#related-accounts)

要瞭解有關Real-Time CDPB2B版的詳細資訊，請參閱 [概述](../../rtcdp/overview.md)。

## 警報 {#alerts}

Experience Platform允許您訂閱各種平台活動的基於事件的警報。 您可以通過 [!UICONTROL 警報] 頁籤，並可以選擇在UI本身或通過電子郵件通知接收警報消息。

**已更新功能**

| 功能 | 說明 |
| --- | --- |
| 新警報規則 | 現在，兩個新警報規則可用於與資料接收相關的源。 請參閱 [警報規則](../../observability/alerts/rules.md) 的子菜單。 |

{style="table-layout:auto"}

有關平台中警報的詳細資訊，請參閱 [警報概述](../../observability/alerts/overview.md)。

## 儀表板 {#dashboards}

Adobe Experience Platform提供 [!DNL dashboards] 您可以通過查看有關組織資料的重要資訊（在每日快照中捕獲）。

### 配置檔案儀表板

「配置式」控制面板顯示您的組織在「配置式儲存」Experience Platform中擁有的屬性（記錄）資料的快照。

**已更新功能**

| 功能 | 說明 |
| --- | --- |
| 未分段的配置檔案構件 | 該構件提供未附加到任何段的所有配置檔案的總數。 生成的數字在上次快照時準確無誤，表示整個組織中配置檔案激活的機會。 查看 [配置檔案標準小部件文檔](../../dashboards/guides/profiles.md#standard-widgets) 的子菜單。 |
| 未分段的配置檔案趨勢構件 | 此 Widget 會提供折線圖，說明在特定時段內未附加到任何區段的所有設定檔數量。該趨勢可以在30天、90天和12個月期間進行可視化。 查看 [配置檔案標準小部件文檔](../../dashboards/guides/profiles.md#standard-widgets) 的子菜單。 |
| 按身份構件分段的配置檔案 | 此 Widget 會依照其唯一識別碼來分類無區段設定檔的總數。資料以條形圖顯示。 查看 [配置檔案標準小部件文檔](../../dashboards/guides/profiles.md#standard-widgets) 的子菜單。 |
| 單個身份配置檔案小部件 | 此小部件提供組織的配置檔案的計數，這些配置檔案只具有一種類型的ID類型，可建立其標識，即電子郵件或ECID。 查看 [配置檔案標準小部件文檔](../../dashboards/guides/profiles.md#standard-widgets) 的子菜單。 |

{style="table-layout:auto"}

有關配置式儀表板的詳細資訊，請參閱 [配置檔案儀表板概述](../../dashboards/guides/profiles.md)。

### 目標儀表板

「目標」控制面板顯示您的組織在Experience Platform中啟用的目標的快照。

**已更新功能**

| 功能 | 說明 |
| --- | --- |
| 目標計數小部件 | 該小部件提供了可用終結點的總數，在該總數中，可在系統內激活和傳遞受眾。 此數字包括使用中和非使用中的目的地。查看 [目標標準構件文檔](../../dashboards/guides/destinations.md#standard-widgets) 的子菜單。 |

{style="table-layout:auto"}

有關平台中目標儀表板的詳細資訊，請參閱 [目標儀表板概述](../../dashboards/guides/destinations.md)。

## 資料收集 {#data-collection}

平台提供一套技術，使您能夠收集客戶端客戶體驗資料並將其發送到Adobe Experience Platform邊緣網路，在該網路中，資料可以得到豐富、轉換並分發到Adobe或非Adobe目的地。

**新功能**

| 功能 | 說明 |
| --- | --- |
| 全局資料流設定 | 現在，在配置資料流時可以配置幾個新的全局設定：地理位置、第一方IDcookie和第三方ID同步。 請參閱 [配置資料流](../../edge/datastreams/overview.md#create) 的子菜單。 |
| [邊緣網路伺服器 API](../../server-api/overview.md) | 伺服器API使客戶能夠使用新的經過驗證的端點與Experience Platform邊緣網路進行交互，以支援各種資料收集，個性化，廣告和營銷使用案例。 |

有關平台中資料收集的詳細資訊，請參閱 [資料收集概述](../../collection/home.md)。

## 查詢服務 {#query-service}

[!DNL Query Service] 允許您使用標準SQL查詢Adobe Experience Platform的資料 [!DNL Data Lake]。 您可以加入來自 [!DNL Data Lake] 並將查詢結果捕獲為新資料集，用於報告、Data Science Workspace或用於接收到即時客戶配置檔案。

**已更新功能**

| 功能 | 說明 |
| --- | --- |
| `table_exists` | 新功能命令用於確認系統中當前是否存在表。 該命令返回一個布爾值： `true` 的 **是** 存在 `false` 如果表 **不** 存在。 查看 [SQL語法文檔](../../query-service/sql/syntax.md) 的子菜單。 |

{style="table-layout:auto"}

有關可用功能的詳細資訊，請參閱 [查詢服務概述](../../query-service/home.md)。

## 來源 {#sources}

Adobe Experience Platform可以從外部源接收資料，同時允許您使用平台服務來構建、標籤和增強資料。 您可以從多種來源(如Adobe應用程式、基於雲的儲存、第三方軟體和您的CRM系統)接收資料。

Experience Platform提供REST風格的API和互動式UI，讓您能夠輕鬆地為各種資料提供程式設定源連接。 通過這些源連接，您可以驗證並連接到外部儲存系統和CRM服務，設定接收運行時間，並在整個過程中管理資料接收。

**已更新功能**

| 功能 | 說明 |
| --- | --- |
| 現在可用於B2B的新源 | 現在，您可以將平台上所有可用的源用於B2B使用案例。 查看 [源目錄](../../sources/home.md) 的子菜單。 |
| 全面提供新 [!DNL Oracle Eloqua] 源 | 您現在可以使用 [!DNL Oracle Eloqua] 源，以無縫地從 [!DNL Oracle Eloqua] 實例（帳戶、市場活動、聯繫人）到平台。 請參閱 [建立 [!DNL Oracle Eloqua] 源連接](../../sources/connectors/marketing-automation/oracle-eloqua.md) 的子菜單。 |
| API增強功能 [!DNL Data Landing Zone] | 的 [!DNL Data Landing Zone] 現在，使用 [!DNL Flow Service] API。 請參閱 [建立 [!DNL Data Landing Zone] 源連接](../../sources/tutorials/api/create/cloud-storage/data-landing-zone.md) 的子菜單。 |

{style="table-layout:auto"}

要瞭解有關源的詳細資訊，請參閱 [源概述](../../sources/home.md)。
