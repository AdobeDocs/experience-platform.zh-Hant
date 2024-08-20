---
keywords: Experience Platform；首頁；熱門主題；身分；身分；XDM圖形；身分服務；身分服務
solution: Experience Platform
title: Identity Service總覽
description: Adobe Experience Platform Identity Service可跨裝置和系統橋接身分，讓您即時提供具影響力的個人數位體驗，協助您更清楚瞭解客戶及其行為。
exl-id: a22dc3f0-3b7d-4060-af3f-fe4963b45f18
source-git-commit: 2a2e3fcc4c118925795951a459a2ed93dfd7f7d7
workflow-type: tm+mt
source-wordcount: '1555'
ht-degree: 2%

---

# Adobe Experience Platform Identity Service

為了提供相關的數位體驗，您需要全面且準確地呈現組成客戶基礎的真實世界實體。

現今的組織與企業面臨大量不同的資料集：您的個別客戶會以各種不同的識別碼呈現。 您的客戶可以連結到不同的網頁瀏覽器(Safari、Google Chrome)、硬體裝置（電話、筆記型電腦）和其他人員識別碼（CRMID、電子郵件帳戶）。 這會建立客戶的分離檢視。

您可以使用Adobe Experience Platform Identity Service及其功能解決這些挑戰，以便：

* 產生將不同身分連結在一起的&#x200B;**身分圖表**，以視覺化呈現客戶如何跨不同管道與您的品牌互動。
* 建立即時客戶個人檔案的圖形，接著用於合併屬性和行為，以建立客戶的全面檢視。
* 使用各種工具執行驗證和偵錯。

本檔案概述Identity Service，以及您如何在Experience Platform內容中使用其功能。

## 術語 {#terminology}

在深入探討Identity Service的詳細資訊之前，請閱讀下表以取得關鍵術語的摘要：

| 詞語 | 定義 |
| --- | --- |
| 身分 | 身分是實體獨有的資料。 通常這是真實世界的物件，例如個人、硬體裝置或網頁瀏覽器（以Cookie表示）。 完整識別包含兩個元素： **識別名稱空間**&#x200B;和&#x200B;**識別值**。 |
| 身分命名空間 | 身分命名空間是特定身分的背景。例如，`Email`的名稱空間可能對應到身分值： **julien<span>@acme.com**。 同樣地，`Phone`的名稱空間可能對應到身分值： `555-555-1234`。 如需詳細資訊，請閱讀[身分名稱空間概觀](./features/namespaces.md)。 |
| 身分識別值 | 身分值是代表真實世界實體的字串，並會透過名稱空間在身分服務中分類。 例如，身分值（字串） **julien<span>@acme.com**&#x200B;可歸類為`Email`名稱空間。 |
| 身分類型 | 身分型別是身分名稱空間的元件。 身分型別會指定身分資料是否連結在身分圖表中。 |
| 連結 | 連結或連結是一種方法，可讓兩個不同的身分分別代表相同的實體。 例如，「`Email` = julien<span>@acme.com」和「`Phone` = 555-555-1234」之間的連結表示兩個身分都代表相同的實體。 這表示與您品牌互動的客戶，其電子郵件地址為julien<span>@acme.com，電話號碼為555-555-1234，兩者是相同的。 |
| 身分識別服務 | Identity Service是Experience Platform中的服務，可連結（或取消連結）身分以維護身分圖表。 |
| 識別圖 | 身分圖表是身分的集合，代表單一客戶。 如需詳細資訊，請參閱[上的使用身分圖表檢視器](./features/identity-graph-viewer.md)的指南。 |
| 即時客戶設定檔 | 即時客戶個人檔案是Adobe Experience Platform中的一項服務，其功能： <ul><li>合併設定檔片段，根據身分圖表建立設定檔。</li><li>將設定檔分段，以便傳送至目的地進行啟用。</li></ul> |
| 設定檔 | 設定檔是主旨、組織或個人的表示法。 設定檔由四個元素組成： <ul><li>屬性：屬性會提供名稱、年齡或性別等資訊。</li><li>行為：行為可提供有關指定設定檔活動的資訊。 例如，設定檔行為可以分辨特定設定檔是「搜尋涼鞋」還是「訂購T恤」。</li><li>身分：對於合併的個人檔案，這會提供與個人相關聯的所有身分資訊。 身分可以分為三種類別：人員（CRMID、電子郵件、電話）、裝置(IDFA、GAID)和Cookie (ECID、AAID)。</li><li>對象成員資格：設定檔所屬的群組（忠誠使用者、住在加利福尼亞的使用者等）</li></ul> |

{style="table-layout:auto"}

## 什麼是Identity Service？

