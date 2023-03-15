---
keywords: 飛艇屬性；飛艇目的地
title: Airship屬性連接
description: 流暢地將Adobe對象資料傳遞至Airship，作為對象屬性，以在Airship內鎖定目標。
exl-id: bfc1b52f-2d68-40d6-9052-c2ee1e877961
source-git-commit: fd2019feb25b540612a278cbea5bf5efafe284dc
workflow-type: tm+mt
source-wordcount: '972'
ht-degree: 0%

---

# [!DNL Airship Attributes] 連接 {#airship-attributes-destination}

## 總覽 {#overview}

[!DNL Airship] 是領先的客戶參與平台，可協助您在客戶生命週期的每個階段，為使用者提供有意義的個人化全通路訊息。

此整合會將Adobe設定檔資料傳遞至 [!DNL Airship] as [屬性](https://docs.airship.com/guides/audience/attributes/) 用於鎖定目標或觸發。

若要深入了解 [!DNL Airship]，請參閱 [Airship檔案](https://docs.airship.com).

>[!TIP]
>
>本檔案頁面由 [!DNL Airship] 團隊。 如有任何查詢或更新請求，請直接與他們聯繫，地址為 [support.airship.com](https://support.airship.com/).

## 先決條件 {#prerequisites}

將受眾區段傳送至之前 [!DNL Airship]，您必須：

* 在 [!DNL Airship] 專案。
* 生成用於驗證的承載令牌。

>[!TIP]
>
>建立 [!DNL Airship] 帳戶 [此註冊連結](https://go.airship.eu/accounts/register/plan/starter/) 如果還沒有。

## 匯出類型和頻率 {#export-type-frequency}

有關目標導出類型和頻率的資訊，請參閱下表。

| 項目 | 類型 | 附註 |
---------|----------|---------|
| 匯出類型 | **[!UICONTROL 設定檔]** | 您要匯出區段的所有成員，以及所需的結構欄位(例如：根據您的欄位對應，以電子郵件地址、電話號碼、姓氏)和/或身分識別。 |
| 匯出頻率 | **[!UICONTROL 串流]** | 串流目的地是「一律開啟」API型連線。 一旦根據區段評估在Experience Platform中更新設定檔，連接器就會將更新傳送至下游的目的地平台。 深入了解 [串流目的地](/help/destinations/destination-types.md#streaming-destinations). |

{style="table-layout:auto"}

## 啟用屬性 {#enable-attributes}

Adobe Experience Platform設定檔屬性類似於 [!DNL Airship] 屬性，並可使用本頁下方示範的對應工具，輕鬆在Platform中彼此對應。

[!DNL Airship] 專案有數個預先定義和預設屬性。 如果您有自訂屬性，則必須在 [!DNL Airship] 第一個。 請參閱 [設定和管理屬性](https://docs.airship.com/tutorials/audience/attributes/) 以取得詳細資訊。

## 生成承載令牌 {#bearer-token}

前往 **[!UICONTROL 設定]** &quot; **[!UICONTROL API與整合]** 在 [飛艇儀表板](https://go.airship.com) 選取 **[!UICONTROL 代號]** 的下一頁。

按一下 **[!UICONTROL 建立代號]**.

為代號提供好記的名稱，例如「Adobe屬性目的地」，並為角色選取「完全存取」。

按一下 **[!UICONTROL 建立代號]** 並將細節保存為機密。

## 使用案例 {#use-cases}

以協助您更清楚了解應如何及何時使用 [!DNL Airship Attributes] 目的地，以下是Adobe Experience Platform客戶可透過此目的地解決的範例使用案例。

### 使用案例#1

運用在Adobe Experience Platform中收集的設定檔資料，針對任何 [!DNL Airship]的頻道。 例如，利用 [!DNL Experience Platform] 設定位置屬性的設定檔資料 [!DNL Airship]. 這可讓酒店品牌顯示每位使用者最近酒店位置的影像。

### 使用案例#2

運用Adobe Experience Platform的屬性，進一步豐富 [!DNL Airship] 設定檔，並與SDK結合，或 [!DNL Airship] 預測性資料。 例如，零售商可以建立具有忠誠度狀態和位置資料（來自Platform的屬性）的區段，以及 [!DNL Airship] 預計會流失資料，將目標明確的訊息傳送給居住在內華達州拉斯維加斯的黃金忠誠度狀態使用者，且產生轉譯的可能性很高。

## 連接到目標 {#connect}

>[!IMPORTANT]
> 
>若要連線至目的地，您需要 **[!UICONTROL 管理目的地]** [存取控制權限](/help/access-control/home.md#permissions). 閱讀 [存取控制概觀](/help/access-control/ui/overview.md) 或聯絡您的產品管理員以取得所需的權限。

若要連線至此目的地，請依照 [目的地設定教學課程](../../ui/connect-destination.md). 在設定目標工作流程中，填寫下列兩節所列的欄位。

### 驗證到目標 {#authenticate}

若要驗證目的地，請填寫必填欄位並選取 **[!UICONTROL 連接到目標]**.

* **[!UICONTROL 承載令牌]**:您從 [!DNL Airship] 控制面板。

### 填寫目的地詳細資訊 {#destination-details}

若要設定目的地的詳細資訊，請填寫下方的必填和選填欄位。 UI中欄位旁的星號表示該欄位為必要欄位。

* **[!UICONTROL 名稱]**:輸入有助於您識別此目的地的名稱。
* **[!UICONTROL 說明]**:輸入此目標的說明。
* **[!UICONTROL 網域]**:選取美國或歐盟資料中心，視 [!DNL Airship] 資料中心適用於此目的地。

### 啟用警報 {#enable-alerts}

您可以啟用警報，接收有關資料流到目標狀態的通知。 從清單中選擇要訂閱的警報，以接收有關資料流狀態的通知。 如需警報的詳細資訊，請參閱 [使用UI訂閱目的地警報](../../ui/alerts.md).

完成提供目標連接的詳細資訊後，請選擇 **[!UICONTROL 下一個]**.

## 啟用此目的地的區段 {#activate}

>[!IMPORTANT]
> 
>若要啟用資料，您需要 **[!UICONTROL 管理目的地]**, **[!UICONTROL 啟動目的地]**, **[!UICONTROL 檢視設定檔]**，和 **[!UICONTROL 檢視區段]** [存取控制權限](/help/access-control/home.md#permissions). 閱讀 [存取控制概觀](/help/access-control/ui/overview.md) 或聯絡您的產品管理員以取得所需的權限。

請參閱 [對串流區段匯出目的地啟用受眾資料](../../ui/activate-segment-streaming-destinations.md) 以取得啟用受眾區段至此目的地的指示。

## 對應考量事項 {#mapping-considerations}

[!DNL Airship] 屬性可在代表裝置例項(例如iPhone)的頻道上設定，或是指名使用者，可將使用者的所有裝置對應至通用識別碼（例如客戶ID）。 如果您的結構中有純文字（未雜湊）電子郵件地址作為主要身分，請在您的 **[!UICONTROL 源屬性]** 並對應至 [!DNL Airship] 在下方的右欄中指定使用者 **[!UICONTROL 目標身分]**，如下所示。

![命名用戶映射](../../assets/catalog/mobile-engagement/airship/mapping.png)

對於應映射到通道（即設備）的標識符，根據源映射到相應的通道。 下圖顯示如何建立兩個對應：

* IDFA iOS Advertising ID至 [!DNL Airship] iOS頻道
* Adobe `fullName` 屬性至 [!DNL Airship] 「全名」屬性

>[!NOTE]
>
>使用顯示在 [!DNL Airship] 為屬性對應選取目標欄位時的控制面板。

**對應身分**

選擇源欄位：

![連接到Airship屬性](../../assets/catalog/mobile-engagement/airship/select-source-identity.png)

選擇目標欄位：

![連接到Airship屬性](../../assets/catalog/mobile-engagement/airship/select-target-identity.png)

**地圖屬性**

選擇源屬性：

![選擇源欄位](../../assets/catalog/mobile-engagement/airship/select-source-attributes.png)

選擇目標屬性：

![選擇目標欄位](../../assets/catalog/mobile-engagement/airship/select-target-attribute.png)

驗證映射：

![通道對應](../../assets/catalog/mobile-engagement/airship/mapping.png)


## 資料使用與控管 {#data-usage-governance}

全部 [!DNL Adobe Experience Platform] 處理資料時，目的地符合資料使用原則。 有關如何 [!DNL Adobe Experience Platform] 強制實施資料控管，請參閱 [資料控管概觀](../../../data-governance/home.md).
