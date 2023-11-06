---
keywords: Experience Platform；首頁；熱門主題；身分；身分；XDM圖形；身分服務；身分服務
solution: Experience Platform
title: Identity Service總覽
description: Adobe Experience Platform Identity Service可跨裝置和系統橋接身分，讓您即時提供具影響力的個人數位體驗，協助您更清楚瞭解客戶及其行為。
exl-id: a22dc3f0-3b7d-4060-af3f-fe4963b45f18
source-git-commit: ad9fb0bcc7bca55da432c72adc94d49e3c63ad6e
workflow-type: tm+mt
source-wordcount: '1839'
ht-degree: 10%

---

# [!DNL Identity Service] 概覽

提供相關的數位體驗需要完全瞭解您的客戶。 當您的客戶資料分散於不同的系統時，這會使工作變得更困難，導致每個個別客戶似乎擁有多個「身分」。

Adobe Experience Platform 身分識別服務透過跨裝置和系統橋接身分，為您提供客戶及其行為的全方位檢視，讓您可即時實現有影響力的個人數位體驗。

替換為 [!DNL Identity Service]，您可以：

- 透過每次互動，確保您的客戶獲得一致、個人化且相關的體驗。
- 將來自不同來源的幾個不同身分拼接在一起，並建立客戶的完整檢視。
- 利用身分圖表來對應不同的身分識別名稱空間，以視覺化方式呈現客戶如何跨不同管道與您的品牌互動。

## 快速入門

在深入瞭解詳細資訊之前 [!DNL Identity Service]，以下是主要術語的簡短摘要：

| 詞語 | 定義 |
| --- | --- |
| 身分 | 身分是實體 (通常為個人) 專屬的資料。登入ID、ECID或忠誠度ID等身分也稱為「已知身分」。 |
| ECID | Experience CloudID (ECID)是跨Experience Platform和Adobe Experience Cloud應用程式使用的共用身分名稱空間。 ECID為客戶身分識別奠定基礎，並作為裝置的主要ID以及身分圖表的基礎節點。 請參閱 [ECID概觀](./ecid.md) 以取得詳細資訊。 |
| 身分命名空間 | 身分識別命名空間用於區分身分識別的內容或類型。例如，身分識別會將「name<span>@email.com」區分為電子郵件地址或將「443522」區分為數值的 CRM ID。身分識別名稱空間是用來查詢個別身分，並提供身分識別值的內容。 這可讓您判斷以下兩個 [!DNL Profile] 包含不同主要ID，但共用相同值的片段 `email` 身分名稱空間，實際上是同一個人。 請參閱 [身分名稱空間總覽](./namespaces.md) 以取得詳細資訊。 |
| 識別圖 | 身分圖表是不同身分之間的關係圖，可讓您以視覺效果呈現並更能瞭解哪些客戶身分拼接在一起，以及如何拼接。 請參閱上的教學課程 [使用身分圖表檢視器](./ui/identity-graph-viewer.md) 以取得詳細資訊。 |
| 個人識別資訊(PII) | PII是可直接識別客戶的資訊，例如電子郵件地址或電話號碼。 PII值通常用於比對。 跨不同系統的客戶多個身分。 |
| 未知或匿名的身分 | 未知或匿名的身分是隔離裝置的指標，但無法識別使用裝置的實際人員。 未知和匿名身分包含訪客的IP位址和Cookie ID等資訊。 雖然未知和匿名身分可提供行為資料，但在客戶提供其PII之前，它們都是有限的。 |

## 什麼是 [!DNL Identity Service]？

客戶每天都會與您的企業互動，並與您的品牌建立持續成長的關係。 一般客戶可能會在您組織資料基礎架構內的任何數量的系統中積極活動，例如您的電子商務、忠誠度和服務檯系統。 同一客戶也可在任意數量的裝置上匿名參與。 [!DNL Identity Service] 可讓您拼湊客戶的完整面貌，彙總可能分散在不同系統間的相關資料。

以消費者與品牌關係的日常範例為例：

