---
title: Adobe Advertising組態設定
description: 啟用或停用Demand-side Platform功能。
source-git-commit: 526cb473a6288f367db9cb00c0277cce7543cd57
workflow-type: tm+mt
source-wordcount: '164'
ht-degree: 0%

---

# Adobe Advertising組態設定

>[!AVAILABILITY]
>
>適用於Web SDK的Adobe Advertising目前處於&#x200B;**測試版**。 功能和檔案可能會有所變更。

**[!UICONTROL Adobe Advertising]**&#x200B;區段可讓您啟用或停用Demand-side Platform (DSP)功能（若用於您的實施）。 如果您的實作使用DSP，則只需設定此欄位。

1. 使用您的Adobe ID憑證登入[experience.adobe.com](https://experience.adobe.com)。
1. 導覽至&#x200B;**[!UICONTROL Data Collection]** > **[!UICONTROL Tags]**。
1. 選取所需的標籤屬性。
1. 導覽至&#x200B;**[!UICONTROL Extensions]**，然後選取&#x200B;**[!UICONTROL Configure]**&#x200B;卡片上的[!UICONTROL Adobe Experience Platform Web SDK]。
1. 向下捲動至&#x200B;**[!UICONTROL Adobe Advertising]**&#x200B;區段。

目前有一個可用選項。

## [!UICONTROL Adobe Advertising DSP]

可啟用或停用Adobe Advertising DSP功能的下拉式功能表。

* **[!UICONTROL Enabled]**：啟用瀏覽追蹤。
* **[!UICONTROL Disabled]**：停用閱覽追蹤。

啟用時，可使用下列設定：

* **[!UICONTROL Advertisers]**：要為其啟用閱覽追蹤的廣告商。
* **[!UICONTROL ID5 partner ID]**：選擇性。 您組織的ID5合作夥伴ID。 此設定允許網頁SDK收集ID5通用ID。
* **[!UICONTROL RampID JavaScript path]**：選擇性。 您組織的[!DNL LiveRamp RampID] JavaScript程式碼的路徑(`ats.js`)。  此設定可讓Web SDK收集[!DNL RampID]個通用ID。
