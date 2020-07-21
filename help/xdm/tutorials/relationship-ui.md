---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: 使用架構架構編輯器定義兩個架構之間的關係
topic: tutorials
translation-type: tm+mt
source-git-commit: 1445646be8fa3416a34408205eadca0a792290c6
workflow-type: tm+mt
source-wordcount: '811'
ht-degree: 0%

---


# 使用 [!DNL Schema Editor]

Adobe Experience Platform的重要部分，在於能夠跨不同通道瞭解客戶之間的關係以及客戶與品牌之間的互動。 在(XDM)結構中定義這 [!DNL Experience Data Model] 些關係，可讓您獲得客戶資料的複雜見解。

本文檔提供了教程，用於使用用戶介面中的定義組織定義的兩個方案之間的一對一 [!DNL Schema Editor] 關係 [!DNL Experience Platform] 。 有關使用API定義方案關係的步驟，請參閱使用方案注 [冊表API定義關係的教程](relationship-api.md)。

## 快速入門

本教學課程需要對 [!DNL XDM System] UI [!DNL Schema Editor] 和 [!DNL Experience Platform] 進行有效瞭解。 在開始本教學課程之前，請先閱讀下列檔案：

* [Experience Platform中的XDM系統](../home.md): XDM及其在Experience Platform中的實作概觀。
* [架構構成基礎](../schema/composition.md): 介紹XDM模式的構建塊。
* [使用架構編輯器建立架構](create-schema-ui.md): 教學課程，涵蓋使用的基本知識 [!DNL Schema Editor]。

## 定義源和目標方案

預期您已經建立了將在關係中定義的兩個方案。 為了進行示範，本教學課程會在組織的忠誠度方案(在「忠誠度會員」架構中定義)的成員與其最愛的酒店（在「酒店」架構中定義）之間建立關係。

模式關係由源模式 **[!UICONTROL 表示]** ，該源模式具有引用目標模式內另一欄位的 **[!UICONTROL 欄位]**。 在後續步驟中，「[!UICONTROL Loyalty Members]」將是來源結構描述，而「Hotels」將充當目標結構描述。

為便於參考，以下幾節將介紹在定義關係之前本教程中使用的每個架構的結構。

### [!UICONTROL 忠誠度成員] 架構

源模式&quot;[!UICONTROL Loyalty Members]&quot;是在教程中為在UI中建立 [模式而構建的模式](create-schema-ui.md)。 它在其「[!UICONTROL \_tenantId]」命名空間下包含「loyalty」物件，其中包含數個忠誠度特定欄位。 其中一個欄位「[!UICONTROL loyaltyId]」是「電子郵件」命名空間下之結構的主要身分識別。 如「架構屬 _性」下所示_，此架構已啟用供使用 [!DNL Real-time Customer Profile](../../profile/home.md)。

![](../images/tutorials/relationship/loyalty-members.png)

### 酒店模式

目標架構「[!UICONTROL Hotels]」包含描述酒店的欄位，包括其地址、品牌、房間數和星級等級。 &quot;[!UICONTROL hotelId]&quot;欄位是「ECID」命名空間下之架構的主要身分。 與「忠[!UICONTROL 誠會員]」不同，此架構未啟用 [!DNL Real-time Customer Profile]。

![](../images/tutorials/relationship/hotels.png)

## 建立關係混合

>[!NOTE]
>
>只有在源架構沒有專用字串類型欄位用作另一個架構的引用時，才需要此步驟。 如果此欄位已在源方案中定義，請跳至定義關係欄位 [的下一步](#relationship-field)。

為了定義兩個方案之間的關係，源方案必須具有專用欄位以用作目標方案的引用。 通過建立新混音，可以將此欄位添加到源模式。

首先，按一 **[!UICONTROL 下]** 「Mixins」區 _段中的「新增_ 」。

![](../images/tutorials/relationship/loyalty-add-mixin.png)

此時將 [!UICONTROL _顯示「添加混音&#x200B;_]」對話框。 在這裡，按一下「**[!UICONTROL &#x200B;建立新Mixin」]**。 在出現的文字欄位中，輸入新混音的顯示名稱和說明。 完成後**[!UICONTROL &#x200B;按一下「新增&#x200B;]**Mixin」。

<img src="../images/tutorials/relationship/loyalty-create-new-mixin.png" width="750"><br>

畫布會重新顯示，「[!UICONTROL Favorite Hotel]」(最愛的酒店 _)會出現_ 在Mixins區。 按一下混音名稱，然後按一 **[!UICONTROL 下根層級]** 「忠誠會員」欄位旁的「新增欄位」。

![](../images/tutorials/relationship/loyalty-add-field.png)

畫布中會在&quot;[!UICONTROL \_tenantId]&quot;命名空間下顯示新欄位。 在「 [!UICONTROL _欄位屬性&#x200B;_]」下，提供欄位名稱和顯示名稱，並將其類型設為「字[!UICONTROL 串]」。

![](../images/tutorials/relationship/relationship-field-details.png)

完成後，按一下「 **[!UICONTROL 套用]**」。

![](../images/tutorials/relationship/relationship-field-apply.png)

更新的「[!UICONTROL favoriteHotel]」欄位會出現在畫布中。 按一下 **[!UICONTROL 保存]** ，完成對架構的更改。

![](../images/tutorials/relationship/relationship-field-save.png)

## 為源方案定義關係欄位 {#relationship-field}

在源架構定義了專用的參考欄位後，可以將其指定為關係欄位。

按一下畫布中的參考欄位，然後向下捲動至欄位屬 _[!UICONTROL 性下方]_，直到出現****關係核取方塊。 選中該複選框可顯示配置關係欄位所需的參數。

![](../images/tutorials/relationship/relationship-checkbox.png)

按一下「參 **[!UICONTROL 考結構]** 」下拉式清單，並選取關係的目標結構(本例中為「[!UICONTROL Hotels]」)。 如果目標方案啟用了聯合功能，則「參考身份名稱空間 **** 」欄位將自動設定為目標方案的主標識的名稱空間。 如果架構未定義主標識，則必須從下拉菜單中手動選擇要使用的命名空間。 Click **[!UICONTROL Apply]** when finished.

![](../images/tutorials/relationship/reference-schema-id-namespace.png)

欄位在畫布中會以關係的形式顯示，顯示目標架構的名稱和參考身分名稱空間。 按一 **[!UICONTROL 下「儲存]** 」以儲存變更並完成工作流程。

![](../images/tutorials/relationship/relationship-save.png)

## 後續步驟

在本教學課程之後，您已使用成功建立兩個結構描述之間的一對一關係 [!DNL Schema Editor]。 有關如何使用API定義關係的步驟，請參閱使用「方案註冊 [表API」定義關係的教程](relationship-api.md)。