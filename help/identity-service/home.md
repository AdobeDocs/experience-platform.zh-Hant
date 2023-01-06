---
keywords: Experience Platform；首頁；熱門主題；身分；身分；XDM圖表；身分服務；身分服務
solution: Experience Platform
title: Identity服務概述
description: Adobe Experience Platform Identity Service可協助您跨裝置和系統橋接身分，以便即時提供具影響力的個人數位體驗，進而更全面了解客戶及其行為。
exl-id: a22dc3f0-3b7d-4060-af3f-fe4963b45f18
source-git-commit: ad9fb0bcc7bca55da432c72adc94d49e3c63ad6e
workflow-type: tm+mt
source-wordcount: '1839'
ht-degree: 0%

---

# [!DNL Identity Service] 概覽

要提供相關的數位體驗，必須全面了解客戶。 當您的客戶資料分散於不同的系統，導致每個個別客戶看起來都有多個「身分」時，就會更加困難。

Adobe Experience Platform Identity Service可跨裝置和系統橋接身分，提供客戶及其行為的全面檢視，讓您即時提供具影響力的個人數位體驗。

使用 [!DNL Identity Service]，您可以：

- 確保客戶透過每次互動獲得一致、個人化且相關的體驗。
- 從不同的來源匯整數個不同的身分，並建立客戶的完整檢視。
- 利用身分圖表來對應不同的身分識別命名空間，以視覺化呈現客戶如何透過不同管道與您的品牌互動。

## 快速入門

在了解 [!DNL Identity Service]，主要術語的摘要如下：

| 詞語 | 定義 |
| --- | --- |
| 身分 | 身分是實體（通常為個人）專屬的資料。 身分識別（例如登入ID、ECID或忠誠度ID）也稱為「已知身分」。 |
| ECID | Experience CloudID(ECID)是跨Experience Platform和Adobe Experience Cloud應用程式使用的共用身分命名空間。 ECID為客戶身分提供基礎，並作為裝置的主要ID，以及身分圖表的基節點。 請參閱 [ECID概觀](./ecid.md) 以取得更多資訊。 |
| 身分命名空間 | 身分命名空間可用來區分身分的內容或類型。 例如，身分會區分「name」<span>@email.com」作為電子郵件地址，或「443522」作為數值CRM ID。 身分識別命名空間可用來尋找個別身分識別，並提供身分值的內容。 這可讓您判斷 [!DNL Profile] 包含不同主要ID，但共用相同值的片段 `email` 身分命名空間實際上是同一個人。 請參閱 [身分命名空間概述](./namespaces.md) 以取得更多資訊。 |
| 身分圖 | 身分圖表是不同身分之間關係的地圖，可讓您以視覺化方式呈現並更清楚了解哪些客戶身分識別會匯整在一起，以及匯整方式。 請參閱 [使用身分圖表檢視器](./ui/identity-graph-viewer.md) 以取得更多資訊。 |
| 個人識別資訊(PII) | PII是可直接識別客戶的資訊，例如電子郵件地址或電話號碼。 PII值常用來比對。 不同系統間客戶的多重身分識別。 |
| 未知或匿名身份 | 未知或匿名的身分是指示器，可隔離裝置，而不識別使用裝置的實際人員。 未知和匿名身分識別包含訪客的IP位址和Cookie ID等資訊。 雖然未知和匿名的身分可提供行為資料，但在客戶提供其PII前，這些身分資料有限。 |

## 什麼是 [!DNL Identity Service]？

每天，客戶都會與您的業務互動，並與您的品牌建立持續成長的關係。 典型客戶可能在貴組織資料基礎架構中的任意數量系統中處於活動狀態，例如您的電子商務、忠誠度和服務台系統。 同一客戶也可以在任何數量的設備上匿名參與。 [!DNL Identity Service] 可讓您將客戶的完整圖片拼湊在一起，以匯總可能分散在不同系統的相關資料。

以消費者與品牌關係的日常範例為例：

