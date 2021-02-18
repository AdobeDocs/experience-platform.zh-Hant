---
title: Adobe Experience Platform Web SDK的單頁應用程式實作
description: 瞭解如何使用Adobe Target建立Adobe Experience Platform Web SDK的單頁應用程式(SPA)實作。
keywords: target;adobe target;xdm檢視；視圖；單頁應用程式；SPA;SPA生命週期；客戶端；AB測試；AB；體驗目標；XT;VEC
translation-type: tm+mt
source-git-commit: 69f2e6069546cd8b913db453dd9e4bc3f99dd3d9
workflow-type: tm+mt
source-wordcount: '1665'
ht-degree: 12%

---


# 單頁應用程式實作

Adobe Experience Platform Web SDK提供多樣化功能，讓您的企業能夠運用新一代的用戶端技術(例如單頁應用程式(SPA))進行個人化。

傳統的網站採用「頁面至頁面」導覽模型 (又稱為「多頁應用程式」)，網站設計與 URL 緊密結合，而從某網頁轉換到另一個網頁，需要頁面載入。

現代的Web應用程式（例如單頁應用程式）則採用一種模型，可快速使用瀏覽器UI轉換，這通常不受頁面重新載入的影響。 客戶互動（例如捲動、點按和游標移動）可觸發這些體驗。 隨著現代網路的范式演變，傳統通用事件（例如頁面載入）與部署個人化和實驗的關聯性不再有效。

![](assets/spa-vs-traditional-lifecycle.png)

## 適用於SPA的平台網頁SDK的優點

以下是將Adobe Experience Platform Web SDK用於單頁應用程式的一些優點：

* 可在頁面載入時快取所有選件，以減少對單一伺服器呼叫發出的多個伺服器呼叫。
* 大幅改善您網站上的使用者體驗，因為選件會立即透過快取顯示，而不會因傳統伺服器呼叫而延遲。
* 單一程式碼行和一次性開發人員設定可讓行銷人員透過SPA上的Visual Experience Composer(VEC)建立並執行A/B和Experience Targeting(XT)活動。

## XDM檢視和單頁應用程式

適用於SPA的Adobe Target VEC運用了稱為「檢視」的概念：邏輯的視覺元素群組，可組成SPA體驗。 因此，根據使用者互動，單頁應用程式可視為透過檢視進行轉換，而非URL。 檢視通常可代表整個網站或網站內的分組視覺元素。

為進一步說明「檢視」是什麼，下列範例使用React中建置的虛擬線上電子商務網站來探索範例「檢視」。

導覽至首頁後，英雄影像會促銷復活節銷售，以及網站上最新推出的產品。 在這種情況下，可以為整個主螢幕定義視圖。 此視圖可簡稱為「首頁」。

![](assets/example-views.png)

隨著客戶對企業所銷售的產品越來越感興趣，他們決定按一下&#x200B;**產品**&#x200B;連結。 與首頁相似，產品網站整體可定義為一個檢視。此檢視可命名為「產品——全部」。

![](assets/example-products-all.png)

由於「檢視」可定義為整個網站或網站上的一組視覺元素，因此產品網站上顯示的四種產品可分組，並視為「檢視」。 此檢視可命名為「產品」。

![](assets/example-products.png)

當客戶決定按一下&#x200B;**載入更多**&#x200B;按鈕以探索網站上的更多產品時，網站URL不會變更，但此處可建立檢視，僅代表顯示的第二列產品。 檢視名稱可能是&quot;products-page-2&quot;。

![](assets/example-load-more.png)

客戶決定從網站購買幾種產品，然後繼續到結帳畫面。 在結帳站點上，客戶可以選擇正常交貨或快速交貨。 「檢視」可以是網站上任何視覺元素群組，因此可針對傳送偏好設定建立「檢視」，並稱為「傳送偏好設定」。

![](assets/example-check-out.png)

「檢視」的概念可進一步延伸。 這些只是網站上可定義的幾個檢視範例。

## 實施XDM視圖

XDM檢視可在Adobe Target中運用，讓行銷人員透過Visual Experience Composer在SPA上執行A/B和XT測試。 這需要執行下列步驟，才能完成一次性開發人員設定：

1. 安裝[Adobe Experience Platform Web SDK](../../fundamentals/installing-the-sdk.md)
2. 確定您單頁應用程式中要個性化的所有XDM視圖。
3. 在定義XDM視圖後，為了傳遞AB或XT VEC活動，在單頁應用程式中實施`sendEvent()`函式，其中`renderDecisions`設定為`true`並且相應的XDM視圖。 必須在`xdm.web.webPageDetails.viewName`中傳遞XDM視圖。 此步驟可讓行銷人員運用Visual Experience Composer來啟動這些XDM的A/B和XT測試。

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
>在第一個`sendEvent()`呼叫中，將會擷取並快取所有應轉譯給使用者的XDM檢視。 隨後傳入XDM視圖的`sendEvent()`調用將從快取中讀取，並在不進行伺服器調用的情況下呈現。

## `sendEvent()` 函式示例

本節概述三個範例，說明如何在React中呼叫`sendEvent()`函式，以建立虛擬的電子商務SPA。

### 範例1:A/B測試首頁

行銷團隊想要在整個首頁上執行A/B測試。

![](assets/use-case-1.png)

要在整個主站點上運行A/B測試，`sendEvent()`必須在XDM `viewName`設定為`home`時調用：

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

行銷團隊希望在使用者按一下「載入更多」後，將價格標籤顏色變更為紅色，以個人化第二列產品。****

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

