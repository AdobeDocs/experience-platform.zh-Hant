---
keywords: 廣告；克雷蒂奧；
title: Criteo連接
description: Criteo可支援受信任且具影響力的廣告，透過開放網際網路為每位消費者帶來更豐富的體驗。 Criteo擁有全球最大的商務資料集和同級最佳的人工智慧，可確保整個購物歷程的每個接觸點都經過個人化，以便在適當的時間以適當的廣告觸及客戶。
exl-id: e6f394b2-ab82-47bb-8521-1cf9d01a203b
source-git-commit: 8211ca28462548e1c17675e504e6de6f5cc55e73
workflow-type: tm+mt
source-wordcount: '1007'
ht-degree: 3%

---

# (Beta)Criteo連接

## 總覽 {#overview}

>[!IMPORTANT]
>
>此檔案頁面由Criteo建立。 這目前是測試版產品，功能可能會有所變更。 如有任何查詢或更新請求，請直接與Criteo聯繫 [此處](mailto:criteoTechnicalPartnerships@criteo.com).

Criteo可支援受信任且具影響力的廣告，透過開放網際網路為每位消費者帶來更豐富的體驗。 Criteo擁有全球最大的商務資料集和同級最佳的人工智慧，可確保整個購物歷程的每個接觸點都經過個人化，以便在適當的時間以適當的廣告觸及客戶。

## 先決條件 {#prerequisites}

