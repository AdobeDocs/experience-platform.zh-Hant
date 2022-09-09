---
title: 檔案自助服務範本//以目的地名稱取代
description: 使用此範本，在Adobe Experience Platform目錄中為您的目的地建立公開檔案。//將取代為概述區段中的段落
exl-id: 99700474-8bf6-4176-acc1-38814e17c995
source-git-commit: 788c02622b5176b41eb6da70bed0994d4824c984
workflow-type: tm+mt
source-wordcount: '1452'
ht-degree: 1%

---

# YourDestination連線 {#your-destination}

*瀏覽此模板時，替換或刪除所有斜體段落（從此模板開始）。*

*首先，請更新頁面頂端的中繼資料（標題和說明）。 請忽略此頁上的所有UICONTROL實例。 這個標籤可協助我們的機器翻譯程式將頁面正確翻譯成我們支援的多種語言。 在您提交檔案後，我們會為其新增標籤。*

>[!IMPORTANT]
>
>* 按照模板中概述的順序填入此模板中的所有部分。
>* 根據合作夥伴的意見，此範本不常更新。 開始編寫目的地的檔案之前，請確定您已下載 [最新版範本](/help/destinations/destination-sdk/docs-framework/assets/yourdestination-template.zip).


## 總覽 {#overview}

*提供您公司的簡短概觀，包括為客戶提供的價值。 加入產品檔案首頁的連結，以供進一步閱讀。*

>[!IMPORTANT]
>
>本檔案頁面由 *YourDestination* 團隊。 如有任何查詢或更新請求，請直接與他們聯繫，地址為 *插入連結或電子郵件地址，以便您可以在此處獲得更新 `support@YourDestination.com`.*

## 使用案例 {#use-cases}

以協助您更清楚了解應如何及何時使用 *YourDestination* 目的地，以下是Adobe Experience Platform客戶可透過此目的地解決的範例使用案例。

### 使用案例#1 {#use-case-1}

*針對行動訊息平台：*

*一個房屋租賃與銷售平台想要向客戶的Android和iOS裝置推播行動通知，讓他們知道，他們之前在尋找租房的地區有100個更新清單。*

### 使用案例#2 {#use-case-2}

*針對社交網路平台：*

*運動服裝品牌想透過其社交媒體帳戶觸及現有客戶。 服飾品牌可將自己的CRM電子郵件地址擷取至Adobe Experience Platform、從自己的離線資料建立區段，並將這些區段傳送至您的目的地，以在客戶的社交媒體摘要中顯示廣告。*

## 先決條件 {#prerequisites}

*在本節中新增客戶開始在Adobe Experience Platform使用者介面中設定目的地前，需要注意之事項的相關資訊。 這可以是：*

* *需要添加到允許清單*
* *電子郵件雜湊要求*
* *任何你方的賬戶細節*
* *如何取得API金鑰以連線至您的平台*

*如果這對客戶有用，您可以連結至相關檔案。*

## 支援的身分 {#supported-identities}

*在本節中新增目的地所支援身分的相關資訊。 我們已預先填入一些標準值。 刪除未套用至您目的地的值，以及任何未預填的值。*

*YourDestination* 支援啟用下表所述的身分。 深入了解 [身分](/help/identity-service/namespaces.md).

