---
title: Adobe Experience Platform Web SDK的單頁應用程式實作
description: 瞭解如何使用Adobe Target建立Adobe Experience Platform Web SDK的單頁應用程式(SPA)實作。
keywords: target；adobe target；xdm檢視；檢視；單頁應用程式；SPA；SPA生命週期；使用者端；AB測試；AB；體驗鎖定目標；XT；VEC
exl-id: cc48c375-36b9-433e-b45f-60e6c6ea4883
source-git-commit: b6e084d2beed58339191b53d0f97b93943154f7c
workflow-type: tm+mt
source-wordcount: '1817'
ht-degree: 7%

---


# 實作單頁應用程式

Adobe Experience Platform Web SDK提供豐富的功能，讓貴公司能以新世代使用者端技術(例如單頁應用程式(SPA))為基礎進行個人化。

傳統網站採用「頁面至頁面」導覽模型（又稱為「多頁應用程式」），網站設計與URL緊密結合，而從某網頁轉換到另一個網頁，需要頁面載入。

單頁應用程式等新式Web應用程式已改為採用可加快瀏覽器UI呈現速度的模型，且通常與頁面重新載入無關。 這些體驗可由客戶互動觸發，例如捲動、點按和游標移動。 隨著現代網路環境的不斷演化，傳統的一般事件（例如頁面載入）與部署個人化和實驗不再具有相關性。

![與傳統頁面生命週期比較，顯示SPA生命週期的圖表。](assets/spa-vs-traditional-lifecycle.png)

## 適用於SPA的Platform Web SDK的優點

以下是為單頁應用程式使用Adobe Experience Platform Web SDK的一些好處：

* 可在頁面載入時快取所有選件，以減少對單一伺服器呼叫發出的多個伺服器呼叫。
* 顯著改善網站的使用者體驗，因為選件可透過快取立即顯示，避免傳統伺服器呼叫造成的時間延遲。
* 只要編寫一行程式碼和進行開發人員一次性設定，行銷人員就能透過SPA上的視覺化體驗撰寫器(VEC)建立及執行A/B和體驗鎖定目標(XT)活動。

## xdm檢視和單頁應用程式

適用於SPA的Adobe Target VEC充分利用「檢視」的概念：視覺化元素的邏輯組合，共同構成SPA體驗。 因此，單頁應用程式可視為根據使用者互動轉換檢視，而不是轉換URL。 檢視通常可代表整個網站或網站內的分組視覺元素。

為了進一步說明什麼是檢視，以下範例使用在React中實作的假想線上電子商務網站來探索範例檢視。

導覽至首頁後，主圖影像會宣傳復活節特賣以及網站上提供的最新產品。 在這種情況下，可以為整個主畫面定義檢視。 此檢視可以簡單地稱為「home」。

![瀏覽器視窗中單頁應用程式的影像範例。](assets/example-views.png)

當客戶對業務所銷售的產品越來越感興趣時，他們決定按一下 **產品** 連結。 與首頁相似，產品網站整體可定義為一個檢視。此檢視可命名為「products-all」。

![瀏覽器視窗中單頁應用程式的範例影像，其中顯示所有產品。](assets/example-products-all.png)

由於檢視可定義為整個網站或網站上一組視覺元素，因此產品網站上顯示的四個產品可分組並視為檢視。 此檢視可命名為「products」。

![瀏覽器視窗中單頁應用程式的範例影像，其中顯示範例產品。](assets/example-products.png)

當客戶決定按一下 **載入更多** 按鈕瀏覽網站上的更多產品，在此情況下，網站URL不會變更，但可在此處建立檢視，以僅代表顯示的第二列產品。 檢視名稱可以是「products-page-2」。

![瀏覽器視窗中單頁應用程式的範例影像，其他頁面上會顯示範例產品。](assets/example-load-more.png)

客戶決定從網站購買一些產品，然後進入結帳畫面。 在結帳站台，客戶可以選擇一般配送或快捷配送。 檢視可以是網站上的任何一組視覺元素，因此可以為傳遞偏好設定建立檢視，並稱為「傳遞偏好設定」。

