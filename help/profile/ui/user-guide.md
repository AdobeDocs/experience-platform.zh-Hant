---
keywords: Experience Platform；配置檔案；即時客戶配置檔案；故障排除；API；統一配置檔案；統一配置檔案；配置檔案；rtcp；啟用配置檔案；啟用配置檔案；聯合架構；聯合配置檔案；聯合配置檔案
title: 即時客戶概要檔案UI指南
description: 即時客戶配置檔案可建立您每個客戶的整體視圖，將來自多個渠道的資料組合在一起，包括線上、離線、CRM和第三方資料。 本文檔是與Adobe Experience Platform用戶介面中的即時客戶概要檔案交互的指南。
exl-id: 792a3a73-58a4-4163-9212-4d43d24c2770
source-git-commit: 0f7ef438db5e7141197fb860a5814883d31ca545
workflow-type: tm+mt
source-wordcount: '1951'
ht-degree: 0%

---

# [!DNL Real-Time Customer Profile] UI指南

[!DNL Real-Time Customer Profile] 建立您每個客戶的整體視圖，將來自多個渠道的資料組合在一起，包括線上、離線、CRM和第三方資料。 本文檔用作與 [!DNL Real-Time Customer Profile] Adobe Experience Platform用戶介面(UI)中的資料。

## 快速入門

本UI指南要求瞭解 [!DNL Experience Platform] 管理涉及的服務 [!DNL Real-Time Customer Profiles]。 在閱讀本指南或在UI中工作之前，請查看以下服務的文檔：

* [[!DNL Real-Time Customer Profile] 概述](../home.md):基於來自多個源的聚合資料提供統一、即時的用戶配置檔案。
* [[!DNL Identity Service]](../../identity-service/home.md):啟用 [!DNL Real-Time Customer Profile] 通過橋接來自不同資料源的身份（在它們被攝取時） [!DNL Platform]。
* [[!DNL Experience Data Model (XDM)]](../../xdm/home.md):標準化框架 [!DNL Platform] 組織客戶體驗資料。

## [!UICONTROL 概觀]

在Experience PlatformUI中，選擇 **[!UICONTROL 配置檔案]** 的下界 **[!UICONTROL 概述]** 頁籤。

>[!NOTE]
>
>如果您的組織是新加入平台的，並且尚未建立活動的配置檔案資料集或合併策略， [!UICONTROL 配置檔案] 儀表板不可見。 相反， [!UICONTROL 概述] 頁籤顯示幫助您開始使用即時客戶配置檔案的連結和文檔。

### 配置檔案儀表板 {#profile-dashboard}

配置檔案儀表板概述了與您組織的配置檔案資料相關的關鍵度量。

要瞭解更多資訊，請訪問 [配置檔案儀表板指南](../../dashboards/guides/profiles.md)。

![此時將顯示「配置檔案」操控板。](../../dashboards/images/profiles/dashboard-overview.png)

## [!UICONTROL 瀏覽] 頁籤度量

選擇 **[!UICONTROL 瀏覽]** 頁籤，顯示與組織的配置檔案資料相關的多個度量。 您還可以使用此頁籤使用合併策略或標識瀏覽配置檔案儲存，如本指南下一節中所述。

