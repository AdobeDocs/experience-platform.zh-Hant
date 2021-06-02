---
keywords: Experience Platform；首頁；熱門主題；身分；身分；XDM圖表；身分服務；身分服務
solution: Experience Platform
title: Identity服務概述
topic-legacy: overview
description: Adobe Experience Platform Identity Service可協助您跨裝置和系統橋接身分，以便即時提供具影響力的個人數位體驗，進而更全面了解客戶及其行為。
exl-id: a22dc3f0-3b7d-4060-af3f-fe4963b45f18
source-git-commit: 288f24351788ed4b8a0c68cffe5eb5c91ed01691
workflow-type: tm+mt
source-wordcount: '1734'
ht-degree: 0%

---

# [!DNL Identity Service] 概觀

要提供相關的數位體驗，必須全面了解客戶。 當您的客戶資料分散於不同的系統，導致每個個別客戶看起來都有多個「身分」時，就會更加困難。 Adobe Experience Platform [!DNL Identity Service]可協助您跨裝置和系統橋接身分，以便即時提供具影響力的個人數位體驗，進而更全面了解客戶及其行為。

## 瞭解 [!DNL Identity Service]

每天，客戶都會與您的業務互動，並與您的品牌建立持續成長的關係。 典型客戶可能在貴組織資料基礎架構中的任意數量系統中處於活動狀態，例如電子商務、忠誠度和服務台系統。 同一客戶也可以在任何數量的設備上匿名參與。 [!DNL Identity Service] 可讓您將客戶的完整圖片拼湊在一起，以匯總可能分散在不同系統的相關資料。

以消費者與品牌關係的日常範例為例：

Mary在您的電子商務網站上有一個帳戶，過去她在那裡完成了一些訂單。 她通常用自己的筆記型電腦去購物，每次都在那裡登錄。 不過，在一次探訪期間，她使用平板電腦購買涼鞋，但並未下訂單，也未登入。

此時，Mary的活動會以兩個不同的設定檔顯示：她的電子商務登入和平板電腦裝置（可能由裝置ID識別）。

Mary稍後會繼續其平板電腦工作階段，並在訂閱電子報時提供其電子郵件地址。 執行此動作時，串流擷取會在其設定檔中新增新身分，作為記錄資料。 因此，[!DNL Identity Service]現在會將Mary的平板電腦裝置活動與其電子商務帳戶記錄產生關聯。

在下次點按她的平板電腦時，您的目標內容可能會反映Mary的完整設定檔和歷史記錄，而不只是未知購物者使用的平板電腦。

[!DNL Identity Service]定義和維護的身分關係由[!DNL Real-time Customer Profile]運用，以建立客戶及其與您品牌互動的完整圖片。 如需詳細資訊，請參閱[即時客戶設定檔概述](../profile/home.md)。

### 身分

身分是實體（通常為個人）專屬的資料。 登入ID、ECID或忠誠度ID等身分識別，即為已知身分識別。

PII（例如電子郵件地址和電話號碼）可直接識別客戶。 因此，PII可用來比對客戶跨系統的多重身分。

未知或匿名的身分識別會挑出裝置，而不會識別實際使用該裝置的人員。 此類別包含訪客的IP位址和Cookie ID等資訊。 雖然可使用未知身分從裝置收集行為資料，但在客戶在歷程中提供PII之前，將這些身分資料與裝置或媒體相關聯的方式有限。

