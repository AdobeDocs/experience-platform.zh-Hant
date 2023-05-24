---
keywords: Experience Platform；主題；熱門主題；UI;UI;XDM;XDM系統；經驗資料模型；經驗資料模型；資料模型；資料模型；資料模型；架構編輯器；架構編輯器；架構；架構；架構；建立；關係；參考；引用；
solution: Experience Platform
title: 使用架構編輯器定義兩個架構之間的關係
description: 本文檔提供了一個教程，用於使用Experience Platform用戶介面中的架構編輯器定義兩個架構之間的關係。
type: Tutorial
exl-id: feed776b-bc8d-459b-9700-e5c9520788c0
source-git-commit: 5caa4c750c9f786626f44c3578272671d85b8425
workflow-type: tm+mt
source-wordcount: '1109'
ht-degree: 9%

---

# 使用 [!DNL Schema Editor] {#relationship-ui}

>[!CONTEXTUALHELP]
>id="platform_schemas_relationships"
>title="方案關係"
>abstract="屬於不同類別的方案可藉由關係欄位建立內容連結，從而讓您能夠建置更複雜的分段規則。如需有關方案關係的詳細資訊，請查看此文件。"

>[!CONTEXTUALHELP]
>id="platform_xdm_1to1_reference_schema"
>title="參考方案"
>abstract="選取要建立關係的方案。此方案可能和目前方案屬於不同類別。如需有關方案關係的詳細資訊，請查看此文件。"

>[!CONTEXTUALHELP]
>id="platform_xdm_1to1_identity_namespace"
>title="參考身分識別命名空間"
>abstract="適用於參考方案的主要身分識別欄位的命名空間 (類型)。參考方案必須有一個已建立的主要身分識別欄位才能參與關係。如需有關方案關係的詳細資訊，請查看此文件。"

瞭解客戶之間的關係以及客戶與品牌之間通過各種渠道進行的互動是Adobe Experience Platform的重要部分。 在結構中定義這些關係 [!DNL Experience Data Model] (XDM)架構使您能夠對客戶資料獲得複雜的見解。

而架構關係可通過使用聯合架構和 [!DNL Real-Time Customer Profile]，這僅適用於共用同一類的方案。 要在屬於不同類的兩個架構之間建立關係，必須將專用關係欄位添加到源架構中，該源架構引用其他相關架構的標識。

本文檔提供了使用中的架構編輯器定義兩個架構之間的關係的教程 [!DNL Experience Platform] 用戶介面。 有關使用API定義架構關係的步驟，請參見上的教程 [使用方案註冊表API定義關係](relationship-api.md)。

>[!NOTE]
>
>有關如何在Adobe Real-time Customer Data PlatformB2B版中建立多對一關係的步驟，請參見上的指南 [建立B2B關係](./relationship-b2b.md)。

## 快速入門

本教程要求您對 [!DNL XDM System] 和架構編輯器 [!DNL Experience Platform] UI。 在開始本教程之前，請查看以下文檔：

* [XDM系統在Experience Platform](../home.md):XDM及其在XDM中的應用 [!DNL Experience Platform]。
* [架構組合的基礎](../schema/composition.md):介紹了XDM模式的構件。
* [使用 [!DNL Schema Editor]](create-schema-ui.md):本教程介紹使用 [!DNL Schema Editor]。

## 定義源和引用方案

預期您已經建立了將在關係中定義的兩個架構。 為了進行演示，本教程將建立組織忠誠計畫的成員之間的關係（在「」中定義）[!DNL Loyalty Members]&quot;架構及其最喜愛的酒店(定義於「[!DNL Hotels]&quot;架構)。

