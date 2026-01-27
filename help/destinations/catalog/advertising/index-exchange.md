---
title: 索引交換
description: 連線至Index Exchange （索引）並啟用您的資料，以便在索引UI中建立的交易鎖定您的對象區段。
source-git-commit: 4ecd3b60a6b45a94285785049fd4dee99d7c9bdf
workflow-type: tm+mt
source-wordcount: '1083'
ht-degree: 2%

---


# [!DNL Index Exchange] {#index-exchange}

## 概觀 {#overview}

[!DNL Index]是全球廣告供應端平台，可協助媒體擁有者將其內容在各熒幕上的價值最大化。 憑藉超過20年的產業領導力，[!DNL Index]將全球各大品牌與頂級體驗製作者連結在一起，以提供高品質的消費者體驗。

使用此目的地聯結器可將受眾區段直接從Adobe Experience Platform匯出至[!DNL Index Exchange]的程式化廣告平台。

匯出後，這些受眾區段可用於鎖定媒體所有者、市集合作夥伴的交易，或市集廠商與發佈者和組織者共用的交易。

>[!IMPORTANT]
>
>目的地聯結器和檔案頁面是由[!DNL Index]團隊建立和維護的。 如有問題或更新要求，請直接在[technical_am_marketplace@indexexchange.com](mailto:technical_am_marketplace@indexexchange.com)聯絡他們。

## 使用案例 {#use-cases}

為協助您更清楚瞭解您應如何及何時使用[!DNL Index Exchange]目的地，以下是Experience Platform客戶可藉由使用此目的地解決的範例使用案例。

### 在行動、網頁和CTV平台上鎖定使用者 {#targeting-users}

想要從Experience Platform將對象傳送至[!DNL Index]，以使用大量識別碼來鎖定行動、Web和CTV平台上的使用者的媒體擁有者、市集合作夥伴或市集廠商。

### 在行動、網頁和CTV平台上鎖定特定內容 {#targeting-content}

想要從Experience Platform將對象傳送至[!DNL Index]，以使用特定URL、應用程式套件組合或內容ID在行動、Web和CTV平台中尋找特定內容的目標使用者的媒體擁有者、市集合作夥伴或市集廠商。

## 先決條件 {#prerequisites}

使用此目的地時，對象區段必須使用其他程式向[!DNL Index]註冊，然後才能出現在您的帳戶中。 請連絡您的[!DNL Index Exchange]帳戶代表以取得此程式的協助。

## 支援的身分 {#supported-identities}

[!DNL Index]支援下表所述的身分啟用。 深入瞭解[身分](/help/identity-service/features/namespaces.md)。

