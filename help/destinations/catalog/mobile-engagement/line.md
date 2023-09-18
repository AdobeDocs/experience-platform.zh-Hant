---
keywords: 行動；行動參與目的地；LINE；LINE行動參與目的地
title: LINE連線
description: LINE目的地可讓您新增設定檔至平台對象，並為連線的使用者提供個人化體驗。
last-substantial-update: 2022-11-08T00:00:00Z
exl-id: 9981798a-61f2-4a09-9a33-57e63eb36d43
source-git-commit: 05e996f9e33e0d8be3d15a9ab3baaaf6d8152b5a
workflow-type: tm+mt
source-wordcount: '1214'
ht-degree: 0%

---

# [!DNL LINE] 連線

## 概觀 {#overview}

[[!DNL LINE]](https://line.me/en/) 是一個連線人物、服務和資訊的常用通訊平台，並且已從聊天應用程式成長為娛樂、社交和日常活動的中樞。

這個 [!DNL Adobe Experience Platform] [目的地](/help/destinations/home.md) 可運用 [[!DNL LINE] 傳訊API](https://developers.line.biz/en/reference/messaging-api/). 您可以從您的Experience Platform對象中啟用設定檔，作為內的連線 [!DNL LINE] 滿足您的業務需求。

[!DNL LINE] 使用持有人權杖作為驗證機制，以與 [!DNL LINE] 傳訊API。 向您的驗證指示 [!DNL LINE] 執行個體顯示於以下更深入的 [驗證到目的地](#authenticate) 區段。

## 使用案例 {#use-cases}

行銷人員可以鎖定行動參與目的地中的使用者，並內建受眾 [!DNL Adobe Experience Platform]. 此外，您也可以根據客戶自己的屬性，為他們提供個人化體驗 [!DNL Adobe Experience Platform] 設定檔，當對象和設定檔在中更新時 [!DNL Adobe Experience Platform].

## 先決條件 {#prerequisites}

### [!DNL LINE] 必備條件 {#prerequisites-destination}

請注意中的下列必要條件 [!DNL LINE]，以將資料從Platform匯出至 [!DNL LINE] 帳戶：

#### 您需要擁有 [!DNL LINE] 帳戶 {#prerequisites-account}

您必須註冊並建立 [!DNL LINE] 帳戶（如果尚未擁有）。 若要建立帳戶：

1. 導覽至 [!DNL LINE] [帳戶登入](https://account.line.biz/login?redirectUri=https%3A%2F%2Fmanager.line.biz%2F) 頁面
2. 選取 **[!UICONTROL 建立帳戶]**.

#### 收集 [!DNL LINE channel access token (long-lived)] 從 [!DNL LINE] 開發人員主控台 {#gather-credentials}

允許平台存取 [!DNL LINE] 資源，您需要 *[!DNL Channel access token (long-lived)]* 從所需 [!DNL LINE] *傳訊API* 頻道。

1. 使用您的帳戶登入 [!DNL LINE] 帳戶至 [[!DNL LINE] 開發人員主控台](https://developers.line.biz/console).
1. 接下來，存取 *[!DNL Providers]* 清單，然後選取 *[!DNL Provider]* ，最後選取 *傳訊API* 存取其設定的管道。 如果您是第一次存取開發人員主控台，請遵循 [[!DNL LINE] 檔案](https://developers.line.biz/en/docs/messaging-api/getting-started/) 完成建立提供者所需的步驟。
1. 最後，導覽至 ***[!DNL Channel access token]*** 區段並複製 ***[!DNL Channel access token (long-lived)]*** 以下範圍內所需的值： [驗證到目的地](#authenticate) 步驟。

| 認證 | 說明 | 範例 |
| --- | --- | --- |
| `[!DNL Channel access token (long-lived)]` | 您的 [!DNL LINE Channel access token (long-lived)]。 | `aaa2112XSMWqLXR7..........nyilFU=` |

請參閱 [[!DNL LINE] 檔案](https://developers.line.biz/en/docs/messaging-api/getting-started/) ，以取得建立管道或將管道新增至現有管道的指引 [!DNL LINE] 帳戶透過 [!DNL LINE] 開發人員主控台。

## 支援的身分 {#supported-identities}

[!DNL LINE] 支援下表中描述的身分更新和匯出。 進一步瞭解 [身分](/help/identity-service/namespaces.md).

| 目標身分 | 說明 |
|---|---|
| 廣告商ID (IFA) | 當來源身分是IFA時，選取廣告商(IFA)目標身分的ID *(廣告商適用的Apple ID)* 或GAID *(Google Advertising ID)名稱空間。 |
| LINE使用者ID | 當來源身分識別為LINE使用者ID時，選取UserID目標身分。 |

## 匯出型別和頻率 {#export-type-frequency}

請參閱下表以取得目的地匯出型別和頻率的資訊。

| 項目 | 類型 | 附註 |
---------|----------|---------|
| 匯出型別 | **[!UICONTROL 以設定檔為基礎]** | 您正在匯出某個對象的所有成員，而這些成員中都有用於的識別碼（名稱、電話號碼或其他）。 [!DNL LINE] 目的地。 |
| 匯出頻率 | **[!UICONTROL 串流]** | 串流目的地是「一律開啟」的API型連線。 一旦根據對象評估在Experience Platform中更新了設定檔，聯結器就會將更新傳送至下游的目的地平台。 深入瞭解 [串流目的地](/help/destinations/destination-types.md#streaming-destinations). |

{style="table-layout:auto"}

## 連線到目的地 {#connect}

>[!IMPORTANT]
>
>若要連線到目的地，您需要 **[!UICONTROL 管理目的地]** [存取控制許可權](/help/access-control/home.md#permissions). 閱讀 [存取控制總覽](/help/access-control/ui/overview.md) 或聯絡您的產品管理員以取得必要許可權。

若要連線至此目的地，請遵循以下說明的步驟： [目的地設定教學課程](../../ui/connect-destination.md). 在設定目標工作流程中，填寫以下兩個區段中列出的欄位。

範圍 **[!UICONTROL 目的地]** > **[!UICONTROL 目錄]** 搜尋 [!DNL LINE]. 或者，您可以在 **[!UICONTROL 行動參與]** 類別。

### 驗證到目的地 {#authenticate}

若要驗證目的地，請選取 **[!UICONTROL 連線到目的地]**.
![顯示如何驗證的平台UI熒幕擷圖。](../../assets/catalog/mobile-engagement/line/authenticate-destination.png)

填寫以下必填欄位。
* **[!UICONTROL 持有人權杖]**：您的 [!DNL LINE Channel access token (long-lived)] 從 [!DNL LINE] 開發人員主控台。 請參閱 [收集認證](#gather-credentials) 區段。

如果提供的詳細資料有效，UI會顯示 **[!UICONTROL 已連線]** 帶有綠色勾號的狀態。 然後您可以繼續下一步驟。

### 填寫目的地詳細資料 {#destination-details}

若要設定目的地的詳細資訊，請填寫下方的必填和選用欄位。 UI中欄位旁的星號表示該欄位為必填欄位。
![顯示目的地詳細資訊的平台UI熒幕擷圖。](../../assets/catalog/mobile-engagement/line/destination-details.png)

* **[!UICONTROL 名稱]**：您日後可辨識此目的地的名稱。
* **[!UICONTROL 說明]**：可協助您日後識別此目的地的說明。
* **[!UICONTROL 對象型別]**：選取 **[!UICONTROL 廣告商ID (IFA)]** 如果您要匯出的身分屬於型別 *廣告商ID (IFA)*. 選取 **[!UICONTROL LINE使用者ID]** 如果您要匯出的身分屬於型別 *LINE使用者ID*. 請參閱 [支援的身分](#supported-identities) 區段，以取得身分型別的詳細資訊。

### 啟用警示 {#enable-alerts}

您可以啟用警報以接收有關傳送到您目的地的資料流狀態的通知。 從清單中選取警報以訂閱接收有關資料流狀態的通知。 如需警示的詳細資訊，請參閱以下指南： [使用UI訂閱目的地警報](../../ui/alerts.md).

當您完成提供目的地連線的詳細資訊時，請選取「 」 **[!UICONTROL 下一個]**.

## 啟用此目的地的對象 {#activate}

>[!IMPORTANT]
> 
>* 若要啟用資料，您需要 **[!UICONTROL 管理目的地]**， **[!UICONTROL 啟用目的地]**， **[!UICONTROL 檢視設定檔]**、和 **[!UICONTROL 檢視區段]** [存取控制許可權](/help/access-control/home.md#permissions). 閱讀 [存取控制總覽](/help/access-control/ui/overview.md) 或聯絡您的產品管理員以取得必要許可權。
>* 要匯出 *身分*，您需要 **[!UICONTROL 檢視身分圖表]** [存取控制許可權](/help/access-control/home.md#permissions). <br> ![選取工作流程中反白顯示的身分名稱空間，以將對象啟用至目的地。](/help/destinations/assets/overview/export-identities-to-destination.png "選取工作流程中反白顯示的身分名稱空間，以將對象啟用至目的地。"){width="100" zoomable="yes"}

讀取 [將設定檔和受眾啟用至串流受眾匯出目標](/help/destinations/ui/activate-segment-streaming-destinations.md) 以取得啟用此目的地對象的指示。

### 對應屬性和身分 {#map}

若要正確將對象資料從Adobe Experience Platform傳送至 [!DNL LINE] 目的地，您必須進行欄位對應步驟。 對應包括在Platform帳戶中的Experience Data Model (XDM)結構描述欄位與來自目標目的地的對應對應專案之間建立連結。 若要正確將XDM欄位對應至 [!DNL LINE] 目的地欄位，請遵循下列步驟：

根據您的來源身分，必須對應以下目標身分名稱空間： |目標身分 |來源欄位 |目標欄位 | | — | — | — | |廣告商ID (IFA) | `IDFA` 或 `GAID` | `LineId` | | LINE使用者ID | `UserID` | `LineId` |

如果您的目標身分是 *LINE使用者ID* 您將需要下列專案：
![Platform UI熒幕擷圖範例，顯示將LINE使用者ID用於目標身分識別時的Target對應。](../../assets/catalog/mobile-engagement/line/mappings-userid.png)

如果您的目標身分是 *廣告商ID (IFA)* 您將需要下列專案：
![平台UI熒幕擷圖範例顯示將廣告商(IFA)的ID用於目標身分識別時的Target對應。](../../assets/catalog/mobile-engagement/line/mappings-idfa.png)

## 驗證資料匯出 {#exported-data}

成功將資料匯出出Experience Platform後， [!DNL LINE] 目的地會在中建立新對象 [!DNL LINE] 使用選取的對象名稱。

若要驗證您是否已正確設定目的地，請遵循下列步驟：

1. 在 [!DNL LINE]，登入 [管理員主控台](https://manager.line.biz/).

1. 接下來，導覽至 **[!UICONTROL 資料控制項]** > **[!UICONTROL 受眾]** ，並檢查 **[!UICONTROL 對象名稱]** 欄。

1. 更新的磁碟區會符合區段內的計數。

1. 此 *型別* 欄將提及 **[!UICONTROL 使用者ID]** 如果您匯出的身分屬於型別 *使用者ID*. 同樣地， *型別* 欄將提及 **[!UICONTROL 行動廣告ID]** 如果您匯出的身分屬於型別 *IDFA*.

中的設定範例 [!DNL LINE] 如下所示：
![LINE UI熒幕擷圖顯示對象數量。](../../assets/catalog/mobile-engagement/line/audience-volume.png)

## 資料使用與控管 {#data-usage-governance}

全部 [!DNL Adobe Experience Platform] 處理您的資料時，目的地符合資料使用原則。 如需如何操作的詳細資訊 [!DNL Adobe Experience Platform] 強制執行資料控管，請參閱 [資料控管概觀](/help/data-governance/home.md).
