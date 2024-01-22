---
keywords: 飛艇標籤；飛艇目的地
title: 飛艇標籤連線
description: 將Adobe對象資料順暢地傳遞給Airship，作為Airship中用於鎖定目標的對象標籤。
exl-id: 84cf5504-f0b5-48d8-8da1-ff91ee1dc171
source-git-commit: c3ef732ee82f6c0d56e89e421da0efc4fbea2c17
workflow-type: tm+mt
source-wordcount: '970'
ht-degree: 2%

---

# [!DNL Airship Tags] 連線 {#airship-tags-destination}

## 概觀

[!DNL Airship] 是領先的客戶參與平台，可在客戶生命週期的每個階段，協助您為使用者提供有意義、個人化的全通路訊息。

這項整合可將Adobe Experience Platform受眾資料傳遞至 [!DNL Airship] 作為 [標籤](https://docs.airship.com/guides/audience/tags/) 進行定位或觸發。

若要深入瞭解 [!DNL Airship]，請參閱 [飛艇檔案](https://docs.airship.com).


>[!TIP]
>
>此目的地聯結器和檔案頁面是由 [!DNL Airship] 團隊。 如有任何查詢或更新要求，請直接聯絡他們： [support.airship.com](https://support.airship.com/).

## 先決條件

傳送Adobe Experience Platform對象至之前 [!DNL Airship]，您必須：

* 在您的中建立標籤群組 [!DNL Airship] 專案。
* 產生持有人權杖以進行驗證。

>[!TIP]
> 
>建立 [!DNL Airship] 帳戶透過 [此註冊連結](https://go.airship.eu/accounts/register/plan/starter/) 如果您尚未這樣做。

## 支援的對象 {#supported-audiences}

本節說明您可以將哪些型別的對象匯出至此目的地。

| 對象來源 | 支援 | 說明 |
---------|----------|----------|
| [!DNL Segmentation Service] | ✓ (A) | 透過Experience Platform產生的對象 [分段服務](../../../segmentation/home.md). |
| 自訂上傳 | ✓ | 受眾 [已匯入](../../../segmentation/ui/overview.md#import-audience) 從CSV檔案Experience Platform為。 |

{style="table-layout:auto"}

## 匯出型別和頻率 {#export-type-frequency}

請參閱下表以取得目的地匯出型別和頻率的資訊。

| 項目 | 類型 | 附註 |
---------|----------|---------|
| 匯出型別 | **[!UICONTROL 對象匯出]** | 您正在匯出某個對象的所有成員，而這些成員具有在「飛艇標籤」目的地中使用的識別碼。 |
| 匯出頻率 | **[!UICONTROL 串流]** | 串流目的地是「一律開啟」的API型連線。 一旦根據對象評估在Experience Platform中更新了設定檔，聯結器就會將更新傳送至下游的目的地平台。 深入瞭解 [串流目的地](/help/destinations/destination-types.md#streaming-destinations). |

{style="table-layout:auto"}

## 標籤群組

Adobe Experience Platform中的受眾概念類似 [標籤](https://docs.airship.com/guides/audience/tags/) 在Airship中，實施上有細微差異。 此整合會對應使用者的 [Experience Platform區段中的成員資格](../../../xdm/field-groups/profile/segmentation.md) 是否存在 [!DNL Airship] 標籤之間。 例如，在Platform對象中， `xdm:status` 變更為 `realized`，則標籤會新增至 [!DNL Airship] 此設定檔對應的頻道或具名使用者。 如果 `xdm:status` 變更為 `exited`，則會移除標籤。

若要啟用此整合，請建立 *標籤群組* 在 [!DNL Airship] 已命名 `adobe-segments`.

>[!IMPORTANT]
>
>建立新標籤群組時 **不檢查** 顯示「[!DNL Allow these tags to be set only from your server]「。 這麼做會導致Adobe標籤整合失敗。

另請參閱 [管理標籤群組](https://docs.airship.com/tutorials/manage-project/messaging/tag-groups) 以取得建立標籤群組的指示。

## 產生持有人權杖

前往 **[!UICONTROL 設定]** &quot; **[!UICONTROL API和整合]** 在 [飛艇儀表板](https://go.airship.com) 並選取 **[!UICONTROL Token]** 在左側功能表中。

按一下 **[!UICONTROL 建立Token]**.

為您的Token提供好記的名稱，例如「Adobe標籤目的地」，並為該角色選取「完全存取」。

按一下 **[!UICONTROL 建立Token]** 並將詳細資料儲存為機密檔案。

## 使用案例

為了協助您更清楚瞭解您應如何及何時使用 [!DNL Airship Tags] 目的地，以下是Adobe Experience Platform客戶可以使用此目的地解決的範例使用案例。

### 使用案例#1

零售商或娛樂平台可建立其忠誠度客戶的使用者設定檔，並將這些受眾傳遞至 [!DNL Airship] 適用於行動裝置行銷活動上的訊息目標定位。

### 使用案例#2

當使用者進入或退出Adobe Experience Platform中的特定對象時，即時觸發一對一訊息。

例如，零售商在Platform中設定牛仔褲品牌特定對象。 只要某人將其牛仔褲偏好設定為特定品牌，該零售商現在就能觸發行動裝置訊息。

## 連線到目標 {#connect}

>[!IMPORTANT]
> 
>若要連線到目的地，您需要 **[!UICONTROL 檢視目的地]** 和 **[!UICONTROL 管理目的地]** [存取控制許可權](/help/access-control/home.md#permissions). 閱讀 [存取控制總覽](/help/access-control/ui/overview.md) 或聯絡您的產品管理員以取得必要許可權。

若要連線至此目的地，請遵循以下說明的步驟： [目的地設定教學課程](../../ui/connect-destination.md). 在設定目標工作流程中，填寫以下兩個區段中列出的欄位。

### 驗證目標 {#authenticate}

若要向目的地進行驗證，請填寫必填欄位並選取 **[!UICONTROL 連線到目的地]**.

* **[!UICONTROL 持有人權杖]**：您從產生的持有人權杖 [!DNL Airship] 儀表板。

### 填寫目標詳細資訊 {#destination-details}

若要設定目的地的詳細資訊，請填寫下方的必填和選用欄位。 UI中欄位旁的星號表示該欄位為必填欄位。

* **[!UICONTROL 名稱]**：輸入有助於您識別此目的地的名稱。
* **[!UICONTROL 說明]**：輸入此目的地的說明。
* **[!UICONTROL 網域]**：選取美國或歐洲的資料中心，視何者為何 [!DNL Airship] 資料中心會套用至此目的地。

### 啟用警示 {#enable-alerts}

您可以啟用警報以接收有關傳送到您目的地的資料流狀態的通知。 從清單中選取警報以訂閱接收有關資料流狀態的通知。 如需警示的詳細資訊，請參閱以下指南： [使用UI訂閱目的地警報](../../ui/alerts.md).

當您完成提供目的地連線的詳細資訊時，請選取「 」 **[!UICONTROL 下一個]**.

## 啟動此目標的對象 {#activate}

>[!IMPORTANT]
> 
>若要啟用資料，您需要 **[!UICONTROL 檢視目的地]**， **[!UICONTROL 啟用目的地]**， **[!UICONTROL 檢視設定檔]**、和 **[!UICONTROL 檢視區段]** [存取控制許可權](/help/access-control/home.md#permissions). 閱讀 [存取控制總覽](/help/access-control/ui/overview.md) 或聯絡您的產品管理員以取得必要許可權。

另請參閱 [啟用受眾資料至串流受眾匯出目的地](../../ui/activate-segment-streaming-destinations.md) 以取得啟用此目的地對象的指示。

## 對應考量事項 {#mapping-considerations}

[!DNL Airship] 標籤可在頻道上設定，以代表裝置例項，例如iPhone，或可對映所有使用者裝置至共同識別碼（例如客戶ID）的已命名使用者。 如果您的結構描述中以純文字（未雜湊）電子郵件地址為主要身分，請選取結構描述中的電子郵件欄位 **[!UICONTROL 來源屬性]** 並將對應至 [!DNL Airship] 已命名使用者在下的右側欄 **[!UICONTROL 目標身分]**，如下所示。

![已命名的使用者對應](../../assets/catalog/mobile-engagement/airship-tags/mapping-option-2.png)

對於應對應至管道（即裝置）的識別碼，請根據來源對應至適當的管道。 下列影像說明如何將Google Advertising ID對應至 [!DNL Airship] Android頻道。

![連線到飛艇標籤](../../assets/catalog/mobile-engagement/airship-tags/select-source-identity.png)
![連線到飛艇標籤](../../assets/catalog/mobile-engagement/airship-tags/select-target-identity.png)
![頻道對應](../../assets/catalog/mobile-engagement/airship-tags/mapping-option.png)

## 資料使用與控管 {#data-usage-governance}

全部 [!DNL Adobe Experience Platform] 處理您的資料時，目的地符合資料使用原則。 如需如何操作的詳細資訊 [!DNL Adobe Experience Platform] 強制資料控管，請參閱 [資料控管概觀](../../../data-governance/home.md).
