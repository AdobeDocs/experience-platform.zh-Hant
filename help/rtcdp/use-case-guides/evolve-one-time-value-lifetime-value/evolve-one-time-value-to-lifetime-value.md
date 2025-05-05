---
title: 將一次性客戶價值提升至期限價值
description: 瞭解如何建立個人化行銷活動，以根據特定客戶的屬性、行為和過去購買提供最佳補充性產品或服務。
feature: Use Cases
exl-id: 45f72b5e-a63b-44ac-a186-28bac9cdd442
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '3181'
ht-degree: 26%

---

# 將一次性客戶價值提升至期限價值

>[!IMPORTANT]
> 
>* 本頁提供Real-Time CDP和Adobe Journey Optimizer的實作範例，以達成上述使用案例。 使用頁面上提供的圖、資格標準和其他欄位作為指南，而不是規範圖。
>* 若要完成此使用案例，您需要取得Real-Time CDP和Adobe Journey Optimizer的授權。 請閱讀下方[先決條件和規劃區段](#prerequisites-and-planning)的詳細資訊。

實施一次性客戶價值至終身價值的使用案例，以提高品牌參與度和品牌忠誠度。 運用Experience Platform的強大功能，並加上[Real-Time CDP](/help/rtcdp/home.md)和[Journey Optimizer](https://experienceleague.adobe.com/zh-hant/docs/journey-optimizer/using/ajo-home)，在多個管道或歷程上建立連線的客戶體驗。

您鎖定的角色是您屬性中不常見的訪客，這些訪客在過去三個月中進行了一些購買。

考慮這些造訪您屬性並偶爾購買您所提供產品或服務的客戶。 您可能會想要建立個人化行銷活動來吸引這些客戶，讓您的品牌可以為他們提供較長期的價值，而非一次性價值。 瞭解如何：

* 收集和管理資料
* 建立對象
* 建立歷程以在Adobe Journey Optimizer中鎖定這些對象，並在Real-Time CDP中啟用它們。

![逐步將一次性值演變成期限值高階視覺化概觀。](../evolve-one-time-value-lifetime-value/images/diagram-business-use-case.png){zoomable="yes"}

## 必要條件和規劃 {#prerequisites-and-planning}

考量到您已在內部定義業務目標和目標，以提高品牌忠誠度。 這可以轉換為執行使用案例，以提高客戶參與度和忠誠度。

為此，所需的技術包含兩個Experience Platform應用程式[Real-Time CDP](https://experienceleague.adobe.com/docs/experience-platform/rtcdp/overview.html?lang=zh-Hant)和[Adobe Journey Optimizer](https://experienceleague.adobe.com/docs/journey-optimizer/using/get-started/get-started.html?lang=zh-Hant)。 以下列出您在實作使用案例時將使用的兩個應用程式的各種功能和UI元素。

>[!TIP]
>
>確保您擁有所有這些區域所需的[屬性型存取控制權限](/help/access-control/abac/end-to-end-guide.md)，或要求系統管理員授予您必要的權限。

* [[!DNL Adobe Real-Time Customer Data Platform (Real-Time CDP)]](https://experienceleague.adobe.com/docs/platform-learn/tutorials/rtcdp/understanding-the-real-time-customer-data-platform.html?lang=zh-Hant)：整合跨資料來源的資料，以推動行銷活動。 然後，使用此資料來建立行銷活動客群，並呈現用於電子郵件和網頁促銷圖磚的個人化資料元素 (例如姓名或帳戶相關資訊)。最後，Real-Time CDP也可用來啟用付費媒體目的地的受眾。
   * [結構描述](/help/xdm/home.md)
   * [輪廓](/help/profile/home.md)
   * [資料集](/help/catalog/datasets/overview.md)
   * [客群](/help/segmentation/home.md)
   * [目標](/help/destinations/home.md)
* [[!DNL Adobe Journey Optimizer]](https://experienceleague.adobe.com/docs/journey-optimizer/using/orchestrate-journeys/journey.html?lang=zh-Hant)：設計歷程、設定觸發器，並建立正確的訊息以回應您的訪客。
   * [事件或客群觸發](https://experienceleague.adobe.com/docs/journey-optimizer/using/offer-decisioning/collect-event-data/data-collection.html?lang=zh-Hant)
   * [對象和活動](https://experienceleague.adobe.com/docs/journey-optimizer/using/audiences-profiles-identities/audiences/about-audiences.html?lang=zh-Hant)
   * [歷程](https://experienceleague.adobe.com/docs/journey-optimizer/using/orchestrate-journeys/journey.html?lang=zh-Hant)

## Real-Time CDP和Journey Optimizer架構

以下是Real-Time CDP和Journey Optimizer各種元件的高階架構檢視。 此圖表顯示資料如何流經兩個Experience Platform應用程式，從資料收集到透過歷程或促銷活動啟用到目的地的時間，以達到本頁面所述的使用案例。

![架構高階視覺化概觀。](/help/rtcdp/use-case-guides/evolve-one-time-value-lifetime-value/images/architecture-diagram.png){zoomable="yes"}

## 如何實現使用案例：高層級概觀 {#achieve-the-use-case-high-level}

以下是工作流程的高層級概觀，結合歷程工作流程與啟動工作流程。

在下圖的工作流程範例中，您會尋找符合特定條件的客戶，並誘使他們返回您的網站或應用程式。 您想要在歷程中設定這些值，其中這些值會以較重複的方式傳回，而不是在您的屬性上有限的活動。 您正嘗試讓他們回到您的屬性，一旦他們回到屬性中，您就會讓他們進入歷程，在您的網站上進行週期性購買。 此處設定的行銷活動上限為每月一次與客戶的互動。

首先，請傳送訊息給高價值和低頻率客戶的對象。 然後檢查他們是否在過去三十天內收到此訊息。 如果沒有，您可以將他們輸入歷程，例如新的訂閱方案。 然後，您可以等候幾天（在此範例中是七天）。 之後，如果他們尚未購買您傳送訊息的訂閱，您可以透過目的地傳送付費媒體廣告。 如果他們已購買訂閱，您可以讓他們輸入訂單確認歷程，從而完成使用案例。

>[!IMPORTANT]
>
>如本頁進一步所述，藉由在您的結構描述中擁有[專屬的同意欄位群組](#customer-attributes-schema)以及[實作同意原則](#privacy-consent)，所有動作和工作流程都會以隱私權和同意優先的方式實作。

>[!BEGINSHADEBOX]

![逐步將一次性值演變成期限值高階視覺化概觀。](../evolve-one-time-value-lifetime-value/images/step-by-step.png){zoomable="yes"}

1. 您建立結構描述和資料集，然後為[!UICONTROL 設定檔]標籤這些資料集。
2. 系統會透過Web SDK、Mobile Edge SDK或API收集資料並整合至Experience Platform。 也可以使用 Analytics Data Connector，但可能會導致歷程延遲。
3. 您將輪廓載入到 Real-Time CDP 並建立控管原則，以確保以負責方式使用資料。
4. 您可從設定檔清單建立焦點受眾，以檢查高值和低頻率客戶。
5. 您在[!DNL Adobe Journey Optimizer]中建立兩個歷程，一個傳送訊息給使用者有關新訂閱程式的資訊，另一個則傳送訊息給他們，讓他們稍後確認購買。
6. 如有需要，您可以啟用尚未購買您訂閱之客戶受眾，並前往想要的付費媒體目的地。

>[!ENDSHADEBOX]

## 如何實現使用案例 {#achieve-use-case-instruction}

若要完成上述高階概覽中的每個步驟，請閱讀以下章節，其中提供詳細資訊和詳細指示的連結。

### 您將使用的 UI 功能和元素 {#ui-functionality-and-elements}

當您完成實施使用案例的步驟時，您將使用本檔案開頭列出的Real-Time CDP、Adobe Journey Optimizer功能和UI元素。 確保您擁有所有這些區域所需的屬性型存取控制權限，或要求系統管理員授予您必要的權限。

### 建立結構描述設計並指定欄位群組 {#schema-design}

體驗資料模型 (XDM) 資源是在 [!DNL Adobe Experience Platform] 內的[!UICONTROL 結構描述] 工作區中接受管理。您可以檢視及探索[!DNL Adobe]提供的核心資源（例如，[!UICONTROL 欄位群組]），並為您的組織建立自訂資源和結構描述。

如需深入了解如何建立[結構描述](https://experienceleague.adobe.com/docs/experience-platform/xdm/home.html?lang=zh-Hant)，請參閱[建立結構描述教學課程](/help/xdm/tutorials/create-schema-ui.md)。

在此範例實施中，您可以針對使用案例使用數個結構描述設計，以將一次性值演化為期限值。 每個結構描述都包含要設定的特定必填欄位，以及一些建議的欄位。

根據實作範例，Adobe建議您建立下列三個結構描述來完成此使用案例：

* [客戶屬性結構描述](#customer-attributes-schema) （設定檔結構描述）
* [客戶數位交易結構描述](#customer-digital-transactions-schema) （體驗事件結構描述）
* [客戶離線交易結構描述](#customer-offline-transactions-schema) （體驗事件結構描述）

#### 客戶屬性結構描述 {#customer-attributes-schema}

使用此結構描述來建構並參考構成客戶資訊的設定檔資料。 該資料通常會透過您的 CRM 或類似系統被擷取至 [!DNL Adobe Experience Platform]，並且有必要參考用來個人化、行銷同意和加強分段功能的客戶詳細資訊。

![已強調欄位群組的客戶屬性結構描述](/help/rtcdp/use-case-guides/evolve-one-time-value-lifetime-value/images/customer-attributes-schema.png)

客戶屬性結構描述以 [!UICONTROL XDM 個人輪廓]類別表示，其中包括以下欄位群組：

+++人口統計詳細資料 (欄位群組)

[人口統計詳細資料](/help/xdm/field-groups/profile/demographic-details.md)是 XDM 個人輪廓類別的標準結構描述欄位群組。此欄位群組提供根層級個人物件，其子欄位在描述個人的資訊。

+++

+++個人聯絡詳細資料 (欄位群組)

[個人聯絡詳細資訊](/help/xdm/field-groups/profile/personal-contact-details.md)是XDM個人設定檔類別的標準結構描述欄位群組，可描述個人的聯絡資訊。

+++

+++外部來源系統稽核詳細資料 (欄位群組)

[外部來源系統稽核屬性](/help/xdm/data-types/external-source-system-audit-attributes.md)是一種標準的體驗資料模式 (XDM) 資料類型，用於擷取外部來源系統的稽核詳細資料。

+++

+++同意和偏好設定欄位群組 (欄位群組)

[同意和偏好設定](/help/xdm/field-groups/profile/consents.md)欄位群組提供單一物件類型的欄位、同意，以擷取同意和偏好設定資訊。

+++

#### 客戶數位交易結構描述 {#customer-digital-transactions-schema}

此結構用於建構和參考事件資料，這些資料構成了您的網站或其他相關數位平台上發生的客戶活動。 此資料通常會透過[網頁SDK](/help/web-sdk/home.md)擷取到[!DNL Adobe Experience Platform]，且為參考各種瀏覽和轉換事件所必需，這些事件用於觸發歷程、詳細的線上客戶分析和增強的分段功能。

![反白欄位群組的客戶數位交易結構描述](/help/rtcdp/use-case-guides/evolve-one-time-value-lifetime-value/images/customer-digital-transactions-schema.png)

客戶數位交易結構描述是以 [!UICONTROL XDM ExperienceEvent] 類別表示，其中包括以下欄位群組：

+++Adobe Experience Platform Web SDK ExperienceEvent (欄位群組)

| 欄位 | 需求 |
| --- | --- |
| `device.model` | 建議 |
| `environment.browserDetails.userAgent` | 建議 |

+++

+++Web 詳細資料 (欄位群組)

[網頁詳細資料](/help/xdm/field-groups/event/web-details.md)是XDM ExperienceEvent類別的標準結構描述欄位群組，用於描述有關互動、頁面詳細資料和反向連結等網頁詳細資料事件的資訊。

+++

+++消費者體驗事件 (欄位群組)

此欄位群組包含使用者在您的Web屬性上採取的各種動作相關資訊，例如購買或瀏覽事件。

| 欄位 | 需求 |
| --- | --- |
| `commerce.cart.cartID` | 建議 |
| `commerce.cart.cartSource` | 建議 |
| `commerce.cartAbandons.id` | 建議 |
| `commerce.cartAbandons.value` | 建議 |
| `commerce.order.orderType` | 建議 |
| `commerce.order.payments.paymentAmount` | 建議 |
| `commerce.order.payments.paymentType` | 建議 |
| `commerce.order.payments.transactionID` | 建議 |
| `commerce.order.priceTotal` | 建議 |
| `commerce.order.purchaseID` | 建議 |
| `commerce.productListAdds.id` | 建議 |
| `commerce.productListAdds.value` | 建議 |
| `commerce.productListOpens.id` | 建議 |
| `commerce.productListOpens.value` | 建議 |
| `commerce.productListRemoval.id` | 建議 |
| `commerce.productListRemoval.value` | 建議 |
| `commerce.productListViews.id` | 建議 |
| `commerce.productListViews.value` | 建議 |
| `commerce.productViews.id` | 建議 |
| `commerce.productViews.value` | 建議 |
| `commerce.purchases.id` | 建議 |
| `commerce.purchases.value` | 建議 |
| `marketing.campaignGroup` | 建議 |
| `marketing.campaignName` | 建議 |
| `marketing.trackingCode` | 建議 |
| `productListItems.name` | 建議 |
| `productListItems.priceTotal` | 建議 |
| `productListItems.product` | 建議 |
| `productListItems.quantity` | 建議 |

+++

+++一般使用者 ID 詳細資料 (欄位群組)

[一般使用者ID詳細資訊](/help/xdm/field-groups/event/enduserids.md)欄位群組包含有關您使用者的各種資訊，例如造訪您的網站時他們是否經過驗證，以及有關其身分的資訊。

+++

+++外部來源系統稽核詳細資料 (欄位群組)

外部來源系統稽核屬性是一種標準體驗資料模式 (XDM) 的資料類型，這模式會擷取外部來源系統的稽核詳細資料。

+++

#### 客戶離線交易結構描述 {#customer-offline-transactions-schema}

此結構描述是用來安排和引用構成發生在您網站以外平台上客戶活動的事件資料。此資料通常會從POS （或類似系統）擷取到[!DNL Adobe Experience Platform]，且通常會透過API連線串流到Experience Platform。 閱讀[批次擷取](/help/ingestion/batch-ingestion/getting-started.md)。 其目的是引用用來觸發歷程、深度的線上和離線客戶分析以及加強分段功能的各種離線轉換事件。

![反白欄位群組的客戶離線交易結構描述](/help/rtcdp/use-case-guides/evolve-one-time-value-lifetime-value/images/customer-offline-transactions-schema.png)

客戶離線交易結構描述以 [!UICONTROL XDM ExperienceEvent] 類別示，其中包括以下欄位群組：

+++商務詳細資料 (欄位群組)

[Commerce詳細資料](/help/xdm/field-groups/event/commerce-details.md)是[!DNL XDM ExperienceEvent]類別的標準結構描述欄位群組，用於描述商業資料，例如產品資訊（SKU、名稱、數量）和標準購物車作業（訂購、結帳、捨棄）。

+++

+++個人聯絡詳細資料 (欄位群組)

[[!UICONTROL 個人連絡人詳細資料]](/help/xdm/field-groups/profile/personal-contact-details.md)是[!DNL XDM Individual Profile]類別的標準結構描述欄位群組，說明個別人員的連絡資訊。

+++

+++外部來源系統稽核詳細資料 (欄位群組)

外部來源系統稽核屬性是一種標準體驗資料模式 (XDM) 的資料類型，此模式會擷取外部來源系統的稽核詳細資料。

+++

#### Adobe Web 連接器結構描述 {#adobe-web-connector-schema}

>[!NOTE]
>
>如果您使用 [!DNL Adobe Analytics Data Connector]，這是一個實施選項。

此結構用於建構和參考事件資料，這些資料構成了您的網站或其他相關數位平台上發生的客戶活動。 此結構描述類似於「客戶數位交易」結構描述，但不同之處在於，當Web SDK不是資料收集的選項時，它可以這樣做。 因此，當您利用[!DNL Adobe Analytics Data Connector]將您的線上資料當作主要或次要資料流傳送到[!DNL Adobe Experience Platform]時，可以使用此結構描述。

![欄位群組醒目提示的Adobe Web聯結器結構描述](/help/rtcdp/use-case-guides/evolve-one-time-value-lifetime-value/images/adobe-web-schema.png)

[!DNL Adobe] Web 連接器結構描述以 [!UICONTROL XDM ExperienceEvent] 類別表示，其中包括以下欄位群組：

+++Adobe Analytics ExperienceEvent 範本 (欄位群組)

[[!UICONTROL Adobe Analytics ExperienceEvent完整擴充功能]](/help/xdm/field-groups/event/analytics-full-extension.md)是標準結構描述欄位群組，可擷取Adobe Analytics所收集的一般量度。

+++

### 從結構描述建立資料集 {#dataset-from-schema}

資料集是一組資料的儲存和管理結構。用來完成此範例實作的每個結構描述都有一個資料集。

如需深入了解如何從結構描述建立[資料集](/help/catalog/datasets/overview.md)，請參閱[資料集 UI 指南](/help/catalog/datasets/user-guide.md)。

>[!NOTE]
>
>與結構描述建立步驟類似，您需要啟用資料集以包含在即時客戶輪廓中。如需深入了解關於啟用資料集以用於即時客戶輪廓，請閱讀[建立結構描述教學課程](/help/xdm/tutorials/create-schema-ui.md#profile)。

### 隱私權、同意和資料控管 {#privacy-consent}

#### 同意原則

>[!IMPORTANT]
>
>法律規定必須讓客戶能夠取消訂閱來自品牌的通訊，以及確保遵循此選擇。 在[隱私權法規概觀](https://experienceleague.adobe.com/docs/experience-platform/privacy/regulations/overview.html?lang=zh-Hant)中，了解更多有關適用法律。

請考慮實作下列[同意原則](https://experienceleague.adobe.com/docs/platform-learn/data-collection/web-sdk/consent/overview.html?lang=zh-Hant)，並在您聯絡訪客前詢問其同意：

* 如果為 `consents.marketing.email.val = "Y"`，則可以發送電子郵件
* 如果為 `consents.marketing.sms.val = "Y"`，則可以發送簡訊
* 如果為 `consents.marketing.push.val = "Y"`，則可以推播
* 如果為 `consents.share.val = "Y"`，則可以進行廣告

#### 資料控管標籤和執行

請考慮新增並強制實行下列[資料控管標籤](/help/data-governance/labels/overview.md)：

* 個人電子郵件地址會用作直接可識別的資料，用於識別或聯絡特定個人而非裝置。
   * `personalEmail.address = I1`

#### 行銷原則

您建立的歷程不需要[行銷原則](/help/data-governance/policies/overview.md)作為此使用案例的一部分。 不過，您可以視需要考慮以下原則：

* 限制敏感資料
* 限制現場廣告
* 限制電子郵件目標定位
* 限制跨網站目標定位
* 限制將直接可識別資料與匿名資料相結合

### 建立對象 {#create-audiences}

此使用案例需要您建立兩個受眾，以定義由個人資料存放區中的個人資料子集共用的特定屬性或行為，以區分可行銷的人員群組。 在Adobe Experience Platform中可以透過多種方式建立對象：

* 如需如何建立對象的詳細資訊，請參閱[對象服務UI指南](https://experienceleague.adobe.com/docs/experience-platform/segmentation/ui/overview.html?lang=zh-Hant#create-audience)。
* 如需如何構成[對象](/help/segmentation/home.md)的相關資訊，請閱讀[對象構成UI指南](/help/segmentation/ui/audience-composition.md)。
* 如需如何透過Experience Platform衍生的區段定義來建立對象的詳細資訊，請參閱[對象產生器UI指南](/help/segmentation/ui/segment-builder.md)。

尤其是，您必須在使用案例的不同步驟中建立和使用兩個對象，如下圖所示。

![標示的對象。](/help/rtcdp/use-case-guides/evolve-one-time-value-lifetime-value/images/audiences-highlighted-in-diagram.png){zoomable="yes"}

>[!BEGINTABS]

>[!TAB Adobe Journey Optimizer合格對象]

此高值和低頻率對象包含您想要透過歷程聯絡的設定檔，以告知他們新的訂閱計畫。 對象詳細資料如下：

* 說明：過去3個月內總支出超過$250的設定檔
* 對象中需要的欄位和條件：
   * 事件： `commerce.order.payments.paymentamount`
*總和：>= $250
   * 事件型別： `commerce.purchases`
*時間戳記：不足三個月前


>[!TAB 付費媒體對象]

建立此對象時，會納入過去3個月內總計花費超過$250且過去7天內未購買過的設定檔。 對象詳細資料如下：

* 說明：過去3個月內合共花費超過$250且過去7天內未購買過的設定檔。
* 所需欄位和條件：
   * 事件型別： `journey.feedback`
      * 運算元： = true
   * 事件：`experience.journeyOrchestration.stepEvents.nodeName`
      * 運算元： = JourneyStepEventTracker — 未購買訂閱
      * 時間戳記：過去7天
   * EventType不是： `commerce.purchases`
      * 時間戳記：&lt;= 7天前（現在）
   * 活動： SKU
      * 值： = `subscription`

>[!ENDTABS]

### 歷程在 Adobe Journey Optimizer 中建立 {#journey-setup}

>[!NOTE]
>
>[!DNL Adobe Journey Optimizer] 並不涵蓋圖中顯示的所有內容。所有[付費媒體廣告](/help/destinations/catalog/social/overview.md)都是在[!UICONTROL 目的地] [工作區](/help/destinations/ui/destinations-workspace.md)中建立。

[[!DNL Adobe Journey Optimizer]](https://experienceleague.adobe.com/docs/journey-optimizer/using/orchestrate-journeys/journey.html?lang=zh-Hant) 協助您向其客戶傳送連結的、情境式和個人化體驗。客戶歷程是客戶與品牌互動的整個過程。每個使用案例歷程都需要特定資訊。

若要完成此使用案例，您必須建立兩個個別的歷程：

* 期限歷程，其中包含您傳送給高價值、低頻率客戶的訊息
* 回應您的呼叫並購買訂閱之使用者的訂單確認歷程。

![個醒目提示的歷程。](/help/rtcdp/use-case-guides/evolve-one-time-value-lifetime-value/images/journeys-highlighted-in-diagram.png){zoomable="yes"}

下面列出的是每個歷程分支所需的精確資料。

>[!BEGINTABS]

>[!TAB 期限歷程]

期限歷程針對過去30天內未鎖定的高價值與低頻率客戶的對象。 系統會向這些客戶顯示訊息，如果7天後仍未購買，您可以將非購買者納入您可向其中顯示付費媒體廣告的受眾。 如果他們確實有購買，您可以在訂單確認歷程中設定購買者，詳細資訊見個別索引標籤。

![期限歷程高階視覺化概觀。](/help/rtcdp/use-case-guides/evolve-one-time-value-lifetime-value/images/lifetime-journey.png "一次性值至期限歷程高階視覺化概觀。"){zoomable="yes"}

+++詳細歷程邏輯

上方顯示的歷程遵循下列邏輯。

1. 讀取對象：針對在上述對象區段中建立的第一個對象，使用[讀取對象活動](https://experienceleague.adobe.com/docs/journey-optimizer/using/orchestrate-journeys/about-journey-building/read-audience.html?lang=zh-Hant)。

2. 條件 — 偏好頻道：使用[條件活動](https://experienceleague.adobe.com/docs/journey-optimizer/using/orchestrate-journeys/about-journey-building/condition-activity.html?lang=zh-Hant)來決定如何透過電子郵件、簡訊或推播通知聯絡客戶。 使用三個動作活動來建立三個分支。

3. 等候：使用[等待活動](https://experienceleague.adobe.com/docs/journey-optimizer/using/orchestrate-journeys/about-journey-building/read-audience.html?lang=zh-Hant)等候，直到您接聽購買。

4. 條件 — 過去7天內的購買訂閱？：使用條件活動來監聽過去七天內的產品購買。

5. JourneyStepEventTracker — 未購買訂閱：對尚未購買訂閱的訪客使用[自訂動作](https://experienceleague.adobe.com/docs/journey-optimizer/using/orchestrate-journeys/about-journey-building/using-custom-actions.html?lang=zh-Hant)，即使收到您的訊息。 作為歷程結束時的自訂條件的一部分，請建立`journey.feedback`事件，並將其新增到根據[!UICONTROL 歷程步驟事件]結構描述的資料集。 您將使用此事件來細分尚未購買訂閱的對象，以及透過付費媒體廣告定位的對象。

+++

>[!TAB 訂購確認歷程]

訂單確認歷程聚焦於是否透過網站或行動應用程式進行購買。 客戶成功完成購買（例如與您的公司的訂閱）後，您便可以在訂單確認歷程中進行設定。

![客戶訂購確認歷程的高層次視覺概觀。](/help/rtcdp/use-case-guides/evolve-one-time-value-lifetime-value/images/order-confirmation-journey.png "客戶訂購確認歷程的高層次視覺概觀。"){zoomable="yes"}

+++歷程邏輯

在確認歷程中使用下列建議的事件、欄位和動作：

* 歷程由線上購買事件觸發
   * 結構描述：客戶數位交易
   * 欄位：
      * `EventType`
   * 條件：
      * `EventType = commerce.purchases`
      * 欄位：
         * `Commerce.purchases.id`
         * `Commerce.purchases.value`
         * `eventType`
         * `identityMap.authenticatedState`
         * `identityMap.id`
         * `identityMap.primary`
         * `productListItems.SKU`
         * `productListItems.currencyCode`
         * `productListItems.name`
         * `productListItems.priceTotal`
         * `productListItems.product`
         * `productListItems.productImageUrl`
         * `productListItems.quantity`
         * `timestamp`
         * `endUserIDs._experience.emailid.authenticatedState`
         * `endUserIDs._experience.emailid.id`
         * `endUserIDs._experience.emailid.namespace.code`
         * `_id`

+++

+++關鍵歷程邏輯

* 歷程登入邏輯
   * 訂購事件

* 條件
   * 選取「目標管道」 （您可以選取一或多個管道來擴大觸及範圍）。
      * 訂單確認本質上視為服務，因此通常不需要進行同意檢查。
      * 電子郵件
      * 推播
      * 簡訊

   * 管道內容個人化
      * 顯示訂購詳細資訊，並能以表格形式顯示產品清單。

+++

>[!ENDTABS]

如需有關在[!DNL Adobe Journey Optimizer]中建立歷程的詳細資訊，請閱讀[開始使用歷程](https://experienceleague.adobe.com/docs/journey-optimizer/using/orchestrate-journeys/journey.html?lang=zh-Hant)指南。

### 設定顯示付費媒體廣告的目的地 {#paid-media-ads}

即使您為新方案傳送訊息給某些使用者，他們也可能尚未購買您的訂閱。 等候數天後（在此範例使用案例中為7天），您可以決定向這些使用者顯示付費媒體廣告，以鼓勵他們購買您的訂閱。

針對付費媒體廣告，請使用Real-Time CDP中的目的地架構。 從許多可用的廣告目的地中選取一個，向您的客戶顯示付費媒體廣告，並將您[先前建立](#create-audiences)的付費媒體對象啟用到您選擇的目的地。 檢視可用[廣告](/help/destinations/catalog/advertising/overview.md)和[社交](/help/destinations/catalog/social/overview.md)目的地的概觀。

若要瞭解如何啟用目的地的資料(例如[交易台](/help/destinations/catalog/advertising/tradedesk.md)或[Google客戶比對](/help/destinations/catalog/advertising/google-customer-match.md))，請閱讀以下檔案：

* [建立新的目的地連線](/help/destinations/ui/connect-destination.md)
* [啟用受眾資料至串流受眾匯出目的地](/help/destinations/ui/activate-segment-streaming-destinations.md)

## 後續步驟 {#next-steps}

透過將您的低頻率和高價值使用者設定在歷程中，並向其中子集顯示付費媒體廣告，您有望將部分媒體廣告從一次性價值轉換為終身價值客戶，從而提高您的品牌忠誠度和客戶參與量度。

接下來，您可以探索Real-Time CDP支援的其他使用案例，例如[聰明地重新吸引客戶](/help/rtcdp/use-case-guides/intelligent-re-engagement/intelligent-re-engagement.md)或[在您的Web屬性上向未經驗證的使用者顯示個人化內容](/help/rtcdp/partner-data/onsite-personalization.md)。
