---
keywords: Experience Platform；首頁；熱門主題；UI; XDM; XDM系統；體驗資料模型；體驗資料模型；體驗資料模型；資料模型；結構編輯器；結構編輯器；結構；結構；結構；建立；關係；關係；參考；參考；
solution: Experience Platform
title: 使用結構編輯器定義兩個結構之間的關係
description: 本檔案提供一個教學課程，用於使用Experience Platform使用者介面中的結構編輯器定義兩個結構之間的關係。
topic-legacy: tutorial
type: Tutorial
exl-id: feed776b-bc8d-459b-9700-e5c9520788c0
source-git-commit: 2118dc175b421e856c6b0a33a83a7238f01b7ee3
workflow-type: tm+mt
source-wordcount: '1020'
ht-degree: 0%

---

# 使用[!DNL Schema Editor]定義兩個結構之間的關係

>[!NOTE]
>
>如果您使用即時客戶資料平台B2B版，請參閱[建立B2B關係](./relationship-b2b.md)的指南。

了解客戶之間的關係，以及客戶在不同管道與品牌互動的能力，是Adobe Experience Platform的重要一環。 在[!DNL Experience Data Model](XDM)結構內定義這些關係，可讓您對客戶資料獲得複雜的深入分析。

雖然可透過使用聯合架構和[!DNL Real-time Customer Profile]來推斷架構關係，但這隻適用於共用相同類別的架構。 要在屬於不同類的兩個架構之間建立關係，必須將專用的關係欄位添加到源架構中，該源架構引用目標架構的標識。

