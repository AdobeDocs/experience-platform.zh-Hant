---
title: Medallia連線
description: 針對目標Medallia調查和意見回饋收集啟用設定檔，以更好地瞭解客戶需求和期望。
exl-id: 2c2766eb-7be1-418c-bf17-d119d244de92
source-git-commit: ba39f62cd77acedb7bfc0081dbb5f59906c9b287
workflow-type: tm+mt
source-wordcount: '1135'
ht-degree: 2%

---

# Medallia連線

## 概觀 {#overview}

針對目標Medallia調查和意見回饋收集啟用設定檔，以更好地瞭解客戶需求和期望。

>[!IMPORTANT]
>
>此目的地聯結器和檔案頁面是由Medallia團隊建立和維護的。 如有任何查詢或更新要求，請直接透過adobe-integrations@medallia.com聯絡。

## 使用案例 {#use-cases}

為協助您更清楚瞭解如何使用Medallia目的地，以下是Adobe Experience Platform客戶可使用此目的地解決的範例使用案例。

### 使用案例#1

B2B品牌想要評估並簡化其上線計畫。 他們想要將個人化調查即時傳送給剛完成入門流程的客戶。

### 使用案例#2

零售商想要更瞭解客戶對訂單履行情況的偏好設定。 他們想要傳送簡短的1題SMS調查，給過去一個月曾經線上上和店內購買過的客戶。

## 先決條件 {#prerequisites}

建立Medallia連線需要下列資訊：
* **OAuth權杖端點URL**
* **使用者端識別碼**
* **使用者端密碼**
* **API閘道URL**
* **匯入API名稱**

請與您的Medallia傳送團隊合作，以取得這些詳細資料。

## 支援的身分 {#supported-identities}

Medallia支援下表所述的身分啟用。 深入瞭解[身分](/help/identity-service/features/namespaces.md)。

| 目標身分 | 說明 | 考量事項 |
|---|---|---|
| 電子郵件 | 電子郵件地址 | 當您想要傳送電子郵件邀請調查時，請選取電子郵件目標身分。 當設定檔與多個電子郵件地址關聯時，Medallia只會觸發第一個電子郵件的邀請。 |
| 電話 | 以E.164格式雜湊的電話號碼 | 當您想要傳送簡訊型調查時，請選取電話目標身分識別。 電話號碼必須是E.164格式，其中包括加號(+)、國際國家/地區撥號代碼、當地區碼和電話號碼。 例如：(+)（國家代碼）（區號）（電話號碼）。 當設定檔與多個電話號碼關聯時，Medallia只會觸發第一個電話號碼的邀請。 |

{style="table-layout:auto"}

## 匯出型別和頻率 {#export-type-frequency}

請參閱下表以取得目的地匯出型別和頻率的資訊。

