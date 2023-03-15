---
keywords: 飛艇標籤；飛艇目的地
title: Airship標籤連接
description: 流暢地將Adobe對象資料傳遞至Airship，作為對象標籤，以在Airship內鎖定目標。
exl-id: 84cf5504-f0b5-48d8-8da1-ff91ee1dc171
source-git-commit: fd2019feb25b540612a278cbea5bf5efafe284dc
workflow-type: tm+mt
source-wordcount: '944'
ht-degree: 0%

---

# [!DNL Airship Tags] 連接 {#airship-tags-destination}

## 總覽

[!DNL Airship] 是領先的客戶參與平台，可協助您在客戶生命週期的每個階段，為使用者提供有意義的個人化全通路訊息。

此整合會將Adobe Experience Platform區段資料傳遞至 [!DNL Airship] as [標籤](https://docs.airship.com/guides/audience/tags/) 用於鎖定目標或觸發。

若要深入了解 [!DNL Airship]，請參閱 [Airship檔案](https://docs.airship.com).


>[!TIP]
>
>本檔案頁面由 [!DNL Airship] 團隊。 如有任何查詢或更新請求，請直接與他們聯繫，地址為 [support.airship.com](https://support.airship.com/).

## 先決條件

將Adobe Experience Platform區段傳送至 [!DNL Airship]，您必須：

* 在 [!DNL Airship] 專案。
* 生成用於驗證的承載令牌。

>[!TIP]
> 
>建立 [!DNL Airship] 帳戶 [此註冊連結](https://go.airship.eu/accounts/register/plan/starter/) 如果還沒有。

## 匯出類型和頻率 {#export-type-frequency}

有關目標導出類型和頻率的資訊，請參閱下表。

| 項目 | 類型 | 附註 |
---------|----------|---------|
| 匯出類型 | **[!UICONTROL 區段匯出]** | 您正在匯出區段（對象）的所有成員，以及Airship Tags目的地中使用的識別碼。 |
| 匯出頻率 | **[!UICONTROL 串流]** | 串流目的地是「一律開啟」API型連線。 一旦根據區段評估在Experience Platform中更新設定檔，連接器就會將更新傳送至下游的目的地平台。 深入了解 [串流目的地](/help/destinations/destination-types.md#streaming-destinations). |

{style="table-layout:auto"}

## 標籤群組

Adobe Experience Platform中的區段概念類似於 [標籤](https://docs.airship.com/guides/audience/tags/) 在飛艇上，在實施上稍有差異。 此整合會對應使用者的 [Experience Platform區段的成員資格](../../../xdm/field-groups/profile/segmentation.md) 是否存在 [!DNL Airship] 標籤。 例如，在平台區段中， `xdm:status` 變更 `realized`，則標籤會新增至 [!DNL Airship] 此設定檔對應的頻道或指名使用者。 若 `xdm:status` 變更 `exited`，則會移除標籤。

若要啟用此整合，請建立 *標籤群組* in [!DNL Airship] 已命名 `adobe-segments`.

>[!IMPORTANT]
>
>建立新標籤組時 **不檢查** 「[!DNL Allow these tags to be set only from your server]」。 這麼做會導致Adobe標籤整合失敗。

請參閱 [管理標籤群組](https://docs.airship.com/tutorials/manage-project/messaging/tag-groups) 以取得建立標籤群組的說明。

## 生成承載令牌

前往 **[!UICONTROL 設定]** &quot; **[!UICONTROL API與整合]** 在 [飛艇儀表板](https://go.airship.com) 選取 **[!UICONTROL 代號]** 的下一頁。

按一下 **[!UICONTROL 建立代號]**.

提供您代號的好記名稱，例如「Adobe標籤目的地」，並為角色選取「完全存取」。

按一下 **[!UICONTROL 建立代號]** 並將細節保存為機密。

## 使用案例

以協助您更清楚了解應如何及何時使用 [!DNL Airship Tags] 目的地，以下是Adobe Experience Platform客戶可透過此目的地解決的範例使用案例。

### 使用案例#1

零售商或娛樂平台可建立其忠誠客戶的使用者設定檔，並將這些區段傳入 [!DNL Airship] ，以在行動促銷活動上鎖定訊息。

### 使用案例#2

當使用者落入或離開Adobe Experience Platform內的特定區段時，即時觸發一對一訊息。

例如，零售商在Platform中設定牛仔褲品牌專屬區段。 當某人將牛仔褲偏好設定設為特定品牌時，該零售商現在可以觸發行動訊息。

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

[!DNL Airship] 標籤可在代表裝置例項(例如iPhone)的頻道上設定，或是指名使用者，可將使用者的所有裝置對應至通用識別碼（例如客戶ID）。 如果您的結構中有純文字（未雜湊）電子郵件地址作為主要身分，請在您的 **[!UICONTROL 源屬性]** 並對應至 [!DNL Airship] 在下方的右欄中指定使用者 **[!UICONTROL 目標身分]**，如下所示。

![命名用戶映射](../../assets/catalog/mobile-engagement/airship-tags/mapping-option-2.png)

對於應映射到通道（即設備）的標識符，根據源映射到相應的通道。 下列影像顯示如何將Google Advertising ID對應至 [!DNL Airship] Android頻道。

![連接到Airship標籤](../../assets/catalog/mobile-engagement/airship-tags/select-source-identity.png)
![連接到Airship標籤](../../assets/catalog/mobile-engagement/airship-tags/select-target-identity.png)
![通道對應](../../assets/catalog/mobile-engagement/airship-tags/mapping-option.png)

## 資料使用與控管 {#data-usage-governance}

全部 [!DNL Adobe Experience Platform] 處理資料時，目的地符合資料使用原則。 有關如何 [!DNL Adobe Experience Platform] 強化資料控管，請參閱 [資料控管概觀](../../../data-governance/home.md).
