---
keywords: Experience Platform; home；熱門主題；存取控制；adobe管理控制台
solution: Experience Platform
topic: overview
title: 存取控制概觀
description: Adobe Experience Platform的存取控制權是透過Adobe Admin Console提供。 此功能運用Admin Console中的產品設定檔，可連結使用者與權限和沙盒。
translation-type: tm+mt
source-git-commit: c277caabe851c81f66b822c07a25f4b94466eef0
workflow-type: tm+mt
source-wordcount: '1281'
ht-degree: 2%

---


# 存取控制概觀

[!DNL Experience Platform]的存取控制權是透過[Adobe Admin Console](https://adminconsole.adobe.com)提供。 此功能運用[!DNL Admin Console]中的產品設定檔，將使用者與權限和沙盒連結在一起。

## 存取控制階層和工作流程

要配置[!DNL Experience Platform]的訪問控制，您必須對具有[!DNL Experience Platform]產品整合的組織具有管理員權限。 授予或撤消權限的最低角色是產品配置檔案管理員。 其他可管理權限的管理員角色包括產品管理員（可管理產品內的所有設定檔）和系統管理員（無限制）。 如需詳細資訊，請參閱[管理角色](https://helpx.adobe.com/enterprise/using/admin-roles.html)上的Adobe說明中心文章。

>[!NOTE]
>
>從此開始，本檔案中任何提及「管理員」的內容，都是指產品設定檔管理員或以上（如上所述）。

獲取和分配訪問權限的高級工作流可總結如下：

- 在授權Adobe Experience Platform或使用Experience Platform的應用程式／應用程式服務後，會傳送電子郵件給授權期間指定的管理員。
- 管理員登入[Adobe Admin Console](#adobe-admin-console)，並從概述頁面上的產品清單中選擇&#x200B;**Adobe Experience Platform**。
- 管理員可以檢視預設的[產品設定檔](#product-profiles)，或視需要建立新的客戶產品設定檔。
- 管理員可以編輯任何現有產品設定檔的權限和使用者。
- 在建立或編輯產品配置檔案時，管理員使用&#x200B;**[!UICONTROL 用戶]**&#x200B;頁籤將用戶添加到配置檔案中，並通過訪問&#x200B;**[!UICONTROL 權限]**&#x200B;頁籤授予這些用戶權限（例如&quot;[!UICONTROL 讀取資料集]&quot;或&quot;[!UICONTROL 管理方案]&quot;）。 同樣地，管理員也可以使用相同的權限標籤來指派沙盒的存取權。
- 當使用者登入[!DNL Experience Platform]使用者介面時，其對[!DNL Platform]功能的存取是由步驟2中授予的權限所驅動。 例如，如果用戶沒有「[!UICONTROL 查看資料集]」權限，則該用戶將看不到側面菜單中的&#x200B;**[!UICONTROL 資料集]**&#x200B;頁籤。

有關如何在[!DNL Experience Platform]中管理訪問控制的詳細步驟，請參見[訪問控制使用手冊](./ui/overview.md)。

所有對[!DNL Experience Platform] API的呼叫都經過驗證，以取得權限，如果目前使用者內容中找不到適當的權限，則會傳回錯誤。 在UI中，元素會根據授予目前使用者的權限而隱藏或變更。

## Adobe Admin Console

Adobe Admin Console提供一個集中位置，可讓您管理Adobe產品權益並存取您的組織。 通過控制台，您可以授予用戶組對各種[!DNL Platform]功能的訪問權限，如&quot;[!UICONTROL 管理資料集]&quot;、&quot;[!UICONTROL 查看資料集]&quot;或&quot;[!UICONTROL 管理配置檔案]&quot;。

### 產品設定檔

在[!DNL Admin Console]中，會透過使用產品設定檔，將權限指派給使用者。 產品設定檔可讓您授予一或多個使用者權限，並包含他們透過產品設定檔指派給他們的沙盒範圍的存取權。 使用者可以指派給屬於您組織的一或多個產品設定檔。

### 預設產品設定檔

[!DNL Experience Platform] 提供兩個預先設定的預設產品設定檔。下表概述每個預設設定檔中提供的內容，包括其授與存取權的沙盒，以及其在該沙盒範圍內授與的權限。

| 產品設定檔 | 沙盒存取 | 權限 |
| --- | --- | --- |
| 預設生產完整存取權 | 生產 | 適用於[!DNL Experience Platform]的所有權限，「沙盒管理」權限除外。 |
| 沙盒管理員 | 不適用 | 僅提供「沙盒管理」權限的存取。 |

## 沙盒與權限

非生產沙盒是資料虛擬化的一種形式，可讓您將資料與其他沙盒隔離，通常用於開發實驗、測試或試用。 產品描述檔的權限可讓描述檔的使用者存取他們已獲授權存取的沙盒環境中的[!DNL Platform]功能。 預設的Experience Platform授權會授與您5個沙盒（1個製作和4個非製作）。 您可新增10個非生產沙盒，最多可新增75個沙盒。 如需詳細資訊，請連絡您的IMS組織管理員或Adobe銷售代表。

如需[!DNL Experience Platform]中沙盒的詳細資訊，請參閱[沙盒概述](../sandboxes/home.md)。

### 存取沙盒

沙盒的存取是透過產品設定檔來管理。 有關如何為產品配置檔案啟用對沙盒訪問的詳細步驟，請參閱[訪問控制使用手冊](./ui/overview.md)。

可授予使用者產品設定檔中一或多個沙盒的存取權。 如果一位使用者包含在兩或多個產品設定檔中，該使用者將可存取這些設定檔中包含的所有沙盒。

「沙盒管理」權限可讓使用者管理、檢視或重設沙盒。

### 權限

產品描述檔中的權限標籤會顯示該描述檔的作用中沙盒和權限：

![權限概述](./images/permissions-overview.png)

透過[!DNL Admin Console]授予的權限會依類別排序，有些權限會授與對數個低階功能的存取權。

下表概述[!DNL Admin Console]中[!DNL Experience Platform]的可用權限，並說明其授予存取權的特定[!DNL Platform]功能。 有關如何向產品配置檔案添加權限的詳細步驟，請參閱[訪問控制使用手冊](./ui/overview.md)。

| 類別 | 權限 | 說明 |
| --- | --- | --- |
| [!DNL Data Modeling] | [!UICONTROL 管理結構] | 對讀取、建立、編輯和刪除方案和相關資源的訪問。 |
| [!DNL Data Modeling] | [!UICONTROL 檢視結構] | 方案和相關資源的唯讀存取權。 |
| [!DNL Data Modeling] | [!UICONTROL 管理關係] | 訪問讀取、建立、編輯和刪除架構關係。 |
| [!DNL Data Modeling] | [!UICONTROL 管理身分中繼資料] | 存取方案的讀取、建立、編輯和刪除身分中繼資料。 |
| [!DNL Data Management] | [!UICONTROL 管理資料集] | 存取讀取、建立、編輯和刪除資料集。 結構的只讀訪問。 |
| [!DNL Data Management] | [!UICONTROL 檢視資料集] | 資料集和結構描述的只讀訪問。 |
| [!DNL Data Management] | [!UICONTROL 資料監控] | 監視資料集和流的只讀訪問。 |
| [!DNL Profile Management] | [!UICONTROL 管理設定檔] | 存取用於讀取、建立、編輯和刪除客戶個人檔案的資料集。 可用設定檔的唯讀存取權。 |
| [!DNL Profile Management] | [!UICONTROL 檢視設定檔] | 可用設定檔的唯讀存取權。 |
| [!DNL Profile Management] | [!UICONTROL 管理區段] | 存取讀取、建立、編輯和刪除區段。 |
| [!DNL Profile Management] | [!UICONTROL 檢視區段] | 可用區段的唯讀存取權。 |
| [!DNL Profile Management] | [!UICONTROL 管理合併策略] | 可存取讀取、建立、編輯和刪除合併原則。 |
| [!DNL Profile Management] | [!UICONTROL 查看合併策略] | 可用合併策略的唯讀存取權。 |
| [!DNL Profile Management] | [!UICONTROL 匯出區段的對象] | 能夠將評估的觀眾區隔匯出至資料集。 |
| [!DNL Profile Management] | [!UICONTROL 評估對象的區段] | 可評估區段定義，為觀眾產生個人檔案。 |
| [!DNL Identities] | [!UICONTROL 管理身分識別命名空間] | 存取讀取、建立、編輯和刪除身分名稱空間。 |
| [!DNL Identities] | [!UICONTROL 檢視身分識別命名空間] | 身分名稱空間的唯讀存取。 |
| [!DNL Sandbox Administration] | [!UICONTROL 管理沙盒] | 存取讀取、建立、編輯和刪除沙盒。 |
| [!DNL Sandbox Administration] | [!UICONTROL 檢視沙箱] | 屬於您組織的沙盒的唯讀存取權。 |
| [!DNL Sandbox Administration] | [!UICONTROL 重設沙盒] | 可重設沙盒。 |
| [!DNL Destinations] | [!UICONTROL 管理目標] | 存取讀取、建立、編輯和停用目標。 |
| [!DNL Destinations] | [!UICONTROL 查看目標] | 對&#x200B;**[!UICONTROL Catalog]**&#x200B;標籤中可用目標的只讀訪問，以及對&#x200B;**[!UICONTROL Browse]**&#x200B;標籤中已驗證目標的只讀訪問。 |
| [!DNL Destinations] | [!UICONTROL 啟動目標] | 能夠將資料啟動至已建立的作用中目標。 此權限要求將「查看目標」或「管理[!UICONTROL 目標」]授予要激活目標的用戶。 |
| [!DNL Data Ingestion] | [!UICONTROL 管理來源] | 存取讀取、建立、編輯和停用來源。 |
| [!DNL Data Ingestion] | [!UICONTROL 檢視來源] | 對&#x200B;**[!UICONTROL Catalog]**&#x200B;標籤中可用源的只讀訪問，以及對&#x200B;**[!UICONTROL Browse]**&#x200B;標籤中已驗證源的只讀訪問。 |
| [!DNL Data Science Workspace] | [!UICONTROL 管理資料科學工作區] | 存取[!DNL Data Science Workspace]中的讀取、建立、編輯和刪除。 |
| [!DNL Data Governance] | [!UICONTROL 套用資料使用標籤] | 存取讀取、建立和刪除使用標籤。 |
| [!DNL Data Governance] | [!UICONTROL 管理資料使用原則] | 存取讀取、建立、編輯和刪除資料使用原則。 |
| [!DNL Data Governance] | [!UICONTROL 檢視資料使用原則] | 您組織的資料使用政策的唯讀存取權。 |
| [!DNL Query Service] | [!UICONTROL 管理查詢] | 對平台資料的讀取、建立、編輯和刪除結構化SQL查詢的訪問。 |

## 後續步驟

閱讀本指南後，您將瞭解[!DNL Experience Platform]中訪問控制的主要原則。 您現在可以繼續[存取控制使用指南](./ui/overview.md)，以取得有關如何使用[!DNL Admin Console]來建立產品設定檔並指派[!DNL Platform]權限的詳細步驟。