在平台](./images/identity-service-stitching.png)上進行![身分拼接

在企業對客戶(B2C)情境中，客戶會與您的企業互動，並與您的品牌建立關係。 一般客戶可能會在您組織資料基礎架構內的任意數量的系統中活動。 任何特定客戶都可能在您的電子商務、忠誠度和服務檯系統中處於活躍狀態。 同一客戶也可在任何數量的不同裝置上匿名或透過驗證方法進行互動。

考量下列客戶歷程：

* Julien已在您的電子商務網站上建立帳戶，且過去曾訂購一些專案。 Julien通常會使用自己的筆記型電腦購物，並在每次使用時登入她的帳戶。
* 不過，在造訪您的網站期間，她使用平板電腦搜尋涼鞋。 在此工作階段中，由於她使用不同的裝置，因此她既不會登入也不會下訂單。
* 此時，Julien的活動會以兩個個別的設定檔表示：
   * 她的第一個設定檔是電子商務登入ID。 當她使用使用者名稱和密碼組合來驗證她在您的電子商務網站上的工作階段時，就會使用此設定檔。 此設定檔由跨裝置識別碼識別。
   * 她的第二個設定檔是她的平板電腦裝置。 此設定檔是在她使用平板電腦匿名瀏覽您的電子商務網站而未登入其帳戶後建立的。 此設定檔由Cookie識別碼識別。
* 稍後，Julien繼續她的平板電腦工作階段。 不過這次她已登入帳戶。 因此，Identity Service現在會將Julien的平板電腦裝置活動與她的電子商務登入ID建立關聯。
* 日後您的目標內容可能會反映Julien的完整設定檔、購買記錄及匿名瀏覽活動。

>[!IMPORTANT]
>
>您可以使用Identity Service來連結身分識別，並將原本可能分散在不同系統上的客戶完整圖片拼接在一起。

## Identity Service有什麼作用？

Identity Service提供下列作業，以達成其使命：

* 建立自訂名稱空間以符合您組織的需求。
* 建立、更新和檢視身分圖。
* 根據資料集刪除身分。
* 刪除身分以確保法規遵循。

## Identity Service如何連結身分

當身分名稱空間和身分值相符時，就會建立兩個身分之間的連結。

一般登入事件&#x200B;**會將兩個身分**&#x200B;傳送到Experience Platform中：

* 代表已驗證使用者的個人識別碼（例如CRMID）。
* 代表網頁瀏覽器的瀏覽器識別碼（例如ECID）。

考量下列範例：

* 您使用筆記型電腦登入電子商務網站，並使用您的使用者名稱和密碼組合。 此事件可讓您符合驗證使用者的資格，因此Identity Service可辨識您的CRMID。
* 您使用瀏覽器存取電子商務網站時，Identity Service也會將其識別為事件。 此事件會透過ECID在Identity Service中呈現。
* 在幕後，Identity Service會以`CRM_ID:ABC, ECID:123`處理兩個事件。
   * CRMID： ABC是代表您身為已驗證使用者的名稱空間和值。
   * ECID： 123是名稱空間和值，代表筆記型電腦上網頁瀏覽器的使用情形。
* 接下來，如果您以相同的認證登入相同的電子商務網站，但使用手機上的網頁瀏覽器，而非筆記型電腦上的網頁瀏覽器，則會在Identity Service中註冊新的ECID。
* 在幕後，Identity Service會將此新事件當成`{CRM_ID:ABC, ECID:456}`處理，其中CRM_ID：ABC代表您驗證的客戶ID，而ECID：456代表您行動裝置上的網頁瀏覽器。

考慮到上述情況，Identity Service會建立`{CRM_ID:ABC, ECID:123}`與`{CRM_ID:ABC, ECID:456}`之間的連結。 這會產生一個身分圖表，讓您「擁有」三個身分：一個代表個人識別碼(CRMID)，兩個代表Cookie識別碼(ECID)。

如需詳細資訊，請閱讀[身分識別服務如何連結身分識別](./features/identity-linking-logic.md)的指南。

## 身分圖

身分圖表是不同身分名稱空間之間關係的地圖，可讓您以視覺效果呈現並更能瞭解哪些客戶身分連結，以及如何連結。 如需詳細資訊，請參閱[上的教學課程（使用身分圖表檢視器](./features/identity-graph-viewer.md)）。

以下影片旨在協助您瞭解身分和身分圖表。

>[!VIDEO](https://video.tv.adobe.com/v/27841?quality=12&learn=on)

## 瞭解Identity Service在Experience Platform基礎結構中的角色

Identity Service在Experience Platform中扮演著重要的角色。 部分重要整合專案包括：

* [結構描述](../xdm/home.md)：在指定的結構描述中，標示為身分的結構描述欄位允許建立身分圖表。
* [資料集](../catalog/datasets/overview.md)：當資料集已啟用擷取至Real-Time Customer Profile時，會從資料集產生身分圖表，前提是資料集至少有兩個欄位標籤為身分。
* [Web SDK](../web-sdk/home.md)： Web SDK會將體驗事件傳送至Adobe Experience Platform，而且當事件中有兩個或多個身分時，身分識別服務會產生圖形。
* [即時客戶個人檔案](../profile/home.md)：在合併指定個人檔案的屬性和事件之前，即時客戶個人檔案可以參考身分圖表。 如需詳細資訊，請閱讀[瞭解Identity Service和即時客戶個人檔案](./identity-and-profile.md)之間關係的指南。
* [目的地](../destinations/home.md)：目的地可以根據身分名稱空間將設定檔資訊傳送至其他系統，例如雜湊電子郵件。
* [區段比對](../segmentation/ui/segment-match/overview.md)：區段比對在兩個具有相同身分名稱空間和身分值的不同沙箱中比對兩個設定檔。
* [Privacy Service](../privacy-service/home.md)：如果刪除要求包含`identity`，則可使用Privacy Service的隱私權要求處理功能，從身分服務中刪除指定的名稱空間和身分值組合。

