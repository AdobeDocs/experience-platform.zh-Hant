---
title: 使用標籤擴充功能安裝Web SDK
description: 使用Adobe Experience Cloud資料彙集參考Web SDK資料庫。
exl-id: ba8348c9-f642-4230-9f7f-4496d4154d83
source-git-commit: 58cd6300307881c3de7c52e07c401bf2ed908517
workflow-type: tm+mt
source-wordcount: '309'
ht-degree: 0%

---

# 使用標籤擴充功能安裝Web SDK

Adobe提供專屬的標籤擴充功能，可用來實作和設定Web SDK。 此實作方法是Adobe建議的主要方法，以便部署及維護資料收集程式碼。

一旦您符合[必要條件](overview.md)，您就可以使用下列步驟來部署Web SDK標籤擴充功能：

## 在標籤中安裝擴充功能

1. 使用您的Adobe ID憑證登入[experience.adobe.com](https://experience.adobe.com)。
1. 導覽至&#x200B;**[!UICONTROL 資料彙集]** > **[!UICONTROL 標籤]**。
1. 選取所需的標籤屬性，或建立標籤屬性。
1. 導覽至&#x200B;**[!UICONTROL 擴充功能]**，然後選取&#x200B;**[!UICONTROL 目錄]**&#x200B;索引標籤。
1. 找到並安裝&#x200B;**[!UICONTROL Adobe Experience Platform Web SDK]**&#x200B;擴充功能。
1. 為每個環境選取適當的沙箱和資料流，然後按一下[儲存]。**&#x200B;**

如需詳細資訊，請參閱有關如何[設定Web SDK標籤擴充功能](../../tags/extensions/client/web-sdk/web-sdk-extension-configuration.md)的檔案。

## Publish要開發的標籤程式碼

此標籤現已安裝Web SDK擴充功能。 您現在可以發佈標籤程式碼以用於開發環境。

1. 導覽至&#x200B;**[!UICONTROL 發佈流程]**，然後選取&#x200B;**[!UICONTROL 新增資料庫]**。
1. 為此程式庫指定所需的名稱，例如「新增Web SDK程式庫」。 將[!UICONTROL 環境]下拉式功能表設定為[開發]。
1. 選取&#x200B;**[!UICONTROL 新增所有變更的資源]**，然後按一下&#x200B;**[!UICONTROL 儲存並建置至開發]**。

## 在您的網站上安裝載入器程式碼

現在標籤程式碼已發佈，您可以將標籤載入器程式碼新增至您的網站。

1. 導覽至&#x200B;**[!UICONTROL 環境]**，然後按一下「開發」旁的方塊圖示，以開啟包含此環境安裝指示的強制回應視窗。
1. 複製內嵌程式碼並將其貼到網站的`<head>`標籤中。

## 填寫您的實作並發佈至生產環境

如需擴充功能本身的詳細資訊，請參閱[Web SDK擴充功能概觀](../../tags/extensions/client/web-sdk/overview.md)，如需導覽標籤介面的詳細資訊，請參閱[標籤概觀](../../tags/home.md)。
