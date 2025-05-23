---
keywords: Experience Platform；設定檔；即時客戶設定檔；統一設定檔；統一；設定檔；rtcp；啟用設定檔；啟用設定檔；聯合結構描述；聯合設定檔；聯合設定檔
title: 聯合結構描述UI指南
type: Documentation
description: 在Adobe Experience Platform使用者介面(UI)中，您可以輕鬆檢視組織內的任何聯合結構描述，並預覽特定類別的欄位、身分、關係和貢獻結構描述。 本指南提供如何使用Experience Platform UI檢視和探索聯合結構的詳細資訊。
exl-id: 52af0d77-e37d-4ed8-9dee-71a50b337b4e
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '1204'
ht-degree: 0%

---

# [!UICONTROL 聯合結構描述] UI指南

在Adobe Experience Platform使用者介面(UI)中，您可以輕鬆檢視組織內的任何聯合結構描述，並預覽特定類別的欄位、身分、關係和貢獻結構描述。 本指南提供如何使用Experience Platform UI檢視和探索聯合結構的詳細資訊。

## 快速入門

此UI指南需要瞭解與管理即時客戶設定檔資料有關的各種[!DNL Experience Platform]服務。 在閱讀本指南或使用UI之前，請檢視以下服務的檔案：

* [[!DNL Real-Time Customer Profile]](../home.md)：根據來自多個來源的彙總資料，提供統一的即時消費者設定檔。
* [[!DNL Identity Service]](../../identity-service/home.md)：啟用[!DNL Real-Time Customer Profile]，方法是在不同資料來源中的身分擷取到[!DNL Experience Platform]時將其橋接起來。
* [[!DNL Experience Data Model (XDM)]](../../xdm/home.md)： [!DNL Experience Platform]用來組織客戶體驗資料的標準化架構。

## 瞭解聯合結構描述

即時客戶個人檔案可讓您建立強大、集中的個人檔案，其中包含客戶屬性和時間戳記事件，每個客戶在與Adobe Experience Platform整合的系統間互動。 此資料的格式和結構由Experience Data Model (XDM)結構描述提供，每個結構描述都以XDM類別為基礎，並包含與該類別相容的欄位。

結構描述可以針對多個使用案例建立，參照相同類別但包含其使用的特定欄位。 為設定檔啟用結構描述時，它會成為聯合結構描述的一部分。 換句話說，聯合結構描述是由共用相同類別並已為設定檔啟用的多個結構描述所組成。 聯合結構描述讓您能夠檢視共用相同類別的結構描述中包含的所有欄位的合併。 即時客戶設定檔使用聯合結構描述，以建立每個個別客戶的整體檢視。