- Mary在您的電子商務網站上有一個帳戶，她過去在那裡完成了一些訂單。 她通常用自己的筆記型電腦去購物，每次都在那裡登錄。 不過，在一次探訪期間，她使用平板電腦購買涼鞋，但並未下訂單，也未登入。
- 此時，Mary的活動會以兩個不同的設定檔顯示：
   - 她的電子商務登錄
   - 她的平板電腦，可能由裝置ID識別
- Mary稍後會繼續其平板電腦工作階段，並在訂閱電子報時提供其電子郵件地址。 執行此動作時，串流擷取會在其設定檔中新增新身分，作為記錄資料。 因此， [!DNL Identity Service] 現在，Mary的平板電腦裝置活動與其電子商務帳戶記錄有關。
- 在下次點按她的平板電腦時，您的目標內容可能會反映Mary的完整設定檔和歷史記錄，而不只是未知購物者使用的平板電腦。

![Platform上的身分識別匯整](./images/identity-service-stitching.png)

基本上， [!DNL Identity Service] 可讓您將客戶的完整圖片拼湊在一起，匯總可能分散在不同系統的相關資料。 具有 [!DNL Identity Service] 「即時客戶設定檔」會運用定義和維護功能，建立客戶及其與您品牌互動的完整畫面。 如需詳細資訊，請參閱 [即時客戶個人檔案概觀](../profile/home.md).

### 使用案例

範例 [!DNL Identity Service] 實施包括：

- 電信公司可能依賴「電話號碼」值，在該值中，電話號碼會指離線和線上資料集中感興趣的同一個人。
- 零售公司可能會在離線資料集中使用「電子郵件地址」，並線上上資料集中使用ECID，因為匿名訪客的百分比很高。
- 銀行在離線資料集（如分行交易）中可能偏好使用「帳號」。 它們可能依賴線上資料集中的「登入ID」，因為大部分訪客在造訪期間都會經過驗證。
- 您的客戶也可能有唯一的專屬ID，例如GUID或其他通用唯一識別碼。

## 身分命名空間 {#identity-namespace}

>[!CONTEXTUALHELP]
>id="platform_identity_namespace"
>title="身分識別命名空間"
>abstract="身分命名空間可用來區分身分的內容或類型。 例如，身分會區分「name」<span>@email.com」作為電子郵件地址，或「443522」作為數值CRM ID。"
>text="Learn more in documentation"

>[!CONTEXTUALHELP]
>id="platform_identity_value"
>title="身分值"
>abstract="身分值是代表不重複個人、組織或資產的識別碼。 值代表的內容或身分類型由對應的身分命名空間定義。 當跨設定檔片段比對記錄資料時，命名空間和身分值必須符合。當跨設定檔片段比對記錄資料時，命名空間和身分值必須符合。"
>text="Learn more in documentation"

如果你問一個人「你的ID是什麼？」 如果沒有任何進一步的背景，他們就很難提供有用的答案。 根據相同邏輯，表示標識值的字串值（無論是系統生成的ID還是電子郵件地址）僅在提供給字串值上下文的限定符時完成：身分識別命名空間。

您的客戶可能會透過線上和離線管道的組合與您的品牌互動，導致如何將這些分散的互動協調為單一客戶身分的難題。

從在多個裝置和管道中識別客戶開始，即可了解客戶。 Platform使用身分識別命名空間來達成此目的。 身分命名空間是識別碼，例如電子郵件或電話，用來提供客戶身分識別的其他內容。 身分識別命名空間可用來尋找或連結個別身分識別，以及提供身分值的內容。 請參閱 [身分命名空間概述](./namespaces.md) 以取得更多資訊。

## 身分圖

身分圖表是不同身分識別命名空間之間關係的地圖，可讓您以視覺化方式呈現並更清楚了解將哪些客戶身分識別連結在一起，以及連結方式。 請參閱 [使用身分圖表檢視器](./ui/identity-graph-viewer.md) 以取得更多資訊。

以下影片旨在支援您對身分和身分圖表的了解。

