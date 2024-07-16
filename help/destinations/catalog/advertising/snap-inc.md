---
title: Snap Inc連線
description: 瞭解如何連線至Snapchat Ads平台以及從Experience Platform匯出您的對象。
exl-id: 1f0f2dc0-5f3d-424b-9b22-b1a14ac30039
source-git-commit: ba39f62cd77acedb7bfc0081dbb5f59906c9b287
workflow-type: tm+mt
source-wordcount: '1012'
ht-degree: 2%

---

# Snap Inc連線

## 概觀 {#overview}

[Snapchat廣告](https://forbusiness.snapchat.com/)是為每個企業製作的，無論規模或產業為何。 全熒幕數位廣告可激發對您業務最重要的人員採取行動，成為Snapchaters日常對話的一部分。

>[!IMPORTANT]
>
>此目的地聯結器和檔案頁面是由&#x200B;*Snap Inc*&#x200B;團隊建立和維護。 若有任何查詢或更新要求，請直接透過&#x200B;*dev-support@snap.com*&#x200B;聯絡他們

## 使用案例 {#use-cases}

此目的地可讓行銷人員將Experience Platform中建立的使用者對象匯入至Snapchat廣告，並使用這些對象來鎖定其廣告。

## 先決條件 {#prerequisites}

若要使用此目的地，您必須有Snapchat Ads帳戶。 請參閱本檔案以瞭解如何建立虛擬報表套裝：

[開始使用Snapchat Advertising](https://businesshelp.snapchat.com/s/article/overview?language=en_US)

## 限制 {#limitations}

* Snap Inc不支援特定對象區段的多個身分。 啟用區段時，請僅對應一個身分。
* Snap Inc不支援重新命名區段。 若要重新命名區段，您必須先停用、重新命名，然後再加以啟用。
* 無法定義對象區段成員的保留期間。 所有成員都有期限保留期，在被移除之前都會留在受眾中。

## 支援的身分 {#supported-identities}

*Snap Inc*&#x200B;目的地支援啟用下表所述的身分。 深入瞭解[身分](/help/identity-service/features/namespaces.md)。

所有傳送至&#x200B;*Snap Inc*&#x200B;目的地的識別碼都必須以SHA-256格式進行雜湊處理。 若要在傳送純文字識別碼到目的地之前先進行雜湊處理，請在對應目的地的目標識別碼時勾選&#x200B;**[!UICONTROL 套用轉換]**&#x200B;選項。

>[!WARNING]
> 
> Snap Inc目的地不會接受未雜湊的識別碼，傳送這些識別碼可能會導致錯誤。


>[!IMPORTANT]
> 
> Snap Inc目的地不支援多個身分。 請僅選取一個身分。

| 目標身分 | 說明 | 考量事項 |
|---|---|---|
| 電子郵件地址 | SHA-256雜湊電子郵件地址 | 將電子郵件地址對應到目標識別欄位&#x200B;*emailAddress*。 |
| 電話號碼 | SHA-256雜湊電話號碼 | 將電子郵件地址對應到目標識別欄位&#x200B;*phoneNumber*。 |
| GAID | SHA-256雜湊的Google Advertising ID | 將Google Advertising ID對應至目標身分欄位&#x200B;*gaid*。 |
| IDFA | SHA-256雜湊的Apple Advertising ID | 將Apple Advertising ID對應至目標身分欄位&#x200B;*idfa*。 |

{style="table-layout:auto"}

## 匯出型別和頻率 {#export-type-frequency}

請參閱下表以取得目的地匯出型別和頻率的資訊。

| 項目 | 類型 | 附註 |
---------|----------|---------|
| 匯出類型 | **[!UICONTROL 對象匯出]** | 您正在匯出具有&#x200B;*YOURDESTINATION*&#x200B;目的地中所使用之識別碼（名稱、電話號碼或其他）的對象的所有成員。 |
| 匯出頻率 | **[!UICONTROL 串流]** | 串流目的地是「一律開啟」的API型連線。 一旦根據對象評估在Experience Platform中更新了設定檔，聯結器就會將更新傳送至下游的目的地平台。 深入瞭解[串流目的地](/help/destinations/destination-types.md#streaming-destinations)。 |

{style="table-layout:auto"}

## 正在連線到Snap Inc {#connect}

>[!IMPORTANT]
> 
>若要連線到目的地，您需要&#x200B;**[!UICONTROL 檢視目的地]**&#x200B;和&#x200B;**[!UICONTROL 管理目的地]** [存取控制許可權](/help/access-control/home.md#permissions)。 閱讀[存取控制總覽](/help/access-control/ui/overview.md)或連絡您的產品管理員以取得必要的許可權。

### 驗證目標 {#authenticate}

若要驗證目的地，請遵循下列步驟：

1. 從Adobe Experience Platform的目的地目錄中尋找&#x200B;*Snap Inc*&#x200B;目的地，並選取&#x200B;**設定**。
2. 選取&#x200B;**[!UICONTROL 連線到目的地]**。 系統會將您重新導向至下列畫面：
   ![驗證畫面1](/help/destinations/assets/catalog/advertising/snapchat-ads/auth1.png)
3. 輸入您的Snapchat認證，並選取&#x200B;**登入**。
4. 您將會看到Adobe Experience Platform將能夠存取的Snapchat資料。 選取&#x200B;**繼續**&#x200B;以繼續連線程式。

![驗證畫面2](/help/destinations/assets/catalog/advertising/snapchat-ads/auth2.png)

選取「繼續」後，請等候系統重新將您導向Adobe Experience Platform。

### 填寫目標詳細資訊 {#destination-details}

![目的地詳細資料](/help/destinations/assets/catalog/advertising/snapchat-ads/destinationdetails.png)

若要設定目的地的詳細資料，請填寫必填欄位，然後選取&#x200B;**[!UICONTROL 下一步]**。

* **[!UICONTROL 名稱]**：您日後可辨識此目的地的名稱。
* **[!UICONTROL 描述]**：可協助您日後識別此目的地的描述。
* **[!UICONTROL 帳戶ID]**：與您要匯入對象之廣告帳戶相關聯的廣告帳戶ID。 如需如何尋找此專案的詳細資訊，請參閱Snapchat商務說明中心](https://businesshelp.snapchat.com/s/article/biz-acct-id?language=en_US)上的[本檔案。

>[!IMPORTANT]
> 
>輸入不正確或無效的Snapchat廣告帳戶ID將導致對象啟用失敗。 請再次確認您輸入的廣告帳戶ID是否正確。

### 啟用警示 {#enable-alerts}

您可以啟用警報以接收有關傳送到您目的地的資料流狀態的通知。 從清單中選取警報以訂閱接收有關資料流狀態的通知。 如需警示的詳細資訊，請參閱[使用UI訂閱目的地警示](../../ui/alerts.md)的指南。

當您完成提供目的地連線的詳細資訊後，請選取&#x200B;**[!UICONTROL 下一步]**。

## 啟動此目標的對象 {#activate}

>[!IMPORTANT]
> 
>* 若要啟用資料，您需要&#x200B;**[!UICONTROL 檢視目的地]**、**[!UICONTROL 啟用目的地]**、**[!UICONTROL 檢視設定檔]**&#x200B;和&#x200B;**[!UICONTROL 檢視區段]** [存取控制許可權](/help/access-control/home.md#permissions)。 閱讀[存取控制總覽](/help/access-control/ui/overview.md)或連絡您的產品管理員以取得必要的許可權。
>* 若要匯出&#x200B;*身分*，您需要&#x200B;**[!UICONTROL 檢視身分圖表]** [存取控制許可權](/help/access-control/home.md#permissions)。<br> ![選取工作流程中反白的身分名稱空間，以啟用目的地的對象。](/help/destinations/assets/overview/export-identities-to-destination.png "選取工作流程中反白顯示的身分名稱空間，以啟用目的地的對象。"){width="100" zoomable="yes"}

閱讀[將設定檔和對象啟用至串流對象匯出目的地](/help/destinations/ui/activate-segment-streaming-destinations.md)，以瞭解啟用此目的地對象的指示。

## 驗證資料匯出 {#exported-data}

啟用受眾至&#x200B;*Snap Inc*&#x200B;目的地後，您將可以在Snap Ads管理員的&#x200B;[**受眾**&#x200B;區段](https://businesshelp.snapchat.com/s/article/audience-sharing)中看到受眾。 若要導覽至本區段，請依照下列步驟進行：

1. 登入[快照廣告管理員](https://ads.snapchat.com/)
2. 從畫面左上角的下拉式功能表中選取&#x200B;**對象**。 您會在對象資料庫中看到您在Adobe Experience Platform中啟用的對象：

![對象](/help/destinations/assets/catalog/advertising/snapchat-ads/audiences.png)

請注意，當Adobe對象首次啟動至Snap Inc時，您一開始會將其視為空白對象。 這是因為Adobe Experience Platform在評估對象之前，不會將成員資料匯出到Snap Inc。 如需如何在Experience Platform中評估對象的詳細資訊，請參閱[分段服務總覽](https://experienceleague.adobe.com/docs/experience-platform/segmentation/home.html#evaluate-segments)。

## 資料使用與控管 {#data-usage-governance}

處理您的資料時，所有[!DNL Adobe Experience Platform]目的地都符合資料使用原則。 如需[!DNL Adobe Experience Platform]如何強制資料控管的詳細資訊，請參閱[資料控管概觀](/help/data-governance/home.md)。
