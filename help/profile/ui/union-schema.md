---
keywords: Experience Platform；配置檔案；即時客戶配置檔案；統一配置檔案；統一配置檔案；統一配置檔案；配置檔案；rtcp；啟用配置檔案；啟用配置檔案；聯合模式；聯合配置檔案；聯合配置檔案
title: Union Schema UI指南
topic-legacy: guide
type: Documentation
description: 在Adobe Experience Platform用戶介面(UI)中，您可以輕鬆查看組織內的任何聯合架構，並預覽特定類的欄位、身份、關係和貢獻架構。 本指南提供如何使用平台UI檢視和探索聯合架構的詳細資訊。
exl-id: 52af0d77-e37d-4ed8-9dee-71a50b337b4e
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '1028'
ht-degree: 0%

---

# [!UICONTROL Union schema] UI指南

在Adobe Experience Platform用戶介面(UI)中，您可以輕鬆查看組織內的任何聯合架構，並預覽特定類的欄位、身份、關係和貢獻架構。 本指南提供如何使用平台UI檢視和探索聯合架構的詳細資訊。

## 快速入門

本UI指南需要瞭解管理即時客戶個人檔案資料時涉及的各種[!DNL Experience Platform]服務。 在閱讀本指南或在UI中工作之前，請先閱讀下列服務的檔案：

* [[!DNL Real-time Customer Profile]](../home.md):根據來自多個來源的匯整資料，提供統一、即時的消費者個人檔案。
* [[!DNL Identity Service]](../../identity-service/home.md):可在 [!DNL Real-time Customer Profile] 不同資料來源的身分被吸收時，橋接其身分 [!DNL Platform]。
* [[!DNL Experience Data Model (XDM)]](../../xdm/home.md):組織客戶體驗資 [!DNL Platform] 料的標準化架構。

## 瞭解聯合結構

即時客戶個人檔案可讓您建立強穩、集中的個人檔案，其中包含客戶屬性和時間戳記事件，每個客戶互動都跨與Adobe Experience Platform整合的系統。 此資料的格式和結構由Experience Data Model(XDM)架構提供，每個架構都以XDM類別為基礎，並包含與該類別相容的欄位。

可以為多個使用案例建立結構描述，引用相同的類，但包含其使用的特定欄位。 為配置檔案啟用架構後，它將成為聯合架構的一部分。 換句話說，聯合方案由多個方案組成，這些方案共用相同的類，並且已啟用配置檔案。 聯合架構可讓您查看共用同一類的架構中包含的所有欄位的合併。 即時客戶個人檔案使用聯合架構來建立每個客戶的整體檢視。

使用聯合架構需要對XDM架構有深入的瞭解。 有關詳細資訊，請首先閱讀[架構構成的基本資訊](../../xdm/schema/composition.md)。

## 查看聯合結構

若要導覽至平台UI內的聯合結構，請從左側導覽中選擇&#x200B;**[!UICONTROL Profiles]**，然後選擇&#x200B;**[!UICONTROL Union Schema]**&#x200B;標籤。 將開啟[!UICONTROL Union Schema]頁籤，以顯示當前所選類的聯合模式。

![](../images/union-schema/union-schema-landing.png)

## 選擇類

要顯示特定XDM類的聯合模式，請從&#x200B;**[!UICONTROL Class]**&#x200B;下拉式清單中選擇該類。 由於並非所有類都具有聯合方案，因此下拉清單中只有具有聯合方案的類（即具有已啟用配置檔案的方案的類）可用。

選擇類後，顯示的模式將更新以反映所選類的聯合模式。 例如，您可以選擇&#x200B;**[!UICONTROL XDM Individual Profile]**&#x200B;來查看該類的聯合模式。

![](../images/union-schema/union-schema-class.png)

## 探索聯合結構

您可以上下捲動來檢視完整的架構結構，並選取右角括弧(`>`)來展開巢狀欄位，以探索聯合架構。

![](../images/union-schema/union-schema-explore.png)

選取任何欄位以檢視其詳細資料，包括顯示名稱、資料類型、說明、路徑、建立日期和上次修改日期。 您也可以檢視包含您選取欄位的貢獻方案清單。

![](../images/union-schema/union-schema-explore-field.png)

選擇貢獻方案的名稱會揭示與該方案相關的資料集名稱，這些資料集會將資料擷取至選取的欄位。 每個資料集名稱都會以連結的形式顯示。 選取資料集名稱會在新視窗中開啟該資料集的活動標籤。

有關資料集的詳細資訊，包括查看資料集活動和在UI中預覽資料集資料集資料，請訪問[資料集UI指南](../../catalog/datasets/user-guide.md)。

![](../images/union-schema/union-schema-field-datasets.png)

## 檢視貢獻結構

通過選擇&#x200B;**[!UICONTROL All contributing schemas]**&#x200B;展開方案清單，還可以查看哪些特定方案將對聯合方案作出貢獻。 根據您選擇的類和您的組織在Platform中建立的方案數，此清單可以是包含單個方案的簡短清單或包含多個方案的長清單。

![](../images/union-schema/union-schema-contributing-schemas.png)

選擇特定方案的名稱會突出顯示您所選方案中的聯合方案中的欄位。 在選擇架構後，聯合架構會以黑色條顯示為灰色，指示作用架構中的欄位。

![](../images/union-schema/union-schema-select-schema.png)

## 檢視身分

通過UI，您可以通過選擇&#x200B;**[!UICONTROL Identities]**&#x200B;展開清單來查看聯合架構中包含的身份清單。

![](../images/union-schema/union-schema-identities.png)

從清單中選擇單個標識會導致顯示的模式根據需要自動更新，以顯示標識欄位。 如果識別欄位已巢狀化，這可能包括展開多個欄位。

聯合模式中突出顯示了身份欄位，該身份的詳細資訊顯示在螢幕的右側。 詳細資訊包括包含身份欄位的貢獻方案清單，您可以深入查看以查找到與該方案相關的資料集的連結，這些資料集將資料收錄到選定的身份欄位中。

![](../images/union-schema/union-schema-select-identity.png)

## 檢視關係

聯合模式UI還允許您查看已基於所選模式類為模式定義的關係。 定義關係是連接屬於不同類別的兩個結構描述的一種方式，以便獲得更複雜的客戶資料見解。

如果已為所選類建立關係，則選擇&#x200B;**[!UICONTROL Relationships]**&#x200B;將顯示用於建立關係的欄位清單。 並非所有方案都使用或需要定義關係，因此關係部分通常不包含任何欄位。

若要進一步瞭解架構關係，包括如何使用UI定義它們，請造訪[本檔案，瞭解架構關係](../../xdm/tutorials/relationship-ui.md)。

![](../images/union-schema/union-schema-relationships.png)

從清單中選擇關係欄位會根據需要更新顯示的方案，以顯示突出顯示的關係欄位。 如果關係欄位是巢狀的，這可能包括展開多個欄位。

![](../images/union-schema/union-schema-select-relationship.png)

## 後續步驟

閱讀本指南，您現在知道如何使用[!DNL Experience Platform] UI檢視和導覽聯合結構。 有關方案的詳細資訊，包括方案在整個平台中的使用方式，請首先閱讀[XDM系統概述](../../xdm/home.md)。
