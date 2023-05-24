---
title: Adobe Analytics分機的發行說明
description: Adobe Analytics標籤擴展在Adobe Experience Platform的最新發行說明。
exl-id: 3c7b4ec0-4b81-4ef4-b15f-6ad102525840
source-git-commit: 88939d674c0002590939004e0235d3da8b072118
workflow-type: tm+mt
source-wordcount: '1333'
ht-degree: 84%

---

# Adobe Analytics擴展發行說明

以下是Adobe Analytics標籤擴展的發行說明清單。

>[!NOTE]
>
>分析標籤擴展(如果經常響應對 [AppMeasurement JavaScript庫](https://experienceleague.adobe.com/docs/analytics/implementation/js/overview.html?lang=zh-Hant)。 請參閱 [《 AppMeasurement發行說明》](https://experienceleague.adobe.com/docs/analytics/implementation/appmeasurement-updates.html?lang=zh-Hant) 詳細瞭解下面提到的具體版本。

## 2022 年 9 月 23 日

**Adobe Analytics 擴充功能 1.9.1 版**

**功能**:

* 已升級到AppMeasurement v2.23.0。
* 擴展現在可以收集高熵 [用戶代理客戶端提示](https://developer.mozilla.org/en-US/docs/Web/HTTP/Client_hints#user-agent_client_hints) 由最新版本的AppMeasurement支援。

## 2022 年 2 月 28 日

**Adobe Analytics 擴充功能 1.9.0 版**

**錯誤修正**:

* 已刪除AppMeasurement中的某些調試語句。

## 2021 年 11 月 29 日

**Adobe Analytics 擴充功能 1.8.8 版**

**錯誤修正**:

* 已將AppMeasurement升級到v2.22.3。

## 2021 年 9 月 16 日

**Adobe Analytics 擴充功能 1.8.7 版**

**錯誤修正**:

* 已將AppMeasurement升級到v2.22.2。
* 已刪除不建議使用的buildInfo.environment

## 2021 年 8 月 24 日

**Adobe Analytics 擴充功能 1.8.6 版**

**錯誤修正**:

* 已升級 [AppMeasurement到v2.22.1](https://experienceleague.adobe.com/docs/analytics/implementation/appmeasurement-updates.html?lang=zh-Hant)。
* 已更新回退linkName以鏡像Activity Map邏輯，而不是使用innerHTML。

## 2020 年 8 月 6 日

**Adobe Analytics 擴充功能 1.8.5 版**

**錯誤修正**:

* 此欄位留空時，AAM 模組設定中設定的 Cookie 名稱不正確。此錯誤已修正。

**功能**:

* [AppMeasurement 已更新為 2.22.0 版](https://experienceleague.adobe.com/docs/analytics/implementation/appmeasurement-updates.html?lang=zh-Hant)。
* UI 些微變動，現在其他設定會以選單收合的形式顯示，而非核取方塊。

## 2020 年 6 月 2 日

**Adobe Analytics 擴充功能 1.8.4 版**

**錯誤修正**:

* 修正購物車事件 (prodView、scAdd、scView 等) 未顯示在事件下拉式清單中的問題。現在，您可以從下拉式清單中選取這些事件。

**功能**:

* 現在您可以關閉擴充功能中的 Activity Map，不需使用自訂代碼。Activity Map 會以個別模組的形式 (類似於 AAM 模組) 載入，而且您可以視需求將其關閉。
* 盡可能減少階層變數和其他選項，簡化 UI。
* 新增欄位，以便從擴充功能設定 UI 設定購買 ID。

## 2020 年 3 月 10 日

**Adobe Analytics 擴充功能 1.8.3 版**

**錯誤修正**:

* 修正使用自訂資料庫時，若未在 Analytics 中設定報表套裝，則嘗試設定變數時，系統會擲回規則設定錯誤的問題。
* 建立 eVar 時，系統無法顯示「從」prop 複製的選項，反之亦然。現在此問題已獲得修正，以反映舊版中的行為。

**功能**:

* [將 AppMeasurement 更新至 2.20.0 版](https://experienceleague.adobe.com/docs/analytics/implementation/appmeasurement-updates.html?lang=zh-Hant)

## 2020 年 3 月 2 日

**Adobe Analytics 擴充功能 1.8.2 版**

**錯誤修正**:

* 修正數值事件和序列化貨幣使用錯誤語法的問題

**功能**:

* [將 AppMeasurement 更新至 2.18.0 版](https://experienceleague.adobe.com/docs/analytics/implementation/appmeasurement-updates.html?lang=zh-Hant)
* 將 Audience Manager 模組中的 DIL 資料庫更新至 9.4 版
* 增加擴充功能中輸入欄位的長度
* 擴充功能和動作設定中的 eVar 和 prop 現在會顯示 Analytics 的好記名稱
* 在擴充功能設定的「Cookie」區段中新增核取方塊，可讓您編寫安全 Cookie
* 新增三種設定至 Audience Manager 模組。新增啟用記錄、URL 目的地及 Cookie 目的地的設定

## 2019 年 11 月 13 日

**Adobe Analytics 擴充功能 1.8.1 版**

**錯誤修正**:

* 已修正進階 evar 和 prop 無法儲存的錯誤。

## 2019 年 11 月 1 日

**Adobe Analytics 擴充功能 1.8.0 版**

**錯誤修正**:

* 修正少數客戶在下拉式清單中看不到報告套裝選項的錯誤
* 修正使用 ECID 時，部分變數未正確設定的錯誤

**功能**:

* 在擴充功能檢視中，依數值排序 eVar、prop 和事件
* 變更後端結構，以支援 Magento 內容資料

## 2019 年 9 月 6 日

**Adobe Analytics 擴充功能 1.7.8 版**

**錯誤修正**:

* 修正部分使用者在下拉式清單中找不到報表套裝選項的錯誤
* 修正動作無法正確引發的問題

## 2019 年 9 月 5 日

**Adobe Analytics 擴充功能 1.7.7 版**

**功能**:

* 將 AppMeasurement 更新至 2.17 版
* 更新 Audience Manager 模組以支援 DIL 9.3
* 更新欄位寬度以提供更多空間

**錯誤修正**:

* 修正選擇加入/退出的設定錯誤
* 修正使用 ECID 時變數未正確設定的錯誤

## 2019 年 7 月 18 日

**Adobe Analytics 擴充功能 1.7.6 版**

**功能**:

* 更新 Adobe Analytics 擴充功能，以支援 Audience Manager 的 DIL 9.2

* 更新擴充功能以支援 [AppMeasurement 2.15.0](https://experienceleague.adobe.com/docs/analytics/implementation/appmeasurement-updates.html#version-2.15.0)
* 已刪除以下複選框，因為它不再受支援：&quot;不要將目標發佈IFRAME附加到DOM或火災目標&quot;

## 2019 年 6 月 4 日

**Adobe Analytics 擴充功能 1.7.5 版**

**功能**:

* 將 Adobe Analytics 擴充功能更新為 [AppMeasurement 2.14.0](https://experienceleague.adobe.com/docs/analytics/implementation/appmeasurement-updates.html?lang=en#version-2.14.0)，其中包括已知的 clearVars 問題的修正。
* 新增 Exchange 連結至擴充功能。選取下拉式選單並選擇「擴充功能資訊」，即可取得 Exchange 清單

**錯誤修正**:

* 修正 UI 中顯示不正確的 eVar 從清單裡遭刪除的錯誤
* 修正當嘗試新增多個報表套裝時，需要 SSL 追蹤伺服器的錯誤。新增多個報表套裝時需有追蹤伺服器，但 SSL 追蹤伺服器欄位為選用。

## 2019 年 4 月 15 日

**Adobe Analytics 擴充功能 1.7.4 版**

**錯誤修正**:

* 在發現 appMeasurement 2.13.0 中的錯誤後，已復原擴充功能。appMeasurement 2.13.0 會造成無法傳送 ECID，因此，如果您已安裝 1.7.3，建議升級至 1.7.4 以避免此問題。請注意，clearVars 會繼續使用，直到 appMeasurement 的更新版本發行為止

## 2019 年 4 月 12 日

**Adobe Analytics 擴充功能 1.7.3 版**

**錯誤修正**:

* 將 Adobe Analytics 擴充功能更新為 appMeasurement 2.13.0，其中包括已知的 clearVars 問題的修正。

## 2019 年 3 月 21 日

**Adobe Analytics 擴充功能 1.7.2 版**

**功能**:

* 將 Adobe Analytics 擴充功能更新為 DIL 9.1。
* 將 Adobe Analytics 擴充功能更新為 appMeasurement 2.12。
* 將 Adobe Analytics 擴充功能檢視升級為 React-Spectrum。
* 在設定頁面中設定報表套裝時，您現在會看到包含公司中所有報表套裝的下拉式清單，讓您更方便選取適當的報表套裝。

## 2019 年 3 月 7 日

**Adobe Analytics 擴充功能 1.7.1 版**

**錯誤修正**:

* 在 1.7 版中發現錯誤後，將擴充功能復原至 1.6 版。

## 2019 年 2 月 11 日

**Adobe Analytics 擴充功能 1.6 版**

**功能**:

* 將 Adobe Analytics 擴充功能更新至 DIL 9.0，以支援選擇加入機制。
* 將 Adobe Analytics 擴充功能更新至 AppMeasurement 2.11，以支援選擇加入。

**錯誤修正**:

* 修正與 Prototype JS 的衝突。Analytics 擴充功能現在支援標準 prototype.js 程式庫。

## 2018 年 11 月 9 日

**Adobe Analytics 擴充功能 1.5.1 版**

**錯誤修正**:

* 將 DIL 模組降級為 7.0 版，以修正造成分析信標無法引發的問題

## 2018 年 11 月 5 日

**Adobe Analytics 擴充功能 1.5 版**

**功能**:

* 更新 Adobe Analytics 擴充功能，以支援 Audience Manager 的 DIL 8.0
* 將「從值序列化」欄位分隔為兩個欄位：「事件 ID」和「事件值」。這會修正指派值而非序列化事件的問題
   * 請注意：如果您使用字串 (例如，Event7=3:abc123) 以便使用目前欄位來新增 ID，則需要更新輸入，以反映「事件 ID」欄位中的 ID

**錯誤修正**：

* 修正無法正確填入貨幣代碼的錯誤

## 2018 年 10 月 11 日

**Adobe Analytics 擴充功能 1.4 版**

**功能**:

* 將追蹤 Cookie 名稱移轉至擴充功能設定。

**錯誤修正**:

* 修正問題，以便在沒有 trackerProperties 物件可用時，設定變數不會當機。

## 2018 年 6 月 5 日

**Adobe Analytics 擴充功能 1.3 版**

**功能**:

* 更新 Adobe Analytics 擴充功能以支援 AppMeasurement 2.9。
* 在 Adobe Analytics 擴充功能中新增「讓追蹤器可於全域存取」功能，這樣可讓追蹤器在 `windows.s` 下設為全域範圍。

**錯誤修正**:

* 修正從詳細檢視返回時，造成清單檢視重設的錯誤
* 修正一些錯誤，以改善修訂選擇器中的資源載入效能
* 修正多個規則會覆寫 Adobe Analytics 擴充功能中 s.events 的錯誤

## 2018 年 3 月 20 日

**Adobe Analytics 擴充功能 1.2 版**

**功能**:

* 將 AppMeasurement.js 更新至 2.8.0
* 新增伺服器端轉送支援

## 2018 年 2 月 8 日

**Adobe Analytics 擴充功能 1.1 版**

**功能**:

* AppMeasurement 已更新至 2.6 版
* 初始化的分析跟蹤器現在通過Adobe Experience Platform標籤擴展中的共用模組公開，因此其他擴展可以包括與其交互的代碼。

**錯誤修正**:

* 修正 Adobe Analytics 擴充功能中造成「錯誤。AppMeasurement 初始化期間缺少報表套裝 ID」出現在瀏覽器主控台中的錯誤。
