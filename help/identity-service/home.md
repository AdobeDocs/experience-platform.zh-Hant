---
keywords: Experience Platform；首頁；熱門主題；身份；XDM圖形；身份服務；身份服務
solution: Experience Platform
title: Identity Service概述
description: Adobe Experience Platform身份服務通過跨設備和系統橋接身份，幫助您更好地瞭解客戶及其行為，讓您能夠即時提供有影響的個人數字型驗。
exl-id: a22dc3f0-3b7d-4060-af3f-fe4963b45f18
source-git-commit: ad9fb0bcc7bca55da432c72adc94d49e3c63ad6e
workflow-type: tm+mt
source-wordcount: '1839'
ht-degree: 8%

---

# [!DNL Identity Service] 概覽

提供相關數字型驗需要全面瞭解您的客戶。 當您的客戶資料分散在不同的系統中，導致每個客戶都顯示有多個「身份」時，這就變得更加困難了。

Adobe Experience Platform身份服務通過跨設備和系統橋接身份，讓您能夠全面瞭解客戶及其行為，讓您能夠即時提供有影響的個人數字型驗。

與 [!DNL Identity Service]，您可以：

- 確保您的客戶通過每次交互獲得一致、個性化和相關的體驗。
- 將不同來源的多種不同身份組合在一起，並建立您客戶的全面視圖。
- 利用標識圖來映射不同的標識命名空間，為您提供了客戶如何通過不同渠道與您的品牌進行交互的直觀表示。

## 快速入門

在深入瞭解 [!DNL Identity Service]以下是關鍵術語的簡要摘要：

| 詞語 | 定義 |
| --- | --- |
| 身分 | 身分是實體 (通常為個人) 專屬的資料。諸如登錄ID、ECID或會員ID等標識也稱為「已知標識」。 |
| ECID | Experience CloudID(ECID)是跨Experience Platform和Adobe Experience Cloud應用程式使用的共用標識命名空間。 ECID為客戶身份提供了基礎，用作設備的主ID和身份圖的基節點。 查看 [ECID概述](./ecid.md) 的子菜單。 |
| 標識命名空間 | 身分識別命名空間用於區分身分識別的內容或類型。例如，身分識別會將「name<span>@email.com」區分為電子郵件地址或將「443522」區分為數值的 CRM ID。標識命名空間用於查找單個標識並提供標識值的上下文。 這允許您確定 [!DNL Profile] 包含不同主ID但共用相同值的片段 `email` 標識名稱空間實際上是同一個個體。 查看 [標識命名空間概述](./namespaces.md) 的子菜單。 |
| 識別圖 | 身份圖是不同身份之間關係的映射，使您能夠直觀顯示並更好地瞭解哪些客戶身份被拼合在一起，以及如何拼合。 請參閱上的教程 [使用標識圖形查看器](./ui/identity-graph-viewer.md) 的子菜單。 |
| 個人身份資訊(PII) | PII是可直接識別客戶的資訊，如電子郵件地址或電話號碼。 PII值通常用於匹配。 客戶在不同系統間的多重身份。 |
| 未知或匿名身份 | 未知或匿名身份是指在不識別使用設備的實際人員的情況下隔離設備的指示器。 未知和匿名身份包括訪問者的IP地址和cookie ID等資訊。 儘管未知和匿名身份可以提供行為資料，但在客戶提供其PII之前，這些身份是有限的。 |

## 什麼是 [!DNL Identity Service]？

每天，客戶都會與您的企業進行互動，並與您的品牌建立不斷增長的關係。 典型的客戶可能在您組織的資料基礎架構中的任意數量系統中處於活動狀態，例如您的電子商務、忠誠度和服務台系統。 同一客戶也可以在任意數量的設備上匿名接洽。 [!DNL Identity Service] 允許您將客戶的完整圖片拼湊起來，聚合相關資料，否則這些資料可能會分散到不同的系統中。

以消費者與品牌關係的日常示例為例：

- 瑪麗在你的電子商務網站上有一個帳戶，她過去在那裡已經完成了一些訂單。 她通常使用個人筆記型電腦購物，每次都在那裡登錄。 然而，在一次探訪中，她用平板電腦購買涼鞋，但沒有訂單，也沒有登錄。
- 此時，Mary的活動將顯示為兩個單獨的配置檔案：
   - 她的電子商務登錄名
   - 她的平板電腦設備，可能通過設備ID識別
- 瑪麗後來在訂閱您的通訊時繼續其平板電腦會話並提供電子郵件地址。 在這樣做後，流式攝取會增加一個新的身份，作為她個人資料中的記錄資料。 因此， [!DNL Identity Service] 現在，瑪麗的平板電腦活動與她的電子商務賬戶歷史有關。
- 下次點擊她的平板電腦時，你的目標內容可能反映瑪麗的完整形象和歷史，而不僅僅是一個不知名購物者使用的平板電腦。

![平台上的身份拼接](./images/identity-service-stitching.png)

實際上， [!DNL Identity Service] 允許您將客戶的完整圖片拼湊起來，聚合相關資料，否則這些資料可能會分散到不同的系統中。 身份關係 [!DNL Identity Service] 「即時客戶配置檔案」利用定義和維護功能來構建客戶及其與您品牌的交互的完整畫面。 有關詳細資訊，請參見 [即時客戶概要資訊概述](../profile/home.md)。

### 使用案例

示例 [!DNL Identity Service] 實現包括：

- 電信公司可以依賴「電話號碼」值，即電話號碼是指線下和線上資料集中感興趣的同一個人。
- 由於匿名訪問者的高百分比，零售公司可以在離線資料集中使用「電子郵件地址」，在線上資料集中使用ECID。
- 銀行可能更喜歡離線資料集中的「帳號」，如分行交易。 它們可能依賴於線上資料集中的「登錄ID」，因為大多數訪問者在訪問期間都會經過身份驗證。
- 您的客戶也可能具有唯一的專有ID，如GUID或其他通用唯一標識符。

