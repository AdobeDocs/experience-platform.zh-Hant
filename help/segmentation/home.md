---
keywords: Experience Platform;home;popular topics;segmentation;Segmentation;segment service;segment;Segment;Segments;segments
solution: Experience Platform
title: Adobe Experience Platform細分服務
topic: overview
description: 本檔案概述區段服務及其在Adobe Experience Platform中所扮演的角色。
translation-type: tm+mt
source-git-commit: 8f7ce97cdefd4fe79cb806e71e12e936caca3774
workflow-type: tm+mt
source-wordcount: '1991'
ht-degree: 0%

---


# Adobe Experience Platform [!DNL Segmentation Service] overview

Adobe Experience Platform提 [!DNL Segmentation Service] 供使用者介面和REST風格的API，讓您從資料中建立細分並產生受 [!DNL Real-time Customer Profile] 眾。 這些區段是集中設定和維護的， [!DNL Platform]任何Adobe解決方案都可輕鬆存取。

本檔案概述其在Adobe [!DNL Segmentation Service] Experience Platform中所扮演的角色。

## Getting started with [!DNL Segmentation Service]

請務必瞭解本檔案中使用的下列主要術語：

- **區段**:將大量個人（例如客戶、潛在客戶、使用者或組織）分成具有相似特性且回應類似行銷策略的較小群組。
- **區段定義**:用於描述目標對象的關鍵特性或行為的規則集。 概念化後，區段定義中概述的規則會用來決定區段的合格讀者成員。
- **觀眾**:符合區段定義條件的結果描述檔集。

## 區段的運作方式

區段是定義描述檔商店中描述檔子集所共用的特定屬性或行為，以區分適銷人員群組和客戶群的程式。 例如，在名為「您忘記購買運動鞋嗎？」的電子郵件促銷活動中，您可能希望擁有在過去30天內搜尋跑鞋但未完成購買的所有使用者的觀眾。

在概念上定義區段後，就會內建區段 [!DNL Experience Platform]。 通常，區段是由行銷人員或受眾專員建立，但有些組織希望由行銷部門與資料分析人員共同建立。 在檢視要傳送至的資料時 [!DNL Platform]，資料分析人員會選擇將用來建立區段規則或條件的欄位和值，以建立區段定義。 這是使用UI或API來完成的。

## 建立區段

無論是使用API建立還是使用， [!DNL Segment Builder]區段最終都會使用( [!DNL Profile Query Language] PQL)定義。 在此處，概念區段定義會以擷取符合標準的描述檔所建立的語言加以說明。 有關詳細資訊，請參 [見PQL概述](./pql/overview.md)。

若要瞭解如何在（的UI實作）中建 [!DNL Segment Builder] 立和使用區段，請參 [!DNL Segmentation Service]閱區段產 [生器指南](./ui/overview.md)。

如需使用API建立區段定義的詳細資訊，請參閱使用API [建立觀眾區段的教學課程](./tutorials/create-a-segment.md)。

>[!NOTE]
>
>在模式被擴展時，所有以後的上載都必須相應地更新新添加的欄位。 如需自訂(XDM)的 [!DNL Experience Data Model] 詳細資訊，請造訪 [架構編輯器教學課程](../xdm/tutorials/create-schema-ui.md)。

## 評估區段

### 串流區段

串流區段是持續不斷的資料選擇程式，可因應使用者活動而更新區段。 建立並儲存區段後，區段定義會套用至的傳入資料 [!DNL Real-time Customer Profile]。 區段新增和移除作業會定期處理，確保目標受眾保持相關性。

若要進一步瞭解串流區段，請閱讀串流 [區段檔案](./api/streaming-segmentation.md)。

### 批次分段

作為持續資料選擇程式的替代選擇，批次分段會透過區段定義一次移動所有描述檔資料，以產生對應的觀眾。 建立後，會儲存此區段，以便匯出以供使用。

若要瞭解如何評估區段，請參閱區 [段評估教學課程](./tutorials/evaluate-a-segment.md)。

## 存取區段結果

若要瞭解如何存取匯出的區段，請參閱區段 [評估教學課程](./tutorials/evaluate-a-segment.md)。

## 區段中繼資料

區段中繼資料可協助您在任何區段重複使用及／或組合時建立索引。

合成區段(透過API或 [!DNL Segment Builder])需要您定義區段名稱並合併原則。

### 區段名稱

建立新區段時，您必須提供區段名稱。 區段名稱可用來識別由建立之系列中的特定區段 [!DNL Segmentation Service]。 因此，區段名稱應具有說明性、簡明和獨特性。