- Mary在您的電子商務網站上有一個帳戶，她過去曾在該帳戶上完成一些訂單。 她通常使用自己的筆記型電腦購物，每次都會登入其中。 不過，在其中一次造訪中，她使用平板電腦購買涼鞋，但並未下訂單，亦未登入。
- 此時，Mary的活動會顯示為兩個個別的設定檔：
   - 她的電子商務登入
   - 她的平板電腦裝置，可能由裝置ID識別
- Mary稍後會恢復她的平板電腦工作階段，並在訂閱電子報時提供電子郵件地址。 在這樣做時，串流擷取會在她的設定檔中新增身分作為記錄資料。 因此， [!DNL Identity Service] 現在將Mary的平板電腦裝置活動與她的電子商務帳戶記錄建立關聯。
- 在她的平板電腦上按一下後，您的目標內容可能會反映Mary的完整個人資料和歷史記錄，而不僅僅是未知購物者使用的平板電腦。

![Platform上的身分彙整](./images/identity-service-stitching.png)

基本上， [!DNL Identity Service] 可讓您拼湊客戶的完整面貌，彙總可能分散在不同系統間的相關資料。 身分關係 [!DNL Identity Service] 即時客戶個人檔案會利用定義和維護功能，來建立客戶及其與您品牌互動的完整面貌。 如需詳細資訊，請參閱 [即時客戶個人檔案總覽](../profile/home.md).

### 使用案例

範例 [!DNL Identity Service] 實施包括：

- 電信公司可能會依賴「電話號碼」值，電話號碼會指涉離線和線上資料集中的同一人。
- 由於匿名訪客的百分比很高，零售公司可能會在離線資料集中使用「電子郵件地址」，並線上上資料集中使用ECID。
- 銀行可能偏好使用離線資料集中的「帳號」，例如分行交易。 它們可能會以線上資料集中的「登入ID」為依據，因為大多數訪客在造訪期間都會經過驗證。
- 您的客戶也可能有唯一的專屬ID，例如GUID或其他通用唯一識別碼。

## 身分命名空間 {#identity-namespace}

>[!CONTEXTUALHELP]
>id="platform_identity_namespace"
>title="身分識別命名空間"
>abstract="身分識別命名空間用於區分身分識別的內容或類型。例如，身分識別會將「name<span>@email.com」區分為電子郵件地址或將「443522」區分為數值的 CRM ID。"
>text="Learn more in documentation"

>[!CONTEXTUALHELP]
>id="platform_identity_value"
>title="身分識別值"
>abstract="身分識別值是代表唯一個人、組織或資產的識別碼。該值代表的身分識別的內容或類型由相對應的身分識別命名空間定義。在不同設定檔片段之間比對記錄資料時，命名空間和身分識別值必須相符。"
>text="Learn more in documentation"

如果您問某人「您的ID為何？」 如果沒有進一步的內容，他們很難提供有用的答案。 按照相同的邏輯，代表身分值（不論是系統產生的ID或電子郵件地址）的字串值，只有在提供提供字串值內容的限定詞時才會完成：身分名稱空間。

您的客戶可能透過線上和離線頻道的結合與您的品牌互動，導致如何協調這些分散互動為單一客戶身分識別的挑戰。

瞭解您跨多個裝置和管道的客戶，首先要瞭解他們在每個管道中的識別方式。 Platform會使用身分名稱空間來達成此目的。 身分名稱空間是像電子郵件或電話之類的識別碼，用來提供客戶身分識別的其他內容。 身分識別名稱空間是用來查詢或連結個別身分，以及提供身分識別值的內容。 請參閱 [身分名稱空間總覽](./namespaces.md) 以取得詳細資訊。

## 身分圖

身分圖表是不同身分名稱空間之間關係的地圖，可讓您以視覺效果呈現並更能瞭解哪些客戶身分連結，以及如何連結。 請參閱上的教學課程 [使用身分圖表檢視器](./ui/identity-graph-viewer.md) 以取得詳細資訊。

以下影片旨在協助您瞭解身分和身分圖表。

