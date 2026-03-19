---
title: Adobe Advertising 設定
description: 啟用或停用Demand-side Platform功能。
exl-id: 594fd75d-bb13-4146-9105-1398e24c4c16
source-git-commit: 6c05d8abde0e4d6b07fe37d6e3eacd5d3dd67ec2
workflow-type: tm+mt
source-wordcount: '209'
ht-degree: 25%

---

# Adobe Advertising 設定 {#advertising}

>[!AVAILABILITY]
>
>適用於Web SDK的Adobe Advertising目前處於&#x200B;**測試版**。 功能和檔案可能會有所變更。

>[!CONTEXTUALHELP]
>id="platform_tags_websdk_advertising"
>title="Adobe Advertising"
>abstract="進行 Adobe Advertising 整合相關設定。請注意，啟用點進測量不需要廣告設定。Search、Social 和 Commerce 的用戶端不需採取其他動作，不過，需求方平台 (DSP) 使用者必須在此區段中設定廣告商才能測量瀏覽後轉換。"

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