本文檔提供了使用[!DNL Experience Platform]用戶介面中的架構編輯器定義兩個架構之間關係的教程。 有關使用API定義架構關係的步驟，請參閱有關使用架構註冊表API](relationship-api.md)定義關係的教程。[

## 快速入門

本教學課程需要妥善了解[!DNL XDM System]和[!DNL Experience Platform] UI中的結構編輯器。 開始本教學課程之前，請檢閱下列檔案：

* [Experience Platform中的XDM系統](../home.md):概略說明XDM及其實作方 [!DNL Experience Platform]式。
* [結構構成基本概念](../schema/composition.md):介紹XDM結構的建置組塊。
* [使用 [!DNL Schema Editor]](create-schema-ui.md)建立結構：本教學課程說明使用的基本 [!DNL Schema Editor]知識。

## 定義源和目標架構

您應已建立將在關係中定義的兩個結構。 為了示範，本教學課程會在組織的忠誠計畫（在「[!DNL Loyalty Members]」架構中定義）成員與其最喜愛的酒店（在「[!DNL Hotels]」架構中定義）之間建立關係。

>[!IMPORTANT]
>
>若要建立關係，兩個結構都必須定義主要身分，並且必須為[!DNL Real-time Customer Profile]啟用。 如果您需要如何據以設定結構的指引，請參閱架構建立教學課程中[啟用結構以用於Profile](./create-schema-ui.md#profile)的一節。

架構關係由&#x200B;**源架構**&#x200B;內的專用欄位表示，該欄位引用&#x200B;**目標架構**&#x200B;內的另一個欄位。 在後續步驟中，「[!DNL Loyalty Members]」將是源架構，而「[!DNL Hotels]」將充當目標架構。

為了參考，以下幾節將說明定義關係之前本教學課程中使用的每個架構的結構。

### [!DNL Loyalty Members] 綱要

源架構「[!DNL Loyalty Members]」基於[!DNL XDM Individual Profile]類，是在[教程中為在UI](create-schema-ui.md)中建立架構構建的架構。 其`_tenantId`命名空間下包含`loyalty`物件，其中包含數個忠誠度專屬欄位。 其中一個欄位`loyaltyId`是[!UICONTROL Email]命名空間下架構的主要身分。 如&#x200B;**[!UICONTROL 架構屬性]**&#x200B;下所示，此架構已啟用，可在[!DNL Real-time Customer Profile]中使用。

![](../images/tutorials/relationship/loyalty-members.png)

### [!DNL Hotels] 綱要

目標架構「[!DNL Hotels]」基於自定義「[!DNL Hotels]」類，並包含描述酒店的欄位。

![](../images/tutorials/relationship/hotels.png)

為了參與關係，目標架構必須具有主要身分。 在此範例中，使用自訂的「Hotel ID」身分命名空間，將`hotelId`欄位當作主要身分識別。

![酒店主要身份](../images/tutorials/relationship/hotel-identity.png)

>[!NOTE]
>
>若要了解如何建立自訂身分識別命名空間，請參閱[Identity Service檔案](../../identity-service/namespaces.md#manage-namespaces)。

設定主要身分後，必須為[!DNL Real-time Customer Profile]啟用目標架構。

![啟用設定檔](../images/tutorials/relationship/hotel-profile.png)

## 建立關係架構欄位組

>[!NOTE]
>
>只有在源架構沒有專用的字串類型欄位用作目標架構的引用時，才需要執行此步驟。 如果源架構中已定義此欄位，請跳到定義關係欄位](#relationship-field)的下一步。[

要定義兩個架構之間的關係，源架構必須具有專用欄位以用作目標架構的引用。 您可以建立新架構欄位組，將此欄位添加到源架構。

首先，在&#x200B;**[!UICONTROL 欄位組]**&#x200B;區段中選擇&#x200B;**[!UICONTROL Add]**。

![](../images/tutorials/relationship/loyalty-add-field-group.png)

將顯示[!UICONTROL 添加欄位組]對話框。 從此處，選擇&#x200B;**[!UICONTROL 建立新欄位組]**。 在顯示的文本欄位中，輸入新欄位組的顯示名稱和說明。 完成後，選擇&#x200B;**[!UICONTROL 添加欄位組]**。

![](../images/tutorials/relationship/create-field-group.png)

畫布會重新顯示，「[!DNL Favorite Hotel]」出現在&#x200B;**[!UICONTROL 欄位群組]**&#x200B;區段中。 選擇欄位組名稱，然後選擇根級別`Loyalty Members`欄位旁的&#x200B;**[!UICONTROL 添加欄位]**。

![](../images/tutorials/relationship/loyalty-add-field.png)

在畫布中的`_tenantId`命名空間下會顯示新欄位。 在&#x200B;**[!UICONTROL 欄位屬性]**&#x200B;下，提供欄位的欄位名稱和顯示名稱，並將其類型設定為&quot;[!UICONTROL 字串]&quot;。

![](../images/tutorials/relationship/relationship-field-details.png)

完成後，選擇&#x200B;**[!UICONTROL Apply]**。

![](../images/tutorials/relationship/relationship-field-apply.png)

更新的`favoriteHotel`欄位會顯示在畫布中。 選擇&#x200B;**[!UICONTROL 保存]**&#x200B;以完成對架構的更改。

![](../images/tutorials/relationship/relationship-field-save.png)

## 為源架構定義關係欄位 {#relationship-field}

在源架構定義了專用的引用欄位後，您可以將其指定為關係欄位。

在畫布中選取`favoriteHotel`欄位，然後在&#x200B;**[!UICONTROL 欄位屬性]**&#x200B;下向下捲動，直到出現&#x200B;**[!UICONTROL 關係]**&#x200B;核取方塊為止。 選取核取方塊以顯示設定關係欄位所需的參數。

![](../images/tutorials/relationship/relationship-checkbox.png)

選擇&#x200B;**[!UICONTROL 引用架構]**&#x200B;的下拉清單，然後選擇關係（本示例中為&quot;[!DNL Hotels]&quot;）的目標架構。 如果為[!DNL Profile]啟用目標架構，則將&#x200B;**[!UICONTROL 引用標識命名空間]**&#x200B;欄位自動設定為目標架構的主標識的命名空間。 如果架構未定義主要身分，您必須從下拉式功能表手動選取您打算使用的命名空間。 完成後，選擇&#x200B;**[!UICONTROL Apply]**。

![](../images/tutorials/relationship/reference-schema-id-namespace.png)

`favoriteHotel`欄位現在會在畫布中以關係強調顯示，顯示目標架構的名稱和參考身分命名空間。 選擇&#x200B;**[!UICONTROL Save]**&#x200B;以保存更改並完成工作流。

![](../images/tutorials/relationship/relationship-save.png)

## 後續步驟

依照本教學課程，您已使用[!DNL Schema Editor]成功建立兩個結構之間的一對一關係。 有關如何使用API定義關係的步驟，請參閱有關使用Schema Registry API](relationship-api.md)定義關係的[教程。
