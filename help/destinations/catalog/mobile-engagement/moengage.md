---
title: Moengage連線
description: Moengage是客戶參與平台，可即時促進消費者與品牌之間以客戶為中心的互動。
last-substantial-update: 2023-10-11T00:00:00Z
exl-id: 051f1a10-3c41-4c0a-b187-bf80de0565f0
source-git-commit: 1b507e9846a74b7ac2d046c89fd7c27a818035ba
workflow-type: tm+mt
source-wordcount: '987'
ht-degree: 2%

---

# [!DNL Moengage] 連線

## 概觀 {#overview}

使用[!DNL Moengage]目的地來連線您的Adobe資料（使用者屬性、區段和事件），並將其對應至MoEngage即時處理。 然後，客戶可以對這些資料採取行動，提供個人化、鎖定目標的體驗。

透過Adobe，整合非常簡單且直覺。 只需取用任何Adobe使用者設定檔，並將其對應至MoEngage使用者屬性即可。

>[!IMPORTANT]
>
>此目的地聯結器和檔案頁面是由&#x200B;*Moengage*&#x200B;團隊建立和維護。 若有任何查詢或更新要求，請直接在&#x200B;*`https://help.moengage.com/hc/en-us`.*&#x200B;聯絡他們

## 使用案例 {#use-cases}

行銷人員想要透過[!DNL Moengage]行銷活動鎖定使用者區段(內建於Adobe Experience Platform)。 此外，他們還想根據Adobe Experience Platform設定檔中的屬性來個人化促銷活動內容。 透過這項整合，只要在Adobe Experience Platform中更新區段和設定檔，使用者和屬性就會在MoEngage中更新。

## 先決條件 {#prerequisites}

在將Adobe Experience Platform資料傳送至[!DNL Moengage]之前，請注意下列必要條件：

* 若要搭配Adobe Experience Platform使用MoEngage目的地，使用者必須先擁有其[!DNL Moengage]帳戶的存取權。 請造訪以下頁面以註冊或登入您的MoEngage帳戶： https://app.moengage.com


## 支援的身分 {#supported-identities}

[!DNL Moengage]支援下表所述的身分啟用。

| 目標身分 | 說明 | 考量事項 |
|---|------------------------------------------------------------------------------------------|----------------------------------------------------------------------------------------|
| user_id | 在[!DNL Moengage]系統中唯一識別使用者設定檔的唯一識別碼。 | 此識別碼支援字串型別。 需要user_id或anonymous_id其中之一 |
| anonymous_id | 未知使用者設定檔的另一個識別碼，表示系統中不存在的設定檔。 | 此識別碼支援字串型別。 需要user_id或anonymous_id其中之一 |

{style="table-layout:auto"}

## 匯出型別和頻率 {#export-type-frequency}

請參閱下表以取得目的地匯出型別和頻率的資訊。

