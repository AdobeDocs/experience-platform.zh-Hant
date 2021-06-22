---
keywords: Experience Platform；設定檔；即時客戶設定檔；疑難排解；API；統一設定檔；統一設定檔；統一設定檔；rtcp；啟用設定檔；啟用設定檔；聯合結構；聯合設定檔；聯合設定檔
title: 即時客戶個人檔案UI指南
topic-legacy: guide
description: 「即時客戶設定檔」可結合來自多個管道的資料，包括線上、離線、CRM和協力廠商資料，讓您全面了解每個客戶。 本檔案可做為在Adobe Experience Platform使用者介面中與即時客戶設定檔互動的指南。
exl-id: 792a3a73-58a4-4163-9212-4d43d24c2770
source-git-commit: 2791c32abe582d51d05d4bf0488ba82dfadfd053
workflow-type: tm+mt
source-wordcount: '1319'
ht-degree: 0%

---

# [!DNL Real-time Customer Profile] UI指南

[!DNL Real-time Customer Profile] 結合來自多個管道的資料，包括線上、離線、CRM和協力廠商資料，建立個別客戶的全方位檢視。本檔案可做為在Adobe Experience Platform使用者介面(UI)中與[!DNL Real-time Customer Profile]資料互動的指南。

## 快速入門

本UI指南需要了解與管理[!DNL Real-time Customer Profiles]相關的各種[!DNL Experience Platform]服務。 閱讀本指南或使用UI之前，請先檢閱本檔案以了解下列服務：

* [[!DNL Real-time Customer Profile]](../home.md):根據來自多個來源的匯總資料，提供統一的即時消費者設定檔。
* [[!DNL Identity Service]](../../identity-service/home.md):可在 [!DNL Real-time Customer Profile] 擷取不同資料來源的身分時，將其橋接至中，以 [!DNL Platform]啟用。
* [[!DNL Experience Data Model (XDM)]](../../xdm/home.md):組織客戶體驗資 [!DNL Platform] 料的標準化架構。

## 概覽

在Experience PlatformUI中，在左側導覽中選取&#x200B;**[!UICONTROL Profiles]**&#x200B;以開啟顯示[!UICONTROL Profiles]控制面板的&#x200B;**[!UICONTROL Overview]**&#x200B;標籤。

>[!NOTE]
>
>如果您的組織是初次使用Platform，且尚未建立作用中的設定檔資料集或合併原則，則不會顯示[!UICONTROL Profiles]控制面板。 相反地， [!UICONTROL 概述]標籤會顯示可協助您開始使用即時客戶設定檔的連結和檔案。

###  設定檔控制面板  {#profile-dashboard}

**[!UICONTROL Profiles]**&#x200B;控制面板概述與貴組織的Profile資料相關的關鍵量度。

若要深入了解，請造訪[設定檔控制面板指南](../../dashboards/guides/profiles.md)。

![](../../dashboards/images/profiles/dashboard-overview.png)

## 瀏覽

選取&#x200B;**[!UICONTROL Browse]**&#x200B;標籤，以依身分瀏覽設定檔。

![](../images/user-guide/profiles-browse.png)

### 設定檔量度{#profile-metrics}

在&#x200B;**[!UICONTROL Browse]**&#x200B;標籤的右側，是與您的設定檔資料相關的數個重要量度，包括您的設定檔總數[](#profile-count)，以及依命名空間](#profiles-by-namespace)的[設定檔清單。

系統會使用貴組織的預設合併原則評估這些設定檔量度。 有關使用合併策略的詳細資訊，包括如何定義預設合併策略，請參閱[合併策略概述](../merge-policies/overview.md)。

除了這些量度外，設定檔量度區段也提供上次更新的日期和時間，顯示上次評估量度的時間。

![](../images/user-guide/profiles-profile-metrics.png)

### 配置檔案計數{#profile-count}

設定檔計數會在您的組織的預設合併原則已合併設定檔片段，以針對每個個別客戶建立單一設定檔後，顯示您組織在[!DNL Experience Platform]內擁有的設定檔總數。 換句話說，您的組織可能有多個與跨不同管道與您的品牌互動的單一客戶相關的描述檔片段，但這些片段會合併在一起（根據預設合併原則），並傳回「1」個描述檔的計數，因為這些片段都與同一個個人相關。

設定檔計數也包含具有屬性（記錄資料）的設定檔，以及僅包含時間序列（事件）資料的設定檔，例如Adobe Analytics設定檔。 設定檔計數會定期重新整理，以提供Platform內最新的設定檔總數。

當記錄擷取至[!DNL Profile]存放區時，計數會增加或減少5%以上，便會觸發工作以更新計數。 對於串流資料工作流程，會每小時進行檢查，以判斷是否符合5%的增加或減少臨界值。 若已觸發，則會自動觸發工作以更新設定檔計數。 對於批次內嵌，在成功將批次內嵌至設定檔存放區後15分鐘內，如果符合5%的增加或減少臨界值，則會執行工作以更新設定檔計數。

### 按命名空間{#profiles-by-namespace}列出的配置檔案

**[!UICONTROL 依命名空間的設定檔]**&#x200B;量度會顯示設定檔存放區中所有合併設定檔的命名空間總數和劃分。 依命名空間的設定檔總數（換句話說，將每個命名空間顯示的值加總）一律會高於設定檔計數量度，因為一個設定檔可以有多個相關聯的命名空間。 例如，如果客戶在多個管道上與您的品牌互動，則多個命名空間將會與該個別客戶相關聯。

