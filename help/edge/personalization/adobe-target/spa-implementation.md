---
title: Adobe Experience PlatformWeb SDK單頁應用程式實現
description: 瞭解如何使用Adobe Target建立Adobe Experience PlatformWeb SDK的單頁SPA應用程式()實現。
keywords: 目標；adobe目標；xdm視圖視圖；單頁應用程SPA序；生SPA命週期；客戶端；AB測試；AB；體驗瞄準；XT;VEC
exl-id: cc48c375-36b9-433e-b45f-60e6c6ea4883
source-git-commit: 0085306a2f5172eb19590cc12bc9645278bd2b42
workflow-type: tm+mt
source-wordcount: '1665'
ht-degree: 13%

---

# 單頁應用程式實現

Adobe Experience PlatformWeb SDK提供豐富的功能，使您的企業能夠在下一代客戶端技術（如單頁應用程式）上執行個性化SPA。

傳統的網站採用「頁面至頁面」導覽模型 (又稱為「多頁應用程式」)，網站設計與 URL 緊密結合，而從某網頁轉換到另一個網頁，需要頁面載入。

現代的Web應用程式，如單頁應用程式，已經採用了一種模型，該模型可以推動瀏覽器UI渲染的快速使用，而UI渲染通常與頁面重載無關。 這些體驗可通過客戶交互（如捲軸、點擊和游標移動）來觸發。 隨著現代網路的范式不斷演化，傳統通用事件（如頁面負載）與部署個性化和實驗的相關性不再有效。

![](assets/spa-vs-traditional-lifecycle.png)

## 平台Web SDK的優SPA點

將Adobe Experience PlatformWeb SDK用於單頁應用程式的好處如下：

* 可在頁面載入時快取所有選件，以減少對單一伺服器呼叫發出的多個伺服器呼叫。
* 極大地改善了您站點上的用戶體驗，因為服務可通過快取立即顯示，而不會因傳統伺服器調用而延遲。
* 單行代碼和一次性開發人員設定使營銷人員能夠通過您的Visual Experience Composer(VEC)建立和運行A/B和體驗目標(XT)活SPA動。

## XDM視圖和單頁應用程式

Adobe TargetVECSPA利用了一個叫做「視圖：一組邏輯的視覺元素，這些元素共同組成了一SPA種體驗。 因此，基於用戶交互，單頁應用程式可被視為通過視圖而不是URL進行轉換。 檢視通常可代表整個網站或網站內的分組視覺元素。

為進一步解釋視圖，以下示例使用React中實現的假設線上電子商務站點來瀏覽示例視圖。

瀏覽到主網站後，英雄形象會宣傳復活節銷售活動以及網站上提供的最新產品。 在這種情況下，可以為整個主螢幕定義視圖。 這種觀點可以簡單地稱為&quot;家&quot;。

![](assets/example-views.png)

隨著客戶對業務所銷售的產品更感興趣，他們決定按一下 **產品** 的子菜單。 與首頁相似，產品網站整體可定義為一個檢視。此視圖可命名為「產品全部」。

![](assets/example-products-all.png)

由於視圖可以定義為整個站點或站點上的一組可視元素，因此產品站點上顯示的四個產品可以分組並視為視圖。 此視圖可命名為「產品」。

![](assets/example-products.png)

當客戶決定按一下 **載入更多** 按鈕以瀏覽網站上的更多產品，此時網站URL不會更改，但可以在此處建立一個視圖，以僅表示顯示的第二行產品。 視圖名稱可以是「products-page-2」。

![](assets/example-load-more.png)

客戶決定從現場購買幾種產品，然後繼續到結帳螢幕。 在結帳地點，客戶可以選擇正常交貨或快遞。 視圖可以是站點上的任意一組可視元素，因此可以為交貨首選項建立視圖並稱為「交貨首選項」。

![](assets/example-check-out.png)

「視圖」的概念可以進一步擴展。 這些只是幾個可在站點上定義的視圖示例。

## 實施XDM視圖

XDM Views可在Adobe Target使用，使營銷人員能夠通過Visual Experience Composer運行A/B和XTSPAtest。 這要求執行以下步驟以完成一次性開發程式設定：

1. 安裝 [Adobe Experience PlatformWeb SDK](../../fundamentals/installing-the-sdk.md)
2. 確定要個性化的單頁應用程式中的所有XDM視圖。
3. 定義XDM視圖後，為了傳遞AB或XT VEC活動，請實施 `sendEvent()` 函式 `renderDecisions` 設定為 `true` 和「單頁應用程式」中相應的XDM視圖。 必須傳入XDM視圖 `xdm.web.webPageDetails.viewName`。 此步驟使營銷人員能夠利用Visual Experience Composer為這些XDM啟動A/B和XTtest。

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
>第一個 `sendEvent()` 調用時，應呈現給最終用戶的所有XDM視圖都將被提取並快取。 後續 `sendEvent()` 傳入了XDM視圖的調用將從快取中讀取，並在不進行伺服器調用的情況下呈現。

## `sendEvent()` 函式示例

本節概述了三個示例，說明如何調用 `sendEvent()` 函式對假設的電子商SPA務。

### 示例1:A/Btest首頁

營銷團隊希望在整個首頁上運行A/Btest。

![](assets/use-case-1.png)

要在全家網站運行A/Btest, `sendEvent()` 必須與XDM一起調用 `viewName` 設定為 `home`:

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

