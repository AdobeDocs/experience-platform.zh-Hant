---
title: 智慧型重新吸引
description: 在關鍵轉換時刻提供引人注目的互聯體驗，以智慧方式重新吸引不常造訪的客戶。
source-git-commit: 79ba0e350d64f43558af9bc3c2ecd4ac13d11499
workflow-type: tm+mt
source-wordcount: '3424'
ht-degree: 56%

---

# 以智慧方式重新吸引您的客戶回訪

以聰明又負責的方式完成轉換之前，重新與放棄轉換的客戶互動。 透過體驗而不是提醒來與失效的客戶互動，以增強轉換並推動使用者端期限價值的增長。

採用即時考量，考量所有消費者品質和行為，並根據線上和離線事件提供快速的重新資格。

![逐步智慧型重新吸引的高層次視覺概觀。](../intelligent-re-engagement/images/step-by-step.png)

## 使用案例概述

您將透過重新參與歷程的範例來建構結構描述、資料集和對象。 您也會探索在中設定範例歷程所需的功能 [!DNL Adobe Journey Optimizer] 以及在目的地建立付費媒體廣告所需的使用者。 本指南使用在下列使用案例歷程中重新吸引客戶的範例：

* **重新參與歷程**  — 鎖定已放棄在網站和行動應用程式上瀏覽產品的客戶。
* **捨棄的購物車歷程**  — 鎖定已將產品放入購物車但尚未在網站和行動應用程式上購買的客戶。
* **訂單確認歷程**  — 著重於透過網站和行動應用程式進行的產品購買。

## 必要條件和規劃 {#prerequisites-and-planning}

當您完成實作使用案例的步驟時，您將使用以下 Real-Time CDP 功能和 UI 元素 (按使用順序列出)。確保您擁有所有這些區域所需的屬性型存取控制權限，或要求系統管理員授予您必要的權限。

