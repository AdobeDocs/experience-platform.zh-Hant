---
keywords: Experience Platform；首頁；熱門主題；存取控制；adobe admin console
solution: Experience Platform
topic-legacy: overview
title: 存取控制概覽
description: Adobe Experience Platform的存取控制可透過Adobe Admin Console提供。 此功能會運用Admin Console中的產品設定檔，將使用者與權限和沙箱連結。
exl-id: 591d59ad-2784-4ae4-a509-23649ce712c9
source-git-commit: 88593d921d6ad97fc4dfb059f0272817caee06c7
workflow-type: tm+mt
source-wordcount: '1375'
ht-degree: 2%

---

# 存取控制概覽

[!DNL Experience Platform]的訪問控制通過[Adobe Admin Console](https://adminconsole.adobe.com)提供。 此功能會運用[!DNL Admin Console]中的產品設定檔，將使用者與權限和沙箱連結。

## 存取控制階層與工作流程

要配置[!DNL Experience Platform]的訪問控制，您必須擁有具有[!DNL Experience Platform]產品整合的組織的管理員權限。 授予或撤回權限的最低角色為產品設定檔管理員。 可管理權限的其他管理員角色包括產品管理員（可管理產品內的所有設定檔）和系統管理員（無限制）。 如需詳細資訊，請參閱[管理角色](https://helpx.adobe.com/enterprise/using/admin-roles.html)上的Adobe Help Center文章。

>[!NOTE]
>
>此後，本檔案中任何「管理員」的提及，都指產品設定檔管理員或更高版本（如上所述）。

取得和指派存取權限的高階工作流程摘要如下：

- 授權Adobe Experience Platform或使用Experience Platform的應用程式/應用程式服務後，會傳送電子郵件給授權期間指定的管理員。
- 管理員登入[Adobe Admin Console](#adobe-admin-console)，並從概覽頁面上的產品清單中選取&#x200B;**Adobe Experience Platform**。
- 管理員可以檢視預設的[產品設定檔](#product-profiles)，或視需要建立新的客戶產品設定檔。
- 管理員可以編輯任何現有產品設定檔的權限和使用者。
- 建立或編輯產品設定檔時，管理員會使用&#x200B;**[!UICONTROL users]**&#x200B;標籤將使用者新增至設定檔，並透過存取&#x200B;**[!UICONTROL permissions]**&#x200B;標籤，授予這些使用者權限（例如&quot;[!UICONTROL 讀取資料集]&quot;或&quot;[!UICONTROL 管理結構]&quot;）。 同樣地，管理員也可以使用相同的權限索引標籤，將存取權指派給沙箱。
- 當使用者登入[!DNL Experience Platform]使用者介面時，其[!DNL Platform]功能的存取權限會由步驟2授予他們的權限驅動。 例如，如果使用者沒有「[!UICONTROL 檢視資料集]」權限，該使用者將看不到側面功能表中的&#x200B;**[!UICONTROL 資料集]**&#x200B;標籤。

有關如何在[!DNL Experience Platform]中管理訪問控制的詳細步驟，請參閱[訪問控制使用手冊](./ui/overview.md)。

所有對[!DNL Experience Platform] API的呼叫均經過權限驗證，若在目前的使用者內容中找不到適當的權限，則會傳回錯誤。 根據授予目前使用者的權限，UI中的元素會隱藏或變更。

## Adobe Admin Console

Adobe Admin Console提供管理Adobe產品權益和組織存取權限的集中位置。 透過主控台，您可以為各種[!DNL Platform]功能（例如「[!UICONTROL 管理資料集]」、「[!UICONTROL 檢視資料集]」或「[!UICONTROL 管理設定檔]」）授予使用者群組存取權限。

### 產品設定檔

在[!DNL Admin Console]中，權限會透過使用產品設定檔指派給使用者。 產品設定檔可讓您授予一或多個使用者的權限，也可包含使用者對透過產品設定檔指派給他們的沙箱範圍的存取。 可將使用者指派給屬於您組織的一或多個產品設定檔。

### 預設產品設定檔

[!DNL Experience Platform] 隨附兩個預先設定的預設產品設定檔。下表概述每個預設設定檔中提供的內容，包括其所授與的存取沙箱，以及其在該沙箱範圍內所授予的權限。

| 產品個人資料 | 沙箱存取 | 權限 |
| --- | --- | --- |
| 預設生產全部訪問 | 生產 | 適用於[!DNL Experience Platform]的所有權限，但沙箱管理權限除外。 |
| 沙箱管理員 | 不適用 | 僅提供對沙箱管理權限的存取。 |

## 沙箱和權限

非生產沙箱是資料虛擬化的一種形式，可讓您將資料與其他沙箱隔離，且通常用於開發實驗、測試或測試。 產品設定檔的權限可讓設定檔的使用者存取其有權存取的沙箱環境中的[!DNL Platform]功能。 預設Experience Platform授權會授予您五個沙箱（一個生產，四個非生產）。 您最多可新增10個非生產沙箱，最多75個沙箱。 如需詳細資訊，請聯絡您的IMS組織管理員或Adobe銷售代表。

如需[!DNL Experience Platform]中沙箱的詳細資訊，請參閱[沙箱概述](../sandboxes/home.md)。

### 存取沙箱

沙箱的存取權是透過產品設定檔管理。 有關如何為產品設定檔啟用沙箱存取的詳細步驟，請參閱[存取控制使用手冊](./ui/overview.md)。

可授予使用者產品設定檔中一或多個沙箱的存取權。 如果兩個或多個產品設定檔中包含一個使用者，該使用者將可存取這些設定檔中包含的所有沙箱。

「沙箱管理」權限可讓使用者管理、檢視或重設沙箱。

### 權限 {#permissions}

產品設定檔中的權限標籤會顯示該設定檔作用中的沙箱和權限：

![權限 — 概觀](./images/permissions-overview.png)

透過[!DNL Admin Console]授予的權限會依類別排序，有些權限會授予對數個低階功能的存取權。

下表概述[!DNL Admin Console]中[!DNL Experience Platform]的可用權限，並說明其授予存取權的特定[!DNL Platform]功能。 如需如何將權限新增至產品設定檔的詳細步驟，請參閱[存取控制使用手冊](./ui/overview.md)。

| 類別 | 權限 | 說明 |
| --- | --- | --- |
| [!DNL Data Modeling] | [!UICONTROL 管理結構] | 存取讀取、建立、編輯和刪除結構和相關資源。 |
| [!DNL Data Modeling] | [!UICONTROL 檢視結構] | 對結構和相關資源的唯讀存取。 |
| [!DNL Data Modeling] | [!UICONTROL 管理關係] | 訪問讀取、建立、編輯和刪除架構關係。 |
| [!DNL Data Modeling] | [!UICONTROL 管理身分中繼資料] | 存取讀取、建立、編輯和刪除結構的身分中繼資料。 |
| [!DNL Data Management] | [!UICONTROL 管理資料集] | 存取讀取、建立、編輯和刪除資料集。 結構的唯讀存取。 |
| [!DNL Data Management] | [!UICONTROL 檢視資料集] | 資料集和結構的唯讀存取權。 |
| [!DNL Data Management] | [!UICONTROL 資料監控] | 監控資料集和資料流的唯讀存取權。 |
| [!DNL Profile Management] | [!UICONTROL 管理設定檔] | 存取讀取、建立、編輯和刪除客戶設定檔所使用的資料集。 可用設定檔的唯讀存取權。 |
| [!DNL Profile Management] | [!UICONTROL 檢視設定檔] | 可用設定檔的唯讀存取權。 |
| [!DNL Profile Management] | [!UICONTROL 管理區段] | 存取讀取、建立、編輯和刪除區段。 |
| [!DNL Profile Management] | [!UICONTROL 檢視區段] | 可用區段的唯讀存取權。 |
| [!DNL Profile Management] | [!UICONTROL 管理合併策略] | 讀取、建立、編輯和刪除合併策略的訪問權限。 |
| [!DNL Profile Management] | [!UICONTROL 查看合併策略] | 對可用合併策略的只讀訪問。 |
| [!DNL Profile Management] | [!UICONTROL 匯出區段的受眾] | 能夠將評估的受眾區段匯出至資料集。 |
| [!DNL Profile Management] | [!UICONTROL 評估受眾的區段] | 可評估區段定義，為對象產生設定檔。 |
| [!DNL Identities] | [!UICONTROL 管理身分識別命名空間] | 存取讀取、建立、編輯和刪除身分識別命名空間。 |
| [!DNL Identities] | [!UICONTROL 檢視身分識別命名空間] | 身分識別命名空間的唯讀存取。 |
| [!DNL Sandbox Administration] | [!UICONTROL 管理沙箱] | 存取讀取、建立、編輯和刪除沙箱。 |
| [!DNL Sandbox Administration] | [!UICONTROL 檢視沙箱] | 屬於您組織的沙箱的唯讀存取權。 |
| [!DNL Sandbox Administration] | [!UICONTROL 重設沙箱] | 重設沙箱的功能。 |
| [!DNL Destinations] | [!UICONTROL 管理目的地] | 讀取、建立、編輯和停用目的地的存取權。 |
| [!DNL Destinations] | [!UICONTROL 檢視目的地] | 對&#x200B;**[!UICONTROL Catalog]**&#x200B;標籤中可用目的地和&#x200B;**[!UICONTROL Browse]**&#x200B;標籤中已驗證目的地的唯讀存取。 |
| [!DNL Destinations] | [!UICONTROL 啟動目的地] | 可將資料啟用至已建立的作用中目的地。 此權限需要授予將啟用目的地的使用者「檢視目的地」或「管理[!UICONTROL 目的地」]。 |
| [!DNL Destinations] | [!UICONTROL 目標編寫] | 可使用[Adobe Experience Platform目標SDK](../destinations/destination-sdk/overview.md)製作目標。 |
| [!DNL Data Ingestion] | [!UICONTROL 管理來源] | 讀取、建立、編輯和禁用源的訪問權。 |
| [!DNL Data Ingestion] | [!UICONTROL 查看源] | 對&#x200B;**[!UICONTROL Catalog]**&#x200B;標籤中可用源和&#x200B;**[!UICONTROL Browse]**&#x200B;標籤中已驗證源的只讀訪問。 |
| [!DNL Data Ingestion] | [!DNL Manage Audience Share Connections] | 存取建立、接受和拒絕合作夥伴握手，以連接兩個IMS組織並啟用[!DNL Segment Match]流程。 |
| [!DNL Data Ingestion] | [!DNL Manage Audience Share] | 與作用中合作夥伴一起存取[!DNL Segment Match]摘要，以讀取、建立、編輯及發佈。 |
| [!DNL Data Science Workspace] | [!UICONTROL 管理Data Science Workspace] | 在[!DNL Data Science Workspace]中讀取、建立、編輯和刪除的權限。 |
| [!DNL Data Governance] | [!UICONTROL 套用資料使用量標籤] | 讀取、建立和刪除使用標籤的存取權。 |
| [!DNL Data Governance] | [!UICONTROL 管理資料使用策略] | 存取讀取、建立、編輯和刪除資料使用原則。 |
| [!DNL Data Governance] | [!UICONTROL 查看資料使用策略] | 屬於貴組織的資料使用原則的唯讀存取。 |
| [!DNL Data Governance] | [!UICONTROL 查看審核日誌] | 以唯讀方式存取Platform活動的檢視記錄[稽核記錄](../landing/governance-privacy-security/audit-logs/overview.md)。 |
| [!DNL Dashboards] | [!UICONTROL 查看許可證使用情況儀表板] | 以唯讀存取權檢視授權使用控制面板。 |
| [!DNL Dashboards] | [!UICONTROL 管理標準控制面板] | 新增尚未在Data Warehouse中的自訂屬性。 |
| [!DNL Query Service] | [!UICONTROL 管理查詢] | 存取讀取、建立、編輯和刪除Platform資料的結構化SQL查詢。 |
| [!DNL Query Service] | [!UICONTROL 管理查詢服務整合] | 有權建立、更新和刪除「查詢服務」存取的未到期憑證。 |

## 後續步驟

閱讀本指南，您已了解[!DNL Experience Platform]中訪問控制的主要原則。 您現在可以繼續參閱[存取控制使用手冊](./ui/overview.md)以取得詳細步驟，了解如何使用[!DNL Admin Console]建立產品設定檔並為[!DNL Platform]指派權限。
