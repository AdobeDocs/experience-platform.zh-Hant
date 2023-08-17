---
title: 智慧型重新參與
description: 在關鍵轉換時刻提供引人入勝且連線的體驗，聰明地重新與不常使用的客戶互動。
hide: true
hidefromtoc: true
source-git-commit: 43e365e20a2fd91a0e822eb6f66bb7db6fc218f5
workflow-type: tm+mt
source-wordcount: '2934'
ht-degree: 8%

---

# 聰明地重新與客戶互動，以回歸

重新與放棄轉換的客戶互動，然後再以聰明且負責的方式完成轉換。 透過體驗而不是提醒來與失效的客戶互動，以增強轉換並推動使用者端期限價值的增長。

採用即時考量，考量所有消費者品質和行為，並根據線上和離線事件提供快速的重新資格。

![逐步智慧型重新參與高階視覺概述。](../intelligent-re-engagement/images/step-by-step.png)

## 使用案例概述

您將透過重新參與歷程的範例來建構結構描述、資料集和對象。 您也會探索在中設定範例歷程所需的功能 [!DNL Adobe Journey Optimizer] 以及在目的地建立付費媒體廣告所需的使用者。 本指南使用在下列使用案例歷程中重新吸引客戶的範例：

* **重新參與歷程**  — 鎖定已放棄在網站和行動應用程式上瀏覽產品的客戶。
* **捨棄的購物車歷程**  — 鎖定已將產品放入購物車但尚未在網站和行動應用程式上購買的客戶。
* **訂單確認歷程**  — 著重於透過網站和行動應用程式進行的產品購買。

## 必要條件和規劃 {#prerequisites-and-planning}

當您完成實作使用案例的步驟時，您將使用以下 Real-Time CDP 功能和 UI 元素 (按使用順序列出)。確保您擁有所有這些區域所需的屬性型存取控制權限，或要求系統管理員授予您必要的權限。

