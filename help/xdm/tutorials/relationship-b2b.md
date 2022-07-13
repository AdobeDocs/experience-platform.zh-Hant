---
title: 定義Real-time Customer Data PlatformB2B版中兩個架構之間的關係
description: 瞭解如何在Real-time Customer Data PlatformB2B版中定義兩個架構之間的多對一關係。
exl-id: 14032754-c7f5-46b6-90e6-c6e99af1efba
source-git-commit: a95e5cf02e993d6c761abd74c98c0967a89eb678
workflow-type: tm+mt
source-wordcount: '1401'
ht-degree: 0%

---

# 在Real-time Customer Data PlatformB2B版中定義兩個架構之間的多對一關係

>[!CONTEXTUALHELP]
>id="platform_xdm_b2b_reference_schema"
>title="引用架構"
>abstract="選擇要與建立關係的架構。 根據架構的類，它還可能與B2B上下文中的其他實體存在現有關係。 請參見文檔以瞭解B2B架構類如何彼此關聯。"

Real-time Customer Data PlatformB2B版提供了幾個體驗資料模型(XDM)類，這些類捕獲基本B2B資料實體，包括 [帳戶](../classes/b2b/business-account.md)。 [機會](../classes/b2b/business-opportunity.md)。 [活動](../classes/b2b/business-campaign.md)。 通過基於這些類構建架構並啟用它們以用於 [即時客戶概要資訊](../../profile/home.md)，可以將來自不同源的資料合併到稱為聯合架構的統一表示中。

但是，聯合架構只能包含由共用同一類的架構捕獲的欄位。 這是架構關係的來源。 通過在B2B架構中實現關係，您可以描述這些業務實體如何相互關聯，並可以在下游分段使用案例中包括來自多個類的屬性。

下圖提供了一個示例，說明在基本實現中不同的B2B類如何彼此關聯：

![B2B類關係](../images/tutorials/relationship-b2b/classes.png)

本教程介紹在即時CDP B2B版中定義兩個架構之間多對一關係的步驟。

>[!NOTE]
>
>如果您沒有使用Real-time Customer Data PlatformB2B版或想建立一對一關係，請參閱上的指南 [建立一對一關係](./relationship-ui.md) 的雙曲餘切值。
>
>本教程重點介紹如何在平台UI中手動建立B2B架構之間的關係。 如果從B2B源連接引入資料，則可以使用自動生成實用程式來建立所需的架構、標識和關係。 有關B2B命名空間和架構的詳細資訊，請參閱源文檔 [使用自動生成實用程式](../../sources/connectors/adobe-applications/marketo/marketo-namespaces.md)。

## 快速入門

本教程要求您對 [!DNL XDM System] 和架構編輯器 [!DNL Experience Platform] UI。 在開始本教程之前，請查看以下文檔：

* [XDM系統在Experience Platform](../home.md):XDM及其在XDM中的應用 [!DNL Experience Platform]。
* [架構組合的基礎](../schema/composition.md):介紹了XDM模式的構件。
* [使用 [!DNL Schema Editor]](create-schema-ui.md):本教程介紹如何在UI中生成和編輯架構的基本知識。

## 定義源和目標架構

預期您已經建立了將在關係中定義的兩個架構。 為了進行演示，本教程將建立業務機會（在「 」中定義）之間的關係[!DNL Opportunities]&quot;架構及其關聯的業務帳戶(在&quot;[!DNL Accounts]&quot;架構)。

模式關係由 **源架構** 引用的 **目標架構**。 在後續步驟中， &quot;[!DNL Opportunities]&quot;用作源架構，而&quot;[!DNL Accounts]&quot;用作目標架構。

### 理解B2B關係中的恆等式

>[!CONTEXTUALHELP]
>id="platform_xdm_b2b_identity_namespace"
>title="引用標識命名空間"
>abstract="引用架構的主標識欄位的命名空間（類型）。 引用架構必須具有已建立的主標識欄位才能參與關係。 有關B2B關係中的標識的詳細資訊，請參閱文檔。"

要建立關係，目標架構必須具有已定義的主標識。 為B2B實體設定主標識時，請記住，如果您跨不同系統或位置收集基於字串的實體ID，則它們可能會重疊，這可能導致平台中的資料衝突。

為此，所有標準B2B類都包含符合 [[!UICONTROL B2B源] 資料類型](../data-types/b2b-source.md)。 此資料類型提供B2B實體的字串標識符的欄位以及有關標識符源的其他上下文資訊。 其中一個領域， `sourceKey`，連接資料類型中其他欄位的值，以生成實體的唯一標識符。 此欄位應始終用作B2B實體架構的主標識。

![sourceKey欄位](../images/tutorials/relationship-b2b/sourcekey.png)

