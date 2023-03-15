---
title: Medallia連接
description: 啟用目標式Medalia調查和意見收集的設定檔，以便更清楚了解客戶需求和期望。
exl-id: 2c2766eb-7be1-418c-bf17-d119d244de92
source-git-commit: dd18350387aa6bdeb61612f0ccf9d8d2223a8a5d
workflow-type: tm+mt
source-wordcount: '1096'
ht-degree: 1%

---

# Medallia連接

## 總覽 {#overview}

啟用目標式Medalia調查和意見收集的設定檔，以便更清楚了解客戶需求和期望。

>[!IMPORTANT]
>
>此檔案頁面由Medallia團隊建立。 如有任何查詢或更新請求，請直接通過adobe-integrations@medallia.com聯繫。

## 使用案例 {#use-cases}

為協助您更清楚了解Medallia目的地的使用方式和時機，以下是Adobe Experience Platform客戶可借由使用此目的地解決的範例使用案例。

### 使用案例#1

B2B品牌希望評估並簡化其入門計畫。 他們想要將個人化調查即時傳送給剛完成上線程式的客戶。

### 使用案例#2

零售商希望更清楚了解客戶對訂單履行的偏好。 他們想要傳送簡短的1問簡訊調查給過去一個月進行線上和店內購買的客戶。

## 先決條件 {#prerequisites}

建立Medallia連線需要下列資訊：
* **OAuth代號端點URL**
* **用戶端ID**
* **用戶端密碼**
* **API閘道URL**
* **匯入API名稱**

請與您的Medallia傳送團隊合作，以取得這些詳細資訊。

## 支援的身分 {#supported-identities}

Medallia支援下表所述的身分識別啟用。 深入了解 [身分](/help/identity-service/namespaces.md).

| Target身分 | 說明 | 考量事項 |
|---|---|---|
| 電子郵件 | 電子郵件地址 | 當您要傳送電子郵件邀請調查時，請選取電子郵件目標身分。 當設定檔與多個電子郵件地址相關聯時，Medallia只會觸發第一封電子郵件的邀請。 |
| phone | 雜湊為E.164格式的電話號碼 | 當您要傳送SMS型調查時，請選取電話目標身分。 電話號碼必須為E.164格式，其中包括加號(+)、國際國家/地區呼叫代碼、本地區代碼和電話號碼。 例如：(+)（國家/地區代碼）（區號）（電話號碼）。 當設定檔與多個電話號碼相關聯時，Medallia只會觸發第一個電話號碼的邀請。 |

{style="table-layout:auto"}

## 匯出類型和頻率 {#export-type-frequency}

有關目標導出類型和頻率的資訊，請參閱下表。