* [[!DNL Adobe Real-Time Customer Data Platform (Real-Time CDP)]](https://experienceleague.adobe.com/docs/platform-learn/tutorials/rtcdp/understanding-the-real-time-customer-data-platform.html)  — 整合各種資料來源的資料以利行銷活動。 然後，使用此資料來建立行銷活動對象，並呈現用於電子郵件和網頁促銷圖磚的個人化資料元素 (例如姓名或帳戶相關資訊)。CDP 也用於跨電子郵件和網頁啟動對象 (透過 [!DNL Adobe Target]).
   * [架構](/help/xdm/home.md)
   * [設定檔](/help/profile/home.md)
   * [資料集](/help/catalog/datasets/overview.md)
   * [對象](/help/segmentation/home.md)
   * [[!DNL Adobe Journey Optimizer]](https://experienceleague.adobe.com/docs/journey-optimizer/using/orchestrate-journeys/journey.html)
   * [目的地](/help/destinations/home.md)
   * [事件或對象觸發](https://experienceleague.adobe.com/docs/journey-optimizer/using/offer-decisioning/collect-event-data/data-collection.html)
   * [對象/事件](https://experienceleague.adobe.com/docs/journey-optimizer/using/audiences-profiles-identities/audiences/about-audiences.html)
   * [歷程動作](https://experienceleague.adobe.com/docs/journey-optimizer/using/orchestrate-journeys/journey.html)

### 如何實現使用案例：高層級概觀 {#achieve-the-use-case-high-level}

以下是三個重新參與歷程範例的高層級概觀。

>[!BEGINTABS]

>[!TAB 重新吸引歷程]

重新參與歷程會鎖定網站和行動應用程式上放棄的產品瀏覽。 當產品被檢視但未被購買或新增到購物車時，會觸發此歷程。如果過去 24 小時內沒有新增清單，則三天後會觸發品牌吸引。<p>![客戶智慧型重新吸引歷程的高層次視覺概觀。](../intelligent-re-engagement/images/re-engagement-journey.png "客戶智慧型重新吸引歷程的高層次視覺概觀。"){width="2560" zoomable="yes"}</p>

1. 您可以建立方案和資料集，然後標籤為 [!UICONTROL 個人資料].
2. 資料會透過Web SDK、Mobile Edge SDK或API整合至Experience Platform。 也可以使用Analytics Data Connector，但可能會導致歷程延遲。
3. 您可將設定檔載入到Real-Time CDP中，並建立治理政策以確保負責任地使用。
4. 您可以從設定檔清單建立焦點對象，以檢查 **客戶** 已在過去三天進行參與。
5. 您在中建立重新參與歷程 [!DNL Adobe Journey Optimizer].
6. 如有需要，與&#x200B;**資料合作夥伴**&#x200B;協作，將對象啟動到所需付費媒體目的地。
7. [!DNL Adobe Journey Optimizer] 檢查同意並傳送設定的各種動作。

>[!TAB 捨棄購物車歷程]

捨棄的購物車歷程鎖定已放入購物車但尚未在網站和行動應用程式上購買的產品。 此外，付費媒體行銷活動也會使用此方法啟動和停止。<p>![客戶捨棄購物車歷程的高層次視覺概觀。](../intelligent-re-engagement/images/abandoned-cart-journey.png "客戶捨棄購物車歷程的高層次視覺概觀。"){width="2560" zoomable="yes"}</p>

1. 您可以建立方案和資料集，其標籤為 [!UICONTROL 個人資料].
2. 資料會透過Web SDK、Mobile Edge SDK或API整合至Experience Platform。 也可以使用Analytics Data Connector，但可能會導致歷程延遲。
3. 您可將設定檔載入到Real-Time CDP中，並建立治理政策以確保負責任地使用。
4. 您可以從設定檔清單建立焦點對象，以檢查 **客戶** 已將專案放入購物車，但尚未完成購買。 **[!UICONTROL 新增到購物車]**&#x200B;事件會啟動計時器；計時器會等待 30 分鐘，然後檢查是否有購買。如果尚未購買，則 **客戶** 新增至 **[!UICONTROL 捨棄購物車]** 對象。
5. 您在中建立捨棄的購物車歷程 [!DNL Adobe Journey Optimizer].
6. 如有需要，與&#x200B;**資料合作夥伴**&#x200B;協作，將對象啟動到所需付費媒體目的地。
7. [!DNL Adobe Journey Optimizer] 檢查同意並傳送設定的各種動作。

>[!TAB 訂購確認歷程]

訂購確認歷程著重在透過網站和行動應用程式購買的產品。<p>![客戶訂購確認歷程的高層次視覺概觀。](../intelligent-re-engagement/images/order-confirmation-journey.png "客戶訂購確認歷程的高層次視覺概觀。"){width="2560" zoomable="yes"}</p>

1. 您可以建立方案和資料集，然後標籤為 [!UICONTROL 個人資料].
2. 資料會透過Web SDK、Mobile Edge SDK或API整合至Experience Platform。 也可以使用Analytics Data Connector，但可能會導致歷程延遲。
3. 您可將設定檔載入到Real-Time CDP中，並建立治理政策以確保負責任地使用。
4. 您可在中建立確認歷程 [!DNL Adobe Journey Optimizer].
5. [!DNL Adobe Journey Optimizer] 使用偏好的管道傳送訂單確認訊息。

>[!ENDTABS]

## 如何達成使用案例 {#achieve-use-case-instruction}

要完成上述高層次概觀中的每個步驟，請閱讀以下各節中更多資訊和更詳細說明的連結。

### 您將使用的 UI 功能和元素 {#ui-functionality-and-elements}

當您完成實作使用案例的步驟時，您將使用 Real-Time CDP 功能和 UI 元素 (本文件開頭所列)。確保您擁有所有這些區域所需的屬性型存取控制權限，或要求系統管理員授予您必要的權限。

### 建立結構描述設計並指定欄位群組 {#schema-design}

Experience Data Model (XDM)資源是在以下管理： [!UICONTROL 方案] 中的工作區 [!DNL Adobe Experience Platform]. 您可以檢視並探索所提供的核心資源： [!DNL Adobe] (例如， [!UICONTROL 欄位群組])並為您的組織建立自訂資源和結構描述。

如需關於建立的詳細資訊 [結構描述](https://experienceleague.adobe.com/docs/experience-platform/xdm/home.html?lang=zh-Hant)，閱讀 [建立結構描述教學課程。](/help/xdm/tutorials/create-schema-ui.md)

重新參與使用案例使用了四個結構描述設計。 每個結構描述都需要設定特定欄位，以及一些強烈建議的欄位。

#### 客戶屬性結構描述

此結構用於建構和參考構成客戶資訊的設定檔資料。 此資料通常會內嵌至 [!DNL Adobe Experience Platform] 透過CRM或類似系統，且為參考用於個人化、行銷同意和增強細分功能的客戶詳細資料所必需。

客戶屬性結構以 [!UICONTROL XDM個別設定檔] 類別，包括下列欄位群組：

+++個人聯絡詳細資料 (欄位群組)

[個人聯絡詳細資料](/help/xdm/field-groups/profile/personal-contact-details.md)是 XDM 個人設定檔類別的標準結構描述欄位群組，主要在描述個人的聯絡資訊。

| 欄位 | 需求 | 說明 |
| --- | --- | --- |
| `mobilePhone.number` | 必要 | 個人手機號碼，用來發送 SMS。 |
| `personalEmail.address` | 必要 | 個人電子郵件地址。 |

+++

+++人口統計詳細資料 (欄位群組)

[人口統計詳細資料](/help/xdm/field-groups/profile/demographic-details.md)是 XDM 個人設定檔類別的標準結構描述欄位群組。此欄位群組提供根層級個人物件，其子欄位在描述個人的資訊。

| 欄位 | 需求 |
| --- | --- |
| `person.name.firstName` | 建議 |
| `person.name.lastName` | 建議 |

+++

+++外部來源系統稽核詳細資料 (欄位群組)

[外部來源系統稽核屬性](/help/xdm/data-types/external-source-system-audit-attributes.md)是一種標準的體驗資料模式 (XDM) 資料類型，用於擷取外部來源系統的稽核詳細資料。

+++

+++同意和偏好設定欄位群組 (欄位群組)

[同意和偏好設定](/help/xdm/field-groups//profile/consents.md)欄位群組提供單一物件類型的欄位、同意，以擷取同意和偏好設定資訊。

| 欄位 | 需求 |
| --- | --- |
| `consents.marketing.email.val` | 必要 |
| `consents.marketing.preferred` | 必要 |
| `consents.marketing.push.val` | 必要 |
| `consents.marketing.sms.val` | 必要 |
| `consents.personalize.content.val` | 必要 |
| `consents.share.val` | 必要 |

+++

+++設定檔測試詳細資料 (欄位群組)

此欄位群組用於最佳做法。

+++

#### 客戶數位交易結構描述

此結構用於建構和參考事件資料，這些資料構成了您的網站和/或相關數位平台上發生的客戶活動。 此資料通常會內嵌至 [!DNL Adobe Experience Platform] 透過Web SDK，且為參考用於觸發歷程、詳細線上客戶分析和增強細分功能的各種瀏覽和轉換事件所必需。

客戶數位交易結構描述是由 [!UICONTROL XDM ExperienceEvent] 類別，包括下列欄位群組：

+++Adobe Experience Platform Web SDK ExperienceEvent (欄位群組)

| 欄位 | 需求 |
| --- | --- |
| `device.model` | 建議 |
| `environment.browserDetails.userAgent` | 建議 |

+++

+++Web 詳細資料 (欄位群組)

Web 詳細資料是 XDM ExperienceEvent 類別的標準結構描述欄位群組，用於描述 Web 詳細資料事件的相關資訊，例如互動、頁面詳細資料和反向連結。

| 欄位 | 需求 | 說明 |
| --- | --- | --- |
| `web.webInteraction.linkClicks.id` | 建議 | 對應於互動之網頁連結或 URL 的 ID。 |
| `web.webInteraction.linkClicks.value` | 建議 | 對應於互動之網頁連結或 URL 的點擊次數。 |
| `web.webInteraction.name` | 建議 | 網頁的名稱。 |
| `web.webInteraction.URL` | 建議 | 網頁的 URL。 |
| `web.webPageDetails.name` | 建議 | 發生網頁互動的網頁名稱。 |
| `web.webPageDetails.URL` | 建議 | 發生網頁互動的網頁 URL。 |
| `web.webReferrer.URL` | 建議 | 描述網頁互動的反向連結，即訪客在目前網頁互動記錄之前所瀏覽的上一個 URL。 |

+++

+++消費者體驗事件 (欄位群組)

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

| 欄位 | 需求 | 說明 |
| --- | --- | --- |
| `endUserIDs._experience.emailid.authenticatedState` | 必要 | 一般使用者電子郵件地址 ID 驗證狀態。 |
| `endUserIDs._experience.emailid.id` | 必要 | 一般使用者電子郵件地址 ID。 |
| `endUserIDs._experience.emailid.namespace.code` | 必要 | 一般使用者電子郵件地址 ID 命名空間代碼。 |
| `endUserIDs._experience.mcid.authenticatedState` | 必要 | [!DNL Adobe] Marketing Cloud ID (MCID) 驗證狀態。MCID 現在稱為 Experience Cloud ID (ECID)。 |
| `endUserIDs._experience.mcid.id` | 必要 | [!DNL Adobe] Marketing CloudID (MCID)。 MCID 現在稱為 Experience Cloud ID (ECID)。 |
| `endUserIDs._experience.mcid.namespace.code` | 必要 | [!DNL Adobe] Marketing Cloud ID (MCID) 命名空間代碼。 |

+++

+++外部來源系統稽核詳細資料 (欄位群組)

外部來源系統稽核屬性是一種標準體驗資料模式 (XDM) 的資料類型，這模式會擷取外部來源系統的稽核詳細資料。

+++

#### 客戶離線交易結構描述

此結構用於建構和參考構成您的客戶活動（在您網站以外的平台上發生）的事件資料。 此資料通常會內嵌至 [!DNL Adobe Experience Platform] 從POS （或類似系統），且通常透過API連線串流至Platform。 其目的是參考各種離線轉換事件，這些事件用於觸發歷程、深層線上和離線客戶分析，以及增強分段功能。

客戶離線交易結構描述會以 [!UICONTROL XDM ExperienceEvent] 類別，包括下列欄位群組：

+++商務詳細資料 (欄位群組)

| 欄位 | 需求 | 說明 |
| --- | --- | --- |
| `commerce.cart.cartID` | 必要 | 購物車的 ID。 |
| `commerce.order.orderType` | 必要 | 描述產品訂購類型的物件。 |
| `commerce.order.payments.paymentAmount` | 必要 | 描述產品訂購付款金額的物件。 |
| `commerce.order.payments.paymentType` | 必要 | 描述產品訂購付款類型的物件。 |
| `commerce.order.payments.transactionID` | 必要 | 物件產品訂購交易 ID。 |
| `commerce.order.purchaseID` | 必要 | 物件產品訂單購買 ID。 |
| `productListItems.name` | 必要 | 代表客戶所選產品的項目名稱清單。 |
| `productListItems.priceTotal` | 必要 | 代表客戶所選產品的項目清單總價。 |
| `productListItems.product` | 必要 | 選取的產品。 |
| `productListItems.quantity` | 必要 | 代表客戶所選產品的項目清單數量。 |

+++

+++個人聯絡詳細資料 (欄位群組)

| 欄位 | 需求 | 說明 |
| --- | --- | --- |
| `mobilePhone.number` | 必要 | 個人手機號碼，用來發送 SMS。 |
| `personalEmail.address` | 必要 | 個人電子郵件地址。 |

+++

+++外部來源系統稽核詳細資料 (欄位群組)

外部來源系統稽核屬性是一種標準體驗資料模式 (XDM) 的資料類型，此模式會擷取外部來源系統的稽核詳細資料。

+++

#### Adobe Web 連接器結構描述

>[!NOTE]
>
>若您使用 [!DNL Adobe Analytics Data Connector].

此結構用於建構和參考事件資料，這些資料構成了您的網站和/或相關數位平台上發生的客戶活動。 此結構描述類似於「客戶數位交易」結構描述，但不同之處在於，這是為了在Web SDK不是資料收集的選項時使用；因此，當您使用時，需要此結構描述 [!DNL Adobe Analytics Data Connector] 將您的線上資料傳送到 [!DNL Adobe Experience Platform] 作為主要或次要資料流。

此 [!DNL Adobe] Web聯結器結構描述是由 [!UICONTROL XDM ExperienceEvent] 類別，包括下列欄位群組：

+++Adobe Analytics ExperienceEvent 範本 (欄位群組)

| 欄位 | 需求 | 說明 |
| --- | --- | --- |
| `web.webInteraction.linkClicks.id` | 建議 | 對應於互動之網頁連結或 URL 的 ID。 |
| `web.webInteraction.linkClicks.value` | 建議 | 對應於互動之網頁連結或 URL 的點擊次數。 |
| `web.webInteraction.name` | 建議 | 網頁的名稱。 |
| `web.webInteraction.URL` | 建議 | 網頁的 URL。 |
| `web.webPageDetails.name` | 建議 | 發生網頁互動的網頁名稱。 |
| `web.webPageDetails.URL` | 建議 | 發生網頁互動的網頁 URL。 |
| `web.webReferrer.URL` | 建議 | 描述網頁互動的反向連結，即訪客在目前網頁互動記錄之前所瀏覽的上一個 URL。 |
| `commerce.cart.cartID` | 建議 | |
| `commerce.cart.cartSource` | 建議 | |
| `commerce.cartAbandons.id` | 建議 | |
| `commerce.cartAbandons.value` | 建議 | |
| `commerce.order.orderType` | 建議 | |
| `commerce.order.payments.paymentAmount` | 建議 | |
| `commerce.order.payments.paymentType` | 建議 | |
| `commerce.order.payments.transactionID` | 建議 | |
| `commerce.order.priceTotal` | 建議 | |
| `commerce.order.purchaseID` | 建議 | |
| `commerce.productListAdds.id` | 建議 | |
| `commerce.productListAdds.value` | 建議 | |
| `commerce.productListOpens.id` | 建議 | |
| `commerce.productListOpens.value` | 建議 | |
| `commerce.productListRemoval.id` | 建議 | |
| `commerce.productListRemoval.value` | 建議 | |
| `commerce.productListViews.id` | 建議 | |
| `commerce.productListViews.value` | 建議 | |
| `commerce.productViews.id` | 建議 | |
| `commerce.productViews.value` | 建議 | |
| `commerce.purchases.id` | 建議 | |
| `commerce.purchases.value` | 建議 | |
| `marketing.campaignGroup` | 建議 | |
| `marketing.campaignName` | 建議 | |
| `marketing.trackingCode` | 建議 | |
| `productListItems.name` | 建議 | |
| `productListItems.priceTotal` | 建議 | |
| `productListItems.product` | 建議 | |
| `productListItems.quantity` | 建議 | |
| `endUserIDs._experience.emailid.authenticatedState` | 必要 | 一般使用者電子郵件地址 ID 驗證狀態。 |
| `endUserIDs._experience.emailid.id` | 必要 | 一般使用者電子郵件地址 ID。 |
| `endUserIDs._experience.emailid.namespace.code` | 必要 | 一般使用者電子郵件地址 ID 命名空間代碼。 |
| `endUserIDs._experience.mcid.authenticatedState` | 必要 | [!DNL Adobe] Marketing Cloud ID (MCID) 驗證狀態。MCID 現在稱為 Experience Cloud ID (ECID)。 |
| `endUserIDs._experience.mcid.id` | 必要 | [!DNL Adobe] Marketing CloudID (MCID)。 MCID 現在稱為 Experience Cloud ID (ECID)。 |
| `endUserIDs._experience.mcid.namespace.code` | 必要 | [!DNL Adobe] Marketing Cloud ID (MCID) 命名空間代碼。 |

+++

+++外部來源系統稽核詳細資料 (欄位群組)

外部來源系統稽核屬性是一種標準體驗資料模式 (XDM) 的資料類型，此模式會擷取外部來源系統的稽核詳細資料。

+++

### 從結構描述建立資料集 {#dataset-from-schema}

資料集是一組資料的儲存和管理結構。 智慧型重新參與歷程的每個結構描述都有單一資料集。

如需如何建立 [資料集](/help/catalog/datasets/overview.md) 從結構描述中，閱讀 [資料集UI指南](/help/catalog/datasets/user-guide.md).

>[!NOTE]
>
>與結構描述建立步驟類似，您需要啟用資料集以包含在即時客戶設定檔中。如需深入了解關於啟用資料集以用於即時客戶設定檔，請閱讀[建立架構教學課程](/help/xdm/tutorials/create-schema-ui.md#profile)。

### 隱私權、同意和資料治理 {#privacy-consent}

#### 同意原則

>[!IMPORTANT]
>
>向客戶提供從品牌接收通訊的取消訂閱功能是法律要求，同時可確保提供此選擇。進一步瞭解 [隱私權法規概述](https://experienceleague.adobe.com/docs/experience-platform/privacy/regulations/overview.html).

建立重新參與路徑時，請遵循以下步驟 [同意原則](https://experienceleague.adobe.com/docs/platform-learn/data-collection/web-sdk/consent/overview.html) 應考慮：

* 如果 `consents.marketing.email.val = "Y"` 然後可以傳送電子郵件給
* 如果 `consents.marketing.sms.val = "Y"` 然後可以使用簡訊
* 如果 `consents.marketing.push.val = "Y"` 然後可以推送
* 如果 `consents.share.val = "Y"` 然後可以廣告

#### 資料控管標籤和強制執行

建立重新參與路徑時，請遵循以下步驟 [資料控管標籤](/help/data-governance/labels/overview.md) 應考慮：

* 個人電子郵件地址可作直接可識別資料供運用，可識別或聯絡特定個人而非裝置。
   * `personalEmail.address = I1`

#### 行銷原則

沒有 [行銷政策](/help/data-governance/policies/overview.md) 重新參與歷程的必要專案，但您可視需要考量下列專案：

* 限制敏感資料
* 限制現場廣告
* 限制電子郵件目標定位
* 限制跨站台目標定位
* 限制將直接可識別資料與匿名資料相結合

### 建立對象 {#create-audience}

#### 建立品牌重新吸引歷程的對象

重新吸引歷程使用對象來定義設定檔儲存區中設定檔子集共用的特定屬性或行為，以從您的客戶群中區隔出可行銷的一群人。您可在以下位置以多種方式建立對象： [!DNL Adobe Experience Platform].

如需如何建立受眾的詳細資訊，請參閱 [Audience Service UI指南](https://experienceleague.adobe.com/docs/experience-platform/segmentation/ui/overview.html#create-audience).

如需有關如何直接撰寫的詳細資訊 [受眾](/help/segmentation/home.md)，閱讀 [對象構成UI指南](/help/segmentation/ui/audience-composition.md).

如需深入了解如何透過平台衍生的區段定義來建立對象，請參閱[對象建立器 UI 指南](/help/segmentation/ui/segment-builder.md)。

>[!BEGINTABS]

>[!TAB 重新吸引歷程]

此對象是為傳統「購物車放棄」情境的增強功能而建立。 放棄購物車通常聚焦於購物車新增而在特定時段內沒有後續購買，此對象會尋找較早的參與，尤其是可能已瀏覽特定產品但未新增至購物車，且在特定時段內您的網站上沒有後續活動的使用者。 此受眾有助於讓符合此包含條件的客戶將您的品牌放在「心上」，也可以讓他們的數位財產與傳統電子商務模式不同的客戶運用。

以下事件用於重新吸引歷程，其中使用者線上檢視產品，並且在接下來的 24 小時內沒有將產品新增到購物車，隨後的 3 天內沒有參與品牌。

設定此對象時需要下列欄位和條件：

* `EventType: commerce.productViews`
   * `Timestamp: <= 24 hours before now`
* `EventType is not: commerce.procuctListAdds`
   * `Timestamp: <= 24 hours before now, GAP(>= 3 days)`
* `EventType: application.launch or web.webpagedetails.pageViews or commerce.purchases`
   * `Timestamp: <= 2 days before now`

重新參與歷程的描述項顯示為：

`Include audience who have at least 1 EventType = ProductViews event THEN have at least 1 Any event where (EventType does not equal commerce.productListAdds) and occurs in last 24 hour(s) then after 3 days do not have any Any event where (EventType = application.launch or web.webpagedetails.pageViews or commerce.purchases) and occurs in last 2 day(s).`

>[!TAB 捨棄購物車歷程]

建立此對象是為了支援典型的「購物車放棄」案例。 其目的是尋找將產品新增至購物車但最終未完成購買的客戶。 此對象不僅可協助客戶將您的品牌放在「心上」，還可協助客戶保留產品，無需後續購買。

以下事件用於放棄的購物車歷程，使用者在此歷程中將產品新增至購物車，但未在過去24小時內完成購買或清除購物車。

設定此對象時需要下列欄位和條件：

* `EventType: commerce.productListAdds`
   * `Timestamp: >= 1 days before now and <= 4 days before now `
* `EventType: commerce.purchases`
   * `Timestamp: <= 4 days before now`
* `EventType: commerce.productListRemovals`
   * `Timestamp: <= 4 days before now`

捨棄的購物車歷程的描述項顯示為：

`Include EventType = commerce.productListAdds between 30 min and 1440 minutes before now. exclude EventType = commerce.purchases 30 minutes before now OR EventType = commerce.productListRemovals AND Cart ID equals Product List Adds1 Cart ID (the inclusion event).`

>[!TAB 訂購確認歷程]

此歷程不需要建立任何對象。

>[!ENDTABS]

### 歷程在 Adobe Journey Optimizer 中建立 {#journey-setup}

>[!NOTE]
>
>[!DNL Adobe Journey Optimizer] 不包含圖表中顯示的所有內容。 全部 [付費媒體廣告](/help/destinations/catalog/social/overview.md) 建立於 [!UICONTROL 目的地].

[[!DNL Adobe Journey Optimizer]](https://experienceleague.adobe.com/docs/journey-optimizer/using/orchestrate-journeys/journey.html) 協助您為客戶提供連結、情境式和個人化的體驗。 客戶歷程是客戶與品牌互動的整個過程。每個使用案例歷程都需要特定資訊。 下面列出的是每個歷程分支所需的精確資料。

>[!BEGINTABS]

>[!TAB 重新吸引歷程]

重新參與歷程會鎖定網站和行動應用程式上放棄的產品瀏覽。<p>![客戶智慧型重新吸引歷程的高層次視覺概觀。](../intelligent-re-engagement/images/re-engagement-journey.png "客戶智慧型重新吸引歷程的高層次視覺概觀。"){width="2560" zoomable="yes"}</p>

+++事件

* 活動1：產品檢視
   * 結構描述：客戶數位交易
   * 欄位：
      * `EventType`
   * 條件：
      * `EventType = commerce.productViews`
      * 欄位：
         * `Commerce.productViews.id`
         * `Commerce.productViews.value`
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

* 事件2：加入購物車
   * 結構描述：客戶數位交易
   * 欄位：
      * `EventType`
   * 條件：
      * `EventType = commerce.productListAdds`
      * 欄位：
         * `Commerce.productListAdds.id`
         * `Commerce.productListAdds.value`
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
         * `commerce.cart.cartID`
         * `endUserIDs._experience.emailid.authenticatedState`
         * `endUserIDs._experience.emailid.id`
         * `endUserIDs._experience.emailid.namespace.code`
         * `_id`

* 活動3：品牌參與度
   * 結構描述：客戶數位交易
   * 欄位：
      * `EventType`
   * 條件：
      * `EventType in application.launch, commerce.purchases, web.webpagedetails.pageViews`
      * 欄位：
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
         * `web.webpagedetails.URL`
         * `web.webpagedetails.isHomePage`
         * `web.webpagedetails.name`
         * `endUserIDs._experience.emailid.authenticatedState`
         * `endUserIDs._experience.emailid.id`
         * `endUserIDs._experience.emailid.namespace.code`
         * `_id`
         * `Commerce.purchases.id`
         * `Commerce.purchases.value`
         * `shipping.address.city`
         * `shipping.address.countryCode`
         * `shipping.address.postalCode`
         * `shipping.address.state`
         * `shipping.address.street1`
         * `shipping.address.street2`
         * `shipping.shipDate`
         * `shipping.trackingNumber`
         * `shipping.trackingURL`

+++

+++關鍵歷程邏輯

* 歷程登入邏輯
   * 產品檢視事件

* 條件
   * 檢查自上次訪客檢視產品以來至少有一次線上或離線購買事件。
      * 結構描述：客戶數位交易
      * `eventType = commerce.purchases`
      * `timestamp > timestamp of product last viewed`

   * 檢查自上次訪客瀏覽產品以來至少有一次離線購買事件
      * 結構描述：客戶離線交易
      * `eventType = commerce.purchases`
      * `timestamp > timestamp of product last viewed`

   * 條件 - 選取目標管道
      * 電子郵件
         * `consents.marketing.email.val = y`
      * 推播
         * `consents.marketing.push.val=y`
      * 簡訊
         * `consents.marketing.sms.val = y`

   * 管道個人化
      * 個人化管道內容以產品檢視為基礎

+++

>[!TAB 捨棄購物車歷程]

捨棄的購物車歷程鎖定已放入購物車但尚未在網站和行動應用程式上購買的產品。<p>![客戶捨棄購物車歷程的高層次視覺概觀。](../intelligent-re-engagement/images/abandoned-cart-journey.png "客戶捨棄購物車歷程的高層次視覺概觀。"){width="2560" zoomable="yes"}</p>

+++事件

* 事件2：加入購物車
   * 結構描述：客戶數位交易
   * 欄位：
      * `EventType`
   * 條件：
      * `EventType = commerce.productListAdds`
      * 欄位：
         * `Commerce.productListAdds.id`
         * `Commerce.productListAdds.value`
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
         * `commerce.cart.cartID`
         * `endUserIDs._experience.emailid.authenticatedState`
         * `endUserIDs._experience.emailid.id`
         * `endUserIDs._experience.emailid.namespace.code`
         * `_id`

* 活動4：線上購買
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

* 活動3：品牌參與度
   * 結構描述：客戶數位交易
   * 欄位：
      * `EventType`
   * 條件：
      * `EventType in application.launch, commerce.purchases, web.webpagedetails.pageViews`
      * 欄位：
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
         * `web.webpagedetails.URL`
         * `web.webpagedetails.isHomePage`
         * `web.webpagedetails.name`
         * `endUserIDs._experience.emailid.authenticatedState`
         * `endUserIDs._experience.emailid.id`
         * `endUserIDs._experience.emailid.namespace.code`
         * `_id`
         * `Commerce.purchases.id`
         * `Commerce.purchases.value`
         * `shipping.address.city`
         * `shipping.address.countryCode`
         * `shipping.address.postalCode`
         * `shipping.address.state`
         * `shipping.address.street1`
         * `shipping.address.street2`
         * `shipping.shipDate`
         * `shipping.trackingNumber`
         * `shipping.trackingURL`

+++

+++關鍵歷程邏輯

* 歷程登入邏輯
   * `AddToCart` 活動

* AuthenticatedState 位於已驗證

* 條件：自上次捨棄購物車以來離線購買：
   * 結構描述：客戶離線交易
   * `eventType = commerce.purchases`
   * `timestamp > timestamp of cart was last abandoned`

* 條件：自上次捨棄購物車以來購物車已清空：
   * 結構描述：客戶數位交易
   * `eventType = commerce.cartCleared`
   * `cartID` （購物車的ID）
   * `timestamp > timestamp of cart was last abandoned`

* 選取目標管道 (選取一個或多個管道以擴大觸及範圍)
   * 電子郵件
      * `consents.marketing.email.val = y`
   * 推播
      * `consents.marketing.push.val = y`
   * 簡訊
      * `consents.marketing.sms.val = y`
   * 管道個人化
      * 顯示購物車詳細資訊，並能以表格形式顯示多個產品。

+++

>[!TAB 訂購確認歷程]

訂購確認歷程著重在透過網站和行動應用程式購買的產品。<p>![客戶訂購確認歷程的高層次視覺概觀。](../intelligent-re-engagement/images/order-confirmation-journey.png "客戶訂購確認歷程的高層次視覺概觀。"){width="2560" zoomable="yes"}</p>

+++事件

* 活動4：線上購買
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
   * 選取目標管道 (選取一個或多個管道以擴大觸及範圍)。
      * 訂單確認本質上視為服務，因此通常不需要進行同意檢查。
      * 電子郵件
      * 推播
      * 簡訊

   * 管道內容個人化
      * 顯示訂購詳細資訊，並能以表格形式顯示產品清單。

+++

>[!ENDTABS]

如需深入了解如何在 [!DNL Adobe Journey Optimizer] 建立歷程，請參閱[歷程快速入門指南](https://experienceleague.adobe.com/docs/journey-optimizer/using/orchestrate-journeys/journey.html)。

### 在目的地中設定付費媒體廣告 {#paid-media-ads}

目的地框架用於付費媒體廣告。檢查同意後，它會傳送至設定的各種目的地。 如需有關目的地的詳細資訊，請參閱 [目的地概觀](/help/destinations/home.md) 檔案。

#### 目的地所需資料

串流區段匯出目的地 (例如 Facebook、Google 目標客戶比對、Google DV360) 支援來自客戶資料的各種身分：

* `personalEmail.address`
* `ECID`
* `mobilePhone.number`

捨棄購物車區段是採串流傳輸，因此可由目的地框架用於此使用案例。

* 串流/已觸發
   * [廣告](/help/destinations/catalog/advertising/overview.md)/[付費媒體和社交](/help/destinations/catalog/social/overview.md)
   * [行動](/help/destinations/catalog/mobile-engagement/overview.md)
   * [串流目的地](/help/destinations/catalog/streaming/http-destination.md)
   * [自訂 Destination SDK](/help/destinations/destination-sdk/overview.md)
