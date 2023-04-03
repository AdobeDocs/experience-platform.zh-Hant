---
title: 實作Adobe Experience Platform Assurance延伸功能
description: 本指南說明如何實作和安裝Adobe Experience Platform Assurance擴充功能。
source-git-commit: 24f452bdb923179eefe53fdb28d3a92d43e533cd
workflow-type: tm+mt
source-wordcount: '400'
ht-degree: 2%

---


# 實作Adobe Experience Platform Assurance延伸功能

本教學課程說明如何在Mobile SDK中安裝及實作Platform Assurance擴充功能。 如需將保證擴充功能新增至應用程式的指示，請參閱 [Adobe Experience Platform Assurance擴充功能概觀](https://developer.adobe.com/client-sdks/documentation/platform-assurance-sdk/#add-the-aep-assurance-extension-to-your-app).

## 快速入門

若要安裝及實作Assurance擴充功能，您需要存取下列服務：

- 此 [Adobe Experience Platform資料收集UI](https://experience.adobe.com/#/data-collection/)
- [Adobe Experience Platform保障](https://experience.adobe.com/assurance)

## 建立行動 屬性

>[!NOTE]
>
>如果您已有行動屬性，則可繼續進行下一個步驟。

在資料收集UI中，選取 **[!UICONTROL 標籤]**. 隨即顯示行動裝置和Web屬性清單，其中包含您組織所屬屬性的相關資訊。 選擇 **[!UICONTROL 新屬性]** 來建立新屬性。

![系統會反白顯示「新屬性」按鈕，顯示您選取要建立新屬性的內容](./images/implement-assurance/create-new-property.png)

此 **[!UICONTROL 建立屬性]** 頁。 輸入新屬性的名稱並選取 **[!UICONTROL 行動]** 作為您的平台。 插入詳細資訊後，請選取 **[!UICONTROL 儲存]** 來建立行動屬性。

>[!NOTE]
>
>行動屬性的 **[!UICONTROL 隱私權]** 設定 **not** 會影響保證的資料收集。

![此時將顯示「建立屬性」頁。 您可以在此處插入行動屬性的相關資訊。](./images/implement-assurance/create-property.png)

## 安裝Assurance擴充功能

選取您要在中安裝Assurance擴充功能的行動屬性。

![此時會顯示「標籤屬性」頁面，並反白顯示選取的行動屬性。](./images/implement-assurance/select-mobile-property.png)

此 **行動屬性詳細資訊** 頁。 選擇 **[!UICONTROL 擴充功能]** 以開啟目前與您行動屬性相關聯的擴充功能清單。

![隨即顯示行動屬性詳細資訊頁面。 會顯示最近活動的相關資訊。 擴充功能標籤會反白顯示。](./images/implement-assurance/tag-properties.png)

選擇 **[!UICONTROL 目錄]** 若要查看可新增至行動屬性的擴充功能清單。 使用篩選器，找出 **[!UICONTROL AEP保證]** 擴充功能，然後選取 **[!UICONTROL 安裝]**.

![擴充功能目錄隨即顯示。 系統會篩選及顯示「保證」擴充功能，並反白顯示安裝按鈕。](./images/implement-assurance/assurance-extension.png)

## 後續步驟

現在您已在行動屬性中安裝「保證」擴充功能，即可開始在應用程式中使用「保證」。 若要了解如何將保證擴充功能新增至您的應用程式，請參閱 [Adobe Experience Platform Assurance擴充功能概觀](https://developer.adobe.com/client-sdks/documentation/platform-assurance-sdk/#add-the-aep-assurance-extension-to-your-app). 若要了解如何使用Assurance，請閱讀 [使用保證指南](./using-assurance.md).