* 您必須擁有管理員使用者帳戶 [Criteo管理中心](https://marketing.criteo.com).
* 您需要您的Criteo廣告商ID（如果您沒有此ID，請向Criteo連絡人詢問）。
* 你需要提供 [!DNL GUM caller ID]，以備您使用 [!DNL GUM ID] 做為識別碼。

## 限制 {#limitations}

* 克里蒂奧只接受 [!DNL SHA-256]雜湊和純文字電子郵件(將轉換為 [!DNL SHA-256] )。 請勿傳送任何PII（個人識別資訊，例如個人姓名或電話號碼）。
* Criteo需要由客戶提供至少一個標識符。 優先順序 [!DNL GUM ID] 做為雜湊電子郵件的識別碼，因為這有助於提高匹配率。

![先決條件](../../assets/catalog/advertising/criteo/prerequisites.png)

## 支援的身分 {#supported-identities}

Criteo支援下表所述的身份激活。 深入了解 [身分](https://experienceleague.adobe.com/docs/experience-platform/identity/namespaces.html?lang=en#getting-started).

| Target身分 | 說明 | 考量事項 |
| --- | --- | --- |
| `email_sha256` | 使用SHA-256演算法雜湊的電子郵件地址 | Adobe Experience Platform支援純文字和SHA-256雜湊電子郵件地址。 當來源欄位包含未雜湊屬性時，請檢查 [!UICONTROL 套用轉換] 選項，讓Platform在啟動時自動雜湊資料。 |
| `gum_id` | 克里蒂奧 [!DNL GUM] Cookie識別碼 | [!DNL GUM IDs] 允許客戶保持其用戶識別系統與Criteo的用戶識別([!DNL UID])。 如果識別碼類型為 `gum_id`，此為其他參數， [!DNL GUM Caller ID]，也必須包含。 請洽詢您的Criteo客戶團隊，以取得適當 [!DNL GUM Caller ID] 或者獲取更多有關此資訊 [!DNL GUM ID] 視需要同步。 |

## 匯出類型和頻率 {#export-type-frequency}

有關目標導出類型和頻率的資訊，請參閱下表。

| 項目 | 類型 | 附註 |
| --- | --- | --- |
| 匯出類型 | 區段匯出 | 您正在匯出區段（對象）的所有成員，其中包含 [!DNL Criteo] 目的地。 |
| 匯出頻率 | 串流 | 串流目的地是「一律開啟」API型連線。 一旦根據區段評估在Experience Platform中更新設定檔，連接器就會將更新傳送至下游的目的地平台。 深入了解 [串流目的地](../../destination-types.md#streaming-destinations). |

## 使用案例 {#use-cases}

協助您更清楚了解如何使用 [!DNL Criteo] 目的地，以下是Adobe Experience Platform客戶可達成的目標 [!DNL Criteo]:

### 使用案例1 :取得流量

透過相關的產品優惠方案和靈活的創意素材，展示您的業務。 有了智慧型產品建議，您的廣告會自動加入最有可能觸發造訪和參與的產品。 彈性的鎖定目標可讓您從Criteo的商務資料集或您自己的潛在客戶清單和AdobeCDP區段建立受眾。

### 使用案例2 :提高網站轉換

當訪客離開您的網站時，請提醒他們下一步要前往的位置，顯示特別優惠和高度相關選件，借此重新定位可增加轉換的廣告，以提醒他們有哪些遺漏。 連結您的AdobeCDP區段，重新與現有客戶互動，或鎖定與您最忠誠的購物者類似的消費者。

## 連接到Criteo {#connect}

>[!IMPORTANT]
> 
>若要連線至目的地，您需要 **[!UICONTROL 管理目的地]** [存取控制權限](/help/access-control/home.md#permissions). 閱讀 [存取控制概觀](/help/access-control/ui/overview.md) 或聯絡您的產品管理員以取得所需的權限。

若要連線至此目的地，請依照 [目的地設定教學課程](../../ui/connect-destination.md).

### 驗證克里蒂奧

連接步驟如下：

1. 登入Adobe Experience Platform並連線至Criteo目的地。

   ![登入](../../assets/catalog/advertising/criteo/connect-destination.png)

1. 系統會將您重新導向至Criteo以授權連線。 您可能需要先使用您的Criteo憑證登入：

   ![登入](../../assets/catalog/advertising/criteo/log-in-1.png)

   ![登入](../../assets/catalog/advertising/criteo/log-in-2.png)

   ![登入](../../assets/catalog/advertising/criteo/log-in-3.png)


### 連線參數 {#connection-parameters}

在驗證目標後，請填寫以下連接參數。

![連線參數](../../assets/catalog/advertising/criteo/connection-parameters.png)

| 欄位 | 說明 | 必填 |
| --- | --- | --- |
| 名稱 | 可協助您日後辨識此目的地的名稱。 您在此選擇的名稱會是 [!DNL Audience] 名稱（在Criteo管理中心），在以後階段無法修改。 | 是 |
| 說明 | 說明可協助您日後識別此目的地。 | 無 |
| 廣告商ID | 貴組織的Criteo廣告商ID。 請連絡您的Criteo客戶經理以取得此資訊。 | 是 |
| 克里蒂奧 [!DNL GUM caller ID] | [!DNL GUM Caller ID] 貴組織。 請洽詢您的Criteo客戶團隊，以取得適當 [!DNL GUM Caller ID] 或者獲取更多有關此資訊 [!DNL GUM] 視需要同步。 | 是，只要 [!DNL GUM ID] 是作為識別碼提供 |

### 啟用警報 {#enable-alerts}

您可以啟用警報，接收有關資料流到目標狀態的通知。 從清單中選擇要訂閱的警報，以接收有關資料流狀態的通知。 如需警報的詳細資訊，請參閱 [使用UI訂閱目的地警報](../../ui/alerts.md).

完成提供目標連接的詳細資訊後，請選擇 **[!UICONTROL 下一個]**.

## 啟用此目的地的區段 {#activate-segments}

>[!IMPORTANT]
> 
>若要啟用資料，您需要 **[!UICONTROL 管理目的地]**, **[!UICONTROL 啟動目的地]**, **[!UICONTROL 檢視設定檔]**，和 **[!UICONTROL 檢視區段]** [存取控制權限](/help/access-control/home.md#permissions). 閱讀 [存取控制概觀](/help/access-control/ui/overview.md) 或聯絡您的產品管理員以取得所需的權限。

閱讀 [啟動設定檔和區段至串流區段匯出目的地](../../ui/activate-segment-streaming-destinations.md) 以取得啟用受眾區段至此目的地的指示。

## 匯出的資料 {#exported-data}

您可以在 [犯罪管理中心](https://marketing.criteo.com/audience-manager/dashboard).

新增收到之使用者設定檔的要求內文 [!DNL Criteo] 連線看起來類似這樣：

```json
{
  "data": {
    "type": "ContactlistWithUserAttributesAmendment",
    "attributes": {
      "operation": "add",
      "identifierType": "gum",
      "gumCallerId": "123",
      "identifiers": [
        {
          "identifier": "456",
          "attributes": [
            { "key": "ctoid_GumCaller", "value": "123" },
            { "key": "ctoid_Gum", "value": "456" },
            {
              "key": "ctoid_HashedEmail",
              "value": "98833030dc03751f2b2c1a0017078975fdae951aa6908668b3ec422040f2d4be"
            }
          ]
        }
      ]
    }
  }
}
```

移除由 [!DNL Criteo] 連線看起來類似這樣：

```json
{
  "data": {
    "type": "ContactlistWithUserAttributesAmendment",
    "attributes": {
      "operation": "remove",
      "identifierType": "gum",
      "gumCallerId": "123",
      "identifiers": [
        {
          "identifier": "456",
          "attributes": [
            { "key": "ctoid_GumCaller", "value": "123" },
            { "key": "ctoid_Gum", "value": "456" },
            {
              "key": "ctoid_HashedEmail",
              "value": "98833030dc03751f2b2c1a0017078975fdae951aa6908668b3ec422040f2d4be"
            }
          ]
        }
      ]
    }
  }
}
```

## 資料使用與控管 {#data-usage}

處理資料時，所有Adobe Experience Platform目的地都符合資料使用原則。 如需Adobe Experience Platform如何執行資料控管的詳細資訊，請參閱 [資料控管概觀](https://experienceleague.adobe.com/docs/experience-platform/data-governance/home.html?lang=zh-Hant).

## 其他資源

* [克里蒂奧幫助中心](https://help.criteo.com/kb/en)
* [Criteo開發人員入口網站](https://developers.criteo.com)
