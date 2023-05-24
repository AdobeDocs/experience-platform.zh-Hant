---
title: 執行Adobe Experience Platform保證延期
description: 本指南說明如何實施和安裝Adobe Experience Platform保障擴展。
exl-id: b7bd1bb1-1606-4d00-97e0-c329c86d8ca4
source-git-commit: 05a7b73da610a30119b4719ae6b6d85f93cdc2ae
workflow-type: tm+mt
source-wordcount: '400'
ht-degree: 3%

---

# 執行Adobe Experience Platform保證延期

本教程介紹如何在移動SDK中安裝和實施平台保障擴展。 有關將保障擴展添加到應用程式的說明，請閱讀 [Adobe Experience Platform保證延期概述](https://developer.adobe.com/client-sdks/documentation/platform-assurance-sdk/#add-the-aep-assurance-extension-to-your-app)。

## 快速入門

要安裝和實施保障擴展，您需要訪問以下服務：

- 的 [Adobe Experience Platform資料收集UI](https://experience.adobe.com/#/data-collection/)
- [Adobe Experience Platform Assurance](https://experience.adobe.com/assurance)

## 建立行動 屬性

>[!NOTE]
>
>如果您已經擁有移動屬性，則可以繼續下一步。

在資料收集UI中，選擇 **[!UICONTROL 標籤]**。 此時將顯示移動和Web屬性清單，其中包含屬於您組織的屬性的資訊。 選擇 **[!UICONTROL 新建屬性]** 的子菜單。

![「新建屬性」按鈕將突出顯示，顯示您選擇建立新屬性的內容](./images/implement-assurance/create-new-property.png)

的 **[!UICONTROL 建立屬性]** 的子菜單。 輸入新屬性的名稱並選擇 **[!UICONTROL 移動]** 作為平台。 插入詳細資訊後，選擇 **[!UICONTROL 保存]** 的子菜單。

>[!NOTE]
>
>移動屬性 **[!UICONTROL 隱私]** 設定 **不** 影響Assurance的資料收集。

![此時將顯示「建立屬性」頁。 您可以在此處插入有關移動屬性的資訊。](./images/implement-assurance/create-property.png)

## 安裝Assurance擴展

選擇要在中安裝保障擴展的移動屬性。

![將顯示「標籤屬性」頁，並突出顯示選定的移動屬性。](./images/implement-assurance/select-mobile-property.png)

的 **移動屬性詳細資訊** 的子菜單。 選擇 **[!UICONTROL 擴展]** 以顯示當前與移動屬性關聯的擴展的清單。

![將顯示移動屬性詳細資訊頁面。 將顯示有關最近活動的資訊。 加亮顯示擴展頁籤。](./images/implement-assurance/tag-properties.png)

選擇 **[!UICONTROL 目錄]** 查看可添加到mobile屬性的擴展清單。 使用篩選器，找到 **[!UICONTROL AEP保證]** 擴展，然後選擇 **[!UICONTROL 安裝]**。

![將顯示擴展目錄。 「Assurance extension（保證擴展）」將被篩選並顯示，並選中安裝按鈕。](./images/implement-assurance/assurance-extension.png)

## 後續步驟

現在，您已在移動屬性中安裝了保障擴展，您可以開始在應用程式中使用保障。 要瞭解如何將保障擴展添加到您的應用程式，請閱讀 [Adobe Experience Platform保證延期概述](https://developer.adobe.com/client-sdks/documentation/platform-assurance-sdk/#add-the-aep-assurance-extension-to-your-app)。 要瞭解如何使用保證，請閱讀 [使用保障指南](./using-assurance.md)。
