---
keywords: Experience Platform；設定檔；即時客戶設定檔；統一設定檔；統一設定檔；統一；設定檔；rtcp；啟用設定檔；啟用設定檔；聯合結構；聯合設定檔；聯合設定檔
title: 聯合架構UI指南
topic-legacy: guide
type: Documentation
description: 在Adobe Experience Platform使用者介面(UI)中，您可以輕鬆檢視組織內的任何聯合結構，並預覽特定類別的欄位、身分、關係和貢獻結構。 本指南提供如何使用Platform UI檢視和探索聯合結構的詳細資訊。
exl-id: 52af0d77-e37d-4ed8-9dee-71a50b337b4e
source-git-commit: 34e0381d40f884cd92157d08385d889b1739845f
workflow-type: tm+mt
source-wordcount: '1199'
ht-degree: 2%

---

# [!UICONTROL 聯合架構] UI指南

在Adobe Experience Platform使用者介面(UI)中，您可以輕鬆檢視組織內的任何聯合結構，並預覽特定類別的欄位、身分、關係和貢獻結構。 本指南提供如何使用Platform UI檢視和探索聯合結構的詳細資訊。

## 快速入門

本UI指南需要了解 [!DNL Experience Platform] 與管理即時客戶設定檔資料相關的服務。 閱讀本指南或使用UI之前，請先檢閱本檔案以了解下列服務：

* [[!DNL Real-Time Customer Profile]](../home.md):根據來自多個來源的匯總資料，提供統一的即時消費者設定檔。
* [[!DNL Identity Service]](../../identity-service/home.md):啟用 [!DNL Real-Time Customer Profile] 將不同資料來源的身分擷取至 [!DNL Platform].
* [[!DNL Experience Data Model (XDM)]](../../xdm/home.md):標準化框架 [!DNL Platform] 組織客戶體驗資料。

## 了解聯合結構

即時客戶個人檔案可讓您建立強大且集中的設定檔，其中包含客戶屬性和時間戳記事件，每個客戶在與Adobe Experience Platform整合的系統間互動。 此資料的格式和結構由Experience Data Model(XDM)結構提供，每個結構都以XDM類別為基礎，並包含與該類別相容的欄位。

可針對多個使用案例建立結構，參考相同的類別，但包含其使用的特定欄位。 為設定檔啟用結構時，它會成為聯合結構的一部分。 換言之，聯合結構由多個結構組成，這些結構共用相同的類別，並且已為設定檔啟用。 聯合結構描述讓您能夠查看共用相同類別的結構描述中包含的所有欄位的合併。「即時客戶設定檔」使用聯合結構來建立每個客戶的整體檢視。

若要使用聯合結構，您必須深入了解XDM結構。 如需詳細資訊，請先閱讀 [綱要構成基本知識](../../xdm/schema/composition.md).

## 查看聯合結構

若要導覽至Platform UI中的聯合結構，請選取 **[!UICONTROL 設定檔]** 從左側導覽器中，選取 **[!UICONTROL 聯合架構]** 標籤。 此 [!UICONTROL 聯合架構] 頁簽開啟，以顯示當前所選類的聯合架構。

![此時將顯示「聯合架構」頁，並突出顯示「配置檔案」和「聯合架構」頁簽。](../images/union-schema/landing.png)

## 選擇類

若要顯示特定XDM類別的聯合架構，請從 **[!UICONTROL 類別]** 下拉式清單。 由於並非所有類都具有聯合結構，因此下拉式清單中僅提供具有聯合結構的類（即已針對設定檔啟用結構的類）。

選擇類後，顯示的架構將更新以反映所選類的聯合架構。 例如，您可以選取 **[!UICONTROL XDM個別設定檔]** 查看該類的聯合架構。

![會反白顯示包含聯合架構類別的下拉式清單。](../images/union-schema/class.png)

## 探索聯合結構

您可以上下滾動查看完整架構結構並選擇右括弧(`>`)以展開巢狀欄位。

![聯合架構內的一組巢狀欄位會展開。](../images/union-schema/explore.png)

選擇任何欄位以查看其詳細資訊，包括顯示名稱、資料類型、說明、路徑、建立日期和上次修改日期。 您也可以檢視包含您所選欄位的貢獻結構清單。

![會強調顯示聯合架構欄位。 右側邊欄上會顯示醒目提示欄位的詳細資訊。](../images/union-schema/explore-field.png)

選取貢獻結構的名稱會顯示與該結構相關的資料集名稱，這些資料集會將資料擷取至選取的欄位。 每個資料集名稱都會以連結的形式顯示。 選取資料集名稱會在新視窗中開啟該資料集的活動索引標籤。

如需資料集的詳細資訊，包括在UI中檢視資料集活動和預覽資料集資料，請造訪 [資料集UI指南](../../catalog/datasets/user-guide.md).

![系統會強調顯示與結構相關的資料集清單。](../images/union-schema/datasets.png)

## 檢視貢獻結構

您也可以選取 **[!UICONTROL 所有貢獻結構]** 展開結構清單。 根據您選取的類別和貴組織在Platform中建立的結構數目，這可以是包含單一結構的簡短清單，或是包含許多結構的長清單。

![會反白顯示貢獻聯合結構的結構清單。](../images/union-schema/contributing-schemas.png)

選擇特定架構的名稱將突出顯示聯合架構中屬於所選架構的欄位。 選取結構後，聯合結構會以黑色列顯示為灰色，指出參與結構的一部分欄位。

![會反白顯示選取的貢獻結構。 屬於貢獻結構一部分的欄位會維持為黑色，而非貢獻結構一部分的欄位則會呈現灰色。](../images/union-schema/select-schema.png)

## 檢視身分

透過UI，您可以選取 **[!UICONTROL 身分]** 來展開清單。

![會強調顯示屬於聯合架構的身分。](../images/union-schema/identities.png)

從清單中選取個別身分會視需要自動更新顯示的架構，以顯示身分欄位。 如果巢狀內嵌身分欄位，這可能包括展開多個欄位。

聯合架構中會強調顯示身分欄位，而身分的詳細資訊會顯示在畫面的右側。 詳細資訊包含包含身分欄位的貢獻結構清單，您可以向下切入，尋找與要將資料擷取至所選身分欄位之結構相關資料集的連結。

![會反白顯示選取的身分。 右側邊欄上會顯示所選身分的詳細資訊。](../images/union-schema/select-identity.png)

## 查看關係

聯合架構UI還允許您查看已根據所選架構類為架構定義的關係。 定義關係是將屬於不同類別的兩個結構連接起來的方式，以便對客戶資料取得更複雜的深入分析。

如果已為所選類建立關係，則選擇 **[!UICONTROL 關係]** 顯示用於建立關係的欄位清單。 並非所有結構都使用或需要定義關係，因此關係區段通常不包含任何欄位。

若要進一步了解結構關係，包括如何使用UI定義關係，請造訪 [關於方案關係的文檔](../../xdm/tutorials/relationship-ui.md).

![將突出顯示屬於聯合架構的關係。](../images/union-schema/relationships.png)

從清單中選擇關係欄位會根據需要更新顯示的架構，以顯示突出顯示的關係欄位。 如果巢狀內嵌關係欄位，這可能包括展開多個欄位。

![所選關係將突出顯示。 關係的對應欄位也會反白顯示。](../images/union-schema/select-relationship.png)

## 後續步驟

閱讀本指南後，您現在知道如何使用 [!DNL Experience Platform] UI。 如需結構的詳細資訊，包括如何在整個Platform中使用結構，請先閱讀 [XDM系統概觀](../../xdm/home.md).
