---
keywords: linkedin連線；linkedin連線；linkedin目的地；linkedin；
title: Linkedin相符受眾連線
description: 根據雜湊電子郵件，為您的LinkedIn行銷活動啟用設定檔，以用於對象目標定位、個人化和隱藏。
exl-id: 74c233e9-161a-4e4a-98ef-038a031feff0
source-git-commit: 1b507e9846a74b7ac2d046c89fd7c27a818035ba
workflow-type: tm+mt
source-wordcount: '1202'
ht-degree: 3%

---

# [!DNL LinkedIn Matched Audiences] 連線

## 概觀 {#overview}

根據雜湊電子郵件和行動ID，為您的[!DNL LinkedIn]行銷活動啟用設定檔，以用於對象目標定位、個人化和隱藏。

Adobe Experience Platform UI中的![LinkedIn目的地](../../assets/catalog/social/linkedin/catalog.png)

## 使用案例

為協助您更清楚瞭解如何使用[!DNL LinkedIn Matched Audiences]目的地，以下是Adobe Experience Platform客戶可使用此功能解決的使用案例。

軟體公司會組織會議並想要與參與者保持聯絡，並根據其會議出席狀態向他們顯示個人化優惠。 公司可從自己的[!DNL CRM]擷取電子郵件地址或行動裝置ID至Adobe Experience Platform。 接著，他們可以從自己的離線資料建立對象，並將這些對象傳送至[!DNL LinkedIn]社交平台，最佳化其廣告支出。

## 支援的身分 {#supported-identities}

[!DNL LinkedIn Matched Audiences]支援下表所述的身分啟用。 深入瞭解[身分](/help/identity-service/features/namespaces.md)。

