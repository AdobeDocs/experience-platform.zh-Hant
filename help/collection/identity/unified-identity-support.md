---
title: 資料收集中的統一身分支援
description: 瞭解統一的身分支援如何將第一方持續性和支援的第三方啟用在網頁資料收集中結合在一起。
hide: true
hidefromtoc: true
badge: Beta
source-git-commit: 32c2565d31eed4eda28195afaf82aac6f04a6f8a
workflow-type: tm+mt
source-wordcount: '1029'
ht-degree: 3%

---

# 資料收集中的統一身分支援

>[!AVAILABILITY]
>
>此功能目前處於Beta測試階段。 可用性、行為和檔案可能會變更。

統一的身分支援可讓Edge Network同時在第一方和第三方身分內容中運作。 它會結合您所擁有屬性的永續性第一方識別碼，與支援第三方Cookie的瀏覽器中的第三方啟用工作流程。 如需Web SDK如何處理ECID、FPID與其他身分訊號的背景資訊，請參閱資料彙集[中的](./overview.md)身分識別。

透過統一的身分支援，您可以：

* **將受眾觸及範圍最大化**：在協力廠商目的地（DSP、SSP和廣告網路）啟用Experience Platform受眾，以獲得更大份額的流量。
* **維持測量準確度**：維持您擁有的屬性和廣告平台間一致的訪客身分識別。
* **您的實作可經得起未來考驗**：使用第一方裝置識別碼作為您的基礎，同時保持與協力廠商啟用工作流程的相容性。

當訪客進入您的網站時，Edge Network會評估可用的身分訊號，在條件允許時自動連結第一方和第三方內容。 封鎖第三方Cookie的瀏覽器會繼續以第一方模式運作，不會中斷您的實施。

## 運作方式

Edge Network會依照以下優先順序評估可用的身分訊號來產生ECID：

| 優先順序 | 來源 | 內容 | 行為 |
| --- | --- | --- | --- |
| 1 | **Demdex ID** | 第三方 | 如果存在Demdex ID，則會從中內建ECID。 此種子會在共用相同第三方Cookie的網域間產生一致的ECID。 |
| 2 | **FPID** | 第一方 | 如果沒有Demdex ID但有FPID存在，則ECID會從FPID內建，而Demdex ID會從中衍生。 |
| 3 | **Random** | 第一方 | 如果Demdex ID和FPID都不可用，則會產生新的隨機ECID，並從中衍生Demdex ID。 |

ECID和Demdex ID會透過確定性演演算法以密碼方式連結，這表示可以從另一個衍生。 這種關係可讓Edge Network在第一方與第三方身分內容之間轉換，而不需要您實作中的個別訪客處理邏輯。

由於此關係是決定性的，因此在對應的Demdex ID可供使用時，建置在第一方ECID上的受眾可以透過第三方基礎結構啟用。

若訪客已有FPID衍生的ECID，Edge Network會自動將其第一方身分識別連結至第三方身分識別內容。 當瀏覽器支援第三方Cookie且不需要變更實施時，就會透明地發生這種情況。 發生自動連結時：

1. Edge Network會偵測訪客的ECID並非衍生自Demdex ID。
1. 如果訪客的瀏覽器支援第三方Cookie，則會觸發輕量型身分同步作業。
1. 系統會在訪客的第一方ECID與其第三方身分之間建立連結。
1. 此連結儲存在身分存放區中，可在第三方目的地啟用受眾啟用。

自動連結可保留現有ECID並防止訪客斷崖式變化。 一段時間後，當訪客回訪並進行連結時，會有更多對象逐漸符合協力廠商啟用的資格。

協力廠商對象啟用仰賴ID同步（ID同步）。 Edge Network建立或重新整理協力廠商身分時，會在回應中傳回ID同步指示。 這些指示會指示瀏覽器將訪客的身分識別與合作夥伴網域（DSP、廣告網路和其他啟用平台）同步，以便您的Experience Platform受眾可以在該等平台上比對和傳遞。

## 先決條件

整合身分支援需要下列所有專案：

