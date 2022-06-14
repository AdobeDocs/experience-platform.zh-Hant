---
keywords: Experience Platform；主題；熱門主題；UI;UI;XDM;XDM系統；經驗資料模型；經驗資料模型；資料模型；資料模型；資料模型；架構編輯器；架構編輯器；架構；架構；架構；建立；關係；參考；引用；
solution: Experience Platform
title: 使用架構編輯器定義兩個架構之間的關係
description: 本文檔提供了一個教程，用於使用Experience Platform用戶介面中的架構編輯器定義兩個架構之間的關係。
topic-legacy: tutorial
type: Tutorial
exl-id: feed776b-bc8d-459b-9700-e5c9520788c0
source-git-commit: 90f055f2fbeb7571d2f7c1daf4ea14490069f2eb
workflow-type: tm+mt
source-wordcount: '1042'
ht-degree: 0%

---

# 使用 [!DNL Schema Editor]

>[!CONTEXTUALHELP]
>id="platform_schemas_relationships"
>title="架構關係"
>abstract="屬於不同類的架構可以通過關係欄位上下文連結，從而可以構建更複雜的分割規則。"
>text="See the documentation for more information on schema relationships."

>[!NOTE]
>
>如果您使用的是Real-time Customer Data PlatformB2B版，請參閱上的指南 [建立B2B關係](./relationship-b2b.md) 的雙曲餘切值。

瞭解客戶之間的關係以及客戶與品牌之間通過各種渠道進行的互動是Adobe Experience Platform的重要部分。 在結構中定義這些關係 [!DNL Experience Data Model] (XDM)架構使您能夠對客戶資料獲得複雜的見解。

而架構關係可通過使用聯合架構和 [!DNL Real-time Customer Profile]，這僅適用於共用同一類的方案。 要在屬於不同類的兩個架構之間建立關係，必須將專用關係欄位添加到引用目標架構標識的源架構中。

本文檔提供了使用中的架構編輯器定義兩個架構之間的關係的教程 [!DNL Experience Platform] 用戶介面。 有關使用API定義架構關係的步驟，請參見上的教程 [使用方案註冊表API定義關係](relationship-api.md)。

## 快速入門

本教程要求您對 [!DNL XDM System] 和架構編輯器 [!DNL Experience Platform] UI。 在開始本教程之前，請查看以下文檔：

* [XDM系統在Experience Platform](../home.md):XDM及其在XDM中的應用 [!DNL Experience Platform]。
* [架構組合的基礎](../schema/composition.md):介紹了XDM模式的構件。
* [使用 [!DNL Schema Editor]](create-schema-ui.md):本教程介紹使用 [!DNL Schema Editor]。

## 定義源和目標架構

預期您已經建立了將在關係中定義的兩個架構。 為了進行演示，本教程將建立組織忠誠計畫的成員之間的關係（在「」中定義）[!DNL Loyalty Members]&quot;架構及其最喜愛的酒店(定義於「[!DNL Hotels]&quot;架構)。

