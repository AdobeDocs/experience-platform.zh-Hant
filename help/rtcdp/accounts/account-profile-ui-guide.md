---
keywords: rtcdp設定檔；設定檔rtcdp；rtcdp身分；rtcdp合併原則；即時客戶設定檔
title: 帳戶設定檔UI指南
description: 透過使用帳戶設定檔，Adobe Real-Time Customer Data Platform B2B edition可讓您統一來自多個來源的帳戶資訊。 本指南提供在Adobe Experience Platform使用者介面中與帳戶設定檔互動的詳細資訊。
badgeB2B: label="B2B edition" type="Informative" url="https://helpx.adobe.com/legal/product-descriptions/real-time-customer-data-platform-b2b-edition-prime-and-ultimate-packages.html newtab=true"
feature: Profiles, B2B
exl-id: a05e8b84-026e-4482-a288-aa25b441bd69
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '1681'
ht-degree: 0%

---

# 帳戶輪廓 UI 指南

>[!NOTE]
>
>帳戶設定檔僅供Real-Time Customer Data Platform B2B edition客戶使用。 若要進一步瞭解Real-Time CDP，包括每種授權型別可用的功能，請先閱讀[Real-Time CDP概觀](../overview.md)。

帳戶設定檔可讓您統一來自多個來源的帳戶資訊。 此統一的帳戶檢視整合了您多個行銷管道的資料，以及貴組織目前用來儲存客戶帳戶資訊的各種系統。 本檔案提供使用Adobe Experience Platform使用者介面(UI)中可用的Real-Time CDP、B2B edition功能與帳戶設定檔互動的指南。

若要進一步瞭解如何在B2B工作流程中建立帳戶設定檔，請參閱[端對端教學課程](../b2b-tutorial.md)。

## 帳戶設定檔概述 {#account-profiles-overview}

在左側導覽中選取[!UICONTROL 帳戶]下的&#x200B;**[!UICONTROL 設定檔]**，以檢視帳戶設定檔的概觀。 在[!UICONTROL 總覽]標籤下，儀表板會顯示圖形或圖表，在單一進入點顯示Widget。

![帳戶設定檔總覽索引標籤在左側導覽中有設定檔，並反白顯示總覽。](images/b2b-account-profile-overview.png)

如需瞭解詳細資訊，請參閱[[!UICONTROL 帳戶設定檔]](../../dashboards/guides/account-profiles.md)儀表板的檔案。 請參閱[Real-time Customer Data Platform Insights資料模型B2B edition](../../dashboards/data-models/cdp-insights-data-model-b2b.md)的檔案，以取得有關如何使用您的見解資料模型為您的儀表板建立自訂圖表的詳細資訊。

## 設定銷售線索與帳戶的比對 {#configure-lead-to-account-matching}

>[!IMPORTANT]
>
> 只有B2B AI管理員可以啟用、停用及設定銷售機會與帳戶比對服務。 停用服務後，將在24小時內刪除相符的結果。

若要設定銷售機會與帳戶的比對，請在左側導覽的[!UICONTROL 帳戶]下選取&#x200B;**[!UICONTROL 設定檔]**。 在&#x200B;**[!UICONTROL 總覽]**&#x200B;標籤上，選取右上方的&#x200B;**[!UICONTROL 設定]**。

![設定反白顯示的[帳戶設定檔概述]索引標籤。](images/b2b-configuring-accounts-profile.png)

**[!UICONTROL 帳戶設定]**&#x200B;對話方塊開啟。 從此處選取&#x200B;**[!UICONTROL 啟用銷售線索與帳戶的比對]**&#x200B;切換以啟用此功能。 使用下拉式功能表，針對&#x200B;**[!UICONTROL 相符的步調]**&#x200B;設定選取&#x200B;**[!UICONTROL 每日]**。 最後，請選取相關的&#x200B;**[!UICONTROL 符合條件]**&#x200B;選項，然後選取&#x200B;**[!UICONTROL 儲存]**，以確認您的設定並返回&#x200B;**[!UICONTROL 帳戶設定檔]**&#x200B;畫面。

>[!NOTE]
>
> 地址不能作為唯一的符合條件。 必須選取一或多個其他符合條件。

![設定帳戶設定](images/b2b-configuring-account-settings.png)

若要進一步瞭解銷售線索與帳戶的比對，請參閱Real-Time CDP B2B概觀中的[銷售線索與帳戶的比對](../../rtcdp/b2b-ai-ml-services/lead-to-account-matching.md)。

## 瀏覽帳戶設定檔 {#browse-account-profiles}

若要瀏覽帳戶設定檔，請在左側導覽中選取[!UICONTROL 帳戶]下的&#x200B;**[!UICONTROL 設定檔]**。

