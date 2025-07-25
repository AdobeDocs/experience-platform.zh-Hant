---
title: Cloud Connector擴充功能概述
description: 瞭解Adobe Experience Platform中的Cloud Connector事件轉送擴充功能。
exl-id: f3713652-ac32-4171-8dda-127c8c235849
source-git-commit: e832694fed5dbb86b5ed544473d6a79e500a6222
workflow-type: tm+mt
source-wordcount: '1716'
ht-degree: 68%

---

# Cloud Connector擴充功能概述

>[!NOTE]
>
>Adobe Experience Platform Launch 已進行品牌重塑，現在是 Adobe Experience Platform 中的一套資料彙集技術。 因此，這些產品文件都推出多項幾術語變更。如需術語變更的彙整參考資料，請參閱以下[文件](../../../term-updates.md)。

雲端聯結器事件轉送擴充功能可讓您建立自訂HTTP請求，以將資料傳送至目的地或從目的地擷取資料。 Cloud Connector 擴充功能就像 Adobe Experience Platform Edge Network 的郵差一樣，可將資料傳送至尚未具備專屬擴充功能的端點。

您可參閱此參考文件，了解使用此擴充功能建立規則時可使用哪些選項。

## Cloud Connector 擴充功能動作類型

本節說明 Adobe Experience Platform Cloud Connector 擴充功能中可供使用的「傳送資料」動作類型。

### 要求類型

若要選取端點所需的要求型別，請在[!UICONTROL 要求型別]下拉式清單中選取適當的型別。

