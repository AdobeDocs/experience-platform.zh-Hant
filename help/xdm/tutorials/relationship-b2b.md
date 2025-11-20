---
title: 在Real-Time Customer Data Platform B2B edition中定義兩個結構描述之間的關係
description: 瞭解如何在Adobe Real-Time Customer Data Platform B2B edition中定義兩個結構描述之間的多對一關係。
exl-id: 14032754-c7f5-46b6-90e6-c6e99af1efba
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '1726'
ht-degree: 12%

---

# 在 Real-Time Customer Data Platform B2B 版本中定義兩個結構描述之間的多對一關係 {#relationship-b2b}

>[!CONTEXTUALHELP]
>id="platform_xdm_b2b_reference_schema"
>title="參考結構描述"
>abstract="選取要建立關係的結構描述。根據結構描述的類別，結構描述還可能和 B2B 內容中的其他實體存在現有關係。請查看文件以了解 B2B 結構描述類別彼此間的關係。"

Adobe Real-Time Customer Data Platform B2B edition提供可擷取基本B2B資料實體的數個Experience Data Model (XDM)類別，包括[帳戶](../classes/b2b/business-account.md)、[機會](../classes/b2b/business-opportunity.md)、[行銷活動](../classes/b2b/business-campaign.md)等。 透過根據這些類別建立結構描述並啟用它們以用於[即時客戶設定檔](../../profile/home.md)，您可以將不同來源的資料合併到稱為聯合結構描述的統一表示中。

不過，聯合結構描述只能包含共用相同類別的結構描述所擷取的欄位。 這就是結構描述關係的用處。 透過在B2B結構描述中實作關係，您可以說明這些業務實體如何彼此關聯，並可在下游細分使用案例中包含來自多個類別的屬性。

下圖提供不同B2B類別在基本實作中如何相互關聯的範例：

![B2B 階級關係](../images/tutorials/relationship-b2b/classes.png)

本教學涵蓋在即時CDP B2B版中定義兩個結構間多對一關係的步驟。

>[!NOTE]
>
>如果你沒有使用即時客戶資料平台 B2B 版，或想建立一對一的關係，請參考建立 [一對一關係](./relationship-ui.md) 的指南。
>
>本教學重點在於如何在體驗平台介面中手動建立 B2B 架構之間的關聯。 如果你是從 B2B 來源連線帶入資料，可以用自動產生工具來建立所需的結構、身份和關聯。 欲了解更多自動 [產生工具](../../sources/connectors/adobe-applications/marketo/marketo-namespaces.md)的使用資訊，請參閱 B2B 命名空間與結構的原始文件。

## 快速入門

這個教學需要對介面中的結構編輯器[!DNL XDM System]有實際的理解[!DNL Experience Platform]。在開始本教學前，請先閱讀以下文件：

* [XDM 體驗平台](../home.md)系統：XDM 及其實 [!DNL Experience Platform]作概述。
* [結構組合](../schema/composition.md)基礎：XDM 架構的基礎單元介紹。
* [請使用以下 [!DNL Schema Editor]](create-schema-ui.md)工具建立結構：一個教學，涵蓋如何在 UI 中建立和編輯架構的基本知識。

## 定義來源和參考結構描述

您應已建立將在關係中定義的兩個結構描述。 為了示範，本教學課程會建立商機（在「[!DNL Opportunities]」結構描述中定義）與其相關聯的商業帳戶（在「[!DNL Accounts]」結構描述中定義）之間的關係。

結構描述關聯性由&#x200B;**來源結構描述**&#x200B;中的專用欄位表示，該欄位參照&#x200B;**參考結構描述**&#x200B;的主要身分欄位。 在接下來的步驟中，&quot;[!DNL Opportunities]&quot;做為來源結構描述，而&quot;[!DNL Accounts]&quot;做為參考結構描述。

### 了解 B2B 關係中的身分識別

>[!CONTEXTUALHELP]
>id="platform_xdm_b2b_identity_namespace"
>title="參考身分識別命名空間"
>abstract="適用於參考結構描述的主要身分識別欄位的命名空間 (類型)。參考結構描述必須有一個已建立的主要身分識別欄位才能參與關係。請查看文件以了解有關 B2B 關係中身分識別的詳細資訊。"

為了建立關係，參考結構描述必須具有定義的主要身分。 為B2B實體設定主要身分時，請記住，如果您跨不同系統或位置收集字串型實體ID，則這些ID可能會重疊，這可能會導致Experience Platform中的資料衝突。

