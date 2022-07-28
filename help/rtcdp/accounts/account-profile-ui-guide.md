---
keywords: rtcdp配置檔案；配置檔案rtcdp;rtcdp標識；rtcdp合併策略；即時客戶配置檔案
title: 帳戶配置檔案UI指南
description: 通過使用帳戶配置檔案，Real-time Customer Data PlatformB2B版使您能夠統一來自多個來源的帳戶資訊。 本指南提供了與Adobe Experience Platform用戶介面中的帳戶配置檔案交互的詳細資訊。
exl-id: a05e8b84-026e-4482-a288-aa25b441bd69
source-git-commit: e94753236623343dcd739ff65c18248c1112f361
workflow-type: tm+mt
source-wordcount: '1479'
ht-degree: 0%

---

# 帳戶配置檔案UI指南

>[!NOTE]
>
>客戶配置檔案僅對Real-time Customer Data PlatformB2B版客戶可用。 要瞭解有關即時CDP的更多資訊，包括每種許可證類型可用的功能和功能，請首先閱讀 [即時CDP概述](../overview.md)。

帳戶配置檔案使您能夠統一來自多個來源的帳戶資訊。 此帳戶的統一視圖將來自您許多市場營銷渠道和您的組織當前用於儲存客戶帳戶資訊的各種系統的資料匯集在一起。 本文檔提供了使用Adobe Experience Platform用戶介面(UI)中提供的即時CDP、B2B版功能與帳戶配置檔案交互的指南。

要瞭解有關如何作為B2B工作流的一部分建立帳戶配置檔案的詳細資訊，請參閱 [端到端教程](../b2b-tutorial.md)。

## 帳戶配置檔案概述 {#account-profiles-overview}

選擇 **[!UICONTROL 配置檔案]** 在 [!UICONTROL 帳戶] 在左側導航中查看帳戶配置檔案的概述。 在 [!UICONTROL 概述] 頁籤中，該面板顯示在單個入口點中顯示小部件的圖形或圖表。

![顯示小部件的概述頁籤](images/b2b-account-profile-overview.png)