### 示例2:個性化產品

市場營銷團隊希望通過在用戶按一下後將價格標籤顏色更改為紅色來個性化第二行產品 **載入更多**。

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

### 示例3:A/Btest傳遞首選項

市場營銷團隊希望運行A/Btest，以查看在以下情況下是否將按鈕的顏色從藍色更改為紅色 **快遞** 選中後，可以提高轉換（與使兩個交貨選項的按鈕顏色保持為藍色相反）。

![](assets/use-case-3.png)

要根據所選的交貨首選項對站點上的內容進行個性化設定，可為每個交貨首選項建立一個視圖。 當 **正常交付** 選中後，視圖可命名為「簽出 — 正常」。 如果 **快遞** 選中後，視圖可命名為「checkout-express」。

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

## 使用Visual Experience ComposerSPA

定義完XDM視圖並實施後 `sendEvent()` 通過傳遞這些XDM視圖，VEC將能夠檢測這些視圖，並允許用戶為A/B或XT活動建立操作和修改。

>[!NOTE]
>
>要將VEC用於SPA，必須安裝並激活 [火狐](https://addons.mozilla.org/en-US/firefox/addon/adobe-target-vec-helper/) 或 [鉻](https://chrome.google.com/webstore/detail/adobe-target-vec-helper/ggjpideecfnbipkacplkhhaflkdjagak) VEC幫助程式擴展。

### 「修改」面板

「修改」(Modifications)面板捕獲為特定視圖建立的操作。 視圖的所有操作都在該視圖下分組。

![](assets/modifications-panel.png)

### 動作

按一下動作會醒目顯示將套用該動作之網站上的元素。在「視圖」(View)下建立的每個VEC操作都具有以下表徵圖： **資訊**。 **編輯**。 **克隆**。 **移動**, **刪除**。 下表中對這些表徵圖作了更詳細的說明。

![](assets/action-icons.png)

| 圖示 | 說明 |
|---|---|
| 資訊 | 顯示此動作的詳細資料。 |
| 編輯 | 可讓您直接編輯該動作的屬性。 |
| 原地複製 | 將動作原地複製至一或多個存在於修改面板上的檢視，或原地複製至一或多個您已在 VEC 中瀏覽及導覽的目標檢視。動作未必會存在於修改面板中。<br/><br/>**注：** 執行克隆操作後，必須通過瀏覽導航到VEC中的視圖，以查看克隆操作是否是有效操作。 如果無法將動作套用到檢視，則會出現錯誤. |
| 移動 | 可將動作移動至頁面載入事件，或修改面板中已存在的任何其他檢視。<br/><br/>**頁面載入事件：** 與頁面載入事件相對應的任何操作都將應用於Web應用程式的初始頁面載入。 <br/><br/>**注：** 執行移動操作後，必須通過瀏覽導航到VEC中的「視圖」(View)，以查看移動是否是有效操作。 如果無法將動作套用到檢視，則會出現錯誤. |
| 刪除 | 刪除動作。 |

## 使用VEC作為示SPA例

本節概述了使用Visual Experience Composer為A/B或XT活動建立操作和修改的三個示例。

### 示例1:更新「首頁」視圖

在本文檔的早期，為整個主站點定義了一個名為「home」的視圖。 現在，市場營銷團隊希望通過以下方式更新「首頁」視圖：

* 更改 **添加到購物車** 和 **像** 按鈕以淺藍色的比例顯示。 在載入頁面時應發生這種情況，因為它涉及更改頁眉的元件。
* 更改 **2019年最新產品** 標籤 **2019年最熱的產品** 將文本顏色改為紫色。

要在VEC中進行這些更新，請選擇 **合成** 並將這些更改應用到「首頁」視圖。

![](assets/vec-home.png)

### 示例2:更改產品標籤

對於「products-page-2」視圖，營銷團隊希望更改 **價格** 標籤 **銷售價格** 將標籤顏色改為紅色。

要在VEC中進行這些更新，需要執行以下步驟：

1. 選擇 **瀏覽** 的子菜單。
2. 選擇 **產品** 的上界。
3. 選擇 **載入更多** 查看第二行產品。
4. 選擇 **合成** 的子菜單。
5. 應用操作將文本標籤更改為 **銷售價格** 顏色變成紅色。

![](assets/vec-products-page-2.png)

### 示例3:個性化交付首選項樣式

視圖可以在細粒度級別定義，如狀態或單選按鈕中的選項。 在本文檔早期，已為交付首選項、「checkout-normal」和「checkout-express」定義視圖。 市場營銷團隊希望將「結帳快速」視圖的按鈕顏色更改為紅色。

要在VEC中進行這些更新，需要執行以下步驟：

1. 選擇 **瀏覽** 的子菜單。
2. 將產品添加到站點上的購物車。
3. 選擇站點右上角的購物車表徵圖。
4. 選擇 **簽出訂單**。
5. 選擇 **快遞** 單選按鈕 **交貨首選項**。
6. 選擇 **合成** 的子菜單。
7. 更改 **支付** 按鈕。

>[!NOTE]
>
>在「修改」面板中出現「簽出 — 快速」視圖，直到 **快遞** 按鈕。 這是因為 `sendEvent()` 函式 **快遞** 單選按鈕，因此在選中單選按鈕之前，VEC不知道「checkout-express」視圖。

![](assets/vec-delivery-preference.png)