>[!IMPORTANT]
>
>要建立關係，兩個方案必須都定義了主標識並且都為 [!DNL Real-time Customer Profile]。 請參閱 [啟用在配置檔案中使用的架構](./create-schema-ui.md#profile) 在架構建立教程中，如果您需要有關如何相應地配置架構的指導。

模式關係由 **源架構** 是指 **目標架構**。 在後續步驟中， &quot;[!DNL Loyalty Members]&quot;將是源架構，而&quot;[!DNL Hotels]&quot;將用作目標架構。

為便於參考，以下各節介紹在定義關係之前在本教程中使用的每個架構的結構。

### [!DNL Loyalty Members] 架構

源架構「」[!DNL Loyalty Members]」基於 [!DNL XDM Individual Profile] 類，是在教程中為 [在UI中建立架構](create-schema-ui.md)。 它包括 `loyalty` 對象 `_tenantId` 命名空間，其中包含多個特定於忠誠度的欄位。 其中一個領域， `loyaltyId`，用作架構的主標識 [!UICONTROL 電子郵件] 命名空間。 如下所示 **[!UICONTROL 架構屬性]**，此架構已啟用，供使用 [!DNL Real-time Customer Profile]。

![](../images/tutorials/relationship/loyalty-members.png)

### [!DNL Hotels] 架構

目標架構「」[!DNL Hotels]&quot;基於自定義&quot;[!DNL Hotels]&quot;類，包含描述酒店的欄位。

![](../images/tutorials/relationship/hotels.png)

要參與關係，目標架構必須具有主標識。 在此示例中， `hotelId` 欄位用作主標識，使用自定義「Hotel ID」標識命名空間。

![酒店主要身份](../images/tutorials/relationship/hotel-identity.png)

>[!NOTE]
>
>要瞭解如何建立自定義標識命名空間，請參閱 [Identity Service文檔](../../identity-service/namespaces.md#manage-namespaces)。

設定主標識後，必須為 [!DNL Real-time Customer Profile]。

![啟用配置檔案](../images/tutorials/relationship/hotel-profile.png)

## 建立關係架構欄位組

>[!NOTE]
>
>僅當源架構沒有專用字串類型欄位用作對目標架構的引用時，才需要此步驟。 如果此欄位已在源架構中定義，請跳至 [定義關係欄位](#relationship-field)。

為了定義兩個方案之間的關係，源方案必須具有一個專用欄位，以用作對目標方案的引用。 可以通過建立新架構欄位組將此欄位添加到源架構。

通過選擇 **[!UICONTROL 添加]** 的 **[!UICONTROL 欄位組]** 的子菜單。

![](../images/tutorials/relationship/loyalty-add-field-group.png)

的 [!UICONTROL 添加欄位組] 對話框。 從此處，選擇 **[!UICONTROL 建立新欄位組]**。 在顯示的文本欄位中，輸入新欄位組的顯示名稱和說明。 選擇 **[!UICONTROL 添加欄位組]** 的子菜單。

![](../images/tutorials/relationship/create-field-group.png)

畫布重新顯示為&quot;[!DNL Favorite Hotel]「 」出現在 **[!UICONTROL 欄位組]** 的子菜單。 選擇欄位組名稱，然後選擇 **[!UICONTROL 添加欄位]** 根級別旁邊 `Loyalty Members` 的子菜單。

![](../images/tutorials/relationship/loyalty-add-field.png)

在畫布中的 `_tenantId` 命名空間。 下 **[!UICONTROL 欄位屬性]**，為欄位提供欄位名和顯示名，並將其類型設定為&quot;[!UICONTROL 字串]。

![](../images/tutorials/relationship/relationship-field-details.png)

完成後，選擇 **[!UICONTROL 應用]**。

![](../images/tutorials/relationship/relationship-field-apply.png)

已更新 `favoriteHotel` 欄位。 選擇 **[!UICONTROL 保存]** 完成對架構的更改。

![](../images/tutorials/relationship/relationship-field-save.png)

## 為源方案定義關係欄位 {#relationship-field}

在源架構定義了專用引用欄位後，可以將其指定為關係欄位。

選擇 `favoriteHotel` 欄位，然後向下滾動 **[!UICONTROL 欄位屬性]** 直到 **[!UICONTROL 關係]** 的子菜單。 選中該複選框可顯示配置關係欄位所需的參數。

![](../images/tutorials/relationship/relationship-checkbox.png)

選擇的下拉清單 **[!UICONTROL 引用架構]** 並選擇關係的目標架構(&quot;[!DNL Hotels])。 如果為 [!DNL Profile]，也請參見Wiki頁。 **[!UICONTROL 引用標識命名空間]** 欄位將自動設定為目標架構的主標識的命名空間。 如果架構未定義主標識，則必須從下拉菜單中手動選擇計畫使用的命名空間。 選擇 **[!UICONTROL 應用]** 的子菜單。

![](../images/tutorials/relationship/reference-schema-id-namespace.png)

的 `favoriteHotel` 欄位現在在畫布中突出顯示為關係，顯示目標架構的名稱和引用標識名稱空間。 選擇 **[!UICONTROL 保存]** 保存更改並完成工作流。

![](../images/tutorials/relationship/relationship-save.png)

## 後續步驟

通過本教程，您已使用 [!DNL Schema Editor]。 有關如何使用API定義關係的步驟，請參見上的教程 [使用方案註冊表API定義關係](relationship-api.md)。
