---
keywords: 廣告；標準；
title: 標準連線
description: Criteo提供值得信賴且有影響力的廣告，讓開放網際網路上的每位消費者都能獲得更豐富的體驗。 Criteo擁有世界上最大的商業資料集和同級最佳的AI，可確保整個購物歷程的每個接觸點都經過個人化，以在適當的時間透過適當的廣告觸及客戶。
exl-id: e6f394b2-ab82-47bb-8521-1cf9d01a203b
source-git-commit: c3ef732ee82f6c0d56e89e421da0efc4fbea2c17
workflow-type: tm+mt
source-wordcount: '1029'
ht-degree: 3%

---

# (Beta) Criteo連線

## 概觀 {#overview}

>[!IMPORTANT]
>
>此目的地聯結器和檔案頁面是由Criteo建立和維護。 此產品目前為測試版，功能可能會有所變更。 若有任何查詢或更新要求，請直接連絡條件 [此處](mailto:criteoTechnicalPartnerships@criteo.com).

Criteo提供值得信賴且有影響力的廣告，讓開放網際網路上的每位消費者都能獲得更豐富的體驗。 Criteo擁有世界上最大的商業資料集和同級最佳的AI，可確保整個購物歷程的每個接觸點都經過個人化，以在適當的時間透過適當的廣告觸及客戶。

## 先決條件 {#prerequisites}

