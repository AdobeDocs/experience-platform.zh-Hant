---
keywords: Experience Platform；首頁；熱門主題；訪問控制；adobe管理控制台
solution: Experience Platform
topic-legacy: overview
title: 存取控制概覽
description: Adobe Experience Platform的出入控制通過Adobe Admin Console提供。 此功能利用Admin Console中的產品配置檔案，將用戶與權限和沙箱連結起來。
exl-id: 591d59ad-2784-4ae4-a509-23649ce712c9
source-git-commit: 2677d5f0c4369ab692f9e4b16710098a359402d7
workflow-type: tm+mt
source-wordcount: '1384'
ht-degree: 3%

---

# 存取控制概覽

訪問控制 [!DNL Experience Platform] 通過 [Adobe Admin Console](https://adminconsole.adobe.com)。 此功能利用中的產品配置檔案 [!DNL Admin Console]，它將用戶與權限和沙箱連結。

## 訪問控制層次結構和工作流

為了配置訪問控制 [!DNL Experience Platform]，您必須具有具有 [!DNL Experience Platform] 產品整合。 授予或撤消權限的最小角色是產品配置檔案管理員。 可管理權限的其他管理員角色包括產品管理員（可管理產品內的所有配置檔案）和系統管理員（無限制）。 參見Adobe Help Center上的 [管理角色](https://helpx.adobe.com/enterprise/using/admin-roles.html) 的子菜單。

>[!NOTE]
>
>從此開始，本文檔中提及的任何「管理員」都是指產品配置檔案管理員或更高級別（如上所述）。

獲取和分配訪問權限的高級工作流可總結如下：

- 在授權Adobe Experience Platform或使用Experience Platform的應用程式/應用服務後，將向授權期間指定的管理員發送電子郵件。
- 管理員登錄到 [Adobe Admin Console](#adobe-admin-console) 選擇 **Adobe Experience Platform** 從「概述」(Overview)頁面上的產品清單中。
- 管理員可以查看預設 [產品配置檔案](#product-profiles) 或根據需要建立新的客戶產品配置檔案。
- 管理員可以編輯任何現有產品配置檔案的權限和用戶。
- 建立或編輯產品配置檔案時，管理員使用 **[!UICONTROL 用戶]** 頁籤，並授予這些用戶的權限(如「」[!UICONTROL 讀取資料集]&quot;或&quot;[!UICONTROL 管理架構]&quot;)通過訪問 **[!UICONTROL 權限]** 頁籤。 同樣，管理員可以使用相同的權限頁籤將訪問權限分配給沙箱。
- 當用戶登錄到 [!DNL Experience Platform] 用戶介面，他們對 [!DNL Platform] 權能由步驟2中授予的權限驅動。 例如，如果用戶沒有[!UICONTROL 查看資料集]&quot;權限， **[!UICONTROL 資料集]** 頁籤，該用戶將看不到。

有關如何管理中的訪問控制的更詳細步驟 [!DNL Experience Platform]，請參見 [訪問控制使用手冊](./ui/overview.md)。

所有呼叫 [!DNL Experience Platform] API已驗證權限，如果在當前用戶上下文中找不到相應的權限，則將返回錯誤。 在UI中，元素將根據授予當前用戶的權限而隱藏或更改。

## Adobe Admin Console

Adobe Admin Console為管理Adobe產品權利和組織訪問提供了一個中心位置。 通過控制台，您可以授予用戶組對各種不同的訪問權限 [!DNL Platform] 權能，如&quot;[!UICONTROL 管理資料集]&quot;, &quot;[!UICONTROL 查看資料集]&quot;或&quot;[!UICONTROL 管理配置檔案]。

### 產品基本資料

在 [!DNL Admin Console]，通過使用產品配置檔案將權限分配給用戶。 產品配置檔案允許您向一個或多個用戶授予權限，還包含用戶對通過產品配置檔案分配給他們的沙盒範圍的訪問權限。 可以將用戶分配給屬於您組織的一個或多個產品配置檔案。

### 預設產品配置檔案

[!DNL Experience Platform] 帶有兩個預配置的預設產品配置檔案。 下表概述了每個預設配置檔案中提供的內容，包括它們授予訪問權限的沙盒以及它們在該沙盒範圍內授予的權限。

| 產品描述檔 | 沙盒訪問 | 權限 |
| --- | --- | --- |
| 預設生產所有訪問 | 生產 | 適用於 [!DNL Experience Platform]，沙盒管理權限除外。 |
| 沙盒管理員 | 不適用 | 僅提供對沙盒管理權限的訪問。 |

## 沙箱和權限

非生產沙盒是一種資料虛擬化的形式，它允許您將資料與其他沙盒隔離，並通常用於開發實驗、測試或試驗。 產品配置檔案的權限授予配置檔案的用戶訪問 [!DNL Platform] 沙盒環境中已授予其訪問權限的功能。 預設Experience Platform許可證授予您五個沙箱（一個生產箱和四個非生產箱）。 可以添加10個非生產沙箱，最多可以添加75個沙箱。 請聯繫您的IMS組織管理員或Adobe銷售代表，瞭解更多詳細資訊。

有關中的沙箱的詳細資訊 [!DNL Experience Platform]，請參閱 [箱概述](../sandboxes/home.md)。

### 訪問沙箱

通過產品配置檔案管理對沙箱的訪問。 有關如何啟用對產品配置檔案的沙盒的訪問的詳細步驟，請參見 [訪問控制使用手冊](./ui/overview.md)。

用戶可以被授予對產品配置檔案中一個或多個沙箱的訪問權限。 如果兩個或多個產品配置檔案中包括一個用戶，則該用戶將有權訪問這些配置檔案中包括的所有沙盒。

「沙盒管理」權限允許用戶管理、查看或重置沙盒。

### 權限 {#permissions}

產品配置檔案中的「權限」頁籤顯示該配置檔案處於活動狀態的沙箱和權限：

![權限概述](./images/permissions.png)

通過授予的權限 [!DNL Admin Console] 按類別排序，並授予對幾個低級功能的訪問權限。

下表概述了 [!DNL Experience Platform] 的 [!DNL Admin Console]，包含特定 [!DNL Platform] 授予訪問權限的權能。 有關如何向產品配置檔案添加權限的詳細步驟，請參見 [訪問控制使用手冊](./ui/overview.md)。

| 類別 | 權限 | 說明 |
| --- | --- | --- |
| [!DNL Data Modeling] | [!UICONTROL 管理結構] | 訪問讀取、建立、編輯和刪除架構和相關資源。 |
| [!DNL Data Modeling] | [!UICONTROL 檢視結構] | 對架構和相關資源的只讀訪問。 |
| [!DNL Data Modeling] | [!UICONTROL 管理關係] | 訪問讀取、建立、編輯和刪除架構關係。 |
| [!DNL Data Modeling] | [!UICONTROL 管理標識元資料] | 訪問方案的讀取、建立、編輯和刪除標識元資料。 |
| [!DNL Data Management] | [!UICONTROL 管理資料集] | 訪問讀取、建立、編輯和刪除資料集。 架構的只讀訪問。 |
| [!DNL Data Management] | [!UICONTROL 檢視資料集] | 資料集和架構的只讀訪問。 |
| [!DNL Data Management] | [!UICONTROL 資料監視] | 對監視資料集和流的只讀訪問。 |
| [!DNL Profile Management] | [!UICONTROL 管理配置檔案] | 訪問用於客戶配置檔案的讀取、建立、編輯和刪除資料集。 對可用配置檔案的只讀訪問。 |
| [!DNL Profile Management] | [!UICONTROL 查看配置檔案] | 對可用配置檔案的只讀訪問。 |
| [!DNL Profile Management] | [!UICONTROL 管理區段] | 訪問讀取、建立、編輯和刪除段。 |
| [!DNL Profile Management] | [!UICONTROL 查看段] | 對可用段的只讀訪問。 |
| [!DNL Profile Management] | [!UICONTROL 管理合併策略] | 訪問讀取、建立、編輯和刪除合併策略。 |
| [!DNL Profile Management] | [!UICONTROL 查看合併策略] | 對可用合併策略的只讀訪問。 |
| [!DNL Profile Management] | [!UICONTROL 導出段的受眾] | 將評估的受眾段導出到資料集的能力。 |
| [!DNL Profile Management] | [!UICONTROL 為受眾評估段] | 通過評估段定義為受眾生成配置檔案的能力。 |
| [!DNL Identities] | [!UICONTROL 管理身分識別命名空間] | 訪問讀取、建立、編輯和刪除標識命名空間。 |
| [!DNL Identities] | [!UICONTROL 檢視身分識別命名空間] | 標識命名空間的只讀訪問。 |
| [!DNL Sandbox Administration] | [!UICONTROL 管理沙箱] | 訪問讀取、建立、編輯和刪除沙箱。 |
| [!DNL Sandbox Administration] | [!UICONTROL 檢視沙箱] | 屬於您組織的沙箱的只讀訪問。 |
| [!DNL Sandbox Administration] | [!UICONTROL 重置沙盒] | 能夠重置沙盒。 |
| [!DNL Destinations] | [!UICONTROL 管理目標] | 訪問讀取、建立、編輯和禁用目標。 |
| [!DNL Destinations] | [!UICONTROL 查看目標] | 對中的可用目標的只讀訪問 **[!UICONTROL 目錄]** 頁籤和已驗證的目標 **[!UICONTROL 瀏覽]** 頁籤。 |
| [!DNL Destinations] | [!UICONTROL 激活目標] | 能夠將資料激活到已建立的活動目標。 此權限要求「查看目標」或「管理」 [!UICONTROL 目標&quot;] 授予將激活目標的用戶。 |
| [!DNL Destinations] | [!UICONTROL 目標創作] | 使用 [Adobe Experience Platform Destination SDK](../destinations/destination-sdk/overview.md)。 |
| [!DNL Data Ingestion] | [!UICONTROL 管理源] | 訪問讀取、建立、編輯和禁用源。 |
| [!DNL Data Ingestion] | [!UICONTROL 查看源] | 對中可用源的只讀訪問 **[!UICONTROL 目錄]** 頁籤和經過驗證的源 **[!UICONTROL 瀏覽]** 頁籤。 |
| [!DNL Data Ingestion] | [!DNL Manage Audience Share Connections] | 訪問建立、接受和拒絕合作夥伴握手以連接兩個IMS組織並啟用 [!DNL Segment Match] 流。 |
| [!DNL Data Ingestion] | [!DNL Manage Audience Share] | 訪問讀取、建立、編輯和發佈 [!DNL Segment Match] 與活躍的合作夥伴聯繫。 |
| [!DNL Data Science Workspace] | [!UICONTROL 管理資料科學工作區] | 訪問中的讀取、建立、編輯和刪除 [!DNL Data Science Workspace]。 |
| 資料治理 | [!UICONTROL 應用資料使用標籤] | 訪問讀取、建立和刪除使用標籤。 |
| 資料治理 | [!UICONTROL 管理資料使用策略] | 訪問讀取、建立、編輯和刪除資料使用策略。 |
| 資料治理 | [!UICONTROL 查看資料使用策略] | 對屬於您組織的資料使用策略的只讀訪問。 |
| 資料治理 | [!UICONTROL 查看用戶活動日誌] | 對已錄制的視圖的只讀訪問 [審核日誌](../landing/governance-privacy-security/audit-logs/overview.md) 平台活動。 |
| [!DNL Dashboards] | [!UICONTROL 查看許可證使用儀表板] | 查看許可證使用儀表板的只讀訪問。 |
| [!DNL Dashboards] | [!UICONTROL 管理標準儀表板] | 添加尚未在資料倉庫中的自定義屬性。 |
| [!DNL Query Service] | [!UICONTROL 管理查詢] | 對平台資料的讀取、建立、編輯和刪除結構化SQL查詢的訪問。 |
| [!DNL Query Service] | [!UICONTROL 管理查詢服務整合] | 訪問建立、更新和刪除查詢服務訪問的未過期憑據。 |

## 後續步驟

通過閱讀本指南，您已介紹了 [!DNL Experience Platform]。 您現在可以繼續 [訪問控制使用手冊](./ui/overview.md) 有關如何使用的詳細步驟 [!DNL Admin Console] 建立產品配置檔案並分配權限 [!DNL Platform]。