* 您的網站會在您控制的網域上使用第一方資料收集。
* 您的實作使用FPID或其他第一方持續性策略為基礎。
* 您的網頁SDK設定已啟用第三方Cookie。
* 已為資料流啟用第三方ID同步。
* 訪客使用的瀏覽器允許第三方Cookie （請參閱下方的[瀏覽器相容性](#browser-compatibility)）。

## 設定

1. **在Web SDK中啟用第三方Cookie**：在您的Web SDK實作中啟用&#x200B;**使用第三方Cookie**&#x200B;設定。 如果使用標籤延伸，請在&#x200B;**[!UICONTROL Use third-party cookies]**&#x200B;身分組態設定[中啟用](/help/tags/extensions/client/web-sdk/configure/identity.md#use-third-party-cookies)。 如果使用JavaScript資料庫，請將[`thirdPartyCookiesEnabled`](/help/collection/js/commands/configure/thirdpartycookiesenabled.md)設為`true`。

1. **在資料流中啟用協力廠商ID同步**：在資料流的進階設定中啟用&#x200B;**[!UICONTROL Third-Party ID Sync]**&#x200B;選項。 請參閱[建立和設定資料串流](/help/datastreams/configure.md#advanced-options)。

1. **確定第一方持續性已就緒**：確認您的第一方持續性策略（例如FPID）已部署在您擁有的網域上。 檢視資料彙集[中的](fpid.md)第一方裝置識別碼。

## 驗證

若要確認統一身分支援是否正常運作：

1. 開啟瀏覽器的開發人員工具，並導覽至&#x200B;**網路**&#x200B;標籤。
1. 清除現有請求，並在新的或無痕工作階段中觸發網頁SDK事件（頁面載入或自訂事件）。
1. 尋找Edge Network回應（尋找`adobedc.demdex.net`和您的第一方收集端點的呼叫）。
1. 檢查ID同步指示的回應裝載。

當ID同步指示出現時，回應會包含類似下列的`identity:exchange`控制代碼：

```json
{
  "handle": [
    {
      "type": "identity:exchange",
      "payload": [
        {
          "type": "url",
          "id": 411,
          "spec": {
            "url": "https://example.com/...",
            "hideReferrer": false,
            "ttlMinutes": 10080
          }
        },
        {
          "type": "url",
          "id": 89,
          "spec": {
            "url": "https://example.org/...",
            "hideReferrer": true,
            "ttlMinutes": 10080
          }
        }
      ]
    }
  ]
}
```

| 元素 | 說明 |
| --- | --- |
| `type: "identity:exchange"` | 表示有ID同步指示。 |
| `payload`陣列 | 合作夥伴ID同步URL的清單。 |
| `url`個值 | 將URL重新導向至合作夥伴網域，以進行ID同步。 |
| `id`個值 | 合作夥伴識別碼。 |

>[!TIP]
>
>如果您在回應中看不到`identity:exchange`控制代碼：
>
>* 確保您使用新的或無痕瀏覽器工作階段進行測試。 現有身分不會觸發新同步。
>* 確認資料流和網頁SDK設定均已正確設定。
>* 確認您使用的瀏覽器支援第三方Cookie （請參閱下表）。

確認ID同步活動後，請驗證：

* 第一方身分會在您擁有的網域上跨頁面載入依預期持續存在。
* 在您支援的環境中，啟用和報告流程會如預期般運作。

## 瀏覽器相容性 {#browser-compatibility}

協力廠商身分識別功能取決於瀏覽器對協力廠商Cookie的支援。 下表總結了預期行為：

| 瀏覽器 | 協力廠商Cookie支援 | Demdex可用 | 身分行為 |
| --- | --- | --- | --- |
| Google Chrome | 支援 | 是 | Demdex→ECID （跨網域一致） |
| Microsoft Edge | 預設支援 | 是 | Demdex→ECID （跨網域一致） |
| Mozilla Firefox | 預設為封鎖(ETP) | 否（預設） | FPID→ECID （依網域） |
| Apple Safari | 已封鎖(ITP) | 無 | FPID→ECID （依網域） |

對於封鎖第三方Cookie的瀏覽器，第一方識別可繼續正常運作。 只有瀏覽器允許協力廠商Cookie時，才能使用協力廠商啟用功能。

## 限制

* 第三方身分行為完全取決於訪客的瀏覽器是否允許第三方Cookie。 在封鎖協力廠商啟用的瀏覽器中，協力廠商啟用沒有遞補功能。
* 自動連結需要訪客返回網站。 您符合協力廠商啟用資格的對象比例會隨著時間逐漸增加。
