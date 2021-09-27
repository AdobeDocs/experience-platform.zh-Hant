---
title: 定義即時客戶資料平台B2B版本中兩個結構之間的關係
description: 了解如何在即時客戶資料平台B2B版本中定義兩個結構之間的多對一關係。
source-git-commit: d83ad2870b6099d3c6359dcc7cd000ecad8a238f
workflow-type: tm+mt
source-wordcount: '1220'
ht-degree: 0%

---

# 定義即時客戶資料平台B2B版本中兩個結構之間的關係

>[!IMPORTANT]
>
>即時客戶資料平台B2B版目前仍在測試中。 檔案和功能可能會有所變更。

>[!NOTE]
>
>如果您沒有使用即時客戶資料平台B2B版，請參閱[建立非B2B關係的指南](./relationship-ui.md)。

即時客戶資料平台B2B版提供數種擷取基本B2B資料實體的Experience Data Model(XDM)類別，包括[accounts](../classes/b2b/business-account.md)、[opportunitys](../classes/b2b/business-opportunity.md)、[campaigns](../classes/b2b/business-campaign.md)等。 通過基於這些類構建架構並啟用它們以在[即時客戶配置檔案](../../profile/home.md)中使用，您可以將不同源的資料合併為稱為聯合架構的統一表示。

但是，聯合架構只能包含由共用相同類別的結構所擷取的欄位。 這是架構關係的來源。 在B2B結構中實作關係，您便可以說明這些業務實體彼此間的關係，並可在下游細分使用案例中納入多個類別的屬性。

下圖提供在基本實施中不同B2B類如何彼此關聯的範例：

![B2B類關係](../images/tutorials/relationship-b2b/classes.png)

本教學課程涵蓋定義即時CDP B2B Edition中兩個結構之間多對一關係的步驟。