為了解決這個問題，所有標準B2B類別都包含符合[[!UICONTROL B2B Source]資料型別](../data-types/b2b-source.md)的「key」欄位。 此資料型別提供B2B實體的字串識別碼欄位，以及有關識別碼來源的其他內容資訊。 其中一個欄位`sourceKey`串連資料型別中其他欄位的值，以產生實體的完整唯一識別碼。 此欄位一律應用作B2B實體結構描述的主要身分識別。

![來源金鑰欄位](../images/tutorials/relationship-b2b/sourcekey.png)

>[!NOTE]
>
>當[將XDM欄位設定為身分](../ui/fields/identity.md)時，您必須提供身分名稱空間來定義下方的身分。 這可以是Adobe提供的標準名稱空間，或貴組織定義的自訂名稱空間。 實際上，名稱空間只是內容字串，您可以設定為您喜歡的任何值，前提是這對於貴組織分類身分型別很有意義。 如需詳細資訊，請參閱[身分識別名稱空間](../../identity-service/features/namespaces.md)的概觀。

為方便參考，以下幾節將說明在定義關係之前，本教學課程中使用的每個結構描述的結構。 請留意已在結構描述結構中定義主要身分的位置，以及這些身分使用的自訂名稱空間。

### 機會結構描述

來源結構描述&quot;[!DNL Opportunities]&quot;是以[!UICONTROL XDM Business Opportunity]類別為基礎。 類別`opportunityKey`提供的其中一個欄位做為結構描述的識別碼。 具體來說，`sourceKey`物件下的`opportunityKey`欄位設定為名為[!DNL B2B Opportunity]的自訂名稱空間下的結構描述主要身分。

如在&#x200B;**[!UICONTROL Field Properties]**&#x200B;下所見，此結構描述已在[!DNL Real-Time Customer Profile]中啟用。

![結構描述編輯器中的Opportunity結構描述具有opportunityKey物件和Enable for profile切換反白顯示。](../images/tutorials/relationship-b2b/opportunities.png)

### [!DNL Accounts]結構描述

參考結構描述&quot;[!DNL Accounts]&quot;是以[!UICONTROL XDM Account]類別為基礎。 根層級`accountKey`欄位包含的`sourceKey`在名為[!DNL B2B Account]的自訂名稱空間下充當其主要身分。 此結構描述也已啟用以供設定檔使用。

![結構描述編輯器中的Accounts結構描述具有accountKey物件和Enable for profile切換反白顯示。](../images/tutorials/relationship-b2b/accounts.png)

## 為來源結構描述定義關係欄位 {#relationship-field}

>[!CONTEXTUALHELP]
>id="platform_xdm_b2b_relationship_name_current"
>title="目前結構描述中的關係名稱"
>abstract="說明從目前結構描述到參考結構描述的關係的標籤 (例如，「相關帳戶」)。此標籤用於設定檔和客戶細分，以從相關 B2B 實體為資料提供上下文。請查看文件以了解有關建置 B2B 結構描述關係的詳細資訊。"

>[!CONTEXTUALHELP]
>id="platform_xdm_b2b_relationship_name_reference"
>title="參考結構描述中的關係名稱"
>abstract="說明從參考結構描述到目前結構描述的關係的標籤 (例如，「相關機會」)。此標籤用於設定檔和客戶細分，以從相關 B2B 實體為資料提供上下文。請查看文件以了解有關建置 B2B 結構描述關係的詳細資訊。"

為了定義兩個結構描述之間的關係，來源結構描述必須具有專用欄位，以指示參考結構描述的主要身分。 標準B2B類別包含常用相關商業實體的專用來源索引鍵欄位。 例如，[!UICONTROL XDM Business Opportunity]類別包含相關帳戶(`accountKey`)和相關行銷活動(`campaignKey`)的來源金鑰欄位。 不過，如果您需要超過預設的元件，也可以使用自訂欄位群組，將其他[!UICONTROL B2B Source]欄位新增到結構描述中。

>[!NOTE]
>
>目前，從來源結構描述到參考結構描述只能定義多對一和一對一關係。 對於一對多關係，您必須在代表「許多」的結構描述中定義關係欄位。

若要設定關聯性欄位，請在畫布中選取相關欄位，然後在&#x200B;**[!UICONTROL Add relationship]**&#x200B;側邊欄中選取[!UICONTROL Schema properties]。 在[!DNL Opportunities]結構描述的情況下，這是`accountKey.sourceKey`欄位，因為目標是與帳戶建立多對一關係。

![結構描述編輯器，其中sourceKey欄位和Add relationship已反白顯示。](../images/tutorials/relationship-b2b/add-relationship.png)

