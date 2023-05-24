---
title: TestAdobe Target實施與Adobe Experience Platform調試器
description: 瞭解如何使用Adobe Experience Platform調試器test和調試啟用了Adobe Target的網站。
exl-id: f99548ff-c6f2-4e99-920b-eb981679de2d
source-git-commit: c3b5b63767a934be16a479d04853e1250b3bf775
workflow-type: tm+mt
source-wordcount: '1211'
ht-degree: 4%

---

# TestAdobe Target與Adobe Experience Platform調試器的實現

Adobe Experience Platform調試器提供了一套有用的工具，用於測試和調試已與Adobe Target實現一起使用的網站。 本指南介紹在啟用目標的網站上使用平台調試器的一些常見工作流和最佳做法。

## 先決條件

要將平台調試器用於目標，網站必須使用 [at.js庫](https://developer.adobe.com/target/implement/client-side/atjs/how-atjs-works/) 1.x或更高版本。 不支援以前的版本。

## 正在初始化平台調試器

在瀏覽器中開啟要test的網站，然後開啟平台調試器擴展。

選擇 **[!DNL Target]** 的子菜單。 如果平台調試器檢測到站點上正在運行相容版本的at.js，將顯示Adobe Target實現詳細資訊。

![在平台調試器中選擇的目標視圖，表示當前查看的瀏覽器頁面上Adobe Target處於活動狀態](../images/solutions/target/target-initialized.png)

## 全局配置資訊

有關實施的全局配置的資訊顯示在平台調試器中的「目標」視圖頂部。

![平台調試器中突出顯示的目標的全局配置資訊](../images/solutions/target/global-config.png)

| 名稱 | 說明 |
| --- | --- |
| 用戶端代碼 | 標識組織的唯一ID。 |
| 版本 | 網站上當前安裝的Adobe Target庫版本。 |
| 全域請求名稱 | 名稱 [全局框](https://developer.adobe.com/target/implement/client-side/atjs/global-mbox/global-mbox-overview/?) 對於目標實現，預設名稱 `target-global-mbox`。 |
| 頁面載入事件 | 指示是否 [頁載入事件](https://developer.adobe.com/target/implement/client-side/atjs/how-atjs-works/how-atjs-works/#atjs-2x-diagrams) 已經發生了。 僅at.js 2.x支援頁面載入事件。對於不相容的版本，此值預設為 `None`。 |

{style="table-layout:auto"}

## [!DNL Network Requests] {#network}

選擇 **[!DNL Network Requests]** 查看該頁面上提出的每個網路請求的摘要資訊。

![的 [!DNL Network Requests] 在平台調試器中選擇的目標部分](../images/solutions/target/network-requests.png)

在頁面上執行操作（包括重新載入頁面）時，新列會自動添加到表中，允許您查看操作順序以及每個請求之間值的更改方式。

![的 [!DNL Network Requests] 在平台調試器中選擇的目標部分](../images/solutions/target/new-request.png)

將捕獲以下值：

| 名稱 | 說明 |
| --- | --- |
| [!DNL Page Title] | 啟動此請求的頁面標題。 |
| [!DNL Page URL] | 啟動請求的頁面的URL。 |
| [!DNL URL] | 請求的原始URL。 |
| [!DNL Method] | 請求的HTTP方法。 |
| [!DNL Query String] | 從URL獲取的請求的查詢字串。 |
| [!DNL POST Body] | 請求的正文(僅為POST請求設定)。 |
| [!DNL Pathname] | 請求URL的路徑名。 |
| [!DNL Hostname] | 請求URL的主機名。 |
| [!DNL Domain] | 請求URL的域。 |
| [!DNL Timestamp] | 在瀏覽器的時區內請求（或事件）發生時間的時間戳。 |
| [!DNL Time Since Page Load] | 自在請求時初始載入頁面以來的已用時間。 |
| [!DNL Initiator] | 請求的發起方。 換句話說，誰提出了要求？ |
| [!DNL clientCode] | 目標識別的組織帳戶的標識符。 |
| [!DNL requestType] | 用於請求的API。 如果使用at.js 1.x，則值為 `/json`。 如果使用at.js 2.x，則值為 `delivery`。 |
| [!DNL Audience Manager Blob] | 提供有關稱為「blob」的加密Audience Manager元資料的資訊。 |
| [!DNL Audience Location Hint] | 資料收集地區 ID。此為特定 ID 服務資料中心之地理位置的數值識別碼。有關詳細資訊，請參閱Audience Manager文檔。 [DCS區域ID、位置和主機名](https://experienceleague.adobe.com/docs/audience-manager/user-guide/api-and-sdk-code/dcs/dcs-api-reference/dcs-regions.html?lang=zh-Hant) 和Experience Cloud身份服務指南 [`getLocationHint`](https://experienceleague.adobe.com/docs/id-service/using/id-service-api/methods/getlocationhint.html?lang=en#reference-a761030ff06c4439946bb56febf42d4c)。 |
| [!DNL Browser Height] | 瀏覽器高度（以像素為單位）。 |
| [!DNL Browser Time Offset] | 瀏覽器與其時區關聯的時間偏移。 |
| [!DNL Browser Width] | 瀏覽器寬度（以像素為單位）。 |
| [!DNL Color Depth] | 螢幕的顏色深度。 |
| [!DNL context] | 一個對象，包含有關用於發出請求的瀏覽器的上下文資訊，包括螢幕尺寸和客戶端平台。 |
| [!DNL prefetch] | 在中使用的參數 `prefetch` 處理。 |
| [!DNL execute] | 在 `execute` 處理。 |
| [!DNL Experience Cloud Visitor ID] | 如果檢測到，則提供 [Experience CloudID(ECID)](https://experienceleague.adobe.com/docs/id-service/using/intro/overview.html) 分配給當前站點訪問者。 |
| [!DNL experienceCloud] | 保存此特定用戶會話的Experience CloudID:A4T [補充資料ID](https://experienceleague.adobe.com/docs/target/using/integrate/a4t/before-implement.html?#section_2C1F745A2B7D41FE9E30915539226E3A)的 [訪問者ID(ECID)](https://experienceleague.adobe.com/docs/id-service/using/intro/overview.html)。 |
| [!DNL id] | 的 [目標ID](https://developers.adobetarget.com/api/delivery-api/#section/Identifying-Visitors/Target-ID) 給訪客。 |
| [!DNL Mbox Host] | 的 [主機](https://experienceleague.adobe.com/docs/target/using/administer/hosts.html) 目標請求的內容。 |
| [!DNL Mbox PC] | 封裝 [`mbox`](https://developer.adobe.com/target/implement/client-side/atjs/global-mbox/global-mbox-overview/) 會話ID和 [Adobe Target邊](https://experienceleague.adobe.com/docs/target/using/introduction/how-target-works.html#concept_0AE2ED8E9DE64288A8B30FCBF1040934) 位置提示。 at.js使用此值以確保會話和邊緣位置保持粘滯。 |
| [!DNL Mbox Referrer] | 特定的URL引用者 [`mbox`](https://developer.adobe.com/target/implement/client-side/atjs/global-mbox/global-mbox-overview/) 請求。 |
| [!DNL Mbox URL] | 的URL [`mbox`](https://developer.adobe.com/target/implement/client-side/atjs/global-mbox/global-mbox-overview/) 伺服器。 |
| [!DNL Mbox Version] | 版本 [`mbox`](https://developer.adobe.com/target/implement/client-side/atjs/global-mbox/global-mbox-overview/) 正被使用。 |
| [!DNL mbox3rdPartyId] | 的 [`mbox3rdPartyId`](https://experienceleague.adobe.com/docs/target/using/audiences/visitor-profiles/3rd-party-id.html) 分配給當前訪問者。 |
| [!DNL mboxRid] | 的 [`mbox`](https://developer.adobe.com/target/implement/client-side/atjs/global-mbox/global-mbox-overview/) 請求ID。 |
| [!DNL requestId] | 請求的唯一ID。 |
| [!DNL Screen Height] | 螢幕的高度（以像素為單位）。 |
| [!DNL Screen Width] | 螢幕寬度（以像素為單位）。 |
| [!DNL Supplemental Data ID] | 系統生成的ID，用於將訪問者與相應的Adobe Target和Adobe Analytics呼叫匹配。 查看 [A4T故障排除指南](https://experienceleague.adobe.com/docs/target/using/integrate/a4t/troubleshoot-a4t/a4t-troubleshooting.html?#section_75002584FA63456D8D9086172925DD8D) 的子菜單。 |
| [!DNL vst] | 的 [Experience CloudIdentity Service API配置](https://experienceleague.adobe.com/docs/id-service/using/id-service-api/configurations/function-vars.html)。 |
| [!DNL webGLRenderer] | 提供有關頁面上使用的WebGL呈現器的資訊（如果適用）。 |

{style="table-layout:auto"}

要查看特定網路事件上某個參數的詳細資訊，請選擇相關的表單元格。 出現跨距，提供有關參數的進一步資訊，包括說明及其值。 如果值是JSON對象，則對話框將包含對象結構的完全可導航視圖。

![的 [!DNL Network Requests] 在平台調試器中選擇的目標部分](../images/solutions/target/request-param-details.png)

## [!DNL Configuration]

選擇 **[!DNL Configuration]** 啟用或禁用「目標」的其他調試工具選項。

![的 [!DNL Configuration Requests] 在平台調試器中選擇的目標部分](../images/solutions/target/configuration.png)

| 調試工具 | 說明 |
| --- | --- |
| [!DNL Target Console Logging] | 啟用後，允許您訪問瀏覽器控制台頁籤中的at.js日誌。 還可以通過添加 `mboxDebug` 查詢參數（包含任何值）到瀏覽器URL。 |
| [!DNL Target Diable] | 啟用後，該頁上將禁用所有目標功能。 這可用於確定特定於目標的優惠是否是導致該頁上問題的原因。 |
| [!DNL Target Trace] | **注釋**:必須登錄才能啟用此功能。<br><br>啟用後，跟蹤令牌隨每個請求一起發送，並且跟蹤對象在每個響應中返回。 `at.js` 分析響應 `window.__targetTraces`。 每個跟蹤對象包含與[[!DNL Network Requests] )的正文。<ul><li>配置檔案快照，允許您查看請求前後的屬性。</li><li>匹配且不匹配 [活動](https://experienceleague.adobe.com/docs/target/using/activities/target-activities-guide.html)，顯示當前配置檔案為什麼沒有或沒有資格進行特定活動。<ul><li>這有助於確定某個配置檔案在給定時間適合哪些受眾，以及原因。</li><li>目標文檔包含有關不同活動類型的詳細資訊</li></ul></li></ul> |

{style="table-layout:auto"}
