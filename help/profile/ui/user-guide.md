---
keywords: Experience Platform；設定檔；即時客戶設定檔；疑難排解；API；統一設定檔；Unified；設定檔；rtcp；啟用設定檔；啟用設定檔；聯合結構描述；聯合設定檔
title: 即時客戶設定檔UI指南
description: 即時客戶設定檔可為個別客戶建立整體檢視，並結合來自多個管道的資料，包括線上、離線、CRM和第三方資料。 本檔案可用作在Adobe Experience Platform使用者介面中與Real-time Customer Profile互動的指南。
exl-id: 792a3a73-58a4-4163-9212-4d43d24c2770
source-git-commit: d2694170e2860bd32783ad3f1860b0397e847289
workflow-type: tm+mt
source-wordcount: '2004'
ht-degree: 4%

---

# [!DNL Real-Time Customer Profile] 使用者介面指南

[!DNL Real-Time Customer Profile]會針對個別客戶建立整體檢視，並結合來自多個管道的資料，包括線上、離線、CRM和第三方資料。 本檔案可做為在Adobe Experience Platform使用者介面(UI)中與[!DNL Real-Time Customer Profile]資料互動的指南。

## 快速入門

此UI指南需要瞭解與管理[!DNL Experience Platform]有關的各種[!DNL Real-Time Customer Profiles]服務。 在閱讀本指南或使用UI之前，請檢視以下服務的檔案：

* [[!DNL Real-Time Customer Profile] 概述](../home.md)：根據來自多個來源的彙總資料，提供統一的即時消費者設定檔。
* [[!DNL Identity Service]](../../identity-service/home.md)：啟用[!DNL Real-Time Customer Profile]，方法是在不同資料來源中的身分擷取到[!DNL Experience Platform]時將其橋接起來。
* [[!DNL Experience Data Model (XDM)]](../../xdm/home.md)： [!DNL Experience Platform]用來組織客戶體驗資料的標準化架構。

## [!UICONTROL 概觀]

在Experience Platform UI中，選取左側導覽中的&#x200B;**[!UICONTROL 設定檔]**&#x200B;以開啟顯示設定檔儀表板的&#x200B;**[!UICONTROL 概觀]**&#x200B;標籤。

>[!NOTE]
>
>如果您的組織剛開始使用Experience Platform，但尚未建立作用中的設定檔資料集或合併原則，則不會顯示[!UICONTROL 設定檔]儀表板。 [!UICONTROL 總覽]標籤會顯示連結和檔案，協助您開始使用即時客戶個人檔案。

### 輪廓儀表板 {#profile-dashboard}

設定檔控制面板會概述與組織設定檔資料相關的關鍵量度。

若要進一步瞭解，請造訪[設定檔儀表板指南](../../dashboards/guides/profiles.md)。

![設定檔儀表板已顯示。](../../dashboards/images/profiles/dashboard-overview.png)

## [!UICONTROL 瀏覽]索引標籤

在&#x200B;**[!UICONTROL 瀏覽]**&#x200B;索引標籤上，您可以選取切換按鈕，在&#x200B;**卡片**&#x200B;檢視或&#x200B;**圖形**&#x200B;檢視中檢視您的設定檔。

![卡片與圖表檢視切換會反白顯示。](../images/user-guide/card-graph-view.png)

此外，您可以使用合併原則來瀏覽設定檔，或使用身分名稱空間和值來查詢特定設定檔。

![顯示屬於組織的設定檔。](../images/user-guide/profile-browse.png)

### 依[!UICONTROL 合併原則]瀏覽

根據預設，**[!UICONTROL 瀏覽]**&#x200B;索引標籤已設定為您的組織的預設合併原則。 若要選擇不同的合併原則，請選取合併原則名稱旁的`X`，然後使用選取器開啟&#x200B;**[!UICONTROL 選取合併原則]**&#x200B;對話方塊。

>[!NOTE]
>
>如果未選取合併原則，請使用&#x200B;**[!UICONTROL 合併原則]**&#x200B;欄位旁的選擇器按鈕，開啟選取對話方塊。

![合併原則選擇器已反白顯示。](../images/user-guide/browse-by-merge-policy.png)

