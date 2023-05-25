---
title: 摘要標籤
description: 瞭解如何使用Adobe Experience Platform Debugger中的「摘要」標籤。
keywords: Debugger；Experience Platform Debugger 擴充功能；Chrome；擴充功能；摘要；清除；要求；摘要畫面；解決方案；資訊；Analytics；Target；DTM；Audience Manager；Launch；ID 服務
seo-description: Experience Platform Debugger Summary Screen
seo-title: Summary Tab
uuid: 46b17eaa-b611-43cf-8c6a-67b2e9b9d940
exl-id: 91234125-15c4-4111-9ee4-f3af093a3c4d
source-git-commit: f94bba7eb4763230dae6794eb70a75f53a853c53
workflow-type: tm+mt
source-wordcount: '909'
ht-degree: 74%

---

# 摘要標籤

若要執行Adobe Experience Platform Debugger，請在瀏覽器中開啟您要檢查的頁面，然後選取圖示(![](images/start-icon.jpg))。 擴充功能會在 **摘要** 標籤。

![](images/summary.jpg)

此畫面會顯示各種 Adobe Experience Cloud 解決方案的相關資訊。顯示的資訊會依解決方案而異，但通常包括解決方案程式庫和版本 (例如「AppMeasurement 2.9 版」) 和帳戶 ID (例如 Analytics 報表套裝 ID、Target 用戶端代碼、Audience Manager 合作夥伴 ID 等) 的相關資訊。

## Experience Platform Debugger 中顯示的資訊

Experience Platform Debugger 針對各個解決方案顯示的資訊如下：

**Adobe Analytics**

<table id="table_BEB9CC58E59D4D86BC895A8A51D84A2C"> 
 <tbody> 
  <tr> 
   <td colname="col1"> <p>報表套裝 </p> </td> 
   <td colname="col2"> <p><a href="https://experiencecloud.adobe.com/resources/help/zh_TW/reference/report_suites_admin.html" format="html" scope="external">報表套裝</a>可全面而獨立地定義針對選定網站、一組網站或網頁子集的報告。 </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <p>版本 </p> </td> 
   <td colname="col2"> <p>針對頁面定義的 <a href="https://experienceleague.adobe.com/docs/analytics/implementation/js/overview.html?lang=zh-Hant" format="html" scope="external">AppMeasurement</a> 版本 </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <p>訪客版本 </p> </td> 
   <td colname="col2"> <p><a href="https://experienceleague.adobe.com/docs/analytics/import/data-sources/data-types-and-categories/datasrc-visitorid.html" format="html" scope="external">訪客 ID</a> 程式庫的版本。 </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <p>頁面名稱 </p> </td> 
   <td colname="col2"> <p>傳送至 Analytics 的 <a href="https://experiencecloud.adobe.com/resources/help/zh_TW/sc/implement/pageName.html" format="html" scope="external">pageName</a> 變數，包含網站的好記名稱。 </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <p>模組 </p> </td> 
   <td colname="col2"> <p>Adobe Analytics 載入的模組 </p> </td> 
  </tr> 
 </tbody> 
</table>

**Audience Manager**

<table id="table_784AEABADBDA4D14BB9A7A9CB9EF07C3"> 
 <tbody> 
  <tr> 
   <td colname="col1"> <p>合作夥伴 </p> </td> 
   <td colname="col2"> <p>DIL 例項的<a href="https://experiencecloud.adobe.com/resources/help/zh_TW/aam/r_dil_get_partner.html" format="html" scope="external">合作夥伴名稱</a> </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <p>版本 </p> </td> 
   <td colname="col2"> <p>DIL 例項的<a href="https://experiencecloud.adobe.com/resources/help/zh_TW/aam/r_api_return_versions_dil.html" format="html" scope="external">版本號碼</a> </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <p>UUID </p> </td> 
   <td colname="col2"> <p>與 DIL 例項相關聯的<a href="https://experiencecloud.adobe.com/resources/help/zh_TW/aam/ids-in-aam.html" format="html" scope="external">不重複的使用者 ID</a> </p> </td> 
  </tr> 
 </tbody> 