使用聯合結構描述需要深入瞭解XDM結構描述。 如需詳細資訊，請先閱讀結構描述組合[&#128279;](../../xdm/schema/composition.md)的基本知識。

## 檢視聯合結構描述

若要導覽至Experience Platform UI中的聯合結構描述，請從左側導覽中選取&#x200B;**[!UICONTROL 設定檔]**，然後選取&#x200B;**[!UICONTROL 聯合結構描述]**&#x200B;索引標籤。 [!UICONTROL 聯合結構描述]索引標籤會開啟，以顯示目前所選類別的聯合結構描述。

![顯示[聯合結構描述]頁面，並反白顯示[設定檔與聯合結構描述]索引標籤。](../images/union-schema/landing.png)

## 選取類別

若要顯示特定XDM類別的聯合結構描述，請從&#x200B;**[!UICONTROL 類別]**&#x200B;下拉式清單中選取類別。 由於並非所有類別都有聯合結構描述，因此下拉式清單中只會顯示具有聯合結構描述的類別（亦即具有已針對設定檔啟用的結構描述的類別）。

選取類別後，顯示的架構會更新以反映所選類別的聯合架構。 例如，您可以選取&#x200B;**[!UICONTROL XDM個別設定檔]**&#x200B;來檢視該類別的聯合結構描述。

![包含聯合結構描述類別的下拉式清單會反白顯示。](../images/union-schema/class.png)

## 探索聯合結構描述

您可以上下捲動來檢視完整的結構描述結構，並選取右角括弧(`>`)來展開巢狀欄位，以探索聯合結構描述。

![聯合結構描述中的一組巢狀欄位已展開。](../images/union-schema/explore.png)

選取任何欄位以檢視其詳細資訊，包括顯示名稱、資料型別、說明、路徑、建立日期和上次修改日期。 您也可以檢視包含您所選欄位的貢獻結構描述清單。

![聯合結構描述欄位已反白顯示。 有關醒目提示欄位的詳細資訊會顯示在右側邊欄。](../images/union-schema/explore-field.png)

選取參與結構描述的名稱后，系統會顯示與該結構描述相關且將資料擷取至所選欄位的資料集名稱。 每個資料集名稱都會顯示為連結。 選取資料集名稱會在新視窗中開啟該資料集的活動標籤。

如需資料集的詳細資訊，包括在UI中檢視資料集活動和預覽資料集資料，請造訪[資料集UI指南](../../catalog/datasets/user-guide.md)。

![與結構描述相關的資料集清單會反白顯示。](../images/union-schema/datasets.png)

## 檢視參與的結構描述

您也可以選取&#x200B;**[!UICONTROL 所有參與的結構描述]**&#x200B;來展開結構描述清單，以檢視哪些特定結構描述對聯合結構描述有貢獻。 根據您選取的類別以及貴組織在Experience Platform中建立的結構描述數目，這可能是包含單一結構描述的簡短清單，或是包含許多結構描述的完整清單。

![加入聯合結構描述的結構描述清單已反白顯示。](../images/union-schema/contributing-schemas.png)

選取特定綱要的名稱，會醒目顯示聯合綱要中屬於您所選綱要一部分的欄位。 選取結構描述後，聯合結構描述會以灰色顯示，黑色列指示貢獻結構描述一部分的欄位。

![選取的貢獻結構描述會反白顯示。 構成貢獻結構描述一部分的欄位會保留為黑色，而非構成貢獻結構描述一部分的欄位則會呈現灰色。](../images/union-schema/select-schema.png)

## 檢視身分

透過UI，您可以選取&#x200B;**[!UICONTROL Identities]**&#x200B;來展開清單，以檢視包含在聯合結構描述中的身分清單。

![屬於聯合結構描述的身分會反白顯示。](../images/union-schema/identities.png)

從清單中選取個別身分會導致顯示的綱要視需要自動更新，以顯示身分欄位。 如果身分欄位是巢狀的，這可能包括展開多個欄位。

身分欄位會在聯合結構描述中反白顯示，身分的詳細資訊會顯示在畫面的右側。 詳細資訊包括內含身分欄位的貢獻結構描述清單，您可以向下展開以尋找與該結構描述相關的資料集連結，這些資料集會將資料擷取到所選的身分欄位中。

![選取的身分會醒目提示。 有關所選身分的詳細資訊會顯示在右側邊欄。](../images/union-schema/select-identity.png)

## 檢視關係

聯合結構描述UI也可讓您檢視已根據所選結構描述類別為結構描述定義的關係。 定義關係是連線屬於不同類別的兩個結構描述的方式，以取得有關客戶資料的更複雜見解。

如果已為選取的類別建立關聯，選取&#x200B;**[!UICONTROL 關聯]**&#x200B;會顯示用來建立關聯的欄位清單。 並非所有結構描述都使用或需要定義關係，因此關係區段通常不包含任何欄位。

若要進一步瞭解結構描述關係，包括如何使用UI定義它們，請瀏覽關於結構描述關係[&#128279;](../../xdm/tutorials/relationship-ui.md)的本檔案。

![屬於聯合結構描述的關係會反白顯示。](../images/union-schema/relationships.png)

從清單中選取關係欄位會導致顯示的結構描述視需要更新，以顯示反白顯示的關係欄位。 如果關係欄位是巢狀的，這可能包括展開多個欄位。

![選取的關係已反白顯示。 關聯性的對應欄位也反白顯示。](../images/union-schema/select-relationship.png)

## 後續步驟

閱讀本指南後，您現在瞭解如何使用[!DNL Experience Platform] UI檢視和導覽聯合結構描述。 如需結構描述的詳細資訊，包括如何在Experience Platform中使用，請先閱讀[XDM系統總覽](../../xdm/home.md)。
