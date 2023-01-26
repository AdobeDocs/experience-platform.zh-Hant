---
keywords: 行動裝置；行動參與目的地；LINE;LINE行動參與目的地
title: 線路連接
description: LINE目的地可讓您將設定檔新增至您的平台區段，並為連線的使用者提供個人化體驗。
last-substantial-update: 2022-11-08T00:00:00Z
exl-id: 9981798a-61f2-4a09-9a33-57e63eb36d43
source-git-commit: 83778bc5d643f69e0393c0a7767fef8a4e8f66e9
workflow-type: tm+mt
source-wordcount: '1183'
ht-degree: 1%

---

# [!DNL LINE] 連接

## 總覽 {#overview}

[[!DNL LINE]](https://line.me/en/) 是一個熱門的通訊平台，可連接人員、服務和資訊，並已從聊天應用程式發展為娛樂、社交和日常活動的中心。

此 [!DNL Adobe Experience Platform] [目的地](/help/destinations/home.md) 利用 [[!DNL LINE] 傳訊API](https://developers.line.biz/en/reference/messaging-api/). 您可以從Experience Platform區段啟動設定檔，作為內的連線 [!DNL LINE] 滿足您的業務需求。

[!DNL LINE] 使用Bearer Token作為驗證機制，與 [!DNL LINE] 傳訊API。 向您的 [!DNL LINE] 執行個體進一步，在 [驗證到目標](#authenticate) 區段。

## 使用案例 {#use-cases}

身為行銷人員，您可以透過內建區段，在行動參與目的地中鎖定使用者 [!DNL Adobe Experience Platform]. 此外，您也可以根據訪客的屬性，為其提供個人化體驗 [!DNL Adobe Experience Platform] 設定檔，當區段和設定檔在 [!DNL Adobe Experience Platform].

## 先決條件 {#prerequisites}

### [!DNL LINE] 必要條件 {#prerequisites-destination}

請注意下列必要條件，位於 [!DNL LINE]，以便將資料從Platform匯出至 [!DNL LINE] 帳戶：

#### 你需要 [!DNL LINE] 帳戶 {#prerequisites-account}

您需要註冊並建立 [!DNL LINE] 帳戶，如果尚未建立帳戶。 若要建立帳戶：

1. 導覽至 [!DNL LINE] [帳戶登入](https://account.line.biz/login?redirectUri=https%3A%2F%2Fmanager.line.biz%2F) 頁面
2. 選擇 **[!UICONTROL 建立帳戶]**.

#### 收集 [!DNL LINE channel access token (long-lived)] 從 [!DNL LINE] 開發人員控制台 {#gather-credentials}

允許Platform存取 [!DNL LINE] 資源，您需要 *[!DNL Channel access token (long-lived)]* 從所需 [!DNL LINE] *傳訊API* 頻道。

1. 使用 [!DNL LINE] 帳戶 [[!DNL LINE] 開發人員主控台](https://developers.line.biz/console).
1. 接下來，訪問 *[!DNL Providers]* 清單，然後選取 *[!DNL Provider]* ，最後選取 *傳訊API* 存取其設定的通道。 如果您是首次存取開發人員主控台，請遵循 [[!DNL LINE] 檔案](https://developers.line.biz/en/docs/messaging-api/getting-started/) 完成建立提供程式所需的步驟。
1. 最後，導覽至 ***[!DNL Channel access token]*** 區段，並複製 ***[!DNL Channel access token (long-lived)]*** 值 [驗證到目標](#authenticate) 步驟。

| 憑據 | 說明 | 範例 |
| --- | --- | --- |
| `[!DNL Channel access token (long-lived)]` | 您的 [!DNL LINE Channel access token (long-lived)]。 | `aaa2112XSMWqLXR7..........nyilFU=` |

請參閱 [[!DNL LINE] 檔案](https://developers.line.biz/en/docs/messaging-api/getting-started/) 以取得建立管道或將管道新增至現有管道的相關指引 [!DNL LINE] 帳戶 [!DNL LINE] 開發人員控制台。

## 支援的身分 {#supported-identities}

[!DNL LINE] 支援下表所述身分的更新和匯出。 深入了解 [身分](/help/identity-service/namespaces.md).

| Target身分 | 說明 |
|---|---|
| 廣告商的ID(IFA) | 當源標識為IFA時，選擇廣告商(IFA)的目標標識 *(廣告商專用Apple ID)* 或GAID *(Google Advertising ID)命名空間。 |
| 行用戶ID | 當源標識為LINE用戶ID時，選擇UserID目標標識。 |

## 匯出類型和頻率 {#export-type-frequency}

有關目標導出類型和頻率的資訊，請參閱下表。

| 項目 | 類型 | 附註 |
---------|----------|---------|
| 匯出類型 | **[!UICONTROL 設定檔]** | 您正在匯出區段（對象）的所有成員，其中包含 [!DNL LINE] 目的地。 |
| 匯出頻率 | **[!UICONTROL 串流]** | 串流目的地是「一律開啟」API型連線。 一旦根據區段評估在Experience Platform中更新設定檔，連接器就會將更新傳送至下游的目的地平台。 深入了解 [串流目的地](/help/destinations/destination-types.md#streaming-destinations). |

{style=&quot;table-layout:auto&quot;}

## 連接到目標 {#connect}

>[!IMPORTANT]
>
>若要連線至目的地，您需要 **[!UICONTROL 管理目的地]** [存取控制權限](/help/access-control/home.md#permissions). 閱讀 [存取控制概觀](/help/access-control/ui/overview.md) 或聯絡您的產品管理員以取得所需的權限。

若要連線至此目的地，請依照 [目的地設定教學課程](../../ui/connect-destination.md). 在設定目標工作流程中，填寫下列兩節所列的欄位。

內 **[!UICONTROL 目的地]** > **[!UICONTROL 目錄]** 搜尋 [!DNL LINE]. 或者，您也可以在 **[!UICONTROL 行動參與]** 類別。

### 驗證到目標 {#authenticate}

要驗證到目標，請選擇 **[!UICONTROL 連接到目標]**.
![Platform UI螢幕擷取畫面，顯示如何驗證。](../../assets/catalog/mobile-engagement/line/authenticate-destination.png)

填寫下方的必填欄位。
* **[!UICONTROL 承載令牌]**:您的 [!DNL LINE Channel access token (long-lived)] 從 [!DNL LINE] 開發人員控制台。 請參閱 [收集憑據](#gather-credentials) 區段。

如果提供的詳細資料有效，UI會顯示 **[!UICONTROL 已連接]** 狀態（帶綠色複選標籤）。 接著，您可以繼續進行下一個步驟。

### 填寫目的地詳細資訊 {#destination-details}

若要設定目的地的詳細資訊，請填寫下方的必填和選填欄位。 UI中欄位旁的星號表示該欄位為必要欄位。
![Platform UI螢幕擷取畫面，顯示目的地詳細資訊。](../../assets/catalog/mobile-engagement/line/destination-details.png)

* **[!UICONTROL 名稱]**:日後您將透過此名稱識別此目的地。
* **[!UICONTROL 說明]**:未來可協助您識別此目的地的說明。
* **[!UICONTROL 對象類型]**:選擇 **[!UICONTROL 廣告商的ID(IFA)]** 如果您要匯出的身分屬於 *廣告商的ID(IFA)*. 選擇 **[!UICONTROL LINE使用者ID]** 如果您要匯出的身分屬於 *行用戶ID*. 請參閱 [支援的身分](#supported-identities) 區段，以取得身分類型的詳細資訊。

### 啟用警報 {#enable-alerts}

您可以啟用警報，接收有關資料流到目標狀態的通知。 從清單中選擇要訂閱的警報，以接收有關資料流狀態的通知。 如需警報的詳細資訊，請參閱 [使用UI訂閱目的地警報](../../ui/alerts.md).

完成提供目標連接的詳細資訊後，請選擇 **[!UICONTROL 下一個]**.

## 啟用此目的地的區段 {#activate}

>[!IMPORTANT]
>
>若要啟用資料，您需要 **[!UICONTROL 管理目的地]**, **[!UICONTROL 啟動目的地]**, **[!UICONTROL 檢視設定檔]**，和 **[!UICONTROL 檢視區段]** [存取控制權限](/help/access-control/home.md#permissions). 閱讀 [存取控制概觀](/help/access-control/ui/overview.md) 或聯絡您的產品管理員以取得所需的權限。

閱讀 [啟動設定檔和區段至串流區段匯出目的地](/help/destinations/ui/activate-segment-streaming-destinations.md) 以取得啟用受眾區段至此目的地的指示。

### 對應屬性和身分 {#map}

若要將您的對象資料從Adobe Experience Platform正確傳送至 [!DNL LINE] 目的地，您必須執行欄位對應步驟。 對應包含在您的Platform帳戶中的Experience Data Model(XDM)結構欄位與目標目的地對應的欄位之間建立連結。 若要正確將XDM欄位對應至 [!DNL LINE] 目標欄位，請遵循下列步驟：

必鬚根據源標識映射以下目標標識命名空間： |目標身份 |源欄位 |目標欄位 | | — | — | — | |廣告商的ID(IFA) | `IDFA` 或 `GAID` | `LineId` | | LINE使用者ID | `UserID` | `LineId` |

如果您的目標身分識別 *LINE用戶ID* 您需要下列項目：
![平台UI螢幕擷取範例，顯示將LINE使用者ID用於目標身分識別時的Target對應。](../../assets/catalog/mobile-engagement/line/mappings-userid.png)

如果您的目標識別為 *廣告商的ID(IFA)* 您需要下列項目：
![Platform UI的螢幕擷取範例，顯示將ID用於廣告商(IFA)用於目標身分識別時的Target對應。](../../assets/catalog/mobile-engagement/line/mappings-idfa.png)

## 驗證資料匯出 {#exported-data}

成功匯出Experience Platform後， [!DNL LINE] 目的地會在內建立新對象 [!DNL LINE] 使用選取的區段名稱。

若要驗證您是否已正確設定目的地，請遵循下列步驟：

1. 在 [!DNL LINE]，登入 [Manager控制台](https://manager.line.biz/).

1. 接下來，導覽至 **[!UICONTROL 資料控制]** > **[!UICONTROL 對象]** 並檢查名稱與 **[!UICONTROL 對象名稱]** 欄。

1. 更新的卷數會符合區段內的計數。

1. 此 *類型* 欄將會提及 **[!UICONTROL UserID]** 如果您匯出的身分屬於 *UserID*. 同樣地， *類型* 欄將會提及 **[!UICONTROL 行動廣告Id]** 如果您匯出的身分屬於 *IDFA*.

內的範例設定 [!DNL LINE] 如下所示：
![LINE UI螢幕擷圖，顯示對象數量。](../../assets/catalog/mobile-engagement/line/audience-volume.png)

## 資料使用與控管 {#data-usage-governance}

全部 [!DNL Adobe Experience Platform] 處理資料時，目的地符合資料使用原則。 有關如何 [!DNL Adobe Experience Platform] 強制實施資料控管，請參閱 [資料控管概觀](/help/data-governance/home.md).
