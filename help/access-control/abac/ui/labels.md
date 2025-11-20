---
keywords: Experience Platform；首頁；熱門主題；存取控制；屬性型存取控制；ABAC
title: Attribute-based Access Control Manage Labels
description: This document provides information on managing labels through the Permissions interface in Adobe Experience Cloud
exl-id: c790f09c-fda6-48bf-95db-3f5053cd882e
source-git-commit: fded2f25f76e396cd49702431fa40e8e4521ebf8
workflow-type: tm+mt
source-wordcount: '238'
ht-degree: 26%

---

# 管理標籤

>[!NOTE]
>
>To create or view computed attributes with fields containing a given label, you must have access to that label.

Labels allow you to categorize datasets and fields according to usage and access policies that apply to that data. 標籤可隨時套用，提供您選擇控管資料方式的靈活性。 最佳實務建議在資料內嵌至Experience Platform後立即加上標籤，或資料可在Experience Platform中使用後立即加上標籤。

## 建立新標籤 {#create-new-label}

>[!CONTEXTUALHELP]
>id="platform_abac_labelusage"
>title="標籤使用"
>abstract="您可以使用自訂標籤，將資料控管和存取權控制的設定套用至您的資料。"

>[!CONTEXTUALHELP]
>id="platform_permissions_labels_about_create"
>title="建立新標籤"
>abstract="您可以建立適合您組織需求的自訂標籤。自訂標籤可用於資料控管和存取控制設定套用到您的資料。"
>additional-url="https://experienceleague.adobe.com/docs/experience-platform/data-governance/labels/overview.html#manage-labels" text="管理自訂標籤"

>[!NOTE]
>
>There is one single list of labels for a whole organization. To create a custom label, you will need **[!UICONTROL Manage Usage Labels]** permissions on the production sandbox. Label deletion is currently not supported.

To create a new label, select the **[!UICONTROL Labels]** tab in the sidebar and select **[!UICONTROL Create Label]**.

![flac-new-label](../../images/flac-ui/create-label.png)

The **[!UICONTROL Create a new label]** dialog appears, prompting you to enter a name, an optional friendly name and an optional description.

![new-label-info](../../images/flac-ui/new-label-info.png)

完成後，選取&#x200B;**[!UICONTROL Confirm]**。