行銷團隊想要執行A/B測試，以檢視在選取「快速傳送」時，將按鈕的顏色從藍色變更為紅色，是否可大幅提升轉換率（而不是針對兩個傳送選項保留按鈕的藍色）。****

![](assets/use-case-3.png)

若要根據所選的傳送偏好設定個人化網站上的內容，可針對每個傳送偏好設定建立檢視。 選擇&#x200B;**Normal Delivery**&#x200B;時，該視圖可命名為「checkout-normal」。 如果選擇了「快遞」(Express Delivery)**，則「視圖」(View)可命名為「checkout-express」。**

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

## 使用Visual Experience Composer進行SPA

當您定義完XDM視圖並使用傳遞的XDM視圖實施`sendEvent()`後，VEC將能夠檢測這些視圖，並允許用戶為A/B或XT活動建立操作和修改。

>[!NOTE]
>
>若要將VEC用於您的SPA，您必須安裝並啟動[Firefox](https://addons.mozilla.org/en-US/firefox/addon/adobe-target-vec-helper/)或[Chrome](https://chrome.google.com/webstore/detail/adobe-target-vec-helper/ggjpideecfnbipkacplkhhaflkdjagak) VEC Helper Extension。

### 「修改」面板

「修改」面板會擷取為特定檢視所建立的動作。 視圖的所有操作都在該視圖下分組。

![](assets/modifications-panel.png)

### 動作

按一下動作會醒目顯示將套用該動作之網站上的元素。在「視圖」(View)下建立的每個VEC操作都具有以下表徵圖：**資訊**、**編輯**、**克隆**、**移動**&#x200B;和&#x200B;**刪除**。 下表將詳細說明這些圖示。

![](assets/action-icons.png)

| 圖示 | 說明 |
|---|---|
| 資訊 | 顯示此動作的詳細資料。 |
| 編輯 | 可讓您直接編輯該動作的屬性。 |
| 原地複製 | 將動作原地複製至一或多個存在於修改面板上的檢視，或原地複製至一或多個您已在 VEC 中瀏覽及導覽的目標檢視。動作未必會存在於修改面板中。<br/><br/>**注意：** 執行克隆操作後，您必須透過瀏覽導覽至VEC中的檢視，以查看克隆的動作是否為有效的操作。如果無法將動作套用到檢視，則會出現錯誤. |
| 移動 | 可將動作移動至頁面載入事件，或修改面板中已存在的任何其他檢視。<br/><br/>**頁面載入事件：** 與頁面載入事件相對應的任何動作都會套用至網頁應用程式的初始頁面載入。<br/><br/>**注意：**&#x200B;執行移動操作後，必須通過瀏覽導航到VEC中的「視圖」(View)，以查看移動是否為有效操作。如果無法將動作套用到檢視，則會出現錯誤. |
| 刪除 | 刪除動作。 |

## 使用VEC for SPA範例

本節概述使用Visual Experience Composer為A/B或XT活動建立動作和修改的三個範例。

### 範例1:更新「首頁」檢視

在本文稍早的部分，已為整個首頁定義了名為&quot;home&quot;的視圖。 現在，行銷團隊想要以下列方式更新「首頁」檢視：

* 將&#x200B;**新增至購物車**&#x200B;和&#x200B;**贊**&#x200B;按鈕變更為較淺的藍色分享。 在頁面載入期間，這應該會發生，因為它涉及變更頁首的元件。
* 將&#x200B;**2019**&#x200B;的最新產品標籤變更為&#x200B;**2019**&#x200B;最熱的產品，並將文字顏色變更為紫色。

要在VEC中進行這些更新，請選擇&#x200B;**合成**&#x200B;並將這些更改應用到「首頁」視圖。

![](assets/vec-home.png)

### 範例2:變更產品標籤

對於「products-page-2」檢視，行銷團隊會將&#x200B;**Price**&#x200B;標籤變更為&#x200B;**Sale Price**，並將標籤顏色變更為紅色。

若要在VEC中進行這些更新，必須執行下列步驟：

1. 在VEC中選擇&#x200B;**瀏覽**。
2. 在站點的頂部導航中選擇&#x200B;**產品**。
3. 選擇&#x200B;**Load More**&#x200B;一次，以檢視第二列產品。
4. 在VEC中選擇&#x200B;**合成**。
5. 套用動作，將文字標籤變更為&#x200B;**Sale Price**，並將顏色變更為紅色。

![](assets/vec-products-page-2.png)

### 範例3:個人化傳送偏好設定樣式

檢視可在精細層級定義，例如狀態或選項按鈕中的選項。 在本文稍早的章節中，已針對傳送偏好設定、「checkout-normal」和「checkout-express」來定義檢視。 行銷團隊想要將「checkout-express」檢視的按鈕顏色變更為紅色。

若要在VEC中進行這些更新，必須執行下列步驟：

1. 在VEC中選擇&#x200B;**瀏覽**。
2. 將產品新增至網站上的購物車。
3. 選取網站右上角的購物車圖示。
4. 選擇&#x200B;**結帳您的訂單**。
5. 在&#x200B;**傳送偏好設定**&#x200B;下方，選取「快速傳送&#x200B;**」選項按鈕。**
6. 在VEC中選擇&#x200B;**合成**。
7. 將&#x200B;**Pay**&#x200B;按鈕顏色變更為紅色。

>[!NOTE]
>
>在選擇&#x200B;**Express Delivery**&#x200B;單選按鈕之前，「checkout-express」視圖不會出現在「修改」面板中。 這是因為在選擇了&#x200B;**快速傳送**&#x200B;選項按鈕時會執行`sendEvent()`函式，因此VEC在選擇單選按鈕之前不會察覺到「checkout-express」視圖。

![](assets/vec-delivery-preference.png)
