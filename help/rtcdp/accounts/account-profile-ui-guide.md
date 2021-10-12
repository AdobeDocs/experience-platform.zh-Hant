---
keywords: rtcdp設定檔；設定檔rtcdp;rtcdp身分；rtcdp合併原則；即時客戶設定檔
title: 帳戶設定檔UI指南
description: 透過使用帳戶設定檔，Real-time Customer Data Platform B2B Edition可讓您統一來自多個來源的帳戶資訊。 本指南提供與Adobe Experience Platform使用者介面中帳戶設定檔互動的詳細資訊。
exl-id: a05e8b84-026e-4482-a288-aa25b441bd69
source-git-commit: 5bd2afcc594d96878ee51af2e9e99d74b764009e
workflow-type: tm+mt
source-wordcount: '1191'
ht-degree: 0%

---

# 帳戶設定檔UI指南

>[!IMPORTANT]
>
>Real-time Customer Data Platform B2B版目前仍在測試中。 檔案和功能可能會有所變更。

>[!NOTE]
>
>帳戶設定檔僅供Real-time Customer Data Platform B2B Edition客戶使用。 若要深入了解即時CDP，包括每種許可證類型可用的功能，請從閱讀[Real-time CDP overview](../overview.md)開始。

帳戶設定檔可讓您統一來自多個來源的帳戶資訊。 帳戶的統一檢視會匯集來自許多行銷管道的資料，以及貴組織目前用來儲存客戶帳戶資訊的不同系統。 本檔案提供使用Adobe Experience Platform使用者介面(UI)中提供的即時CDP B2B Edition功能，與帳戶設定檔互動的指南。

## 瀏覽帳戶設定檔

若要瀏覽帳戶設定檔，請從左側導覽的[!UICONTROL Accounts]下選取&#x200B;**[!UICONTROL Profiles]**&#x200B;開始。

![](images/b2b-account-browse.png)

在&#x200B;**[!UICONTROL Browse]**&#x200B;標籤中，您可以使用來自所連接企業源的帳戶ID或直接輸入源詳細資訊來瀏覽帳戶配置檔案。

![](images/b2b-account-browse-by.png)

### 按[!UICONTROL 連接的企業源瀏覽]

要按連接的企業源瀏覽帳戶配置檔案，請從&#x200B;**[!UICONTROL Browse by]**&#x200B;下拉清單中選擇&#x200B;**[!UICONTROL Connected enterprise source]**，然後使用&#x200B;**[!UICONTROL Source]**&#x200B;欄位旁的選擇器按鈕選擇連接的源。

![](images/b2b-account-browse.png)

這將開啟&#x200B;**[!UICONTROL 選擇源]**&#x200B;對話框，您可以在其中根據組織已建立的連接選擇源。

>[!NOTE]
>
>貴組織可能為同一服務提供商(例如，Marketo)配置了多個源，因此，務必複查連接名稱、源系統和源系統實例，以確保按正確的源實例進行搜索。

要了解有關連接企業源的詳細資訊，請參閱[源概述](../sources/sources-overview.md)。

![](images/b2b-account-select-source.png)

通過選擇連接名稱旁的單選按鈕，然後使用&#x200B;**[!UICONTROL Select]**&#x200B;返回[!UICONTROL Browse]頁簽，可以選擇源。

在選擇源後，您現在必須輸入與源相關的&#x200B;**[!UICONTROL 帳戶ID]**。 例如，選擇Salesforce源將要求您從Salesforce實例中輸入帳戶ID，以便查看與該ID綁定的帳戶配置檔案。

>[!NOTE]
>
>對於Marketo帳戶ID，有兩個可能的帳戶表可供參考，因此您必須使用特定語法，以確保您檢視的是正確的帳戶。
>
>最常見的標準語法是`.mkto_org`附加的Marketo帳戶ID（例如`1234567.mkto_org`）。 Marketo帳戶型行銷客戶可能有其他值，可使用`.mkto_account`附加的Marketo帳戶ID找到。 如果您不確定要使用哪種語法，請洽詢您的Marketo管理員。

![](images/b2b-account-browse-id.png)

### 按[!UICONTROL Others]瀏覽

即時CDP B2B Edition支援執行直接查詢的功能，它允許您為要查看的帳戶輸入&#x200B;**[!UICONTROL 源名稱]**、**[!UICONTROL 源實例]**&#x200B;和&#x200B;**[!UICONTROL 帳戶ID]**。 通過直接輸入源名稱和實例，您可以提供Experience Platform搜索和顯示正確帳戶配置檔案資料所需的上下文。

