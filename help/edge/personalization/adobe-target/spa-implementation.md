---
title: 適用於Adobe Experience Platform Web SDK的單頁應用程式實作
description: 了解如何使用Adobe Target建立Adobe Experience Platform Web SDK的單頁應用程式(SPA)實作。
keywords: target;adobe target;xdm檢視；檢視；單頁應用程式；SPA;SPA生命週期；用戶端；AB測試；AB；體驗鎖定目標；XT;VEC
exl-id: cc48c375-36b9-433e-b45f-60e6c6ea4883
source-git-commit: 0085306a2f5172eb19590cc12bc9645278bd2b42
workflow-type: tm+mt
source-wordcount: '1665'
ht-degree: 13%

---

# 實作單頁應用程式

Adobe Experience Platform Web SDK提供豐富的功能，讓貴公司能以新世代用戶端技術(例如單頁應用程式(SPA))為基礎進行個人化。

傳統的網站採用「頁面至頁面」導覽模型 (又稱為「多頁應用程式」)，網站設計與 URL 緊密結合，而從某網頁轉換到另一個網頁，需要頁面載入。

單頁應用程式等現代Web應用程式已改採可加速瀏覽器UI轉譯的模型，這種轉譯通常與頁面重新載入無關。 這些體驗可由客戶互動觸發，例如捲動、點按和游標移動。 隨著現代網路的范式不斷演化，傳統通用事件（例如頁面載入）與部署個人化和實驗的相關性已失效。

![](assets/spa-vs-traditional-lifecycle.png)

## 適用於SPA的Platform Web SDK的優點

以下為將Adobe Experience Platform Web SDK用於單頁應用程式的幾項優點：

* 可在頁面載入時快取所有選件，以減少對單一伺服器呼叫發出的多個伺服器呼叫。
* 大幅改善網站上的使用者體驗，因為選件會透過快取立即顯示，而不會因傳統伺服器呼叫而造成延遲時間。
* 一行程式碼和一次性開發人員設定可讓行銷人員透過SPA上的可視化體驗撰寫器(VEC)建立和執行A/B和體驗鎖定目標(XT)活動。

## XDM檢視和單頁應用程式

適用於SPA的Adobe Target VEC充分運用了「檢視」的概念：視覺元素的邏輯群組，可共同組成SPA體驗。 因此，單頁應用程式可視為根據使用者互動轉換檢視，而非轉換URL。 檢視通常可代表整個網站或網站內的分組視覺元素。

為進一步說明檢視，下列範例使用在React中實作的假想線上電子商務網站來探索檢視範例。

導覽至首頁後，主圖影像會促銷復活節特賣活動以及網站上可用的最新產品。 在此情況下，可以為整個主畫面定義檢視。 這種觀點可以簡單地稱為「家」。

![](assets/example-views.png)

隨著客戶對企業銷售的產品越來越感興趣，他們決定按一下 **產品** 連結。 與首頁相似，產品網站整體可定義為一個檢視。此檢視可命名為「products-all」。

![](assets/example-products-all.png)

由於檢視可定義為整個網站或網站上的一組視覺元素，因此產品網站上顯示的四個產品可分組並視為檢視。 此檢視可命名為「products」。

![](assets/example-products.png)

客戶決定按一下 **載入更多** 按鈕來探索網站上的更多產品，這種情況下網站URL不會變更，但您可以在此處建立檢視，僅代表所顯示的第二列產品。 檢視名稱可以是「products-page-2」。

![](assets/example-load-more.png)

客戶決定從網站購買幾項產品，然後繼續到結帳畫面。 在結帳站點，系統會為客戶提供選擇一般送貨或快遞的選項。 檢視可以是網站上的任何視覺元素群組，因此可針對傳送偏好設定建立檢視，並稱為「傳送偏好設定」。

![](assets/example-check-out.png)

檢視的概念可進一步延伸。 這些只是可在網站上定義的幾個檢視範例。

## 實作XDM檢視

可在Adobe Target中運用XDM檢視，讓行銷人員透過可視化體驗撰寫器在SPA上執行A/B和XT測試。 若要完成一次性開發人員設定，必須執行下列步驟：

