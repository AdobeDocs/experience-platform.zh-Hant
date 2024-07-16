---
title: Adobe Experience Platform Web SDK常見問題集
description: 取得有關Adobe Experience Platform Web SDK常見問題的解答。
exl-id: 6ddb4b4d-c9b8-471a-bd2e-135dc4202876
source-git-commit: 002a57d1d5cfb2e7bdbd9b587e77ca4487a28f65
workflow-type: tm+mt
source-wordcount: '2268'
ht-degree: 2%

---


# 常見問答

本指南提供經常詢問關於Adobe Experience Platform Web SDK問題的回答。

## 什麼是Adobe Experience Platform Web SDK？

Adobe Experience Platform Web SDK是使用者端的JavaScript資料庫，可讓您與Adobe Experience Cloud中的各種服務互動。

Web SDK會以與解決方案無關的方式(XDM)傳送資料至Experience PlatformEdge Network，接著將資料對應至解決方案特定的格式和目的地，並即時傳送。

請參閱下列影片以取得有關Web SDK的詳細資訊： [Meet Alloy.js and Never Tag for aeVar或Mbox Rearly](https://www.adobe.com/summit/2020/with-alloy-js-never-tag-for-an-evar-or-mbox-again.html)。

## Adobe Experience Platform Web SDK和先前的解決方案有何不同？

### Experience PlatformWeb SDK之前

目前，您必須根據各個解決方案來部署不同的JavaScript程式庫。

* 每個解決方案都有自己的JavaScript資料庫、結構描述和網域。
* 這些程式庫都不是為了彼此搭配使用而建置的。
* 跨解決方案和Adobe Experience Platform使用案例需要這些不同的程式庫相互依存，導致部署上的摩擦。

雖然Platform中的標籤可讓您儘可能輕鬆部署及管理這些程式庫，但下列專案仍有問題：

* 程式庫大小(頁面上的Adobe程式碼過多)
* 效能（網站載入時間太長）
* 單一使用案例的多次呼叫
* 在個人化呼叫之前等候ECID傳回（導致延遲）
* 分離式資料收集（什麼是evar？）
* 解決方案(A4T)之間的結構描述混淆
* 許多其他不太理想的事物

此外，目前沒有直接將資料傳送至Adobe Experience Platform的JavaScript資料庫。

### 使用Experience Platform Web SDK

新的Web SDK會將下列解決方案的資料傳送至單一目的地(Experience PlatformEdge Network)，並解決上述最常見的解決方案使用案例。

* Adobe Analytics
* Adobe Audience Manager
* Adobe Target
* 訪客 ID
* Adobe Experience Platform

其他解決方案亦將陸續推出。

Adobe Experience Platform Web SDK也可以直接傳送資料給Adobe Experience Platform。 此資料為XDM格式，並對應至伺服器端解決方案架構。

## 這個新Web SDK有何價值？

**效能：** Web SDK比使用所有目前的Adobe程式庫還小，而且頁面載入速度更快。

**簡單性：** XDM、Web SDK、標籤、Edge Network、Adobe Experience Cloud解決方案和Adobe Experience Platform的組合可建立簡單易懂且易於遵循的資料收集故事。

* **XDM：**&#x200B;您用來傳送資料給Adobe的解決方案無關結構描述。 不再為evar或mbox加上標籤。
* **Web SDK：**&#x200B;可讓您輕鬆傳送及接收資料至Adobe Experience PlatformEdge Network。
* **標籤：**&#x200B;簡化網站上Web SDK (以及任何其他JavaScript標籤)的部署和設定。
* **Edge Network：**&#x200B;以資料所需的格式輕鬆將資料路由至Adobe Experience Platform和解決方案。
* **Adobe Experience Platform和Adobe解決方案：**&#x200B;啟用其價值主張。

**控制項：**&#x200B;因為所有資料都使用單一且連線的資料流，所以您可以邏輯地追蹤並控制資料在往返應用程式的每毫秒歷程中看起來的樣子。

**現代且準備好迎接未來：** Web SDK及其與Edge Network的連線已讓Adobe大幅更新Adobe處理資料收集、個人化、同意和未來第三方Cookie的方式。 (這會啟用第一方網域，並由Adobe管理。)

**實現價值時間：** Adobe已努力工作（並將繼續），以便透過標籤儘可能輕鬆地部署Web SDK並將使用者端資料對應到XDM。 完成上述工作後，您就可以開啟或關閉伺服器端的所有其他Adobe解決方案和Adobe Experience Platform服務。 例如，如果您將此用於Adobe Analytics並且想要開啟Target或Experience Platform，您只需在資料流設定上翻轉切換即可開啟這些使用案例。

## 什麼是 [!DNL alloy.js]？

[!DNL alloy.js]是Web SDK JavaScript程式庫的名稱。 在SDK原始程式碼和檔案名稱中會參照。

## 客戶是否需要購買Adobe Experience Platform才能使用[!DNL Web SDK]？

不可以。 任何Adobe Digital Experience客戶都可以免費使用Adobe Experience Platform Web SDK。 想要使用[!DNL Web SDK]的客戶將需要設定正確的許可權，才能在資料收集UI或Experience PlatformUI中建立結構描述、資料集、身分名稱空間和資料串流。

如需設定這些許可權的詳細資訊，請參閱我們關於[資料彙集許可權管理](https://experienceleague.adobe.com/docs/experience-platform/collection/permissions.html)的檔案。

## 哪些人應該使用Web SDK？

Adobe Experience Platform Web SDK是為下列客戶所開發：

* Adobe Experience Platform使用者
   * 如果您需要直接從裝置傳送資料至Adobe Experience Platform，建議您採取此正式方式。
   * Adobe瞭解，如果您已有Adobe Analytics，使用Adobe Analytics聯結器會更快捷，但並非資料收集的長期策略。

* Adobe Experience Cloud解決方案客戶
   * 新的Adobe Analytics、Adobe Audience Manager和Adobe Target客戶應從新的Web SDK開始，而不使用舊版程式庫。
   * 現有客戶若想儘可能獲得最佳化的實施，應使用新的Web SDK。

## 如何存取Web SDK？

Web SDK目前可供一般公眾使用，並可用來將資料傳送至Adobe Experience Cloud產品。 近期即將推出傳送資料給協力廠商解決方案的功能。

SDK免費，並由Adobe免費託管。 如有需要，您可以免費下載並在您自己的伺服器上託管。

Web SDK需要存取[資料流設定](../datastreams/overview.md)和Experience Platform[XDM結構描述產生器](../xdm/tutorials/create-schema-ui.md)，以便Adobe的伺服器能夠正確處理來自SDK的傳入資料。 如果您想要取得存取權，請聯絡您的Adobe客戶團隊，以開始請求流程。

## Web SDK目前支援哪些使用案例？

Web SDK正在迅速發展。 正在處理更多使用案例。 您可以在這裡找到目前支援的[使用案例清單。](https://github.com/orgs/adobe/projects/18/views/1?filterQuery=)

## 目前的客戶必須重新標籤其網站嗎？

視情況而定。 Adobe Experience Platform Web SDK可部署為兩種不同的樣式。 未來的移轉檔案將提供更多詳細資訊。

* **只有另一個標籤：**&#x200B;如果網站已針對解決方案加上標籤，而您不可以重新加上標籤，但您想要將資料傳送至Adobe Experience PlatformEdge Network以供Experience Platform使用案例或即將推出的事件轉送功能（請參閱下文），您可以將`alloy.js`標籤新增至網站，其作用就像是「其他標籤」。

* **唯一標籤：**&#x200B;如果您想要將Web SDK用於Experience Cloud解決方案，您必須將其用於該頁面上的&#x200B;_所有_&#x200B;解決方案。 例如，如果您的網站已針對Adobe Analytics進行標籤，而您想要將其用於Target，則您需要將其用於兩者，以及未來的任何其他網站。

換言之，如果您決定將Adobe Experience Platform Web SDK用於非解決方案使用案例，則可以使用`alloy.js`標籤網站並繼續進行，就像它是一個新的解決方案一樣。 如果您想要將其用於Adobe Analytics、Target、Audience Manager或應用程式使用案例，您可能需要移除頁面上的任何舊版程式碼。

## 我可以在開始使用Web SDK時移轉ECID，讓我的網站訪客不會開始顯示為新訪客嗎？

是，Adobe Experience Platform Web SDK提供身分移轉功能。 如需詳細資訊，請依照[Platform Web SDK身分識別檔案](/help/web-sdk/identity/overview.md#id-migration)中識別碼移轉的指示操作。

## Web SDK與標籤有何不同？

* Experience Platform **中的**&#x200B;標籤可管理裝置代碼。 使用這些變數可更輕鬆部署程式碼。 它們是自由且強大的。

* **Adobe Experience Platform Web SDK**&#x200B;是標籤將針對Adobe使用案例部署的新程式碼的正式名稱。 此外，它也是免費且功能強大。

* **`alloy.js`**&#x200B;是Adobe Experience Platform Web SDK程式碼的檔案名稱。

## 我是否必須使用標籤才能部署Web SDK？

不可以。 您可以自行下載`alloy.js`檔案。

但是：

* Adobe Experience Platform Web SDK需要資料流ID，邊緣網路才能識別資料流，並決定如何處理資料。 此ID會在Experience Platform中建立。 這並不表示您必須使用UI來建立屬性或部署JavaScript程式碼，但您確實需要使用標籤來建立設定ID。

* 標籤不僅是最佳的可用標籤和SDK管理員，可讓您輕鬆部署`alloy.js`並將資料對應至XDM結構描述。 如果您決定不使用標籤，則必須先管理部署`alloy.js`、事件並將資料對應至XDM，才能進行傳送。 _這個_&#x200B;程式比使用標籤要困難得多。

* 建議您使用標籤來部署`alloy.js`，即使這是您使用標籤的唯一專案。

## 什麼是事件轉送？

如果您使用我們的SDK並將XDM傳送至Edge Network，這些新功能事件轉送可讓您安裝新的伺服器端擴充功能，並將資料從我們的邊緣網路對應至任何專案，接著再傳送至任何地方。 將其視為「資料收集即服務」。 這將需要付費，並會隨Adobe Experience Platform提供。

## 什麼是CNAME或第一方網域，這為什麼重要？

有關CNAME的詳細資訊，請參閱[Adobe檔案](https://experienceleague.adobe.com/docs/id-service/using/reference/analytics-reference/cname.html)

## Adobe Experience Platform Web SDK是否使用Cookie？ 若是如此，會使用哪些Cookie？

是，根據您的實作，目前Web SDK會使用1到7個Cookie的任一處。 以下是您在Web SDK中可能會看到的Cookie清單，及其使用方式：

| **名稱** | **maxAge** | **友善的年齡** | **說明** |
|---|---|---|---|
| **kndct_orgid_identity** | 34128000 | 395 天 | 身分Cookie會儲存ECID以及與ECID相關的其他資訊。 |
| **kndctr_orgid_consent_check** | 7200 | 2 小時 | 此工作階段型Cookie會傳送訊號給伺服器，讓伺服器查詢同意偏好設定伺服器端。 |
| **kndctr_orgid_consent** | 15552000 | 180 天 | 此Cookie會儲存使用者對網站的同意偏好設定。 |
| **kndctr_orgid_cluster** | 1800 | 30 分鐘 | 此Cookie會儲存為目前使用者的請求提供服務的Edge Network區域。 URL路徑會使用地區，這樣Edge Network就能將請求路由至正確的地區。 此Cookie具有30分鐘的存留期，因此如果使用者以不同的IP位址連線，則請求可以路由傳送到最接近的區域。 |
| **mbox** | 63072000 | 2 年 | 當Target移轉設定設為true時，就會顯示此Cookie。 這可讓Web SDK設定Target [mbox Cookie](https://developer.adobe.com/target/implement/client-side/atjs/atjs-cookies/)。 |
| **mboxEdgeCluster** | 1800 | 30 分鐘 | 當Target移轉設定設為true時，就會顯示此Cookie。 此Cookie可讓Web SDK將正確的邊緣叢集通訊至at.js，以便當使用者在網站上導覽時，Target設定檔可以保持同步。 |
| **AMCV_###@AdobeOrg** | 34128000 | 395 天 | 只有在Adobe Experience Platform Web SDK上啟用ID移轉功能時，此Cookie才會出現。 在網站的某些部分仍在使用visitor.js時，此Cookie有助於轉換至Web SDK。 如需詳細資訊，請參閱[`idMigrationEnabled`](/help/web-sdk/commands/configure/idmigrationenabled.md)。 |

使用Web SDK時，Edge Network會設定上述一個或多個Cookie。 Edge Network會設定具有`secure`和`sameSite="none"`屬性的所有Cookie。

如果您的網站上目前同時有安全和非安全區段，這可能會干擾使用者識別。 當使用者從網站的安全區段導覽到不安全的區段時，Edge Network會使用請求產生新的`ECID`。

## Adobe Experience Platform Web SDK支援哪些瀏覽器？

Adobe Experience Platform Web SDK的設計可在最新版Google Chrome、Safari、Firefox、Internet Explorer 11和Microsoft Edge Chromium中以最佳方式運作。 在舊版的瀏覽器上使用某些功能時，可能會發生問題。

## 我可以在哪裡取得有關Adobe Experience Platform Web SDK的詳細資訊？

* [文件](/help/web-sdk/home.md)
* [Source代碼](https://github.com/adobe/alloy)

### 支援Internet Explorer {#support-internet-explore}

此SDK使用promise ，這是通訊非同步工作完成的方法。 SDK使用的[Promise](https://developer.mozilla.org/zh-TW/docs/Web/JavaScript/Reference/Global_Objects/Promise)實作原生受到除[!DNL Internet Explorer]外的所有目標瀏覽器的支援。 若要在[!DNL Internet Explorer]上使用SDK，您必須有`window.Promise` [polyfilled](https://remysharp.com/2010/10/08/what-is-a-polyfill)。

若要判斷您是否已經填滿`window.Promise`個：

1. 在[!DNL Internet Explorer]中開啟您的網站。
1. 開啟瀏覽器的偵錯主控台。
1. 在主控台中輸入`window.Promise`，然後按Enter。

如果出現`undefined`以外的專案，表示您可能已經填滿`window.Promise`。 判斷`window.Promise`是否為多填的另一個方法是在完成上述安裝指示後載入您的網站。 如果SDK擲回錯誤，提及Promise相關內容，表示您可能尚未多邊填滿`window.Promise`。

如果您已決定必須polyfill `window.Promise`，請在先前提供的基底程式碼上方加入下列指令碼標籤：

```html
<script src="https://cdn.jsdelivr.net/npm/promise-polyfill@8/dist/polyfill.min.js"></script>
```

此標籤會載入指令碼，以確保`window.Promise`為有效的Promise實作。

>[!NOTE]
>
>如果您選擇載入不同的Promise實作，請確定它支援`Promise.prototype.finally`。

### 支援Internet Explorer

Adobe Experience Platform SDK使用promise ，這是通訊非同步工作完成的方法。 SDK使用的[Promise](https://developer.mozilla.org/zh-TW/docs/Web/JavaScript/Reference/Global_Objects/Promise)實作原生受到除[!DNL Internet Explorer]外的所有目標瀏覽器的支援。 若要在[!DNL Internet Explorer]上使用SDK，您必須有`window.Promise` [polyfilled](https://remysharp.com/2010/10/08/what-is-a-polyfill)。

有一個可用來聚合填滿Promise的資料庫是Promise-Polyfill。 如需如何使用NPM安裝的詳細資訊，請參閱[promise-polyfill檔案](https://www.npmjs.com/package/promise-polyfill)。

>[!NOTE]
>
>如果您選擇載入不同的Promise實作，請確定它支援`Promise.prototype.finally`。