在&#x200B;**[!UICONTROL 瀏覽]**&#x200B;標籤上，您可以使用連線企業來源的帳戶ID或直接輸入來源詳細資訊，來探索帳戶設定檔。

![使用帳戶ID來探索設定檔](images/b2b-account-browse-by.png)

### 依[!UICONTROL 連線的企業來源]瀏覽 {#browse-by-connected-enterprise-source}

若要依連線的企業來源瀏覽帳戶設定檔，請從&#x200B;**[!UICONTROL 瀏覽方式]**&#x200B;下拉式清單中選取&#x200B;**[!UICONTROL 連線的企業來源]**，然後使用&#x200B;**[!UICONTROL Source]**&#x200B;欄位旁的選擇器按鈕選擇連線的來源。

![依連線的企業來源瀏覽帳戶設定檔](images/b2b-account-browse.png)

這會開啟&#x200B;**[!UICONTROL 選取來源]**&#x200B;對話方塊，您可以在此根據貴組織建立的連線來選取來源。

>[!NOTE]
>
>貴組織可能為相同服務提供者設定了多個來源(例如Marketo)，因此請務必檢閱連線名稱、來源系統和來源系統例項，以確保您搜尋的來源例項正確無誤。

若要深入瞭解如何連線企業來源，請參閱[來源概觀](../sources/sources-overview.md)。

您可以選取連線名稱旁的選項按鈕來選擇來源，然後使用&#x200B;**[!UICONTROL 選取]**&#x200B;返回[!UICONTROL 瀏覽]標籤。

![選取來源工作流程](images/b2b-account-select-source.png)

選取來源後，您現在必須輸入與來源相關的&#x200B;**[!UICONTROL 帳戶ID]**。 例如，選取Salesforce來源會要求您從Salesforce執行個體輸入帳戶ID，以檢視與該ID相關聯的帳戶設定檔。

>[!NOTE]
>
>Marketo帳戶ID有兩個可能的帳戶表格可參照，因此您必須使用特定語法，才能確保您檢視的帳戶正確無誤。
>
>最常見的標準語法是Marketo帳戶ID，後面加上`.mkto_org` （例如`1234567.mkto_org`）。 Marketo Account-Based Marketing客戶可能有其他值，您可使用`.mkto_account`附加的Marketo帳戶ID來找到這些值。 如果您不確定要使用哪個語法，請洽詢您的Marketo管理員。

![帳戶ID選擇](images/b2b-account-browse-id.png)

### 由[!UICONTROL 其他]瀏覽 {#browse-by-others}

Real-Time CDP、B2B edition可讓您為想要檢視的帳戶輸入&#x200B;**[!UICONTROL Source名稱]**、**[!UICONTROL Source執行個體]**&#x200B;和&#x200B;**[!UICONTROL 帳戶ID]**，以支援執行直接查詢。 直接輸入來源名稱和例項即可提供Experience Platform搜尋和顯示正確帳戶設定檔資料所需的內容。

在無法直接連線至資料的來源情況下，執行直接查閱的功能相當實用。 例如，如果貴組織有防止直接連線至CRM的資料治理政策，您可以將該資料匯出至雲端儲存系統，然後將其擷取至Experience Platform。

另一個範例可能是您正在對離開系統並進入Experience Platform的資料執行轉換。 您可以使用直接查詢功能來提供資料的內容(例如，指定為Marketo資料，儘管資料來自Amazon S3儲存貯體)，讓系統知道要尋找的位置，以及如何正確呈現資料。

若要開始直接查詢，請從&#x200B;**[!UICONTROL 瀏覽者]**&#x200B;下拉式清單中選取&#x200B;**[!UICONTROL 其他]**，然後為您要檢視的帳戶輸入&#x200B;**[!UICONTROL Source名稱]**、**[!UICONTROL Source執行個體]**&#x200B;以及&#x200B;**[!UICONTROL 帳戶ID]**。

![由其他人瀏覽](images/b2b-account-browse-adhoc.png)

## 檢視帳戶設定檔詳細資料 {#view-account-profile-details}

使用&#x200B;**[!UICONTROL 瀏覽]**&#x200B;標籤尋找帳戶設定檔之後，選取&#x200B;**[!UICONTROL 設定檔識別碼]**&#x200B;會開啟帳戶設定檔的&#x200B;**[!UICONTROL 詳細資料]**&#x200B;標籤。 **[!UICONTROL 詳細資料]**&#x200B;標籤上顯示的設定檔資訊已從多個設定檔片段合併在一起，以形成個別帳戶的單一檢視。 這包括基本屬性和社群媒體資料等帳戶細節。