![瀏覽器視窗中單頁應用程式結帳頁面的範例影像。](assets/example-check-out.png)

檢視的概念可以進一步延伸。 以下只是可在網站上定義的一些檢視範例。

## 實施XDM檢視

在Adobe Target中可運用XDM檢視，讓行銷人員透過視覺化體驗撰寫器在SPA上執行A/B和XT測試。 若要完成一次性開發人員設定，需要執行下列步驟：

1. 安裝 [Adobe Experience Platform Web SDK](/help/web-sdk/install/overview.md)
2. 決定您單頁應用程式中要個人化的所有XDM檢視。
3. 定義XDM檢視後，為傳送AB或XT VEC活動，請實作 `sendEvent()` 函式為 `renderDecisions` 設為 `true` 以及單頁應用程式中對應的XDM檢視。 XDM檢視必須傳入 `xdm.web.webPageDetails.viewName`. 此步驟可讓行銷人員運用視覺化體驗撰寫器，針對這些XDM啟動A/B和XT測試。

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
>在第一個 `sendEvent()` 呼叫，將會擷取並快取所有應該轉譯給使用者的XDM檢視。 後續 `sendEvent()` 含有傳入的XDM檢視的呼叫將會從快取中讀取並轉譯，不需要伺服器呼叫。

## `sendEvent()` 函式範例

本節概述三個範例，說明如何叫用 `sendEvent()` 函式在React中，用於假設性的電子商務SPA。

### 範例1：A/B測試首頁

行銷團隊想要在整個首頁上執行A/B測試。

![瀏覽器視窗中單頁應用程式的影像範例。](assets/use-case-1.png)

若要在整個主網站上執行A/B測試， `sendEvent()` 必須透過XDM叫用 `viewName` 設為 `home`：

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

### 範例2：個人化產品

行銷團隊想要在使用者點按後，將價格標籤的顏色變更為紅色，藉以個人化第二列產品 **載入更多**.