## 標識命名空間 {#identity-namespace}

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

如果你問一個人&quot;你的身份是什麼？&quot; 如果沒有進一步的背景，他們很難提供有用的答案。 根據同一邏輯，表示身份值的字串值（無論是系統生成的ID還是電子郵件地址）僅在提供給字串值上下文的限定符時完成：標識命名空間。

您的客戶可能通過線上和離線渠道的組合與您的品牌進行互動，這就帶來了如何將這些分散的互動協調為單個客戶身份的難題。

通過多個設備和渠道瞭解客戶，首先要在每個渠道中識別他們。 平台通過使用標識命名空間來實現這一點。 標識名稱空間是用於為客戶標識提供附加上下文的標識符，如電子郵件或電話。 標識命名空間用於查找或連結單個標識並提供標識值的上下文。 查看 [標識命名空間概述](./namespaces.md) 的子菜單。

## 標識圖

標識圖是不同標識命名空間之間關係的映射，使您能夠直觀地顯示和更好地瞭解將哪些客戶標識縫合在一起，以及如何縫合。 請參閱上的教程 [使用標識圖形查看器](./ui/identity-graph-viewer.md) 的子菜單。

以下視頻旨在支援您對身份和身份圖形的理解。

>[!VIDEO](https://video.tv.adobe.com/v/27841?quality=12&learn=on)

## 向提供身份資料 [!DNL Identity Service]

本節介紹在Adobe Experience Platform使用之前如何處理提供給 [!DNL Identity Service] 為每個客戶構建身份圖。

### 確定標識欄位

根據企業資料收集策略，您標籤為標識的資料欄位將確定標識映射中包含哪些資料。 為了最大限度地利用Adobe Experience Platform和盡可能最全面的客戶身份資訊，您應上載線上和離線資料。

- 線上資料是描述線上狀態和行為的資料，如用戶名和電子郵件地址。

- 離線資料是指與線上狀態（如CRM系統的ID）不直接相關的資料。 此類資料使您的身份更加強健，並支援跨不同系統的資料聚合。

### 建立其他標識命名空間

雖然Experience Platform提供了多種標準命名空間，但您可能需要建立其他命名空間以正確地對標識進行分類。 有關詳細資訊，請參閱 [查看和建立組織的命名空間](./namespaces.md) 標識名稱空間概述中。

>[!NOTE]
>
>標識名稱空間是標識的限定符。 因此，一旦建立了命名空間，就無法刪除該命名空間。

### 在中包含標識資料 [!DNL Experience Data Model] (XDM)

作為標準化框架 [!DNL Platform] 組織客戶資料， [!DNL Experience Data Model] (XDM)允許跨Experience Platform和與之交互的其他服務共用和理解資料 [!DNL Platform]。 有關詳細資訊，請參閱 [XDM系統概述](../xdm/home.md)。

記錄模式和時間序列模式都提供了包括身份資料的方法。 當資料被攝取時，如果發現來自不同命名空間的資料片段共用公共身份資料，則標識圖將在它們之間建立新關係。

### 將XDM欄位標籤為標識

任何類型的欄位 `string` 在實現記錄或時間序列XDM類的方案中，可將其標籤為標識欄位。 因此，所有輸入到該欄位的資料都將被視為身份資料。

>[!NOTE]
>
>不支援陣列和映射類型欄位，因此不能將其標籤和標籤為標識欄位。

如果標識欄位共用公共PII資料，則還允許標識連結。
例如，通過將電話號碼欄位標籤為身份欄位， [!DNL Identity Service] 自動繪製與發現使用相同電話號碼的其他個人的關係的圖形。

>[!NOTE]
>
>在標籤欄位時提供結果標識的命名空間。

### 為 [!DNL Identity Service]

在流攝入過程中， [!DNL Identity Service ]自動從記錄和時間序列資料中提取身份資料。 但是，在接收資料之前，必須為 [!DNL Identity Service]。 請參閱上的教程  [使用API為Real-Time Customer Profile和Identity Service配置資料集](../profile/tutorials/dataset-configuration.md) 的子菜單。

### 將資料接收到 [!DNL Identity Service]

[!DNL Identity Service] 使用發送到Experience Platform的符合XDM的資料 [批處理](../ingestion/batch-ingestion/overview.md) 或 [流式處理](../ingestion/streaming-ingestion/overview.md)。

以下視頻旨在支援您對Identity Service的理解。 此視頻顯示如何將資料欄位標籤為身份，接收身份資料，然後驗證資料是否已傳到Adobe Experience Platform身份服務專用圖。

>[!WARNING]
>
>的 [!DNL Platform] 以下視頻中顯示的UI已過期。 有關最新的UI螢幕截圖和功能，請參閱文檔。

>[!VIDEO](https://video.tv.adobe.com/v/28167?quality=12&learn=on)

## 資料治理

Adobe Experience Platform是在考慮隱私的情況下構建的，它包括一個資料治理框架以保護您的客戶PII資料。 預設情況下，「電子郵件」或「電話」命名空間下的標識資料是加密的，但為確保敏感資料在保留之前被加密，資料使用標籤可以在資料被接收時或資料到達時應用到資料 [!DNL Platform]。 有關詳細資訊，請閱讀 [資料治理概述](../data-governance/home.md)。

## 後續步驟

既然你瞭解了 [!DNL Identity Service] 以及它在Experience Platform中的作用，您可以開始學習如何使用您的身份圖 [[!DNL Identity Service API]](./api/getting-started.md)。
