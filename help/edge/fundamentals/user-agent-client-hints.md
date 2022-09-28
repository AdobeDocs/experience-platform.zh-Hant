---
title: 用戶代理客戶端提示
description: 了解Web SDK中的使用者代理用戶端提示如何運作
keywords: 用戶代理；客戶端提示；字串；用戶代理字串；低熵；高熵
source-git-commit: 6c974d1a646ff1f3a8f7ad9d67a6840391fc739e
workflow-type: tm+mt
source-wordcount: '1081'
ht-degree: 6%

---


# 用戶代理客戶端提示

## 總覽 {#overview}

每次網頁瀏覽器向網頁伺服器提出請求時，請求的標題都會包含有關瀏覽器和瀏覽器執行環境的資訊。 所有這些資料會匯總為字串，稱為 [!DNL User-Agent] 字串。

以下範例說明 [!DNL User-Agent] 字串在來自於 [!DNL Mac OS] 裝置。

>[!NOTE]
>
>多年來， [!DNL User-Agent] 字串已生長和修改多次。 以下範例顯示以下幾種最常見的 [!DNL User-Agent] 資訊。

```shell
Mozilla/5.0 (Macintosh; Intel Mac OS X 10_15_7) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/105.0.0.0 Safari/537.36`
```

| 欄位 | 值 |
|---|---|
| 軟體名稱 | Chrome |
| 軟體版本 | 105 |
| 完整軟體版本 | 105.0.0.0 |
| 版面引擎名稱 | AppleWebKit |
| 版面引擎版本 | 537.36 |
| 作業系統 | Mac OS X |
| 作業系統版本 | 10.15.7 |
| 裝置 | 英特爾Mac OS X 10_15_7 |

## 使用案例 {#use-cases}

[!DNL User-Agent] 字串一直以來都是行銷和開發團隊的重要工具，可讓您了解瀏覽器、作業系統和裝置如何顯示網站內容，以及使用者如何與網站互動。

[!DNL User-Agent] 字串也可用來封鎖垃圾訊息，並篩選出可編目網站以達到各種其他目的的機器人。

## [!DNL User-Agent] Adobe Experience Cloud中的字串 {#user-agent-in-adobe}

Adobe Experience Cloud解決方案利用 [!DNL User-Agent] 字串。

* Adobe Analytics利用 [!DNL User-Agent] 字串，擴大並衍生與用來造訪網站的作業系統、瀏覽器和裝置相關的其他資訊。
* Adobe Audience Manager和Adobe Target會根據 [!DNL User-Agent] 字串。

## 介紹用戶代理客戶端提示 {#ua-ch}

近年來，網站擁有者和行銷廠商已使用 [!DNL User-Agent] 字串，以及請求標題中包含的其他資訊，以建立數位指紋。 這些指紋可以用作在不知情的情況下識別用戶的手段。

儘管有重要的目的 [!DNL User-Agent] 網站擁有者提供的字串，瀏覽器開發人員已決定變更 [!DNL User-Agent] 字串操作，以限制一般使用者的潛在隱私權問題。

他們開發的解決方案稱為 [用戶代理客戶端提示](https://developer.chrome.com/docs/privacy-sandbox/user-agent/). 客戶端提示仍允許網站收集必要的瀏覽器、作業系統和設備資訊，同時提供更多保護，以防止隱蔽跟蹤方法（如指紋）。

客戶端提示允許網站所有者訪問 [!DNL User-Agent] 串，但更能保護隱私。

當新式瀏覽器將使用者傳送至Web伺服器時， [!DNL User-Agent] 字串會在每個要求時傳送，無論是否需要。 另一方面，客戶端提示強制執行一個模型，伺服器必須向瀏覽器詢問它想了解的有關客戶端的其他資訊。 收到此請求時，瀏覽器可套用其自己的原則或使用者設定，以判斷要傳回的資料。 而不是揭露整個 [!DNL User-Agent] 字串，現在以明確且可稽核的方式管理存取權。

## 瀏覽器支援 {#browser-support}

[用戶代理客戶端提示](https://developer.chrome.com/docs/privacy-sandbox/user-agent/) 是 [!DNL Google Chrome ]第89版。

其他基於Chromium的瀏覽器支援「客戶端提示」API，例如：

* [!DNL Microsoft Edge]
* [!DNL Opera]
* [!DNL Brave]
* [!DNL Chrome for Android]
* [!DNL Opera for Android]
* [!DNL Samsung Internet]

## 類別 {#categories}

用戶代理客戶端提示分為兩類：

* [低熵客戶端提示](#low-entropy)
* [高熵客戶端提示](#high-entropy)

### 低熵客戶端提示 {#low-entropy}

低熵客戶端提示包括不能用於指紋用戶的基本資訊。 瀏覽器品牌、平台等資訊，以及要求是否來自行動裝置。

Web SDK預設會啟用低熵用戶端提示，並會在每個要求時傳遞。

| HTTP 標頭 | JavaScript | 預設包含在使用者代理中 | 預設包含在客戶端提示中 |
|---|---|---|---|
| `Sec-CH-UA` | `brands` | 是 | 是 |
| `Sec-CH-UA-Platform` | `platform` | 是 | 是 |
| `Sec-CH-UA-Mobile` | `mobile` | 是 | 是 |

### 高熵客戶端提示 {#high-entropy}

高熵客戶端提示是有關客戶端設備的更詳細的資訊，如平台版本、體系結構、模型、位（64位或32位平台），或完整的作業系統版本。 此資訊可能用於指紋識別。

| HTTP 標頭 | JavaScript | 預設包含在使用者代理中 | 預設包含在「客戶端提示」中 |
|---|---|---|---|
| `Sec-CH-UA-Platform-Version` | `platformVersion` | 是 | 無 |
| `Sec-CH-UA-Arc` | `architecture` | 是 | 無 |
| `Sec-CH-UA-Model` | `model` | 是 | 無 |
| `Sec-CH-UA-Bitness` | `Bitness` | 是 | 無 |
| `Sec-CH-UA-Full-Version-List` | `fullVersionList` | 是 | 無 |

Web SDK預設會停用高熵用戶端提示。 要啟用它們，您必須手動配置Web SDK以請求高熵客戶端提示。

## 高熵客戶端提示對Experience Cloud解決方案的影響 {#impact-in-experience-cloud-solutions}

某些Adobe Experience Cloud解決方案在產生報表時，會仰賴高熵用戶端提示中包含的資訊。

如果您未在您的環境中啟用高熵客戶端提示，則Adobe Analytics和Audience Manager報表及以下說明的特徵將無法運作。

### Adobe Analytics報告依賴於高熵客戶端提示 {#analytics}

禁用高熵客戶端提示時，以下Adobe Analytics報告將無法工作。

* [瀏覽器](https://experienceleague.adobe.com/docs/analytics/components/dimensions/browser.html)
* [瀏覽器類型](https://experienceleague.adobe.com/docs/analytics/components/dimensions/browser-type.html)
* [作業系統](https://experienceleague.adobe.com/docs/analytics/components/dimensions/operating-systems.html)
* [作業系統類型](https://experienceleague.adobe.com/docs/analytics/components/dimensions/operating-system-types.html)
* [行動維度](https://experienceleague.adobe.com/docs/analytics/components/dimensions/mobile-dimensions.html)

### Audience Manager特徵依賴於高熵客戶端提示 {#aam}

如果您的Audience Manager特徵使用以下任何屬性，則必須啟用高熵客戶端提示。 否則，特徵將停止運作。

* 作業系統版本
* 裝置型號
* 裝置製造商
* 設備供應商

## 啟用高熵客戶端提示 {#enabling-high-entropy-client-hints}

若要在您的Web SDK部署上啟用高熵用戶端提示，您必須包含其他 `highEntropyUserAgentHints` 內容選項，如 [配置檔案](configuring-the-sdk.md#context)，以及您現有的設定。

例如，要從Web屬性中檢索高熵客戶端提示，您的配置如下所示：

`context: ["highEntropyUserAgentHints", "web"]`

## 範例 {#example}

瀏覽器向Web伺服器發出的第一個請求的標題中包含的客戶端提示將包含瀏覽器品牌、瀏覽器的主要版本以及客戶端是否為移動設備的指示器。 每個資料片段都有各自的標題值，而非分組為單一 [!DNL User-Agent] 字串，如下所示：

```shell
Sec-CH-UA: "Chromium";v="101", "Google Chrome";v="101", " Not;A Brand";v="99"