| 項目 | 類型 | 附註 |
---------|----------|---------|
| 匯出類型 | **[!UICONTROL 設定檔]** | 您要匯出區段的所有新合格成員，以及所需的結構欄位(例如：電子郵件地址、電話號碼、姓氏)，如「選取設定檔屬性」畫面中所選 [目的地啟動工作流程](/help/destinations/ui/activate-batch-profile-destinations.md#select-attributes). |
| 匯出頻率 | **[!UICONTROL 串流]** | 串流目的地是「一律開啟」API型連線。 一旦根據區段評估在Experience Platform中更新設定檔，連接器就會將更新傳送至下游的目的地平台。 深入了解 [串流目的地](/help/destinations/destination-types.md#streaming-destinations). |

{style="table-layout:auto"}

## 連接到目標 {#connect}

>[!IMPORTANT]
> 
>若要連線至目的地，您需要 **[!UICONTROL 管理目的地]** [存取控制權限](/help/access-control/home.md#permissions). 閱讀 [存取控制概觀](/help/access-control/ui/overview.md) 或聯絡您的產品管理員以取得所需的權限。

若要連線至此目的地，請依照 [目的地設定教學課程](../../ui/connect-destination.md). 在設定目標工作流程中，填寫下列兩節所列的欄位。

### 驗證到目標 {#authenticate}

若要驗證目的地，請填寫必填欄位並選取 **[!UICONTROL 連接到目標]**.

* **[!UICONTROL OAuth代號端點URL]**:通常採用https://instance.medallia.tld/oauth/tenant/token的形式。
* **[!UICONTROL 用戶端ID]**:請向您的Medallia傳送團隊取得。
* **[!UICONTROL 用戶端密碼]**:請向您的Medallia傳送團隊取得。

![顯示此目標的驗證螢幕的影像。](/help/destinations/assets/catalog/voice/medallia-destination-oauth.png)

### 填寫目的地詳細資訊 {#destination-details}

若要設定目的地的詳細資訊，請填寫下方的必填和選填欄位。 UI中欄位旁的星號表示該欄位為必要欄位。

* **[!UICONTROL 名稱]**:日後您將透過此名稱識別此目的地。
* **[!UICONTROL 說明]**:未來可協助您識別此目的地的說明。
* **[!UICONTROL API閘道URL]**:請向您的Medallia傳送團隊取得。 通常採用https://instance-tenant.apis.medallia.com的形式。
* **[!UICONTROL 匯入API名稱]**:請向您的Medallia傳送團隊取得。 此連線中使用的Medallia匯入API（也稱為Web摘要）名稱。 您可以啟動不同區段至不同的匯入API，以觸發不同的調查程式。

![顯示此目標的目標詳細資訊螢幕的影像。](/help/destinations/assets/catalog/voice/medallia-destination-details.png)

### 啟用警報 {#enable-alerts}

您可以啟用警報，接收有關資料流到目標狀態的通知。 從清單中選擇要訂閱的警報，以接收有關資料流狀態的通知。 如需警報的詳細資訊，請參閱 [使用UI訂閱目的地警報](../../ui/alerts.md).

完成提供目標連接的詳細資訊後，請選擇 **[!UICONTROL 下一個]**.

## 啟用此目的地的區段 {#activate}

>[!IMPORTANT]
> 
>若要啟用資料，您需要 **[!UICONTROL 管理目的地]**, **[!UICONTROL 啟動目的地]**, **[!UICONTROL 檢視設定檔]**，和 **[!UICONTROL 檢視區段]** [存取控制權限](/help/access-control/home.md#permissions). 閱讀 [存取控制概觀](/help/access-control/ui/overview.md) 或聯絡您的產品管理員以取得所需的權限。

閱讀 [啟動設定檔和區段至串流區段匯出目的地](/help/destinations/ui/activate-segment-streaming-destinations.md) 以取得啟用受眾區段至此目的地的指示。

### 對應屬性和身分 {#map}

必鬚根據使用案例對應下列目標身分命名空間：
* 針對電子郵件型調查， **電子郵件** 必須以 **目標欄位** > **選取身分命名空間** > **電子郵件**
* 針對簡訊調查， **phone** 必須以 **目標欄位** > **選取身分命名空間** > **phone**. 電話號碼必須採用E.164格式，其中包括加號(+)、國際國家/地區呼叫代碼、本地區代碼和電話號碼

強烈建議您也對應其他目標自訂屬性，以建立個人化調查，並將客戶的其他相關資訊附加至調查記錄：

* 個人化調查通常會依名稱提供客戶資訊
   * 將客戶的名字對應至 **目標欄位** > **選取自訂屬性** > **屬性名稱** > **名字**
   * 將客戶的姓氏對應至 **目標欄位** > **選取自訂屬性** > **屬性名稱** > **lastname**
* 視需要為任何其他目標自訂屬性新增對應

![顯示身分和屬性之範例對應的影像。](/help/destinations/assets/catalog/voice/medallia-destination-mapping.png)

>[!IMPORTANT]
> 
> 與您的Medallia傳送團隊共用確切的 **屬性名稱** 使用 **目標欄位** > **選取自訂屬性** > **屬性名稱**. 您可能想要擷取要直接共用之對應頁面的螢幕擷圖。

## 匯出的資料 {#exported-data}

在您將區段啟動至目的地後，請通知您的Medallia傳送團隊，讓他們驗證從Adobe Experience Platform匯出至Medallia的資料。 請注意，調查只能在成功進行資料驗證後在Medallia內啟動；在此之前，資料會匯出至Medallia，但不會向客戶觸發調查。

匯出資料的範例JSON如下，此範例會使用螢幕擷取中的範例對應，位於 **對應屬性和身分** 小節：

```json
[
    {
        "profile_raw_encoded": "eyJhdHRyaWJ1dGVzIjp7ImZpcnN",
        "email": "johnsmith@example.com",
        "aep_segments_new": ["c1c3edcc-07cb-4f66-b5dd-aff485148aba"],
        "aep_segments_existing": [],
        "aep_segments_removed": [],
        "firstname":  “John” ,
        "lastname":  “Smith”,
        "contactId": "jsmith120002",
    }
]
```

## 資料使用與控管 {#data-usage-governance}

全部 [!DNL Adobe Experience Platform] 處理資料時，目的地符合資料使用原則。 有關如何 [!DNL Adobe Experience Platform] 強制實施資料控管，請參閱 [資料控管概觀](/help/data-governance/home.md).