>[!VIDEO](https://video.tv.adobe.com/v/27841?quality=12&learn=on)

## 提供身分資料給 [!DNL Identity Service]

本節說明在使用前，如何處理提供給Adobe Experience Platform的資料 [!DNL Identity Service] 為每個客戶建立身分圖。

### 決定身分欄位

您標示為身分的資料欄位，會根據您的企業資料收集策略，決定身分對應中包含的資料。 為了充份發揮Adobe Experience Platform的優點，並盡可能提供最完整的客戶身分識別，您應上傳線上和離線資料。

- 線上資料是描述線上狀態和行為的資料，例如使用者名稱和電子郵件地址。

- 離線資料是指與線上狀態無直接關聯的資料，例如來自CRM系統的ID。 這類資料可讓您的身分更健全，並支援不同系統間的資料內聚。

### 建立其他身分識別命名空間

雖然Experience Platform提供多種標準命名空間，但您可能需要建立其他命名空間，才能正確地為您的身分分類。 如需詳細資訊，請參閱 [檢視和建立組織的命名空間](./namespaces.md) 在「身分命名空間」概述中。

>[!NOTE]
>
>身分識別命名空間是身分識別的限定符。 因此，一旦建立了命名空間，就無法刪除它。

### 在中包含身分資料 [!DNL Experience Data Model] (XDM)

作為標準化框架， [!DNL Platform] 組織客戶資料， [!DNL Experience Data Model] (XDM)可讓您在與互動的Experience Platform和其他服務之間共用及了解資料 [!DNL Platform]. 如需詳細資訊，請參閱 [XDM系統概觀](../xdm/home.md).

記錄和時間序列結構都提供了包含身份資料的方法。 擷取資料時，如果發現來自不同命名空間的資料片段可共用共同身分資料，則身分圖表將建立這些片段之間的新關係。

### 將XDM欄位標示為身分

任何類型的欄位 `string` 在實作記錄或時間序列XDM類別的結構中，可以將標示為身分欄位。 因此，擷取至該欄位的所有資料都會視為身分資料。

>[!NOTE]
>
>不支援陣列和映射類型欄位，不能標籤為標識欄位並標籤為標識欄位。

如果身分欄位共用通用PII資料，也允許連結身分。
例如，通過將電話號碼欄位標籤為身份欄位， [!DNL Identity Service] 自動繪製與發現使用相同電話號碼的其他個人的關係圖。

>[!NOTE]
>
>在標示欄位時，會提供產生身分的命名空間。

### 設定資料集 [!DNL Identity Service]

在串流擷取程式期間， [!DNL Identity Service ]從記錄和時間序列資料中自動提取身份資料。 不過，在可擷取資料之前，必須為 [!DNL Identity Service]. 請參閱  [使用API為即時客戶個人檔案和身分服務設定資料集](../profile/tutorials/dataset-configuration.md) 以取得更多資訊。

### 將資料內嵌至 [!DNL Identity Service]

[!DNL Identity Service] 使用發送到Experience Platform的XDM相容資料，由 [批次內嵌](../ingestion/batch-ingestion/overview.md) 或 [串流內嵌](../ingestion/streaming-ingestion/overview.md).

以下影片旨在支援您對Identity Service的了解。 此影片會示範如何將資料欄位標示為身分、擷取身分資料，然後確認資料已送至Adobe Experience Platform Identity Service私人圖表。

>[!WARNING]
>
>此 [!DNL Platform] 下列影片中顯示的UI已過期。 請參閱檔案，了解最新的UI螢幕擷取畫面和功能。

>[!VIDEO](https://video.tv.adobe.com/v/28167?quality=12&learn=on)

## 資料控管

Adobe Experience Platform的建置秉承隱私權，並包含資料控管架構，以保護客戶PII資料。 「電子郵件」或「電話」命名空間下的身分資料預設會加密，但為了確保敏感資料在持續保存前經過加密，資料使用標籤可在資料擷取時或送達時套用至資料 [!DNL Platform]. 欲知更多資訊，請閱讀 [資料控管概觀](../data-governance/home.md).

## 後續步驟

既然您了解 [!DNL Identity Service] 及其在Experience Platform中的角色，您可以開始了解如何使用您的身分圖表 [[!DNL Identity Service API]](./api/getting-started.md).