* [Adobe Real-time Customer Data Platform (Real-Time CDP)](https://experienceleague.adobe.com/docs/platform-learn/tutorials/rtcdp/understanding-the-real-time-customer-data-platform.html)  — 跨資料來源彙總資料以利行銷活動。 然後會使用此資料來建立行銷活動對象，並呈現用於電子郵件和網頁促銷活動的個人化資料元素（例如名稱或帳戶相關資訊）。 CDP也可用來透過電子郵件和網路(透過Adobe Target)啟用對象。
   * [架構](/help/xdm/home.md)
   * [設定檔](/help/profile/home.md)
   * [資料集](/help/catalog/datasets/overview.md)
   * [對象](/help/segmentation/home.md)
   * [Adobe Journey Optimizer](https://experienceleague.adobe.com/docs/journey-optimizer/using/orchestrate-journeys/journey.html)
   * [目的地](/help/destinations/home.md)
   * [事件或對象觸發器](https://experienceleague.adobe.com/docs/journey-optimizer/using/offer-decisioning/collect-event-data/data-collection.html)
   * [受眾/事件](https://experienceleague.adobe.com/docs/journey-optimizer/using/audiences-profiles-identities/audiences/about-audiences.html)
   * [歷程動作](https://experienceleague.adobe.com/docs/journey-optimizer/using/orchestrate-journeys/journey.html)

### 如何實現使用案例：高層級概觀 {#achieve-the-use-case-high-level}

以下是三個重新參與歷程範例的高層級概觀。

>[!BEGINTABS]

>[!TAB 重新參與歷程]

重新參與歷程會鎖定網站和行動應用程式上放棄的產品瀏覽。 當已檢視產品但未購買或未新增到購物車時，就會觸發此歷程。 如果在過去24小時內沒有清單新增，則會在三天後觸發品牌參與度。<p>![客戶智慧型重新參與歷程高階視覺化概觀。](../intelligent-re-engagement/images/re-engagement-journey.png "客戶智慧型重新參與歷程高階視覺化概觀。"){width="1920" zoomable="yes"}</p>

1. 您可以建立標籤為的結構描述和資料集 [!UICONTROL 個人資料].
2. 資料會透過Web SDK、Mobile Edge SDK或API彙總至Experience Platform中。 也可以使用Analytics Data Connector，但可能會導致歷程延遲。
3. 您可將設定檔載入到Real-Time CDP中，並建立治理政策以確保負責任地使用。
4. 您可以從設定檔清單建立焦點對象，以檢查 **客戶** 已在過去三天進行參與。
5. 您在中建立重新參與歷程 [!DNL Adobe Journey Optimizer].
6. 如有需要，請使用 **資料合作夥伴** 將對象啟用至所需的付費媒體目的地。
7. [!DNL Adobe Journey Optimizer] 檢查同意並傳送設定的各種動作。

>[!TAB 捨棄的購物車歷程]

捨棄的購物車歷程鎖定已放入購物車但尚未在網站和行動應用程式上購買的產品。 此外，付費媒體行銷活動也會使用此方法啟動和停止。<p>![客戶放棄購物車歷程高階視覺化概觀。](../intelligent-re-engagement/images/abandoned-cart-journey.png "客戶放棄購物車歷程高階視覺化概觀。"){width="1920" zoomable="yes"}</p>

1. 您可以建立標籤為的結構描述和資料集 [!UICONTROL 個人資料].
2. 資料會透過Web SDK、Mobile Edge SDK或API彙總至Experience Platform中。 也可以使用Analytics Data Connector，但可能會導致歷程延遲。
3. 您可將設定檔載入到Real-Time CDP中，並建立治理政策以確保負責任地使用。
4. 您可以從設定檔清單建立焦點對象，以檢查 **客戶** 已將專案放入購物車，但尚未完成購買。 此 **[!UICONTROL 加入購物車]** 事件會啟動等待30分鐘的計時器，然後檢查是否購買。 如果尚未購買，則 **客戶** 新增至 **[!UICONTROL 捨棄購物車]** 對象。
5. 您在Adobe Journey Optimizer中建立捨棄的購物車歷程
6. 如有需要，請使用 **資料合作夥伴** 將對象啟用至所需的付費媒體目的地。
7. [!DNL Adobe Journey Optimizer] 檢查同意並傳送設定的各種動作。

>[!TAB 訂單確認歷程]

訂單確認歷程專注於透過網站和行動應用程式進行的產品購買。<p>![客戶訂單確認歷程高階視覺化概觀。](../intelligent-re-engagement/images/order-confirmation-journey.png "客戶訂單確認歷程高階視覺化概觀。"){width="1920" zoomable="yes"}</p>

1. 您可以建立標籤為的結構描述和資料集 [!UICONTROL 個人資料].
2. 資料會透過Web SDK、Mobile Edge SDK或API彙總至Experience Platform中。 也可以使用Analytics Data Connector，但可能會導致歷程延遲。
3. 您可將設定檔載入到Real-Time CDP中，並建立治理政策以確保負責任地使用。
4. 您可以從設定檔清單建立焦點對象，以檢查 **客戶** 已進行購買。
5. 您可以在Adobe Journey Optimizer中建立確認歷程。
6. [!DNL Adobe Journey Optimizer] 使用偏好的管道傳送訂單確認訊息。

>[!ENDTABS]

## 如何實現使用案例：逐步說明 {#step-by-step-instructions}

若要完成上述高階概覽中的每個步驟，請閱讀以下章節，其中提供詳細資訊和詳細指示的連結。

### 您將使用的 UI 功能和元素 {#ui-functionality-and-elements}

當您完成實施使用案例的步驟時，您將使用本檔案開頭列出的Real-Time CDP功能和UI元素。 確保您擁有所有這些區域所需的屬性型存取控制權限，或要求系統管理員授予您必要的權限。

### 建立結構描述設計並指定欄位群組

Experience Data Model (XDM)資源是在以下管理： [!UICONTROL 方案] Adobe Experience Platform中的工作區。 您可以檢視和探索Adobe提供的核心資源，並為您的組織建立自訂資源和結構描述。

如需建立綱要的詳細資訊，請參閱 [建立結構描述教學課程。](/help/xdm/tutorials/create-schema-ui.md)

有四個結構描述設計用於重新參與歷程。 每個結構描述都需要設定特定欄位，以及一些強烈建議的欄位。

#### 客戶屬性結構

客戶屬性結構以 [!UICONTROL XDM個別設定檔] 類別，包括下列欄位群組：

+++個人聯絡詳細資訊（欄位群組）

[個人聯絡詳細資訊](/help/xdm/field-groups/profile/personal-contact-details.md) 是XDM Individual Profile類別的標準結構描述欄位群組，可描述個人的聯絡資訊。

| 欄位 | 需求 | 說明 |
| --- | --- | --- |
| `mobilePhone.number` | 必填 | 用於簡訊的個人行動電話號碼。 |
| `personalEmail.address` | 必填 | 個人的電子郵件地址。 |

+++

+++人口統計細節（欄位群組）

[人口統計細節](/help/xdm/field-groups/profile/demographic-details.md) 是XDM個別設定檔類別的標準結構描述欄位群組。 欄位群組提供根層級的人員物件，其子欄位描述有關個人的資訊。

| 欄位 | 需求 |
| --- | --- |
| `person.name.firstName` | 建議 |
| `person.name.lastName` | 建議 |

+++

+++外部來源系統稽核詳細資料（欄位群組）

[外部來源系統稽核屬性](/help/xdm/data-types/external-source-system-audit-attributes.md) 是標準的體驗資料模型(XDM)資料型別，可擷取有關外部來源系統的稽核細節。

+++

+++同意和偏好設定欄位群組（欄位群組）

[同意和偏好設定](/help/xdm/field-groups//profile/consents.md) 欄位群組提供單一物件型別欄位「同意」，以擷取同意和偏好設定資訊。

| 欄位 | 需求 |
| --- | --- |
| `consents.marketing.email.val` | 必填 |
| `consents.marketing.preferred` | 必填 |
| `consents.marketing.push.val` | 必填 |
| `consents.marketing.sms.val` | 必填 |
| `consents.personalize.content.val` | 必填 |
| `consents.share.val` | 必填 |

+++

+++設定檔測試詳細資訊（欄位群組）

此欄位群組用於最佳實務。

+++

#### 客戶數位交易綱要

客戶數位交易結構描述是由 [!UICONTROL XDM ExperienceEvent] 類別，包括下列欄位群組：

+++Adobe Experience Platform Web SDK ExperienceEvent （欄位群組）

| 欄位 | 需求 |
| --- | --- |
| `device.model` | 建議 |
| `environment.browserDetails.userAgent` | 建議 |

+++

+++網頁詳細資訊（欄位群組）

「網頁詳細資訊」是XDM ExperienceEvent類別的標準結構描述欄位群組，用於描述有關互動、頁面詳細資訊和反向連結等網頁詳細資訊事件的資訊。

| 欄位 | 需求 | 說明 |
| --- | --- | --- |
| `web.webInteraction.linkClicks.id` | 建議 | 與互動對應的網頁連結或URL的ID。 |
| `web.webInteraction.linkClicks.value` | 建議 | 與互動相對應的網頁連結或URL的點按次數。 |
| `web.webInteraction.name` | 建議 | 網頁的名稱。 |
| `web.webInteraction.URL` | 建議 | 網頁的URL。 |
| `web.webPageDetails.name` | 建議 | 發生網路互動的網頁名稱。 |
| `web.webPageDetails.URL` | 建議 | 發生網路互動之網頁的URL。 |
| `web.webReferrer.URL` | 建議 | 說明網頁互動的反向連結，這是目前網頁互動有記錄前訪客剛造訪過的URL。 |

+++

+++取用者體驗事件（欄位群組）

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

+++一般使用者ID詳細資訊（欄位群組）

| 欄位 | 需求 | 說明 |
| --- | --- | --- |
| `endUserIDs._experience.emailid.authenticatedState` | 必填 | 一般使用者電子郵件地址ID驗證狀態。 |
| `endUserIDs._experience.emailid.id` | 必填 | 一般使用者電子郵件地址ID。 |
| `endUserIDs._experience.emailid.namespace.code` | 必填 | 一般使用者電子郵件地址ID名稱空間代碼。 |
| `endUserIDs._experience.mcid.authenticatedState` | 必填 | Adobe Marketing Cloud ID (MCID)驗證狀態。 MCID現在稱為Experience CloudID (ECID)。 |
| `endUserIDs._experience.mcid.id` | 必填 | Adobe Marketing Cloud ID (MCID)。 MCID現在稱為Experience CloudID (ECID)。 |
| `endUserIDs._experience.mcid.namespace.code` | 必填 | Adobe Marketing Cloud ID (MCID)名稱空間程式碼。 |

+++

+++類別值（欄位群組）

| 欄位 | 需求 |
| --- | --- |
| `eventType` | 必填 |
| `timestamp` | 必填 |

+++

+++外部來源系統稽核詳細資料（欄位群組）

外部來源系統稽核屬性是一種標準的體驗資料模型(XDM)資料型別，可擷取有關外部來源系統的稽核細節。

+++

#### 客戶離線交易結構描述

客戶離線交易結構描述會以 [!UICONTROL XDM ExperienceEvent] 類別，包括下列欄位群組：

+++商務詳細資料（欄位群組）

| 欄位 | 需求 | 說明 |
| --- | --- | --- |
| `commerce.cart.cartID` | 必填 | 購物車的ID。 |
| `commerce.order.orderType` | 必填 | 說明產品訂單型別的物件。 |
| `commerce.order.payments.paymentAmount` | 必填 | 說明產品訂單付款金額的物件。 |
| `commerce.order.payments.paymentType` | 必填 | 說明產品訂單付款型別的物件。 |
| `commerce.order.payments.transactionID` | 必填 | 物件產品訂單交易ID。 |
| `commerce.order.purchaseID` | 必填 | 物件產品訂單購買ID。 |
| `productListItems.name` | 必填 | 代表客戶所選取產品的料號名稱清單。 |
| `productListItems.priceTotal` | 必填 | 代表客戶所選取產品的專案清單總價。 |
| `productListItems.product` | 必填 | 選取的產品。 |
| `productListItems.quantity` | 必填 | 代表客戶所選取產品的專案清單數量。 |

+++

+++個人聯絡詳細資訊（欄位群組）

| 欄位 | 需求 | 說明 |
| --- | --- | --- |
| `mobilePhone.number` | 必填 | 用於簡訊的個人行動電話號碼。 |
| `personalEmail.address` | 必填 | 個人的電子郵件地址。 |

+++

+++類別值（欄位群組）

| 欄位 | 需求 |
| --- | --- |
| `eventType` | 必填 |
| `timestamp` | 必填 |

+++

+++外部來源系統稽核詳細資料（欄位群組）

外部來源系統稽核屬性是一種標準的體驗資料模型(XDM)資料型別，可擷取有關外部來源系統的稽核細節。

+++

#### Adobe的Web聯結器結構描述

AdobeWeb聯結器結構描述是由 [!UICONTROL XDM ExperienceEvent] 類別，包括下列欄位群組：

+++Adobe Analytics ExperienceEvent範本（欄位群組）

| 欄位 | 需求 | 說明 |
| --- | --- | --- |
| `web.webInteraction.linkClicks.id` | 建議 | 與互動對應的網頁連結或URL的ID。 |
| `web.webInteraction.linkClicks.value` | 建議 | 與互動相對應的網頁連結或URL的點按次數。 |
| `web.webInteraction.name` | 建議 | 網頁的名稱。 |
| `web.webInteraction.URL` | 建議 | 網頁的URL。 |
| `web.webPageDetails.name` | 建議 | 發生網路互動的網頁名稱。 |
| `web.webPageDetails.URL` | 建議 | 發生網路互動之網頁的URL。 |
| `web.webReferrer.URL` | 建議 | 說明網頁互動的反向連結，這是目前網頁互動有記錄前訪客剛造訪過的URL。 |
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
| `endUserIDs._experience.emailid.authenticatedState` | 必填 | 一般使用者電子郵件地址ID驗證狀態。 |
| `endUserIDs._experience.emailid.id` | 必填 | 一般使用者電子郵件地址ID。 |
| `endUserIDs._experience.emailid.namespace.code` | 必填 | 一般使用者電子郵件地址ID名稱空間代碼。 |
| `endUserIDs._experience.mcid.authenticatedState` | 必填 | Adobe Marketing Cloud ID (MCID)驗證狀態。 MCID現在稱為Experience CloudID (ECID)。 |
| `endUserIDs._experience.mcid.id` | 必填 | Adobe Marketing Cloud ID (MCID)。 MCID現在稱為Experience CloudID (ECID)。 |
| `endUserIDs._experience.mcid.namespace.code` | 必填 | Adobe Marketing Cloud ID (MCID)名稱空間程式碼。 |

+++

+++類別值（欄位群組）

| 欄位 | 需求 |
| --- | --- |
| `eventType` | 必填 |
| `timestamp` | 必填 |

+++

+++外部來源系統稽核詳細資料（欄位群組）

外部來源系統稽核屬性是一種標準的體驗資料模型(XDM)資料型別，可擷取有關外部來源系統的稽核細節。

+++

### 從結構描述建立資料集

資料集是一組資料的儲存和管理結構，通常是包含欄位（列）和結構（欄）的表格。 智慧型重新參與歷程的每個結構描述都有單一資料集。

如需如何從結構描述建立資料集的詳細資訊，請參閱 [資料集UI指南](/help/catalog/datasets/user-guide.md).

>[!NOTE]
>
>與建立結構的步驟類似，您需要啟用包含在Real-Time Customer Profile中的資料集。 如需啟用資料集以用於即時客戶個人檔案的詳細資訊，請參閱 [建立結構描述教學課程。](/help/xdm/tutorials/create-schema-ui.md#profile).

### 隱私權、同意與資料控管

#### 同意原則

>[!IMPORTANT]
>
>法律要求為客戶提供取消訂閱來自品牌之通訊的功能，同時確保遵守此選擇。 進一步瞭解 [Experience Platform 文件](https://experienceleague.adobe.com/docs/experience-platform/privacy/regulations/overview.html)中的適用法規。

建立重新參與路徑時，必須考慮並使用以下同意政策：

* 如果 `consents.marketing.email.val = "Y"` 然後可以傳送電子郵件給
* 如果 `consents.marketing.sms.val = "Y"` 然後可以使用簡訊
* 如果 `consents.marketing.push.val = "Y"` 然後可以推送
* 如果 `consents.share.val = "Y"` 然後可以廣告
* 由客戶實作定義的需求

#### DULE標籤和強制執行

個人電子郵件地址會用作直接可識別的資料，用於識別或聯絡特定個人而非裝置。

* `personalEmail.address = I1`

#### 行銷政策

重新參與歷程不需要其他行銷政策，但可視需要考量下列事項：

* 限制敏感資料
* 限制網站上的廣告
* 限制電子郵件目標定位
* 限制跨網站目標定位
* 限制結合直接可識別的資料與匿名資料

### 建立對象

#### 品牌重新參與歷程的對象建立

重新參與歷程使用受眾來定義由您的個人資料存放區中的個人資料子集共用的特定屬性或行為，以區分可行銷的人員群組與您的客戶群。 您可以在Adobe Experience Platform上以兩種不同的方式建立對象：直接構成對象或透過Platform衍生的區段定義。

如需如何直接撰寫對象的詳細資訊，請參閱 [對象構成UI指南](/help/segmentation/ui/audience-composition.md).

如需如何透過平台衍生的區段定義建立受眾的詳細資訊，請參閱 [Audience Builder UI指南](/help/segmentation/ui/segment-builder.md).

>[!BEGINTABS]

>[!TAB 重新參與歷程]

以下事件用於重新參與歷程，其中使用者線上上檢視產品，且未在未來24小時內新增到購物車，接著在隨後的3天內沒有品牌參與。

設定此對象時需要下列欄位和條件：

* `EventType: commerce.productViews`
   * `Timestamp: <= 24 hours before now`
* `EventType is not: commerce.productListAdds`
   * `Timestamp: <= 24 hours before now, GAP(>= 3 days)`
* `EventType: application.launch or web.webpagedetails.pageViews or commerce.purchases`
   * `Timestamp: <= 2 days before now`

重新參與歷程的描述項顯示為：

`Include audience who have at least 1 EventType = ProductViews event THEN have at least 1 Any event where (EventType does not equal commerce.productListAdds) and occurs in last 24 hour(s) then after 3 days do not have any Any event where (EventType = application.launch or web.webpagedetails.pageViews or commerce.purchases) and occurs in last 2 day(s).`

>[!TAB 捨棄的購物車歷程]

以下事件用於放棄的購物車歷程，使用者在此歷程中將產品新增至購物車，但未在過去24小時內完成購買或清除購物車。

設定此對象時需要下列欄位和條件：

* `EventType: commerce.productListAdds`
   * `Timestamp: >= 30 minutes before now and <= 1440 minutes before now`
* `EventType: commerce.purchases`
   * `Timestamp: <= 30 minutes before now`
* `EventType: commerce.productListRemovals`
   * `Timestamp: <= 30 minutes before now`

捨棄的購物車歷程的描述項顯示為：

`Include EventType = commerce.productListAdds between 30 min and 1440 minutes before now. exclude EventType = commerce.purchases 30 minutes before now OR EventType = commerce.productListRemovals AND Cart ID equals Product List Adds1 Cart ID (the inclusion event).`

>[!ENDTABS]

### Adobe Journey Optimizer中的歷程設定

>[!NOTE]
>
>Adobe Journey Optimizer並未涵蓋此頁面頂端圖表顯示的所有內容。 所有付費媒體廣告皆建立於 [!UICONTROL 目的地].

Adobe Journey Optimizer可協助您為客戶提供連結、情境式和個人化的體驗。 客戶歷程是客戶與品牌互動的整個過程。 每個使用案例歷程都需要特定資訊。 以下列出每個Journey分支所需的精確資料。

>[!BEGINTABS]

>[!TAB 重新參與歷程]

+++活動

* 產品檢視
   * 結構：客戶數位交易
   * 欄位:
      * `EventType`
   * 條件:
      * `EventType = commerce.productViews`
      * 欄位:
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

* 加入購物車
   * 結構：客戶數位交易
   * 欄位:
      * `EventType`
   * 條件:
      * `EventType = commerce.productListAdds`
      * 欄位:
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

* 品牌參與度
   * 結構：客戶數位交易
   * 欄位:
      * `EventType`
   * 條件:
      * `EventType in application.launch, commerce.purchases, web.webpagedetails.pageViews`
      * 欄位:
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

* 歷程進入邏輯
   * 產品檢視事件

* 條件
   * 檢查自上次檢視產品以來是否有至少一個線上或離線購買事件。
      * 結構：客戶數位交易
      * `eventType = commerce.purchases`
      * `timestamp > timestamp of product last viewed`

   * 檢查自上次檢視產品後是否有至少一次離線購買：
      * 結構描述：客戶離線交易v.1
      * `eventType = commerce.purchases`
      * `timestamp > timestamp of product last viewed`

   * 條件 — 選取Target管道
      * 電子郵件
         * `consents.marketing.email.val = y`
      * 推播
         * `consents.marketing.push.val=y`
      * 簡訊
         * `consents.marketing.sms.val = y`

   * 管道個人化
      * 根據產品檢視的個人化管道內容。

+++

>[!TAB 捨棄的購物車歷程]

+++活動

* 加入購物車
   * 結構：客戶數位交易
   * 欄位:
      * `EventType`
   * 條件:
      * `EventType = commerce.productListAdds`
      * 欄位:
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

* 線上購買
   * 結構：客戶數位交易
   * 欄位:
      * `EventType`
   * 條件:
      * `EventType = commerce.purchases`
      * 欄位:
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

* 品牌參與度
   * 結構：客戶數位交易
   * 欄位:
      * `EventType`
   * 條件:
      * `EventType in application.launch, commerce.purchases, web.webpagedetails.pageViews`
      * 欄位:
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

* 歷程進入邏輯
   * `AddToCart` 活動

* 已驗證的AuthenticatedState

* 條件：自購物車上次捨棄後的離線購買：
   * 結構描述：客戶離線交易v.1
   * `eventType = commerce.purchases`
   * `timestamp > timestamp of cart was last abandoned`

* 條件：自從上次捨棄購物車後，購物車已清除：
   * 結構：客戶數位交易v.1
   * `eventType = commerce.cartCleared`
   * `cartID` （購物車的ID）
   * `timestamp > timestamp of cart was last abandoned`

* 選取目標管道（選取一或多個管道以擴大觸及範圍）
   * 電子郵件
      * `consents.marketing.email.val = y`
   * 推播
      * `consents.marketing.push.val = y`
   * 簡訊
      * `consents.marketing.sms.val = y`
   * 管道個人化
      * 顯示購物車詳細資訊，而且能夠以表格格式顯示多個產品。

+++

>[!TAB 訂單確認歷程]

+++活動

* 線上購買
   * 結構：客戶數位交易
   * 欄位:
      * `EventType`
   * 條件:
      * `EventType = commerce.purchases`
      * 欄位:
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

* 歷程進入邏輯
   * 訂購事件

* 條件
   * 選取目標管道（選取一或多個管道以擴大觸及範圍）。
      * 本質上訂單確認會視為提供，因此通常不需要檢查同意。
      * 電子郵件
      * 推播
      * 簡訊

   * 管道內容個人化
      * 顯示訂單詳細資訊，並可使用表格格式顯示產品清單。

+++

>[!ENDTABS]

如需有關在中建立歷程的詳細資訊 [Adobe Journey Optimizer]，閱讀 [開始使用歷程指南](https://experienceleague.adobe.com/docs/journey-optimizer/using/orchestrate-journeys/journey.html).

### 在目的地中設定付費媒體廣告

目的地框架用於付費媒體廣告。 檢查同意後，它會傳送至設定的各種目的地。 例如直接郵件、電子郵件、推播和簡訊。

#### 目的地所需的資料

串流區段匯出目的地(例如Facebook、Google Customer Match、Google DV360)支援客戶資料中的各種身分：

* `personalEmail.address`
* `ECID`
* `mobilePhone.number`

捨棄購物車區段正在串流，因此目標架構可用於此使用案例。

* 串流/觸發
   * [Advertising](/help/destinations/catalog/advertising/overview.md)/[付費媒體與社交](/help/destinations/catalog/social/overview.md)
   * [行動](/help/destinations/catalog/mobile-engagement/overview.md)
   * [串流目的地](/help/destinations/catalog/streaming/http-destination.md)
   * [自訂Destination SDK](/help/destinations/destination-sdk/overview.md)

* 每三小時檔案/排程
   * [電子郵件行銷](/help/destinations/catalog/email-marketing/overview.md)
