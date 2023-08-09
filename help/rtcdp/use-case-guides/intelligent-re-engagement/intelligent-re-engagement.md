---
title: 智慧型重新參與
description: 在關鍵轉換時刻提供引人入勝且連線的體驗，聰明地重新與不常使用的客戶互動。
hide: true
hidefromtoc: true
source-git-commit: 290c914216c1af070e065a38f726e2028c2cea8c
workflow-type: tm+mt
source-wordcount: '3482'
ht-degree: 12%

---

# 聰明地重新與客戶互動，以回歸

智慧型重新參與可讓您設定量身打造的跨頻道滴答式行銷活動，以說服客戶執行特定動作。 該推播行銷活動旨在運作一段有限的時間，其中包括傳送顯示意向電子郵件、簡訊以及提供付費廣告的客戶。 客戶採取適當的動作後，微調行銷活動就會立即結束。

![逐步智慧型重新參與高階視覺概述。](../intelligent-re-engagement/images/step-by-step.png)

## 必要條件和規劃 {#prerequisites-and-planning}

當您完成實作使用案例的步驟時，您將使用以下 Real-Time CDP 功能和 UI 元素 (按使用順序列出)。確保您擁有所有這些區域所需的屬性型存取控制權限，或要求系統管理員授予您必要的權限。