在 **[!UICONTROL 瀏覽]** 頁籤 [配置檔案計數](#profile-count) 以及 [按命名空間配置檔案](#profiles-by-namespace)。

>[!NOTE]
>
>這些配置式度量可能與顯示在 [配置檔案儀表板](#profile-dashboard) 因為使用您組織的預設合併策略評估它們。 有關使用合併策略（包括如何定義預設合併策略）的詳細資訊，請參閱 [合併策略概述](../merge-policies/overview.md)。

除了這些度量外，本節還提供了上次更新的日期和時間，顯示上次評估度量的時間。

![將顯示並突出顯示「配置檔案」度量。](../images/user-guide/browse-metrics.png)

### 設定檔計數 {#profile-count}

配置檔案計數顯示組織在Experience Platform內具有的配置檔案總數，此時，組織的預設合併策略已將配置檔案片段合併到一起，為每個單個客戶形成一個配置檔案。 換句話說，您的組織可能具有多個與單個客戶相關的配置檔案片段，這些客戶通過不同渠道與您的品牌進行交互，但這些片段將合併到一起（根據預設合併策略），並將返回「1」個配置檔案的計數，因為它們都與同一個人相關。

配置檔案計數還包括具有屬性（記錄資料）的配置檔案以及僅包含時間序列（事件）資料的配置檔案，如Adobe Analytics配置檔案。 定期刷新配置檔案計數，以提供平台內最新的配置檔案總數。

#### 更新配置檔案計數度量

當記錄被攝入 [!DNL Profile] 儲存增加或減少計數超過5%，觸發作業以更新計數。 對於流式資料工作流，每小時檢查以確定是否滿足5%的增減閾值。 如果已觸發，則自動觸發作業以更新配置檔案計數。 對於批處理接收，在成功將批處理插入配置檔案儲存15分鐘內，如果滿足5%增加或減少閾值，則運行一個作業以更新配置檔案計數。

### [!UICONTROL 按命名空間分列的配置檔案] {#profiles-by-namespace}

的 **[!UICONTROL 按命名空間分列的配置檔案]** 度量顯示配置檔案儲存中所有合併配置檔案中命名空間的總數和細分。 按命名空間（即將每個命名空間顯示的值加在一起）的配置檔案總數將始終高於配置檔案計數度量，因為一個配置檔案可能有多個與其關聯的命名空間。 例如，如果客戶在多個渠道上與您的品牌進行交互，則多個命名空間將與該客戶關聯。

#### 更新 [!UICONTROL 按命名空間分列的配置檔案] 度量

與 [配置檔案計數](#profile-count) 度量，當記錄被攝入 [!DNL Profile] 儲存增加或減少計數超過5%，觸發作業以更新命名空間度量。 對於流式資料工作流，每小時檢查以確定是否滿足5%的增減閾值。 如果已觸發，則自動觸發作業以更新配置檔案計數。 對於批處理，在成功將批處理插入到 [!DNL Profile] 儲存，如果滿足5%的增加或減少閾值，則運行作業以更新度量。

## 使用 [!UICONTROL 瀏覽] 頁籤，查看概要檔案

在 **[!UICONTROL 瀏覽]** 頁籤，您可以使用合併策略查看示例配置檔案，或使用標識命名空間和值查找特定配置檔案。

![將顯示屬於組織的配置檔案。](../images/user-guide/none-selected.png)

### 瀏覽者 [!UICONTROL 合併策略]

的 **[!UICONTROL 瀏覽]** 頁籤在預設情況下設定為組織的預設合併策略。 要選擇其他合併策略，請選擇 `X` 在合併策略名稱旁邊，然後使用選擇器開啟 **[!UICONTROL 選擇合併策略]** 對話框。

>[!NOTE]
>
>如果未選擇合併策略，請使用 **[!UICONTROL 合併策略]** 的子菜單。

![「合併策略」選擇器將突出顯示。](../images/user-guide/browse-by-merge-policy.png)

從中選擇合併策略 **[!UICONTROL 選擇合併策略]** 對話框，選擇策略名稱旁邊的單選按鈕，然後使用 **[!UICONTROL 選擇]** 返回 [!UICONTROL 瀏覽] 頁籤。 然後可以選擇 **[!UICONTROL 視圖]** 刷新示例配置檔案，並查看應用了新合併策略的配置檔案的抽樣。

![將顯示一個對話框，您可以在其中選擇要篩選依據的合併策略。](../images/user-guide/select-merge-policy.png)

顯示的配置檔案表示在應用所選合併策略後，您組織的配置檔案儲存中最多有20個配置檔案的示例。 在將新資料添加到組織的配置檔案儲存時，將刷新所選合併策略的示例配置檔案。

要查看其中一個示例配置檔案的詳細資訊，請選擇 **[!UICONTROL 配置檔案ID]**。 有關詳細資訊，請參閱本指南後面的部分。 [查看配置檔案詳細資訊](#profile-detail)。

![將顯示與合併策略匹配的配置檔案示例。](../images/user-guide/sample-profiles.png)

要瞭解有關合併策略及其在平台中角色的詳細資訊，請參閱 [合併策略概述](../merge-policies/overview.md)。

### 瀏覽者 [!UICONTROL 身份] {#browse-identity}

在 **[!UICONTROL 瀏覽]** 頁籤，可以使用標識命名空間以按標識值查找特定配置檔案。 按標識瀏覽要求您提供合併策略、標識命名空間和標識值。

![合併策略選擇器將突出顯示。](../images/user-guide/browse-by-merge-policy.png)

如有必要，請使用 **[!UICONTROL 合併策略]** 選擇器以開啟 **[!UICONTROL 選擇合併策略]** 對話框，然後選擇要使用的合併策略。

![將顯示一個對話框，您可以在其中選擇要篩選依據的合併策略。](../images/user-guide/select-merge-policy.png)

然後使用 **[!UICONTROL 標識命名空間]** 選擇器以開啟 **[!UICONTROL 選擇標識命名空間]** 對話框，然後選擇要搜索的命名空間。 如果您的組織有許多命名空間，則可以使用對話框中的搜索欄開始鍵入命名空間的名稱。

您可以選擇一個命名空間以查看其他詳細資訊，或選擇單選按鈕以選擇一個命名空間。 然後，您可以 **[!UICONTROL 選擇]** 繼續。

![將顯示一個對話框，您可以在其中選擇要篩選依據的標識名稱空間。](../images/user-guide/select-identity-namespace.png)

選擇後 [!UICONTROL 標識命名空間] 回到 [!UICONTROL 瀏覽] 的子菜單。 **[!UICONTROL 標識值]** 與所選命名空間相關。

>[!NOTE]
>
>此值特定於單個客戶配置檔案，並且必須為提供的命名空間的有效條目。 例如，選擇標識命名空間「電子郵件」需要有效電子郵件地址形式的標識值。

![要篩選依據的標識值將突出顯示。](../images/user-guide/filter-identity-value.png)

輸入值後，選擇 **[!UICONTROL 視圖]** 並返回與值匹配的單個配置檔案。 選擇 **[!UICONTROL 配置檔案ID]** 查看配置檔案詳細資訊。

![與標識值匹配的配置檔案將突出顯示。](../images/user-guide/filtered-identity-value.png)

## 查看配置檔案詳細資訊 {#profile-detail}

選擇後 **[!UICONTROL 配置檔案ID]**，也請參見Wiki頁。 **[!UICONTROL 詳細資訊]** 的子菜單。 顯示在 **[!UICONTROL 詳細資訊]** 頁籤已從多個配置檔案片段合併在一起，以形成單個客戶的單個視圖。 這包括客戶詳細資訊，如基本屬性、連結標識和渠道首選項。

在組織層還可以更改顯示的預設欄位，以顯示首選的配置檔案屬性。 要瞭解有關自定義這些欄位的詳細資訊，包括添加和刪除屬性以及調整儀表板面板大小的逐步說明，請閱讀 [配置檔案詳細資訊定制指南](profile-customization.md)。

![「詳細資訊」(Details)頁籤將突出顯示。 此時將顯示配置檔案詳細資訊。](../images/user-guide/profile-detail.png)

通過選擇其它可用標籤，您可以查看與單個客戶配置檔案相關的附加資訊。 這些頁籤包括屬性、事件和顯示當前限定了配置檔案的段的段成員資格頁籤。

### 「屬性」頁籤

的 **[!UICONTROL 屬性]** 頁籤提供清單視圖，在應用指定的合併策略後，匯總與單個配置檔案相關的所有屬性。

通過選擇以，這些屬性也可以作為JSON對象來查看 **[!UICONTROL 查看JSON]**。 這對希望更好地瞭解配置檔案屬性如何被引入平台的任何用戶都很有幫助。

![「屬性」(Attributes)頁籤將突出顯示。 此時將顯示配置檔案屬性。](../images/user-guide/attributes.png)

### 「事件」頁籤

的 **[!UICONTROL 事件]** 頁籤包含與客戶關聯的100個最近的ExperienceEvents中的資料。 此資料可能包括開啟的電子郵件、購物車活動和頁面視圖。 選擇 **[!UICONTROL 查看全部]** 對於任何單個事件，都提供作為事件一部分捕獲的附加欄位和值。

通過選擇以，事件也可以作為JSON對象查看 **[!UICONTROL 查看JSON]**。 這有助於瞭解如何在平台中捕獲事件。

![「事件」(Events)頁籤將突出顯示。 將顯示配置檔案事件。](../images/user-guide/events.png)

### 「段成員資格」頁籤

的 **[!UICONTROL 段成員資格]** 頁籤顯示一個清單，其中包含單個客戶配置檔案當前所屬的段的名稱和說明。 此清單會在配置檔案符合段或從段過期時自動更新。 配置檔案當前限定的段的總數顯示在頁籤的右側。

有關Experience Platform分段的詳細資訊，請參閱 [AdobeExperience Platform分段服務文檔](../../segmentation/home.md)。

![「段成員身份」(Segment membership)頁籤將突出顯示。 此時將顯示配置檔案段成員身份詳細資訊。](../images/user-guide/segment-membership.png)

## 合併策略

從主 **[!UICONTROL 配置檔案]** 的 **[!UICONTROL 合併策略]** 頁籤，查看屬於您組織的合併策略清單。 每個列出的策略都顯示其名稱，無論它是否是預設合併策略，以及它所應用的架構類。

有關合併策略的詳細資訊，請參見 [合併策略概述](../merge-policies/overview.md)。

![「合併策略」(Merge Policys)頁籤將突出顯示。 將顯示屬於組織的合併策略。](../images/user-guide/merge-policies.png)

## 聯合架構 {#union-schema}

從主 **[!UICONTROL 配置檔案]** 的 **[!UICONTROL 聯合架構]** 頁籤，查看所接收資料的可用聯合架構。 聯合圖式是所有 [!DNL Experience Data Model] (XDM)同一類下的欄位，其架構已啟用，可在 [!DNL Real-Time Customer Profile]。

有關聯合架構的詳細資訊，請訪問 [聯合架構UI指南](union-schema.md)。

![將突出顯示「聯合架構」頁籤。 將顯示屬於組織的聯合架構。](../images/user-guide/union-schema.png)

## 後續步驟

通過閱讀本指南，您知道如何使用Experience PlatformUI查看和管理組織的配置檔案資料。 有關如何使用Experience PlatformAPI處理配置檔案資料的資訊，請參閱 [即時客戶配置檔案API指南](../api/overview.md)。
