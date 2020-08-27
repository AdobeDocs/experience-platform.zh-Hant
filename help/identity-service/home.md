---
keywords: Experience Platform;home;popular topics;identity;Identity;XDM graphs;identity service;Identity service
solution: Experience Platform
title: Adobe Experience Platform Identity Service
topic: overview
description: Adobe Experience Platform Identity Service可跨裝置和系統橋接身分，協助您更全面地瞭解客戶及其行為，讓您即時提供具影響力的個人化數位體驗。
translation-type: tm+mt
source-git-commit: 8b1b61b6446b28f92d6cf221003674fa09716c53
workflow-type: tm+mt
source-wordcount: '1711'
ht-degree: 0%

---


# [!DNL Identity Service]概述

要提供相關的數位體驗，必須全面瞭解客戶。 當客戶資料分散在不同的系統上時，這會更加困難，導致每個客戶看起來都有多個「身分」。 Adobe Experience Platform可 [!DNL Identity Service] 協助您跨裝置和系統橋接身分，以便即時提供具影響力的個人化數位體驗，從而更全面地瞭解客戶及其行為。

## 瞭解 [!DNL Identity Service]

每天，客戶都會與您的業務互動，並與您的品牌建立不斷成長的關係。 通常客戶在您組織的資料基礎架構中的任何系統（例如您的電子商務、忠誠度和服務台系統）中都很活躍。 同一名客戶也可能會在任何裝置上匿名互動。 [!DNL Identity Service] 允許您將客戶的完整圖片拼湊在一起，以便將原本可能分散在不同系統的相關資料匯集起來。

以消費者與品牌關係的日常範例為例：

Mary在您的電子商務網站上有一個帳戶，她過去在那裡完成了幾筆訂單。 她通常使用個人筆記型電腦購物，每次都會登錄。 不過，在一次拜訪中，她使用平板電腦購買涼鞋，但並未下訂單，也未登入。

此時，Mary的活動會以兩個不同的配置檔案的形式出現：她的電子商務登入和平板電腦裝置，可能是透過裝置ID識別。

瑪麗稍後會繼續其平板電腦作業，並在訂閱您的電子報時提供電子郵件地址。 在這麼做時，串流擷取會在其個人檔案中新增新的身分識別作為記錄資料。 因此，現在 [!DNL Identity Service] Mary的平板電腦裝置活動與其電子商務帳戶記錄有關。

在她的平板電腦上按一下，您的定位內容可以反映瑪麗的完整個人檔案和歷史，而不只是未知顧客使用的平板電腦。

定義和維護的 [!DNL Identity Service] 身分關係可運用來 [!DNL Real-time Customer Profile] 建立客戶及其與品牌互動的完整圖景。 如需詳細資訊，請參 [閱即時客戶個人檔案總覽](../profile/home.md)。

### 身份

身分是實體（通常是個人）專屬的資料。 登入ID、ECID或忠誠度ID等身分稱為已知 **身分**。

PII（例如電子郵件地址和電話號碼）可直接識別客戶。 因此，PII可用於跨系統比對客戶的多個身分。

**未知或匿名身份** ，會挑出裝置，而不會識別實際使用者。 此類別包含訪客的IP位址和Cookie ID等資訊。 雖然可以使用未知身分從裝置收集行為資料，但在客戶在歷程中提供個人識別資訊之前，將這些身分資料關聯到不同裝置或媒體上是有限的。

