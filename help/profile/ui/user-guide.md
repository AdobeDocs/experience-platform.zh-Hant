---
keywords: Experience Platform；設定檔；即時客戶設定檔；疑難排解；API；統一設定檔；統一設定檔；統一設定檔；rtcp；啟用設定檔；啟用設定檔；聯合結構；聯合設定檔；聯合設定檔
title: 即時客戶個人檔案UI指南
topic-legacy: guide
description: 「即時客戶設定檔」可結合來自多個管道的資料，包括線上、離線、CRM和協力廠商資料，讓您全面了解每個客戶。 本檔案可做為在Adobe Experience Platform使用者介面中與即時客戶設定檔互動的指南。
exl-id: 792a3a73-58a4-4163-9212-4d43d24c2770
source-git-commit: 771be1f5939066295c01eb573a13dbb740e8c776
workflow-type: tm+mt
source-wordcount: '1774'
ht-degree: 0%

---

# [!DNL Real-time Customer Profile] UI指南

[!DNL Real-time Customer Profile] 結合來自多個管道的資料，包括線上、離線、CRM和協力廠商資料，建立個別客戶的全方位檢視。本檔案可做為在Adobe Experience Platform使用者介面(UI)中與[!DNL Real-time Customer Profile]資料互動的指南。

## 快速入門

本UI指南需要了解與管理[!DNL Real-time Customer Profiles]相關的各種[!DNL Experience Platform]服務。 閱讀本指南或使用UI之前，請先檢閱本檔案以了解下列服務：

* [[!DNL Real-time Customer Profile] 概述](../home.md):根據來自多個來源的匯總資料，提供統一的即時消費者設定檔。
* [[!DNL Identity Service]](../../identity-service/home.md):可在 [!DNL Real-time Customer Profile] 擷取不同資料來源的身分時，將其橋接至中，以 [!DNL Platform]啟用。
* [[!DNL Experience Data Model (XDM)]](../../xdm/home.md):組織客戶體驗資 [!DNL Platform] 料的標準化架構。

## [!UICONTROL 概觀]

在Experience PlatformUI中，在左側導覽中選取&#x200B;**[!UICONTROL Profiles]**&#x200B;以開啟顯示設定檔控制面板的&#x200B;**[!UICONTROL Overview]**&#x200B;標籤。

>[!NOTE]
>
>如果您的組織是初次使用Platform，且尚未建立作用中的設定檔資料集或合併原則，則不會顯示[!UICONTROL Profiles]控制面板。 相反地， [!UICONTROL 概述]標籤會顯示可協助您開始使用即時客戶設定檔的連結和檔案。

### 設定檔控制面板 {#profile-dashboard}

設定檔控制面板會概述與貴組織設定檔資料相關的關鍵量度。

若要深入了解，請造訪[設定檔控制面板指南](../../dashboards/guides/profiles.md)。

![](../../dashboards/images/profiles/dashboard-overview.png)

##  瀏覽標籤量度

選取&#x200B;**[!UICONTROL Browse]**&#x200B;標籤，以顯示與您組織的設定檔資料相關的數個量度。 您也可以使用此索引標籤，使用合併原則或身分來瀏覽設定檔存放區，如本指南下一節所述。

**[!UICONTROL Browse]**&#x200B;標籤的右側是[設定檔計數](#profile-count)以及按命名空間](#profiles-by-namespace)列出的[設定檔清單。