| 項目 | 類型 | 附註 |
|---------|----------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| 匯出類型 | **[!UICONTROL Profile-based]** | 您正在匯出區段（受眾）的所有成員，其中包含識別碼(user_id、anonymous_id)以及您匯出至[!DNL Moengage]所定義的自訂屬性。 |
| 匯出頻率 | **[!UICONTROL Streaming]** | 串流目的地是「一律開啟」的API型連線。 一旦根據區段評估在Experience Platform中更新了設定檔，聯結器就會將更新傳送至下游的目標平台。 深入瞭解[串流目的地](/help/destinations/destination-types.md#streaming-destinations)。 |

{style="table-layout:auto"}

## 連線到目標 {#connect}

>[!IMPORTANT]
> 
>若要連線到目的地，您需要&#x200B;**[!UICONTROL View Destinations]**&#x200B;和&#x200B;**[!UICONTROL Manage Destinations]** [存取控制許可權](/help/access-control/home.md#permissions)。 閱讀[存取控制總覽](/help/access-control/ui/overview.md)或連絡您的產品管理員以取得必要的許可權。

若要連線到此目的地，請依照[目的地組態教學課程](../../ui/connect-destination.md)中所述的步驟進行。 在設定目標工作流程中，填寫以下兩個區段中列出的欄位。

### 驗證目標 {#authenticate}

若要驗證到目的地，請填寫必填欄位並選取&#x200B;**[!UICONTROL Connect to destination]**。

![Moengage目的地驗證](../../assets/catalog/mobile-engagement/moengage/authentication.png)

### 填寫目標詳細資料 {#destination-details}

若要設定目的地的詳細資訊，請填寫下方的必填和選用欄位。 UI中欄位旁的星號表示該欄位為必填欄位。
![Moengage目的地驗證](../../assets/catalog/mobile-engagement/moengage/settings.png)

* **[!UICONTROL USERNAME]**： [!DNL Moengage]儀表板的設定頁面的資料應用程式識別碼。
* **[!UICONTROL PASSWORD]**： [!DNL Moengage]儀表板的設定頁面中的資料應用程式金鑰。

![Moengage目的地驗證](../../assets/catalog/mobile-engagement/moengage/destination_details.png)

* **[!UICONTROL Name]**：您日後可辨識此目的地的名稱。
* **[!UICONTROL Description]**：可協助您日後識別此目的地的說明。
* **[!UICONTROL Region]**：您的應用程式&#x200B;*資料中心*。

### 啟用警示 {#enable-alerts}

您可以啟用警報以接收有關傳送到您目的地的資料流狀態的通知。 從清單中選取警報以訂閱接收有關資料流狀態的通知。 如需警示的詳細資訊，請參閱[使用UI訂閱目的地警示](../../ui/alerts.md)的指南。

當您完成提供目的地連線的詳細資訊時，請選取&#x200B;**[!UICONTROL Next]**。

## 啟用此目的地的區段 {#activate}

>[!IMPORTANT]
> 
>若要啟用資料，您需要&#x200B;**[!UICONTROL View Destinations]**、**[!UICONTROL Activate Destinations]**、**[!UICONTROL View Profiles]**&#x200B;和&#x200B;**[!UICONTROL View Segments]** [存取控制許可權](/help/access-control/home.md#permissions)。 閱讀[存取控制總覽](/help/access-control/ui/overview.md)或連絡您的產品管理員以取得必要的許可權。

如需啟用此目的地的對象區段的指示，請參閱[啟用串流區段匯出目的地的對象資料](../../ui/activate-segment-streaming-destinations.md)。

### 對應屬性和身分 {#map}

若要將對象資料從[!DNL Adobe Experience Platform]正確傳送至[!DNL Moengage]目的地，您必須完成欄位對應步驟。

對應包括在[!DNL Experience Data Model]帳戶中的[!DNL Experience Platform] (XDM)結構描述欄位之間建立連結，以及從目標目的地建立對應對應專案。

若要將您的XDM欄位正確對應到[!DNL Moengage]目的地欄位，請遵循下列步驟：

在[!UICONTROL Mapping]步驟中，選取&#x200B;**[!UICONTROL Checkbox]**。

![Moengage目的地新增對應](../../assets/catalog/mobile-engagement/moengage/segments.png)

在[!UICONTROL Mapping]步驟中，選取&#x200B;**[!UICONTROL Add new mapping]**。

![Moengage目的地新增對應](../../assets/catalog/mobile-engagement/moengage/mapping.png)

在[!UICONTROL Source Field]區段中，選取空白欄位旁的箭頭按鈕。

![Moengage目的地Source對應](../../assets/catalog/mobile-engagement/moengage/mapping-source.png)

在[!UICONTROL Select source field]視窗中，您可以在兩種類別的XDM欄位之間進行選擇：

* [!UICONTROL Select attributes]：使用此選項將特定欄位從您的XDM結構描述對應到[!DNL Moengage]屬性。

![Moengage目的地對應Source屬性](../../assets/catalog/mobile-engagement/moengage/mapping-attributes.png)

選擇您的來源欄位，然後選取&#x200B;**[!UICONTROL Select]**。

在[!UICONTROL Target Field]區段中，選取欄位右側的對應圖示。

![移動目的地目標對應](../../assets/catalog/mobile-engagement/moengage/mapping-target.png)

在[!UICONTROL Select target field]視窗中，您可以選擇兩種目標欄位類別：

* [!UICONTROL Select identity namespace]：使用此選項將[!DNL Experience Platform]個身分識別名稱空間對應至[!DNL Moengage]個身分識別名稱空間。
* [!UICONTROL Select custom attributes]：使用此選項將XDM屬性對應到您在[!DNL Moengage]帳戶中定義的自訂[!DNL Moengage]屬性。 <br>您也可以使用此選項將現有的XDM屬性重新命名為[!DNL Moengage]。 例如，將`lastName` XDM屬性對應至`Last_Name`中的自訂[!DNL Moengage]屬性，將在`Last_Name`中建立[!DNL Moengage]屬性（如果尚未存在），並將`lastName` XDM屬性對應至該屬性。

![Moengage目的地目標對應欄位](../../assets/catalog/mobile-engagement/moengage/mapping-target-fields.png)

選擇您的目標欄位，然後選取&#x200B;**[!UICONTROL Select]**。

您現在應該會在清單中看到您的欄位對應。

![Moengage目的地對應完成](../../assets/catalog/mobile-engagement/moengage/mapping-complete.png)

若要新增更多對應，請重複上述步驟。

## 匯出的資料/驗證資料匯出 {#exported-data}

若要驗證資料是否已成功匯出至[!DNL Moengage]目的地，請移至[!DNL Moengage]帳戶中的使用者設定檔。 在這裡，您應該找到名為`AEPSegments`的使用者屬性（已自動建立），以及已在Adobe Experience Platform中先前步驟中對應的其他自訂屬性。

`AEPSegments`是[!DNL Moengage]中的陣列型別屬性。 其中會列出使用者在Experience Platform中與之相關聯的所有Adobe對象名稱。


![Moengage目的地對應完成](../../assets/catalog/mobile-engagement/moengage/validation.png)

## 資料使用與控管 {#data-usage-governance}

處理您的資料時，所有[!DNL Adobe Experience Platform]目的地都符合資料使用原則。 如需[!DNL Adobe Experience Platform]如何強制資料控管的詳細資訊，請閱讀[資料控管概觀](/help/data-governance/home.md)。
