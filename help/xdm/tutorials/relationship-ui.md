---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: 使用架構架構編輯器定義兩個架構之間的關係
topic: tutorials
translation-type: tm+mt
source-git-commit: bd9884a24c5301121f30090946ab24d9c394db1b
workflow-type: tm+mt
source-wordcount: '836'
ht-degree: 0%

---


# 使用架構編輯器定義兩個架構之間的關係

Adobe Experience Platform的重要部分，在於能夠跨不同通道瞭解客戶之間的關係以及客戶與品牌之間的互動。 在體驗資料模型(XDM)結構中定義這些關係，可讓您獲得客戶資料的複雜見解。

本檔案提供教學課程，可讓您使用Experience Platform使用者介面中的「架構編輯器」，定義組織所定義的兩個架構之間的一對一關係。 有關使用API定義方案關係的步驟，請參閱使用方案注 [冊表API定義關係的教程](relationship-api.md)。

## 快速入門

本教學課程需要在Experience Platform UI中瞭解XDM系統和架構編輯器。 在開始本教學課程之前，請先閱讀下列檔案：

* [Experience Platform中的XDM系統](../home.md): XDM及其在Experience Platform中的實作概觀。
* [架構構成基礎](../schema/composition.md): 介紹XDM模式的構建塊。
* [使用架構編輯器建立架構](create-schema-ui.md): 教學課程，介紹使用架構編輯器的基本知識。

## 定義源和目標方案

預期您已經建立了將在關係中定義的兩個方案。 為了進行示範，本教學課程會在組織的忠誠度方案（在「忠誠度會員」架構中定義）的成員與其最愛的酒店（在「酒店」架構中定義）之間建立關係。

模式關係由源模式 **表示** ，該源模式具有引用目標模式內另一欄位的 **欄位**。 在後續步驟中，「忠誠度會員」將是來源方案，而「酒店」將充當目標方案。

為便於參考，以下幾節將介紹在定義關係之前本教程中使用的每個架構的結構。

### 忠誠度成員結構

源模式&quot;Loyalty Members&quot;是在教程中為在UI中建立 [模式而構建的模式](create-schema-ui.md)。 它在其&quot;\_tenantId&quot;命名空間下包含「忠誠度」物件，其中包含數個忠誠度特定欄位。 其中一個欄位&quot;loyaltyId&quot;是「電子郵件」名稱空間下之結構的主要身分識別。 如「方案屬 _性」下所示_，此方案已啟用，可用於 [即時客戶描述檔](../../profile/home.md)。

![](../images/tutorials/relationship/loyalty-members.png)

### 酒店模式

目的地結構「酒店」包含描述酒店的欄位，包括其地址、品牌、房間數和星級等級。 &quot;hotelId&quot;欄位是「ECID」命名空間下之結構的主要身分識別。 與「忠誠會員」不同，此結構未啟用即時客戶個人檔案。

![](../images/tutorials/relationship/hotels.png)

## 建立關係混合

>[!NOTE]
>
>只有在源架構沒有專用字串類型欄位用作另一個架構的引用時，才需要此步驟。 如果此欄位已在源方案中定義，請跳至定義關係欄位 [的下一步](#relationship-field)。

為了定義兩個方案之間的關係，源方案必須具有專用欄位以用作目標方案的引用。 通過建立新混音，可以將此欄位添加到源模式。

首先，按一 **下** 「Mixins」區 _段中的「新增_ 」。

![](../images/tutorials/relationship/loyalty-add-mixin.png)

此時將 _顯示「添加混音_ 」對話框。 在這裡，按一下「 **建立新Mixin」**。 在出現的文字欄位中，輸入新混音的顯示名稱和說明。 完成後 **按一下「新增** Mixin」。

<img src="../images/tutorials/relationship/loyalty-create-new-mixin.png" width="750"><br>

畫布會重新顯示，而「忠誠度關係」會出現在「 _Mixins_ 」區段。 按一下混音名稱，然後按一 **下根層級** 「忠誠度成員」欄位旁的「新增欄位」。

![](../images/tutorials/relationship/loyalty-add-field.png)

畫布中會在&quot;\_tenantId&quot;命名空間下顯示新欄位。 在「 _欄位屬性_」下，提供欄位名稱和顯示名稱，並將其類型設為「字串」。

![](../images/tutorials/relationship/relationship-field-details.png)

完成後，按一下「 **套用**」。

![](../images/tutorials/relationship/relationship-field-apply.png)

更新的「loyaltyRelationship」欄位會出現在畫布中。 按一下 **保存** ，完成對架構的更改。

![](../images/tutorials/relationship/relationship-field-save.png)

## 為源方案定義關係欄位 {#relationship-field}

在源架構定義了專用的參考欄位後，可以將其指定為關係欄位。

按一下畫布中的參考欄位，然後向下捲動至欄位屬 _性下方_ ，直到出現 **** 關係核取方塊。 選中該複選框可顯示配置關係欄位所需的參數。

![](../images/tutorials/relationship/relationship-checkbox.png)

按一下「參 **考結構」下拉式清單** ，並選取關係的目標結構（此範例中為「Hotels」）。 如果目標方案啟用了聯合功能，則「參考身份名稱空間 **** 」欄位將自動設定為目標方案的主標識的名稱空間。 如果架構未定義主標識，則必須從下拉菜單中手動選擇要使用的命名空間。 Click **Apply** when finished.

![](../images/tutorials/relationship/reference-schema-id-namespace.png)

欄位在畫布中會以關係的形式顯示，顯示目標架構的名稱和參考身分名稱空間。 按一 **下「儲存** 」以儲存變更並完成工作流程。

![](../images/tutorials/relationship/relationship-save.png)

## 後續步驟

在本教程之後，您已使用方案編輯器成功建立了兩個方案之間的一對一關係。 有關如何使用API定義關係的步驟，請參閱使用「方案註冊 [表API」定義關係的教程](relationship-api.md)。