>[!NOTE]
>
>這些設定檔度量可能與[設定檔控制面板](#profile-dashboard)上顯示的度量不同，因為這些度量是使用您組織的預設合併原則評估的。 有關使用合併策略的詳細資訊，包括如何定義預設合併策略，請參閱[合併策略概述](../merge-policies/overview.md)。

除了這些量度外，本區段還提供上次更新的日期和時間，顯示上次評估量度的時間。

![](../images/user-guide/profiles-browse-metrics.png)

### 設定檔計數 {#profile-count}

設定檔計數會顯示貴組織在Experience Platform內擁有的設定檔總數，當貴組織的預設合併原則已合併設定檔片段，以便為每個個別客戶建立單一設定檔時。 換句話說，您的組織可能有多個與跨不同管道與您的品牌互動的單一客戶相關的描述檔片段，但這些片段會合併在一起（根據預設合併原則），並傳回「1」個描述檔的計數，因為這些片段都與同一個個人相關。

設定檔計數也包含具有屬性（記錄資料）的設定檔，以及僅包含時間序列（事件）資料的設定檔，例如Adobe Analytics設定檔。 設定檔計數會定期重新整理，以提供Platform內最新的設定檔總數。

#### 更新設定檔計數量度

當記錄擷取至[!DNL Profile]存放區時，計數會增加或減少5%以上，便會觸發工作以更新計數。 對於串流資料工作流程，會每小時進行檢查，以判斷是否符合5%的增加或減少臨界值。 若已觸發，則會自動觸發工作以更新設定檔計數。 對於批次內嵌，在成功將批次內嵌至設定檔存放區後15分鐘內，如果符合5%的增加或減少臨界值，則會執行工作以更新設定檔計數。

### [!UICONTROL 依命名空間的設定檔] {#profiles-by-namespace}

**[!UICONTROL 依命名空間的設定檔]**&#x200B;量度會顯示設定檔存放區中所有合併設定檔的命名空間總數和劃分。 依命名空間的設定檔總數（換句話說，將每個命名空間顯示的值加總）一律會高於設定檔計數量度，因為一個設定檔可以有多個相關聯的命名空間。 例如，如果客戶在多個管道上與您的品牌互動，則多個命名空間將會與該個別客戶相關聯。

#### 依命名空間]更新[!UICONTROL 設定檔量度

與[設定檔計數](#profile-count)量度類似，當將記錄擷取至[!DNL Profile]存放區時，計數會增加或減少5%以上時，就會觸發工作以更新命名空間量度。 對於串流資料工作流程，會每小時進行檢查，以判斷是否符合5%的增加或減少臨界值。 若已觸發，則會自動觸發工作以更新設定檔計數。 對於批次內嵌，在成功將批次內嵌至[!DNL Profile]存放區後15分鐘內，若符合5%的增加或減少臨界值，則會執行工作以更新量度。

## 使用[!UICONTROL Browse]標籤來檢視設定檔

在&#x200B;**[!UICONTROL Browse]**&#x200B;標籤上，您可以使用合併原則檢視範例設定檔，或使用身分命名空間和值來尋找特定設定檔。

![](../images/user-guide/browse-by-none-selected.png)

### 按[!UICONTROL 合併策略]瀏覽

預設情況下，將&#x200B;**[!UICONTROL Browse]**&#x200B;頁簽設定為貴組織的預設合併策略。 要選擇不同的合併策略，請選擇合併策略名稱旁的`X`，然後使用選擇器開啟&#x200B;**[!UICONTROL 選擇合併策略]**&#x200B;對話框。

>[!NOTE]
>
>如果未選擇合併策略，請使用&#x200B;**[!UICONTROL Merge policy]**&#x200B;欄位旁邊的選擇器按鈕開啟選擇對話框。

![](../images/user-guide/browse-by-merge-policy.png)

要從&#x200B;**[!UICONTROL 選擇合併策略]**&#x200B;對話框中選擇合併策略，請選擇策略名稱旁的單選按鈕，然後使用&#x200B;**[!UICONTROL 選擇]**&#x200B;返回[!UICONTROL 瀏覽]頁簽。 然後，您可以選擇&#x200B;**[!UICONTROL View]**&#x200B;以刷新示例配置檔案，並查看應用了新合併策略的配置檔案的抽樣。

![](../images/user-guide/select-merge-policy-dialog.png)

顯示的設定檔代表在套用選取的合併原則後，您組織的設定檔存放區中最多20個設定檔的範例。 將新資料新增至組織的設定檔存放區時，會重新整理所選合併原則的範例設定檔。

若要檢視其中一個範例設定檔的詳細資訊，請選取&#x200B;**[!UICONTROL 設定檔ID]**。 如需詳細資訊，請參閱本指南後面的[檢視設定檔詳細資料](#profile-detail)一節。

![](../images/user-guide/sample-profiles.png)

若要進一步了解合併原則及其在Platform中的角色，請參閱[合併原則概述](../merge-policies/overview.md)。


### 按[!UICONTROL Identity]瀏覽 {#browse-identity}

在&#x200B;**[!UICONTROL Browse]**&#x200B;標籤上，您可以使用身分命名空間，以便根據身分值查詢特定設定檔。 依身分瀏覽需要您提供合併原則、身分命名空間和身分值。

![](../images/user-guide/browse-by-identity.png)

如有必要，請使用&#x200B;**[!UICONTROL 合併策略]**&#x200B;選擇器開啟&#x200B;**[!UICONTROL 選擇合併策略]**&#x200B;對話框，並選擇要使用的合併策略。

![](../images/user-guide/select-merge-policy-dialog.png)

然後，使用&#x200B;**[!UICONTROL 身份命名空間]**&#x200B;選擇器開啟&#x200B;**[!UICONTROL 選擇身份命名空間]**&#x200B;對話框，並選擇要搜索的命名空間。 如果您的組織有許多命名空間，您可以使用對話方塊中的搜尋列，開始輸入命名空間的名稱。

您可以選取命名空間以檢視其他詳細資訊，或選取選項按鈕以選擇命名空間。 然後，可以使用&#x200B;**[!UICONTROL 選擇]**&#x200B;繼續。

![](../images/user-guide/profiles-select-identity-namespace.png)

選擇[!UICONTROL 身份命名空間]並返回[!UICONTROL Browse]頁簽後，您可以輸入與所選命名空間相關的&#x200B;**[!UICONTROL 身份值]**。

>[!NOTE]
>
>此值是個別客戶設定檔專屬的值，且必須為所提供命名空間的有效項目。 例如，選取身分命名空間「Email」需要以有效電子郵件地址的形式提供身分值。

![](../images/user-guide/browse-by-identity-values.png)

輸入值後，選擇&#x200B;**[!UICONTROL View]**&#x200B;並返回與值匹配的單個配置檔案。 選取&#x200B;**[!UICONTROL 設定檔ID]**&#x200B;以檢視設定檔詳細資訊。

![](../images/user-guide/browse-by-identity-profile.png)

## 檢視設定檔詳細資訊 {#profile-detail}

選取&#x200B;**[!UICONTROL 設定檔ID]**&#x200B;後， **[!UICONTROL Detail]**&#x200B;標籤隨即開啟。 顯示在&#x200B;**[!UICONTROL Detail]**&#x200B;標籤上的配置檔案資訊已從多個配置檔案片段合併到一起，以形成單個客戶的單一視圖。 這包括客戶詳細資訊，例如基本屬性、連結身分和管道偏好設定。

您也可以在組織層級變更顯示的預設欄位，以顯示偏好的設定檔屬性。 若要進一步了解自訂這些欄位，包括新增和移除屬性以及調整控制面板大小的逐步指示，請參閱[設定檔詳細自訂指南](profile-customization.md)。

![](../images/user-guide/profiles-profile-detail.png)

您可以選取其他可用標籤，以檢視與個別客戶設定檔相關的其他資訊。 這些標籤包含屬性、事件，以及顯示設定檔目前合格之區段的區段成員資格標籤。

![](../images/user-guide/profiles-attributes-events-segments.png)

### 「屬性」索引標籤

**[!UICONTROL Attributes]**&#x200B;頁簽提供一個清單視圖，在應用指定的合併策略後匯總與單個配置檔案相關的所有屬性。

選取&#x200B;**[!UICONTROL 檢視JSON]**，也可將這些屬性視為JSON物件。 如有使用者希望進一步了解設定檔屬性擷取至Platform的方式，此功能將有所幫助。

![](../images/user-guide/profiles-attributes.png)

### 事件索引標籤

**[!UICONTROL Events]**&#x200B;標籤包含與客戶相關聯的ExperienceEvents相關的資料。 這可能包括電子郵件開啟、購物車活動、頁面檢視等。 為任何個別事件選取&#x200B;**[!UICONTROL 檢視全部]**，會提供其他欄位和作為事件一部分擷取的值。

選取&#x200B;**[!UICONTROL 檢視JSON]**，也可將事件視為JSON物件。 這有助於了解Platform中擷取事件的方式。

![](../images/user-guide/profiles-events.png)

### 區段成員資格標籤

**[!UICONTROL 區段成員資格]**&#x200B;索引標籤會顯示清單，其中包含個別客戶設定檔目前所屬區段的名稱和說明。 當設定檔符合區段的資格或過期時，此清單會自動更新。 目前符合設定檔資格的區段總數會顯示在索引標籤的右側。

如需Experience Platform中分段的詳細資訊，請參閱[AdobeExperience Platform分段服務檔案](../../segmentation/home.md)。

![](../images/user-guide/profiles-segment-membership.png)

## 合併策略

從主&#x200B;**[!UICONTROL 配置檔案]**&#x200B;菜單中，選擇&#x200B;**[!UICONTROL 合併策略]**&#x200B;頁簽以查看屬於您組織的合併策略清單。 每個列出的策略都顯示其名稱，無論它是否為預設合併策略，以及它所應用的架構類。

有關合併策略的詳細資訊，請參閱[合併策略概述](../merge-policies/overview.md)。

![](../images/user-guide/profiles-merge-policies.png)

## 聯合架構 {#union-schema}

從主&#x200B;**[!UICONTROL Profiles]**&#x200B;功能表中，選擇&#x200B;**[!UICONTROL 聯合架構]**&#x200B;標籤以查看所擷取資料的可用聯合架構。 聯合架構是同一類下所有[!DNL Experience Data Model](XDM)欄位的合併，其架構已啟用在[!DNL Real-time Customer Profile]中使用。

有關聯合架構的詳細資訊，請訪問[聯合架構UI指南](union-schema.md)。

![](../images/user-guide/profiles-union-schema.png)

## 後續步驟

閱讀本指南後，您就能了解如何使用Experience PlatformUI檢視及管理組織的設定檔資料。 有關如何使用Experience PlatformAPI處理設定檔資料的資訊，請參閱[即時客戶設定檔API指南](../api/overview.md)。
