---
keywords: 飛艇標籤；飛艇目的地
title: 飛艇標籤連線
description: 無縫地將Adobe對象資料傳遞至Airship，作為Airship中用於鎖定的對象標籤。
exl-id: 84cf5504-f0b5-48d8-8da1-ff91ee1dc171
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '972'
ht-degree: 2%

---

# [!DNL Airship Tags]個連線 {#airship-tags-destination}

## 概觀

[!DNL Airship]是領先的客戶參與平台，可在客戶生命週期的每個階段協助您為使用者提供有意義、個人化的全通路訊息。

此整合會將Adobe Experience Platform對象資料作為[標籤](https://docs.airship.com/guides/audience/tags/)傳遞至[!DNL Airship]，以用於鎖定或觸發。

若要深入瞭解[!DNL Airship]，請參閱[飛艇檔案](https://docs.airship.com)。


>[!TIP]
>
>此目的地聯結器和檔案頁面是由[!DNL Airship]團隊建立和維護。 若有任何查詢或更新要求，請直接透過[support.airship.com](https://support.airship.com/)連絡他們。

## 先決條件

在將Adobe Experience Platform對象傳送至[!DNL Airship]之前，您必須：

* 在您的[!DNL Airship]專案中建立標籤群組。
* 產生持有人權杖以進行驗證。

>[!TIP]
> 
>如果您尚未透過[此註冊連結](https://go.airship.eu/accounts/register/plan/starter/)建立[!DNL Airship]帳戶。

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
---------|----------|---------|
| 匯出類型 | **[!UICONTROL 對象匯出]** | 您正在匯出某個對象的所有成員，而這些成員具有在「飛艇標籤」目的地中使用的識別碼。 |
| 匯出頻率 | **[!UICONTROL 串流]** | 串流目的地是「一律開啟」的API型連線。 根據對象評估在Experience Platform中更新設定檔後，聯結器會立即將更新傳送至下游的目標平台。 深入瞭解[串流目的地](/help/destinations/destination-types.md#streaming-destinations)。 |

{style="table-layout:auto"}

## 標籤群組

Adobe Experience Platform中的對象概念類似於Airship中的[標籤](https://docs.airship.com/guides/audience/tags/)，在實施上稍有差異。 此整合將使用者在Experience Platform區段](../../../xdm/field-groups/profile/segmentation.md)中的[成員資格狀態對應至[!DNL Airship]標籤是否存在或不存在。 例如，在`xdm:status`變更為`realized`的Experience Platform對象中，標籤已新增至此設定檔對應到的[!DNL Airship]頻道或具名使用者。 如果`xdm:status`變更為`exited`，標籤將會移除。

若要啟用這項整合，請在[!DNL Airship]中建立一個名為`adobe-segments`的&#x200B;*標籤群組*。

>[!IMPORTANT]
>
>建立新標籤群組時&#x200B;**請勿勾選**&#x200B;顯示&quot;[!DNL Allow these tags to be set only from your server]&quot;的選項按鈕。 這麼做會導致Adobe標籤整合失敗。

如需建立標籤群組的指示，請參閱[管理標籤群組](https://docs.airship.com/tutorials/manage-project/messaging/tag-groups)。

## 產生持有人權杖

移至[飛艇儀表板](https://go.airship.com)中的&#x200B;**[!UICONTROL 設定]** &quot; **[!UICONTROL API和整合]**，然後在左側功能表中選取&#x200B;**[!UICONTROL 代號]**。

按一下&#x200B;**[!UICONTROL 建立Token]**。

為您的Token提供好記的名稱，例如「Adobe標籤目的地」，然後為角色選取「完全存取」。

按一下&#x200B;**[!UICONTROL 建立Token]**，並將詳細資料儲存為機密檔案。

## 使用案例

為協助您更清楚瞭解您應如何及何時使用[!DNL Airship Tags]目的地，以下是Adobe Experience Platform客戶可藉由使用此目的地解決的範例使用案例。

### 使用案例#1

零售商或娛樂平台可建立其忠誠度客戶的使用者設定檔，並將這些對象傳遞至[!DNL Airship]，以便在行動裝置行銷活動中傳送訊息目標定位。

### 使用案例#2

當使用者進入或退出Adobe Experience Platform中的特定對象時，即時觸發一對一訊息。

例如，retailer會在Experience Platform中設定牛仔褲品牌專屬對象。 retailer現在會在有人將牛仔褲偏好設定為特定品牌時，立即觸發行動訊息。

## 連線到目標 {#connect}

>[!IMPORTANT]
> 
>若要連線到目的地，您需要&#x200B;**[!UICONTROL 檢視目的地]**&#x200B;和&#x200B;**[!UICONTROL 管理目的地]** [存取控制許可權](/help/access-control/home.md#permissions)。 閱讀[存取控制總覽](/help/access-control/ui/overview.md)或連絡您的產品管理員以取得必要的許可權。

若要連線到此目的地，請依照[目的地組態教學課程](../../ui/connect-destination.md)中所述的步驟進行。 在設定目標工作流程中，填寫以下兩個區段中列出的欄位。

### 驗證目標 {#authenticate}

若要驗證到目的地，請填入必填欄位，然後選取&#x200B;**[!UICONTROL 連線到目的地]**。

* **[!UICONTROL 持有人權杖]**：您從[!DNL Airship]儀表板產生的持有人權杖。

### 填寫目標詳細資訊 {#destination-details}

若要設定目的地的詳細資訊，請填寫下方的必填和選用欄位。 UI中欄位旁的星號表示該欄位為必填欄位。

* **[!UICONTROL 名稱]**：輸入可協助您識別此目的地的名稱。
* **[!UICONTROL 描述]**：輸入此目的地的描述。
* **[!UICONTROL 網域]**：選取美國或歐盟資料中心，視哪個[!DNL Airship]資料中心套用至此目的地而定。

### 啟用警示 {#enable-alerts}

您可以啟用警報以接收有關傳送到您目的地的資料流狀態的通知。 從清單中選取警報以訂閱接收有關資料流狀態的通知。 如需警示的詳細資訊，請參閱[使用UI訂閱目的地警示](../../ui/alerts.md)的指南。

當您完成提供目的地連線的詳細資訊後，請選取&#x200B;**[!UICONTROL 下一步]**。

## 啟動此目標的對象 {#activate}

>[!IMPORTANT]
> 
>若要啟用資料，您需要&#x200B;**[!UICONTROL 檢視目的地]**、**[!UICONTROL 啟用目的地]**、**[!UICONTROL 檢視設定檔]**&#x200B;和&#x200B;**[!UICONTROL 檢視區段]** [存取控制許可權](/help/access-control/home.md#permissions)。 閱讀[存取控制總覽](/help/access-control/ui/overview.md)或連絡您的產品管理員以取得必要的許可權。

如需啟用此目的地的對象的指示，請參閱[啟用串流對象匯出目的地的對象資料](../../ui/activate-segment-streaming-destinations.md)。

## 對應考量事項 {#mapping-considerations}

[!DNL Airship]標籤可在代表裝置執行個體(例如iPhone)的頻道上設定，或可對映所有使用者裝置至共同識別碼（例如客戶ID）的具名使用者上設定。 如果您的結構描述中有純文字（未雜湊）電子郵件地址作為主要身分，請在&#x200B;**[!UICONTROL Source屬性]**&#x200B;中選取電子郵件欄位，並對應至&#x200B;**[!UICONTROL 目標身分]**&#x200B;下右側欄中的[!DNL Airship]具名使用者，如下所示。

![具名使用者對應](../../assets/catalog/mobile-engagement/airship-tags/mapping-option-2.png)

對於應對應至管道（即裝置）的識別碼，請根據來源對應至適當的管道。 下列影像說明如何將Google Advertising ID對應至[!DNL Airship] Android頻道。

![連線到飛艇標籤](../../assets/catalog/mobile-engagement/airship-tags/select-source-identity.png)
![連線到飛艇標籤](../../assets/catalog/mobile-engagement/airship-tags/select-target-identity.png)
![頻道對應](../../assets/catalog/mobile-engagement/airship-tags/mapping-option.png)

## 資料使用與控管 {#data-usage-governance}

處理您的資料時，所有[!DNL Adobe Experience Platform]目的地都符合資料使用原則。 如需[!DNL Adobe Experience Platform]如何強制資料控管的詳細資訊，請參閱[資料控管概觀](../../../data-governance/home.md)。
