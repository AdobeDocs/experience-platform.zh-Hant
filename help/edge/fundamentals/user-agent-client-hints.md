---
title: 用戶代理客戶端提示
description: 瞭解Web SDK中用戶代理客戶端提示的工作方式。 客戶端提示允許網站所有者訪問用戶 — 代理字串中提供的大部分相同資訊，但是以更加保護隱私的方式。
keywords: 用戶代理；客戶提示；user agent;client hints;字串；用戶代理字串；低熵；高熵
exl-id: a909b1d1-be9d-43ba-bb4b-d28b0c609f65
source-git-commit: 29679e85943f16bcb02064cc60a249a3de61e022
workflow-type: tm+mt
source-wordcount: '1155'
ht-degree: 7%

---

# 用戶代理客戶端提示

## 總覽 {#overview}

每次Web瀏覽器向Web伺服器發出請求時，請求的標題都包括有關瀏覽器和瀏覽器運行所在環境的資訊。 所有這些資料都聚合到一個字串中，稱為 [!DNL User-Agent] 的下界。

這是一個 [!DNL User-Agent] 字串在從運行於 [!DNL Mac OS] 設備。

>[!NOTE]
>
>在多年中，包含在 [!DNL User-Agent] 字串已多次增長和修改。 以下示例顯示了對 [!DNL User-Agent] 的下界。

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
| 裝置 | 英特爾MacOS X 10_15_7 |

## 使用案例 {#use-cases}

[!DNL User-Agent] 長期以來，字串一直被用來為營銷和開發團隊提供重要的洞見，讓他們瞭解瀏覽器、作業系統和設備如何顯示網站內容，以及用戶如何與網站交互。

[!DNL User-Agent] 字串還用於阻止垃圾郵件和過濾為各種其他目的爬網站點的bot。

## [!DNL User-Agent] Adobe Experience Cloud {#user-agent-in-adobe}

Adobe Experience Cloud解決方案利用 [!DNL User-Agent] 弦的形形色色。

* Adobe Analytics利用 [!DNL User-Agent] 字串，用於補充和導出與用於訪問網站的作業系統、瀏覽器和設備相關的其他資訊。
* Adobe Audience Manager和Adobe Target根據由IMF提供的資訊，確定最終用戶的細分和個性化活動 [!DNL User-Agent] 的下界。

## 介紹用戶代理客戶端提示 {#ua-ch}

近年來，網站所有者和營銷供應商都使用 [!DNL User-Agent] 字串以及請求標頭中包含的其他資訊，以建立數字指紋。 這些指紋可以用作在用戶不知情的情況下識別用戶的手段。

儘管有重要的目的 [!DNL User-Agent] 為站點所有者服務的字串，瀏覽器開發人員決定改變 [!DNL User-Agent] 字串操作，以限制最終用戶的潛在隱私問題。

