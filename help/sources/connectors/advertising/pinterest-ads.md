---
keywords: Experience Platform；首頁；熱門主題；Pinterest廣告；
title: Pinterest廣告源概述
description: 瞭解如何使用API或用戶介面將Pinterest廣告連接到Adobe Experience Platform。
badge: β
hide: true
hidefromtoc: true
exl-id: 8edbcb26-0a18-47f1-8012-ca209d99d7a6
source-git-commit: 05a7b73da610a30119b4719ae6b6d85f93cdc2ae
workflow-type: tm+mt
source-wordcount: '984'
ht-degree: 0%

---

# [!DNL Pinterest Ads]

>[!NOTE]
>
>的 [!DNL Pinterest Ads] 源為beta。 閱讀 [源概述](../../home.md#terms-and-conditions) 的子菜單。

Adobe Experience Platform允許從外部源接收資料，同時讓您能夠使用平台服務構建、標籤和增強傳入資料。 您可以從多種源(如Adobe應用程式、基於雲的儲存、資料庫和許多其他源)接收資料。

Experience Platform支援從第三方廣告系統接收資料。 對廣告提供商的支援包括 [!DNL Pinterest Ads]。

[[!DNL Pinterest]](https://www.pinterest.com) 是一個視覺發現引擎，可以在網路上找到食譜、家居裝飾、風格靈感和其他想法。 這些內容是使用插接板格式的影像、動畫GIF和視頻進行小規模顯示的。 [[!DNL Pinterest Ads]](https://ads.pinterest.com/) 使您能夠擴展業務並讓4億用戶 [!DNL Pinterest]。

與 [!DNL Pinterest Ads]，您可以通過目標廣告聯繫用戶以發現和購買您的產品。 針腳 [!DNL Pinterest Ads] 以在相關搜索結果中獲得額外曝光。 訂閱的用戶 [!DNL Pinterest Business] 可以選擇升級現有效能最佳的管腳、建立新影像或視頻，甚至升級從網站固定的影像。 [!DNL Pinterest Ads] 提供多種廣告格式，幫助您實現特定的市場活動目標。

## [!DNL Pinterest] API {#pinterest-apis}

的 [!DNL Pinterest Ads] 源利用 [!DNL Pinterest] 用於檢索的API [!DNL Pinterest Ads] 資料，以及所有效能和指標。 支援的API終結點包括：

* [市場活動分析](https://developers.pinterest.com/docs/api/v5/#operation/campaigns/analytics)
* [廣告組分析](https://developers.pinterest.com/docs/api/v5/#operation/ad_groups/analytics)
* [廣告分析](https://developers.pinterest.com/docs/api/v5/#operation/ads/analytics)

使用 [!DNL Pinterest Ads] 源，將資料從 [!DNL Pinterest] 到Experience Platform，然後可以執行資料分析。 從攝入日期開始，返回90天的回溯範圍。 [!DNL Pinterest Ads] 使用承載令牌作為與通信的驗證機制 [!DNL Pinterest] API。

## 先決條件 {#prerequisites}

建立 [!DNL Pinterest Ads] 源連接是確保您有Pinterest開發人員帳戶。 如果您還沒有，請訪問 [註冊](https://www.pinterest.com/business/create/?next=https://developers.pinterest.com/account-setup/) 頁，以註冊和建立帳戶。

### 設定 [!DNL Pinterest] 應用和生成訪問令牌 {#create-app-and-generate-token}

>[!IMPORTANT]
>
>建議使用 [!DNL Pinterest] 用於生成訪問令牌的API，因為在UI中生成訪問令牌提供了有限的訪問。 通過UI，您只能訪問以下作用域： `pins:read`。 `boards:read` 和 `user_accounts:read`。 此限制不足以用於 [!DNL Pinterest] API。

要生成訪問令牌，請閱讀 [!DNL Pinterest] 嚮導 [設定你的應用](https://developers.pinterest.com/docs/getting-started/set-up-app/) 和 [使用OAuth 2.0進行身份驗證](https://developers.pinterest.com/docs/getting-started/authentication/)。

### 收集所需憑據 {#gather-required-credentials}

為了連接 [!DNL Pinterest Ads] 到平台，必須提供以下連接屬性的值：

| 憑據 | 說明 |
| --- | --- |
| 訪問令牌 | 的 [!DNL Pinterest Ads] 用戶帳戶的訪問令牌。 令牌的用戶帳戶必須是指定的 [!DNL Pinterest Ad] 帳戶或通過Business Access授予他們一個必要的角色：管理員、分析師或市場活動經理。 有關訪問令牌的詳細資訊，請參閱 [[!DNL Pinterest] 生成訪問令牌的指南](https://developers.pinterest.com/docs/getting-started/set-up-app/)。 |
| 廣告帳戶ID | 相關 [!DNL Pinterest Ads] 您業務部門的廣告帳戶ID。 有關檢索Ad帳戶ID的資訊。 訪問 [[!DNL Pinterest] 在Ads Manager中查找ID的指南](https://help.pinterest.com/en/business/article/find-ids-in-ads-manager)。 |
| 市場活動、廣告組或廣告ID | 的 `campaign`。 `ad group`或 `ad` 與廣告帳戶ID對應的ID。 要獲取所需的ID，請導航到 [!DNL Pinterest] 頁面 **Pinterest商業中心** > **廣告帳戶摘要** > **市場活動** / **廣告組** / **廣告** 並複製他們名字下方提到的必需身份證。 |

>[!NOTE]
>
>的 [!DNL Pinterest] API提供單個API以檢索與每個ID關聯的資料。 因此，您只需要傳遞您感興趣的ID類型的相應ID。

## 護欄 {#guardrails}

以下各節提供了有關資料護欄的資訊 [!DNL Pinterest]。

### [!DNL Pinterest] 日期範圍 {#pinterest-date-range}

的 [!DNL Pinterest] API支援 `start_date` 和 `end_date` 參數，用於在給定日期範圍之間檢索分析資料。

* 的 `start_date` 不能超過當前日期之前90天。
* 的 `end_date` 不能超過90天 `start_date`。

調度資料流時，必須配置以下頻率和間隔設定之一：

| 頻率 | 間隔 |
| --- | --- |
| `Day` | 1 |
| `Hour` | 24 |

例如，如果在2023年3月15日設定了接收，並將頻率和間隔設定配置為 `Day=1` 或 `Hour=24`，則 [!DNL Pinterest] API只能從最遠的2022年12月15日檢索資料，因為計算被追溯90天。

### [!DNL Pinterest] 時間範圍 {#pinterest-time-range}

的 [!DNL Pinterest] API支援不同類型的時間粒度，用於如何檢索資料：

| 時間粒度 | 說明 |
| --- | --- |
| **合計** | 資料度量在指定的日期範圍上聚合。 |
| **日** | 資料度量每天被細分。 |
| **小時** | 資料度量按小時細分。 |
| **每週** | 資料度量按周細分。 |
| **每月** | 資料度量按月細分。 |

對於平台， [!DNL Pinterest Ads] 源內部配置為 `Day`即每天進行資料聚合。 例如，使用 `impressions recorded` 作為度量，因為粒度配置為 `DAY`你會 `xx` 印象 `day 1`。 `yy` 印象 `day 2` 等等。

>[!IMPORTANT]
>
>Pinterest對其API每天施加1000個API調用的速率限制，以從廣告、廣告組或廣告活動中讀取資訊。 有關適用於基礎API調用的速率限制的資訊，請參閱 [[!DNL Pinterest] 費率限制文檔](https://developers.pinterest.com/docs/reference/ratelimits/)。

## 連接 [!DNL Pinterest Ads] 到平台 {#connect-to-platform}

以下文檔提供了有關如何連接的資訊 [!DNL Pinterest Ads] 到使用API或用戶介面的平台：

### 連接 [!DNL Pinterest Ads] 到使用API的平台 {#connect-to-platform-using-api}

* [使用流服務API建立Pinterest基連接](../../tutorials/api/create/advertising/pinterest-ads.md)
* [使用流服務API瀏覽資料表](../../tutorials/api/explore/tabular.md)
* [使用流服務API為廣告源建立資料流](../../tutorials/api/collect/advertising.md)

### 連接 [!DNL Pinterest Ads] 到使用UI的平台 {#connect-to-platform-using-ui}

* [在UI中建立Pinterest源連接](../../tutorials/ui/create/advertising/pinterest-ads.md)
* [在UI中為廣告源連接建立資料流](../../tutorials/ui/dataflow/advertising.md)