</table>

**Adobe Experience Platform標籤**

<table id="table_E9574975444A407887E26514D1BB1601"> 
 <tbody> 
  <tr> 
   <td colname="col1"> <p>名稱 </p> </td> 
   <td colname="col2"> <p>標籤的名稱 <a href="https://experienceleague.adobe.com/docs/experience-platform/tags/admin/companies-and-properties.html" format="https" scope="external"> 屬性</a> </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <p>版本 </p> </td> 
   <td colname="col2"> <p>Turbine 版本</a> </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <p>建置日期 </p> </td> 
   <td colname="col2"> <p>標籤 <a href="https://experienceleague.adobe.com/docs/experience-platform/tags/publish/libraries.html" format="https" scope="external"> 資料庫</a> 建置日期 </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <p>環境 </p> </td> 
   <td colname="col2"> <p>此 <a href="https://experienceleague.adobe.com/docs/experience-platform/tags/publish/environments/environments.html" format="https" scope="external"> 環境</a> 由標籤庫使用 </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <p>擴充功能 </p> </td> 
   <td colname="col2"> <p>頁面所使用的擴充功能 </p> </td> 
  </tr> 
 </tbody> 
</table>

**Adobe Experience Platform Web SDK**

<table id="table_DC76D63FA6EF4891906B9E1D3E4A8A6C"> 
 <tbody> 
  <tr> 
   <td colname="col1"> <p>程式庫版本 </p> </td> 
   <td colname="col2"> <p>Adobe Experience Platform Web SDK <a href="https://experienceleague.adobe.com/docs/experience-platform/edge/extension/web-sdk-ext-release-notes.html" format="html" scope="external">程式庫版本</a>號碼 </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <p>命名空間</p> </td> 
   <td colname="col2"> <p>擴充功能的識別名稱</p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <p>屬性 ID </p> </td> 
   <td colname="col2"> <p>擴充功能中指定的標籤屬性名稱 </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <p>邊緣網域 </p> </td> 
   <td colname="col2"> <p>Adobe Experience Platform 擴充功能傳送及接收資料的網域 </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <p>IMS 組織 ID </p> </td> 
   <td colname="col2"> <p>您要在 Adobe 傳送資料的組織 (如同擴充功能中所指定) </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <p>啟用記錄功能 </p> </td> 
   <td colname="col2"> <p>指定是否已為此屬性啟用記錄功能</p> </td> 
  </tr> 
 </tbody> 
</table>

**Adobe Experience Cloud ID 服務**

<table id="table_274CFCEFA8F34D16BB546B4669EC0209"> 
 <tbody> 
  <tr> 
   <td colname="col1"> <p>Experience Cloud 組織 ID </p> </td> 
   <td colname="col2"> <p>您的<a href="https://experiencecloud.adobe.com/resources/help/zh_TW/mcvid/" format="https" scope="external">組織 ID</a> </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <p>版本 </p> </td> 
   <td colname="col2"> <p><a href="https://experienceleague.adobe.com/docs/analytics/import/data-sources/data-types-and-categories/datasrc-visitorid.html" format="html" scope="external">訪客 ID</a> 程式庫版本 </p> </td> 
  </tr> 
 </tbody> 
</table>

**Adobe Target**

