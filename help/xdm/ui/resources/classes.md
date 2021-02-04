---
keywords: Experience Platform;home；熱門主題；api;API;XDM;XDM系統；體驗資料模型；ui;workspace;class;classes;
solution: Experience Platform
title: 在UI中建立和編輯類別
description: 瞭解如何在Experience Platform使用者介面中建立和編輯類別。
topic: user guide
translation-type: tm+mt
source-git-commit: 5bf729197de53e9d24675c8a1d0455e807fb90c5
workflow-type: tm+mt
source-wordcount: '886'
ht-degree: 0%

---


# 在UI中建立和編輯類別

在Experience Data Model(XDM)中，類定義模式將包含的資料的行為方面（記錄或時間序列）。 此外，類還描述了基於該類的所有方案需要包含的最小公共屬性數，並為合併多個相容資料集提供了一種方法。

Adobe提供數種標準（「核心」）XDM類別，包括[!DNL XDM Individual Profile]和[!DNL XDM ExperienceEvent]。 除了這些核心類別外，您也可以建立自己的自訂類別，以說明組織的更多特定使用案例。

本檔案概述如何在Adobe Experience Platform UI中建立、編輯和管理自訂類別。

## 必要條件

本指南需要對XDM System有充分的瞭解。 請參閱[XDM概述](../../home.md)以瞭解XDM在Experience Platform生態系統中的角色，以及[架構構成基礎](../../schema/composition.md)以瞭解類對XDM架構的貢獻。

雖然本指南不是必要的，但建議您也要遵循在UI](../../tutorials/create-schema-ui.md)中構成架構的[教學課程，以熟悉[!DNL Schema Editor]的各種功能。

## 建立新類{#create}

在&#x200B;**[!UICONTROL 方案]**&#x200B;工作區中，選擇&#x200B;**[!UICONTROL 建立方案]**，然後從下拉式清單中選擇&#x200B;**[!UICONTROL 瀏覽]**。

![](../../images/ui/resources/classes/browse-classes.png)

此時將出現一個對話框，允許您從可用類清單中進行選擇。 在對話框頂部，選擇&#x200B;**[!UICONTROL 建立新類]**。 然後，您可以為新類提供顯示名稱（類的簡短、描述性、唯一且用戶友好的名稱）、說明，以及模式將定義的資料的行為（&quot;[!UICONTROL Record]&quot;或&quot;[!UICONTROL Time-series]&quot;）。

完成後，選擇&#x200B;**[!UICONTROL Assign class]**。

![](../../images/ui/resources/classes/class-details.png)

此時會出現[!DNL Schema Editor]，顯示畫布中基於您剛建立的自定義類的新模式。 由於尚未將欄位添加到類中，因此方案只包含`_id`欄位，該欄位表示系統生成的唯一標識符，該標識符自動應用於[!DNL Schema Registry]中的所有資源。

![](../../images/ui/resources/classes/schema.png)

>[!IMPORTANT]
>
>當建立實作組織定義之類的架構時，請記住混合僅可用於相容類。 由於您定義的類是新的，因此在&#x200B;**[!UICONTROL Add mixin]**&#x200B;對話方塊中沒有列出相容的混音。 而是需要[建立新的mixins](./mixins.md#create)，以便與該類別搭配使用。 下次構建實施新類的模式時，您定義的混合將列出並可供使用。

您現在可以開始向類[添加欄位，該類將由採用該類的所有方案共用。](#add-fields)

## 編輯現有類{#edit}

>[!NOTE]
>
>只有您組織定義的自訂類別才能完整編輯和自訂。 對於Adobe定義的核心類，在個別結構描述的上下文中只能編輯其欄位的顯示名稱。 有關詳細資訊，請參閱[編輯架構欄位的顯示名稱一節。](./schemas.md#display-names)
>
>在儲存自訂類別並用於資料擷取後，之後只能對它進行加法變更。 如需詳細資訊，請參閱[模式演化規則](../../schema/composition.md#evolution)。

要編輯現有類，請選擇&#x200B;**[!UICONTROL Browse]**&#x200B;頁籤，然後選擇使用要編輯的類的方案名稱。

![](../../images/ui/resources/classes/select-for-edit.png)

>[!TIP]
>
>您可以使用工作區的搜尋和篩選功能，協助您更輕鬆地尋找結構。 如需詳細資訊，請參閱[探索XDM資源](../explore.md)指南。

出現[!DNL Schema Editor]，畫布中顯示結構。 您現在可以開始向類[添加欄位。](#add-fields)

![](../../images/ui/resources/classes/edit.png)

## 將欄位添加到{#add-fields}類

在[!UICONTROL 架構編輯器]中開啟了使用自定義類的架構後，可以開始向該類添加欄位。 要添加新欄位，請選擇方案名稱旁的&#x200B;**加號(+)**&#x200B;表徵圖。

![](../../images/ui/resources/classes/add-field.png)

>[!IMPORTANT]
>
>請記住，您新增至類別的任何欄位，都會用於採用該類別的所有結構中。 因此，您應仔細考慮哪些欄位在所有架構使用案例中都有用。 如果您正在考慮新增欄位，而該欄位可能只會在此類別下的某些結構中使用，則可能想要考慮透過[改為建立mixin](./mixins.md#create)將它新增至這些結構。

畫布中會顯示&#x200B;**[!UICONTROL 新欄位]**，右側欄位會更新，顯示設定欄位屬性的控制項。 有關如何配置欄位並將其添加到類的具體步驟，請參閱UI](../fields/overview.md#define)中[定義欄位的指南。

繼續將所需的欄位新增至類別。 完成後，選擇&#x200B;**[!UICONTROL Save]**&#x200B;以保存模式和類。

![](../../images/ui/resources/classes/save.png)

如果您先前已建立採用此類別的架構，新新增的欄位將自動顯示在這些架構中。

## 更改方案{#schema}的類

在初始建立過程中，可以在保存模式之前，隨時更改該模式的類。 有關詳細資訊，請參閱[建立和編輯方案](./schemas.md#change-class)的指南。

## 後續步驟

本檔案說明如何使用平台UI建立和編輯類別。 有關[!UICONTROL 方案]工作區功能的詳細資訊，請參閱[[!UICONTROL 方案]工作區概述](../overview.md)。

要瞭解如何使用[!DNL Schema Registry] API管理類，請參見[類端點指南](../../api/classes.md)。