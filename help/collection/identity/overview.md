---
title: 資料收集中的身分
description: 瞭解資料收集如何在Web實作中使用ECID、核心ID、第一方持續性和identityMap。
exl-id: 03060cdb-becc-430a-b527-60c055c2a906
source-git-commit: 696e5098ebf556bfc0fa4fc22ff637cb0835eee0
workflow-type: tm+mt
source-wordcount: '654'
ht-degree: 0%

---

# 資料收集中的身分

Adobe資料收集會使用身分訊號來識別回頭的訪客，並在各個體驗中攜帶內容。 訪客造訪您的網站時，Edge Network會產生一個Experience Cloud ID (ECID)，並將其儲存在第一方Cookie中。 該ECID是跨Adobe Experience Cloud應用程式使用的主要裝置識別碼，也是分析、個人化和對象啟動的基礎。 在您的實作中，您可以透過[`getIdentity`](/help/collection/js/commands/getidentity.md)命令在使用者端存取訪客的ECID。 在資料流層級，您可以使用[資料收集的資料準備](/help/datastreams/data-prep.md)，在它到達下游服務之前，將ECID對應到自訂XDM欄位。

ECID可識別裝置，而非人員。 若要將活動連結至已知人員，您可以使用XDM [`identityMap`](./identity-map.md)在ECID旁邊傳送其他識別碼，例如CRM ID或雜湊電子郵件。 Adobe建議只要有個人層級的名稱空間可用，就將其設為[主要身分](/help/tags/extensions/client/web-sdk/data-element-types.md#identity-map)。

在預設ECID之外，資料收集會根據您的實作支援其他身分識別訊號：

* **第一方裝置識別碼(FPID)**：在您控制的基礎架構上產生和管理裝置識別碼。 Edge Network使用FPID來[種植ECID](./fpid.md)，以便在瀏覽器限制縮短Adobe管理的Cookie有效期限時，在擁有的屬性上提供更強大的Cookie持續性。
* **核心ID**：當有第三方Cookie可用時，參與協力廠商身分識別工作流程的獨立Demdex型識別碼。 CORE ID與ECID不同，可透過[`getIdentity`](/help/collection/js/commands/getidentity.md)擷取。 如需第一方和第三方識別內容如何搭配運作的詳細資訊，請參閱[整合識別支援](./unified-identity-support.md)。

如果您要從訪客API升級，或要協調舊的身分識別行為，請參閱[`idMigrationEnabled`](/help/collection/js/commands/configure/idmigrationenabled.md)以移轉現有的AMCV Cookie。

## 第一方和第三方集合 {#first-party-and-third-party-collection}

Web SDK一律會在您的網域上將身分識別[Cookie](https://experienceleague.adobe.com/en/docs/core-services/interface/data-collection/cookies/web-sdk) （例如`kndctr_` Cookie）設定為第一方Cookie，無論哪個端點會收到資料收集請求。 收集端點（您的實作傳送資料的網域）是另一個選擇，會影響瀏覽器和網路原則處理請求本身的方式。

**第一方集合**&#x200B;會使用指向Edge Network的CNAME，透過您組織控制的網域（例如`data.example.com`）路由資料集合請求。 由於要求會保留在您的網域上，因此不太可能會遭到廣告封鎖程式或瀏覽器網路限制的封鎖。 第一方集合也是從您自己的伺服器基礎結構設定[第一方裝置識別碼](./fpid.md)的先決條件，這是最耐用的可用身分識別策略。 Adobe建議使用[Adobe管理的憑證程式](https://experienceleague.adobe.com/en/docs/core-services/interface/data-collection/adobe-managed-cert)來設定您實作的第一方集合。

**協力廠商集合**&#x200B;會直接傳送要求給Adobe擁有的[`edgeDomain`](/help/collection/js/commands/configure/edgedomain.md) （例如`example.data.adobedc.net`）。 雖然身分Cookie仍會設定為您的網域的第一方，但請求本身會傳送至第三方網域，而有些瀏覽器和廣告封鎖程式可以加以限制。

## 選擇正確的身分模式 {#choose-your-path}

* **在擁有的屬性上加強身分持續性**：當瀏覽器限制縮短Cookie壽命，而您需要在您控制的網站上更強地分析和個人化時，使用[第一方裝置識別碼](./fpid.md)。
* **從應用程式將身分傳送給行動網站**：當訪客開始使用您的行動應用程式，並繼續使用WebView或行動網頁時，請使用[行動對網頁身分共用](./mobile-to-web.md)。
* **跨網域保持身分連續**：當訪客在您組織擁有的Web屬性之間移動，而您想要一致的報表和個人化時，請使用[跨網域共用](./cross-domain-sharing.md)。
* **結合第一方持續性與協力廠商啟用**：當您需要持久的第一方識別與支援的協力廠商啟用流程時，請使用[統一識別支援](./unified-identity-support.md)。
* **傳送個人層級識別碼**：使用[`identityMap`](./identity-map.md)將CRM ID、雜湊電子郵件和其他個人層級識別碼與ECID一併傳送，以便下游服務可以將活動連結至已知人員。
* **瞭解同意如何影響身分**：閱讀[同意與身分](./consent.md)，瞭解當網頁SDK產生ECID、設定Cookie及傳送資料時，`defaultConsent`和`setConsent`如何控制。

如需協助診斷識別問題，例如訪客膨脹、ECID不一致或FPID問題，請參閱[識別疑難排解](./troubleshooting.md)。