[!UICONTROL Add relationship]對話方塊隨即顯示。 使用此對話方塊來指定關係詳細資料。 關聯性型別預設設定為&#x200B;**[!UICONTROL Many-to-one]**。

![反白顯示多對一結構描述關係的[新增關係]對話方塊。](../images/tutorials/relationship-b2b/relationship-dialog.png)

在&#x200B;**[!UICONTROL Reference Schema]**&#x200B;底下，使用搜尋列或下拉式功能表來尋找參考結構描述的名稱。 當你選取參考結構的名稱時，該 **[!UICONTROL Reference Identity Namespace]** 欄位會自動更新到參考架構主要身份的命名空間。

>[!NOTE]
>
>可用的參考結構描述清單會經過篩選，僅包含適用的結構描述。 結構描述&#x200B;**必須**&#x200B;具有指派的主要身分，且是B2B類別或個別設定檔類別。 潛在客戶類別結構描述無法建立關係。

![含有反白的參照結構描述和參照身分名稱空間欄位的[加入關聯性]對話方塊。](../images/tutorials/relationship-b2b/reference-schema.png)

在&#x200B;**[!UICONTROL Relationship Name From Current Schema]**&#x200B;和&#x200B;**[!UICONTROL Relationship Name From Reference Schema]**&#x200B;底下，分別為來源和參考結構描述內容中的關聯性提供易記名稱。 完成後，選取&#x200B;**[!UICONTROL Apply]**&#x200B;以確認變更並儲存關係。

>[!NOTE]
>
>關係名稱不得超過35個字元。

![「新增關係」對話框中「關係名稱」欄位被高亮顯示。](../images/tutorials/relationship-b2b/relationship-name.png)

畫布重新出現，關係欄位現在標記為你先前提供的友善名字。 關係名稱也標示在左側欄杆上，方便查閱。

![套用了新關係名稱的結構編輯器。](../images/tutorials/relationship-b2b/relationship-applied.png)

如果你查看參考結構，關係標記會出現在結構的主要身份欄位旁邊及左側欄。

![結構編輯器中目標結構並標示新的關係標記。](../images/tutorials/relationship-b2b/destination-relationship.png)

## 編輯 B2B 架構關係 {#edit-schema-relationship}

一旦建立結構關係，選擇來源結構中的關係欄位，接著選擇 **[!UICONTROL Edit relationship]**。

>[!NOTE]
>
>要查看所有相關的關係，請在參考結構中選擇主要身份欄位，然後點選 [!UICONTROL View relationships]。
>![結構編輯器中選擇了關係欄位並標示了「檢視關係」。](../images/tutorials/relationship-b2b/view-relationships.png "結構編輯器中選擇了關係欄位並標示了「檢視關係」。"){width="100" zoomable="yes"}

![結構編輯器，標示出關聯欄位與編輯關係。](../images/tutorials/relationship-b2b/edit-b2b-relationship.png)

[!UICONTROL Edit relationship]對話方塊隨即顯示。 您可以在此對話方塊中變更參照結構描述和關係名稱，或刪除關係。 無法變更多對一關係型別。

![編輯關聯性對話方塊。](../images/tutorials/relationship-b2b/edit-b2b-relationship-dialog.png)

為了維護資料完整性並避免分段和其他流程中斷，在管理與連結資料集的結構描述關係時，請考慮以下准則：

* 如果結構描述與資料集相關聯，請避免直接刪除關係，因為這可能會對細分造成負面影響。 請改為在移除關係之前刪除關聯的資料集。
* 您必須先刪除現有的關聯性，才能變更參考結構描述。 但是，應該謹慎執行此操作，因為刪除與關聯資料集的關係可能會造成非預期的後果。
* 將新關係新增到具有現有連結資料集的結構描述可能無法如預期運作，並可能導致潛在衝突。

## 篩選和搜尋關係 {#filter-and-search}

您可以從[!UICONTROL Relationships]工作區的[!UICONTROL Schemas]標籤篩選及搜尋結構描述中的特定關係。 您可以使用此檢視快速找到並管理您的關係。 請閱讀[探索結構描述資源](../ui/explore.md#lookup)上的檔案，以取得篩選選項的詳細說明。

![結構描述工作區中的[關聯性]索引標籤。](../images/tutorials/relationship-b2b/relationship-tab.png)

## 後續步驟

依照此教學課程，您已使用[!DNL Schema Editor]成功建立兩個結構描述之間的多對一關係。 一旦使用以這些結構描述為基礎的資料集擷取資料，且已在設定檔資料存放區中啟用該資料，您就可以將這兩個結構描述的屬性用於[多類別細分使用案例](../../rtcdp/segmentation/b2b.md)。
