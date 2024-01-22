---
title: Snap Inc連線
description: 瞭解如何連線至Snapchat Ads平台以及從Experience Platform匯出您的對象。
exl-id: 1f0f2dc0-5f3d-424b-9b22-b1a14ac30039
source-git-commit: c3ef732ee82f6c0d56e89e421da0efc4fbea2c17
workflow-type: tm+mt
source-wordcount: '1012'
ht-degree: 2%

---

# Snap Inc連線

## 概觀 {#overview}

[Snapchat廣告](https://forbusiness.snapchat.com/) 適合所有企業，無論規模或產業為何。 全熒幕數位廣告可激發對您業務最重要的人員採取行動，成為Snapchaters日常對話的一部分。

>[!IMPORTANT]
>
>此目的地聯結器和檔案頁面是由 *Snap Inc* 團隊。 如有任何查詢或更新要求，請直接聯絡他們： *dev-support@snap.com*

## 使用案例 {#use-cases}

此目的地可讓行銷人員將Experience Platform中建立的使用者對象匯入至Snapchat廣告，並使用這些對象來鎖定其廣告。

## 先決條件 {#prerequisites}

若要使用此目的地，您必須有Snapchat Ads帳戶。 請參閱本檔案以瞭解如何建立虛擬報表套裝：

[開始使用Snapchat廣告](https://businesshelp.snapchat.com/s/article/overview?language=en_US)

## 限制 {#limitations}

* Snap Inc不支援特定對象區段的多個身分。 啟用區段時，請僅對應一個身分。
* Snap Inc不支援重新命名區段。 若要重新命名區段，您必須先停用、重新命名，然後再加以啟用。
* 無法定義對象區段成員的保留期間。 所有成員都有期限保留期，在被移除之前都會留在受眾中。

## 支援的身分 {#supported-identities}

此 *Snap Inc* 目的地支援下表所述的身分啟用。 進一步瞭解 [身分](/help/identity-service/namespaces.md).

所有傳送至的識別碼 *Snap Inc* 目的地必須以SHA-256格式進行雜湊處理。 若要在傳送純文字識別碼到目的地之前進行雜湊處理，請檢查 **[!UICONTROL 套用轉換]** 對應目的地目標識別碼時的選項。

>[!WARNING]
> 
> Snap Inc目的地不會接受未雜湊的識別碼，傳送這些識別碼可能會導致錯誤。


>[!IMPORTANT]
> 
> Snap Inc目的地不支援多個身分。 請僅選取一個身分。

| 目標身分 | 說明 | 考量事項 |
|---|---|---|
| Email Address | SHA-256雜湊電子郵件地址 | 將電子郵件地址對應到目標身分欄位 *電子郵件地址*. |
| 電話號碼 | SHA-256雜湊電話號碼 | 將電子郵件地址對應到目標身分欄位 *phonenumber*. |
| GAID | SHA-256雜湊的Google廣告ID | 將Google Advertising ID對應至目標身分欄位 *gaid*. |
| IDFA | SHA-256雜湊的Apple廣告ID | 將Apple Advertising ID對應至目標身分欄位 *idfa*. |

{style="table-layout:auto"}

## 匯出型別和頻率 {#export-type-frequency}

請參閱下表以取得目的地匯出型別和頻率的資訊。

| 項目 | 類型 | 附註 |
---------|----------|---------|
| 匯出型別 | **[!UICONTROL 對象匯出]** | 您正在匯出某個對象的所有成員，而這些成員中都有用於的識別碼（名稱、電話號碼或其他）。 *您的目的地* 目的地。 |
| 匯出頻率 | **[!UICONTROL 串流]** | 串流目的地是「一律開啟」的API型連線。 一旦根據對象評估在Experience Platform中更新了設定檔，聯結器就會將更新傳送至下游的目的地平台。 深入瞭解 [串流目的地](/help/destinations/destination-types.md#streaming-destinations). |

{style="table-layout:auto"}

## 正在連線到Snap Inc {#connect}

>[!IMPORTANT]
> 
>若要連線到目的地，您需要 **[!UICONTROL 檢視目的地]** 和 **[!UICONTROL 管理目的地]** [存取控制許可權](/help/access-control/home.md#permissions). 閱讀 [存取控制總覽](/help/access-control/ui/overview.md) 或聯絡您的產品管理員以取得必要許可權。

### 驗證目標 {#authenticate}

若要驗證目的地，請遵循下列步驟：

1. 尋找 *Snap Inc* 從Adobe Experience Platform的目的地目錄中選取目的地，然後選取 **設定**.
2. 選取 **[!UICONTROL 連線到目的地]**. 系統會將您重新導向至下列畫面：
   ![驗證畫面1](/help/destinations/assets/catalog/advertising/snapchat-ads/auth1.png)
3. 輸入您的Snapchat認證，然後選取 **登入**.
4. 您將會看到Adobe Experience Platform將能夠存取的Snapchat資料。 選取 **繼續** 以繼續進行連線程式。

![驗證畫面2](/help/destinations/assets/catalog/advertising/snapchat-ads/auth2.png)

選取「繼續」後，請等候系統重新將您導向Adobe Experience Platform。

### 填寫目標詳細資訊 {#destination-details}

![目的地詳細資料](/help/destinations/assets/catalog/advertising/snapchat-ads/destinationdetails.png)

若要設定目的地的詳細資訊，請填寫必填欄位並選取 **[!UICONTROL 下一個]**.

* **[!UICONTROL 名稱]**：您日後可辨識此目的地的名稱。
* **[!UICONTROL 說明]**：可協助您日後識別此目的地的說明。
* **[!UICONTROL 帳戶ID]**：與您要匯入對象之廣告帳戶相關聯的廣告帳戶ID。 如需如何找到此標籤的詳細資訊，請參閱 [此檔案位於Snapchat商務說明中心](https://businesshelp.snapchat.com/s/article/biz-acct-id?language=en_US).

>[!IMPORTANT]
> 
>輸入不正確或無效的Snapchat廣告帳戶ID將導致對象啟用失敗。 請再次確認您輸入的廣告帳戶ID是否正確。

### 啟用警示 {#enable-alerts}

您可以啟用警報以接收有關傳送到您目的地的資料流狀態的通知。 從清單中選取警報以訂閱接收有關資料流狀態的通知。 如需警示的詳細資訊，請參閱以下指南： [使用UI訂閱目的地警報](../../ui/alerts.md).

當您完成提供目的地連線的詳細資訊時，請選取「 」 **[!UICONTROL 下一個]**.

## 啟動此目標的對象 {#activate}

>[!IMPORTANT]
> 
>* 若要啟用資料，您需要 **[!UICONTROL 檢視目的地]**， **[!UICONTROL 啟用目的地]**， **[!UICONTROL 檢視設定檔]**、和 **[!UICONTROL 檢視區段]** [存取控制許可權](/help/access-control/home.md#permissions). 閱讀 [存取控制總覽](/help/access-control/ui/overview.md) 或聯絡您的產品管理員以取得必要許可權。
>* 要匯出 *身分*，您需要 **[!UICONTROL 檢視身分圖表]** [存取控制許可權](/help/access-control/home.md#permissions). <br> ![選取工作流程中反白顯示的身分名稱空間，以將對象啟用至目的地。](/help/destinations/assets/overview/export-identities-to-destination.png "選取工作流程中反白顯示的身分名稱空間，以將對象啟用至目的地。"){width="100" zoomable="yes"}

讀取 [將設定檔和受眾啟用至串流受眾匯出目標](/help/destinations/ui/activate-segment-streaming-destinations.md) 以取得啟用此目的地對象的指示。

## 驗證資料匯出 {#exported-data}

將對象啟用至 *Snap Inc* 目的地，您將能夠在「快照廣告管理員」的 [**受眾** 區段](https://businesshelp.snapchat.com/s/article/audience-sharing). 若要導覽至本區段，請依照下列步驟進行：

1. 登入 [貼齊廣告管理員](https://ads.snapchat.com/)
2. 選取 **受眾** 從畫面左上角的下拉式功能表。 您會在對象資料庫中看到您在Adobe Experience Platform中啟用的對象：

![對象](/help/destinations/assets/catalog/advertising/snapchat-ads/audiences.png)

請注意，當Adobe對象首次啟動至Snap Inc時，您一開始會將其視為空白對象。 這是因為Adobe Experience Platform在評估對象之前，不會將成員資料匯出到Snap Inc。 如需如何在Experience Platform中評估對象的詳細資訊，請參閱 [Segmentation Service概述](https://experienceleague.adobe.com/docs/experience-platform/segmentation/home.html#evaluate-segments).

## 資料使用與控管 {#data-usage-governance}

全部 [!DNL Adobe Experience Platform] 處理您的資料時，目的地符合資料使用原則。 如需如何操作的詳細資訊 [!DNL Adobe Experience Platform] 強制執行資料控管，請參閱 [資料控管概觀](/help/data-governance/home.md).