| Target身分 | 說明 | 考量事項 |
|---|---|---|
| GAID | Google Advertising ID | 當源標識為GAID命名空間時，選擇GAID目標標識。 |
| IDFA | Apple ID for Advertisers | 如果來源識別為IDFA命名空間，請選取IDFA目標識別。 |
| ECID | Experience Cloud ID | 代表ECID的命名空間。 此命名空間也可由下列別名引用：&quot;Adobe Marketing Cloud ID&quot;、&quot;Adobe Experience Cloud ID&quot;、&quot;Adobe Experience Platform ID&quot;。 請參閱下列檔案，內容如下 [ECID](/help/identity-service/ecid.md) 以取得更多資訊。 |
| phone_sha256 | 使用SHA256演算法雜湊的電話號碼 | Adobe Experience Platform支援純文字和SHA256雜湊電話號碼。 當來源欄位包含未雜湊屬性時，請檢查 **[!UICONTROL 套用轉換]** 選項，必須 [!DNL Platform] 啟動時自動雜湊資料。 |
| email_lc_sha256 | 使用SHA256演算法雜湊的電子郵件地址 | Adobe Experience Platform支援純文字和SHA256雜湊電子郵件地址。 當來源欄位包含未雜湊屬性時，請檢查 **[!UICONTROL 套用轉換]** 選項，必須 [!DNL Platform] 啟動時自動雜湊資料。 |
| extern_id | 自訂使用者ID | 當源標識為自定義命名空間時，選擇此目標標識。 |

{style=&quot;table-layout:auto&quot;}

## 匯出類型和頻率 {#export-type-frequency}

*在表格中，僅保留與目的地對應的行。 應該有一行用於「導出」類型，一行用於「導出」頻率。 刪除不適用於您目的地的值。*

有關目標導出類型和頻率的資訊，請參閱下表。

