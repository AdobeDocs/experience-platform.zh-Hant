---
keywords: Experience Platform；首頁；熱門主題；UI；UI；XDM；XDM系統；體驗資料模型；體驗資料模型；資料模型；資料模型；結構描述編輯器；結構描述編輯器；結構描述；結構描述；結構描述；建立；關係；關係；參考；參考；
solution: Experience Platform
title: 使用結構編輯器定義兩個結構描述之間的關係
description: 本檔案提供在Experience Platform使用者介面中使用結構編輯器來定義兩個結構描述之間關係的教學課程。
type: Tutorial
exl-id: feed776b-bc8d-459b-9700-e5c9520788c0
source-git-commit: ba39f62cd77acedb7bfc0081dbb5f59906c9b287
workflow-type: tm+mt
source-wordcount: '1158'
ht-degree: 10%

---

# 使用 [!DNL Schema Editor] 定義兩個方案之間的一對一關係 {#relationship-ui}

>[!CONTEXTUALHELP]
>id="platform_schemas_relationships"
>title="方案關係"
>abstract="屬於不同類別的方案可藉由關係欄位建立內容連結，進而讓您能夠建置更複雜的分段規則。如需有關方案關係的詳細資訊，請查看此文件。"

>[!CONTEXTUALHELP]
>id="platform_xdm_1to1_reference_schema"
>title="參考方案"
>abstract="選取要建立關係的方案。此方案可能和目前方案屬於不同類別。如需有關方案關係的詳細資訊，請查看此文件。"

>[!CONTEXTUALHELP]
>id="platform_xdm_1to1_identity_namespace"
>title="參考身分命名空間"
>abstract="適用於參考方案的主要身分識別欄位的命名空間 (類型)。參考方案必須有一個已建立的主要身分識別欄位才能參與關係。如需有關方案關係的詳細資訊，請查看此文件。"

瞭解客戶之間的關係以及他們跨不同管道與您品牌的互動，是Adobe Experience Platform的重要一環。 在[!DNL Experience Data Model] (XDM)結構描述的結構中定義這些關係，可讓您獲得有關客戶資料的複雜見解。

雖然結構描述關聯性可透過使用聯合結構描述和[!DNL Real-Time Customer Profile]來推斷，但這僅適用於共用相同類別的結構描述。 若要在屬於不同類別的兩個結構描述之間建立關係，必須將專用關係欄位新增到來源結構描述中，該來源結構描述會參考其他相關結構描述的身分。

>[!NOTE]
>
>如果來源和目的地結構描述都屬於相同類別，則不應該使用專用關聯性欄位&#x200B;****。 在此情況下，請使用聯合結構描述UI來檢視關係。 有關如何執行此動作的說明，請參閱聯合結構描述UI指南的[檢視關係](../../profile/ui/union-schema.md#view-relationships)區段。

本檔案提供在[!DNL Experience Platform]使用者介面中使用結構描述編輯器來定義兩個結構描述之間關係的教學課程。 如需使用API定義結構描述關係的步驟，請參閱有關[使用結構描述登入API定義關係的教學課程](relationship-api.md)。

>[!NOTE]
>
>如需如何在Adobe Real-time Customer Data Platform B2B Edition中建立多對一關係的步驟，請參閱[建立B2B關係](./relationship-b2b.md)指南。

## 快速入門

此教學課程需要您實際瞭解[!DNL XDM System]以及[!DNL Experience Platform] UI中的結構描述編輯器。 在開始本教學課程之前，請先檢閱下列檔案：