如下圖所示，已知和匿名身份是[標識圖](#identity-graphs)的重要元件，本文檔稍後將討論這些元件。

![Platform上的身分識別匯整](./images/identity-service-stitching.png)

[!DNL Identity Service]實作範例包括：

- 電信公司可能依賴「電話號碼」值，在該值中，電話號碼會指離線和線上資料集中感興趣的同一個人。
- 零售公司可能會在離線資料集中使用「電子郵件地址」，並線上上資料集中使用ECID，因為匿名訪客的百分比很高。
- 銀行在離線資料集（如分行交易）中可能偏好使用「帳號」。 它們可能依賴線上資料集中的「登入ID」，因為大部分訪客在造訪期間都會經過驗證。
- 您的客戶也可能有唯一的專屬ID，例如GUID或其他通用唯一識別碼。

### 身分資料

如果你問一個人「你的ID是什麼？」 如果沒有任何進一步的背景，他們就很難提供有用的答案。 根據相同邏輯，表示標識值的字串值（無論是系統生成的ID還是電子郵件地址）僅在提供給字串值上下文的限定符時完成：身分識別命名空間。

## 身分識別命名空間與身分圖

您的客戶可能會透過線上和離線管道的組合與您的品牌互動，因此難以將這些分散的互動整合為單一客戶身分。

[!DNL Experience Platform] 通過兩個概念解決此難題： [身分](#identity-namespaces) 名稱和 [身分圖表](#identity-graphs)。

以下影片旨在支援您對身分和身分圖表的了解。 下列影片涵蓋身分收集、身分圖表和API的三項功能。 此外，還描述了如何使用確定性和概率算法來構造私有標識圖，並討論了私有標識圖、Adobe Experience Platform Identity Service Co-Op Graph和第三方圖的作用。

>[!VIDEO](https://video.tv.adobe.com/v/27841?quality=12&learn=on)

### 身分識別命名空間

當您的客戶透過多個管道與您的品牌互動時，包括網路、行動應用程式、客服中心或店面，如果您無法跨管道觀察及追蹤其活動，就很難了解及提供這些服務。

從在多個裝置和管道中識別客戶開始，即可了解客戶。 Adobe Experience Platform會使用身分識別命名空間來達到此目的。
身分命名空間是識別碼，例如裝置ID或電子郵件ID，用於提供資料來源的內容。 身分識別命名空間可用來尋找或連結個別身分識別，以及提供身分值的內容，以避免資料衝突。 例如，ID「123456」可能是指您的電子商務系統中的一個人員，以及服務台系統中的另一個人員。 如需詳細資訊，請參閱[身分命名空間概述](./namespaces.md)。

### 身分圖

身分圖表是不同身分識別命名空間之間關係的對應圖，可以以視覺化呈現客戶如何透過不同管道與品牌互動。

所有客戶身分圖表都會以近乎即時的方式由[!DNL Identity Service]共同管理和更新，以回應客戶活動。

[!DNL Identity Service] 管理僅由您的組織可見且根據您的資料（稱為專用圖表）建立的身分圖表。[!DNL Identity Service] 擷取的資料記錄包含多個身分，並在找到的身分之間新增關係時，可擴大您的私人圖表。

舉例來說，在提供和標示身分資料時，使用電話號碼（例如「工作電話」）可能會產生比您在身分圖表中所想的更多關係，這是需要考慮的可能因素類型。 你可能會發現，許多員工在工作中都提到了相同的數字，而「家」和「移動」更好地使關係盡可能精確。

如需詳細資訊，請參閱有關[存取身分圖檢視器](./ui/identity-graph-viewer.md)的教學課程

## 向[!DNL Identity Service]提供身份資料

本節說明在[!DNL Identity Service]使用前，如何處理提供給Adobe Experience Platform的資料，以便為每個客戶建立身分圖表。

### 決定身分欄位

您標示為身分的資料欄位，會根據您的企業資料收集策略，決定身分對應中包含的資料。 為了充份發揮Adobe Experience Platform的優點，並盡可能提供最完整的客戶身分識別，您應上傳線上和離線資料。

- 線上資料是描述線上狀態和行為的資料，例如使用者名稱和電子郵件地址。

- 離線資料是指與線上狀態無直接關聯的資料，例如來自CRM系統的ID。 這類資料可讓您的身分更健全，並支援不同系統間的資料內聚。

### 建立其他身分識別命名空間

雖然[!DNL Experience Platform]提供多種標準命名空間，但您可能需要建立其他命名空間，才能正確分類您的身分。 如需詳細資訊，請參閱身分命名空間概觀中的[檢視及建立組織的命名空間一節。](./namespaces.md)

>[!NOTE]
>
>身分識別命名空間是身分識別的限定符。 因此，一旦建立了命名空間，就無法刪除它。

### 在[!DNL Experience Data Model](XDM)中包含身分資料

[!DNL Platform]組織客戶資料的標準化架構[!DNL Experience Data Model](XDM)可讓資料在[!DNL Experience Platform]和與[!DNL Platform]互動的其他服務之間共用和理解。 如需詳細資訊，請參閱[XDM系統概述](../xdm/home.md)。

記錄和時間序列結構都提供了包含身份資料的方法。 擷取資料時，如果發現來自不同命名空間的資料片段可共用共同身分資料，則身分圖表將建立這些片段之間的新關係。

### 將XDM欄位標示為身分

架構中實作記錄或時間序列XDM類的任何類型`string`欄位都可標示為身分欄位。 因此，擷取至該欄位的所有資料都會視為身分資料。

>[!NOTE]
>
>不支援陣列和映射類型欄位，不能標籤為標識欄位並標籤為標識欄位。

如果身分欄位共用通用PII資料，也允許連結身分。
例如，[!DNL Identity Service]通過將電話號碼欄位標籤為標識欄位，自動繪製與發現使用相同電話號碼的其他個人之間的關係圖。

>[!NOTE]
>
>在標示欄位時，會提供產生身分的命名空間。

### 為[!DNL Identity Service]配置資料集

在串流擷取程式期間， [!DNL Identity Service ]會自動從記錄和時間序列資料中擷取身分資料。 不過，在可以內嵌資料之前，必須先為[!DNL Identity Service]啟用。 如需詳細資訊，請參閱有關使用API](../profile/tutorials/dataset-configuration.md)為即時客戶設定檔與身分服務設定資料集的教學課程。[

### 將資料內嵌至[!DNL Identity Service]

[!DNL Identity Service] 透過批次內嵌或串流內嵌 [!DNL Experience Platform] 方式， [取](../ingestion/batch-ingestion/overview.md) 用傳送至 [的XDM相容資料](../ingestion/streaming-ingestion/overview.md)。

以下影片旨在支援您對Identity Service的了解。 此影片會示範如何將資料欄位標示為身分、擷取身分資料，然後確認資料已送至Adobe Experience Platform Identity Service私人圖表。

>[!WARNING]
>
>以下影片中顯示的[!DNL Platform] UI已過期。 請參閱檔案，了解最新的UI螢幕擷取畫面和功能。

>[!VIDEO](https://video.tv.adobe.com/v/28167?quality=12&learn=on)

## 資料控管

Adobe Experience Platform的建置秉承隱私權，並包含資料控管架構，以保護客戶PII資料。 「電子郵件」或「電話」命名空間下的身分資料預設會加密，但為了確保敏感資料在持續保存前經過加密，資料使用標籤可在資料被擷取時或在[!DNL Platform]送達時套用至資料。 如需詳細資訊，請參閱[資料控管概述](../data-governance/home.md)。

## 後續步驟

現在您已了解[!DNL Identity Service]的重要概念及其在[!DNL Experience Platform]內的角色，接下來您可以開始了解如何使用[[!DNL Identity Service API]](./api/getting-started.md)使用您的身分圖。
