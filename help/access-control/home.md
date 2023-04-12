---
keywords: Experience Platform；首頁；熱門主題；存取控制；adobe admin console
solution: Experience Platform
title: 存取控制概覽
description: Adobe Experience Platform的存取控制可透過Adobe Admin Console提供。 此功能會運用Admin Console中的產品設定檔，將使用者與權限和沙箱連結。
exl-id: 591d59ad-2784-4ae4-a509-23649ce712c9
source-git-commit: 81f48de908b274d836f551bec5693de13c5edaf1
workflow-type: tm+mt
source-wordcount: '1540'
ht-degree: 3%

---

# 存取控制概覽

的存取控制 [!DNL Experience Platform] 是透過 [Adobe Admin Console](https://adminconsole.adobe.com). 此功能可運用以下產品設定檔： [!DNL Admin Console]，可將使用者與權限和沙箱連結。

## 存取控制階層與工作流程

為了配置 [!DNL Experience Platform]，則您必須擁有具有 [!DNL Experience Platform] 產品整合。 授予或撤回權限的最低角色為產品設定檔管理員。 可管理權限的其他管理員角色包括產品管理員（可管理產品內的所有設定檔）和系統管理員（無限制）。 請參閱Adobe Help Center上的文章： [管理角色](https://helpx.adobe.com/enterprise/using/admin-roles.html) 以取得更多資訊。

>[!NOTE]
>
>此後，本檔案中任何「管理員」的提及，都指產品設定檔管理員或更高版本（如上所述）。

取得和指派存取權限的高階工作流程摘要如下：

- 授權Adobe Experience Platform或使用Experience Platform的應用程式/應用程式服務後，會傳送電子郵件給授權期間指定的管理員。
- 管理員登入 [Adobe Admin Console](#adobe-admin-console) 選取 **Adobe Experience Platform** 從「概觀」頁面上的產品清單。
- 管理員可以檢視預設 [產品設定檔](#product-profiles) 或視需要建立新的客戶產品設定檔。
- 管理員可以編輯任何現有產品設定檔的權限和使用者。
- 建立或編輯產品設定檔時，管理員會使用 **[!UICONTROL 使用者]** 標籤，並授予這些使用者的權限(例如[!UICONTROL 讀取資料集]&quot;或&quot;[!UICONTROL 管理結構]&quot;)，透過存取 **[!UICONTROL 權限]** 標籤。 同樣地，管理員也可以使用相同的權限索引標籤，將存取權指派給沙箱。
- 當使用者登入 [!DNL Experience Platform] 使用者介面，其存取權 [!DNL Platform] 功能是由步驟2授予它們的權限所驅動。 例如，若使用者沒有[!UICONTROL 檢視資料集]「權限， **[!UICONTROL 資料集]** 該使用者將看不到側面功能表中的標籤。

有關如何在 [!DNL Experience Platform]，請參閱 [存取控制使用手冊](./ui/overview.md).

所有呼叫 [!DNL Experience Platform] API會通過權限驗證，如果在目前的使用者內容中找不到適當的權限，則會傳回錯誤。 根據授予目前使用者的權限，UI中的元素會隱藏或變更。

## Adobe Admin Console

Adobe Admin Console提供管理Adobe產品權益和組織存取權限的集中位置。 您可以透過主控台，授與各使用者群組存取權限 [!DNL Platform] 功能，例如「[!UICONTROL 管理資料集]&quot;, &quot;[!UICONTROL 檢視資料集]&quot;或&quot;[!UICONTROL 管理設定檔]」。

### 產品基本資料

在 [!DNL Admin Console]，權限會透過使用產品設定檔指派給使用者。 產品設定檔可讓您授予一或多個使用者的權限，也可包含使用者對透過產品設定檔指派給他們的沙箱範圍的存取。 可將使用者指派給屬於您組織的一或多個產品設定檔。

### 預設產品設定檔

[!DNL Experience Platform] 隨附兩個預先設定的預設產品設定檔。 下表概述每個預設設定檔中提供的內容，包括其所授與的存取沙箱，以及其在該沙箱範圍內所授予的權限。

| 產品描述檔 | 沙箱存取 | 權限 |
| --- | --- | --- |
| 預設生產全部訪問 | 生產 | 適用於 [!DNL Experience Platform]，但沙箱管理權限除外。 |
| 沙箱管理員 | 不適用 | 僅提供對沙箱管理權限的存取。 |

## 沙箱和權限

非生產沙箱是資料虛擬化的一種形式，可讓您將資料與其他沙箱隔離，且通常用於開發實驗、測試或測試。 產品設定檔的權限可授予設定檔的使用者存取權 [!DNL Platform] 沙箱環境中已授予其存取權的功能。 預設Experience Platform授權會授予您五個沙箱（一個生產，四個非生產）。 您最多可新增10個非生產沙箱，最多75個沙箱。 如需詳細資訊，請聯絡貴組織的管理員或Adobe銷售代表。

如需中沙箱的詳細資訊，請參閱 [!DNL Experience Platform]，請參閱 [沙箱概述](../sandboxes/home.md).

### 存取沙箱

沙箱的存取權是透過產品設定檔管理。 如需如何啟用產品設定檔之沙箱的存取權的詳細步驟，請參閱 [存取控制使用手冊](./ui/overview.md).

可授予使用者產品設定檔中一或多個沙箱的存取權。 如果兩個或多個產品設定檔中包含一個使用者，該使用者將可存取這些設定檔中包含的所有沙箱。

「沙箱管理」權限可讓使用者管理、檢視或重設沙箱。

### 權限 {#permissions}

產品設定檔中的權限標籤會顯示該設定檔作用中的沙箱和權限：

![權限 — 概觀](./images/permissions.png)

透過 [!DNL Admin Console] 會依類別排序，而有些權限會授予對數個低階功能的存取權。

下表概述 [!DNL Experience Platform] 在 [!DNL Admin Console]，以及特定 [!DNL Platform] 授予存取權的功能。 如需如何將權限新增至產品設定檔的詳細步驟，請參閱 [存取控制使用手冊](./ui/overview.md).

| 類別 | 權限 | 說明 |
| --- | --- | --- |
| [!DNL Alerts] | [!UICONTROL 查看警報歷史記錄] | 警報歷史記錄的唯讀存取。 |
| [!DNL Alerts] | [!UICONTROL 解決警報] | 存取讀取、編輯和刪除警報。 |
| [!DNL Alerts] | [!UICONTROL 檢視警報] | 警報的唯讀存取。 |
| [!DNL Alerts] | [!UICONTROL 管理警報] | 存取讀取、建立、編輯和刪除警報歷史記錄。 |
| [!DNL Data Hygiene] | [!UICONTROL 查看資料衛生] | 資料衛生的唯讀存取。 |
| [!DNL Data Hygiene] | [!UICONTROL 管理資料衛生] | 讀取、建立、編輯和刪除資料衛生的存取權。 |
| [!DNL Data Modeling] | [!UICONTROL 管理結構描述] | 存取讀取、建立、編輯和刪除結構和相關資源。 |
| [!DNL Data Modeling] | [!UICONTROL 檢視結構描述] | 對結構和相關資源的唯讀存取。 |
| [!DNL Data Modeling] | [!UICONTROL 管理關係] | 訪問讀取、建立、編輯和刪除架構關係。 |
| [!DNL Data Modeling] | [!UICONTROL 管理身分中繼資料] | 存取讀取、建立、編輯和刪除結構的身分中繼資料。 |
| [!DNL Data Management] | [!UICONTROL 管理資料集] | 存取讀取、建立、編輯和刪除資料集。 結構的唯讀存取。 |
| [!DNL Data Management] | [!UICONTROL 檢視資料集] | 資料集和結構的唯讀存取權。 |
| [!DNL Data Management] | [!UICONTROL 資料監控] | 監控資料集和資料流的唯讀存取權。 |
| [!DNL Profile Management] | [!UICONTROL 管理設定檔] | 存取讀取、建立、編輯和刪除用於客戶設定檔的資料集。 可用設定檔的唯讀存取權。 |
| [!DNL Profile Management] | [!UICONTROL 檢視設定檔] | 可用設定檔的唯讀存取權。 |
| [!DNL Profile Management] | [!UICONTROL 管理區段] | 存取讀取、建立、編輯和刪除區段。 |
| [!DNL Profile Management] | [!UICONTROL 檢視區段] | 可用區段的唯讀存取權。 |
| [!DNL Profile Management] | [!UICONTROL 管理合併策略] | 讀取、建立、編輯和刪除合併策略的訪問權限。 |
| [!DNL Profile Management] | [!UICONTROL 查看合併策略] | 對可用合併策略的只讀訪問。 |
| [!DNL Profile Management] | [!UICONTROL 匯出區段的受眾] | 能夠將評估的受眾區段匯出至資料集。 |
| [!DNL Profile Management] | [!UICONTROL 評估受眾的區段] | 可評估區段定義，為對象產生設定檔。 |
| [!DNL Identity Management] | [!UICONTROL 管理身分識別命名空間] | 存取讀取、建立、編輯和刪除身分識別命名空間。 |
| [!DNL Identity Management] | [!UICONTROL 檢視身分命名空間] | 身分識別命名空間的唯讀存取。 |
| [!DNL Identity Management] | [!UICONTROL 檢視身分圖] | 身分圖表的唯讀存取。 |
| [!DNL Sandbox Administration] | [!UICONTROL 管理沙箱] | 存取讀取、建立、編輯和刪除沙箱。 |
| [!DNL Sandbox Administration] | [!UICONTROL 檢視沙箱] | 屬於您組織的沙箱的唯讀存取權。 |
| [!DNL Sandbox Administration] | [!UICONTROL 重設沙箱] | 重設沙箱的功能。 |
| [!DNL Destinations] | [!UICONTROL 管理目的地] | 讀取、建立和刪除目標激活流和目標帳戶的訪問權限。 |
| [!DNL Destinations] | [!UICONTROL 檢視目的地] | 以唯讀方式存取 **[!UICONTROL 目錄]** 標籤和已驗證的目的地 **[!UICONTROL 瀏覽]** 標籤。 |
| [!DNL Destinations] | [!UICONTROL 啟動目的地] | 讓使用者能對現有目的地啟用區段。 在啟動工作流程中啟用對應步驟。 此權限需要 [!UICONTROL 檢視目的地] 或 [!UICONTROL 管理目的地] 授予將對目的地啟用資料的使用者。 |
| [!DNL Destinations] | [!UICONTROL 啟用區段而不對應] | 讓使用者能啟動區段至現有目的地，而不顯示 [對應步驟](../destinations/ui/activate-batch-profile-destinations.md#mapping). 使用者可以在啟用工作流程中新增和移除區段，但無法新增或移除已對應的屬性或身分。 此權限需要 [!UICONTROL 啟動目的地] 將啟用資料至目的地的使用者，可獲得此權限。 |
| [!DNL Destinations] | [!UICONTROL 管理和啟用資料集目的地] | 可讀取、建立、編輯和停用資料集匯出流程。 也能對已建立的作用中資料集啟用資料。 |
| [!DNL Destinations] | [!UICONTROL 目標編寫] | 可使用 [Adobe Experience Platform Destination SDK](../destinations/destination-sdk/overview.md). |
| [!DNL Data Ingestion] | [!UICONTROL 管理來源] | 讀取、建立、編輯和禁用源的訪問權。 |
| [!DNL Data Ingestion] | [!UICONTROL 查看源] | 對 **[!UICONTROL 目錄]** 標籤和已驗證的來源(在 **[!UICONTROL 瀏覽]** 標籤。 |
| [!DNL Data Ingestion] | [!DNL Manage Audience Share Connections] | 訪問建立、接受和拒絕合作夥伴握手以連接兩個組織並啟用 [!DNL Segment Match] 流量。 |
| [!DNL Data Ingestion] | [!DNL Manage Audience Share] | 讀取、建立、編輯和發佈的存取權 [!DNL Segment Match] 與作用中合作夥伴的摘要。 |
| [!DNL Data Science Workspace] | [!UICONTROL 管理Data Science Workspace] | 在中讀取、建立、編輯和刪除 [!DNL Data Science Workspace]. |
| 資料治理 | [!UICONTROL 套用資料使用量標籤] | 讀取、建立和刪除使用標籤的存取權。 |
| 資料治理 | [!UICONTROL 管理資料使用策略] | 存取讀取、建立、編輯和刪除資料使用原則。 |
| 資料治理 | [!UICONTROL 查看資料使用策略] | 屬於貴組織的資料使用原則的唯讀存取。 |
| 資料治理 | [!UICONTROL 查看用戶活動日誌] | 對記錄的檢視的唯讀存取 [稽核記錄](../landing/governance-privacy-security/audit-logs/overview.md) 平台活動。 |
| [!DNL Dashboards] | [!UICONTROL 查看許可證使用情況儀表板] | 以唯讀存取權檢視授權使用控制面板。 |
| [!DNL Dashboards] | [!UICONTROL 管理標準控制面板] | 新增尚未在Data Warehouse中的自訂屬性。 |
| [!DNL Query Service] | [!UICONTROL 管理查詢] | 存取讀取、建立、編輯和刪除Platform資料的結構化SQL查詢。 |
| [!DNL Query Service] | [!UICONTROL 管理查詢服務整合] | 有權建立、更新和刪除「查詢服務」存取的未到期憑證。 |

## 後續步驟

閱讀本指南後，您便了解了 [!DNL Experience Platform]. 您現在可以繼續 [存取控制使用手冊](./ui/overview.md) 以取得如何使用的詳細步驟 [!DNL Admin Console] 若要建立產品設定檔並指派權限 [!DNL Platform].