| 項目 | 類型 | 附註 |
---------|----------|---------|
| 匯出類型 | **[!UICONTROL 區段匯出]** | 您正在匯出區段（對象）的所有成員，其中包含 *YourDestination* 目的地。 |
| 匯出類型 | **[!UICONTROL 設定檔]** | 您要匯出區段的所有成員，以及所需的結構欄位(例如：電子郵件地址、電話號碼、姓氏)，如「選取設定檔屬性」畫面中所選 [目的地啟動工作流程](/help/destinations/ui/activate-batch-profile-destinations.md#select-attributes). |
| 匯出頻率 | **[!UICONTROL 串流]** | 串流目的地是「一律開啟」API型連線。 一旦根據區段評估在Experience Platform中更新設定檔，連接器就會將更新傳送至下游的目的地平台。 深入了解 [串流目的地](/help/destinations/destination-types.md#streaming-destinations). |
| 匯出頻率 | **[!UICONTROL 批次]** | 批次目的地會以3、6、8、12或24小時為增量將檔案匯出至下游平台。 深入了解 [批次檔案型目的地](/help/destinations/destination-types.md#file-based). |

{style=&quot;table-layout:auto&quot;}

## 連接到目標 {#connect}

>[!IMPORTANT]
> 
>若要連線至目的地，您需要 **[!UICONTROL 管理目的地]** [存取控制權限](/help/access-control/home.md#permissions). 閱讀 [存取控制概觀](/help/access-control/ui/overview.md) 或聯絡您的產品管理員以取得所需的權限。

若要連線至此目的地，請依照 [目的地設定教學課程](../../ui/connect-destination.md). 在設定目標工作流程中，填寫下列兩節所列的欄位。

### 驗證到目標 {#authenticate}

*新增客戶在驗證目的地時必須填入的欄位。 這些欄位是目的地特定欄位，取決於您在Destination SDK中的設定。 您目的地的欄位可能與下列欄位不同。 另請提供與下方範例螢幕擷取類似的螢幕擷取畫面。*

若要驗證目的地，請填寫必填欄位並選取 **[!UICONTROL 連接到目標]**.

![螢幕擷圖範例，說明如何驗證至目的地](/help/destinations/destination-sdk/docs-framework/assets/authenticate-destination.png)

* **[!UICONTROL 承載令牌]**:填入承載權杖，以驗證目的地。

### 填寫目的地詳細資訊 {#destination-details}

*新增客戶在設定新目的地時必須填入的欄位。 這些欄位是目的地特定欄位，取決於您在Destination SDK中的設定。 您目的地的欄位可能與下列欄位不同。 另請提供與下方範例螢幕擷取類似的螢幕擷取畫面。*

若要設定目的地的詳細資訊，請填寫下方的必填和選填欄位。 UI中欄位旁的星號表示該欄位為必要欄位。

![螢幕擷圖範例，顯示如何填入目的地的詳細資訊](/help/destinations/destination-sdk/docs-framework/assets/configure-destination-details.png)

* **[!UICONTROL 名稱]**:日後您將透過此名稱識別此目的地。
* **[!UICONTROL 說明]**:未來可協助您識別此目的地的說明。
* **[!UICONTROL 帳戶ID]**:您的 *YourDestination* 帳戶ID。

### 啟用警報 {#enable-alerts}

您可以啟用警報，接收有關資料流到目標狀態的通知。 從清單中選擇要訂閱的警報，以接收有關資料流狀態的通知。 如需警報的詳細資訊，請參閱 [使用UI訂閱目的地警報](../../ui/alerts.md).

完成提供目標連接的詳細資訊後，請選擇 **[!UICONTROL 下一個]**.

## 啟用此目的地的區段 {#activate}

>[!IMPORTANT]
> 
>若要啟用資料，您需要 **[!UICONTROL 管理目的地]**, **[!UICONTROL 啟動目的地]**, **[!UICONTROL 檢視設定檔]**，和 **[!UICONTROL 檢視區段]** [存取控制權限](/help/access-control/home.md#permissions). 閱讀 [存取控制概觀](/help/access-control/ui/overview.md) 或聯絡您的產品管理員以取得所需的權限。

閱讀 [啟動設定檔和區段至串流區段匯出目的地](https://experienceleague.adobe.com/docs/experience-platform/destinations/ui/activate/activate-segment-streaming-destinations.html?lang=en) 以取得啟用受眾區段至此目的地的指示。

### 對應屬性和身分 {#map}

*在啟動工作流程的「對應」步驟中，新增有關來源欄位和目標欄位之間支援對應的資訊。 您的目的地可能支援匯出設定檔屬性、身分識別命名空間或兩者。 某些欄位可能是必填欄位。 Target屬性可預先定義或自訂。 請提出重要注意事項，並使用範例，最好搭配螢幕擷取畫面。 可作為參考的兩個目的地頁面範例：*

* *[佩加](/help/destinations/catalog/personalization/pega.md#mapping-example)*
* *[梅達利亞](/help/destinations/catalog/voice/medallia-connector.md#map)*

## 匯出的資料/驗證資料匯出 {#exported-data}

*新增關於如何將資料匯出至目的地的段落。 這可協助客戶確定他們已正確與您的目的地整合。 例如，您可以提供範例JSON，如下所示。 或者，您也可以從目的地介面提供螢幕擷取畫面和資訊，顯示客戶應如何預期區段在目的地平台中填入。*

```
{
  "person": {
    "email": "yourstruly@adobe.com"
  },
  "segmentMembership": {
    "ups": {
      "7841ba61-23c1-4bb3-a495-00d3g5fe1e93": {
        "lastQualificationTime": "2020-05-25T21:24:39Z",
        "status": "exited"
      },
      "59bd2fkd-3c48-4b18-bf56-4f5c5e6967ae": {
        "lastQualificationTime": "2020-05-25T23:37:33Z",
        "status": "existing"
      }
    }
  },
  "identityMap": {
    "ecid": [
      {
        "id": "14575006536349286404619648085736425115"
      },
      {
        "id": "66478888669296734530114754794777368480"
      }
    ],
    "email_lc_sha256": [
      {
        "id": "655332b5fa2aea4498bf7a290cff017cb4"
      },
      {
        "id": "66baf76ef9de8b42df8903f00e0e3dc0b7"
      }
    ]
  }
}
```

## 資料使用與控管 {#data-usage-governance}

全部 [!DNL Adobe Experience Platform] 處理資料時，目的地符合資料使用原則。 有關如何 [!DNL Adobe Experience Platform] 強制實施資料治理，讀取 [資料控管概觀](/help/data-governance/home.md).

## 其他資源 {#additional-resources}

*您可以提供產品檔案的進一步連結，或您認為對客戶而言重要的任何其他資源，以利其成功。*