* 您必須擁有管理員使用者帳戶 [標準管理中心](https://marketing.criteo.com).
* 您將需要您的Criteo廣告商ID （如果您沒有此ID，請詢問您的Criteo聯絡人）。
* 您需要提供 [!DNL GUM caller ID]，以備您使用 [!DNL GUM ID] 作為識別碼。

## 限制 {#limitations}

* 標準僅接受 [!DNL SHA-256] — 雜湊和純文字電子郵件(將轉換為 [!DNL SHA-256] 之前)。 請勿傳送任何PII （個人識別資訊，例如個人名稱或電話號碼）。
* 條件至少需要由使用者端提供一個識別碼。 它會排定優先順序 [!DNL GUM ID] 做為雜湊電子郵件上的識別碼，因為它有助於提高符合率。

![先決條件](../../assets/catalog/advertising/criteo/prerequisites.png)

## 支援的身分 {#supported-identities}

標準支援下表所述的身分啟用。 進一步瞭解 [身分](https://experienceleague.adobe.com/docs/experience-platform/identity/namespaces.html#getting-started).

| 目標身分 | 說明 | 考量事項 |
| --- | --- | --- |
| `email_sha256` | 使用SHA-256演演算法雜湊的電子郵件地址 | Adobe Experience Platform同時支援純文字和SHA-256雜湊電子郵件地址。 當來源欄位包含未雜湊屬性時，請核取 [!UICONTROL 套用轉換] 選項，讓Platform在啟用時自動雜湊資料。 |
| `gum_id` | 條件 [!DNL GUM] Cookie識別碼 | [!DNL GUM IDs] 允許客戶維持其使用者識別系統與Criteo的使用者識別之間的對應關係([!DNL UID])。 如果識別碼型別為 `gum_id`，其他引數， [!DNL GUM Caller ID]，也必須包含。 請聯絡您的Criteo帳戶團隊以取得適當的 [!DNL GUM Caller ID] 或以取得此專案的詳細資訊 [!DNL GUM ID] 同步（如有需要）。 |

## 匯出型別和頻率 {#export-type-frequency}

請參閱下表以取得目的地匯出型別和頻率的資訊。

| 項目 | 類型 | 附註 |
| --- | --- | --- |
| 匯出型別 | 對象匯出 | 您正在匯出某個對象的所有成員，而這些成員中都有用於的識別碼（名稱、電話號碼或其他）。 [!DNL Criteo] 目的地。 |
| 匯出頻率 | 串流 | 串流目的地是「一律開啟」的API型連線。 一旦根據對象評估在Experience Platform中更新了設定檔，聯結器就會將更新傳送至下游的目的地平台。 深入瞭解 [串流目的地](../../destination-types.md#streaming-destinations). |

## 使用案例 {#use-cases}

為了協助您更清楚瞭解如何使用 [!DNL Criteo] 目的地，以下是Adobe Experience Platform客戶可以達成的一些目標 [!DNL Criteo]：

### 使用案例1 ：取得流量

利用相關的產品選件和彈性的創意來展示您的企業。 有了智慧型產品推薦，您的廣告會自動加入最有可能觸發造訪和參與的產品。 彈性鎖定目標可讓您從Criteo的商務資料集或您自己的潛在客戶清單和AdobeCDP區隔建立受眾。

### 使用案例2 ：提高網站轉換率

訪客離開您的網站時，重新定位廣告以提醒他們缺少什麼，這些廣告可顯示特殊優惠和高度相關的優惠方案，以增加轉換率，無論他們接下來前往何處。 連線您的AdobeCDP受眾，以重新吸引現有客戶或鎖定與最忠實購物者類似的消費者。

## 連線到標準 {#connect}

>[!IMPORTANT]
> 
>若要連線到目的地，您需要 **[!UICONTROL 檢視目的地]** 和 **[!UICONTROL 管理目的地]** [存取控制許可權](/help/access-control/home.md#permissions). 閱讀 [存取控制總覽](/help/access-control/ui/overview.md) 或聯絡您的產品管理員以取得必要許可權。

若要連線至此目的地，請遵循以下說明的步驟： [目的地設定教學課程](../../ui/connect-destination.md).

### 向標準驗證

連線的步驟如下：

1. 登入Adobe Experience Platform並連線至Criteo目的地。

   ![登入](../../assets/catalog/advertising/criteo/connect-destination.png)

1. 系統會將您重新導向至條件以授權連線。 您可能需要先使用Criteo憑證登入：

   ![標準登入](../../assets/catalog/advertising/criteo/log-in-1.png)

   ![標準登入](../../assets/catalog/advertising/criteo/log-in-2.png)

   ![標準登入](../../assets/catalog/advertising/criteo/log-in-3.png)


### 連線參數 {#connection-parameters}

在對目的地進行驗證之後，請填寫以下連線引數。

![連線引數](../../assets/catalog/advertising/criteo/connection-parameters.png)

| 欄位 | 說明 | 必填 |
| --- | --- | --- |
| 名稱 | 可協助您日後辨識此目的地的名稱。 您在此選擇的名稱將是 [!DNL Audience] Criteo Management Center中的名稱，且無法在稍後階段修改。 | 是 |
| 說明 | 有助於您日後識別此目的地的說明。 | 無 |
| 廣告商 ID | 貴組織的條件廣告商ID。 請連絡您的Criteo客戶經理，以取得此資訊。 | 是 |
| 條件 [!DNL GUM caller ID] | [!DNL GUM Caller ID] 您的組織名稱。 請聯絡您的Criteo帳戶團隊以取得適當的 [!DNL GUM Caller ID] 或以取得此專案的詳細資訊 [!DNL GUM] 同步（如有需要）。 | 是，只要 [!DNL GUM ID] 以識別碼形式提供 |

### 啟用警示 {#enable-alerts}

您可以啟用警報以接收有關傳送到您目的地的資料流狀態的通知。 從清單中選取警報以訂閱接收有關資料流狀態的通知。 如需警示的詳細資訊，請參閱以下指南： [使用UI訂閱目的地警報](../../ui/alerts.md).

當您完成提供目的地連線的詳細資訊時，請選取「 」 **[!UICONTROL 下一個]**.

## 啟動此目標的對象 {#activate-segments}

>[!IMPORTANT]
> 
>* 若要啟用資料，您需要 **[!UICONTROL 檢視目的地]**， **[!UICONTROL 啟用目的地]**， **[!UICONTROL 檢視設定檔]**、和 **[!UICONTROL 檢視區段]** [存取控制許可權](/help/access-control/home.md#permissions). 閱讀 [存取控制總覽](/help/access-control/ui/overview.md) 或聯絡您的產品管理員以取得必要許可權。
>* 要匯出 *身分*，您需要 **[!UICONTROL 檢視身分圖表]** [存取控制許可權](/help/access-control/home.md#permissions). <br> ![選取工作流程中反白顯示的身分名稱空間，以將對象啟用至目的地。](/help/destinations/assets/overview/export-identities-to-destination.png "選取工作流程中反白顯示的身分名稱空間，以將對象啟用至目的地。"){width="100" zoomable="yes"}

讀取 [將設定檔和受眾啟用至串流受眾匯出目標](../../ui/activate-segment-streaming-destinations.md) 以取得啟用此目的地對象的指示。

## 匯出的資料 {#exported-data}

您可在以下欄位中檢視匯出的對象： [標準管理中心](https://marketing.criteo.com/audience-manager/dashboard).

新增由接收的使用者設定檔的請求內文 [!DNL Criteo] 連線看起來類似這樣：

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

移除使用者個人資料的請求內文，已由 [!DNL Criteo] 連線看起來類似這樣：

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

處理您的資料時，所有Adobe Experience Platform目的地都符合資料使用原則。 如需Adobe Experience Platform如何實施資料控管的詳細資訊，請參閱 [資料控管概觀](https://experienceleague.adobe.com/docs/experience-platform/data-governance/home.html?lang=zh-Hant).

## 其他資源

* [Criteo說明中心](https://help.criteo.com/kb/en)
* [Criteo開發人員入口網站](https://developers.criteo.com)