* Experience Platform](../home.md)中的[XDM系統： [!DNL Experience Platform]中XDM及其實作的概觀。
* [結構描述組合的基本概念](../schema/composition.md)： XDM結構描述的建置區塊簡介。
* [使用 [!DNL Schema Editor]](create-schema-ui.md)建立結構描述：涵蓋使用[!DNL Schema Editor]基本知識的教學課程。

## 定義來源和參考結構描述

您應已建立將在關係中定義的兩個結構描述。 為了示範，本教學課程會建立組織的熟客方案（定義在「[!DNL Loyalty Members]」結構描述中）成員與其最愛的飯店（定義在「[!DNL Hotels]」結構描述中）之間的關係。

>[!IMPORTANT]
>
>為了建立關聯性，兩個結構描述都必須定義主要身分並啟用[!DNL Real-Time Customer Profile]。 如果您需要如何適當地設定結構描述的指引，請參閱結構描述建立教學課程中[啟用結構描述以用於設定檔](./create-schema-ui.md#profile)的區段。

結構描述關聯性由&#x200B;**來源結構描述**&#x200B;中的專用欄位表示，該欄位指向&#x200B;**參考結構描述**&#x200B;中的另一個欄位。 在接下來的步驟中，&quot;[!DNL Loyalty Members]&quot;將會是來源結構描述，而&quot;[!DNL Hotels]&quot;將會做為參考結構描述。

以下幾節說明在定義關係之前，本教學課程中使用的每個結構描述的結構。

### [!DNL Loyalty Members]結構描述

來源結構描述&quot;[!DNL Loyalty Members]&quot;以[!DNL XDM Individual Profile]類別為基礎，包含描述熟客方案成員的欄位。 其中一個欄位`personalEmail.addess`會當作[!UICONTROL 電子郵件]名稱空間下結構描述的主要身分。 如在&#x200B;**[!UICONTROL 結構描述屬性]**&#x200B;下所見，此結構描述已在[!DNL Real-Time Customer Profile]中啟用。

![](../images/tutorials/relationship/loyalty-members.png)

### [!DNL Hotels]結構描述

參考結構描述&quot;[!DNL Hotels]&quot;以自訂&quot;[!DNL Hotels]&quot;類別為基礎，並包含描述飯店的欄位。 為了參與關聯性，參考結構描述也必須定義主要身分並啟用[!UICONTROL 設定檔]。 在這種情況下，`_tenantId.hotelId`會使用自訂&quot;[!DNL Hotel ID]&quot;身分名稱空間，作為結構描述的主要身分。

為設定檔](../images/tutorials/relationship/hotels.png)啟用![

>[!NOTE]
>
>若要瞭解如何建立自訂身分識別名稱空間，請參閱[身分識別服務檔案](../../identity-service/features/namespaces.md#manage-namespaces)。

## 建立關係欄位群組

>[!NOTE]
>
>只有在您的來源結構描述沒有專用字串型別欄位來當作參考結構描述主要身分的指標時，才需要執行此步驟。 若此欄位已在您的來源結構描述中定義，請跳到下一個步驟[定義關聯性欄位](#relationship-field)。

為了定義兩個結構描述之間的關係，來源結構描述必須具有將指示參考結構描述的主要身分的專用欄位。 您可以建立新的結構描述欄位群組或擴充現有的結構描述欄位群組，將此欄位新增至來源結構描述。

在[!DNL Loyalty Members]結構描述中，將會新增新的`preferredHotel`欄位，以表示忠誠會員偏好公司造訪的飯店。 首先，請選取來源結構描述名稱旁的加號圖示(**+**)。

![](../images/tutorials/relationship/loyalty-add-field.png)

新的欄位預留位置會顯示在畫布中。 在&#x200B;**[!UICONTROL 欄位屬性]**&#x200B;底下，提供欄位名稱和欄位顯示名稱，並將其型別設定為&quot;[!UICONTROL 字串]&quot;。 在&#x200B;**[!UICONTROL 指派給]**&#x200B;下，選取要擴充的現有欄位群組，或輸入唯一名稱以建立新的欄位群組。 在此情況下，會建立新的&quot;[!DNL Preferred Hotel]&quot;欄位群組。

![](../images/tutorials/relationship/relationship-field-details.png)

完成後，選取&#x200B;**[!UICONTROL 套用]**。

![](../images/tutorials/relationship/relationship-field-apply.png)

更新的`preferredHotel`欄位會顯示在畫布中，位於`_tenantId`物件下方，因為它是自訂欄位。 選取&#x200B;**[!UICONTROL 儲存]**&#x200B;以完成您對結構描述的變更。

![](../images/tutorials/relationship/relationship-field-save.png)

## 為來源方案定義關係欄位 {#relationship-field}

一旦您的來源結構描述定義了專用參考欄位後，您就可以將其指定為關係欄位。

>[!NOTE]
>
>以下步驟說明如何使用畫布中的滑鼠右欄控制項來定義關係欄位。 如果您有Real-Time CDP B2B Edition的存取權，也可以使用[相同的對話方塊](./relationship-b2b.md#relationship-field)定義一對一關係，就像建立多對一關係時一樣。

在畫布中選取`preferredHotel`欄位，然後向下捲動至&#x200B;**[!UICONTROL 欄位屬性]**&#x200B;下，直到&#x200B;**[!UICONTROL Relationship]**&#x200B;核取方塊出現為止。 選取核取方塊以顯示設定關係欄位所需的引數。

![](../images/tutorials/relationship/relationship-checkbox.png)

選取&#x200B;**[!UICONTROL 參考結構描述]**&#x200B;的下拉式清單，並選取關聯性的參考結構描述（此範例中為&quot;[!DNL Hotels]&quot;）。 在&#x200B;**[!UICONTROL 參考身分名稱空間]**&#x200B;下，選取參考結構描述之身分欄位的名稱空間（在此案例中為&quot;[!DNL Hotel ID]&quot;）。 完成時選取&#x200B;**[!UICONTROL 套用]**。

![](../images/tutorials/relationship/reference-schema-id-namespace.png)

`preferredHotel`欄位現在會在畫布中反白為關聯性，顯示參考結構描述的名稱。 選取&#x200B;**[!UICONTROL 儲存]**&#x200B;以儲存變更並完成工作流程。

![](../images/tutorials/relationship/relationship-save.png)

## 後續步驟

依照此教學課程，您已使用[!DNL Schema Editor]成功建立兩個結構描述之間的一對一關係。 如需有關如何使用API定義關係的步驟，請參閱有關[使用結構描述登入API定義關係的教學課程](relationship-api.md)。
