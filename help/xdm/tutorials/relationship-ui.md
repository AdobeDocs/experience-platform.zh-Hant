---
keywords: Experience Platform;home;popular topics;ui;UI;XDM;XDM system;;experience data model;Experience data model;Experience Data Model;data model;Data Model;schema editor;Schema Editor;schema;Schema;schemas;Schemas;create;relationship;Relationship;reference;Reference;
solution: Experience Platform
title: 使用架構架構編輯器定義兩個架構之間的關係
description: 本檔案提供教學課程，可讓您使用Experience Platform使用者介面中的「架構編輯器」來定義兩個架構之間的關係。
topic: tutorial
type: Tutorials
translation-type: tm+mt
source-git-commit: 97dfd3a9a66fe2ae82cec8954066bdf3b6346830
workflow-type: tm+mt
source-wordcount: '910'
ht-degree: 0%

---


# 使用 [!DNL Schema Editor]

Adobe Experience Platform的重要部分，在於能夠跨不同通道瞭解客戶之間的關係以及客戶與品牌之間的互動。 在(XDM)結構中定義這 [!DNL Experience Data Model] 些關係，可讓您獲得客戶資料的複雜見解。

雖然方案關係可以通過使用union方案和來推斷 [!DNL Real-time Customer Profile]，但這僅適用於共用相同類的方案。 要在屬於不同類的兩個方案之間建立關係，必須將專用的關 **系欄位添加到源方案** ，該源方案引用目標方案的標識。

本文檔提供了一個教程，用於使用用戶介面中的方案編輯器定義兩個方案之 [!DNL Experience Platform] 間的關係。 有關使用API定義方案關係的步驟，請參閱使用方案注 [冊表API定義關係的教程](relationship-api.md)。

## 快速入門

本教學課程需要對UI中的 [!DNL XDM System] 架構編輯器和架構編輯器有正確 [!DNL Experience Platform] 的認識。 在開始本教學課程之前，請先閱讀下列檔案：

* [Experience Platform中的XDM系統](../home.md):XDM及其實施概述於 [!DNL Experience Platform]。
* [架構構成基礎](../schema/composition.md):介紹XDM模式的構建塊。
* [使用 [!DNL Schema Editor]](create-schema-ui.md):教學課程，涵蓋使用的基本知識 [!DNL Schema Editor]。

## 定義源和目標方案

預期您已經建立了將在關係中定義的兩個方案。 為了進行示範，本教學課程會在組織的忠誠度方案(在「[!DNL Loyalty Members]」架構中定義)成員與其最愛的酒店(在「[!DNL Hotels]」架構中定義)之間建立關係。