>[!IMPORTANT]
>
>從2025年9月開始，您無法再將[!DNL IDFA]對應為目標身分，因為[!DNL IDFA]目的地不再支援[!DNL LinkedIn Matched Audiences]。 如需詳細資訊，請參閱[!DNL LinkedIn Matched Audiences]整合[檔案](https://learn.microsoft.com/en-us/linkedin/marketing/matched-audiences/create-and-manage-segment-users?view=li-lms-2025-07&tabs=http#idtypes)。 這項變更是因為LinkedIn的需求，與任何Experience Platform目的地服務升級無關。


| 目標身分 | 說明 | 考量事項 |
|---|---|---|
| GAID | GOOGLE ADVERTISING ID | 當您的來源身分是GAID名稱空間時，請選取此目標身分。 |
| email_lc_sha256 | 使用SHA256演演算法雜湊的電子郵件地址 | Adobe Experience Platform同時支援純文字和SHA256雜湊電子郵件地址。 請依照[ID符合需求](#id-matching-requirements-id-matching-requirements)區段中的指示操作，針對純文字和雜湊電子郵件分別使用適當的名稱空間。 當您的來源欄位包含未雜湊的屬性時，請核取&#x200B;**[!UICONTROL Apply transformation]**&#x200B;選項，讓[!DNL Experience Platform]在啟用時自動雜湊資料。 |

{style="table-layout:auto"}

## 支援的對象 {#supported-audiences}

本節說明您可以將哪些型別的對象匯出至此目的地。

| 對象來源 | 支援 | 說明 |
|---------|----------|----------|
| [!DNL Segmentation Service] | ✓ | 透過Experience Platform [細分服務](../../../segmentation/home.md)產生的對象。 |
| 自訂上傳 | ✓ | 對象[從CSV檔案匯入](../../../segmentation/ui/audience-portal.md#import-audience)至Experience Platform。 |

{style="table-layout:auto"}

## 匯出型別和頻率 {#export-type-frequency}

請參閱下表以取得目的地匯出型別和頻率的資訊。

| 項目 | 類型 | 附註 |
|---------|----------|---------|
| 匯出類型 | **[!UICONTROL Audience export]** | 您正在匯出具有[!DNL LinkedIn Matched Audiences]目的地中所使用識別碼（名稱、電話號碼及其他）之對象的所有成員。 |
| 匯出頻率 | **[!UICONTROL Streaming]** | 串流目的地是「一律開啟」的API型連線。 根據對象評估在Experience Platform中更新設定檔後，聯結器會立即將更新傳送至下游的目標平台。 深入瞭解[串流目的地](/help/destinations/destination-types.md#streaming-destinations)。 |

{style="table-layout:auto"}

## LinkedIn帳戶必要條件 {#LinkedIn-account-prerequisites}

使用[!UICONTROL LinkedIn Matched Audience]目的地之前，請先確定您的[!DNL LinkedIn Campaign Manager]帳戶具有[!DNL Creative Manager]或更高的許可權等級。

若要瞭解如何編輯您的[!DNL LinkedIn Campaign Manager]使用者許可權，請參閱LinkedIn檔案中的[新增、編輯及移除Advertising帳戶的使用者許可權](https://www.linkedin.com/help/lms/answer/5753)。

## ID比對要求 {#id-matching-requirements}

[!DNL LinkedIn Matched Audiences]要求未明確傳送任何個人識別資訊(PII)。 因此，啟用至[!DNL LinkedIn Matched Audiences]的對象可以從&#x200B;*雜湊*&#x200B;識別碼中中斷連線，例如電子郵件地址或行動裝置ID。

根據您擷取至Adobe Experience Platform的ID型別，您必須遵守其對應的要求。

## 電子郵件雜湊需求 {#email-hashing-requirements}

您可以將電子郵件地址雜湊後再擷取至Adobe Experience Platform，或在Experience Platform中清楚使用電子郵件地址，並在啟用時將[!DNL Experience Platform]個電子郵件地址雜湊。

若要瞭解如何在Experience Platform中擷取電子郵件地址，請參閱[批次擷取總覽](/help/ingestion/batch-ingestion/overview.md)和[串流擷取總覽](/help/ingestion/streaming-ingestion/overview.md)。

如果您選擇自行雜湊電子郵件地址，請務必遵守下列要求：

* 修剪電子郵件字串中所有開頭和結尾的空格。 例如： `johndoe@example.com`，而非`<space>johndoe@example.com<space>`；
* 雜湊電子郵件字串時，請務必雜湊小寫字串；
   * 範例： `example@email.com`，而非`EXAMPLE@EMAIL.COM`；
* 確認雜湊字串全部為小寫
   * 範例： `55e79200c1635b37ad31a378c39feb12f120f116625093a19bc32fff15041149`，而非`55E79200C1635B37AD31A378C39FEB12F120F116625093A19bC32FFF15041149`；
* 請勿對字串執行Salt處理。

>[!NOTE]
>
>來自未雜湊名稱空間的資料在啟用時由[!DNL Experience Platform]自動雜湊。
>&#x200B;> 屬性來源資料不會自動雜湊。
> 
> 在[身分對應](../../ui/activate-segment-streaming-destinations.md#mapping)步驟中，當您的來源欄位包含未雜湊的屬性時，請核取&#x200B;**[!UICONTROL Apply transformation]**&#x200B;選項，讓[!DNL Experience Platform]在啟用時自動雜湊資料。
> 
> **[!UICONTROL Apply transformation]**&#x200B;選項只有在您選取屬性做為來源欄位時才會顯示。 選擇名稱空間時不會顯示。

![身分對應轉換](../../assets/ui/activate-destinations/identity-mapping-transformation.png)

## 連線到目標 {#connect}

>[!IMPORTANT]
> 
>若要連線到目的地，您需要&#x200B;**[!UICONTROL View Destinations]**&#x200B;和&#x200B;**[!UICONTROL Manage Destinations]** [存取控制許可權](/help/access-control/home.md#permissions)。 閱讀[存取控制總覽](/help/access-control/ui/overview.md)或連絡您的產品管理員以取得必要的許可權。

若要連線到此目的地，請依照[目的地組態教學課程](../../ui/connect-destination.md)中所述的步驟進行。 在設定目標工作流程中，填寫以下兩個區段中列出的欄位。

以下影片也會示範設定[!DNL LinkedIn Matched Audiences]目的地及啟用對象的步驟。

>[!VIDEO](https://video.tv.adobe.com/v/332599/?quality=12&learn=on&captions=eng)

>[!NOTE]
>
>Experience Platform使用者介面經常更新，自從錄製此影片後，可能已經變更。 如需最新資訊，請參閱[目的地設定教學課程](../../ui/connect-destination.md)。

### 驗證目標 {#authenticate}

1. 在目的地目錄中尋找[!DNL LinkedIn Matched Audiences]目的地並選取&#x200B;**[!UICONTROL Set Up]**。
2. 選擇「**[!UICONTROL Connect to destination]**」。
   ![驗證LinkedIn](/help/destinations/assets/catalog/social/linkedin/authenticate-linkedin-destination.png)
3. 輸入您的LinkedIn認證並選取&#x200B;**登入**。

### 重新整理驗證認證 {#refresh-authentication-credentials}

LinkedIn權杖每60天過期。 您可以從&#x200B;**[!UICONTROL Account expiration date]**&#x200B;或&#x200B;**[[!UICONTROL Accounts]](../../ui/destinations-workspace.md#accounts)**&#x200B;索引標籤中的&#x200B;**[[!UICONTROL Browse]](../../ui/destinations-workspace.md#browse)**&#x200B;欄監視權杖到期日。

代號過期後，將資料匯出至目的地時即停止運作。 若要避免出現這種情況，請執行以下步驟來重新驗證：

1. 導覽至&#x200B;**[!UICONTROL Destinations]** > **[!UICONTROL Accounts]**
2. （選用）使用頁面上可用的篩選器，僅顯示LinkedIn帳戶。
   ![篩選以僅顯示LinkedIn帳戶](/help/destinations/assets/catalog/social/linkedin/refresh-oauth-filters.png)
3. 選取您要重新整理的帳戶，選取省略符號並選取&#x200B;**[!UICONTROL Edit details]**。
   ![選取[編輯詳細資料]控制項](/help/destinations/assets/catalog/social/linkedin/refresh-oauth-edit-details.png)
4. 在強制回應視窗中，選取&#x200B;**[!UICONTROL Reconnect OAuth]**&#x200B;並使用您的LinkedIn認證重新驗證。
   使用Reconnect OAuth選項的![模型視窗](/help/destinations/assets/catalog/social/linkedin/reconnect-oauth-control.png)

>[!SUCCESS]
> 
>您的驗證認證已更新，其到期時間已重設為60天。

### 填寫目標詳細資訊 {#destination-details}

>[!CONTEXTUALHELP]
>id="platform_destinations_connect_linkedin_accountid"
>title="帳戶 ID"
>abstract="您的 LinkedIn 行銷活動管理員帳戶 ID。您可以在您的 LinkedIn 行銷活動管理員帳戶中找到此 ID。"

若要設定目的地的詳細資訊，請填寫下方的必填和選用欄位。 UI中欄位旁的星號表示該欄位為必填欄位。

* **[!UICONTROL Name]**：您日後可辨識此目的地的名稱。
* **[!UICONTROL Description]**：可協助您日後識別此目的地的說明。
* **[!UICONTROL Account ID]**：您的[!DNL LinkedIn Campaign Manager Account ID]。 您可以在您的[!DNL LinkedIn Campaign Manager]帳戶中找到此ID。

### 啟用警示 {#enable-alerts}

您可以啟用警報以接收有關傳送到您目的地的資料流狀態的通知。 從清單中選取警報以訂閱接收有關資料流狀態的通知。 如需警示的詳細資訊，請參閱[使用UI訂閱目的地警示](../../ui/alerts.md)的指南。

當您完成提供目的地連線的詳細資訊時，請選取&#x200B;**[!UICONTROL Next]**。

## 啟動此目標的對象 {#activate}

>[!IMPORTANT]
> 
>* 若要啟用資料，您需要&#x200B;**[!UICONTROL View Destinations]**、**[!UICONTROL Activate Destinations]**、**[!UICONTROL View Profiles]**&#x200B;和&#x200B;**[!UICONTROL View Segments]** [存取控制許可權](/help/access-control/home.md#permissions)。 閱讀[存取控制總覽](/help/access-control/ui/overview.md)或連絡您的產品管理員以取得必要的許可權。
>* 若要匯出&#x200B;*身分*，您需要&#x200B;**[!UICONTROL View Identity Graph]** [存取控制許可權](/help/access-control/home.md#permissions)。<br> ![選取工作流程中反白的身分名稱空間，以啟用目的地的對象。](/help/destinations/assets/overview/export-identities-to-destination.png "選取工作流程中反白顯示的身分名稱空間，以啟用目的地的對象。"){width="100" zoomable="yes"}

如需啟用此目的地的對象的指示，請參閱[啟用串流對象匯出目的地的對象資料](../../ui/activate-segment-streaming-destinations.md)。

## 匯出的資料 {#exported-data}

成功啟用意味著[!DNL LinkedIn]自訂對象是以程式設計方式在[[!DNL LinkedIn Campaign Manager]](https://www.linkedin.com/campaignmanager/login)中建立。 當使用者符合或不符合啟用的受眾的資格時，會調整受眾成員資格。

>[!TIP]
>
>Adobe Experience Platform與[!DNL LinkedIn Matched Audiences]之間的整合支援歷史受眾回填。 當您對目的地啟用對象時，所有歷史對象資格都會傳送到[!DNL LinkedIn]。