>[!NOTE]
>
>本教學課程著重於如何在Platform UI中手動建立B2B結構之間的關係。 如果您要從B2B來源連線匯入資料，可使用自動產生公用程式來建立所需的結構、身分和關係。 有關使用自動生成實用程式](../../sources/connectors/adobe-applications/marketo/marketo-namespaces.md)的[的詳細資訊，請參閱B2B命名空間和架構的源文檔。

## 快速入門

本教學課程需要妥善了解[!DNL XDM System]和[!DNL Experience Platform] UI中的結構編輯器。 開始本教學課程之前，請檢閱下列檔案：

* [Experience Platform中的XDM系統](../home.md):概略說明XDM及其實作方 [!DNL Experience Platform]式。
* [結構構成基本概念](../schema/composition.md):介紹XDM結構的建置組塊。
* [使用 [!DNL Schema Editor]](create-schema-ui.md)建立結構：本教學課程說明如何在UI中建立和編輯結構描述的基本知識。

## 定義源和目標架構

您應已建立將在關係中定義的兩個結構。 為了演示，本教程建立了業務機會（在&quot;[!DNL Opportunities]&quot;架構中定義）與其關聯的業務帳戶（在&quot;[!DNL Accounts]&quot;架構中定義）之間的關係。

架構關係由&#x200B;**源架構**&#x200B;內引用&#x200B;**目標架構**&#x200B;的主標識欄位的專用欄位表示。 在下列步驟中，「[!DNL Opportunities]」作為源架構，而「[!DNL Accounts]」作為目標架構。

### 了解B2B關係中的身分

若要建立關係，兩個結構都必須定義主要身分，並且必須為[!DNL Real-time Customer Profile]啟用。 為B2B實體設定主要身分時，請記住，如果您跨不同系統或位置收集字串型實體ID，可能會重疊，這可能會在Platform中導致資料衝突。

為此，所有標準B2B類都包含符合[[!UICONTROL B2B源]資料類型](../data-types/b2b-source.md)的「key」欄位。 此資料類型提供B2B實體字串識別碼的欄位，以及識別碼來源的其他內容資訊。 其中一個欄位`sourceKey`串連資料類型中其他欄位的值，以產生實體的唯一標識符。 此欄位應一律作為B2B實體結構的主要身分。

![sourceKey欄位](../images/tutorials/relationship-b2b/sourcekey.png)

>[!NOTE]
>
>當[將XDM欄位設為identity](../ui/fields/identity.md)時，您必須提供身分命名空間以定義底下的身分。 這可以是Adobe提供的標準命名空間，或您的組織定義的自訂命名空間。 實際上，命名空間只是內容字串，只要對貴組織來說對分類身分類型有意義，就可以設為您喜歡的任何值。 如需詳細資訊，請參閱[身分識別命名空間](../../identity-service/namespaces.md)上的概觀。

為了參考，以下幾節將說明定義關係之前本教學課程中使用的每個架構的結構。 請留意主要身分識別在架構結構中的定義位置，以及其使用的自訂命名空間。

### [!DNL Opportunities] 綱要

源架構「[!DNL Opportunities]」基於[!UICONTROL  XDM Business Opportunity]類。 類`opportunityKey`提供的其中一個欄位用作架構的標識符。 具體來說， `opportunityKey`物件下的`sourceKey`欄位會在名為[!DNL B2B Opportunity]的自訂命名空間下設為架構的主要身分。
如**[!UICONTROL 架構屬性]**&#x200B;下所示，此架構已啟用，可在[!DNL Real-time Customer Profile]中使用。

![機會結構](../images/tutorials/relationship-b2b/opportunities.png)

### [!DNL Accounts] 綱要

目標架構「[!DNL Accounts]」基於[!UICONTROL XDM帳戶]類。 根級別`accountKey`欄位包含`sourceKey`，該欄位在名為[!DNL B2B Account]的自訂命名空間下作為其主要身分。 此架構也已啟用，可在「設定檔」中使用。

![帳戶結構](../images/tutorials/relationship-b2b/accounts.png)

## 為源架構定義關係欄位 {#relationship-field}

要定義兩個架構之間的關係，源架構必須具有引用目標架構主要標識的專用欄位。 標準B2B類包括常用相關業務實體的專用源密鑰欄位。 例如，[!UICONTROL XDM Business Opportunity]類包含相關帳戶(`accountKey`)和相關促銷活動(`campaignKey`)的源密鑰欄位。 但是，如果需要的元件超過預設元件，您也可以使用自訂欄位群組，將其他[!UICONTROL B2B來源]欄位新增至架構。

>[!NOTE]
>
>目前，從源架構到目標架構只能定義多對一關係。 對於一對多關係，您必須在表示「多」的結構中定義關係欄位。

若要設定關係欄位，請選取畫布中相關欄位旁的箭頭圖示（![箭頭圖示](../images/tutorials/relationship-b2b/arrow.png)）。 在[!DNL Opportunities]架構中，這是`accountKey.sourceKey`欄位，因為目標是與帳戶建立多對一關係。

![關係按鈕](../images/tutorials/relationship-b2b/relationship-button.png)

此時將顯示一個對話框，允許您指定關係的詳細資訊。 關係類型會自動設為&#x200B;**[!UICONTROL 多對一]**。

![關係對話](../images/tutorials/relationship-b2b/relationship-dialog.png)

在&#x200B;**[!UICONTROL 參考架構]**&#x200B;下，使用搜索欄查找目標架構的名稱。 當您反白顯示目標架構的名稱時，**[!UICONTROL 參考身分命名空間]**&#x200B;欄位會自動更新架構主要身分識別的命名空間。

![參考結構](../images/tutorials/relationship-b2b/reference-schema.png)

在&#x200B;**[!UICONTROL 「當前架構的關係名稱」]**&#x200B;和&#x200B;**[!UICONTROL 「參考架構的關係名稱」]**&#x200B;下，分別為源架構和目標架構上下文中的關係提供友好名稱。 完成後，選擇&#x200B;**[!UICONTROL Save]**&#x200B;以應用更改並保存架構。

![關係名稱](../images/tutorials/relationship-b2b/relationship-name.png)

畫布會重新顯示，「關係」欄位現在會以您先前提供的好記名稱標示。 關係名稱也會列在左側邊欄下方，以方便參考。

![已應用關係](../images/tutorials/relationship-b2b/relationship-applied.png)

如果您檢視目標架構的結構，關係標籤會出現在架構的主要身分欄位旁和左側邊欄中。

![目標架構關係標籤](../images/tutorials/relationship-b2b/destination-relationship.png)

## 後續步驟

依照本教學課程，您已使用[!DNL Schema Editor]成功建立兩個結構之間的多對一關係。 使用以這些結構為基礎的資料集匯入資料，且該資料已在設定檔資料存放區中啟動後，您就可以將這兩個結構的屬性用於多類別劃分使用案例。 如需詳細資訊，請參閱Real-time CDP B2B Edition的相關檔案。