如下圖所示，已知和匿名身份都是身份圖的重 [要元件](#identity-graphs)，本文檔稍後將討論。

![平台上的身份拼接](./images/identity-service-stitching.png)

實作范 [!DNL Identity Service] 例包括：

- 電信公司可能依賴「電話號碼」值，其中電話號碼是指線下和線上資料集的同一個人。
- 零售公司可能會在離線資料集中使用「電子郵件地址」，而且由於匿名訪客的比例很高，因此可能會線上上資料集中使用ECID。
- 銀行可能偏好離線資料集中的「帳號」，例如分行交易。 他們可能依賴線上資料集中的「登入ID」，因為大部分訪客在瀏覽期間都會經過驗證。
- 您的客戶也可能擁有唯一的專屬ID，例如GUID或其他普遍唯一識別碼。

### 身分資料

如果你問一個人&quot;你的身份證是什麼？&quot; 如果沒有進一步的背景，他們很難提供有用的答案。 根據相同邏輯，表示身分值的字串值（無論是系統產生的ID還是電子郵件地址）只有在提供給字串值上下文的限定詞時才會完成：識別名稱空間。

## 身份名稱空間和身份圖

您的客戶可能會透過結合線上及線下通道與品牌互動，因此，如何將這些零散的互動整合為單一客戶識別，是個挑戰。

[!DNL Experience Platform] 通過兩個概念來解決此難題： [身分名稱空間](#identity-namespaces) 和 [身分圖表](#identity-graphs)。

以下影片旨在協助您瞭解身分和身分圖。 以下視訊涵蓋Identity Collection、Identity Graphs和API的3種功能。 此外，還說明如何使用確定性和概率性演算法來建構私人身分識別圖，並討論私人身分識別圖、Adobe Experience Platform Identity Service Co-Op Graph和協力廠商圖的角色。

>[!IMPORTANT]
>
> 概率私用圖表仍在開發中，並設定稍後發佈。

>[!VIDEO](https://video.tv.adobe.com/v/27841?quality=12&learn=on)

### 身分名稱空間

當您的客戶在多個通道（包括網路、行動應用程式、客服中心或店面）與您的品牌互動時，如果您無法跨通道觀察和追蹤他們的活動，就很難瞭解並提供服務。

透過不同的裝置和通道瞭解客戶，首先要在每個通道中識別客戶。 Adobe Experience Platform透過使用身分名稱空間來實現此目標。
身分命名空間是用於提供資料來源之上下文的識別碼，例如裝置ID或電子郵件ID。 身分名稱空間可用來尋找或連結個別身分，並提供身分值的上下文，以避免資料衝突。 例如，ID &quot;123456&quot;可能是指電子商務系統中的一個人，以及服務台系統中的另一人。 如需詳細資訊，請參閱 [身分命名空間概觀](./namespaces.md)。

### 身分圖

身分圖是不同身分名稱空間之間關係的地圖，提供您視覺化的呈現方式，說明客戶如何透過不同通道與您的品牌互動。

所有客戶識別圖表都會以近乎即時的 [!DNL Identity Service] 方式共同管理和更新，以回應客戶活動。

[!DNL Identity Service] 管理僅由您的組織可見的識別圖形，並根據您的資料（稱為專用圖形）建立。 [!DNL Identity Service] 當收錄的資料記錄包含多個身分時，增加您的私人圖表，並在找到的身分之間新增關係。

例如，使用電話號碼（例如「工作電話」）可能會產生比您想要在身分圖表中建立的關係，以說明提供及標示身分資料時要考慮的潛在因素類型。 您可能會發現許多員工在工作時都使用相同的號碼，而「家」和「行動」更能確保關係盡可能精確。

## 提供身分資料至 [!DNL Identity Service]

本節說明在為每個客戶建立身分圖表之前，如何處理提供給Adobe Experience Platform [!DNL Identity Service] 的資料。

### 決定身分欄位

根據您的企業資料收集策略，您標示為身分的資料欄位會決定哪些資料會包含在您的身分映射中。 為了充份運用Adobe Experience Platform的優點和最全面的客戶身分，您應上傳線上和離線資料。

- 線上資料是描述線上存在與行為的資料，例如使用者名稱與電子郵件地址。

- 離線資料是指與線上存在無直接關聯的資料，例如來自CRM系統的ID。 此類資料可讓您的身分識別更健全，並支援不同系統間的資料整合。

### 建立其他身分名稱空間

雖然 [!DNL Experience Platform] 提供多種標準名稱空間，但您可能需要建立其他名稱空間，以正確分類您的身分。 如需詳細資訊，請參閱識別名稱空 [間概觀中有關檢視和建立組織名稱空間](./namespaces.md) 的章節。

>[!NOTE]
>
>身份名稱空間是身份的限定詞。 因此，命名空間一旦建立後，便無法刪除。

### 在(XDM)中包 [!DNL Experience Data Model] 含身分資料

作為組織客戶資料的 [!DNL Platform] 標準化框架， [!DNL Experience Data Model] (XDM)允許在與其他服務互動時，共 [!DNL Experience Platform] 用和瞭解資料 [!DNL Platform]。 如需詳細資訊，請參閱 [XDM系統概觀](../xdm/home.md)。

記錄和時間序列模式都提供了包含身份資料的方法。 當擷取資料時，如果發現不同名稱空間的資料片段共用共同身分資料，則識別圖會在它們之間建立新的關係。

### 將XDM欄位標示為身分

架構中實作記 `string` 錄或時間序列XDM類的任何類型欄位都可以標籤為標識欄位。 因此，所有納入該欄位的資料都會視為身分資料。

如果身分欄位共用共同的PII資料，也允許連結身分。
例如，將電話號碼欄位標示為身分欄位， [!DNL Identity Service] 即可自動繪製與其他使用相同電話號碼之個人的關係圖。

>[!NOTE]
>
>在標籤欄位時，會提供產生的身分名稱空間。

### 設定資料集 [!DNL Identity Service]

在串流擷取程式中，自 [!DNL Identity Service ]動從記錄和時間序列資料擷取身分資料。 但是，在可以吸收資料之前，必須先啟用資料 [!DNL Identity Service]。 如需詳細資 [訊，請參閱使用API為即時客戶個人檔案和身分服務設定資料集的教學課程](../profile/tutorials/dataset-configuration.md) 。

### 將資料內嵌至 [!DNL Identity Service]

[!DNL Identity Service] 使用批次擷取或串流擷取 [!DNL Experience Platform] 傳送至 [的XDM相](../ingestion/batch-ingestion/overview.md) 容資料 [](../ingestion/streaming-ingestion/overview.md)。

以下視訊旨在支援您對Identity Service的瞭解。 此影片示範如何將資料欄位標示為身分、擷取身分資料，然後確認資料已傳至Adobe Experience Platform Identity Service私用圖表。

>[!WARNING]
>
> 下 [!DNL Platform] 列視訊中顯示的UI已過時。 請參閱檔案以取得最新的UI螢幕擷取和功能。

>[!VIDEO](https://video.tv.adobe.com/v/28167?quality=12&learn=on)

## 資料治理

Adobe Experience Platform是以隱私權為考量而建立，並包含資料治理架構，以保護客戶PII資料。 「電子郵件」或「電話」名稱空間下的身分資料預設會加密，但為了確保機密資料在保存前已加密，資料使用標籤可在收到資料時或傳入資料時套用至資料 [!DNL Platform]。 如需詳細資訊，請閱讀資 [料治理概觀](../data-governance/home.md)。

## 後續步驟

現在，您已瞭解其中的 [!DNL Identity Service] 主要概念及其角色 [!DNL Experience Platform]，可以開始學習如何使用 [[!DNL Identity Service API]使用身分圖表](./api/getting-started.md)。
