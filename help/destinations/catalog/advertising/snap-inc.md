---
title: （測試版）Snap Inc連接
description: 了解如何連線至Snapchat Ads平台，並從Experience Platform中匯出您的受眾區段。
exl-id: 1f0f2dc0-5f3d-424b-9b22-b1a14ac30039
source-git-commit: 44e056407f5089c927752f00cc6bf173d7640b83
workflow-type: tm+mt
source-wordcount: '1006'
ht-degree: 1%

---

# （測試版）Snap Inc

## 總覽 {#overview}

[Snapchat Ads](https://forbusiness.snapchat.com/) 不管規模大小或行業如何，每家企業都能生產。 成為Snapchatters日常與全螢幕數字廣告對話的一部分，這些廣告能夠激勵那些對您的業務最重要的人採取行動。

>[!IMPORTANT]
>
>本檔案頁面由 *Snap Inc* 團隊。 這目前是測試版產品，功能可能會有所變更。 如有任何查詢或更新請求，請直接與他們聯繫，地址為 *dev-support@snap.com*

## 使用案例 {#use-cases}

此目的地可讓行銷人員將Experience Platform中建立的使用者區段匯入Snapchat Ads，並用於鎖定其廣告。

## 先決條件 {#prerequisites}

若要使用此目的地，您必須擁有Snapchat Ads帳戶。 請參閱本檔案，了解如何建立下列檔案：

[開始使用Snapchat廣告](https://businesshelp.snapchat.com/s/article/overview?language=en_US)

## 限制 {#limitations}

* Snap Inc不支援給定受眾段的多個身份。 啟用區段時，請僅對應一個身分。
* Snap Inc不支援更名段。 若要重新命名區段，您必須停用、重新命名，然後啟用。
* 無法定義對象區段成員的保留期。 所有成員都具有期限保留，並會在區段中，直到移除為止。

## 支援的身分 {#supported-identities}

此 *Snap Inc* 目的地支援啟用下表所述的身分。 深入了解 [身分](/help/identity-service/namespaces.md).

傳送至 *Snap Inc* 目的地必須以SHA-256格式雜湊。 若要在將純文字識別碼傳送至目的地之前加以雜湊，請檢查 **[!UICONTROL 套用轉換]** 選項。

>[!WARNING]
> 
> Snap Inc目的地將不接受未雜湊的標識符，發送這些標識符可能會導致錯誤。


>[!IMPORTANT]
> 
> Snap Inc目標不支援多個身份。 請僅選擇一個身份。

| Target身分 | 說明 | 考量事項 |
|---|---|---|
| Email Address | SHA-256雜湊電子郵件地址 | 將電子郵件地址映射至目標身分欄位 *emailAddress*. |
| 電話號碼 | SHA-256雜湊電話號碼 | 將電子郵件地址映射至目標身分欄位 *phoneNumber*. |
| GAID | SHA-256雜湊Google Advertising ID | 將Google Advertising ID對應至目標身分欄位 *gaid*. |
| IDFA | SHA-256雜湊Apple Advertising ID | 將Apple Advertising ID對應至目標身分欄位 *idfa*. |

{style="table-layout:auto"}

## 匯出類型和頻率 {#export-type-frequency}

有關目標導出類型和頻率的資訊，請參閱下表。

| 項目 | 類型 | 附註 |
---------|----------|---------|
| 匯出類型 | **[!UICONTROL 區段匯出]** | 您正在匯出區段（對象）的所有成員，其中包含 *您的目的地* 目的地。 |
| 匯出頻率 | **[!UICONTROL 串流]** | 串流目的地是「一律開啟」API型連線。 一旦根據區段評估在Experience Platform中更新設定檔，連接器就會將更新傳送至下游的目的地平台。 深入了解 [串流目的地](/help/destinations/destination-types.md#streaming-destinations). |

{style="table-layout:auto"}

## 連接到Snap Inc {#connect}

>[!IMPORTANT]
> 
>若要連線至目的地，您需要 **[!UICONTROL 管理目的地]** [存取控制權限](/help/access-control/home.md#permissions). 閱讀 [存取控制概觀](/help/access-control/ui/overview.md) 或聯絡您的產品管理員以取得所需的權限。

### 驗證到目標 {#authenticate}

要驗證到目標，請執行以下步驟：

1. 尋找 *Snap Inc* 目的地(來自Adobe Experience Platform的目的地目錄)，然後選取 **設定**.
2. 選擇 **[!UICONTROL 連接到目標]**. 系統會將您重新導向至下列畫面：
   ![驗證螢幕1](/help/destinations/assets/catalog/advertising/snapchat-ads/auth1.png)
3. 輸入您的Snapchat憑據並選擇 **登入**.
4. 您將看到Adobe Experience Platform將能存取的Snapchat資料。 選擇 **繼續** 繼續連接過程。

![驗證螢幕2](/help/destinations/assets/catalog/advertising/snapchat-ads/auth2.png)

選取「繼續」後，請等到系統將您重新導向回Adobe Experience Platform。

### 填寫目的地詳細資訊 {#destination-details}

![目的地詳細資訊](/help/destinations/assets/catalog/advertising/snapchat-ads/destinationdetails.png)

若要設定目的地的詳細資訊，請填寫必填欄位並選取 **[!UICONTROL 下一個]**.

* **[!UICONTROL 名稱]**:日後您將透過此名稱識別此目的地。
* **[!UICONTROL 說明]**:未來可協助您識別此目的地的說明。
* **[!UICONTROL 帳戶ID]**:與您要匯入區段之廣告帳戶相關聯的廣告帳戶ID。 有關如何查找此資訊的詳細資訊，請參閱 [Snapchat業務幫助中心的本文檔](https://businesshelp.snapchat.com/s/article/biz-acct-id?language=en_US).

>[!IMPORTANT]
> 
>輸入錯誤或無效的Snapchat廣告帳戶ID會導致區段啟動失敗。 請仔細檢查您是否輸入了正確的廣告帳戶ID。

### 啟用警報 {#enable-alerts}

您可以啟用警報，接收有關資料流到目標狀態的通知。 從清單中選擇要訂閱的警報，以接收有關資料流狀態的通知。 如需警報的詳細資訊，請參閱 [使用UI訂閱目的地警報](../../ui/alerts.md).

完成提供目標連接的詳細資訊後，請選擇 **[!UICONTROL 下一個]**.

## 啟用此目的地的區段 {#activate}

>[!IMPORTANT]
> 
>若要啟用資料，您需要 **[!UICONTROL 管理目的地]**, **[!UICONTROL 啟動目的地]**, **[!UICONTROL 檢視設定檔]**，和 **[!UICONTROL 檢視區段]** [存取控制權限](/help/access-control/home.md#permissions). 閱讀 [存取控制概觀](/help/access-control/ui/overview.md) 或聯絡您的產品管理員以取得所需的權限。

閱讀 [啟動設定檔和區段至串流區段匯出目的地](/help/destinations/ui/activate-segment-streaming-destinations.md) 以取得啟用受眾區段至此目的地的指示。

## 驗證資料匯出 {#exported-data}

將區段啟用至 *Snap Inc* 目的地，您將能在Snap Ads Manager的 [**對象** 節](https://businesshelp.snapchat.com/s/article/audience-sharing). 若要導覽至本區段，請依照下列步驟操作：

1. 登入 [Snap Ads Manager](https://ads.snapchat.com/)
2. 選擇 **對象** 從螢幕左上角的下拉式功能表。 您會在對象庫中看到您在Adobe Experience Platform中啟動的區段：

![受眾](/help/destinations/assets/catalog/advertising/snapchat-ads/audiences.png)

請注意，當Adobe段首次激活到Snap Inc時，您最初會將其視為空對象。 這是因為Adobe Experience Platform在評估段之前不會將成員資料導出到Snap Inc。 如需如何評估Experience Platform區段的詳細資訊，請參閱 [區段服務概觀](https://experienceleague.adobe.com/docs/experience-platform/segmentation/home.html?lang=en#evaluate-segments).

## 資料使用與控管 {#data-usage-governance}

全部 [!DNL Adobe Experience Platform] 處理資料時，目的地符合資料使用原則。 有關如何 [!DNL Adobe Experience Platform] 強制實施資料控管，請參閱 [資料控管概觀](/help/data-governance/home.md).
