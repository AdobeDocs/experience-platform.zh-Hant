---
title: 實作 Adobe Experience Platform Assurance 擴充功能
description: 本指南會說明如何實作和安裝 Adob​​e Experience Platform Assurance 擴充功能。
exl-id: b7bd1bb1-1606-4d00-97e0-c329c86d8ca4
source-git-commit: 05a7b73da610a30119b4719ae6b6d85f93cdc2ae
workflow-type: ht
source-wordcount: '400'
ht-degree: 100%

---

# 實作 Adobe Experience Platform Assurance 擴充功能

本教學課程會說明如何在 Mobile SDK 中安裝和實作 Platform Assurance 擴充功能。如需有關如何將 Assurance 擴充功能新增到您的應用程式的說明，請閱讀 [Adobe Experience Platform Assurance 擴充功能概觀](https://developer.adobe.com/client-sdks/documentation/platform-assurance-sdk/#add-the-aep-assurance-extension-to-your-app)。

## 快速入門

為了安裝和實作 Assurance 擴充功能，您需要存取以下服務：

- [Adobe Experience Platform 資料集合 UI](https://experience.adobe.com/#/data-collection/)。
- [Adobe Experience Platform Assurance](https://experience.adobe.com/assurance)

## 建立行動資產

>[!NOTE]
>
>如果您已經擁有行動資產，則可以繼續進行下一步。

在資料集合 UI 中，選取&#x200B;**[!UICONTROL 標記]**。行動和 Web 屬性清單會隨即顯示，其中會包含有關屬於貴組織的屬性的資訊。選取&#x200B;**[!UICONTROL 新屬性]**，即可建立一個新的屬性。

![反白顯示「新增屬性」按鈕，以顯示您為了建立新屬性所選取的內容](./images/implement-assurance/create-new-property.png)

**[!UICONTROL 建立屬性]**&#x200B;頁面會隨即顯示。輸入新屬性的名稱並選取&#x200B;**[!UICONTROL 行動]**&#x200B;作為您的平台。插入您的詳細資料後，請選取&#x200B;**[!UICONTROL 儲存]**&#x200B;以建立行動資產。

>[!NOTE]
>
>行動資產的&#x200B;**[!UICONTROL 隱私]**&#x200B;設定並&#x200B;**不會**&#x200B;影響 Assurance 的資料集合。

![顯示「建立屬性」頁面。您可以在這裡插入有關您的行動資產的資訊。](./images/implement-assurance/create-property.png)

## 安裝 Assurance 擴充功能

選取要在其中安裝 Assurance 擴充功能的行動資產。

![顯示「標記屬性」頁面，其中會反白顯示選取的行動資產。](./images/implement-assurance/select-mobile-property.png)

**行動資產詳細資料**&#x200B;頁面會隨即顯示。選取&#x200B;**[!UICONTROL 擴充功能]**，以顯示目前和您的行動資產相關聯的擴充功能的清單。

![顯示「行動資產詳細資料」頁面。顯示&#x200B;最近活動的相關資訊。反白顯示擴充功能索引標籤。](./images/implement-assurance/tag-properties.png)

選取&#x200B;**[!UICONTROL 目錄]**，以查看可新增到行動資產的擴充功能的清單。使用篩選器，找到 **[!UICONTROL AEP Assurance]** 擴充功能，然後選取&#x200B;**[!UICONTROL 安裝]**。

![顯示擴充功能目錄。篩選並顯示 Assurance 擴充功能，並反白顯示「安裝」按鈕。](./images/implement-assurance/assurance-extension.png)

## 後續步驟

由於您已在行動資產中安裝了 Assurance 擴充功能，您可以開始在應用程式中使用 Assurance。若要了解如何將 Assurance 擴充功能新增到您的應用程式的說明，請閱讀 [Adobe Experience Platform Assurance 擴充功能概觀](https://developer.adobe.com/client-sdks/documentation/platform-assurance-sdk/#add-the-aep-assurance-extension-to-your-app)。若要了解如何使用 Assurance，請閱讀「[使用 Assurance 的指南](./using-assurance.md)」。