>[!NOTE]
>
>在規劃區段時，請記住，區段可從任何其他區段參考，並與之結合。 選取名稱時，請考慮您的群體可能包含可重複使用的部分。

### 合併原則

合併策略是用於確定在 [!DNL Profile] 特定條件下如何將資料按優先順序排列並合併為統一視圖的規則。
如果未定義合併策略，則使用默 [!DNL Platform] 認的合併策略。 如果您想要使用組織專屬的合併原則，可以建立自己的合併原則，並將其標示為組織的預設值。

有關合併策略的詳細資訊，請參閱合 [並策略指南](../profile/api/merge-policies.md)。

>[!NOTE]
>
>觀眾人數的估計是根據組織的預設描述檔合併原則。

### 其他區段中繼資料

除了區段名稱和合併原則外， [!DNL Segment Builder] 還提供您額外的「區段說明」中繼資料欄位，您可在此欄位摘要區段定義的用途。

## 進階細分功能

可將區段設定為結合串流資料擷取與下列任何進階區段功能， [持續產生觀眾](../ingestion/streaming-ingestion/overview.md) :
- [循序分段](#sequential)
- [動態細分](#dynamic)
- [多實體分段](#multi-entity)

以下幾節將更詳細地討論這些進階功能。

## 循序分段 {#sequential}

標準的使用者歷程在本質上是循序的。 Adobe Experience Platform可讓您定義一系列有序的細分，以反映此歷程，從而在事件發生時捕捉事件序列。 您可以使用中的視覺化事件時間軸，依所需順序排列事件 [!DNL Segment Builder]。

需要循序劃分的客戶歷程範例包括產品檢視>產品新增>結帳>無購買。

## 動態細分 {#dynamic}

動態細分可解決行銷人員在建立行銷宣傳的細分時，傳統上所面臨的可擴充性問題。

與靜態分段不同，動態分段需要明確且重複擷取每個可能的使用案例，動態分段使用變數來建立規則邏輯並動態表達關係。

### 使用案例：尋找在家庭以外購買的客戶

為了說明此進階細分功能的價值，請考慮由資料架構師與行銷人員協作，以識別在其祖國以外進行採購的客戶。

**問題**

靜態區段需要您先定義具有唯一首頁狀態屬性的個別區段，然後再篩選不等於首頁狀態的購買事件。 此類型的明確區段會是「我在尋找來自猶他州的人，他們購買的州並非猶他州」。 使用此方法建立觀眾時，您必須為每個美國州定義一個區段，共50個區段。

由於不同的區段組合不可避免地會隨著您的縮放而產生，因此靜態區段所需的手動程式變得更耗時，降低整體效率。

**解決方案**

透過將變數指派至購買狀態屬性，您的動態區段可簡化為「在購買狀態不等於客戶首頁狀態的情況下尋找購買」。 如此可讓您將50個靜態區段合併為單一動態區段。

## 多實體分段 {#multi-entity}

透過進階的多實體分段功能，您可以使用多個XDM類別來建立區段，從而為人員結構描述新增擴充功能。 因此，在區段定 [!DNL Segmentation Service] 義期間，可以存取其他欄位，就像這些欄位是描述檔資料儲存的原生欄位。

多實體細分提供根據業務需求相關資料識別受眾所需的彈性。 此程式可以快速、輕鬆地完成，而不需要查詢資料庫的專業知識。 這可讓您將關鍵資料新增至區段，而不需對資料串流進行昂貴的變更，或等待後端資料合併。

以下影片旨在支援您對多實體分段的瞭解，並概述多實體分段和分段內容（分段負載）。

>[!VIDEO](https://video.tv.adobe.com/v/28947?quality=12&learn=on)

### 使用案例：價格驅動促銷

為了說明此進階細分功能的價值，請考慮由資料架構師與行銷人員協作。

在此示例中，資料架構師使用鍵將個人(由具有和作為其基本類的方案 [!DNL XDM Individual Profile][!DNL XDM ExperienceEvent] 組成)的資料連接到另一個類。 加入後，資料架構師或行銷人員可以在區段定義期間使用這些新欄位，就像這些欄位是基本類別架構的原生欄位。

**問題**

資料架構設計人員和行銷人員都適用於相同的服裝零售商。 這家零售商在北美地區擁有超過1,000家門店，並在產品生命週期中定期降低產品價格。 因此，行銷人員想要執行特殊促銷活動，讓購買這些商品的購物者有機會以折扣價格購買這些商品。

資料架構師的資源包括存取客戶瀏覽的網頁資料，以及包含產品SKU識別碼的購物車新增資料。 此外，他們還可以存取個別的「產品」類別，儲存其他產品資訊（包括產品價格）。 他們的指引是關注在過去14天內將產品加入購物車但並未購買產品的客戶，因為此產品的價格已經下跌。

**解決方案**

>[!NOTE]
>
>在此範例中，我們假設資料架構師已建立ID命名空間。

使用API，資料架構師會將架構的金鑰 [!DNL ExperienceEvent] 與「產品」類別建立關聯。 這樣做可讓資料架構師使用「產品」類別中的其他欄位，就像這些欄位是架構的原生欄 [!DNL ExperienceEvent] 位。 作為配置工作的最後一步，資料架構師需要將適當的資料引入配置工作中 [!DNL Real-time Customer Profile]。 若要這麼做，請啟用「產品」資料集以搭配使用 [!DNL Profile]。 在設定工作完成後，資料架構人員或行銷人員都可在中建立目標區段 [!DNL Segment Builder]。

請參閱 [架構構成概述](../xdm/schema/composition.md#union) ，瞭解如何定義跨XDM類的關係。

<!-- ## Personalization payload

Segments can now carry a payload of contextual details to enable deep personalization of Adobe Solutions as well as external non-Adobe applications. These payloads can be added while defining your target segment.

With contextual data built into the segment itself, this advanced Segmentation Service feature allows you to better connect with your customer.

Segment Payload helps you answer questions surrounding your customer’s frame of reference such as:
- What: What product was purchased? What product should be recommended next?
- When: At what time and date did the purchase occur?
- Where: In which store or city did the customer make their purchase?

While this solution does not change the binary nature of segment membership, it does add additional context to each profile through an associated segment membership object. Each segment membership object has the capacity to include three kinds of contextual data:

- **Identifier**: this is the ID for the segment 
- **Attributes**: this would include information about the segment ID such as last qualification time, XDM version, status and so on.
- **Event data**: Specific aspects of experience events which resulted in the profile qualifying for the segment

Adding this specific data to the segment itself allows execution engines to personalize the experience for the customers in their target audience. -->

### 使用個案

為了說明此進階分段功能的價值，請考慮三個標準使用案例，以說明在「分段裝載」增強功能之前，行銷應用程式所面臨的挑戰：
- 電子郵件個人化
- 電子郵件重新定位
- 廣告重新定位

**電子郵件個人化**

建立電子郵件促銷活動的行銷人員可能會嘗試在過去三個月內使用最近的客戶商店購買來建立目標對象的區段。 理想情況下，此區段同時需要進行購買之商店的項目名稱和名稱。 在增強功能之前，挑戰在於從購買事件中擷取商店識別碼，並將它指派給該客戶的個人檔案。

**電子郵件重新定位**

針對「購物車放棄」的電子郵件促銷活動建立和限定細分通常很複雜。 在進行增強之前，由於需要的資料可供使用，所以很難知道要將哪些產品加入個人化訊息中。 放棄產品的資料與體驗事件有關，而體驗事件過去在監控及擷取資料方面十分困難。

**廣告重新定位**

行銷人員面臨的另一個傳統挑戰，是建立廣告以重新鎖定已放棄購物車項目的客戶。 雖然區段定義可解決此項挑戰，但在增強功能之前，並沒有正式的方法來區分購買的產品與放棄的產品。 現在，您可以在區段定義期間鎖定特定資料集。

## [!DNL Segmentation Service] 資料類型

[!DNL Segmentation Service] 支援多種資料類型，包括：

- 字串
- 統一資源標識符
- Enum
- 數字
- 長
- 整數
- 簡短
- 位元組
- 布林值
- 日期
- 日期時間
- 陣列
- 物件
- 地圖
- 事件
- 外部受眾
- 區段

有關這些支援資料類型的詳細資訊，請參閱支援的資 [料類型檔案](./data-types.md)。

## 後續步驟

[!DNL Segmentation Service] 提供整合的工作流程，從資料建立區 [!DNL Real-time Customer Profile] 段。 總之：

- [!DNL Segmentation] 是從描述檔商店定義描述檔子集的程式，可讓您描述所需有價群組的行為或屬性。 [!DNL Segmentation Service] 使這個過程成為可能。
- 規劃區段時，請記住，區段可從任何其他區段參考，並與之結合。
- 您可以根據描述檔資料、相關時間系列資料或兩者，從規則建立區段。
- 區段可依需求或持續評估。 在隨選評估時，所有描述檔資料都會一次傳遞至區段定義。 持續評估時，資料流會在資料流進入區段定義時 [!DNL Platform]。

若要瞭解如何在UI中定義區段，請參閱「區 [段產生器」指南](./ui/overview.md)。 如需使用API建立區段定義的詳細資訊，請參閱使用API [建立區段的教學課程](./tutorials/create-a-segment.md)。