| 項目 | 類型 | 附註 |
---------|----------|---------|
| 匯出類型 | **[!UICONTROL 以設定檔為基礎]** | 您正在匯出區段的所有新合格成員，以及所需的結構描述欄位（例如：電子郵件地址、電話號碼、姓氏），如[目的地啟用工作流程](/help/destinations/ui/activate-batch-profile-destinations.md#select-attributes)的選取設定檔屬性畫面中所選。 |
| 匯出頻率 | **[!UICONTROL 串流]** | 串流目的地是「一律開啟」的API型連線。 一旦根據對象評估在Experience Platform中更新了設定檔，聯結器就會將更新傳送至下游的目的地平台。 深入瞭解[串流目的地](/help/destinations/destination-types.md#streaming-destinations)。 |

{style="table-layout:auto"}

## 連線到目標 {#connect}

>[!IMPORTANT]
> 
>若要連線到目的地，您需要&#x200B;**[!UICONTROL 檢視目的地]**&#x200B;和&#x200B;**[!UICONTROL 管理目的地]** [存取控制許可權](/help/access-control/home.md#permissions)。 閱讀[存取控制總覽](/help/access-control/ui/overview.md)或連絡您的產品管理員以取得必要的許可權。

若要連線到此目的地，請依照[目的地組態教學課程](../../ui/connect-destination.md)中所述的步驟進行。 在設定目標工作流程中，填寫以下兩個區段中列出的欄位。

### 驗證目標 {#authenticate}

若要驗證到目的地，請填入必填欄位，然後選取&#x200B;**[!UICONTROL 連線到目的地]**。

* **[!UICONTROL OAuth權杖端點URL]**：通常採用https://instance.medallia.tld/oauth/tenant/token的形式。
* **[!UICONTROL 使用者端識別碼]**：從您的Medallia傳遞團隊取得。
* **[!UICONTROL 使用者端密碼]**：從您的Medallia傳遞團隊取得。

![顯示這個目的地之驗證畫面的影像。](/help/destinations/assets/catalog/voice/medallia-destination-oauth.png)

### 填寫目標詳細資訊 {#destination-details}

若要設定目的地的詳細資訊，請填寫下方的必填和選用欄位。 UI中欄位旁的星號表示該欄位為必填欄位。

* **[!UICONTROL 名稱]**：您日後可辨識此目的地的名稱。
* **[!UICONTROL 描述]**：可協助您日後識別此目的地的描述。
* **[!UICONTROL API閘道URL]**：從您的Medallia傳遞團隊取得。 通常採用https://instance-tenant.apis.medallia.com的形式。
* **[!UICONTROL 匯入API名稱]**：從您的Medallia傳遞團隊取得。 用於此連線的Medallia Import API （也稱為Web摘要）名稱。 您可以對不同的匯入API啟用不同的對象，以觸發不同的調查計畫。

![顯示這個目的地之目的地詳細資訊畫面的影像。](/help/destinations/assets/catalog/voice/medallia-destination-details.png)

### 啟用警示 {#enable-alerts}

您可以啟用警報以接收有關傳送到您目的地的資料流狀態的通知。 從清單中選取警報以訂閱接收有關資料流狀態的通知。 如需警示的詳細資訊，請參閱[使用UI訂閱目的地警示](../../ui/alerts.md)的指南。

當您完成提供目的地連線的詳細資訊後，請選取&#x200B;**[!UICONTROL 下一步]**。

## 啟動此目標的對象 {#activate}

>[!IMPORTANT]
> 
>* 若要啟用資料，您需要&#x200B;**[!UICONTROL 檢視目的地]**、**[!UICONTROL 啟用目的地]**、**[!UICONTROL 檢視設定檔]**&#x200B;和&#x200B;**[!UICONTROL 檢視區段]** [存取控制許可權](/help/access-control/home.md#permissions)。 閱讀[存取控制總覽](/help/access-control/ui/overview.md)或連絡您的產品管理員以取得必要的許可權。
>* 若要匯出&#x200B;*身分*，您需要&#x200B;**[!UICONTROL 檢視身分圖表]** [存取控制許可權](/help/access-control/home.md#permissions)。<br> ![選取工作流程中反白的身分名稱空間，以啟用目的地的對象。](/help/destinations/assets/overview/export-identities-to-destination.png "選取工作流程中反白顯示的身分名稱空間，以啟用目的地的對象。"){width="100" zoomable="yes"}

閱讀[將設定檔和對象啟用至串流對象匯出目的地](/help/destinations/ui/activate-segment-streaming-destinations.md)，以瞭解啟用此目的地對象的指示。

### 對應屬性和身分 {#map}

下列目標身分名稱空間必須根據使用案例進行對應：
* 對於電子郵件調查，**電子郵件**&#x200B;必須使用&#x200B;**目標欄位** > **選取身分名稱空間** > **電子郵件**&#x200B;對應為目標欄位
* 對於以簡訊為基礎的調查，**電話**&#x200B;必須使用&#x200B;**目標欄位** > **選取身分名稱空間** > **電話**&#x200B;對應為目標欄位。 電話號碼必須是E.164格式，其中包括加號(+)、國際國家/地區撥號代碼、當地區碼和電話號碼

強烈建議您也對應其他目標自訂屬性，以建立個人化調查，並將有關客戶的額外資訊附加至調查記錄：

* 個人化調查通常會依名稱為客戶提供服務
   * 將客戶的名字對應至&#x200B;**目標欄位** > **選取自訂屬性** > **屬性名稱** > **名字**
   * 將客戶的姓氏對應至&#x200B;**目標欄位** > **選取自訂屬性** > **屬性名稱** > **姓氏**
* 視需要新增任何其他目標自訂屬性的對應

![顯示身分和屬性範例對應的影像。](/help/destinations/assets/catalog/voice/medallia-destination-mapping.png)

>[!IMPORTANT]
> 
> 使用&#x200B;**目標欄位** > **選取自訂屬性** > **屬性名稱**，與您的Medallia傳遞團隊共用每個對應目標自訂屬性的確切&#x200B;**屬性名稱**。 您可能希望直接分享對應頁面的熒幕擷圖。

## 匯出的資料 {#exported-data}

一旦您將區段啟動至目的地，請通知您的Medallia傳送團隊，以便他們驗證從Adobe Experience Platform匯出至Medallia的資料。 請注意，調查只能在資料驗證成功後於Medallia中啟動；在此之前，資料將匯出至Medallia，但不會向客戶觸發調查。

以下提供匯出資料的JSON範例，此範例使用上述&#x200B;**對應屬性和身分**&#x200B;區段中的熒幕擷圖中的對應：

```json
[
    {
        "profile_raw_encoded": "eyJhdHRyaWJ1dGVzIjp7ImZpcnN",
        "email": "johnsmith@example.com",
        "aep_segments_new": ["c1c3edcc-07cb-4f66-b5dd-aff485148aba"],
        "aep_segments_existing": [],
        "aep_segments_removed": [],
        "firstname":  "John" ,
        "lastname":  "Smith",
        "contactId": "jsmith120002",
    }
]
```

## 資料使用與控管 {#data-usage-governance}

處理您的資料時，所有[!DNL Adobe Experience Platform]目的地都符合資料使用原則。 如需[!DNL Adobe Experience Platform]如何強制資料控管的詳細資訊，請參閱[資料控管概觀](/help/data-governance/home.md)。