與[設定檔計數](#profile-count)量度類似，當將記錄擷取至[!DNL Profile]存放區時，計數會增加或減少5%以上時，就會觸發工作以更新命名空間量度。 對於串流資料工作流程，會每小時進行檢查，以判斷是否符合5%的增加或減少臨界值。 若已觸發，則會自動觸發工作以更新設定檔計數。 對於批次內嵌，在成功將批次內嵌至[!DNL Profile]存放區後15分鐘內，若符合5%的增加或減少臨界值，則會執行工作以更新量度。

### 合併策略

**[!UICONTROL 合併策略]**&#x200B;選擇器會自動為您的組織選擇預設合併策略。 如果不想使用該合併策略，可以選擇預設合併策略旁的`X`以開啟&#x200B;**[!UICONTROL 選擇合併策略]**&#x200B;對話框，在該對話框中可以選擇其他合併策略。

若要進一步了解合併原則及其在Platform中的角色，請參閱[合併原則概述](../merge-policies/overview.md)。

![](../images/user-guide/profiles-search-merge-policy.png)

### 身分命名空間

**[!UICONTROL 身份命名空間]**&#x200B;選擇器將開啟一個對話框，您可以在其中選擇要搜索的身份命名空間，並可以通過選擇篩選表徵圖並選擇要添加或刪除的屬性來自定義搜索中顯示的屬性。

![](../images/user-guide/profiles-search-filter.png)

從&#x200B;**[!UICONTROL 選擇身份命名空間]**&#x200B;對話框中，選擇要搜索的命名空間，或使用對話框中的搜索欄開始鍵入命名空間的名稱。 您可以選擇一個命名空間以查看其他詳細資訊，在找到要使用的命名空間後，可以選擇單選按鈕，然後按&#x200B;**[!UICONTROL 選擇]**&#x200B;以繼續。

![](../images/user-guide/profiles-select-identity-namespace.png)

### 身分值

選取身分命名空間後，您會返回&#x200B;**[!UICONTROL Browse]**&#x200B;標籤，您可在此輸入&#x200B;**[!UICONTROL 身分值]**。 此值是個別客戶設定檔專屬的值，且必須為所提供命名空間的有效項目。 例如，選取身分命名空間「Email」需要以有效電子郵件地址的形式提供身分值。

![](../images/user-guide/profiles-show-profile.png)

輸入值後，選擇&#x200B;**[!UICONTROL 顯示配置檔案]**&#x200B;並返回與值匹配的單個配置檔案。 選取&#x200B;**[!UICONTROL 設定檔ID]**&#x200B;以檢視設定檔詳細資訊。

![](../images/user-guide/profiles-display-profile.png)

### 配置檔案詳細資訊{#profile-detail}

選取&#x200B;**[!UICONTROL 設定檔ID]**&#x200B;後， **[!UICONTROL Detail]**&#x200B;標籤隨即開啟。 顯示在&#x200B;**[!UICONTROL Detail]**&#x200B;標籤上的配置檔案資訊已從多個配置檔案片段合併到一起，以形成單個客戶的單一視圖。 這包括客戶詳細資訊，例如基本屬性、連結身分和管道偏好設定。 您也可以在組織層級變更顯示的預設欄位，以顯示偏好的設定檔屬性。 若要進一步了解自訂這些欄位，包括新增和移除屬性以及調整控制面板大小的逐步指示，請參閱[設定檔詳細自訂指南](profile-customization.md)。

![](../images/user-guide/profiles-profile-detail.png)

您可以選取其他可用標籤，以檢視與個別設定檔相關的其他資訊。 這些標籤包含屬性、事件和區段成員資格，以顯示目前符合設定檔資格的區段。

![](../images/user-guide/profiles-attributes-events-segments.png)

## 合併策略

從主&#x200B;**[!UICONTROL 配置檔案]**&#x200B;菜單中，選擇&#x200B;**[!UICONTROL 合併策略]**&#x200B;頁簽以查看屬於您組織的合併策略清單。 每個列出的策略都顯示其名稱，無論它是否為預設合併策略，以及它所應用的架構類。

有關合併策略的詳細資訊，請參閱[合併策略概述](../merge-policies/overview.md)。

![](../images/user-guide/profiles-merge-policies.png)

## 聯合架構{#union-schema}

從主&#x200B;**[!UICONTROL Profiles]**&#x200B;功能表中，選擇&#x200B;**[!UICONTROL 聯合架構]**&#x200B;標籤以查看所擷取資料的可用聯合架構。 聯合架構是同一類下所有[!DNL Experience Data Model](XDM)欄位的合併，其架構已啟用在[!DNL Real-time Customer Profile]中使用。

有關聯合架構的詳細資訊，請訪問[聯合架構UI指南](union-schema.md)。

![](../images/user-guide/profiles-union-schema.png)

## 後續步驟

閱讀本指南後，您現在知道如何使用[!DNL Experience Platform] UI檢視和管理您的[!DNL Profile]資料。 有關如何使用即時客戶設定檔API使用設定檔資料的資訊，請參閱[設定檔開發人員指南](../api/overview.md)。
