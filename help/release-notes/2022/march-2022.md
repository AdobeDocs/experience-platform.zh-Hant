---
title: Adobe Experience Platform 發行說明 (2022 年 3 月版)
description: Adobe Experience Platform 2022 年 3 月版發行說明。
exl-id: 0d499aa6-e25d-4d34-ad32-5e4ab361cba1
source-git-commit: 7f3459f678c74ead1d733304702309522dd0018b
workflow-type: tm+mt
source-wordcount: '1183'
ht-degree: 20%

---

# Adobe Experience Platform 發行說明

**發行日期： 2022年3月30日**

Adobe Experience Platform 的新功能：

- [稽核記錄](#audit-logs)
- [Real-Time CDP B2B edition中的相關帳戶](#related-accounts)

Adobe Experience Platform 現有功能的更新：

- [警示](#alerts)
- [[!DNL Dashboards]](#dashboards)
- [資料彙集](#data-collection)
- [[!DNL Query Service]](#query-service)
- [來源](#sources)

## 稽核記錄 {#audit-logs}

Experience Platform可讓您稽核各種服務和功能的使用者活動。 稽核記錄會提供有關何時何地執行哪些操作的資訊。

**新功能**

| 功能 | 說明 |
| --- | --- |
| 資料集、結構、類別、欄位群組、資料型別、沙箱、目的地、區段、合併原則、計算屬性、產品設定檔和帳戶的稽核記錄(Adobe) | 這些是稽核記錄檔所記錄的資源。 如果啟用此功能，將會在活動發生時自動收集稽核記錄。 您不需要手動啟用記錄收集。 |
| 匯出稽核記錄 | 稽核記錄檔可以下載為`CSV`或`JSON`檔案。 產生的檔案會直接儲存到您的電腦中。 |

{style="table-layout:auto"}

如需Experience Platform中稽核記錄的詳細資訊，請參閱[稽核記錄概觀](../../landing/governance-privacy-security/audit-logs/overview.md)。

## Real-Time CDP B2B edition中的相關帳戶 {#related-accounts}

>[!NOTE]
>
>「相關帳戶」功能僅適用於Real-Time CDP B2B edition的客戶。

B2B企業通常將其客戶資訊儲存在多個系統中，每個系統僅包含相同真實世界商業實體的部分或甚至衝突資料。 這帶來了巨大的挑戰，難以準確瞭解客戶，因此會降低B2B行銷和銷售工作的效率和成效。 隨著相關帳戶的發行，[!DNL Real-Time CDP B2B]現在會顯示與您瀏覽的帳戶類似的帳戶清單。 您可以在區段定義中加入相關科目，以擴大您的業務範圍，或在區段中套用更廣的標準。

請在下列檔案頁面中進一步瞭解此功能：

- [Real-Time CDP B2B edition中的相關帳戶概觀](../../rtcdp/b2b-ai-ml-services/related-accounts.md)
- [帳戶設定檔UI指南中的相關帳戶標籤](../../rtcdp/accounts/account-profile-ui-guide.md#related-accounts-tab)
- [如何在區段定義中使用相關科目](../../rtcdp/segmentation/b2b.md#related-accounts)

若要進一步瞭解Real-Time CDP B2B edition，請參閱[總覽](../../rtcdp/overview.md)。

## 警報 {#alerts}

Experience Platform 可讓您訂閱各種 Experience Platform 活動的事件型警報。您可以透過 Experience Platform 使用者介面中的「[!UICONTROL 警報]」標籤訂閱不同的警報規則，而且可以選擇在使用者介面本身內或透過電子郵件通知接收警報訊息。

**更新的功能**

| 功能 | 說明 |
| --- | --- |
| 新警報規則 | 與資料擷取相關的來源現在提供兩種新警報規則。 如需更新的警示型別清單，請參閱[警示規則](../../observability/alerts/rules.md)的概觀。 |

{style="table-layout:auto"}

如需Experience Platform中警示的詳細資訊，請參閱[警示概觀](../../observability/alerts/overview.md)。

## 儀表板 {#dashboards}

Adobe Experience Platform提供多個[!DNL dashboards]，您可以透過它檢視有關您組織資料的重要資訊，如每日快照期間所擷取。

### 設定檔儀表板

設定檔儀表板會顯示貴組織在Experience Platform的設定檔存放區中擁有的屬性（記錄）資料快照。

**更新的功能**

| 功能 | 說明 |
| --- | --- |
| 未分段的設定檔Widget | Widget提供未附加至任何區段的所有設定檔總數。 產生的數字在最後一個快照集之前是準確的，代表您組織內設定檔啟用的機會。 如需詳細資訊，請參閱[設定檔標準Widget檔案](../../dashboards/guides/profiles.md#standard-widgets)。 |
| 未分段的設定檔趨勢Widget | 這個小工具會提供折線圖，描述在特定時段內未附加到任何區段的輪廓數量。趨勢可以在30天、90天和12個月的期間中進行視覺化。 如需詳細資訊，請參閱[設定檔標準Widget檔案](../../dashboards/guides/profiles.md#standard-widgets)。 |
| 依身分Widget區分的未分段設定檔 | 此Widget會依唯一識別碼將未分段的設定檔總數分類。 資料會以長條圖顯示。 如需詳細資訊，請參閱[設定檔標準Widget檔案](../../dashboards/guides/profiles.md#standard-widgets)。 |
| 單一身分設定檔Widget | 此Widget提供貴組織只有一種ID型別（電子郵件或ECID）可建立其身分的設定檔計數。 如需詳細資訊，請參閱[設定檔標準Widget檔案](../../dashboards/guides/profiles.md#standard-widgets)。 |

{style="table-layout:auto"}

如需設定檔儀表板的詳細資訊，請參閱[設定檔儀表板概觀](../../dashboards/guides/profiles.md)。

### 目的地儀表板

目的地儀表板會顯示貴組織在 Experience Platform 中啟用的目的地的快照。

**更新的功能**

| 功能 | 說明 |
| --- | --- |
| 目的地計數Widget | Widget提供可在系統中啟用及傳遞對象的可用端點總數。 此數字包含使用中及非使用中的目的地。 如需詳細資訊，請參閱[目的地標準Widget檔案](../../dashboards/guides/destinations.md#standard-widgets)。 |

{style="table-layout:auto"}

如需Experience Platform中目標儀表板的詳細資訊，請參閱[目標儀表板總覽](../../dashboards/guides/destinations.md)。

## 資料彙集 {#data-collection}

Experience Platform提供了一套技術，可讓您收集使用者端客戶體驗資料並將資料傳送至Adobe Experience Platform Edge Network，在那裡可以擴充和轉換資料，並將其分發至Adobe或非Adobe目的地。

**新功能**

| 功能 | 說明 |
| --- | --- |
| 全域資料流設定 | 您現在可在設定資料流時設定數個新的全域設定：地理位置、第一方ID Cookie和協力廠商ID同步。 如需詳細資訊，請參閱資料串流UI指南中[設定資料串流](../../datastreams/overview.md#create)的相關章節。 |
| [Edge Network API](https://developer.adobe.com/data-collection-apis/docs/getting-started/) | Edge Network API可讓客戶使用新的、經過驗證的端點與Experience Platform Edge Network互動，以支援各種資料收集、個人化、廣告和行銷使用案例。 |

如需Experience Platform中資料收集的詳細資訊，請參閱[資料收集概觀](../../collection/home.md)。

## 查詢服務 {#query-service}

[!DNL Query Service]可讓您使用標準SQL在Adobe Experience Platform [!DNL Data Lake]中查詢資料。 您可以加入 [!DNL Data Lake] 中的任何資料集，並將查詢結果擷取為新資料集，以用於報告、資料科學工作區，或攝取至即時客戶設定檔中。

**更新的功能**

| 功能 | 說明 |
| --- | --- |
| `table_exists` | 新特徵指令用於確認表格目前是否存在於系統中。 如果資料表&#x200B;**確實**&#x200B;存在，命令會傳回布林值： `true`，如果資料表&#x200B;**確實**&#x200B;存在，則傳回`false`。 如需詳細資訊，請參閱[SQL語法檔案](../../query-service/sql/syntax.md)。 |

{style="table-layout:auto"}

如需可用功能的詳細資訊，請參閱[查詢服務總覽](../../query-service/home.md)。

## 來源 {#sources}

Adobe Experience Platform可內嵌來自外部來源的資料，同時允許您使用Experience Platform服務來建構、加標籤及增強這些資料。 您可以從各種來源擷取資料，例如 Adob&#x200B;&#x200B;e 應用程式、雲端型儲存空間、協力廠商軟體和 CRM 系統。

Experience Platform 可提供 RESTful API 和互動式 UI，可讓您輕鬆為各種資料提供者設定來源連線。這些來源連線可讓您驗證並連線至外部儲存系統和CRM服務、設定擷取執行的時間，以及管理整個過程中的資料擷取。

**更新的功能**

| 功能 | 說明 |
| --- | --- |
| 現在有新的來源可用於B2B使用 | 您現在可以在Experience Platform上針對B2B使用案例使用所有可用的來源。 如需可用來源的完整清單，請參閱[來源目錄](../../sources/home.md)。 |
| 新[!DNL Oracle Eloqua]來源的一般可用性 | 您現在可以使用[!DNL Oracle Eloqua]來源，順暢地從[!DNL Oracle Eloqua]執行個體（帳戶、行銷活動、連絡人）擷取資料至Experience Platform。 如需詳細資訊，請參閱有關[建立 [!DNL Oracle Eloqua] 來源連線](../../sources/connectors/marketing-automation/oracle-eloqua.md)的檔案。 |
| [!DNL Data Landing Zone]的API增強功能 | 使用[!DNL Flow Service] API時，[!DNL Data Landing Zone]來源現在支援自動偵測檔案屬性。 如需詳細資訊，請參閱有關[建立 [!DNL Data Landing Zone] 來源連線](../../sources/tutorials/api/create/cloud-storage/data-landing-zone.md)的檔案。 |

{style="table-layout:auto"}

若要深入瞭解來源，請參閱[來源概觀](../../sources/home.md)。
