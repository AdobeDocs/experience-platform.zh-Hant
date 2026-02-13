---
title: 資料流組態設定
description: 設定資料串流，以使用網頁SDK標籤擴充功能將資料傳送至。
exl-id: 2d2504c6-b3f9-4e7b-aff4-a8d8d6c4e3dd
source-git-commit: 6c05d8abde0e4d6b07fe37d6e3eacd5d3dd67ec2
workflow-type: tm+mt
source-wordcount: '251'
ht-degree: 1%

---

# 資料流組態設定 {#datastreams}

>[!CONTEXTUALHELP]
>id="platform_tags_websdk_datastreams"
>title="資料串流"
>abstract="必填。在Edge Network中設定您想要傳送資料的目的地資料流。"

此設定區段可讓您決定要將資料傳送至哪個[資料流](/help/datastreams/overview.md)。 **所有傳送至Edge Network的資料都需要資料串流識別碼。**

1. 使用您的Adobe ID憑證登入[experience.adobe.com](https://experience.adobe.com)。
1. 導覽至&#x200B;**[!UICONTROL Data Collection]** > **[!UICONTROL Tags]**。
1. 選取所需的標籤屬性。
1. 導覽至&#x200B;**[!UICONTROL Extensions]**，然後選取&#x200B;**[!UICONTROL Configure]**&#x200B;卡片上的[!UICONTROL Adobe Experience Platform Web SDK]。
1. 向下捲動至&#x200B;**[!UICONTROL Datastreams]**&#x200B;區段。

![此影像顯示標籤UI中Web SDK標籤擴充功能的資料流設定](../assets/web-sdk-ext-datastreams.png)

選取資料串流時，您可以對每個[環境](/help/tags/ui/publishing/environments.md) （[!UICONTROL Development]、[!UICONTROL Staging]和[!UICONTROL Production]）執行此操作。 如果您想要將開發、測試和生產環境之間傳送的資料分開，這些欄位就十分實用。 它提供了便利的工作流程，只要在每個個別環境中安裝正確的標籤載入器，您就不需要擔心傳送資料到錯誤的資料流。

您可以使用下列其中一種方法填入資料串流ID：

* **[!UICONTROL Choose from list]**：每個環境都包含兩個下拉式功能表，可讓您為選取的環境選取沙箱和資料流。 每個下拉式功能表中的值取決於您在每個[沙箱](/help/datastreams/overview.md)中設定的[資料串流](/help/sandboxes/ui/overview.md)。

* **[!UICONTROL Enter values]**：除了使用下拉式功能表選取所需的資料流外，您也可以直接手動指定所需的資料流ID。 每個環境都可讓您直接輸入資料串流ID，或使用[資料元素](/help/tags/ui/managing-resources/data-elements.md)填入此欄位。
