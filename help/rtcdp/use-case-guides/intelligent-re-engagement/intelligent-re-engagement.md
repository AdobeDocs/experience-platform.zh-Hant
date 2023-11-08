---
title: 智慧型重新吸引
description: 在關鍵轉換時刻提供引人注目的互聯體驗，以智慧方式重新吸引不常造訪的客戶。
exl-id: 13f6dbc9-7471-40bf-824d-27922be0d879
source-git-commit: d47ddc474fcaf19eaff8ddcd67139dec5c417720
workflow-type: tm+mt
source-wordcount: '3594'
ht-degree: 54%

---

# 以智慧方式重新吸引您的客戶回訪

>[!NOTE]
>
>此為實作範例，本頁上的範例（例如區段語法）僅為範例。 由於實作方法可能有所差異，您應參考這些範例。

以聰明負責的方式重新吸引放棄轉換的客戶。 透過體驗與失效的客戶互動，以提高轉換率並增加使用者端期限值。

採用即時考慮方式、將所有消費者的品質和行為納入考量，並根據線上和線下事件提供更快的重新資格認證。

![智慧型重新參與高階視覺化概觀。](../intelligent-re-engagement/images/step-by-step.png)

## 使用案例概觀 {#overview}

當您透過重新參與案例的範例工作時，將建構結構描述、資料集和對象。 您還將探索在 [!DNL Adobe Journey Optimizer] 設定範例歷程所需的功能，以及探索在目的地中製作付費媒體廣告所需的功能。本指南使用在下面所述使用案例中重新吸引客戶的範例：

* **放棄的產品瀏覽案例**  — 鎖定已放棄在網站和行動應用程式上瀏覽產品的客戶。
* **捨棄的購物車案例**  — 將產品放入購物車但尚未在網站和行動應用程式上購買的目標客戶。
* **訂單確認案例**  — 著重於透過網站和行動應用程式進行的產品購買。

## 必要條件和規劃 {#prerequisites-and-planning}

完成實施使用案例的步驟後，您將運用下列Real-Time CDP和Adobe Journey Optimizer功能（依使用順序列出）。 確保您擁有所有這些區域所需的[屬性型存取控制權限](/help/access-control/home.md)，或要求系統管理員授予您必要的權限。