>[!IMPORTANT]
>
>為了建立關係，兩個方案都必須已定義主要身份，並啟用 [!DNL Real-time Customer Profile]。 如果需要有關如何 [相應配置方案的指導](./create-schema-ui.md#profile) ，請參見架構建立教程中啟用方案以便在配置檔案中使用一節。

架構關係由源架構內的專用欄位 **表示** ，該欄位引用目標架構內的另 **一欄位**。 在後續步驟中，&quot;[!DNL Loyalty Members]&quot;將是源模式，而&quot;[!DNL Hotels]&quot;將充當目標模式。

為便於參考，以下幾節將介紹在定義關係之前本教程中使用的每個架構的結構。

### [!DNL Loyalty Members] 架構

源模式&quot;[!DNL Loyalty Members]&quot;基於類 [!DNL XDM Individual Profile] ，是在UI中建立模式的教程 [中構建的模式](create-schema-ui.md)。 它在其命名 `loyalty` 空間下包含一 `_tenantId` 個物件，其中包含數個忠誠度特定欄位。 其中一個欄位 `loyaltyId`是「電子郵件」名稱空間下之架構的主要 [!UICONTROL 身分] 。 如「架構屬 **[!UICONTROL 性」下所示]**，此架構已啟用供使用 [!DNL Real-time Customer Profile]。

![](../images/tutorials/relationship/loyalty-members.png)

### [!DNL Hotels] 架構

目標架構「[!DNL Hotels]」是以自訂「[!DNL Hotels]」類別為基礎，並包含描述酒店的欄位。 該 `hotelId` 欄位用作自定義命名空間下的架構的主要標 `hotelId` 識。 與架構 [!DNL Loyalty Members] 一樣，此架構也已啟用 [!DNL Real-time Customer Profile]。

![](../images/tutorials/relationship/hotels.png)

## 建立關係混合

>[!NOTE]
>
>僅當源架構沒有專用字串類型欄位用作目標架構的引用時，才需要此步驟。 如果此欄位已在源方案中定義，請跳至定義關係欄位 [的下一步](#relationship-field)。

為了定義兩個方案之間的關係，源方案必須具有專用欄位以用作目標方案的引用。 通過建立新混音，可以將此欄位添加到源模式。

首先，在「 **[!UICONTROL Mixins]** 」區段中選 **[!UICONTROL 取「新增]** 」。

![](../images/tutorials/relationship/loyalty-add-mixin.png)

此時將 [!UICONTROL 顯示「添加混音] 」對話框。 從這裡，選擇「 **[!UICONTROL 建立新混音」]**。 在出現的文字欄位中，輸入新混音的顯示名稱和說明。 完成 **[!UICONTROL 時選擇]** 「新增混音」。

<img src="../images/tutorials/relationship/loyalty-create-new-mixin.png" width="750"><br>

畫布會重新顯示，而「[!DNL Favorite Hotel]」會顯示在 **[!UICONTROL Mixins區]** 。 選取混音名稱，然後選 **[!UICONTROL 取根層級欄位旁]** ，新增欄 `Loyalty Members` 位。

![](../images/tutorials/relationship/loyalty-add-field.png)

新欄位會出現在畫布中名稱空間 `_tenantId` 下。 在「 **[!UICONTROL 欄位屬性]**」下，提供欄位名稱和顯示名稱，並將其類型設為「字[!UICONTROL 串]」。

![](../images/tutorials/relationship/relationship-field-details.png)

完成後，選擇「應 **[!UICONTROL 用」]**。

![](../images/tutorials/relationship/relationship-field-apply.png)

更新的欄 `favoriteHotel` 位會出現在畫布中。 選擇 **[!UICONTROL 保存]** ，以最終完成對架構的更改。

![](../images/tutorials/relationship/relationship-field-save.png)

## 為源方案定義關係欄位 {#relationship-field}

在源架構定義了專用的參考欄位後，可以將其指定為關係欄位。

選取畫 `favoriteHotel` 布中的欄位，然後在「欄位屬性」下方向下卷 **[!UICONTROL 動]** ，直到出現「 **[!UICONTROL 關係]** 」核取方塊。 選中該複選框可顯示配置關係欄位所需的參數。

![](../images/tutorials/relationship/relationship-checkbox.png)

選擇參考方 **[!UICONTROL 案的下拉式清單]** ，並選取關係的目標方案(在此範例中[!DNL Hotels]為「」)。 如果為啟用了目標方 [!DNL Profile]案，則 **[!UICONTROL Reference identity namespace]** （參考標識名稱空間）欄位將自動設定為目標方案的主標識的命名空間。 如果架構未定義主標識，則必須從下拉菜單中手動選擇要使用的命名空間。 完成 **[!UICONTROL 時選擇]** 「應用」。

![](../images/tutorials/relationship/reference-schema-id-namespace.png)

欄位 `favoriteHotel` 現在會在畫布中反白標示為關係，顯示目標架構的名稱和參考身分名稱空間。 選擇 **[!UICONTROL 「保存]** 」(Save)以保存更改並完成工作流。

![](../images/tutorials/relationship/relationship-save.png)

## 後續步驟

在本教學課程之後，您已使用成功建立兩個結構描述之間的一對一關係 [!DNL Schema Editor]。 有關如何使用API定義關係的步驟，請參閱使用「方案註冊 [表API」定義關係的教程](relationship-api.md)。