若要從&#x200B;**[!UICONTROL 選取合併原則]**&#x200B;對話方塊中選擇合併原則，請選取原則名稱旁的單選按鈕，然後使用&#x200B;**[!UICONTROL 選取]**&#x200B;返回[!UICONTROL 瀏覽]索引標籤。 然後，您可以選取&#x200B;**[!UICONTROL 檢視]**&#x200B;以重新整理範例設定檔，並檢視套用新合併原則的設定檔樣本。

![會顯示一個對話方塊，您可在其中選取要篩選的合併原則。](../images/user-guide/select-merge-policy.png)

顯示的設定檔代表在套用所選合併原則後，貴組織設定檔存放區中最多20個設定檔的範例。 將新資料新增到貴組織的設定檔存放區時，會重新整理所選合併原則的範例設定檔。

若要檢視其中一個範例設定檔的詳細資料，請選取&#x200B;**[!UICONTROL 設定檔識別碼]**。 如需詳細資訊，請參閱本指南稍後關於[檢視設定檔詳細資料](#profile-detail)的章節。

![顯示符合合併原則的範例設定檔。](../images/user-guide/profile-browse-table.png)

若要進一步瞭解合併原則及其在Experience Platform中的角色，請參閱[合併原則概觀](../merge-policies/overview.md)。

### 依[!UICONTROL 身分]瀏覽 {#browse-identity}

在&#x200B;**[!UICONTROL 瀏覽]**&#x200B;索引標籤上，您可以使用身分名稱空間，依身分值查詢特定設定檔。 依身分瀏覽需要您提供合併原則、身分名稱空間和身分值。

![合併原則選擇器已反白顯示。](../images/user-guide/browse-by-merge-policy.png)

必要時，請使用&#x200B;**[!UICONTROL 合併原則]**&#x200B;選擇器開啟&#x200B;**[!UICONTROL 選取合併原則]**&#x200B;對話方塊，並選擇要使用的合併原則。

![會顯示一個對話方塊，您可在其中選取要篩選的合併原則。](../images/user-guide/select-merge-policy.png)

然後使用&#x200B;**[!UICONTROL 身分識別名稱空間]**&#x200B;選取器開啟&#x200B;**[!UICONTROL 選取身分識別名稱空間]**&#x200B;對話方塊，並選擇您要搜尋的名稱空間。 如果您的組織有許多名稱空間，您可以使用對話方塊中的搜尋列，開始輸入名稱空間的名稱。

您可以選取名稱空間以檢視其他詳細資訊，或選取選項按鈕以選擇名稱空間。 然後，您可以使用&#x200B;**[!UICONTROL 選取]**&#x200B;以繼續。

![會顯示一個對話方塊，您可在其中選取要篩選的身分名稱空間。](../images/user-guide/select-identity-namespace.png)

選取[!UICONTROL 身分識別名稱空間]並返回[!UICONTROL 瀏覽]索引標籤後，您可以輸入與所選名稱空間相關的&#x200B;**[!UICONTROL 身分識別值]**。

>[!NOTE]
>
>此值專屬於個別客戶設定檔，且必須是所提供名稱空間的有效專案。 例如，選取身分名稱空間「電子郵件」需要有效電子郵件地址形式的身分值。

![您要篩選的身分值已反白顯示。](../images/user-guide/browse-identity.png)

輸入值之後，選取&#x200B;**[!UICONTROL 檢視]**&#x200B;並傳回符合值的單一設定檔。 選取&#x200B;**[!UICONTROL 設定檔識別碼]**&#x200B;以檢視設定檔。

![符合身分值的設定檔會反白顯示。](../images/user-guide/filtered-identity-value.png)

## 檢視設定檔 {#view-profile}

>[!CONTEXTUALHELP]
>id="platform_errors_uplib_201001_404"
>title="找不到實體"
>abstract="這代表 Experience Platform 無法找到所要求的實體。若要解決此錯誤，請嘗試以下其中一項解決方案：<ul><li>確保您所要存取的實體 URL 列出正確的設定檔 ID。</li><li>確保您擁有所要存取的實體之正確的組織和沙箱組合。</li></ul>"

選取&#x200B;**[!UICONTROL 設定檔識別碼]**&#x200B;後，**[!UICONTROL 詳細資料]**&#x200B;索引標籤會開啟。 **[!UICONTROL 詳細資料]**&#x200B;標籤上顯示的設定檔資訊已從多個設定檔片段合併在一起，以形成個別客戶的單一檢視。 這包括基本屬性、連結的身分和管道偏好設定等客戶細節。

