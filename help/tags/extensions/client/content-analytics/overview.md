---
title: Adobe Content Analytics擴充功能概觀
description: 瞭解Adobe Experience Platform中的Adobe Content Analytics標籤擴充功能。
exl-id: fcc46c86-e765-4bc7-bfdf-b8b10e8afacc
source-git-commit: 5f852b69b0eb0a5e6a9119f14eb9e1f51c8a2e33
workflow-type: tm+mt
source-wordcount: '658'
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

選取&#x200B;**[!UICONTROL 安裝]**&#x200B;之後，您必須設定Adobe Content Analytics標籤延伸並儲存設定。


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

您可以覆寫&#x200B;**[!UICONTROL 沙箱]**&#x200B;和&#x200B;**[!UICONTROL 生產資料流]**&#x200B;的自動選取值，以備您想在其他沙箱上搭配不同的資料流使用Content Analytics時使用。 這樣做時，您可以從可用的下拉式功能表中選取沙箱和資料流，或選取&#x200B;**[!UICONTROL 輸入值]**&#x200B;並為每個環境輸入自訂資料流ID。

>[!IMPORTANT]
>
>當您設定另一個沙箱和資料串流時，請確保
>
>* 選取的沙箱尚未與其他Content Analytics設定建立關聯，並且
>* 任何選取的資料流都會將Experience Platform服務設定為已啟用的Content Analytics體驗事件資料集。

請參閱[資料串流](../../../../datastreams/overview.md)指南，瞭解如何設定資料串流。

## 設定體驗擷取和定義

在&#x200B;**[!UICONTROL 體驗擷取與定義]**&#x200B;區段中，您可以啟用&#x200B;**[!UICONTROL 包含體驗]**，以便在為Content Analytics收集資料時包含體驗。

![影像顯示延伸模組](assets/aca-tag-experiencecapture.png)中的體驗擷取與定義區段

1. 啟用&#x200B;**[!UICONTROL 包含體驗]**。
1. 選擇性。 指定在您的網站上呈現內容的方式。 引數是&#x200B;**[!UICONTROL 網域規則運算式]**&#x200B;和&#x200B;**[!UICONTROL 查詢引數]**&#x200B;的零個或多個組合。
   1. 輸入&#x200B;**[!UICONTROL 網域規則運算式]**，例如`^(?!.*\b(store|help|admin)\b)`。
   1. 指定&#x200B;**[!UICONTROL 查詢引數]**&#x200B;的逗號分隔清單，例如`outdoors, patio, kitchen`。
使用![關閉](./assets/CrossSize300.svg)刪除個別引數，或使用&#x200B;**[!UICONTROL 全部清除]**&#x200B;刪除所有引數。
1. 如果要移除網域規則運算式和查詢引數的組合，請選取&#x200B;**[!UICONTROL 移除]**。
1. 如果要新增其他規則運算式和查詢參陣列合，請選取&#x200B;**[!UICONTROL 新增Regex]**。

## 設定事件篩選

在&#x200B;**[!UICONTROL 事件篩選]**&#x200B;區段中，您可以修改規則運算式，以便在為Content Analytics收集資料時篩選&#x200B;**[!UICONTROL 頁面URL]**&#x200B;和&#x200B;**[!UICONTROL Assets URL]**。 您在[Content Analytics引導式設定精靈](https://experienceleague.adobe.com/en/docs/analytics-platform/using/content-analytics/configuration/guided)中定義的規則運算式會自動填入。

![此影像顯示標籤UI中Adobe Content Analytics標籤擴充功能的事件篩選設定](assets/aca-tag-eventfiltering.png)


### 範例

* 您想從Content Analytics排除所有檔案頁面。<br/>使用以下規則運算式： `^(?!.*documentation).*`
* 您想從Content Analytics中排除所有標誌JPEG和SVG影像。<br/>使用以下規則運算式： `^(?!.*(logo\.jpg|\.svg)).*$`

您可以使用&#x200B;**[!UICONTROL 測試Regex]**，在&#x200B;**[!UICONTROL 規則運算式測試器]**&#x200B;中測試您的規則運算式。

![在標籤UI中顯示Adobe Content Analytics標籤擴充功能之規則運算式測試器的影像](assets/aca-tag-regextester.png)