請注意，[!DNL Index Exchange]目的地每個上載僅支援一個身分型別。 設定目的地詳細資料時，您必須指定適當的識別碼型別（請參閱下面的[「填寫目的地詳細資料」](#destination-details)區段）。

若要上傳多個身分型別，請為每個身分型別分別建立[!DNL Index Exchange]目的地的執行個體。

| 目標身分 | 說明 | 考量事項 |
| --- | --- | --- |
| GAID | GOOGLE ADVERTISING ID | 如果來源身分是GAID名稱空間，請選取GAID作為目標身分。 |
| IDFA | 廣告商適用的Apple ID | 如果您的來源身分識別是IDFA名稱空間，請選取IDFA目標身分識別。 |
| Windows AID | Windows Advertising ID | 如果您的來源識別是Windows AID名稱空間，請選取Windows AID目標識別。 |
| extern_id | 自訂使用者ID | 如果您的來源身分是自訂名稱空間，請選取此目標身分。 |

{style="table-layout:auto"}

## 支援的對象 {#supported-audiences}

本節說明您可以將哪些對象型別匯出至此目的地。

| 對象來源 | 支援 | 說明 |
| --------- | ---------- | ---------- |
| [!DNL Segmentation Service] | ✓ | 透過Experience Platform [細分服務](../../../segmentation/home.md)產生的對象。 |
| 自訂上傳 | ✓ | 對象[從CSV檔案匯入](../../../segmentation/ui/overview.md#import-audience)至Experience Platform。 |

{style="table-layout:auto"}

## 匯出型別和頻率 {#export-type-frequency}

請參閱下表以取得目的地匯出型別和頻率的資訊。

| 項目 | 類型 | 附註 |
| --------- | ---------- | --------- | 
| 匯出類型 | **[!UICONTROL Segment export]** | 匯出區段（對象）的所有成員，其中包含用於[!DNL Index Exchange]目的地中的識別碼（IDFA、GAID或其他）。 |
| 匯出頻率 | **[!UICONTROL Batch]** | 以3、6、8、12或24小時的間隔將檔案匯出至下游平台。 深入瞭解[批次檔案型目的地](/help/destinations/destination-types.md#file-based)。 |

{style="table-layout:auto"}

## 連線到目標 {#connect}

>[!IMPORTANT]
> 
>若要連線到目的地，您需要&#x200B;**[!UICONTROL View Destinations]**&#x200B;和&#x200B;**[!UICONTROL Manage Destinations]** [存取控制許可權](/help/access-control/home.md#permissions)。 閱讀[存取控制總覽](/help/access-control/ui/overview.md)或連絡您的產品管理員以取得必要的許可權。

若要連線到此目的地，請依照[目的地組態教學課程](../../ui/connect-destination.md)中所述的步驟進行。 在設定目標工作流程中，填寫以下兩個區段中列出的欄位。

### 填寫目標詳細資料 {#destination-details}

若要設定目的地的詳細資料，請填寫下列欄位。 UI中欄位旁的星號表示該欄位為必填欄位。

![目的地詳細資料](../../assets/catalog/advertising/index-exchange/destination-details.png)

* [!UICONTROL Name]：輸入名稱以協助您稍後辨識此目的地。
* [!UICONTROL Description]：輸入說明以協助您稍後識別此目的地。
* [!UICONTROL Identifier Type]：選取索引提供的識別碼型別，以符合您要傳送給[!DNL Index]的識別碼。 請參閱下表列出支援的識別碼型別。 如果您不確定要使用哪個識別碼型別，請連絡您的[!DNL Index]代表。 若要傳送多個識別碼型別，請為此目的地建立個別的執行個體。
* [!UICONTROL Account ID]：輸入您的[!DNL Index]帳戶識別碼。 這與您的發佈者ID不同。 如果您不確定要使用哪個ID，請聯絡您的[!DNL Index]代表。

#### 支援的識別碼型別

| 識別碼型別 | 說明 |
|------------------ | ------------- |
| [!DNL appbundle] | 行動應用程式套件組合 |
| [!DNL contentid] | 內容ID |
| [!DNL deviceid] | 裝置ID (如 IDFA、GAID、WAID等) |
| [!DNL ip] | IP位址 |
| [!DNL postcode] | 郵遞區號 |
| [!DNL url] | 網站URL |
| [!DNL ppid_xxx] | 如需PPID識別碼，請聯絡您的[!DNL Index Exchange]帳戶代表以尋求協助。 |

{style="table-layout:auto"}

### 啟用警示 {#enable-alerts}

您可以啟用警示以接收有關您資料流到此目的地的狀態通知。 從清單中選取一或多個警報，以訂閱資料流的狀態通知。 如需詳細資訊，請參閱[使用UI訂閱目的地警示指南](../../ui/alerts.md)。
當您完成提供目的地連線的詳細資訊時，請選取**[!UICONTROL Next]**。

## 啟用此目的地的區段 {#activate}

>[!IMPORTANT]
> 
>* 若要啟用資料，您需要&#x200B;**[!UICONTROL View Destinations]**、**[!UICONTROL Activate Destinations]**、**[!UICONTROL View Profiles]**&#x200B;和&#x200B;**[!UICONTROL View Segments]** [存取控制許可權](/help/access-control/home.md#permissions)。 閱讀[存取控制總覽](/help/access-control/ui/overview.md)或連絡您的產品管理員以取得必要的許可權。
>* 若要匯出&#x200B;*身分*，您需要&#x200B;**[!UICONTROL View Identity Graph]** [存取控制許可權](/help/access-control/home.md#permissions)。<br> ![選取工作流程中反白的身分名稱空間，以啟用目的地的對象。](/help/destinations/assets/overview/export-identities-to-destination.png "選取工作流程中反白顯示的身分名稱空間，以啟用目的地的對象。"){width="100" zoomable="yes"}

讀取[啟用批次設定檔匯出目的地的對象資料](/help/destinations/ui/activate-batch-profile-destinations.md)，以取得啟用此目的地的對象區段的指示。

### 對應屬性和身分 {#map}

選取來源欄位：

* 選取識別碼（通常是IDFA或自訂ID名稱空間等名稱空間）。 這必須對應於設定目的地時選取的「識別碼型別」。 例如，使用IDFA識別碼做為來源欄位時，目的地必須已設定為「deviceid」識別碼型別。

選取目標欄位：

* 目標欄位的名稱會忽略且不重要。 目的地只關心要傳送的識別碼型別，這是由設定目的地時選取的識別碼型別所決定。

![對應屬性和身分](../../assets/catalog/advertising/index-exchange/identity-mapping.png)

### 向[!DNL Index]註冊區段 {#register-segments}

在將資料啟用至目的地之前或之後，請聯絡您的[!DNL Index]代表以註冊您計畫啟用的區段。 您的代表會提供如何註冊其他區段詳細資料的指示，包括名稱、ID、說明和定價（如適用）。

## 匯出的資料/驗證資料匯出 {#exported-data}

註冊完成後，區段將可在您的[!DNL Index]帳戶中定位。 若要確認資料正確接收，請連絡您的[!DNL Index]代表，他可提供所接收區段資料量的詳細資訊。

## 資料使用與控管 {#data-usage-governance}

處理您的資料時，所有Experience Platform目的地都符合資料使用原則。 如需Experience Platform如何強制資料控管的詳細資訊，請閱讀[資料控管概觀](/help/data-governance/home.md)。
