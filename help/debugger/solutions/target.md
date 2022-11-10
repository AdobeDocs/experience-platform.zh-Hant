---
title: 使用Adobe Target Debugger測試Adobe Experience Platform實作
description: 了解如何使用Adobe Experience Platform Debugger測試和除錯已啟用Adobe Target的網站。
source-git-commit: 1ce7ac78936040d76faa3a58b92333a737fbeb66
workflow-type: tm+mt
source-wordcount: '1220'
ht-degree: 5%

---

# 使用Adobe Experience Platform Debugger測試Adobe Target實作

Adobe Experience Platform Debugger提供一套實用工具，可用來測試和除錯已與Adobe Target實作搭配使用的網站。 本指南涵蓋在啟用Target的網站上使用Platform Debugger的一些常見工作流程和最佳實務。

## 先決條件

若要使用Platform Debugger for Target，網站必須使用 [at.js資料庫](https://developer.adobe.com/target/implement/client-side/atjs/how-atjs-works/) 1.x版或更新版本。 不支援舊版。

## 初始化Platform Debugger

在瀏覽器中開啟您要測試的網站，然後開啟Platform Debugger擴充功能。

選擇 **[!DNL Target]** 的下一頁。 如果Platform Debugger偵測到網站上執行的at.js相容版本，則會顯示Adobe Target實作詳細資料。

![在Platform Debugger中選取的Target檢視，表示Adobe Target在目前檢視的瀏覽器頁面上處於作用中狀態](../images/solutions/target/target-initialized.png)

## 全局配置資訊

實作的全域設定的相關資訊會顯示在Platform Debugger的Target檢視頂端。

![Platform Debugger中醒目提示的Target全域設定資訊](../images/solutions/target/global-config.png)

| 名稱 | 說明 |
| --- | --- |
| 用戶端代碼 | 識別貴組織的唯一ID。 |
| 版本 | 網站上目前安裝的Adobe Target程式庫版本。 |
| 全域請求名稱 | 的名稱 [全域mbox](https://developer.adobe.com/target/implement/client-side/atjs/global-mbox/global-mbox-overview/?) 對於Target實作，預設名稱為 `target-global-mbox`. |
| 頁面載入事件 | 指示 [頁面載入事件](https://developer.adobe.com/target/implement/client-side/atjs/how-atjs-works/how-atjs-works/#atjs-2x-diagrams) 已發生。 at.js 2.x僅支援頁面載入事件。對於不相容的版本，此值預設為 `None`. |

{style=&quot;table-layout:auto&quot;}

## [!DNL Network Requests] {#network}

選擇 **[!DNL Network Requests]** 查看頁面上提出的每個網路請求的摘要資訊。

![此 [!DNL Network Requests] 在Platform Debugger中針對所選目標選取的區段](../images/solutions/target/network-requests.png)

當您在頁面上執行動作時（包括重新載入頁面），新的欄會自動新增至表格，讓您檢視動作順序，以及每個請求之間值的變更方式。

![此 [!DNL Network Requests] 在Platform Debugger中針對所選目標選取的區段](../images/solutions/target/new-request.png)

會擷取下列值：

| 名稱 | 說明 |
| --- | --- |
| [!DNL Page Title] | 起始此請求的頁面標題。 |
| [!DNL Page URL] | 起始請求的頁面URL。 |
| [!DNL URL] | 要求的原始URL。 |
| [!DNL Method] | 要求的HTTP方法。 |
| [!DNL Query String] | 請求的查詢字串，取自URL。 |
| [!DNL POST Body] | 請求的內文(僅針對POST請求而設定)。 |
| [!DNL Pathname] | 請求URL的路徑名。 |
| [!DNL Hostname] | 要求URL的主機名稱。 |
| [!DNL Domain] | 要求URL的網域。 |
| [!DNL Timestamp] | 請求（或事件）發生時間的時間戳記，位於瀏覽器的時區內。 |
| [!DNL Time Since Page Load] | 自頁面初次載入以來的請求時間。 |
| [!DNL Initiator] | 請求的發起者。 換句話說，誰提出了要求？ |
| [!DNL clientCode] | Target所識別之組織帳戶的識別碼。 |
| [!DNL requestType] | 用於請求的API。 如果使用at.js 1.x，值為 `/json`. 如果使用at.js 2.x，值為 `delivery`. |
| [!DNL Audience Manager Blob] | 提供加密Audience Manager中繼資料的資訊，稱為「blob」。 |
| [!DNL Audience Location Hint] | 資料收集地區 ID。此為特定 ID 服務資料中心之地理位置的數值識別碼。如需詳細資訊，請參閱Audience Manager檔案，位於 [DCS地區ID、位置與主機名稱。](https://experienceleague.adobe.com/docs/audience-manager/user-guide/api-and-sdk-code/dcs/dcs-api-reference/dcs-regions.html?lang=zh-Hant) 和Experience CloudIdentity服務指南 [`getLocationHint`](https://experienceleague.adobe.com/docs/id-service/using/id-service-api/methods/getlocationhint.html?lang=en#reference-a761030ff06c4439946bb56febf42d4c). |
| [!DNL Browser Height] | 瀏覽器高度（像素）。 |
| [!DNL Browser Time Offset] | 與其時區相關聯的瀏覽器時差。 |
| [!DNL Browser Width] | 瀏覽器寬度（像素）。 |
| [!DNL Color Depth] | 螢幕的色彩深度。 |
| [!DNL context] | 此物件包含提出要求之瀏覽器的相關內容資訊，包括螢幕維度和用戶端平台。 |
| [!DNL prefetch] | 在 `prefetch` 處理。 |
| [!DNL execute] | 期間使用的參數 `execute` 處理。 |
| [!DNL Experience Cloud Visitor ID] | 如果檢測到，則提供 [Experience CloudID(ECID)](https://experienceleague.adobe.com/docs/id-service/using/intro/overview.html) 指派給目前網站訪客的訪客。 |
| [!DNL experienceCloud] | 保有此特定使用者工作階段的Experience CloudID:a4T [補充資料ID](https://experienceleague.adobe.com/docs/target/using/integrate/a4t/before-implement.html?#section_2C1F745A2B7D41FE9E30915539226E3A)和 [訪客ID(ECID)](https://experienceleague.adobe.com/docs/id-service/using/intro/overview.html). |
| [!DNL id] | 此 [目標ID](https://developers.adobetarget.com/api/delivery-api/#section/Identifying-Visitors/Target-ID) 對訪客。 |
| [!DNL Mbox Host] | 此 [主機](https://experienceleague.adobe.com/docs/target/using/administer/hosts.html) Target要求時，才會收到通知。 |
| [!DNL Mbox PC] | 封裝 [`mbox`](https://developer.adobe.com/target/implement/client-side/atjs/global-mbox/global-mbox-overview/) 工作階段ID和 [Adobe Target Edge](https://experienceleague.adobe.com/docs/target/using/introduction/how-target-works.html#concept_0AE2ED8E9DE64288A8B30FCBF1040934) 位置提示。 at.js會使用此值，以確保工作階段和邊緣位置保持黏著。 |
| [!DNL Mbox Referrer] | 特定 [`mbox`](https://developer.adobe.com/target/implement/client-side/atjs/global-mbox/global-mbox-overview/) 請求。 |
| [!DNL Mbox URL] | 的URL [`mbox`](https://developer.adobe.com/target/implement/client-side/atjs/global-mbox/global-mbox-overview/) 伺服器。 |
| [!DNL Mbox Version] | 版本 [`mbox`](https://developer.adobe.com/target/implement/client-side/atjs/global-mbox/global-mbox-overview/) 被使用。 |
| [!DNL mbox3rdPartyId] | 此 [`mbox3rdPartyId`](https://experienceleague.adobe.com/docs/target/using/audiences/visitor-profiles/3rd-party-id.html) 指派給目前的訪客。 |
| [!DNL mboxRid] | 此 [`mbox`](https://developer.adobe.com/target/implement/client-side/atjs/global-mbox/global-mbox-overview/) 要求ID。 |
| [!DNL requestId] | 請求的唯一ID。 |
| [!DNL Screen Height] | 螢幕的高度（像素）。 |
| [!DNL Screen Width] | 螢幕的寬度（像素）。 |
| [!DNL Supplemental Data ID] | 系統產生的ID，用來比對訪客與對應的Adobe Target和Adobe Analytics呼叫。 請參閱 [A4T疑難排解指南](https://experienceleague.adobe.com/docs/target/using/integrate/a4t/troubleshoot-a4t/a4t-troubleshooting.html?#section_75002584FA63456D8D9086172925DD8D) 以取得更多資訊。 |
| [!DNL vst] | 此 [Experience CloudIdentity服務API設定](https://experienceleague.adobe.com/docs/id-service/using/id-service-api/configurations/function-vars.html). |
| [!DNL webGLRenderer] | 提供頁面上使用之WebGL轉譯器的相關資訊（若適用）。 |

{style=&quot;table-layout:auto&quot;}

要查看特定網路事件參數的詳細資訊，請選擇相關的表單元格。 此時會出現彈出視窗，提供參數的詳細資訊，包括說明及其值。 如果值是JSON物件，對話方塊會包含物件結構的完全導覽檢視。

![此 [!DNL Network Requests] 在Platform Debugger中針對所選目標選取的區段](../images/solutions/target/request-param-details.png)

## [!DNL Configuration]

選擇 **[!DNL Configuration]** 啟用或停用選取其他Target偵錯工具。

![此 [!DNL Configuration Requests] 在Platform Debugger中針對所選目標選取的區段](../images/solutions/target/configuration.png)

| 偵錯工具 | 說明 |
| --- | --- |
| [!DNL Target Console Logging] | 啟用後，可讓您存取瀏覽器控制台索引標籤中的at.js記錄檔。 您也可以新增 `mboxDebug` 查詢參數（含任何值）至瀏覽器URL。 |
| [!DNL Target Diable] | 啟用後，頁面上會停用所有Target功能。 這可用來判斷特定於Target的選件是否是造成頁面上問題的原因。 |
| [!DNL Target Trace] | **附註**:您必須登入才能啟用此功能。<br><br>啟用後，追蹤Token會隨每個請求一併傳送，並在每個回應中傳回追蹤物件。 `at.js` 解析回應 `window.__targetTraces`. 每個跟蹤對象包含與[[!DNL Network Requests] 標籤]，並新增下列內容：<ul><li>設定檔快照，可讓您查看請求前後的屬性。</li><li>匹配和不匹配 [活動](https://experienceleague.adobe.com/docs/target/using/activities/target-activities-guide.html)，顯示目前設定檔為何未符合特定活動的資格。<ul><li>這可協助識別設定檔在指定時間點符合哪些對象資格，以及為何需要。</li><li>Target檔案包含有關不同活動類型的詳細資訊</li></ul></li></ul> |

{style=&quot;table-layout:auto&quot;}