<table id="table_D30E0CD20FB04E41862B22655136E043"> 
 <tbody> 
  <tr> 
   <td colname="col1"> <p>用戶端代碼 </p> </td> 
   <td colname="col2"> <p>您的 Target <a href="https://experienceleague.adobe.com/docs/target/using/implement-target/client-side/at-js-implementation/deploy-at-js/implementing-target-without-a-tag-manager.html" format="html" scope="external">用戶端代碼</a> </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <p>版本 </p> </td> 
   <td colname="col2"> <p>您目前的 <a href="https://experienceleague.adobe.com/docs/target/using/implement-target/client-side/at-js-implementation/target-atjs-versions.html" format="html" scope="external">at.js</a> 或 mbox.js 版本 </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <p>全域請求名稱 </p> </td> 
   <td colname="col2"> <p><a href="https://experienceleague.adobe.com/docs/target/using/implement-target/client-side/global-mbox/understanding-global-mbox.html" format="html" scope="external">全域 mbox</a> 是指 Target 實作中各網頁頂端所發出的單一伺服器呼叫 </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <p>頁面載入事件 </p> </td> 
   <td colname="col2"> <p>頁面載入時觸發的<a href="https://experienceleague.adobe.com/docs/experience-platform/tags/extensions/adobe/target/overview.html" format="html" scope="external">事件</a>類型 </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <p>請求名稱 </p> </td> 
   <td colname="col2"> <p>頁面上某個<a href="https://experienceleague.adobe.com/docs/target/using/implement-target/client-side/global-mbox/understanding-global-mbox.html" format="html" scope="external">位置</a>周圍的請求名稱。只有當您在程式碼或 Tag Manager 中實作 Debugging 事件監聽器，並在 Target UI 中開啟必要的<a href="https://experienceleague.adobe.com/docs/target/using/administer/response-tokens.html" format="html" scope="external">回應 Token</a> 時，才能無須驗證即可取得。 </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <p>活動名稱 </p> </td> 
   <td colname="col2"> <p>Target <a href="https://experienceleague.adobe.com/docs/target/using/activities/activities.html" format="html" scope="external">促銷活動或活動</a>的名稱。只有當您在程式碼或 Tag Manager 中實作 Debugging 事件監聽器，並在 Target UI 中開啟必要的<a href="https://experienceleague.adobe.com/docs/target/using/administer/response-tokens.html" format="html" scope="external">回應 Token</a> 時，才能無須驗證即可取得。 </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <p>活動 ID </p> </td> 
   <td colname="col2"> <p>Target 活動 ID。只有當您在程式碼或 Tag Manager 中實作 Debugging 事件監聽器，並在 Target UI 中開啟必要的<a href="https://experienceleague.adobe.com/docs/target/using/administer/response-tokens.html" format="html" scope="external">回應 Token</a> 時，才能無須驗證即可取得。 </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <p>體驗名稱 </p> </td> 
   <td colname="col2"> <p>Target <a href="https://experienceleague.adobe.com/docs/target/using/experiences/experiences.html" format="html" scope="external">體驗</a>的名稱。只有當您在程式碼或 Tag Manager 中實作 Debugging 事件監聽器，並在 Target UI 中開啟必要的<a href="https://experienceleague.adobe.com/docs/target/using/administer/response-tokens.html" format="html" scope="external">回應 Token</a> 時，才能無須驗證即可取得。 </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <p>體驗 ID </p> </td> 
   <td colname="col2"> <p>Target 體驗 ID。只有當您在程式碼或 Tag Manager 中實作 Debugging 事件監聽器，並在 Target UI 中開啟必要的<a href="https://experienceleague.adobe.com/docs/target/using/administer/response-tokens.html" format="html" scope="external">回應 Token</a> 時，才能無須驗證即可取得。 </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <p>優惠方案名稱</p> </td> 
   <td colname="col2"> <p>Target <a href="https://experienceleague.adobe.com/docs/target/using/experiences/offers/manage-content.html" format="html" scope="external">選件</a>的名稱。只有當您在程式碼或 Tag Manager 中實作 Debugging 事件監聽器，並在 Target UI 中開啟必要的<a href="https://experienceleague.adobe.com/docs/target/using/administer/response-tokens.html" format="html" scope="external">回應 Token</a> 時，才能無須驗證即可取得。 </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <p>選件 ID </p> </td> 
   <td colname="col2"> <p>Target 選件 ID。只有當您在程式碼或 Tag Manager 中實作 Debugging 事件監聽器，並在 Target UI 中開啟必要的<a href="https://experienceleague.adobe.com/docs/target/using/administer/response-tokens.html" format="html" scope="external">回應 Token</a> 時，才能無須驗證即可取得。 </p> </td> 
  </tr> 
 </tbody> 
</table>