此外，您可以檢視有關設定檔的其他詳細資料，例如其[屬性](#attributes)、[事件](#events)和[對象會籍](#audience-membership)。

### 詳細資訊標籤 {#profile-detail}

**[!UICONTROL 詳細資料]**&#x200B;索引標籤提供有關所選設定檔的更多詳細資訊，並分為四個部分：客戶設定檔深入分析、AI insight Widget、可自訂的Widget和自動分類的Widget。

![設定檔詳細資訊頁面已顯示。](../images/user-guide/profile-details.png)

此外，您可以切換是否顯示AI產生的深入分析、顯示與邊緣比較的中樞詳細資訊，以及在圖形檢視中檢視詳細資訊。

![上方列出的切換(AI產生的深入分析、Hub或Edge資料，以及卡片或圖表檢視)會醒目提示。](../images/user-guide/profile-toggles.png)

#### 客戶輪廓深入分析 {#customer-profile-insights}

**[!UICONTROL 客戶設定檔深入分析]**&#x200B;區段會顯示設定檔屬性的簡短簡介。 這包括設定檔ID、電子郵件、電話號碼、性別、出生日期，以及設定檔的身分和對象會籍。

![顯示客戶設定檔深入分析區段。](../images/user-guide/customer-profile-insights.png)

#### AI 洞察小工具 {#ai-insight-widgets}

[!BADGE Alpha]{type=Informative}此功能目前在Alpha中。

**[!UICONTROL AI insight Widget]**&#x200B;區段會顯示AI產生的小工具。 這些介面工具會根據設定檔資料，包括人口統計（例如年齡、性別或位置）、使用者行為（例如購買記錄、網站活動或社群媒體參與）以及心理變數（例如興趣、偏好或生活方式選擇），提供對設定檔的快速深入分析。 所有AI Widget都使用設定檔中已&#x200B;**存在**&#x200B;的資料。

![顯示AI insight Widget區段。](../images/user-guide/ai-insight-widgets.png)

#### 可自訂的小工具 {#customizable-widgets}

**[!UICONTROL 可自訂的Widget]**&#x200B;區段會顯示您可自訂以符合業務需求的Widget。 您可以將屬性群組至個別的Widget、移除不要的Widget，或調整Widget的配置。

顯示的預設欄位也可以在組織層級變更以顯示偏好的設定檔屬性。 若要深入瞭解如何自訂這些欄位，包括新增和移除屬性以及調整儀表板面板大小的逐步指示，請閱讀[設定檔詳細資料自訂指南](profile-customization.md)。

![顯示可自訂的Widget區段。](../images/user-guide/customizable-widgets.png)

您也可以選擇在檢視屬性名稱作為其顯示名稱與其欄位路徑名稱之間切換。 若要在這兩個顯示之間切換，請選取&#x200B;**[!UICONTROL 顯示顯示名稱]**&#x200B;切換按鈕。

![顯示名稱切換已反白顯示。](../images/user-guide/show-display-names.png)

#### 自動分類的小工具 {#auto-classified-widgets}

[!BADGE Alpha]{type=Informative}此功能目前在Alpha中。

**[!UICONTROL 自動分類Widget]**&#x200B;區段顯示的Widget可運用聯合結構描述來判斷屬性所屬的來源欄位群組，提供更清楚的資料來源內容。 您可以使用搜尋列更輕鬆地在Widget中尋找關鍵字。

這些Widget會結合事件資料（與體驗事件Widget）和屬性資料，好讓您可以統一檢視您的設定檔。 您可以使用這些Widget來探索設定檔資料的結構，以更妥善地建構您的[可自訂的Widget](#customizable-widgets)。

>[!NOTE]
>
>如果有多個來源欄位群組，Widget只會使用&#x200B;**一個**&#x200B;可用選項。

![顯示自動分類的Widget區段。](../images/user-guide/auto-classified-widgets.png)

### 屬性標籤 {#attributes}

**[!UICONTROL 屬性]**&#x200B;索引標籤提供清單檢視，在套用指定的合併原則之後，彙總與單一設定檔相關的所有屬性。

也可以選取&#x200B;**[!UICONTROL 檢視JSON]**，將這些屬性視為JSON物件。 對於想更瞭解如何將設定檔屬性擷取到Experience Platform的使用者，此功能會很有幫助。

![[屬性]索引標籤會反白顯示。 顯示設定檔屬性。](../images/user-guide/attributes.png)

若要檢視Edge上可用的屬性，請在資料位置選擇器上選取&#x200B;**[!UICONTROL Edge]**。

![屬性標籤中的資料位置選擇器會反白顯示。](../images/user-guide/attributes-select.png)

如需邊緣設定檔的詳細資訊，請閱讀[邊緣設定檔檔案](../edge-profiles.md)。

### 事件標籤 {#events}

**[!UICONTROL Events]**&#x200B;索引標籤包含來自與客戶相關聯的100個最新ExperienceEvents的資料。 此資料可能包括電子郵件開啟、購物車活動和頁面檢視。 為任何個別事件選取「**[!UICONTROL 檢視全部]**」，可提供額外的欄位和值做為事件的一部分擷取。

也可以選取&#x200B;**[!UICONTROL 檢視JSON]**，將事件檢視為JSON物件。 這有助於瞭解如何在Experience Platform中擷取事件。

![[事件]索引標籤會反白顯示。 顯示設定檔事件。](../images/user-guide/events.png)

### 對象成員資格標籤 {#audience-membership}

**[!UICONTROL 對象成員資格]**&#x200B;標籤會顯示清單，其中包含個別客戶設定檔目前所屬對象的名稱和說明。 當設定檔符合對象資格或過期時，此清單會自動更新。 設定檔目前符合資格的受眾總數會顯示在索引標籤的右側。

如需Experience Platform中區段的詳細資訊，請參閱[Adobes Experience Platform Segmentation Service檔案](../../segmentation/home.md)。

![標示對象成員資格標籤。 顯示設定檔的對象成員資格詳細資料。](../images/user-guide/audience-membership.png)

若要檢視Edge上可用設定檔的對象成員資格，請在資料位置選取器中選取&#x200B;**[!UICONTROL Edge]**。 您可以在[邊緣分段指南](../../segmentation/methods/edge-segmentation.md)中找到邊緣分段的詳細資訊。

![對象成員資格標籤中的資料位置選擇器會醒目提示。](../images/user-guide/audience-membership-select.png)

## 合併原則

從主要&#x200B;**[!UICONTROL 設定檔]**&#x200B;功能表中，選取&#x200B;**[!UICONTROL 合併原則]**&#x200B;索引標籤，以檢視屬於您組織的合併原則清單。 每個列出的原則都會顯示其名稱（無論是否為預設的合併原則）及其套用的結構描述類別。

如需合併原則的詳細資訊，請參閱[合併原則概觀](../merge-policies/overview.md)。

![[合併原則]索引標籤會反白顯示。 顯示屬於組織的合併原則。](../images/user-guide/merge-policies.png)

## 聯集結構 {#union-schema}

從主要&#x200B;**[!UICONTROL 設定檔]**&#x200B;功能表中，選取&#x200B;**[!UICONTROL 聯合結構描述]**&#x200B;索引標籤，以檢視您擷取資料的可用聯合結構描述。 聯合結構描述是相同類別下所有[!DNL Experience Data Model] (XDM)欄位的合併，其結構描述已在[!DNL Real-Time Customer Profile]中啟用。

如需聯合結構描述的詳細資訊，請造訪[聯合結構描述UI指南](union-schema.md)。

![聯合結構描述索引標籤會反白顯示。 會顯示屬於組織的聯合結構描述。](../images/user-guide/union-schema.png)

## 計算屬性 {#computed-attributes}

從主要&#x200B;**[!UICONTROL 設定檔]**&#x200B;功能表中，選取&#x200B;**[!UICONTROL 計算屬性]**&#x200B;索引標籤，以檢視屬於您組織的計算屬性清單。

![已反白顯示[計算屬性]索引標籤。](../images/user-guide/computed-attributes.png)

如需計算屬性的詳細資訊，請閱讀[計算屬性總覽](../computed-attributes/overview.md)。 如需如何在Experience Platform UI中使用計算屬性的詳細資訊，請參閱[計算屬性UI指南](../computed-attributes/ui.md)。

## 後續步驟

閱讀本指南後，您就會知道如何使用Experience Platform UI檢視及管理組織的設定檔資料。 有關如何使用Experience Platform API處理設定檔資料的資訊，請參閱[即時客戶設定檔API指南](../api/overview.md)。