請參閱[上的文檔[!UICONTROL 帳戶配置檔案]]((../../dashboards/guides/account-profiles.md)儀表板以瞭解詳細資訊。

## 瀏覽帳戶配置檔案 {#browse-account-profiles}

要瀏覽帳戶配置檔案，請首先選擇 **[!UICONTROL 配置檔案]** 在 [!UICONTROL 帳戶] 的上界。

![選擇左導航中的配置檔案](images/b2b-account-browse.png)

在 **[!UICONTROL 瀏覽]** 頁籤，您可以使用連接的企業來源的帳戶ID或直接輸入來源詳細資訊來瀏覽帳戶配置檔案。

![使用帳戶ID瀏覽配置檔案](images/b2b-account-browse-by.png)

### 瀏覽者 [!UICONTROL 連接的企業源] {#browse-by-connected-enterprise-source}

要按連接的企業源瀏覽帳戶配置檔案，請選擇 **[!UICONTROL 連接的企業源]** 從 **[!UICONTROL 瀏覽者]** 下拉清單，然後使用旁邊的選擇器按鈕選擇連接的源 **[!UICONTROL 源]** 的子菜單。

![按連接的企業源瀏覽帳戶配置檔案](images/b2b-account-browse.png)

開啟 **[!UICONTROL 選擇源]** 對話框，您可以在其中根據您的組織已建立的連接選擇源。

>[!NOTE]
>
>您的組織可能為同一服務提供商(例如Marketo)配置了多個源，因此，必須查看連接名稱、源系統和源系統實例，以確保您按正確的源實例進行搜索。

要瞭解有關連接企業源的詳細資訊，請參閱 [源概述](../sources/sources-overview.md)。

![選擇源工作流](images/b2b-account-select-source.png)

通過選擇連接名稱旁邊的單選按鈕，可以選擇源，然後使用 **[!UICONTROL 選擇]** 返回 [!UICONTROL 瀏覽] 頁籤。

在選定源後，您現在必須輸入 **[!UICONTROL 帳戶ID]** 與源相關。 例如，選擇Salesforce來源將要求您從Salesforce實例中輸入帳戶ID，以便查看綁定到該ID的帳戶配置檔案。

>[!NOTE]
>
>對於Marketo帳戶ID，有兩個可能的帳戶表可以被引用，因此您必須使用特定語法以確保查看正確的帳戶。
>
>最常見的標準語法是附加的Marketo帳戶ID `.mkto_org` (例如， `1234567.mkto_org`)。 MarketoAccount-Based Marketing客戶可能具有附加值，這些值可以使用附加的Marketo帳戶ID找到 `.mkto_account`。 如果您不確定要使用哪種語法，請與您的Marketo管理員聯繫。

![帳戶ID選擇](images/b2b-account-browse-id.png)

### 瀏覽者 [!UICONTROL 其他] {#browse-by-others}

即時CDP B2B Edition支援通過輸入 **[!UICONTROL 源名稱]**。 **[!UICONTROL 源實例]**, **[!UICONTROL 帳戶ID]** 您想查看的帳戶。 通過直接輸入源名稱和實例，您可以提供Experience Platform搜索和顯示正確的帳戶配置檔案資料所需的上下文。

在無法直接與資料建立源連接的情況下，執行直接查找的能力非常有用。 例如，如果您的組織已制定了阻止直接連接到CRM的資料治理策略，則可以將該資料導出到雲儲存系統，然後將其導入Experience Platform。

另一個示例可能是您正在對資料執行轉換，轉換時間為資料離開系統並進入平台之間。 您可以使用直接查找功能為資料提供上下文(例如，指定資料是Marketo資料，儘管它來自AmazonS3儲存桶)，以便系統知道查找位置以及如何正確呈現資料。

要開始直接查找，請選擇 **[!UICONTROL 其他]** 從 **[!UICONTROL 瀏覽者]** 下拉清單，然後輸入 **[!UICONTROL 源名稱]**。 **[!UICONTROL 源實例]**, **[!UICONTROL 帳戶ID]** 您想查看的帳戶。

![其他人瀏覽](images/b2b-account-browse-adhoc.png)

## 查看帳戶配置檔案詳細資訊 {#view-account-profile-details}

使用 **[!UICONTROL 瀏覽]** 頁籤，選擇 **[!UICONTROL 配置檔案ID]** 開啟 **[!UICONTROL 詳細資訊]** 頁籤。 顯示在 **[!UICONTROL 詳細資訊]** 已從多個配置檔案片段合併到一起，以形成單個帳戶的單個視圖。 這包括基本屬性和社交媒體資料等帳戶詳細資訊。

在組織層也可以更改顯示的預設欄位以顯示首選帳戶配置檔案屬性。

>[!NOTE]
>
>客戶配置檔案也提供類似功能，並且已建立了分步指南，其中包含添加和刪除屬性、調整面板大小等說明。 請閱讀 [配置檔案詳細資訊定制指南](../../profile/ui/profile-customization.md) 來瞭解更多資訊。

![查看帳戶配置檔案詳細資訊](images/b2b-account-details.png)

通過選擇另一個可用頁籤，您可以查看與帳戶相關的附加詳細資訊。 這些標籤包括屬性、人員和機會標籤，這些標籤顯示了與整個企業系統的帳戶相關的開啟和關閉的機會。 有關每個頁籤的詳細資訊，請參閱以下各節。

## 「屬性」頁籤 {#attributes-tab}

的 **[!UICONTROL 屬性]** 頁籤列出與帳戶相關的所有記錄資訊。 這包括來自多個源的屬性資料，這些源已合併在一起，以形成帳戶的單個視圖。

除了能夠查看清單中的資料外，您還可以使用搜索欄搜索特定屬性或以JSON形式查看記錄資料。

![「屬性」頁籤](images/b2b-account-attributes.png)

## 「人員」頁籤 {#people-tab}

的 **[!UICONTROL 人物]** 頁籤提供與帳戶關聯的個人清單。 這些人員可能是組織內不同團隊管理的不同企業系統的聯繫人和主管，但在即時CDP和B2B版中，他們作為單個清單一起顯示，使您能夠看到客戶聯繫人的更全面的視圖。

>[!NOTE]
>
>的 [!UICONTROL 人物] 頁籤顯示與帳戶關聯的最多25人的清單。 對於擁有25名以上關聯人員的賬戶，系統會隨機抽樣25條記錄。

除向您顯示聯繫人資訊的快照外，列出的每個人還包括 **[!UICONTROL 配置檔案ID]**，此連結可按一下，允許您瀏覽該個人的即時客戶配置檔案。 要瞭解有關查看與您的帳戶相關的單個客戶配置檔案的詳細資訊，請訪問指南 [在即時CDP B2B版中瀏覽配置檔案](../profile/profile-browse.md)。

![「人員」頁籤](images/b2b-account-people.png)

## 機會頁籤 {#opportunities-tab}

的 **[!UICONTROL 機會]** 頁籤提供與帳戶相關的未結和已結業務機會的資訊。 這些機會可能會從多個來源被引入Experience Platform中，但即時CDP和B2B版本使營銷人員能夠輕鬆地在一個位置看到所有這些機會。

>[!NOTE]
>
>的 [!UICONTROL 機會] 頁籤顯示與帳戶關聯的最多25個機會的清單。 對於具有25個以上關聯機會的客戶，系統顯示25條記錄的隨機抽樣。

每個機會都包括諸如機會名稱、其金額、階段以及該機會是開啟、關閉、贏得還是丟失等資訊。

![「客戶機會」頁籤](images/b2b-account-opportunities.png)

## 「相關帳戶」頁籤 {#related-accounts-tab}

的 **[!UICONTROL 相關帳戶]** 頁籤提供有關可能與您正在瀏覽的帳戶相關的其他帳戶的資訊。 有關功能的詳細資訊，請閱讀 [相關帳戶概述](/help/rtcdp/b2b-ai-ml-services/related-accounts.md)。

>[!NOTE]
>
>* 相關帳戶組最多可以有30個帳戶配置檔案。 如果發現30個以上的帳戶配置檔案相關，則它們被任意拆分為多個組，每個組的成員不超過30個。 帳戶配置檔案的「相關帳戶」組始終包括其自身。
>* 的 [!UICONTROL 相關帳戶] 頁籤當前顯示與您正在瀏覽的帳戶關聯的最多25個相關帳戶的清單。 這是將來更新中要解決的限制。 儘管有此UI限制，但在段定義中使用相關帳戶時，對於30個相關帳戶配置檔案組，所有配置檔案都用於目標。


每個相關帳戶都包括諸如帳戶配置檔案ID和名稱、其帳戶源密鑰等資訊，以及與首頁、地址、父帳戶、電話、行業和年度收入相關的進一步資訊。

![「相關帳戶」頁籤](images/b2b-account-related-accounts.png)

您可以使用此清單中的相關帳戶進行細分。 查看 [分段示例](/help/rtcdp/segmentation/b2b.md#related-account) 瞭解如何使用相關帳戶來擴展您在段定義中的觸角。