Sec-CH-UA-Mobile: ?0

Sec-CH-UA-Platform: "macOS
```

等價 [!DNL User-Agent] 相同瀏覽器的標題看起來會像這樣：

```shell
Mozilla/5.0 (Macintosh; Intel Mac OS X 10_15_7) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/101.0.4951.54 Safari/537.36
```

雖然資訊類似，但向伺服器發出的第一個請求包含客戶端提示。 這些僅包含 [!DNL User-Agent] 字串。 請求中缺少的是作業系統架構、完整作業系統版本、版面引擎名稱、版面引擎版本和完整瀏覽器版本。

不過，在後續的請求中， [!DNL Client Hints API] 允許Web伺服器詢問有關該設備的其他詳細資訊。 當請求這些值時，根據瀏覽器策略或用戶設定，瀏覽器響應可能包括該資訊。

以下是由 [!DNL Client Hints API] 請求高熵值時：


```json
{
   "architecture":"x86",
   "bitness":"64",
   "brands":[
      {
         "brand":" Not A;Brand",
         "version":"99"
      },
      {
         "brand":"Chromium",
         "version":"100"
      },
      {
         "brand":"Google Chrome",
         "version":"100"
      }
   ],
   "fullVersionList":[
      {
         "brand":" Not A;Brand",
         "version":"99.0.0.0"
      },
      {
         "brand":"Chromium",
         "version":"100.0.4896.127"
      },
      {
         "brand":"Google Chrome",
         "version":"100.0.4896.127"
      }
   ],
   "mobile":false,
   "model":"",
   "platformVersion":"12.2.1"
}
```