他們開發的解決方案稱為 [用戶代理客戶端提示](https://developer.chrome.com/docs/privacy-sandbox/user-agent/)。 客戶端提示仍允許網站收集必要的瀏覽器、作業系統和設備資訊，同時還可以增強對隱蔽跟蹤方法（如指紋）的保護。

客戶端提示允許網站所有者訪問中提供的大部分相同資訊 [!DNL User-Agent] 串，但更能保護隱私。

當現代瀏覽器將用戶發送到Web伺服器時， [!DNL User-Agent] 無論是否需要字串，都會在每個請求上發送字串。 另一方面，客戶端提示則強制實施一個模型，在該模型中，伺服器必須向瀏覽器詢問其希望瞭解的有關客戶端的其他資訊。 在接收到此請求時，瀏覽器可以應用其自己的策略或用戶配置來確定返回哪些資料。 而不是暴露 [!DNL User-Agent] 預設情況下，所有請求都使用字串，現在以顯式和可審核的方式管理訪問。

## 瀏覽器支援 {#browser-support}

[用戶代理客戶端提示](https://developer.chrome.com/docs/privacy-sandbox/user-agent/) 是 [!DNL Google Chrome ]版本89。

其他基於鉻的瀏覽器支援客戶端提示API，例如：

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

低熵客戶端提示包括不能用於指紋用戶的基本資訊。 諸如瀏覽器品牌、平台以及請求是否來自移動設備等資訊。

預設情況下，在Web SDK中啟用低熵客戶端提示，並在每個請求上傳遞。

| HTTP 標頭 | JavaScript | 預設情況下包括在用戶代理中 | 預設情況下包括在客戶端提示中 |
|---|---|---|---|
| `Sec-CH-UA` | `brands` | 是 | 是 |
| `Sec-CH-UA-Platform` | `platform` | 是 | 是 |
| `Sec-CH-UA-Mobile` | `mobile` | 是 | 是 |

### 高熵客戶端提示 {#high-entropy}

高熵客戶端提示是有關客戶端設備的更詳細的資訊，如平台版本、體系結構、型號、位（64位或32位平台）或完整作業系統版本。 此資訊可能用於指紋。

| HTTP 標頭 | JavaScript | 預設情況下包括在用戶代理中 | 預設情況下包括在客戶端提示中 |
|---|---|---|---|
| `Sec-CH-UA-Platform-Version` | `platformVersion` | 是 | 無 |
| `Sec-CH-UA-Arc` | `architecture` | 是 | 無 |
| `Sec-CH-UA-Model` | `model` | 是 | 無 |
| `Sec-CH-UA-Bitness` | `Bitness` | 是 | 無 |
| `Sec-CH-UA-Full-Version-List` | `fullVersionList` | 是 | 無 |

預設情況下，Web SDK會禁用高熵客戶端提示。 要啟用它們，必須手動配置Web SDK以請求高熵客戶端提示。

## 高熵客戶端提示對Experience Cloud解決方案的影響 {#impact-in-experience-cloud-solutions}

一些Adobe Experience Cloud解決方案在生成報告時依賴於包含在高熵客戶端提示中的資訊。

如果未在您的環境中啟用高熵客戶端提示，則下面介紹的Adobe Analytics和Audience Manager報告和特性將不起作用。

### Adobe Analytics報告依賴高熵客戶端提示 {#analytics}

的 [作業系統](https://experienceleague.adobe.com/docs/analytics/components/dimensions/operating-systems.html?lang=zh-Hant) 維包括作為高熵客戶端提示儲存的作業系統版本。 如果未啟用高熵客戶端提示，則對於從Crr瀏覽器收集的點擊，作業系統版本可能不準確。

### Audience Manager特徵依賴於高熵客戶端提示 {#aam}

[!DNL Google] 已更新 [!DNL Chrome] 瀏覽器功能，使通過 `User-Agent` 標題。 因此，Audience Manager客戶使用 [DIL](https://experienceleague.adobe.com/docs/audience-manager/user-guide/dil-api/dil-overview.html?lang=en) 將不再獲得基於特徵的可靠資訊 [平台級密鑰](https://experienceleague.adobe.com/docs/audience-manager/user-guide/features/traits/trait-device-targeting.html?lang=zh-Hant)。

Audience Manager使用平台級密鑰進行目標的客戶必須切換到 [Experience PlatformWeb SDK](https://experienceleague.adobe.com/docs/experience-platform/edge/home.html?lang=zh-Hant) 而不是 [DIL](https://experienceleague.adobe.com/docs/audience-manager/user-guide/dil-api/dil-overview.html?lang=en)，啟用 [高熵客戶端提示](#enabling-high-entropy-client-hints) 繼續接收可靠的性狀資料。

## 啟用高熵客戶端提示 {#enabling-high-entropy-client-hints}

要在Web SDK部署中啟用高熵客戶端提示，必須包括 `highEntropyUserAgentHints` context選項，如中所述 [配置文檔](configuring-the-sdk.md#context)，與現有配置一起使用。

例如，要從Web屬性中檢索高熵客戶端提示，您的配置將如下所示：

`context: ["highEntropyUserAgentHints", "web"]`

## 範例 {#example}

瀏覽器向Web伺服器發出的第一個請求的標題中包含的客戶端提示將包含瀏覽器品牌、瀏覽器的主要版本以及客戶端是否是移動設備的指示器。 每段資料將具有其自己的標題值，而不是分組為單個 [!DNL User-Agent] 字串，如下所示：

```shell
Sec-CH-UA: "Chromium";v="101", "Google Chrome";v="101", " Not;A Brand";v="99"

Sec-CH-UA-Mobile: ?0

Sec-CH-UA-Platform: "macOS
```

等效 [!DNL User-Agent] 同一瀏覽器的標題如下所示：

```shell
Mozilla/5.0 (Macintosh; Intel Mac OS X 10_15_7) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/101.0.4951.54 Safari/537.36
```

雖然資訊相似，但向伺服器發出的第一個請求包含客戶端提示。 這些僅包括中可用內容的子集 [!DNL User-Agent] 的下界。 請求中缺少作業系統體系結構、完整作業系統版本、佈局引擎名稱、佈局引擎版本和完整瀏覽器版本。

然而，於隨後之要求時，本 [!DNL Client Hints API] 允許web伺服器詢問有關該設備的其他詳細資訊。 當根據瀏覽器策略或用戶設定請求這些值時，瀏覽器響應可能包括該資訊。

下面是由 [!DNL Client Hints API] 請求高熵值時：


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