顯示的預設欄位也可以在組織層級變更，以顯示慣用的帳戶設定檔屬性。

>[!NOTE]
>
>類似的功能適用於客戶設定檔，而且已建立逐步指南，其中包含新增和移除屬性、調整面板大小等指示。 請閱讀[設定檔詳細資料自訂指南](../../profile/ui/profile-customization.md)以瞭解更多資訊。

![檢視帳戶設定檔詳細資料](images/b2b-account-details.png)

您可以選取另一個可用索引標籤，以檢視與帳戶相關的其他詳細資料。 這些標籤包括屬性、人員以及商機標籤，可顯示與整個企業系統中的帳戶相關的未結與已結商機。 請參閱下列各節，瞭解各標籤的詳細資訊。

## 屬性標籤 {#attributes-tab}

**[!UICONTROL 屬性]**&#x200B;索引標籤會列出與帳戶相關的所有記錄資訊。 這包括來自多個來源的屬性資料，這些資料已合併在一起，以形成帳戶的單一檢視。

除了能夠檢視清單中的資料之外，您還可以使用搜尋列搜尋特定屬性，或以JSON檢視記錄資料。

![屬性標籤](images/b2b-account-attributes.png)

## 「人員」索引標籤 {#people-tab}

**[!UICONTROL 人員]**&#x200B;索引標籤提供與帳戶關聯的個人人員清單。 這些人員可能是來自不同企業系統、由組織內不同團隊管理的聯絡人和銷售機會，但在Real-Time CDPB2B edition中，他們以單一清單的形式呈現，可讓您檢視帳戶聯絡人的整體檢視。

>[!NOTE]
>
>[!UICONTROL 人員]索引標籤會顯示與該帳戶相關聯的最多25人清單。 若帳戶擁有超過25個關聯人員，則系統顯示25筆記錄的隨機抽樣。

除了顯示連絡人資訊的快照之外，列出的每個人員也包含&#x200B;**[!UICONTROL 設定檔ID]**，這是一個可點按的連結，可讓您探索該個人的即時客戶設定檔。 若要進一步瞭解如何檢視與您的帳戶相關的個別客戶設定檔，請瀏覽指南，以在B2B edition的Real-Time CDP中瀏覽設定檔[](../profile/profile-browse.md)。

![人員索引標籤](images/b2b-account-people.png)

## 機會標籤 {#opportunities-tab}

**[!UICONTROL 商機]**&#x200B;索引標籤提供與帳戶相關的未結與已結商機的資訊。 這些機會可能會從多個來源擷取至Experience Platform，不過Real-Time CDP讓B2B edition行銷人員可以輕鬆地在一個位置一起看到所有這些機會。

>[!NOTE]
>
>[!UICONTROL 商機]索引標籤會顯示與帳戶相關聯之商機的清單，最多可達25個。 若客戶擁有超過25個相關商機，系統會顯示隨機抽樣，共25筆記錄。

每個商機都包含商機的名稱、數量、階段，以及商機是否開啟、關閉、成功或失敗等資訊。

![帳戶機會標籤](images/b2b-account-opportunities.png)

## 「相關帳戶」標籤 {#related-accounts-tab}

**[!UICONTROL 相關帳戶]**&#x200B;索引標籤提供與您瀏覽的帳戶相關的其他帳戶資訊。 如需功能的深入資訊，請閱讀[相關帳戶概述](/help/rtcdp/b2b-ai-ml-services/related-accounts.md)。

>[!NOTE]
>
>* 「相關」帳戶群組最多可以有30個帳戶設定檔。 如果發現超過30個帳戶設定檔相關，則會任意將其分割成多個群組，每個群組的成員不超過30個。 帳戶設定檔的「相關帳戶」群組一律包含自身。
>* [!UICONTROL 相關帳戶]索引標籤目前會顯示與您瀏覽的帳戶相關聯的相關帳戶清單，最多可包含25個相關帳戶。 此限制將在未來的更新中解決。 儘管有此UI限制，當您在區段定義中使用相關帳戶時，對於30個相關帳戶設定檔的群組，所有設定檔都用於定位。

每個相關帳戶都包含帳戶設定檔ID和名稱、帳戶來源金鑰等資訊，以及與首頁、地址、父帳戶、電話、產業和年度收入相關的進一步資訊。

![相關帳戶標籤](images/b2b-account-related-accounts.png)

您可以使用此清單中的相關帳戶進行細分。 請參閱[區段範例](/help/rtcdp/segmentation/b2b.md#related-account)以瞭解如何使用相關帳戶來擴大您在區段定義中的觸及範圍。