1. 安裝 [Adobe Experience Platform Web SDK](../../fundamentals/installing-the-sdk.md)
2. 決定您要個人化的單頁應用程式中的所有XDM檢視。
3. 定義XDM檢視後，若要傳送AB或XT VEC活動，請實作 `sendEvent()` 函式 `renderDecisions` 設為 `true` 和單頁應用程式中對應的XDM檢視。 必須傳入XDM檢視 `xdm.web.webPageDetails.viewName`. 此步驟可讓行銷人員運用可視化體驗撰寫器，為這些XDM啟動A/B和XT測試。

   ```javascript
   alloy("sendEvent", { 
     "renderDecisions": true, 
     "xdm": { 
       "web": { 
         "webPageDetails": { 
         "viewName":"home" 
         }
       } 
     } 
   });
   ```

>[!NOTE]
>
>第一個 `sendEvent()` 呼叫，系統會擷取並快取所有應轉譯給使用者的XDM檢視。 後續 `sendEvent()` 傳入XDM檢視的呼叫將從快取中讀取，且不需伺服器呼叫即可呈現。

## `sendEvent()` 函式範例

本節概述三個範例，說明如何叫用 `sendEvent()` 函式（在React中）以取得假想的電子商務SPA。

### 範例1:A/B測試首頁

行銷團隊想要在整個首頁上執行A/B測試。

![](assets/use-case-1.png)

要在整個主站點上運行A/B測試， `sendEvent()` 必須與XDM叫用 `viewName` 設為 `home`:

```jsx
function onViewChange() { 
  
  var viewName = window.location.hash; // or use window.location.pathName if router works on path and not hash 

  viewName = viewName || 'home'; // view name cannot be empty 

  // Sanitize viewName to get rid of any trailing symbols derived from URL 

  if (viewName.startsWith('#') || viewName.startsWith('/')) { 
    viewName = viewName.substr(1); 
  }
   
  alloy("sendEvent", { 
    "renderDecisions": true, 
    "xdm": { 
      "web": { 
        "webPageDetails": { 
          "viewName":"home" 
        } 
      } 
    }
  }); 
} 

// react router v4 

const history = syncHistoryWithStore(createBrowserHistory(), store); 

history.listen(onViewChange); 

// react router v3 

<Router history={hashHistory} onUpdate={onViewChange} > 
```

### 範例2:個人化產品

行銷團隊想要將使用者點按後的價格標籤顏色變更為紅色，以個人化第二列產品 **載入更多**.

![](assets/use-case-2.png)

```jsx
function onViewChange(viewName) { 

  alloy("sendEvent", { 
    "renderDecisions": true, 
    "xdm": { 
      "web": { 
        "webPageDetails": { 
          "viewName": viewName
        }
      } 
    } 
  }); 
} 

class Products extends Component { 
  
  render() { 
    return ( 
      <button type="button" onClick={this.handleLoadMoreClicked}>Load more</button> 
    ); 
  } 

  handleLoadMoreClicked() { 
    var page = this.state.page + 1; // assuming page number is derived from component’s state 
    this.setState({page: page}); 
    onViewChange('PRODUCTS-PAGE-' + page); 
  } 

} 
```

### 範例3:A/B測試傳送偏好設定

行銷團隊想執行A/B測試，以查看按鈕的顏色是否在 **快遞** 選取「 」可增加轉換次數（與兩個傳送選項的按鈕均保持藍色相反）。

![](assets/use-case-3.png)

若要根據選取的傳送偏好設定個人化網站上的內容，可針對每個傳送偏好設定建立一個檢視。 當 **正常傳送** ，則可將「檢視」命名為「checkout-normal」。 若 **快遞** ，則可將「檢視」命名為「checkout-express」。

```jsx
function onViewChange(viewName) { 
  alloy("sendEvent", { 
    "renderDecisions": true, 
    "xdm": { 
      "web": { 
        "webPageDetails": { 
          "viewName": viewName 
        }
      }
    }
  }); 
} 

class Checkout extends Component { 

  render() { 
    return ( 
      <div onChange={this.onDeliveryPreferenceChanged}> 
        <label> 
          <input type="radio" id="normal" name="deliveryPreference" value={"Normal Delivery"} defaultChecked={true}/> 
          <span> Normal Delivery (7-10 business days)</span> 
        </label> 
        <label> 
          <input type="radio" id="express" name="deliveryPreference" value={"Express Delivery"}/> 
          <span> Express Delivery* (2-3 business days)</span> 
        </label> 
      </div> 
    ); 
  } 

  onDeliveryPreferenceChanged(evt) { 
    var selectedPreferenceValue = evt.target.value; 
    onViewChange(selectedPreferenceValue); 
  } 

} 
```

## 使用適用於SPA的可視化體驗撰寫器

完成XDM檢視的定義並實作後 `sendEvent()` 傳入這些XDM檢視後，VEC就能偵測這些檢視，並允許使用者建立A/B或XT活動的動作和修改。

