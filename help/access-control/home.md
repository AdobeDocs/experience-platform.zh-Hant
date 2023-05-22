---
keywords: Experience Platform；首頁；熱門主題；訪問控制；adobe管理控制台
solution: Experience Platform
title: 存取控制概覽
description: Adobe Experience Platform的出入控制通過Adobe Admin Console提供。 此功能利用Admin Console中的產品配置檔案，將用戶與權限和沙箱連結起來。
exl-id: 591d59ad-2784-4ae4-a509-23649ce712c9
source-git-commit: 88bfcdef65b4a938d573b1beb1952c7e030ebc13
workflow-type: tm+mt
source-wordcount: '1567'
ht-degree: 2%

---

# 存取控制概覽

通過以下方式提供對Adobe Experience Platform的訪問控制： **[!UICONTROL 權限]** 在 [Adobe Experience Cloud](https://experience.adobe.com/)。 此功能利用角色和策略，將用戶與權限和沙箱連結起來。

## 訪問控制層次結構和工作流

要配置Experience Platform的訪問控制，您必須對具有Experience Platform產品的組織具有系統或產品管理員權限。 可授予或撤消權限的最小角色是產品管理員。 可管理權限的其他管理員角色是系統管理員（無限制）。 參見Adobe Help Center上的 [管理角色](https://helpx.adobe.com/enterprise/using/admin-roles.html) 的子菜單。

>[!NOTE]
>
>從此開始，本文檔中提及的任何「管理員」都指產品管理員或更高級別（如上所述）。

獲取和分配訪問權限的高級工作流可總結如下：

- 在授權Adobe Experience Platform或使用Experience Platform的應用程式/應用服務後，將向授權期間指定的管理員發送電子郵件。
- 管理員登錄到 [Adobe Admin Console](#adobe-admin-console) 選擇 **Adobe Experience Platform** 從「概述」(Overview)頁面上的產品清單中。
- 要授予對Experience Platform的訪問權限，管理員需要將用戶添加到預設產品配置檔案： `AEP-Default-All-Users`。
- 在Experience Platform權限中，管理員可以建立新角色或編輯任何現有角色的權限和用戶。
- 建立或編輯角色時，管理員使用 **[!UICONTROL 用戶]** 頁籤，並授予這些用戶的權限(如「」[!UICONTROL 讀取資料集]&quot;或&quot;[!UICONTROL 管理架構]&quot;)編輯角色的權限。 同樣，管理員可以使用相同的編輯選項為沙箱分配訪問權限。
- 當用戶登錄到Experience Platform用戶介面時，其對Experience Platform權能的訪問由從上一步授予他們的權限驅動。 例如，如果用戶沒有 [!UICONTROL 查看資料集] 權限， **[!UICONTROL 資料集]** 頁籤，該用戶將看不到。

有關如何在Experience Platform中管理訪問控制的更詳細步驟，請參見 [訪問控制使用手冊](./ui/overview.md)。

所有對Experience PlatformAPI的調用都已驗證權限，如果在當前用戶上下文中找不到相應的權限，則將返回錯誤。 在UI中，元素將根據授予當前用戶的權限而隱藏或更改。

## 權限 {#platform-permissions}

[!UICONTROL 權限] 為您的組織提供了管理Experience Platform訪問的中心位置。 通過 [!UICONTROL 權限]，您可以授予用戶組對各種Experience Platform權能的訪問權限，如 [!UICONTROL 管理資料集]。 [!UICONTROL 查看資料集]或 [!UICONTROL 管理配置檔案]。

### 角色

在 [!UICONTROL 角色] 部分，通過使用角色將權限分配給用戶。 角色允許您向一個或多個用戶授予權限，還包含他們對通過角色分配給他們的沙盒的範圍的訪問權限。 用戶可以分配給屬於您組織的一個或多個角色。

### 預設角色

Experience Platform有兩個預配置的預設角色。 下表概述了每個預設配置檔案中提供的內容，包括它們授予訪問權限的沙盒以及它們在該沙盒範圍內授予的權限。

| 角色 | 沙盒訪問 | 權限 |
| --- | --- | --- |
| 預設生產所有訪問 | 生產 | 除沙盒管理權限外，適用於Experience Platform的所有權限。 |
| 沙盒管理員 | 不適用 | 僅提供對沙盒管理權限的訪問。 |

## 沙箱和權限

非生產沙盒是一種資料虛擬化的形式，它允許您將資料與其他沙盒隔離，並通常用於開發實驗、測試或試驗。 角色的權限允許角色的用戶訪問他們已授予其訪問權限的沙盒環境中的Experience Platform功能。 預設Experience Platform許可證授予您五個沙箱（一個生產箱和四個非生產箱）。 可以添加10個非生產沙箱，最多可以添加75個沙箱。 有關詳細資訊，請聯繫您組織的管理員或Adobe銷售代表。

有關Experience Platform中沙箱的詳細資訊，請參閱 [箱概述](../sandboxes/home.md)。

### 訪問沙箱

通過角色管理對沙箱的訪問。 有關如何啟用對角色的沙盒的訪問的詳細步驟，請參見 [基於屬性的訪問控制角色指南](./abac/ui/roles.md)。

可以授予用戶對角色中一個或多個沙箱的訪問權限。 如果一個用戶包含在兩個或多個角色中，則該用戶將有權訪問這些角色中包含的所有沙盒。

「沙盒管理」權限允許用戶管理、查看或重置沙盒。

### 資源權限 {#permissions}

資源 [!UICONTROL 權限] 角色中的頁籤顯示該角色處於活動狀態的文本框和權限：

![權限概述](./images/permissions.png)

通過資源權限授予的權限按類別排序，其中一些權限授予對若干低級功能的訪問權限。

下表概述了角色中Experience Platform的可用權限，以及它們授予訪問權限的特定Experience Platform權能的說明。 有關如何向角色添加權限的詳細步驟，請參見 [基於屬性的訪問控制角色指南](./abac/ui/roles.md)。

| 類別 | 權限 | 說明 |
| --- | --- | --- |
| [!DNL Alerts] | [!UICONTROL 查看警報歷史記錄] | 警報歷史記錄的只讀訪問。 |
| [!DNL Alerts] | [!UICONTROL 解決警報] | 訪問讀取、編輯和刪除警報。 |
| [!DNL Alerts] | [!UICONTROL 查看警報] | 警報的只讀訪問。 |
| [!DNL Alerts] | [!UICONTROL 管理警報] | 訪問讀取、建立、編輯和刪除警報歷史記錄。 |
| [!DNL Data Hygiene] | [!UICONTROL 查看資料衛生] | 資料衛生的只讀訪問。 |
| [!DNL Data Hygiene] | [!UICONTROL 管理資料衛生] | 訪問讀取、建立、編輯和刪除資料衛生。 |
| [!DNL Data Modeling] | [!UICONTROL 管理結構描述] | 訪問讀取、建立、編輯和刪除架構和相關資源。 |
| [!DNL Data Modeling] | [!UICONTROL 檢視結構描述] | 對架構和相關資源的只讀訪問。 |
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
| [!DNL Identity Management] | [!UICONTROL 管理身分識別命名空間] | 訪問讀取、建立、編輯和刪除標識命名空間。 |
| [!DNL Identity Management] | [!UICONTROL 檢視身分命名空間] | 標識命名空間的只讀訪問。 |
| [!DNL Identity Management] | [!UICONTROL 查看標識圖] | 標識圖形的只讀訪問。 |
| [!DNL Sandbox Administration] | [!UICONTROL 管理沙箱] | 訪問讀取、建立、編輯和刪除沙箱。 |
| [!DNL Sandbox Administration] | [!UICONTROL 檢視沙箱] | 屬於您組織的沙箱的只讀訪問。 |
| [!DNL Sandbox Administration] | [!UICONTROL 重置沙盒] | 能夠重置沙盒。 |
| [!DNL Destinations] | [!UICONTROL 管理目標] | 訪問讀取、建立和刪除目標激活流和目標帳戶。 |
| [!DNL Destinations] | [!UICONTROL 查看目標] | 對中的可用目標的只讀訪問 **[!UICONTROL 目錄]** 頁籤和已驗證的目標 **[!UICONTROL 瀏覽]** 頁籤。 |
| [!DNL Destinations] | [!UICONTROL 激活目標] | 允許用戶將段激活到現有目標。 啟用激活工作流中的映射步驟。 此權限要求 [!UICONTROL 查看目標] 或 [!UICONTROL 管理目標] 將授予將資料激活到目標的用戶。 |
| [!DNL Destinations] | [!UICONTROL 激活段而不映射] | 使用戶能夠激活到現有目標的段，而不顯示 [映射步驟](../destinations/ui/activate-batch-profile-destinations.md#mapping)。 用戶可以在激活工作流中添加和刪除段，但不能添加或刪除映射的屬性或標識。 此權限要求 [!UICONTROL 激活目標] 授予將將資料激活到目標的用戶的權限。 |
| [!DNL Destinations] | [!UICONTROL 管理和激活資料集目標] | 能夠讀取、建立、編輯和禁用資料集導出流。 還能將資料激活到已建立的活動資料集。 |
| [!DNL Destinations] | [!UICONTROL 目標創作] | 使用 [Adobe Experience Platform Destination SDK](../destinations/destination-sdk/overview.md)。 |
| [!DNL Data Ingestion] | [!UICONTROL 管理源] | 訪問讀取、建立、編輯和禁用源。 |
| [!DNL Data Ingestion] | [!UICONTROL 查看源] | 對中可用源的只讀訪問 **[!UICONTROL 目錄]** 頁籤和經過驗證的源 **[!UICONTROL 瀏覽]** 頁籤。 |
| [!DNL Data Ingestion] | [!DNL Manage Audience Share Connections] | 訪問建立、接受和拒絕合作夥伴握手以連接兩個組織並啟用 [!DNL Segment Match] 流。 |
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

通過閱讀本指南，您已介紹了Experience Platform中訪問控制的主要原則。 您現在可以繼續 [基於屬性的訪問控制使用手冊](./abac/overview.md) 有關如何使用Experience Cloud建立角色和為Experience Platform分配權限的詳細步驟。
