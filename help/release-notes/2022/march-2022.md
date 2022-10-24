---
title: Adobe Experience Platform發行說明2022年3月
description: 2022年3月Adobe Experience Platform發行說明。
exl-id: 0d499aa6-e25d-4d34-ad32-5e4ab361cba1
source-git-commit: 14e3eff3ea2469023823a35ee1112568f5b5f4f7
workflow-type: tm+mt
source-wordcount: '1194'
ht-degree: 5%

---

# Adobe Experience Platform 發行說明

**發行日期：2022 年 3 月 30 日**

Adobe Experience Platform的新功能：

- [稽核記錄](#audit-logs)
- [Real-Time CDP B2B版中的相關帳戶](#related-accounts)

Adobe Experience Platform 現有功能更新：

- [警報](#alerts)
- [[!DNL Dashboards]](#dashboards)
- [資料收集](#data-collection)
- [[!DNL Query Service]](#query-service)
- [來源](#sources)

## 稽核記錄 {#audit-logs}

Experience Platform可讓您稽核各種服務和功能的使用者活動。 稽核記錄會提供關於執行動作的人員以及執行時間的資訊。

**新功能**

| 功能 | 說明 |
| --- | --- |
| 資料集、結構、類別、欄位群組、資料類型、沙箱、目的地、區段、合併原則、計算屬性、產品設定檔和帳戶(Adobe)的稽核記錄 | 這些是由稽核記錄所記錄的資源。 如果啟用功能，稽核記錄會在活動發生時自動收集。 您不需要手動啟用記錄檔收集。 |
| 導出審核日誌 | 稽核記錄可下載為 `CSV` 或 `JSON` 檔案。 產生的檔案會直接儲存至您的電腦。 |

{style=&quot;table-layout:auto&quot;}

如需Platform中稽核記錄的詳細資訊，請參閱 [稽核記錄概述](../../landing/governance-privacy-security/audit-logs/overview.md).

## Real-Time CDP B2B版中的相關帳戶 {#related-accounts}

>[!NOTE]
>
>「相關帳戶」功能僅適用於Real-Time CDP B2B版的客戶。

B2B企業通常將客戶資訊儲存在多個系統中，每個系統都只包含同一實際業務實體的部分或甚至衝突資料。 這對於準確了解客戶構成了巨大挑戰，因此降低了B2B行銷和銷售工作的效率和效益。 隨著相關帳戶的發行， [!DNL Real-Time CDP B2B] 現在會顯示與您瀏覽之帳戶類似的帳戶清單。 您可以在區段定義中加入相關帳戶，以擴大觸及範圍，或在區段中套用更廣的條件。

請參閱下列檔案頁面，以深入了解此功能：

- [Real-Time CDP B2B版中的相關帳戶概述](../../rtcdp/b2b-ai-ml-services/related-accounts.md)
- [帳戶設定檔UI指南中的相關帳戶標籤](../../rtcdp/accounts/account-profile-ui-guide.md#related-accounts-tab)
- [如何在區段定義中使用相關帳戶](../../rtcdp/segmentation/b2b.md#related-accounts)

若要進一步了解Real-Time CDP B2B版，請參閱 [概述](../../rtcdp/overview.md).

## 警報 {#alerts}

Experience Platform可讓您訂閱各種平台活動的事件型警報。 您可以透過 [!UICONTROL 警報] 標籤，並可選擇在UI本身或透過電子郵件通知接收警報訊息。

**更新功能**

| 功能 | 說明 |
| --- | --- |
| 新警報規則 | 現在有兩個新的警報規則可用於資料擷取的相關來源。 請參閱 [警報規則](../../observability/alerts/rules.md) 以取得更新的警報類型清單。 |

{style=&quot;table-layout:auto&quot;}

如需Platform中警報的詳細資訊，請參閱 [警報概觀](../../observability/alerts/overview.md).

## 儀表板 {#dashboards}

Adobe Experience Platform提供多個 [!DNL dashboards] 通過它可以查看有關組織資料的重要資訊，如每日快照時捕獲的。

### 設定檔控制面板

「設定檔」控制面板會顯示您的組織在「設定檔存放區」內Experience Platform的屬性（記錄）資料快照。

**更新功能**

| 功能 | 說明 |
| --- | --- |
| 未細分的設定檔Widget | 介面工具集提供未附加至任何區段的所有設定檔總數。 生成的數字與上次快照時的資料一致，並代表整個組織的配置檔案激活機會。 請參閱 [profiles standard widget檔案](../../dashboards/guides/profiles.md#standard-widgets) 以取得更多資訊。 |
| 未分段的設定檔趨勢Widget | 此介面工具集提供線條圖圖示，說明指定時段內未附加至任何區段的設定檔數量。 趨勢可以在30天、90天和12個月期間內視覺化。 請參閱 [profiles standard widget檔案](../../dashboards/guides/profiles.md#standard-widgets) 以取得更多資訊。 |
| 依身分識別Widget的未分段設定檔 | 此介面工具集會依其唯一識別碼來分類未分段的設定檔總數。 資料以橫條圖視覺化。 請參閱 [profiles standard widget檔案](../../dashboards/guides/profiles.md#standard-widgets) 以取得更多資訊。 |
| 單一身分設定檔Widget | 此介面工具集可提供貴組織的設定檔計數，這些設定檔只有一種可建立其身分的ID類型，可能是電子郵件或ECID。 請參閱 [profiles standard widget檔案](../../dashboards/guides/profiles.md#standard-widgets) 以取得更多資訊。 |

{style=&quot;table-layout:auto&quot;}

如需設定檔控制面板的詳細資訊，請參閱 [設定檔控制面板概觀](../../dashboards/guides/profiles.md).

### 目的地控制面板

「目標」控制面板會顯示貴組織已在Experience Platform中啟用的目標的快照。

**更新功能**

| 功能 | 說明 |
| --- | --- |
| 目的地計數介面工具集 | 介面工具集提供可在系統中啟用和傳遞受眾的可用端點總數。 此數字包含使用中和非使用中目的地。 請參閱 [destinations standard widget檔案](../../dashboards/guides/destinations.md#standard-widgets) 以取得更多資訊。 |

{style=&quot;table-layout:auto&quot;}

如需Platform中「目標」控制面板的詳細資訊，請參閱 [目的地控制面板概觀](../../dashboards/guides/destinations.md).

## 資料收集 {#data-collection}

Platform提供一套技術，可讓您收集用戶端客戶體驗資料，並傳送至Adobe Experience Platform Edge Network，以便在中加以擴充、轉換及分送至Adobe或非Adobe目的地。

**新功能**

| 功能 | 說明 |
| --- | --- |
| 全域資料流設定 | 現在當您設定資料流時，可以設定數個新的全域設定：地理位置、第一方ID Cookie和第三方ID同步。 請參閱 [設定資料流](../../edge/datastreams/overview.md#create) 資料流UI指南中，以取得詳細資訊。 |
| [邊緣網路伺服器 API](../../server-api/overview.md) | 伺服器API可讓客戶使用新的已驗證端點與Experience Platform邊緣網路互動，以支援各種資料收集、個人化、廣告和行銷使用案例。 |

如需Platform中資料收集的詳細資訊，請參閱 [資料匯集概述](../../collection/home.md).

## 查詢服務 {#query-service}

[!DNL Query Service] 可讓您使用標準SQL在Adobe Experience Platform中查詢資料 [!DNL Data Lake]. 您可以從 [!DNL Data Lake] 並將查詢結果擷取為新資料集，以用於報表、Data Science Workspace或擷取至「即時客戶個人檔案」。

**更新功能**

| 功能 | 說明 |
| --- | --- |
| `table_exists` | 新功能命令用於確認系統中當前是否存在表。 命令返回一個布爾值： `true` 如果表格 **does** 存在，且 `false` 如果表格顯示 **not** 存在。 請參閱 [SQL語法文檔](../../query-service/sql/syntax.md) 以取得更多資訊。 |

{style=&quot;table-layout:auto&quot;}

有關可用功能的詳細資訊，請參閱 [查詢服務概述](../../query-service/home.md).

## 來源 {#sources}

Adobe Experience Platform可內嵌來自外部來源的資料，同時允許您使用Platform服務來建構、加標籤及增強該資料。 您可以內嵌來自各種來源的資料，例如Adobe應用程式、雲端儲存、協力廠商軟體和您的CRM系統。

Experience Platform提供RESTful API和互動式UI，讓您輕鬆為各種資料提供者設定來源連線。 這些源連接允許您驗證並連接到外部儲存系統和CRM服務、設定獲取運行的時間，以及在整個過程中管理資料獲取。

**更新功能**

| 功能 | 說明 |
| --- | --- |
| B2B使用現已提供新來源 | 現在，在B2B使用案例中，您可以使用Platform上所有可用的來源。 請參閱 [來源目錄](../../sources/home.md) 以取得可用來源的完整清單。 |
| 全面推出 [!DNL Oracle Eloqua] 來源 | 您現在可以使用 [!DNL Oracle Eloqua] 源無縫地從 [!DNL Oracle Eloqua] 例項（帳戶、行銷活動、連絡人）至Platform。 請參閱 [建立 [!DNL Oracle Eloqua] 源連接](../../sources/connectors/marketing-automation/oracle-eloqua.md) 以取得更多資訊。 |
| 適用於 [!DNL Data Landing Zone] | 此 [!DNL Data Landing Zone] 原始碼現在支援使用 [!DNL Flow Service] API。 請參閱 [建立 [!DNL Data Landing Zone] 源連接](../../sources/tutorials/api/create/cloud-storage/data-landing-zone.md) 以取得更多資訊。 |

{style=&quot;table-layout:auto&quot;}

若要進一步了解來源，請參閱 [來源概觀](../../sources/home.md).