>[!NOTE]
>
>若要針對SPA使用VEC，您必須安裝並啟用 [Firefox](https://addons.mozilla.org/en-US/firefox/addon/adobe-target-vec-helper/) 或 [鉻黃](https://chrome.google.com/webstore/detail/adobe-target-vec-helper/ggjpideecfnbipkacplkhhaflkdjagak) VEC Helper擴充功能。

### 「修改」面板

「修改」面板會擷取為特定檢視建立的動作。 視圖的所有操作都在該視圖下分組。

![](assets/modifications-panel.png)

### 動作

按一下動作會醒目顯示將套用該動作之網站上的元素。在檢視下建立的每個VEC動作都有下列圖示： **資訊**, **編輯**, **原地複製**, **移動**，和 **刪除**. 下表將詳細說明這些表徵圖。

![](assets/action-icons.png)

| 圖示 | 說明 |
|---|---|
| 資訊 | 顯示此動作的詳細資料。 |
| 編輯 | 可讓您直接編輯該動作的屬性。 |
| 原地複製 | 將動作原地複製至一或多個存在於修改面板上的檢視，或原地複製至一或多個您已在 VEC 中瀏覽及導覽的目標檢視。動作未必會存在於修改面板中。<br/><br/>**注意：** 執行原地復製作業後，您必須透過瀏覽導覽至VEC中的檢視，才能查看原地複製動作是否為有效作業。 如果無法將動作套用到檢視，則會出現錯誤. |
| 移動 | 可將動作移動至頁面載入事件，或修改面板中已存在的任何其他檢視。<br/><br/>**頁面載入事件：** 任何對應至頁面載入事件的動作都會套用至網頁應用程式的初始頁面載入上。 <br/><br/>**注意：** 執行移動作業後，您必須透過瀏覽導覽至VEC中的檢視，才能查看該移動作業是否有效。 如果無法將動作套用到檢視，則會出現錯誤. |
| 刪除 | 刪除動作。 |

## 使用VEC取得SPA範例

本節概述使用可視化體驗撰寫器來建立A/B或XT活動之動作和修改的三個範例。

### 範例1:更新「首頁」視圖

在本文檔的前面，為整個首頁定義了一個名為「home」的視圖。 現在，行銷團隊想要以下列方式更新「首頁」檢視：

* 變更 **新增至購物車** 和 **贊** 按鈕以更淺的藍色。 這應會在頁面載入期間發生，因為涉及變更標頭的元件。
* 變更 **2019年最新產品** 標籤為 **2019年最熱的產品** 並將文字顏色變更為紫色。

若要在VEC中進行這些更新，請選取 **撰寫** 並將這些變更套用至「首頁」檢視。

![](assets/vec-home.png)

### 範例2:變更產品標籤

對於「products-page-2」檢視，行銷團隊想要變更 **價格** 標籤為 **售價** 並將標籤顏色變更為紅色。

若要在VEC中進行這些更新，需執行下列步驟：

1. 選擇 **瀏覽** 在VEC中。
2. 選擇 **產品** ，即可檢視此屬性。
3. 選擇 **載入更多** 一次，檢視產品的第二列。
4. 選擇 **撰寫** 在VEC中。
5. 套用動作以將文字標籤變更為 **售價** 顏色變成紅色。

![](assets/vec-products-page-2.png)

### 範例3:個人化傳送偏好設定樣式

檢視可在精細層級定義，例如選項按鈕的狀態或選項。 在本檔案的前面，已針對傳送偏好設定、「checkout-normal」和「checkout-express」定義檢視。 行銷團隊想要將「checkout-express」檢視的按鈕顏色變更為紅色。

若要在VEC中進行這些更新，需執行下列步驟：

1. 選擇 **瀏覽** 在VEC中。
2. 將產品新增至網站上的購物車。
3. 選取網站右上角的購物車圖示。
4. 選擇 **結帳訂單**.
5. 選取 **快遞** 選項按鈕 **傳送偏好設定**.
6. 選擇 **撰寫** 在VEC中。
7. 變更 **支付** 按鈕顏色變為紅色。

>[!NOTE]
>
>「checkout-express」檢視不會出現在「修改」面板中，直到 **快遞** 選項按鈕。 這是因為 `sendEvent()` 函式於 **快遞** 已選取選項按鈕，因此在選取選項按鈕之前，VEC不會察覺「checkout-express」檢視。

![](assets/vec-delivery-preference.png)