* [[!DNL Adobe Real-Time Customer Data Platform (Real-Time CDP)]](https://experienceleague.adobe.com/docs/platform-learn/tutorials/rtcdp/understanding-the-real-time-customer-data-platform.html)- 整合跨資料來源的資料，以推動行銷活動。然後，使用此資料來建立行銷活動對象，並呈現用於電子郵件和網頁促銷圖磚的個人化資料元素 (例如姓名或帳戶相關資訊)。CDP 也用於跨電子郵件和網頁啟動對象 (透過 [!DNL Adobe Target]).
   * [結構描述](/help/xdm/home.md)
   * [設定檔](/help/profile/home.md)
   * [資料集](/help/catalog/datasets/overview.md)
   * [對象](/help/segmentation/home.md)
   * [[!DNL Adobe Journey Optimizer]](https://experienceleague.adobe.com/docs/journey-optimizer/using/orchestrate-journeys/journey.html)
   * [目的地](/help/destinations/home.md)

* [[!DNL Adobe Journey Optimizer]](https://experienceleague.adobe.com/docs/journey-optimizer-learn/tutorials/introduction-to-journey-optimizer/introduction.html?lang=zh-Hant)  — 協助您為客戶提供連結、情境式和個人化的體驗。
   * [事件或對象觸發](https://experienceleague.adobe.com/docs/journey-optimizer/using/offer-decisioning/collect-event-data/data-collection.html)
   * [對象/事件](https://experienceleague.adobe.com/docs/journey-optimizer/using/audiences-profiles-identities/audiences/about-audiences.html)
   * [歷程動作](https://experienceleague.adobe.com/docs/journey-optimizer/using/orchestrate-journeys/journey.html)

## 如何實現使用案例 {#achieve-use-case-instruction}

以下是3個重新參與範例情景的高層級概觀。

>[!BEGINTABS]

>[!TAB 放棄的產品瀏覽情境]

放棄的產品瀏覽情境會鎖定網站和行動應用程式上放棄的產品瀏覽。 當已檢視產品但未購買或未新增到購物車時，就會觸發此情境。 在此範例中，如果過去24小時內沒有清單新增，則會在3天後觸發品牌參與度。<p>![客戶智慧型放棄的產品瀏覽情境高階視覺化概觀。](../intelligent-re-engagement/images/re-engagement-journey.png "客戶智慧型放棄的產品瀏覽情境高階視覺化概觀。"){width="1920" zoomable="yes"}</p>

1. 您可以建立方案和資料集，然後啟用 [!UICONTROL 個人資料].
2. 您可以透過Web SDK、Mobile SDK或API將資料內嵌至Experience Platform。 也可以使用 Analytics Data Connector，但可能會導致歷程延遲。
3. 您可以內嵌其他已啟用設定檔的資料，這些資料可以透過身分圖表連結至已驗證的網頁和/或行動應用程式訪客。
4. 您從設定檔清單建立重點對象，以檢查&#x200B;**使用者**&#x200B;在過去三天是否有進行參與行動。
5. 您會在中建立放棄的產品瀏覽歷程 [!DNL Adobe Journey Optimizer].
6. 如有需要，與&#x200B;**資料合作夥伴**&#x200B;協作，將對象啟動到所需付費媒體目的地。
7. [!DNL Adobe Journey Optimizer] 檢查是否同意並發送設定的各種動作。

>[!TAB 捨棄的購物車情境]

放棄購物車情況適用於產品已放入購物車但尚未在網站和行動應用程式上購買的情況。 此外，付費媒體行銷活動可以使用此方法開始和停止。<p>![客戶放棄購物車案例高階視覺化概觀。](../intelligent-re-engagement/images/abandoned-cart-journey.png "客戶放棄購物車案例高階視覺化概觀。"){width="1920" zoomable="yes"}</p>

1. 您可以建立結構描述和資料集，並為以下專案啟用 [!UICONTROL 個人資料].
2. 您可以透過Web SDK、Mobile SDK或API將資料內嵌至Experience Platform。 也可以使用 Analytics Data Connector，但可能會導致歷程延遲。
3. 您可以內嵌其他已啟用設定檔的資料，這些資料可以透過身分圖表連結至已驗證的網頁和/或行動應用程式訪客。
4. 您從設定檔清單建立重點對象，以檢查&#x200B;**客戶**&#x200B;是否已將商品放入購物車但尚未完成購買。**[!UICONTROL 新增到購物車]**&#x200B;事件會啟動計時器；計時器會等待 30 分鐘，然後檢查是否有購買。如果沒有購買，那麼會將&#x200B;**客戶**&#x200B;新增到&#x200B;**[!UICONTROL 捨棄購物車]**&#x200B;對象。
5. 您在 [!DNL Adobe Journey Optimizer] 中建立一個廢棄購物車歷程。
6. 如有需要，與&#x200B;**資料合作夥伴**&#x200B;協作，將對象啟動到所需付費媒體目的地。
7. [!DNL Adobe Journey Optimizer] 檢查是否同意並發送設定的各種動作。

>[!TAB 訂單確認案例]

訂購確認案例聚焦於透過網站和行動應用程式進行的產品購買。<p>![客戶訂單確認案例高階視覺化概觀。](../intelligent-re-engagement/images/order-confirmation-journey.png "客戶訂單確認案例高階視覺化概觀。"){width="1920" zoomable="yes"}</p>

1. 您可以建立方案和資料集，然後啟用 [!UICONTROL 個人資料].
2. 您可以透過Web SDK、Mobile SDK或API將資料內嵌至Experience Platform。 也可以使用 Analytics Data Connector，但可能會導致歷程延遲。
3. 您可以內嵌其他已啟用設定檔的資料，這些資料可以透過身分圖表連結至已驗證的網頁和/或行動應用程式訪客。
4. 您在 [!DNL Adobe Journey Optimizer] 中建立一個確認歷程。
5. [!DNL Adobe Journey Optimizer] 使用偏好管道發送訂購確認訊息。

>[!ENDTABS]

要完成上述高層次概觀中的每個步驟，請閱讀以下各節中更多資訊和更詳細說明的連結。

### 建立方案並指定欄位群組 {#schema-design}

體驗資料模型 (XDM) 資源是在 [!DNL Adobe Experience Platform] 內的[!UICONTROL 結構描述] 工作區中接受管理。您可以檢視並探索所提供的核心資源： [!DNL Adobe] （例如，欄位群組）並為您的組織建立自訂資源和結構描述。

如需關於建立的詳細資訊 [結構描述](/help/xdm/home.md)，請參閱 [建立結構描述教學課程。](/help/xdm/tutorials/create-schema-ui.md) 和 [使用XDM為您的客戶體驗資料建立模型](https://experienceleague.adobe.com/docs/courses/using/experienceplatform-d-1-2021-1-xdm.html).

有四種用於重新吸引使用案例的結構描述設計。每個結構描述都需要設定特定欄位。 您需要啟用要包含在即時客戶個人檔案中的結構描述。 如需啟用結構以用於Real-Time Customer Profile的詳細資訊，請參閱 [為即時客戶個人檔案啟用結構](/help/xdm/ui/resources/schemas.md#enable-a-schema-for-real-time-customer-profile).

#### 客戶屬性結構描述

此結構描述是用來安排和參考構成客戶資訊的設定檔資料。此資料通常會內嵌至 [!DNL Adobe Experience Platform] 透過CRM或類似系統，且為參考用於個人化、行銷同意和增強受眾功能的客戶詳細資料所必需。

客戶屬性結構描述以 [[!UICONTROL XDM 個人設定檔]](/help/xdm/classes/individual-profile.md)類別表示，其中包括以下欄位群組：

+++個人聯絡詳細資料 (欄位群組)

[個人聯絡詳細資料](/help/xdm/field-groups/profile/personal-contact-details.md)是 XDM 個人設定檔類別的標準結構描述欄位群組，主要在描述個人的聯絡資訊。

| 欄位 | 需求 | 說明 |
| --- | --- | --- |
| `mobilePhone.number` | 必要 | 個人手機號碼，用來發送 SMS。 |
| `personalEmail.address` | 必要 | 個人電子郵件地址。 |

+++

+++外部來源系統稽核詳細資料 (欄位群組)

[外部來源系統稽核屬性](/help/xdm/data-types/external-source-system-audit-attributes.md)是一種標準的體驗資料模式 (XDM) 資料類型，用於擷取外部來源系統的稽核詳細資料。

+++

+++同意和偏好設定欄位群組 (欄位群組)

此 [同意和偏好設定](/help/xdm/field-groups//profile/consents.md) 欄位群組提供單一物件型別欄位「同意」，以擷取同意和偏好設定資訊。

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

此結構描述是用來安排和引用構成發生在您網站和/或關聯數位平台上客戶活動的事件資料。此資料通常會內嵌至 [!DNL Adobe Experience Platform] via [Web SDK](/help/edge/home.md) 且是參考各種用於觸發歷程、詳細線上客戶分析和增強受眾功能的瀏覽和轉換事件所必需的。

客戶數位交易結構描述是由 [[!UICONTROL XDM ExperienceEvent]](/help/xdm/classes/experienceevent.md) 類別。

+++XDM ExperienceEvent （類別）

| 欄位 | 需求 | 說明 |
| --- | --- | --- |
| `_id` | 必填 | 唯一識別內嵌至的個別事件 [!DNL Adobe Experience Platform]. |
| `timestamp` | 必要 | 事件發生時間的ISO 8601時間戳記，格式如RFC 3339第5.6節所述。此時間戳記必須發生在過去。 |
| `eventType` | 必要 | 指出事件類別型別的字串。 |

+++

此 [[!UICONTROL XDM ExperienceEvent]](/help/xdm/classes/experienceevent.md) 類別包括下列欄位群組：

+++一般使用者 ID 詳細資料 (欄位群組)

此 [一般使用者ID詳細資訊](/help/xdm/field-groups/event/enduserids.md) 欄位群組是用來說明個人在多個Adobe應用程式中的身分資訊。

| 欄位 | 需求 | 說明 |
| --- | --- | --- |
| `endUserIDs._experience.emailid.authenticatedState` | 必要 | 一般使用者電子郵件地址 ID 驗證狀態。 |
| `endUserIDs._experience.emailid.id` | 必要 | 一般使用者電子郵件地址 ID。 |
| `endUserIDs._experience.emailid.namespace.code` | 必要 | 一般使用者電子郵件地址 ID 命名空間代碼。 |
| `endUserIDs._experience.mcid.authenticatedState` | 必要 | [!DNL Adobe] Marketing Cloud ID (MCID) 驗證狀態。MCID 現在稱為 Experience Cloud ID (ECID)。 |
| `endUserIDs._experience.mcid.id` | 必要 | [!DNL Adobe] Marketing Cloud ID (MCID)。MCID 現在稱為 Experience Cloud ID (ECID)。 |
| `endUserIDs._experience.mcid.namespace.code` | 必要 | [!DNL Adobe] Marketing Cloud ID (MCID) 命名空間代碼。 |

+++

+++外部來源系統稽核詳細資料 (欄位群組)

外部來源系統稽核屬性是一種標準體驗資料模式 (XDM) 的資料類型，這模式會擷取外部來源系統的稽核詳細資料。

+++

#### 客戶離線交易結構描述

此結構描述是用來安排和引用構成發生在您網站以外平台上客戶活動的事件資料。該資料通常是從 POS (或類似系統) 被擷取至 [!DNL Adobe Experience Platform]，且大部份通常會透過 API 連線串流至平台。其目的是參考各種離線轉換事件，這些事件用於觸發歷程、深層線上和離線客戶分析，以及增強受眾功能。

客戶離線交易結構描述會以 [[!UICONTROL XDM ExperienceEvent]](/help/xdm/classes/experienceevent.md) 類別。

+++XDM ExperienceEvent （類別）

| 欄位 | 需求 | 說明 |
| --- | --- | --- |
| `_id` | 必填 | 唯一識別內嵌至的個別事件 [!DNL Adobe Experience Platform]. |
| `timestamp` | 必要 | 事件發生時間的ISO 8601時間戳記，格式如RFC 3339第5.6節所述。此時間戳記必須發生在過去。 |
| `eventType` | 必要 | 指出事件類別型別的字串。 |

+++

此 [[!UICONTROL XDM ExperienceEvent]](/help/xdm/classes/experienceevent.md) 類別包括下列欄位群組：

+++商務詳細資料 (欄位群組)

此 [商業細節](/help/xdm/field-groups/event/commerce-details.md) 欄位群組用於說明商業資料，例如產品資訊（SKU、名稱、數量）和標準購物車操作（訂購、結帳、捨棄）。

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

[個人聯絡詳細資料](/help/xdm/field-groups/profile/personal-contact-details.md)是 XDM 個人設定檔類別的標準結構描述欄位群組，主要在描述個人的聯絡資訊。

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
>如果您使用 [[!DNL Adobe Analytics Source Connector]](/help/sources/connectors/adobe-applications/analytics.md)，這是一個實施選項。

此結構描述是用來安排和引用構成發生在您網站和/或關聯數位平台上客戶活動的事件資料。此結構描述類似於「客戶數位交易」結構描述，但不同之處在於其適用時機 [Web SDK](/help/edge/home.md) 不是資料收集的選項；因此，當您使用 [!DNL Adobe Analytics Source Connector] 將您的線上資料傳送到 [!DNL Adobe Experience Platform] 作為主要或次要資料流。

此 [!DNL Adobe] Web聯結器結構描述是由 [[!UICONTROL XDM ExperienceEvent]](/help/xdm/classes/experienceevent.md) 類別。

+++XDM ExperienceEvent （類別）

| 欄位 | 需求 | 說明 |
| --- | --- | --- |
| `_id` | 必填 | 唯一識別內嵌至的個別事件 [!DNL Adobe Experience Platform]. |
| `timestamp` | 必要 | 事件發生時間的ISO 8601時間戳記，格式如RFC 3339第5.6節所述。此時間戳記必須發生在過去。 |
| `eventType` | 必要 | 指出事件類別型別的字串。 |

+++

此 [[!UICONTROL XDM ExperienceEvent]](/help/xdm/classes/experienceevent.md) 類別包括下列欄位群組：

+++Adobe Analytics ExperienceEvent 範本 (欄位群組)

此 [Adobe Analytics ExperienceEvent](/help/xdm/field-groups/event/analytics-full-extension.md) 欄位群組會擷取Adobe Analytics所收集的一般量度。

| 欄位 | 需求 | 說明 |
| --- | --- | --- |
| `endUserIDs._experience.emailid.authenticatedState` | 必要 | 一般使用者電子郵件地址 ID 驗證狀態。 |
| `endUserIDs._experience.emailid.id` | 必要 | 一般使用者電子郵件地址 ID。 |
| `endUserIDs._experience.emailid.namespace.code` | 必要 | 一般使用者電子郵件地址 ID 命名空間代碼。 |
| `endUserIDs._experience.mcid.authenticatedState` | 必要 | [!DNL Adobe] Marketing Cloud ID (MCID) 驗證狀態。MCID 現在稱為 Experience Cloud ID (ECID)。 |
| `endUserIDs._experience.mcid.id` | 必要 | [!DNL Adobe] Marketing Cloud ID (MCID)。MCID 現在稱為 Experience Cloud ID (ECID)。 |
| `endUserIDs._experience.mcid.namespace.code` | 必要 | [!DNL Adobe] Marketing Cloud ID (MCID) 命名空間代碼。 |

+++

+++外部來源系統稽核詳細資料 (欄位群組)

外部來源系統稽核屬性是一種標準體驗資料模式 (XDM) 的資料類型，此模式會擷取外部來源系統的稽核詳細資料。

+++

### 從結構描述建立資料集 {#create-datasets}

資料集是一組資料的儲存和管理結構。智慧型重新參與情境的每個結構描述都應該有自己的資料集。

如需深入了解如何從結構描述建立[資料集](/help/catalog/datasets/overview.md)，請參閱[資料集 UI 指南](/help/catalog/datasets/user-guide.md)。

>[!NOTE]
>
>與結構描述建立步驟類似，您需要啟用資料集以包含在即時客戶設定檔中。如需啟用資料集以用於即時客戶個人檔案的詳細資訊，請參閱以下教學課程： [將資料帶入即時客戶個人檔案](https://experienceleague.adobe.com/docs/platform-learn/tutorials/profiles/bring-data-into-the-real-time-customer-profile.html?lang=zh-Hant).

### 同意與資料控管 {#privacy-consent}

>[!IMPORTANT]
>
>法律規定必須讓客戶能夠取消訂閱來自品牌的通訊，以及確保遵循此選擇。 在[隱私權法規概觀](https://experienceleague.adobe.com/docs/experience-platform/privacy/regulations/overview.html)中，了解更多有關適用法律。

#### 同意原則

建立重新參與路徑時，請考慮新增下列專案 [同意原則](https://experienceleague.adobe.com/docs/platform-learn/data-collection/web-sdk/consent/overview.html)：

* 如果為 `consents.marketing.email.val = "Y"`，則可以發送電子郵件
* 如果為 `consents.marketing.sms.val = "Y"`，則可以發送 SMS
* 如果為 `consents.marketing.push.val = "Y"`，則可以推播
* 如果為 `consents.share.val = "Y"`，則可以進行廣告

#### 資料控管標籤和執行

建立重新參與路徑時，請考慮新增下列專案 [資料控管標籤](/help/data-governance/labels/overview.md)：

* 個人電子郵件地址可作直接可識別資料供運用，可識別或聯絡特定個人而非裝置。
   * `personalEmail.address = I1`

#### 資料使用原則

沒有 [資料使用原則](/help/data-governance/policies/overview.md) 放棄的產品瀏覽情境的必要專案。 不過，您應考量下列事項：

* 限制敏感資料
* 限制現場廣告
* 限制電子郵件目標定位
* 限制跨站台目標定位
* 限制將直接可識別資料與匿名資料相結合

### 建立對象 {#create-audience}

重新參與案例使用受眾來定義由個人資料存放區中的個人資料子集共用的特定屬性或行為，以將可行銷的人員群組與您的客戶群區分開來。 您可以在中以多種方式建立對象 [!DNL Adobe Experience Platform].

如需如何建立受眾的詳細資訊，請參閱 [audience service UI指南](https://experienceleague.adobe.com/docs/experience-platform/segmentation/ui/overview.html#create-audience).

如需深入了解如何直接組成[對象](/help/segmentation/home.md)，請參閱[對象組成 UI 指南](/help/segmentation/ui/audience-composition.md)。

如需如何透過平台衍生的對象定義來建立對象的詳細資訊，請參閱 [Audience Builder UI指南](/help/segmentation/ui/segment-builder.md).

>[!BEGINTABS]

>[!TAB 放棄的產品瀏覽情境]

建立此對象是為了加強經典的「購物車放棄」情境。雖然購物車放棄通常是著重在購物車新增但在特定時間內未接著購買的情形，但此類對象尋求較早參與，特別是在特定時間內於您網站上可能瀏覽過特定產品但未加入購物車且沒有後續活動的人。此對象有助於讓符合此納入標準的客戶「優先考慮」您的品牌，也可運用在數位屬性可能不同於傳統電子商務模式的客戶。

+++放棄的產品檢視，過去三天無參與

以下事件適用於放棄的產品瀏覽情境，即使用者於線上檢視產品，且未在接下來的3天內參與（網站造訪、應用程式造訪、線上購買、離線購買及加入購物車事件）。

設定此對象時需要以下欄位和條件：

* `eventType: commerce.productViews`
* 與 `THEN` （循序事件）排除 `eventType: commerce.procuctListAdds` 或 `application.launch` 或 `web.webpagedetails.pageViews` 或 `commerce.purchases` （包括線上和離線）
   * `Timestamp: > 3 days after productView`

+++

+++過去三天有參與的產品檢視

以下事件適用於放棄的產品瀏覽情境，即使用者於線上檢視產品，並在隨後3天內參與（網站造訪、應用程式造訪、線上購買、離線購買及新增至購物車事件）。

設定此對象時需要以下欄位和條件：

* `eventType: commerce.productViews`
* 與 `THEN` （循序事件）包括 `eventType: commerce.procuctListAdds` 或 `application.launch` 或 `web.webpagedetails.pageViews` 或 `commerce.purchases` （包括線上和離線）
   * `Timestamp: > 3 days after productView`

+++過去一天內的參與串流

以下事件適用於放棄的產品瀏覽情境，即使用者在過去1天內參與其中（網站造訪、應用程式造訪、線上購買、離線購買及加入購物車事件）。

設定此對象時需要以下欄位和條件：

* `eventType: commerce.procuctListAdds or application.launch or web.webpagedetails.pageViews or commerce.purchases`
   * `Timestamp: in last 1 day` （串流）

+++

+++過去三天的參與批次

以下事件適用於放棄的產品瀏覽情境，即使用者在過去3天內參與其中（網站造訪、應用程式造訪、線上購買、離線購買及加入購物車事件）。

設定此對象時需要以下欄位和條件：

* `EventType: commerce.procuctListAdds or application.launch or web.webpagedetails.pageViews or commerce.purchases`
   * `Timestamp: in last 3 days` （批次）

+++

>[!TAB 捨棄的購物車情境]

建立此對象是為了支持一般「購物車放棄」情境。其目的是找到將產品加入購物車但最後未購買的客戶。此對象不僅有助於您的客戶「最先想到」您的品牌，而且還有助於他們保留被遺棄而未繼續購買的產品。

下列事件適用於放棄購物車的情況，即使用者在1至4天前將產品新增至購物車，但未完成購買或清除購物車。

設定此對象時需要以下欄位和條件：

* `eventType: commerce.productListAdds`
   * `Timestamp: >= 1 days before now and <= 4 days before now `
* `eventType: commerce.purchases`
   * `Timestamp: <= 4 days before now`
* `eventType: commerce.productListRemovals`
   * `Timestamp: <= 4 days before now`

放棄的購物車情境的描述項顯示為：

`Include eventType = commerce.productListAdds between 30 min and 1440 minutes before now. exclude eventType = commerce.purchases 30 minutes before now OR eventType = commerce.productListRemovals AND Cart ID equals Product List Adds1 Cart ID (the inclusion event).`

>[!TAB 訂單確認案例]

此歷程不需要建立任何對象。

>[!ENDTABS]

### 歷程在 Adobe Journey Optimizer 中建立 {#journey-setup}

>[!NOTE]
>
>[!DNL Adobe Journey Optimizer] 並不涵蓋圖中顯示的所有內容。所有[付費媒體廣告](/help/destinations/catalog/social/overview.md)均在[!UICONTROL 目的地]中建立。

[[!DNL Adobe Journey Optimizer]](https://experienceleague.adobe.com/docs/journey-optimizer/using/orchestrate-journeys/journey.html) 協助您向其客戶傳送連結的、情境式和個人化體驗。客戶歷程是客戶與品牌互動的整個過程。每個使用案例歷程需要特定的資訊。以下列出每個歷程所需的精確資料。

>[!BEGINTABS]

>[!TAB 放棄的產品瀏覽情境]

放棄的產品瀏覽情境會鎖定網站和行動應用程式上放棄的產品瀏覽。<p>![客戶放棄的產品瀏覽案例高階視覺化概觀。](../intelligent-re-engagement/images/re-engagement-journey.png "客戶放棄的產品瀏覽案例高階視覺化概觀。"){width="1920" zoomable="yes"}</p>

+++事件

* 事件 1：產品檢視
   * 結構描述：客戶數位交易
   * 欄位：
      * `eventType`
   * 條件：
      * `eventType = commerce.productViews`
      * 欄位：
         * `commerce.productViews.id`
         * `commerce.productViews.value`
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

* 事件 2：加入購物車
   * 結構描述：客戶數位交易
   * 欄位：
      * `eventType`
   * 條件：
      * `eventType = commerce.productListAdds`
      * 欄位：
         * `commerce.productListAdds.id`
         * `commerce.productListAdds.value`
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

* 事件 3：品牌參與度
   * 結構描述：客戶數位交易
   * 欄位：
      * `eventType`
   * 條件：
      * `eventType in application.launch, commerce.purchases, web.webpagedetails.pageViews`
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
         * `commerce.purchases.id`
         * `commerce.purchases.value`
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

   * 檢查自上次訪客瀏覽產品以來至少有一次離線購買事件：
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

>[!TAB 捨棄的購物車情境]

捨棄的購物車案例會鎖定已放入購物車但尚未在網站和行動應用程式上購買的產品。<p>![客戶放棄購物車案例高階視覺化概觀。](../intelligent-re-engagement/images/abandoned-cart-journey.png "客戶放棄購物車案例高階視覺化概觀。"){width="1920" zoomable="yes"}</p>

+++事件

* 事件 2：加入購物車
   * 結構描述：客戶數位交易
   * 欄位：
      * `eventType`
   * 條件：
      * `eventType = commerce.productListAdds`
      * 欄位：
         * `commerce.productListAdds.id`
         * `commerce.productListAdds.value`
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

* 事件 4：網上購買
   * 結構描述：客戶數位交易
   * 欄位：
      * `eventType`
   * 條件：
      * `eventType = commerce.purchases`
      * 欄位：
         * `commerce.purchases.id`
         * `commerce.purchases.value`
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

* 事件 3：品牌參與度
   * 結構描述：客戶數位交易
   * 欄位：
      * `eventType`
   * 條件：
      * `eventType in application.launch, commerce.purchases, web.webpagedetails.pageViews`
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
         * `commerce.purchases.id`
         * `commerce.purchases.value`
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
   * `cartID` (購物車的 ID)
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

>[!TAB 訂單確認案例]

訂購確認案例聚焦於透過網站和行動應用程式進行的產品購買。<p>![客戶訂單確認案例高階視覺化概觀。](../intelligent-re-engagement/images/order-confirmation-journey.png "客戶訂單確認案例高階視覺化概觀。"){width="1920" zoomable="yes"}</p>

+++事件

* 事件 4：網上購買
   * 結構描述：客戶數位交易
   * 欄位：
      * `eventType`
   * 條件：
      * `eventType = commerce.purchases`
      * 欄位：
         * `commerce.purchases.id`
         * `commerce.purchases.value`
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

### 在目的地設定付費媒體廣告 {#paid-media-ads}

目的地框架用於付費媒體廣告。只要勾選同意，系統會發送到設定的各種目的地。若要了解更有關目的地，請參閱[目的地概觀](/help/destinations/home.md)文件。

#### 目的地所需資料

串流受眾匯出目標(例如Facebook、Google Customer Match、Google DV360)支援客戶資料中的各種身分：

* `personalEmail.address`
* `ECID`
* `mobilePhone.number`

捨棄購物車對象會評估為串流對象，因此可用於此使用案例的目的地架構。

* 串流/已觸發
   * [廣告](/help/destinations/catalog/advertising/overview.md)/[付費媒體和社交](/help/destinations/catalog/social/overview.md)
   * [行動](/help/destinations/catalog/mobile-engagement/overview.md)
   * [串流目的地](/help/destinations/catalog/streaming/http-destination.md)
   * [使用Destination SDK建立的自訂目的地。](/help/destinations/destination-sdk/overview.md)。如果您是Real-Time CDP Ultimate客戶，也可以建立私人帳戶 [使用Destination SDK的自訂目的地](/help/destinations/destination-sdk/overview.md#productized-and-custom-integrations)