![瀏覽器視窗中單頁應用程式的範例影像，顯示個人化優惠方案。](assets/use-case-2.png)

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
    var page = this.state.page + 1; // assuming page number is derived from component's state 
    this.setState({page: page}); 
    onViewChange('PRODUCTS-PAGE-' + page); 
  } 

} 
```

### 範例3：A/B測試傳送偏好設定

行銷團隊想要執行A/B測試，以瞭解何時將按鈕的顏色從藍色變更為紅色 **快速運送** 選取可以提高轉換次數（與讓兩個傳送選項的按鈕顏色保持藍色相反）。

![瀏覽器視窗中具有A/B測試的單頁應用程式影像範例。](assets/use-case-3.png)

若要根據選取的傳遞偏好設定個人化網站內容，可針對每個傳遞偏好設定建立「檢視」。 時間 **正常傳遞** 選取時，可將「檢視」命名為「checkout-normal」。 如果 **快速運送** 選取時，可將檢視命名為「checkout-express」。

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

## 使用適用於SPA的視覺化體驗撰寫器

當您完成定義XDM檢視並實作時 `sendEvent()` 透過傳入這些XDM檢視，VEC將能夠偵測這些檢視，並允許使用者建立A/B或XT活動的動作或修改。

>[!NOTE]
>
>若要針對SPA使用VEC，您必須安裝並啟用 [Firefox](https://addons.mozilla.org/en-US/firefox/addon/adobe-target-vec-helper/) 或 [鉻黃](https://chrome.google.com/webstore/detail/adobe-target-vec-helper/ggjpideecfnbipkacplkhhaflkdjagak) VEC Helper擴充功能。

### 「修改」面板

「修改」面板會擷取為特定檢視所建立的動作。 「檢視」的所有動作會分組到「該檢視」下。

![瀏覽器視窗的側邊欄中顯示具有頁面載入選項的「修改」面板。](assets/modifications-panel.png)

### 動作

按一下動作會醒目顯示將套用該動作之網站上的元素。在檢視下建立的每個VEC動作都有下列圖示： **資訊**， **編輯**， **原地複製**， **移動**、和 **刪除**. 下表會詳細說明這些圖示。

![動作圖示](assets/action-icons.png)

| 圖示 | 說明 |
|---|---|
| 資訊 | 顯示此動作的詳細資料。 |
| 編輯 | 可讓您直接編輯該動作的屬性。 |
| 原地複製 | 將動作原地複製至一或多個存在於修改面板上的檢視，或原地複製至一或多個您已在VEC中瀏覽及導覽的目標檢視。 動作未必會存在於修改面板中。<br/><br/>**注意：** 完成復製作業後，您必須透過瀏覽導覽至VEC中的檢視，才能檢視該複製動作的作業是否有效。 如果無法將動作套用到檢視，則會出現錯誤. |
| 移動 | 可將動作移動至頁面載入事件，或修改面板中已存在的任何其他檢視。<br/><br/>**頁面載入事件：** 任何對應至頁面載入事件的動作，都會套用到網頁應用程式的初始頁面載入上。 <br/><br/>**注意：** 執行移動作業後，您必須透過瀏覽導覽至VEC中的檢視，才能檢視該移動作業是否有效。 如果無法將動作套用到檢視，則會出現錯誤. |
| 刪除 | 刪除動作。 |

## 使用適用於SPA的VEC範例

本節概述三個使用視覺化體驗撰寫器建立A/B或XT活動之動作和修改的範例。

### 範例1：更新「首頁」檢視

在此檔案的早些時候，曾為整個首頁網站定義名為「home」的檢視。 現在，行銷團隊想要以下列方式更新「首頁」檢視：

* 變更 **加入購物車** 和 **按讚** 按鈕變淺為藍色。 這應在頁面載入期間發生，因為它涉及變更標題的元件。
* 變更 **2019年最新產品** 標籤到 **2019年最暢銷產品** 並將文字顏色變更為紫色。

若要在VEC中進行這些更新，請選取 **撰寫** 並將這些變更套用至「首頁」檢視。

![視覺化體驗撰寫器範例頁面。](assets/vec-home.png)

### 範例2：變更產品標籤

針對「products-page-2」檢視，行銷團隊想要變更 **價格** 標籤到 **售價** 並將標籤顏色變更為紅色。

若要在VEC中進行這些更新，需執行下列步驟：

1. 選取 **瀏覽** （在VEC中）。
2. 選取 **產品** 在網站頂端導覽列中。
3. 選取 **載入更多** 一次，以檢視產品的第二列。
4. 選取 **撰寫** （在VEC中）。
5. 套用動作以將文字標籤變更為 **售價** 顏色變成紅色。

![具有產品標籤的視覺化體驗撰寫器範例頁面。](assets/vec-products-page-2.png)

### 範例3：個人化傳送偏好設定樣式

您可以在精細層次定義檢視，例如單選按鈕的狀態或選項。 本檔案先前針對傳遞偏好設定「checkout-normal」和「checkout-express」定義了「檢視」。 行銷團隊想要將「checkout-express」檢視的按鈕顏色變更為紅色。

若要在VEC中進行這些更新，需執行下列步驟：

1. 選取 **瀏覽** （在VEC中）。
2. 將產品新增至網站上的購物車。
3. 選取網站右上角的購物車圖示。
4. 選取 **結帳訂單**.
5. 選取 **快速運送** 下的選項按鈕 **傳遞偏好設定**.
6. 選取 **撰寫** （在VEC中）。
7. 變更 **付款** 按鈕顏色變成紅色。

>[!NOTE]
>
>「checkout-express」檢視不會出現在修改面板中，直到 **快速運送** 已選取選項按鈕。 這是因為 `sendEvent()` 函式執行時機 **快速運送** 因為已選取選項按鈕，所以VEC不會察覺「checkout-express」檢視，直到選取選項按鈕為止。

![視覺化體驗撰寫器顯示傳遞偏好設定選擇器。](assets/vec-delivery-preference.png)