>[!IMPORTANT]
>
>要建立關係，兩個方案必須都定義了主標識並且都為 [!DNL Real-Time Customer Profile]。 請參閱 [啟用在配置檔案中使用的架構](./create-schema-ui.md#profile) 在架構建立教程中，如果您需要有關如何相應地配置架構的指導。

模式關係由 **源架構** 指向另一個欄位 **參考模式**。 在後續步驟中， &quot;[!DNL Loyalty Members]&quot;將是源架構，而&quot;[!DNL Hotels]&quot;將用作引用架構。

以下各節介紹在定義關係之前在本教程中使用的每個架構的結構。

### [!DNL Loyalty Members] 架構

源架構「」[!DNL Loyalty Members]」基於 [!DNL XDM Individual Profile] 類，包含描述忠誠計畫成員的欄位。 其中一個領域， `personalEmail.addess`，用作架構的主標識 [!UICONTROL 電子郵件] 命名空間。 如下所示 **[!UICONTROL 架構屬性]**，此架構已啟用，供使用 [!DNL Real-Time Customer Profile]。

![](../images/tutorials/relationship/loyalty-members.png)

### [!DNL Hotels] 架構

引用架構「[!DNL Hotels]&quot;基於自定義&quot;[!DNL Hotels]&quot;類，包含描述酒店的欄位。 為了參與關係，引用方案還必須定義並為 [!UICONTROL 配置檔案]。 在這個例子中， `_tenantId.hotelId`使用自定義「」作為架構的主標識[!DNL Hotel ID]&quot;標識命名空間。

![啟用配置檔案](../images/tutorials/relationship/hotels.png)

>[!NOTE]
>
>要瞭解如何建立自定義標識命名空間，請參閱 [Identity Service文檔](../../identity-service/namespaces.md#manage-namespaces)。

## 建立關係欄位組

>[!NOTE]
>
>只有在源架構沒有專用的字串類型欄位用作指向引用架構主標識的指針時，才需要此步驟。 如果此欄位已在源架構中定義，請跳至 [定義關係欄位](#relationship-field)。

為了定義兩個架構之間的關係，源架構必須有一個專用欄位，該欄位將指示引用架構的主標識。 可以通過建立新架構欄位組或擴展現有架構欄位組將此欄位添加到源架構。

對於 [!DNL Loyalty Members] 架構，新 `preferredHotel` 欄位將被添加，以指示忠誠會員為公司拜訪首選的酒店。 首先選擇加號表徵圖(**+**)。

![](../images/tutorials/relationship/loyalty-add-field.png)

在畫布中將顯示新的欄位佔位符。 下 **[!UICONTROL 欄位屬性]**，為欄位提供欄位名和顯示名，並將其類型設定為&quot;[!UICONTROL 字串]。 下 **[!UICONTROL 分配給]**，選擇要擴展的現有欄位組，或鍵入唯一名稱以建立新欄位組。 在此情況下，新的&quot;[!DNL Preferred Hotel]「 」欄位組已建立。

![](../images/tutorials/relationship/relationship-field-details.png)

完成後，選擇 **[!UICONTROL 應用]**。

![](../images/tutorials/relationship/relationship-field-apply.png)

已更新 `preferredHotel` 欄位出現在畫布中，位於 `_tenantId` 對象，因為它是自定義欄位。 選擇 **[!UICONTROL 保存]** 完成對架構的更改。

![](../images/tutorials/relationship/relationship-field-save.png)

## 為源方案定義關係欄位 {#relationship-field}

在源架構定義了專用引用欄位後，可以將其指定為關係欄位。

>[!NOTE]
>
>下面的步驟介紹如何使用畫布中的右滑軌控制項定義關係欄位。 如果您有訪問Real-Time CDPB2B版的權限，您還可以使用 [同一對話](./relationship-b2b.md#relationship-field) 建立多對一關係時。

選擇 `preferredHotel` 欄位，然後向下滾動 **[!UICONTROL 欄位屬性]** 直到 **[!UICONTROL 關係]** 的子菜單。 選中該複選框可顯示配置關係欄位所需的參數。

![](../images/tutorials/relationship/relationship-checkbox.png)

選擇的下拉清單 **[!UICONTROL 引用架構]** 並選擇關係的引用架構(&quot;[!DNL Hotels])。 下 **[!UICONTROL 引用標識命名空間]**，選擇引用架構的標識欄位的命名空間(在本例中，為「[!DNL Hotel ID]「)。 選擇 **[!UICONTROL 應用]** 的子菜單。

![](../images/tutorials/relationship/reference-schema-id-namespace.png)

的 `preferredHotel` 欄位現在在畫布中突出顯示為關係，顯示引用架構的名稱。 選擇 **[!UICONTROL 保存]** 保存更改並完成工作流。

![](../images/tutorials/relationship/relationship-save.png)

## 後續步驟

通過本教程，您已使用 [!DNL Schema Editor]。 有關如何使用API定義關係的步驟，請參見上的教程 [使用方案註冊表API定義關係](relationship-api.md)。
