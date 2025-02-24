---
title: Adobe Content Analytics擴充功能概觀
description: 瞭解Adobe Experience Platform中的Adobe Content Analytics標籤擴充功能。
hide: true
hidefromtoc: true
source-git-commit: d6288d9515d7efaf874cb056f06d04b2002fd369
workflow-type: tm+mt
source-wordcount: '532'
ht-degree: 0%

---

# Adobe Content Analytics擴充功能概觀

[!DNL Adobe Content Analytics]標籤延伸允許追蹤網站上的內容相關事件。 此擴充功能會透過Experience Platform Edge Network，從Web屬性將內容資料（體驗和資產）傳送至Adobe Experience Cloud中的資料流。

擴充功能可讓您將特定內容相關事件資料串流到Platform，以便在Customer Journey Analytics的內容分析報表中使用該資料。

本檔案說明如何在標籤UI中設定標籤擴充功能。

## 安裝Adobe Content Analytics標籤擴充功能 {#install}

>[!NOTE]
>
>Adobe Content Analytics標籤擴充功能會作為標籤屬性的一部分自動安裝，在使用[Content Analytics引導式設定精靈](https://experienceleague.adobe.com/en/docs/analytics-platform/using/content-analytics/configuration/guided){target="_blank"}時自動建立。


### 手動安裝

若是手動設定，Adobe Content Analytics標籤擴充功能需要安裝屬性。 如果您尚未這樣做，請參閱有關[建立標籤屬性](https://experienceleague.adobe.com/en/docs/platform-learn/implement-in-websites/configure-tags/create-a-property)的檔案。

建立屬性之後，或選取使用[Content Analytics引導式設定精靈](https://experienceleague.adobe.com/en/docs/analytics-platform/using/content-analytics/configuration/guided)建立的屬性時，請開啟屬性並選取左側列的&#x200B;**[!UICONTROL 擴充功能]**&#x200B;標籤。

選取&#x200B;**[!UICONTROL 目錄]**&#x200B;索引標籤。 從可用的擴充功能清單中，尋找&#x200B;**[!DNL Adobe Content Analytics]**&#x200B;擴充功能，然後選取&#x200B;**[!UICONTROL 安裝]**。

![影像顯示已選取Web SDK擴充功能的Tags UI](assets/aca-tag-install.png)

選取&#x200B;**[!UICONTROL 安裝]**&#x200B;後，您必須設定Adobe Content Analytics標籤擴充功能並儲存設定。


<!--
## Configure schema

The [Content Analytics guided configuration wizard](https://experienceleague.adobe.com/en/docs/analytics-platform/using/content-analytics/configuration/guided) automatically populates the proper value for the **[!UICONTROL Tenant Schema Name]**. 

![Image that shows the Schema configuration of the Adobe Content Analytics tag extension in the Tags UI](assets/aca-tag-schema.png)

>[!WARNING]
>
>Do not modify the value for **[!UICONTROL Tenant Schema Name]**.

-->

## 設定資料串流

[Content Analytics引導式設定精靈](https://experienceleague.adobe.com/en/docs/analytics-platform/using/content-analytics/configuration/guided)會自動選取&#x200B;**[!UICONTROL 沙箱]**&#x200B;和&#x200B;**[!UICONTROL 生產資料流]**&#x200B;的適當值。 您可以選擇設定其他&#x200B;**[!UICONTROL 中繼資料流]**&#x200B;和&#x200B;**[!UICONTROL 開發資料流]**。

![此影像顯示標籤UI中Adobe Content Analytics標籤擴充功能的「資料串流」設定](assets/aca-tag-datastreams.png)

您可以覆寫&#x200B;**[!UICONTROL 沙箱]**&#x200B;和&#x200B;**[!UICONTROL 生產資料流]**&#x200B;的自動選取值，以備您想要在不同沙箱上使用內容分析並搭配不同資料流時使用。 這樣做時，您可以從可用的下拉式功能表中選取沙箱和資料流，或選取&#x200B;**[!UICONTROL 輸入值]**&#x200B;並為每個環境輸入自訂資料流ID。

>[!IMPORTANT]
>
>當您設定另一個沙箱和資料串流時，請確保
>
>* 選取的沙箱尚未與其他Content Analytics設定建立關聯，並且
>* 任何選取的資料流都會將Experience Platform服務設定為已啟用的Content Analytics體驗事件資料集。

請參閱[資料串流](../../../../datastreams/overview.md)指南，瞭解如何設定資料串流。



## 設定事件篩選

在&#x200B;**[!UICONTROL 事件篩選]**&#x200B;區段中，您可以修改規則運算式，以便在收集Content Analytics的資料時篩選&#x200B;**[!UICONTROL 頁面URL]**&#x200B;和&#x200B;**[!UICONTROL Assets URL]**。 您在[Content Analytics引導式設定精靈](https://experienceleague.adobe.com/en/docs/analytics-platform/using/content-analytics/configuration/guided)中定義的規則運算式會自動填入。

![此影像顯示標籤UI中Adobe Content Analytics標籤擴充功能的事件篩選設定](assets/aca-tag-eventfiltering.png)


### 範例

* 您想從Content Analytics排除所有檔案頁面。<br/>使用以下規則運算式： `^(?!.*documentation).*`
* 您想從Content Analytics排除所有標誌JPEG和SVG影像。<br/>使用以下規則運算式： `^(?!.*(logo\.jpg|\.svg)).*$`

您可以使用&#x200B;**[!UICONTROL 測試Regex]**，在&#x200B;**[!UICONTROL 規則運算式測試器]**&#x200B;中測試您的規則運算式。

![在標籤UI中顯示Adobe Content Analytics標籤擴充功能之規則運算式測試器的影像](assets/aca-tag-regextester.png)