>[!NOTE]
>
>當 [將XDM欄位設定為標識](../ui/fields/identity.md)，必須提供標識名稱空間以在下定義標識。 這可以是Adobe提供的標準命名空間，也可以是組織定義的自定義命名空間。 在實踐中，命名空間只是一個上下文字串，可以設定為任何您喜歡的值，前提是它對於組織對標識類型的分類有意義。 請參閱 [標識命名空間](../../identity-service/namespaces.md) 的子菜單。

為便於參考，以下各節介紹在定義關係之前在本教程中使用的每個架構的結構。 請注意在架構結構中定義了主要標識的位置以及它們使用的自定義命名空間。

### [!DNL Opportunities] 架構

源架構「」[!DNL Opportunities]」基於 [!UICONTROL XDM業務機會] 類。 類提供的一個欄位， `opportunityKey`，用作架構的標識符。 具體而言， `sourceKey` 欄位 `opportunityKey` 對象在名為的自定義命名空間下設定為架構的主標識 [!DNL B2B Opportunity]。

如下所示 **[!UICONTROL 架構屬性]**，此架構已啟用，供使用 [!DNL Real-time Customer Profile]。

![機會架構](../images/tutorials/relationship-b2b/opportunities.png)

### [!DNL Accounts] 架構

目標架構「」[!DNL Accounts]」基於 [!UICONTROL XDM帳戶] 類。 根級別 `accountKey` 欄位包含 `sourceKey` 在稱為 [!DNL B2B Account]。 此架構也已啟用，以便在配置檔案中使用。

![帳戶架構](../images/tutorials/relationship-b2b/accounts.png)

## 為源方案定義關係欄位 {#relationship-field}

>[!CONTEXTUALHELP]
>id="platform_xdm_b2b_relationship_name_current"
>title="當前架構的關係名稱"
>abstract="描述從當前架構到引用架構的關係（例如「相關帳戶」）的標籤。 此標籤用於配置檔案和分段，以向相關B2B實體的資料提供上下文。 有關構建B2B架構關係的詳細資訊，請參閱文檔。"

>[!CONTEXTUALHELP]
>id="platform_xdm_b2b_relationship_name_reference"
>title="引用架構中的關係名稱"
>abstract="描述從引用架構到當前架構的關係的標籤（例如，「Related Opportunities」）。 此標籤用於配置檔案和分段，以向相關B2B實體的資料提供上下文。 有關構建B2B架構關係的詳細資訊，請參閱文檔。"

為了定義兩個方案之間的關係，源方案必須有一個引用目標方案主標識的專用欄位。 標準B2B類包括用於常見相關業務實體的專用源關鍵字欄位。 例如， [!UICONTROL XDM業務機會] 類包含相關帳戶的源關鍵字欄位(`accountKey`)和相關活動(`campaignKey`)。 但是，您也可以添加其他 [!UICONTROL B2B源] 使用自定義欄位組（如果需要的元件多於預設元件）將欄位輸入架構。

>[!NOTE]
>
>當前，只能從源架構到目標架構定義多對一和一對一關係。 對於一對多關係，必須在表示「many」的架構中定義關係欄位。

要設定關係欄位，請選擇箭頭表徵圖(![箭頭表徵圖](../images/tutorials/relationship-b2b/arrow.png))。 對於 [!DNL Opportunities] 架構，這是 `accountKey.sourceKey` 欄位，因為目標是與帳戶建立多對一關係。

![關係按鈕](../images/tutorials/relationship-b2b/relationship-button.png)

此時將顯示一個對話框，用於指定關係的詳細資訊。 關係類型自動設定為 **[!UICONTROL 多對一]**。

![關係對話框](../images/tutorials/relationship-b2b/relationship-dialog.png)

下 **[!UICONTROL 引用架構]**，使用搜索欄查找目標架構的名稱。 突出顯示目標架構的名稱時， **[!UICONTROL 引用標識命名空間]** 欄位將自動更新到架構的主標識的命名空間。

![引用架構](../images/tutorials/relationship-b2b/reference-schema.png)

下 **[!UICONTROL 當前架構中的關係名稱]** 和 **[!UICONTROL 引用架構中的關係名稱]**，分別在源架構和目標架構的上下文中為關係提供友好名稱。 完成後，選擇 **[!UICONTROL 保存]** 應用更改並保存架構。

![關係名稱](../images/tutorials/relationship-b2b/relationship-name.png)

畫布重新出現，關係欄位現在用您先前提供的友好名稱標籤。 關係名稱也列在左滑軌下以便參考。

![已應用關係](../images/tutorials/relationship-b2b/relationship-applied.png)

如果查看目標架構的結構，則關係標籤將出現在架構的主標識欄位旁邊和左側欄中。

![目標架構關係標籤](../images/tutorials/relationship-b2b/destination-relationship.png)

## 後續步驟

通過本教程，您已使用 [!DNL Schema Editor]。 一旦使用基於這些架構的資料集進行資料攝取並且資料已在配置檔案資料儲存中激活，您就可以使用兩個架構中的屬性來進行多類分段使用案例。 有關詳細資訊，請參見Real-time CDP B2B Edition上的文檔。
