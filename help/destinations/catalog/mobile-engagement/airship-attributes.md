---
keywords: 飛艇屬性；飛艇目的地
title: 飛艇屬性連線
description: 將Adobe對象資料順暢地傳遞給Airship，作為Airship中用於鎖定的對象屬性。
exl-id: bfc1b52f-2d68-40d6-9052-c2ee1e877961
source-git-commit: 8e37ff057ec0fb750bc7b4b6f566f732d9fe5d68
workflow-type: tm+mt
source-wordcount: '1048'
ht-degree: 0%

---

# [!DNL Airship Attributes] 連線 {#airship-attributes-destination}

## 概觀 {#overview}

[!DNL Airship] 是領先的客戶參與平台，可在客戶生命週期的每個階段，協助您為使用者提供有意義、個人化的全通路訊息。

這項整合會將Adobe設定檔資料傳遞至 [!DNL Airship] 作為 [屬性](https://docs.airship.com/guides/audience/attributes/) 進行定位或觸發。

若要深入瞭解 [!DNL Airship]，請參閱 [飛艇檔案](https://docs.airship.com).

>[!TIP]
>
>此目的地聯結器和檔案頁面是由 [!DNL Airship] 團隊。 如有任何查詢或更新要求，請直接聯絡他們： [support.airship.com](https://support.airship.com/).

## 先決條件 {#prerequisites}

將受眾傳送至之前 [!DNL Airship]，您必須：

* 啟用中的屬性 [!DNL Airship] 專案。
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
| 匯出型別 | **[!UICONTROL 以設定檔為基礎]** | 您正在匯出區段的所有成員，以及所需的結構欄位（例如：電子郵件地址、電話號碼、姓氏）和/或身分，視您的欄位對應而定。 |
| 匯出頻率 | **[!UICONTROL 串流]** | 串流目的地是「一律開啟」的API型連線。 一旦根據對象評估在Experience Platform中更新了設定檔，聯結器就會將更新傳送至下游的目的地平台。 深入瞭解 [串流目的地](/help/destinations/destination-types.md#streaming-destinations). |

{style="table-layout:auto"}

## 啟用屬性 {#enable-attributes}

Adobe Experience Platform設定檔屬性類似於 [!DNL Airship] 屬性之間對應，並可使用本頁面下方進一步說明的對應工具，在Platform中輕鬆進行對應。

[!DNL Airship] 專案具有數個預先定義的和預設屬性。 如果您有自訂屬性，則必須在下列位置定義該屬性： [!DNL Airship] 第一。 另請參閱 [設定及管理屬性](https://docs.airship.com/tutorials/audience/attributes/) 以取得詳細資訊。

## 產生持有人權杖 {#bearer-token}

前往 **[!UICONTROL 設定]** &quot; **[!UICONTROL API和整合]** 在 [飛艇儀表板](https://go.airship.com) 並選取 **[!UICONTROL Token]** 在左側功能表中。

按一下 **[!UICONTROL 建立Token]**.

為您的Token提供好記的名稱，例如「Adobe屬性目的地」，然後為角色選取「完全存取」。

按一下 **[!UICONTROL 建立Token]** 並將詳細資料儲存為機密檔案。

## 使用案例 {#use-cases}

為了協助您更清楚瞭解您應如何及何時使用 [!DNL Airship Attributes] 目的地，以下是Adobe Experience Platform客戶可以使用此目的地解決的範例使用案例。

### 使用案例#1

善用Adobe Experience Platform中收集的設定檔資料，在任一 [!DNL Airship]的管道。 例如，善用 [!DNL Experience Platform] 設定檔資料，以設定位置屬性 [!DNL Airship]. 這可讓飯店品牌為每位使用者顯示最近的飯店位置影像。

### 使用案例#2

運用Adobe Experience Platform的屬性進一步豐富 [!DNL Airship] 設定檔並將其與SDK或 [!DNL Airship] 預測資料。 例如，零售商可建立具有忠誠度狀態和位置資料（來自Platform的屬性）的受眾，並且 [!DNL Airship] 預測會流失資料，以傳送高針對性訊息給住在內華達州拉斯維加斯的金級忠誠度使用者，且流失率很高。

## 連線到目的地 {#connect}

>[!IMPORTANT]
> 
>若要連線到目的地，您需要 **[!UICONTROL 管理目的地]** [存取控制許可權](/help/access-control/home.md#permissions). 閱讀 [存取控制總覽](/help/access-control/ui/overview.md) 或聯絡您的產品管理員以取得必要許可權。

若要連線至此目的地，請遵循以下說明的步驟： [目的地設定教學課程](../../ui/connect-destination.md). 在設定目標工作流程中，填寫以下兩個區段中列出的欄位。

### 驗證到目的地 {#authenticate}

若要向目的地進行驗證，請填寫必填欄位並選取 **[!UICONTROL 連線到目的地]**.

* **[!UICONTROL 持有人權杖]**：您從產生的持有人權杖 [!DNL Airship] 儀表板。

### 填寫目的地詳細資料 {#destination-details}

若要設定目的地的詳細資訊，請填寫下方的必填和選用欄位。 UI中欄位旁的星號表示該欄位為必填欄位。

* **[!UICONTROL 名稱]**：輸入有助於您識別此目的地的名稱。
* **[!UICONTROL 說明]**：輸入此目的地的說明。
* **[!UICONTROL 網域]**：選取美國或歐洲的資料中心，視何者為何 [!DNL Airship] 資料中心會套用至此目的地。

### 啟用警示 {#enable-alerts}

您可以啟用警報以接收有關傳送到您目的地的資料流狀態的通知。 從清單中選取警報以訂閱接收有關資料流狀態的通知。 如需警示的詳細資訊，請參閱以下指南： [使用UI訂閱目的地警報](../../ui/alerts.md).

當您完成提供目的地連線的詳細資訊時，請選取「 」 **[!UICONTROL 下一個]**.

## 啟用此目的地的對象 {#activate}

>[!IMPORTANT]
> 
>* 若要啟用資料，您需要 **[!UICONTROL 管理目的地]**， **[!UICONTROL 啟用目的地]**， **[!UICONTROL 檢視設定檔]**、和 **[!UICONTROL 檢視區段]** [存取控制許可權](/help/access-control/home.md#permissions). 閱讀 [存取控制總覽](/help/access-control/ui/overview.md) 或聯絡您的產品管理員以取得必要許可權。
>* 要匯出 *身分*，您需要 **[!UICONTROL 檢視身分圖表]** [存取控制許可權](/help/access-control/home.md#permissions). <br> ![選取工作流程中反白顯示的身分名稱空間，以將對象啟用至目的地。](/help/destinations/assets/overview/export-identities-to-destination.png "選取工作流程中反白顯示的身分名稱空間，以將對象啟用至目的地。"){width="100" zoomable="yes"}

另請參閱 [啟用受眾資料至串流受眾匯出目的地](../../ui/activate-segment-streaming-destinations.md) 以取得啟用此目的地對象的指示。

## 對應考量事項 {#mapping-considerations}

[!DNL Airship] 屬性可在代表裝置例項(例如iPhone)的頻道上設定，或可將所有使用者裝置對應至共同識別碼（例如客戶ID）的命名使用者上設定。 如果您的結構描述中以純文字（未雜湊）電子郵件地址為主要身分，請選取結構描述中的電子郵件欄位 **[!UICONTROL 來源屬性]** 並將對應至 [!DNL Airship] 已命名使用者在下的右側欄 **[!UICONTROL 目標身分]**，如下所示。

![已命名的使用者對應](../../assets/catalog/mobile-engagement/airship/mapping.png)

對於應對應至管道（即裝置）的識別碼，請根據來源對應至適當的管道。 下列影像顯示如何建立兩個對應：

* 將IDFA iOS Advertising ID設為 [!DNL Airship] iOS管道
* Adobe `fullName` 歸因至 [!DNL Airship] 「全名」屬性

>[!NOTE]
>
>使用好記的名稱，該名稱會顯示在 [!DNL Airship] 儀表板來選取屬性對應的目標欄位時。

**對應身分**

選取來源欄位：

![連線到飛艇屬性](../../assets/catalog/mobile-engagement/airship/select-source-identity.png)

選取目標欄位：

![連線到飛艇屬性](../../assets/catalog/mobile-engagement/airship/select-target-identity.png)

**對應屬性**

選取來源屬性：

![選取來源欄位](../../assets/catalog/mobile-engagement/airship/select-source-attributes.png)

選取目標屬性：

![選取目標欄位](../../assets/catalog/mobile-engagement/airship/select-target-attribute.png)

驗證對應：

![頻道對應](../../assets/catalog/mobile-engagement/airship/mapping.png)


## 資料使用與控管 {#data-usage-governance}

全部 [!DNL Adobe Experience Platform] 處理您的資料時，目的地符合資料使用原則。 如需如何操作的詳細資訊 [!DNL Adobe Experience Platform] 強制執行資料控管，請參閱 [資料控管概觀](../../../data-governance/home.md).