* [Adobe Real-time Customer Data Platform (Real-Time CDP)](https://experienceleague.adobe.com/docs/platform-learn/tutorials/rtcdp/understanding-the-real-time-customer-data-platform.html)  — 跨資料來源彙總資料以利行銷活動。 然後會使用此資料來建立行銷活動對象，並呈現用於電子郵件和網頁促銷活動的個人化資料元素（例如，名稱或帳戶相關資訊）。 CDP也可用來透過電子郵件和網路(透過Adobe Target)啟用對象。
   * [結構描述](/help/xdm/home.md)
   * [設定檔](/help/profile/home.md)
   * [對象](/help/segmentation/home.md)
   * [Adobe Journey Optimizer](https://experienceleague.adobe.com/docs/journey-optimizer/using/orchestrate-journeys/journey.html)
   * [事件或對象觸發器](https://experienceleague.adobe.com/docs/journey-optimizer/using/offer-decisioning/collect-event-data/data-collection.html)
   * [受眾/事件](https://experienceleague.adobe.com/docs/journey-optimizer/using/audiences-profiles-identities/audiences/about-audiences.html)
   * [歷程動作](https://experienceleague.adobe.com/docs/journey-optimizer/using/orchestrate-journeys/journey.html)

### 如何實現使用案例：高層級概觀 {#achieve-the-use-case-high-level}

有三個重新參與歷程已建立。

>[!BEGINTABS]

>[!TAB 重新參與歷程]

重新參與歷程會鎖定網站和應用程式上放棄的產品瀏覽。 瀏覽產品時，如果沒有購買產品或加入購物車，則會觸發此歷程。 如果在過去24小時內沒有清單新增，則會在三天後觸發品牌參與度。

![客戶智慧型重新參與歷程高階視覺化概觀。](../intelligent-re-engagement/images/re-engagement-journey.png)

1. 資料會透過Edge Network （偏好方法）彙總至Web SDK/Mobile SDK/Edge Network API擷取中。
2. 作為 **客戶**，即可建立標示為 [!UICONTROL 個人資料].
3. 作為 **客戶**，您可將設定檔載入到Real-Time CDP中，並建立治理政策以確保負責任地使用。
4. 作為 **客戶**，您可從設定檔清單建立焦點對象，以檢查 **使用者** 在過去三天中建立了品牌參與度。
5. 作為 **客戶**，您將會在Adobe Journey Optimizer中建立重新參與歷程。
6. 如有需要，請使用 **資料合作夥伴** 將對象啟用至所需的付費媒體目的地。
7. Adobe Journey Optimizer會檢查同意，並傳送所設定的各種動作。

>[!TAB 捨棄的購物車歷程]

這個捨棄的購物車歷程鎖定已放入購物車但並未在網站和應用程式上購買的產品。 用於啟動和停止付費媒體行銷活動

![客戶放棄購物車歷程高階視覺化概觀。](../intelligent-re-engagement/images/abandoned-cart-journey.png)

1. 資料會透過Edge Network （偏好方法）彙總至Web SDK/Mobile SDK/Edge Network API擷取中。
2. 作為 **客戶**，即可建立標示為 [!UICONTROL 個人資料].
3. 作為 **客戶**，您可將設定檔載入到Real-Time CDP中，並建立治理政策以確保負責任地使用。
4. 作為 **客戶**，您可從設定檔清單建立焦點對象，以檢查 **使用者** 已將專案放入購物車，但尚未完成購買。 此 **[!UICONTROL 加入購物車]** 事件會啟動等待30分鐘的計時器，然後檢查是否購買。 如果尚未購買，則 **使用者** 新增至 **[!UICONTROL 捨棄購物車]** 對象。
5. 作為 **客戶**，您將會在Adobe Journey Optimizer中建立捨棄的購物車歷程
6. 如有需要，請使用 **資料合作夥伴** 將對象啟用至所需的付費媒體目的地。
7. Adobe Journey Optimizer會檢查同意，並傳送所設定的各種動作。

>[!TAB 訂單確認歷程]

此訂單確認歷程會鎖定網站和應用程式上的產品購買。

![客戶訂單確認歷程高階視覺化概觀。](../intelligent-re-engagement/images/order-confirmation-journey.png)

1. 資料會透過Edge Network （偏好方法）彙總至Web SDK/Mobile SDK/Edge Network API擷取中。
2. 作為 **客戶**，即可建立標示為 [!UICONTROL 個人資料].
3. 作為 **客戶**，您可將設定檔載入到Real-Time CDP中，並建立治理政策以確保負責任地使用。
4. 作為 **客戶**，您可從設定檔清單建立焦點對象，以檢查 **使用者** 已進行購買。
5. 作為 **客戶**，您將會在Adobe Journey Optimizer中建立確認歷程。
6. Adobe Journey Optimizer會使用偏好的管道來傳送訂單確認訊息。

>[!ENDTABS]

## 如何實現使用案例：逐步說明 {#step-by-step-instructions}

請閱讀以下章節，其中包含進一步檔案的連結，以完成上述高階概覽中的每個步驟。

### 您將使用的 UI 功能和元素 {#ui-functionality-and-elements}

當您完成實作使用案例的步驟時，您將使用以下 Real-Time CDP 功能和 UI 元素 (按使用順序列出)。確保您擁有所有這些區域所需的屬性型存取控制權限，或要求系統管理員授予您必要的權限。

* [結構描述](/help/xdm/home.md)
* [設定檔](/help/profile/home.md)
* [資料集](/help/catalog/datasets/overview.md)
* [對象](/help/segmentation/home.md)
* [Adobe Journey Optimizer](https://experienceleague.adobe.com/docs/journey-optimizer/using/orchestrate-journeys/journey.html)
* [目的地](/help/destinations/home.md)

### 建立結構描述設計並指定欄位群組

Experience Data Model (XDM)資源是在以下管理： [!UICONTROL 方案] Adobe Experience Platform中的工作區。 您可以檢視並探索 Adobe 提供的核心資源，並為貴組織建立自訂資源和結構描述。

若要建立方案，請完成以下步驟：

1. 瀏覽至 **[!UICONTROL 資料管理]** > **[!UICONTROL 方案]** 並選取 **[!UICONTROL 建立結構描述]**.
2. 選取 **[!UICONTROL XDM個別設定檔]/[!UICONTROL XDM ExperienceEvent]**.
3. 瀏覽至 **[!UICONTROL 欄位群組]** 並選取 **[!UICONTROL 新增]**.
4. 使用搜尋方塊來尋找及選取欄位群組，然後選取 **[!UICONTROL 新增欄位群組]**.
5. 為結構描述命名並選擇性地提供說明。
6. 選取「**[!UICONTROL 儲存]**」。

![建立結構描述之步驟的記錄。](../intelligent-re-engagement/images/create-a-schema.gif)

如需建立綱要的詳細資訊，請參閱 [建立結構描述教學課程。](/help/xdm/tutorials/create-schema-ui.md)

有4個結構描述設計用於重新參與歷程。 每個結構描述都需要設定特定欄位，以及一些強烈建議的欄位。

#### 客戶屬性結構的欄位群組需求

客戶屬性結構為 [!UICONTROL XDM個別設定檔] 架構，包含下列欄位群組：

+++個人聯絡詳細資訊（欄位群組）

[個人聯絡詳細資訊](/help/xdm/field-groups/profile/personal-contact-details.md) 是XDM Individual Profile類別的標準結構描述欄位群組，可描述個人的聯絡資訊。

| 欄位 | 需求 | 說明 |
| --- | --- | --- |
| mobilePhone.number | 必填 | 用於簡訊的個人行動電話號碼。 |
| personalEmail.address | 必填 | 個人的電子郵件地址。 |

+++

+++人口統計細節（欄位群組）

[人口統計細節](/help/xdm/field-groups/profile/demographic-details.md) 是XDM個別設定檔類別的標準結構描述欄位群組。 欄位群組提供根層級的人員物件，其子欄位描述有關個人的資訊。

| 欄位 | 需求 |
| --- | --- |
| person.name.firstName | 建議 |
| person.name.lastName | 建議 |

+++

+++外部來源系統稽核詳細資料（欄位群組）

[外部來源系統稽核屬性](/help/xdm/data-types/external-source-system-audit-attributes.md) 是標準的體驗資料模型(XDM)資料型別，可擷取有關外部來源系統的稽核細節。

+++

+++同意和偏好設定欄位群組（欄位群組）

[同意和偏好設定](/help/xdm/field-groups//profile/consents.md) 欄位群組提供單一物件型別欄位「同意」，以擷取同意和偏好設定資訊。

| 欄位 | 需求 |
| --- | --- |
| consents.marketing.email.val | 必填 |
| consents.marketing.preferred | 必填 |
| consents.marketing.push.val | 必填 |
| consents.marketing.sms.val | 必填 |
| consents.personalize.content.val | 必填 |
| consents.share.val | 必填 |

+++

+++設定檔測試詳細資訊（欄位群組）

此欄位群組用於最佳實務。

+++

![突顯欄位群組清單的客戶屬性結構。](../intelligent-re-engagement/images/customer-attributes.png)

#### 客戶數位交易綱要的欄位群組需求

客戶數位交易結構描述是 [!UICONTROL XDM ExperienceEvent] 架構，包含下列欄位群組：

+++Adobe Experience Platform Web SDK ExperienceEvent （欄位群組）

| 欄位 | 需求 |
| --- | --- |
| device.model | 建議 |
| environment.browserDetails.userAgent | 建議 |

+++

+++網頁詳細資訊（欄位群組）

「網頁詳細資訊」是XDM ExperienceEvent類別的標準結構描述欄位群組，用於描述有關互動、頁面詳細資訊和反向連結等網頁詳細資訊事件的資訊。

| 欄位 | 需求 | 說明 |
| --- | --- | --- |
| web.webInteraction.linkClicks.id | 建議 | 與互動對應的網頁連結或URL的ID。 |
| web.webInteraction.linkClicks.value | 建議 | 與互動相對應的網頁連結或URL的點按次數。 |
| web.webInteraction.name | 建議 | 網頁的名稱。 |
| web.webInteraction.URL | 建議 | 網頁的URL。 |
| web.webPageDetails.name | 建議 | 發生網路互動的網頁名稱。 |
| web.webPageDetails.URL | 建議 | 發生網路互動之網頁的URL。 |
| web.webReferrer.URL | 建議 | 說明網頁互動的反向連結，這是目前網頁互動有記錄前訪客剛造訪過的URL。 |

+++

+++取用者體驗事件（欄位群組）

| 欄位 | 需求 |
| --- | --- |
| commerce.cart.cartID | 建議 |
| commerce.cart.cartSource | 建議 |
| commerce.cartAbandons.id | 建議 |
| commerce.cartAbandons.value | 建議 |
| commerce.order.orderType | 建議 |
| commerce.order.payments.paymentAmount | 建議 |
| commerce.order.payments.paymentType | 建議 |
| commerce.order.payments.transactionID | 建議 |
| commerce.order.priceTotal | 建議 |
| commerce.order.purchaseID | 建議 |
| commerce.productListAdds.id | 建議 |
| commerce.productListAdds.value | 建議 |
| commerce.productListOpens.id | 建議 |
| commerce.productListOpens.value | 建議 |
| commerce.productListRemoval.id | 建議 |
| commerce.productListRemoval.value | 建議 |
| commerce.productListViews.id | 建議 |
| commerce.productListViews.value | 建議 |
| commerce.productViews.id | 建議 |
| commerce.productViews.value | 建議 |
| commerce.purchases.id | 建議 |
| commerce.purchases.value | 建議 |
| marketing.campaignGroup | 建議 |
| marketing.campaignName | 建議 |
| marketing.trackingCode | 建議 |
| productListItems.name | 建議 |
| productListItems.priceTotal | 建議 |
| productListItems.product | 建議 |
| productListItems.quantity | 建議 |

+++

+++一般使用者ID詳細資訊（欄位群組）

| 欄位 | 需求 | 說明 |
| --- | --- | --- |
| endUserIDs._experience.emailid.authenticatedState | 必填 | 一般使用者電子郵件地址ID驗證狀態。 |
| endUserIDs._experience.emailid.id | 必填 | 一般使用者電子郵件地址ID。 |
| endUserIDs._experience.emailid.namespace.code | 必填 | 一般使用者電子郵件地址ID名稱空間代碼。 |
| endUserIDs._experience.mcid.authenticatedState | 必填 | Adobe Marketing Cloud ID (MCID)驗證狀態。 MCID現在稱為Experience CloudID (ECID)。 |
| endUserIDs._experience.mcid.id | 必填 | Adobe Marketing Cloud ID (MCID)。 MCID現在稱為Experience CloudID (ECID)。 |
| endUserIDs._experience.mcid.namespace.code | 必填 | Adobe Marketing Cloud ID (MCID)名稱空間程式碼。 |

+++

+++類別值（欄位群組）

| 欄位 | 需求 |
| --- | --- |
| eventtype | 必填 |
| timestamp | 必填 |

+++

+++外部來源系統稽核詳細資料（欄位群組）

外部來源系統稽核屬性是一種標準的體驗資料模型(XDM)資料型別，可擷取有關外部來源系統的稽核細節。

+++

![強調欄位群組清單的客戶數位交易結構描述。](../intelligent-re-engagement/images/customer-digital-transactions.png)

#### 客戶離線交易結構描述的欄位群組需求

客戶離線交易結構描述是 [!UICONTROL XDM ExperienceEvent] 架構，包含下列欄位群組：

+++商務詳細資料（欄位群組）

| 欄位 | 需求 | 說明 |
| --- | --- | --- |
| commerce.cart.cartID | 必填 | 購物車的ID。 |
| commerce.order.orderType | 必填 | 說明產品訂單型別的物件。 |
| commerce.order.payments.paymentAmount | 必填 | 說明產品訂單付款金額的物件。 |
| commerce.order.payments.paymentType | 必填 | 說明產品訂單付款型別的物件。 |
| commerce.order.payments.transactionID | 必填 | 物件產品訂單交易ID。 |
| commerce.order.purchaseID | 必填 | 物件產品訂單購買ID。 |
| productListItems.name | 必填 | 代表客戶所選取產品的料號名稱清單。 |
| productListItems.priceTotal | 必填 | 代表客戶所選取產品的專案清單總價。 |
| productListItems.product | 必填 | 選取的產品。 |
| productListItems.quantity | 必填 | 代表客戶所選取產品的專案清單數量。 |

+++

+++個人聯絡詳細資訊（欄位群組）

| 欄位 | 需求 | 說明 |
| --- | --- | --- |
| mobilePhone.number | 必填 | 用於簡訊的個人行動電話號碼。 |
| personalEmail.address | 必填 | 個人的電子郵件地址。 |

+++

+++類別值（欄位群組）

| 欄位 | 需求 |
| --- | --- |
| eventtype | 必填 |
| timestamp | 必填 |

+++

+++外部來源系統稽核詳細資料（欄位群組）

外部來源系統稽核屬性是一種標準的體驗資料模型(XDM)資料型別，可擷取有關外部來源系統的稽核細節。

+++

![醒目提示欄位群組清單的客戶離線交易結構描述。](../intelligent-re-engagement/images/customer-offline-transactions.png)

#### AdobeWeb聯結器結構描述的欄位群組需求

AdobeWeb聯結器結構描述是 [!UICONTROL XDM ExperienceEvent] 架構，包含下列欄位群組：

+++Adobe Analytics ExperienceEvent範本（欄位群組）

| 欄位 | 需求 | 說明 |
| --- | --- | --- |
| web.webInteraction.linkClicks.id | 建議 | 與互動對應的網頁連結或URL的ID。 |
| web.webInteraction.linkClicks.value | 建議 | 與互動相對應的網頁連結或URL的點按次數。 |
| web.webInteraction.name | 建議 | 網頁的名稱。 |
| web.webInteraction.URL | 建議 | 網頁的URL。 |
| web.webPageDetails.name | 建議 | 發生網路互動的網頁名稱。 |
| web.webPageDetails.URL | 建議 | 發生網路互動之網頁的URL。 |
| web.webReferrer.URL | 建議 | 說明網頁互動的反向連結，這是目前網頁互動有記錄前訪客剛造訪過的URL。 |
| commerce.cart.cartID | 建議 | |
| commerce.cart.cartSource | 建議 | |
| commerce.cartAbandons.id | 建議 | |
| commerce.cartAbandons.value | 建議 | |
| commerce.order.orderType | 建議 | |
| commerce.order.payments.paymentAmount | 建議 | |
| commerce.order.payments.paymentType | 建議 | |
| commerce.order.payments.transactionID | 建議 | |
| commerce.order.priceTotal | 建議 | |
| commerce.order.purchaseID | 建議 | |
| commerce.productListAdds.id | 建議 | |
| commerce.productListAdds.value | 建議 | |
| commerce.productListOpens.id | 建議 | |
| commerce.productListOpens.value | 建議 | |
| commerce.productListRemoval.id | 建議 | |
| commerce.productListRemoval.value | 建議 | |
| commerce.productListViews.id | 建議 | |
| commerce.productListViews.value | 建議 | |
| commerce.productViews.id | 建議 | |
| commerce.productViews.value | 建議 | |
| commerce.purchases.id | 建議 | |
| commerce.purchases.value | 建議 | |
| marketing.campaignGroup | 建議 | |
| marketing.campaignName | 建議 | |
| marketing.trackingCode | 建議 | |
| productListItems.name | 建議 | |
| productListItems.priceTotal | 建議 | |
| productListItems.product | 建議 | |
| productListItems.quantity | 建議 | |
| endUserIDs._experience.emailid.authenticatedState | 必填 | 一般使用者電子郵件地址ID驗證狀態。 |
| endUserIDs._experience.emailid.id | 必填 | 一般使用者電子郵件地址ID。 |
| endUserIDs._experience.emailid.namespace.code | 必填 | 一般使用者電子郵件地址ID名稱空間代碼。 |
| endUserIDs._experience.mcid.authenticatedState | 必填 | Adobe Marketing Cloud ID (MCID)驗證狀態。 MCID現在稱為Experience CloudID (ECID)。 |
| endUserIDs._experience.mcid.id | 必填 | Adobe Marketing Cloud ID (MCID)。 MCID現在稱為Experience CloudID (ECID)。 |
| endUserIDs._experience.mcid.namespace.code | 必填 | Adobe Marketing Cloud ID (MCID)名稱空間程式碼。 |

+++

+++類別值（欄位群組）

| 欄位 | 需求 |
| --- | --- |
| eventtype | 必填 |
| timestamp | 必填 |

+++

+++外部來源系統稽核詳細資料（欄位群組）

外部來源系統稽核屬性是一種標準的體驗資料模型(XDM)資料型別，可擷取有關外部來源系統的稽核細節。

+++

![AdobeWeb聯結器結構描述，醒目提示欄位群組清單。](../intelligent-re-engagement/images/adobe-web-connector.png)

### 從結構描述建立資料集

資料集是資料集合的儲存和管理結構，通常是包含方案 (欄) 和欄位 (列) 的表格。 對於智慧型重新參與歷程，每個結構描述都將有一個資料集。

若要從結構描述建立資料集，請完成以下步驟：

1. 瀏覽至「**[!UICONTROL 資料管理]** > **[!UICONTROL 資料集]**」並選取「**[!UICONTROL 建立資料集]**」。
2. 選取&#x200B;**[!UICONTROL 「從結構建立資料集」]**。
3. 選取您建立的相關重新參與綱要。
4. 為資料集命名，並提供說明 (非必填)。
5. 選取「**[!UICONTROL 完成]**」。

![從結構描述建立資料集的步驟記錄。](../intelligent-re-engagement/images/dataset-from-schema.gif)

請注意，與結構描述建立步驟類似，您需要啟用資料集以包含在即時客戶設定檔中。如需進一步了解如何啟用資料集以用於即時客戶設定檔，請閱讀[建立結構描述教學課程](/help/xdm/tutorials/create-schema-ui.md#profile)。

![啟用設定檔資料集](../intelligent-re-engagement/images/enable-dataset-for-profile.png)。

### 隱私權、同意與資料控管

#### 同意原則

>[!IMPORTANT]
>
>法律要求為客戶提供取消訂閱來自品牌之通訊的功能，同時確保遵守此選擇。 進一步瞭解 [Experience Platform 文件](https://experienceleague.adobe.com/docs/experience-platform/privacy/regulations/overview.html)中的適用法規。

設定重新參與歷程時，需要考慮並使用以下同意原則：

* 如果consents.marketing.email.val = &quot;Y&quot; ，則可以使用電子郵件
* 如果consents.marketing.sms.val = &quot;Y&quot; ，則可以SMS
* 如果consents.marketing.push.val = &quot;Y&quot; ，則可以
* 如果consents.share.val = &quot;Y&quot; ，則可以Advertise
* 由客戶實作定義的需求

#### DULE標籤和強制執行

個人電子郵件地址會用作直接可識別的資料，可用於識別或聯絡特定人員，而不是裝置。

* personalEmail.address = I1

#### 行銷政策

重新參與歷程沒有其他行銷政策，但您可視需要考量下列事項：

* 視需要考慮
* 限制敏感資料
* 限制網站上的廣告
* 限制電子郵件目標定位
* 限制跨網站目標定位
* 限制結合直接可識別的資料與匿名資料

### 建立對象

若要建立對象，請完成以下步驟：

1. 瀏覽至 **[!UICONTROL 客戶]** > **[!UICONTROL 受眾]** 並選取 **[!UICONTROL 建立對象]**.
2. 選取 **[!UICONTROL 建置規則]** 並選取 **[!UICONTROL 建立]**.
3. 瀏覽至 **[!UICONTROL 欄位]** 並選取 **[!UICONTROL 活動]** 標籤。
4. 導覽或使用搜尋方塊來尋找事件型別，然後將其拖曳至產生器。 最後，拖曳事件型別以新增事件規則。
5. 為結構描述命名並選擇性地提供說明。
6. 選取「**[!UICONTROL 儲存]**」。

![建立受眾之步驟的記錄。](../intelligent-re-engagement/images/create-an-audience.gif)

如需如何建立受眾的詳細資訊，請參閱 [Audience Builder UI指南](/help/segmentation/ui/segment-builder.md).

#### 品牌重新參與歷程的對象建立

每個重新參與歷程的對象需要設定特定事件，以進行區段資格。 這些細節可在每個歷程的對應標籤下找到。

>[!BEGINTABS]

>[!TAB 重新參與歷程]

以下事件用於重新參與歷程，其中使用者線上上檢視產品，且未在未來24小時內新增到購物車，接著在隨後的3天內沒有品牌參與。

包含具有至少1個EventType = ProductViews事件的對象，接著具有至少1個任何事件，其中（EventType不等於commerce.productListAdds）且發生在過去24小時內，然後3天後，不具有任何任何事件，其中（EventType = application.launch或web.webpagedetails.pageViews或commerce.purchases）且發生在過去2天。

![顯示規則集的重新參與對象熒幕擷圖。](../intelligent-re-engagement/images/re-engagement-audience.png)

>[!TAB 捨棄的購物車歷程]

以下事件適用於將產品新增至購物車，但未在過去24小時內完成購買或清除購物車的設定檔。

include EventType = commerce.productListAdds介於30分鐘和1440分鐘之間。
排除EventType = commerce.purchases現在之前30分鐘，或EventType = commerce.productListRemovals且購物車ID等於產品清單Adds1購物車ID （包含事件）。

![顯示規則集的重新參與對象熒幕擷圖。](../intelligent-re-engagement/images/abandoned-cart-audience.png)

>[!ENDTABS]

如需建立受眾的詳細資訊，請參閱 [Audience Builder UI指南](/help/segmentation/ui/segment-builder.md).

### Adobe Journey Optimizer中的歷程設定

>[!NOTE]
>
>Adobe Journey Optimizer並未涵蓋此頁面頂端圖表顯示的所有內容。 所有付費媒體廣告皆建立於 [!UICONTROL 目的地].

每個使用案例可以擁有的多個歷程需要特定資訊。 各歷程分支所需的特定資料可在下方對應標籤上找到。

>[!BEGINTABS]

>[!TAB 重新參與歷程]

![Adobe Journey Optimizer中的客戶重新參與歷程概覽](../intelligent-re-engagement/images/re-engagement-ajo.png)

+++活動

* 產品檢視
   * 結構：客戶數位交易
   * 欄位:
      * 事件型別
   * 條件:
      * EventType = commerce.productViews
      * 欄位:
         * Commerce.productViews.id
         * Commerce.productViews.value
         * eventtype
         * identityMap.authenticatedState
         * identityMap.id
         * identityMap.primary
         * productListItems.SKU
         * productListItems.currencyCode
         * productListItems.name
         * productListItems.priceTotal
         * productListItems.product
         * productListItems.productImageUrl
         * productListItems.quantity
         * timestamp
         * endUserIDs._experience.emailid.authenticatedState
         * endUserIDs._experience.emailid.id
         * endUserIDs._experience.emailid.namespace.code
         * _id

* 加入購物車
   * 結構：客戶數位交易
   * 欄位:
      * 活動類型
   * 條件:
      * 事件型別= commerce.productListAdds
      * 欄位:
         * Commerce.productListAdds.id
         * Commerce.productListAdds.value
         * eventtype
         * identityMap.authenticatedState
         * identityMap.id
         * identityMap.primary
         * productListItems.SKU
         * productListItems.currencyCode
         * productListItems.name
         * productListItems.priceTotal
         * productListItems.product
         * productListItems.productImageUrl
         * productListItems.quantity
         * timestamp
         * commerce.cart.cartID
         * endUserIDs._experience.emailid.authenticatedState
         * endUserIDs._experience.emailid.id
         * endUserIDs._experience.emailid.namespace.code
         * _id

* 品牌參與度
   * 結構：客戶數位交易
   * 欄位:
      * 事件型別
   * 條件:
      * application.launch、commerce.purchases、web.webpagedetails.pageViews中的EventType
      * 欄位:
         * eventtype
         * identityMap.authenticatedState
         * identityMap.id
         * identityMap.primary
         * productListItems.SKU
         * productListItems.currencyCode
         * productListItems.name
         * productListItems.priceTotal
         * productListItems.product
         * productListItems.productImageUrl
         * productListItems.quantity
         * timestamp
         * web.webpagedetails.URL
         * web.webpagedetails.isHomePage
         * web.webpagedetails.name
         * endUserIDs._experience.emailid.authenticatedState
         * endUserIDs._experience.emailid.id
         * endUserIDs._experience.emailid.namespace.code
         * _id
         * Commerce.purchases.id
         * Commerce.purchases.value
         * shipping.address.city
         * shipping.address.countryCode
         * shipping.address.postalCode
         * shipping.address.state
         * shipping.address.street1
         * shipping.address.street2
         * shipping.shipDate
         * shipping.trackingNumber
         * shipping.trackingURL

+++

+++關鍵歷程邏輯

* 歷程進入邏輯
   * 產品檢視事件

* 條件
   * 檢查自上次檢視產品以來是否有至少一個線上或離線購買事件。
      * 結構：客戶數位交易
      * eventType = commerce.purchases
      * 上次檢視之產品的時間戳記>時間戳記

   * 檢查自上次檢視產品後是否有至少一次離線購買：
      * 結構描述：客戶離線交易v.1
      * eventType = commerce.purchases
      * 上次檢視之產品的時間戳記>時間戳記

   * 條件 — 選取Target管道
      * 電子郵件
         * consents.marketing.email.val = y
      * 推播
         * consents.marketing.push.val=y
      * 簡訊
         * consents.marketing.sms.val = y

   * 管道個人化
      * 根據產品檢視的個人化管道內容。

+++

>[!TAB 捨棄的購物車歷程]

![Adobe Journey Optimizer概觀中的客戶放棄購物車歷程](../intelligent-re-engagement/images/abandoned-cart-ajo.png)

+++活動

* 加入購物車
   * 結構：客戶數位交易
   * 欄位:
      * 活動類型
   * 條件:
      * 事件型別= commerce.productListAdds
      * 欄位:
         * Commerce.productListAdds.id
         * Commerce.productListAdds.value
         * eventtype
         * identityMap.authenticatedState
         * identityMap.id
         * identityMap.primary
         * productListItems.SKU
         * productListItems.currencyCode
         * productListItems.name
         * productListItems.priceTotal
         * productListItems.product
         * productListItems.productImageUrl
         * productListItems.quantity
         * timestamp
         * commerce.cart.cartID
         * endUserIDs._experience.emailid.authenticatedState
         * endUserIDs._experience.emailid.id
         * endUserIDs._experience.emailid.namespace.code
         * _id

* 線上購買
   * 結構：客戶數位交易
   * 欄位:
      * 活動類型
   * 條件:
      * 事件型別= commerce.purchases
      * 欄位:
         * Commerce.purchases.id
         * Commerce.purchases.value
         * eventtype
         * identityMap.authenticatedState
         * identityMap.id
         * identityMap.primary
         * productListItems.SKU
         * productListItems.currencyCode
         * productListItems.name
         * productListItems.priceTotal
         * productListItems.product
         * productListItems.productImageUrl
         * productListItems.quantity
         * timestamp
         * endUserIDs._experience.emailid.authenticatedState
         * endUserIDs._experience.emailid.id
         * endUserIDs._experience.emailid.namespace.code
         * _id

* 品牌參與度
   * 結構：客戶數位交易
   * 欄位:
      * 事件型別
   * 條件:
      * application.launch、commerce.purchases、web.webpagedetails.pageViews中的EventType
      * 欄位:
         * eventtype
         * identityMap.authenticatedState
         * identityMap.id
         * identityMap.primary
         * productListItems.SKU
         * productListItems.currencyCode
         * productListItems.name
         * productListItems.priceTotal
         * productListItems.product
         * productListItems.productImageUrl
         * productListItems.quantity
         * timestamp
         * web.webpagedetails.URL
         * web.webpagedetails.isHomePage
         * web.webpagedetails.name
         * endUserIDs._experience.emailid.authenticatedState
         * endUserIDs._experience.emailid.id
         * endUserIDs._experience.emailid.namespace.code
         * _id
         * Commerce.purchases.id
         * Commerce.purchases.value
         * shipping.address.city
         * shipping.address.countryCode
         * shipping.address.postalCode
         * shipping.address.state
         * shipping.address.street1
         * shipping.address.street2
         * shipping.shipDate
         * shipping.trackingNumber
         * shipping.trackingURL

+++

+++關鍵歷程邏輯

* 歷程進入邏輯
   * AddToCart事件

* 已驗證的AuthenticatedState

* 條件：自購物車上次捨棄後的離線購買：
   * 結構描述：客戶離線交易v.1
   * eventType = commerce.purchases
   * 購物車的時間戳記>上次放棄的時間戳記

* 條件：自從上次捨棄購物車後，購物車已清除：
   * 結構：客戶數位交易v.1
   * eventType = commerce.cartCleared
   * cartID （購物車的ID）
   * 購物車的時間戳記>上次放棄的時間戳記

* 選取目標管道（選取一或多個管道以擴大觸及範圍）
   * 電子郵件
      * consents.marketing.email.val = y
   * 推播
      * consents.marketing.push.val = y
   * 簡訊
      * consents.marketing.sms.val = y
   * 管道個人化
      * 顯示購物車詳細資訊，而且能夠以表格格式顯示多個產品。

+++

>[!TAB 訂單確認歷程]

![Adobe Journey Optimizer中的客戶訂單確認歷程概覽](../intelligent-re-engagement/images/order-confirmation-ajo.png)

+++活動

* 線上購買
   * 結構：客戶數位交易
   * 欄位:
      * 事件型別
   * 條件:
      * 事件型別= commerce.purchases
      * 欄位:
         * Commerce.purchases.id
         * Commerce.purchases.value
         * eventtype
         * identityMap.authenticatedState
         * identityMap.id
         * identityMap.primary
         * productListItems.SKU
         * productListItems.currencyCode
         * productListItems.name
         * productListItems.priceTotal
         * productListItems.product
         * productListItems.productImageUrl
         * productListItems.quantity
         * timestamp
         * endUserIDs._experience.emailid.authenticatedState
         * endUserIDs._experience.emailid.id
         * endUserIDs._experience.emailid.namespace.code
         * _id

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

目的地框架用於付費媒體廣告。 檢查同意後，它會傳送到設定的各種目的地。 例如直接郵件、電子郵件等。

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