>[!VIDEO](https://video.tv.adobe.com/v/27841?quality=12&learn=on)

## 提供身分資料給 [!DNL Identity Service]

本節說明提供給Adobe Experience Platform的資料在使用前如何進行處理 [!DNL Identity Service] 為每位客戶建立身分圖表。

### 決定身分欄位

根據您的企業資料收集策略，您標籤為身分的資料欄位將決定哪些資料包含在身分對應中。 若要發揮Adobe Experience Platform的最大效益和最完整的客戶身分識別，您應同時上傳線上和離線資料。

- 線上資料是描述線上狀態和行為的資料，例如使用者名稱和電子郵件地址。

- 離線資料是指與線上狀態不直接相關的資料，例如CRM系統的ID。 這類資料可讓您的身分識別更加健全，並支援不同系統間的資料內聚力。

### 建立其他身分名稱空間

雖然Experience Platform提供各種標準名稱空間，但您可能需要建立其他名稱空間以將您的身分正確分類。 如需詳細資訊，請參閱以下章節： [檢視和建立組織的名稱空間](./namespaces.md) 身分名稱空間概觀中的。

>[!NOTE]
>
>身分名稱空間是身分的限定詞。 因此，建立名稱空間後就無法刪除。

### 包含身分資料 [!DNL Experience Data Model] (XDM)

作為標準化架構的資訊， [!DNL Platform] 組織客戶資料， [!DNL Experience Data Model] (XDM)可讓您透過Experience Platform和其他與互動的服務來共用和瞭解資料 [!DNL Platform]. 如需詳細資訊，請參閱 [XDM系統概覽](../xdm/home.md).

記錄和時間序列結構描述都提供了包含身分資料的方法。 在擷取資料時，如果發現來自不同名稱空間的資料片段共用共同的身分資料，身分圖表會在這些資料片段之間建立新的關係。

### 將XDM欄位標示為身分

任何型別的欄位 `string` 在實作記錄或時間序列的結構描述中，XDM類別可以標示為身分欄位。 因此，所有擷取至該欄位的資料都將被視為身分資料。

>[!NOTE]
>
>陣列和對應型別欄位不受支援，且無法標籤為身分欄位。

如果身分欄位共用常見的PII資料，則這些身分欄位也允許連結身分。
例如，將電話號碼欄位標示為身分欄位， [!DNL Identity Service] 自動繪製與其他使用相同電話號碼之個人的關係圖。

>[!NOTE]
>
>在標籤欄位時，會提供所產生身分的名稱空間。

### 設定資料集 [!DNL Identity Service]

在串流擷取程式期間， [!DNL Identity Service]自動從記錄和時間序列資料中擷取身分資料。 不過，在可以內嵌資料之前，必須先啟用 [!DNL Identity Service]. 請參閱上的教學課程  [使用API為即時客戶個人資料和身分服務設定資料集](../profile/tutorials/dataset-configuration.md) 以取得詳細資訊。

### 將資料內嵌至 [!DNL Identity Service]

[!DNL Identity Service] 使用透過以下任一方式傳送給Experience Platform的XDM相容資料： [批次擷取](../ingestion/batch-ingestion/overview.md) 或 [串流擷取](../ingestion/streaming-ingestion/overview.md).

以下影片旨在協助您瞭解Identity Service。 此影片說明如何將資料欄位標示為身分、擷取身分識別資料，然後驗證資料是否已送入Adobe Experience Platform Identity Service私人圖表。

>[!WARNING]
>
>此 [!DNL Platform] 以下影片中顯示的UI已過期。 請參閱檔案以瞭解最新的UI熒幕擷取畫面及功能。

>[!VIDEO](https://video.tv.adobe.com/v/28167?quality=12&learn=on)

## 資料控管

Adobe Experience Platform建置時已考慮到隱私權，並包含資料控管架構，以保護您的客戶PII資料。 預設會加密「電子郵件」或「電話」名稱空間下的身分資料，但為了確保敏感資料在儲存前就已加密，資料使用標籤可在資料內嵌或傳入時套用至資料 [!DNL Platform]. 如需詳細資訊，請閱讀 [資料控管概觀](../data-governance/home.md).

## 後續步驟

現在您已瞭解 [!DNL Identity Service] 以及其在Experience Platform中的角色，您就可以開始瞭解如何使用身分圖表 [[!DNL Identity Service API]](./api/getting-started.md).