| 方法 | 說明 |
|---|---|
| [GET](https://developer.mozilla.org/zh-TW/docs/Web/HTTP/Methods/GET) | 要求呈現指定的資源。使用 GET 的要求應當只會擷取資料。 |
| [POST](https://developer.mozilla.org/zh-TW/docs/Web/HTTP/Methods/POST) | 將實體提交至指定資源，通常會造成伺服器狀態改變或產生副作用。 |
| [PUT](https://developer.mozilla.org/en-US/docs/Web/HTTP/Methods/PUT) | 以要求裝載取代目標資源當下的所有呈現方式。 |
| [PATCH](https://developer.mozilla.org/en-US/docs/Web/HTTP/Methods/PATCH) | 對資源進行部分修改。 |
| [DELETE](https://developer.mozilla.org/en-US/docs/Web/HTTP/Methods/DELETE) | 刪除指定的資源。 |

### 端點 URL

在「要求類型」下拉式選單旁的文字欄位中，輸入您要傳送資料的端點 URL。

### 查詢參數、標頭和內文設定

您可使用「查詢參數」、「標頭」和「內文資料元素」等索引標籤，控制要傳送給指定端點的資料。

#### 查詢參數

為您要以查詢字串參數形式傳送的每個索引鍵/值組定義索引鍵和值。若要手動輸入資料元素，請使用大括弧資料元素代碼化進行事件轉送。 若要以索引鍵或值的形式參照資料元素「siteSection」的值，請輸入 `{{siteSection}}`。或者，您也可以從下拉式選單中選取先前建立的資料元素。

若要新增更多查詢引數，請選取&#x200B;**[!UICONTROL 新增其他]**。

#### 標頭

為您要以標頭傳送的每個索引鍵/值組定義索引鍵和值。若要手動輸入資料元素，請使用大括弧資料元素代碼化進行事件轉送。 若要以索引鍵或值的形式參照資料元素「pageName」的值，請輸入 `{{pageName}}`。或者，您也可以從下拉式選單中選取先前建立的資料元素。

若要新增其他標頭，請選取&#x200B;**[!UICONTROL 新增其他]**。

預先定義的標頭如下表所示。不僅限使用下列標頭，您也可以視需求新增專屬的自訂標頭，以便使用。

>[!NOTE]
>
>如需下列標頭的詳細資訊，請參閱 [https://developer.mozilla.org/zh-TW/docs/Web/HTTP/Headers](https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers)。

| 標頭 | 說明 |
|---|---|
| [A-IM](https://developer.mozilla.org/zh-TW/docs/Web/HTTP/Headers/Accept) | |
| [Accept](https://developer.mozilla.org/zh-TW/docs/Web/HTTP/Headers/Accept) | |
| [Accept-Charset](https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers/Accept-Charset) | |
| [Accept-Encoding](https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers/Accept-Encoding) | |
| [Accept-Language](https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers/Accept-Language) | |
| [Accept-Datetime](https://developer.mozilla.org/zh-TW/docs/Web/HTTP/Headers/Accept) | 由使用者代理程式傳送，表示想存取原始資源的過去狀態。為此，針對原始資源 TimeGate 所發送的 HTTP 要求中會傳送 `Accept-Datetime` 標頭，其值表示所需原始資源過去狀態的日期時間。 |
| Access-Control-Request-Headers | 瀏覽器在發出[預檢要求](https://developer.mozilla.org/en-US/docs/Glossary/preflight_request)時使用，讓伺服器知道用戶端提出實際要求時，可能會傳送哪些 [HTTP 標頭](https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers)。 |
| Access-Control-Request-Method | 瀏覽器在發出[預檢要求](https://developer.mozilla.org/en-US/docs/Glossary/preflight_request)時使用，讓伺服器知道用戶端提出實際要求時可能會使用哪種 [HTTP 方法](https://developer.mozilla.org/en-US/docs/Web/HTTP/Methods)。此標頭為必填項目，因為預檢要求一概都是 [OPTION](https://developer.mozilla.org/en-US/docs/Web/HTTP/Methods/OPTIONS)，且不使用與實際要求相同的方法。 |
| Authorization | 包含向伺服器驗證使用者代理程式的認證。 |
| [Cache-Control](https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers/Cache-Control) | 要求和回應中快取機制的指示詞。 |
| [Connection](https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers/Connection) | 控制當前的交易完成後，網路連線是否維持開啟狀態。 |
| [Content-Length](https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers/Content-Length) | 資源大小，以位元組十進位值表示。 |
| [Content-Type](https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers/Content-Type) | 表示資源的媒介類型。 |
| Cookie | 包含伺服器先前以 [`Set-Cookie`](https://developer.mozilla.org/zh-TW/docs/Web/HTTP/Headers/Set-Cookie) 標頭傳送及儲存的 [HTTP Cookie](https://developer.mozilla.org/zh-TW/docs/Web/HTTP/Cookies)。 |
| Date | 一般 HTTP 標頭會包含產生訊息的日期和時間。 |
| [DNT](https://developer.mozilla.org/zh-TW/docs/Web/HTTP/Headers/DNT) | 表示使用者的追蹤偏好設定。 |
| Expect | 表示伺服器必須滿足才能正確處理要求的期望。 |
| Forwarded | 包含來自[反向 Proxy 伺服器](https://developer.mozilla.org/en-US/docs/Web/HTTP/Proxy_servers_and_tunneling)的資訊，但在要求路徑涉及 Proxy 時，資訊遭到更改或遺失。 |
| From | 包含真人使用者的網際網路電子郵件地址，發出要求的使用者代理程式由該使用者控制。 |
| Host | 指定要求預計抵達的伺服器主機和連接埠號碼。 |
| If-Match | |
| If-Modified-Since | |
| [If-None-Match](https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers/If-None-Match) | |
| [If-Range](https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers/If-Range) | |
| [If-Unmodified-Since](https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers/If-Unmodified-Since) | |
| [Max-Forwards](https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers/If-Unmodified-Since) | |
| [Origin](https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers/Origin) | |
| [Pragma](https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers/Pragma) | 實作專用標頭，可能會在要求回應鏈的任何位置產生多種效果，功用是與未有 Cache-Control 標頭的 HTTP/1.0 快取回溯相容。 | |
| [Proxy-Authorization](https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers/Proxy-Authorization) |
| [Range](https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers/Range) | 表示伺服器應傳回的文件部分。 | |
| [Referer](https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers/Referer) | 上一個網頁的網址，使用者在此點選連結，前往當前所要求存取的頁面。 | |
| TE | 指定使用者代理程式願意接受的傳輸編碼(較直觀的名稱為 `Accept-Transfer-Encoding`)。 |
| Upgrade | 「[`Upgrade`」標頭欄位的相關 RFC 文件為 RFC 7230 第 6.7 節](https://tools.ietf.org/html/rfc7230#section-6.7)。該標準建立了在當前用戶端、伺服器、傳輸通訊協定連線上升級或改用其他通訊協定的規則。例如，只要伺服器決定認可並實作「`Upgrade`」標頭欄位，此標頭即可標準允許用戶端從 HTTP 1.1 變更為 HTTP 2.0。雙方均不需接受「`Upgrade`」標頭欄位中指定的條款。用戶端和伺服器標頭皆可適用。如果指定「`Upgrade`」標頭欄位，傳送者必須指定「`upgrade`」選項以傳送「`Connection`」標頭欄位。 | |
| [User-Agent](https://developer.mozilla.org/zh-TW/docs/Web/HTTP/Headers/User-Agent) | 包含特徵字串，供同級的網路通訊協定識別發出要求的軟體使用者代理程式，了解其應用程式類型、作業系統、軟體廠商或軟體版本等詳細資訊。 |
| [Via](https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers/Via) | 由正向和反向 Proxy 新增，可顯示於要求標頭和回應標頭中。 |
| [Warning](https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers/Warning) | 潛在問題的一般警告資訊。 |
| X-CSRF-Token | |
| X-Requested-With | |

#### Body as JSON

為您要在要求內文中傳送的每個索引鍵/值組定義索引鍵和值。若要手動輸入資料元素，請使用大括弧資料元素代碼化進行事件轉送。 若要以索引鍵或值的形式參照資料元素「appSection」的值，請輸入 `{{appSection}}`。或者，您也可以從下拉式選單中選取先前建立的資料元素。

若要新增其他索引鍵/值組，請選取&#x200B;**[!UICONTROL 新增其他]**。

#### Body as Raw

為您要在要求內文中傳送的每個索引鍵/值組定義索引鍵和值。若要手動輸入資料元素，請使用大括弧資料元素代碼化進行事件轉送。 若要以索引鍵或值的形式參照資料元素「appSection」的值，請輸入 `{{appSection}}`。或者，您也可以從下拉式選單中選取先前建立的資料元素。您可以新增一或多個資料元素。

### 進階

事件轉送中規則內的動作會依序執行。 某些情況下，您或許可以從外部來源擷取不在用戶端傳入事件上的資料，然後接受此回應，並在單一規則內的後續動作中轉換資料或將資料傳送至最終目的地。進階區段中的「儲存要求回應」會啟用此功能。

若要儲存端點的回應內文，請勾選&#x200B;**[!UICONTROL 儲存要求回應]**&#x200B;方塊，並在文字欄位中定義回應索引鍵。

如果您已將回應索引鍵定義為「`productDetails`」，請在資料元素中參照此資料，接著在同一規則的後續動作中參照此資料元素。若要建立參照「`productDetail`」的資料元素，請建立「`path`」類型的資料元素，並輸入以下路徑：

```Json
arc.ruleStash.[EXTENSION-NAME-HERE].responses.[RESPONSE-KEY-HERE] 

arc.ruleStash.adobe-cloud-connector.reponses.productDetails 
```

## 新增相互傳輸層安全性([!DNL mTLS])規則至您的事件轉送程式庫 {#mtls-rules}

[!DNL mTLS]憑證是數位認證，可證明安全通訊中的伺服器或使用者端身分。 當您使用[!DNL mTLS]服務API時，這些憑證可協助您驗證並加密Adobe Experience Platform事件轉送的互動。 此過程不僅可保護您的資料，還可確保每個連線都來自信任的合作夥伴。

### 安裝Adobe Cloud Connector擴充功能 {#install}

若要安裝擴充功能，[請建立事件轉送屬性](../../../ui/event-forwarding/overview.md#properties)，或選取要編輯的現有屬性。

在左側面板中選取&#x200B;**[!UICONTROL 擴充功能]**。 在&#x200B;**[!UICONTROL 目錄]**&#x200B;標籤中，選取&#x200B;**[!UICONTROL Adobe Cloud Connector]**&#x200B;卡片，然後選取&#x200B;**[!UICONTROL 安裝]**。

![顯示[!DNL Adobe Cloud Connector]擴充卡醒目提示安裝的擴充功能目錄。](../../../images/extensions/server/cloud-connector/install-extension.png)

### 設定事件轉送規則 {#rule}

>[!NOTE]
>
>若要設定使用[!DNL mTLS]的規則，您必須安裝Adobe Cloud Connector 1.2.4版或更新版本。

安裝擴充功能後，您可以建立使用[!DNL mTLS]的事件轉送規則，並將其新增至程式庫。

在您的事件轉送屬性中建立新的事件轉送[規則](../../../ui/managing-resources/rules.md)。 提供規則的名稱，然後在&#x200B;**[!UICONTROL 動作]**&#x200B;下新增動作，並將擴充功能設為&#x200B;**[!UICONTROL Adobe Cloud Connector]**。 接著，選取&#x200B;**[!UICONTROL 動作型別]**&#x200B;的&#x200B;**[!UICONTROL 擷取呼叫]**。

![「事件轉送屬性規則」檢視中，醒目顯示新增事件轉送規則動作設定所需的欄位。](../../../images/extensions/server/cloud-connector/event-action.png)

進行選取後，會出現其他控制項，以設定[!DNL mTLS]要求的方法和目的地。 若要在環境中啟用使用中憑證，請選取&#x200B;**[!UICONTROL 在[!DNL mTLS]]**&#x200B;中啟用，然後選取&#x200B;**[!UICONTROL 保留變更]**&#x200B;以儲存規則。

![事件轉送屬性規則檢視，包含其他控制欄位並醒目提示變更。](../../../images/extensions/server/cloud-connector/save-rule.png)

您的新規則現已準備就緒。 選取&#x200B;**[!UICONTROL 儲存至程式庫]**，然後選取&#x200B;**[!UICONTROL 組建]**&#x200B;以進行部署。 [!DNL mTLS]要求現在已啟用，並可在您的程式庫中使用。

![事件轉送規則，其中的save to library and build已反白顯示。](../../../images/extensions/server/cloud-connector/save-build.png)

## 後續步驟

本指南說明如何在事件轉送中設定mTLS規則。 如需為環境設定mTLS的詳細資訊，請參閱[相互傳輸層安全性([!DNL mTLS])指南](../cloud-connector/mtls.md)。

如需Experience Platform中事件轉送功能的詳細資訊，請參閱[事件轉送概觀](../../../ui/event-forwarding/overview.md)。
