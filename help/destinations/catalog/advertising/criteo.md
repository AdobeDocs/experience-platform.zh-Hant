---
keywords: 廣告；罪；
title: Criteo連接
description: Criteo能夠讓可信、有影響力的廣告為開放網際網路上的每個消費者帶來更豐富的體驗。 Criteo擁有全球最大的商業資料集和一流的人工智慧，確保整個購物過程中的每個觸點都個性化，以便在適當的時間通過正確的廣告接觸到客戶。
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
>此文檔頁面由Criteo建立。 這是當前的試用版產品，功能可能會更改。 如有任何查詢或更新請求，請直接與Criteo聯繫 [這裡](mailto:criteoTechnicalPartnerships@criteo.com)。

Criteo能夠讓可信、有影響力的廣告為開放網際網路上的每個消費者帶來更豐富的體驗。 Criteo擁有全球最大的商業資料集和一流的人工智慧，確保整個購物過程中的每個觸點都個性化，以便在適當的時間通過正確的廣告接觸到客戶。

## 先決條件 {#prerequisites}

* 您需要具有管理員用戶帳戶 [克里特奧管理中心](https://marketing.criteo.com)。
* 您需要您的Criteo廣告商ID（如果您沒有此ID，請咨詢您的Criteo聯繫人）。
* 你需要提供 [!DNL GUM caller ID]，以防您使用 [!DNL GUM ID] 作為標識符。

## 限制 {#limitations}

* 克里泰奧只接受 [!DNL SHA-256] — 散列和純文字檔案電子郵件(將轉換為 [!DNL SHA-256] 發送前)。 請勿發送任何PII（個人識別資訊，如個人姓名或電話號碼）。
* Criteo需要客戶端提供至少一個標識符。 它優先考慮 [!DNL GUM ID] 作為散列電子郵件的標識符，因為它有助於提高匹配率。

![先決條件](../../assets/catalog/advertising/criteo/prerequisites.png)

## 支援的身份 {#supported-identities}

Criteo支援激活下表中描述的身份。 瞭解有關 [身份](https://experienceleague.adobe.com/docs/experience-platform/identity/namespaces.html?lang=en#getting-started)。

| 目標標識 | 說明 | 考量事項 |
| --- | --- | --- |
| `email_sha256` | 使用SHA-256算法散列的電子郵件地址 | Adobe Experience Platform支援純文字檔案和SHA-256散列電子郵件地址。 如果源欄位包含未散列的屬性，請檢查 [!UICONTROL 應用轉換] 選項，使平台在激活時自動散列資料。 |
| `gum_id` | 克里泰奧 [!DNL GUM] cookie標識符 | [!DNL GUM IDs] 允許客戶保持其用戶識別系統與Criteo的用戶識別([!DNL UID])。 如果標識符類型為 `gum_id`，其他參數 [!DNL GUM Caller ID]。 請聯繫您的Criteo客戶團隊，以瞭解 [!DNL GUM Caller ID] 或者獲取更多有關此的資訊 [!DNL GUM ID] 同步（如果需要）。 |

## 導出類型和頻率 {#export-type-frequency}

有關目標導出類型和頻率的資訊，請參閱下表。

| 項目 | 類型 | 附註 |
| --- | --- | --- |
| 導出類型 | 區段匯出 | 您正在導出段（受眾）的所有成員，其中使用的標識符（名稱、電話號碼或其他） [!DNL Criteo] 目標。 |
| 導出頻率 | 流 | 流目標是基於API的「始終開啟」連接。 一旦基於段評估在Experience Platform中更新配置檔案，連接器就將更新下游發送到目標平台。 閱讀有關 [流目標](../../destination-types.md#streaming-destinations)。 |

## 使用案例 {#use-cases}

幫助您更好地瞭解如何使用 [!DNL Criteo] 目的地，以下是Adobe Experience Platform客戶可以實現的一些目標 [!DNL Criteo]:

### 用例1 :獲取流量

通過相關產品選項和靈活的創意來展示您的業務。 借助智慧產品推薦，您的廣告將自動顯示最有可能引發訪問和參與的產品。 靈活的定位允許您從Criteo的商業資料集或您自己的潛在客戶清單和AdobeCDP段構建受眾。

### 用例2 :增加網站轉換

當訪問者離開您的網站時，提醒他們，無論他們下一步去哪裡，都會展示特別優惠和超相關優惠，以增加轉換率的重新定位廣告，會遺漏什麼。 連接您的AdobeCDP網段，以重新吸引與您最忠誠的購物者相似的現有客戶或目標消費者。

## 連接到Criteo {#connect}

>[!IMPORTANT]
> 
>要連接到目標，您需要 **[!UICONTROL 管理目標]** [訪問控制權限](/help/access-control/home.md#permissions)。 閱讀 [訪問控制概述](/help/access-control/ui/overview.md) 或聯繫您的產品管理員以獲取所需權限。

要連接到此目標，請按照 [目標配置教程](../../ui/connect-destination.md)。

### 驗證到Criteo

要連接的步驟如下：

1. 登錄到Adobe Experience Platform並連接到Criteo目標。

   ![登入](../../assets/catalog/advertising/criteo/connect-destination.png)

1. 您將被重定向到Criteo以授權連接。 您可能需要首先使用Criteo憑據登錄：

   ![Criteo登錄](../../assets/catalog/advertising/criteo/log-in-1.png)

   ![Criteo登錄](../../assets/catalog/advertising/criteo/log-in-2.png)

   ![Criteo登錄](../../assets/catalog/advertising/criteo/log-in-3.png)


### 連接參數 {#connection-parameters}

向目標進行身份驗證後，請填寫以下連接參數。

![連接參數](../../assets/catalog/advertising/criteo/connection-parameters.png)

| 欄位 | 說明 | 必填 |
| --- | --- | --- |
| 名稱 | 一個名稱，用於幫助您識別將來的此目標。 您在此處選擇的名稱是 [!DNL Audience] 名稱，無法在稍後階段修改。 | 是 |
| 說明 | 一個說明，可幫助您將來確定此目標。 | 無 |
| 廣告商ID | 貴組織的Criteo Dactier ID。 請聯繫您的Criteo客戶經理以獲取此資訊。 | 是 |
| 克里泰奧 [!DNL GUM caller ID] | [!DNL GUM Caller ID] 你的組織。 請聯繫您的Criteo客戶團隊，以瞭解 [!DNL GUM Caller ID] 或者獲取更多有關此的資訊 [!DNL GUM] 同步（如果需要）。 | 是，只要 [!DNL GUM ID] 作為標識符提供 |

### 啟用警報 {#enable-alerts}

您可以啟用警報來接收有關目標資料流狀態的通知。 從清單中選擇要訂閱的警報以接收有關資料流狀態的通知。 有關警報的詳細資訊，請參閱上的指南 [使用UI訂閱目標警報](../../ui/alerts.md)。

完成提供目標連接的詳細資訊後，選擇 **[!UICONTROL 下一個]**。

## 將段激活到此目標 {#activate-segments}

>[!IMPORTANT]
> 
>要激活資料，您需要 **[!UICONTROL 管理目標]**。 **[!UICONTROL 激活目標]**。 **[!UICONTROL 查看配置檔案]**, **[!UICONTROL 查看段]** [訪問控制權限](/help/access-control/home.md#permissions)。 閱讀 [訪問控制概述](/help/access-control/ui/overview.md) 或聯繫您的產品管理員以獲取所需權限。

閱讀 [激活配置檔案和段以流式處理段導出目標](../../ui/activate-segment-streaming-destinations.md) 有關激活此目標受眾段的說明。

## 導出的資料 {#exported-data}

可在 [犯罪管理中心](https://marketing.criteo.com/audience-manager/dashboard)。

添加由 [!DNL Criteo] 連接類似於以下內容：

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

刪除由 [!DNL Criteo] 連接類似於以下內容：

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

## 資料使用和治理 {#data-usage}

所有Adobe Experience Platform目標在處理資料時都符合資料使用策略。 有關Adobe Experience Platform如何實施資料治理的詳細資訊，請閱讀 [資料治理概述](https://experienceleague.adobe.com/docs/experience-platform/data-governance/home.html?lang=zh-Hant)。

## 其他資源

* [克里特奧幫助中心](https://help.criteo.com/kb/en)
* [Criteo開發人員門戶](https://developers.criteo.com)