在無法直接連線至資料的來源情況下，執行直接查閱的功能相當實用。 例如，如果貴組織已制定資料控管原則，防止直接連線至CRM，您可以將該資料匯出至雲端儲存系統，然後內嵌至Experience Platform。

另一個範例可能是，您在資料離開系統並進入Platform之間執行轉換。 您可以使用直接查詢功能來提供資料的內容(例如，指定該資料為Marketo資料，儘管事實上該資料來自Amazon S3儲存貯體)，讓系統知道要尋找的位置，以及如何正確轉譯資料。

若要開始直接查閱，請從&#x200B;**[!UICONTROL Browse by]**&#x200B;下拉式清單中選取&#x200B;**[!UICONTROL Others]**，然後針對您要檢視的帳戶輸入&#x200B;**[!UICONTROL Source name]**、**[!UICONTROL Source instance]**&#x200B;和&#x200B;**[!UICONTROL Account ID]**。

![](images/b2b-account-browse-adhoc.png)

## 查看帳戶配置檔案詳細資訊

使用&#x200B;**[!UICONTROL Browse]**&#x200B;標籤查找帳戶配置檔案後，選擇&#x200B;**[!UICONTROL Profile ID]**&#x200B;將開啟帳戶配置檔案的&#x200B;**[!UICONTROL Detail]**&#x200B;標籤。 顯示在&#x200B;**[!UICONTROL Detail]**&#x200B;標籤上的配置檔案資訊已從多個配置檔案片段合併到一起，以形成單個帳戶的單個視圖。 這包括基本屬性和社交媒體資料等帳戶詳細資訊。

您也可以在組織層級變更顯示的預設欄位，以顯示偏好的帳戶設定檔屬性。

>[!NOTE]
>
>客戶設定檔也有類似的功能，而且已建立逐步指南，內含新增和移除屬性、調整面板大小等指示。 請參閱[設定檔詳細資料自訂指南](../../profile/ui/profile-customization.md)以深入了解。

![](images/b2b-account-details.png)

您可以選取其他可用標籤，以檢視與帳戶相關的其他詳細資訊。 這些頁簽包括屬性、人員和機會頁簽，這些頁簽顯示與企業系統中的帳戶相關的未結和已結業務機會。 請參閱下列章節，以取得每個標籤的詳細資訊。

## 「屬性」索引標籤

**[!UICONTROL Attributes]**&#x200B;頁簽列出與帳戶相關的所有記錄資訊。 這包括來自多個來源的屬性資料，這些來源已合併在一起，以形成帳戶的單一檢視。

除了能夠檢視清單中的資料之外，您還可以使用搜尋列來搜尋特定屬性，或以JSON形式檢視記錄資料。

![](images/b2b-account-attributes.png)

## 人員標籤

**[!UICONTROL People]**&#x200B;索引標籤提供與帳戶相關聯的個別人員清單。 這些人員可能是來自您組織內不同團隊管理的不同企業系統的聯絡人和銷售線索，但在即時CDP B2B Edition中，他們會以單一清單的形式一起呈現，讓您更全面地了解客戶聯絡人。

>[!NOTE]
>
>[!UICONTROL People]索引標籤會顯示與帳戶相關聯的最多25人的清單。 對於擁有25個以上關聯人員的帳戶，系統會顯示25個記錄的隨機抽樣。

除了顯示聯繫人資訊的快照外，列出的每個人還包含&#x200B;**[!UICONTROL 配置檔案ID]**，該連結是可點擊的連結，允許您瀏覽該個人的即時客戶配置檔案。 若要進一步了解如何檢視與您帳戶相關的個別客戶設定檔，請參閱[在即時CDP, B2B Edition](../profile/profile-browse.md)中瀏覽設定檔的指南。

![](images/b2b-account-people.png)

## 「機會」頁簽

**[!UICONTROL Opportunity]**&#x200B;頁簽提供與帳戶相關的未結和已結業務機會的資訊。 這些機會可能會從多個來源Experience Platform，但即時CDP B2B Edition可讓行銷人員輕鬆在一個地方一起查看所有這些機會。

>[!NOTE]
>
>[!UICONTROL Opportunitys]頁簽顯示與帳戶關聯的多達25個機會的清單。 對於擁有25個以上關聯機會的帳戶，系統會顯示25條記錄的隨機抽樣。

每個機會都包括以下資訊：機會的名稱、其金額、階段，以及該機會是開啟、關閉、成功還是丟失。

![](images/b2b-account-opportunities.png)
