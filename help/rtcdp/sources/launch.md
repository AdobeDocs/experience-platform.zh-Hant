---
keywords: 啟動網頁標籤；網頁標籤啟動；網站標籤；網頁標籤；啟動；啟動
title: 教學課程使用Adobe Launch實作網站標籤
seo-title: 使用Adobe Launch實作網站標籤
description: 使用Adobe Launch在Adobe Experience Platform中實作網站標籤
seo-description: 使用Adobe Launch在Adobe Experience Platform中實作網站標籤
translation-type: tm+mt
source-git-commit: 00010d38a5d05800aeac9af8505093fee3593b45
workflow-type: tm+mt
source-wordcount: '493'
ht-degree: 8%

---


# 教學課程：使用Adobe Launch實作網站標籤

本教學課程說明如何實作網站標籤，以便使用Adobe Launch將資料傳送至Adobe Experience Platform。

## 必要條件

* 在[!DNL Platform]中建立必要的模式和資料集。
* 必要的設定已部署在Experience Edge中，且具有相符的設定ID和Edge網域。
* 公司CMS已設定為在每個頁面上提供JavaScript物件，並包含您傳送至平台所需的資料。

## 步驟

本教學課程包含下列步驟：

1. 安裝Adobe Experience Platform [!DNL Web SDK]擴充功能。
1. 建立規則，告知[!DNL Launch]要傳送哪些資料。
1. 將擴充功能和規則整合在程式庫中。

## 安裝Adobe Experience Platform [!DNL Web SDK]擴充功能

首先，安裝Adobe Experience Platform [!DNL Web SDK]擴充功能。

1. 在[!DNL Launch]中，開啟&#x200B;**[!UICONTROL 擴展]**&#x200B;頁籤。

   ![image](assets/launch-overview.png)

1. 從Launch Extension Catalog選取Adobe Experience Platform Web SDK擴充功能
配置螢幕隨即開啟。

   ![影像](assets/launch-extension-install.png)

   如需詳細資訊，請參閱[!DNL Launch]檔案中的[擴充功能](https://docs.adobe.com/content/help/en/launch/using/reference/manage-resources/extensions/overview.html)。

1. 設定擴充功能.

   您現在唯一需要的設定是：

   * **設定ID:** 指定您從Adobe代表取得的設定ID。
   * **邊緣網域：** 指定您從Adobe代表取得的邊緣網域。

1. 選擇&#x200B;**[!UICONTROL Save]**&#x200B;並繼續下一步。

## 建立規則以告知[!DNL Launch]要傳送哪些資料

接著，建立規則讓[!DNL Launch]知道您要傳送哪些資料至Adobe Experience Platform，以及您要在何時傳送。

1. 在&#x200B;**[!UICONTROL Rules]**&#x200B;標籤下，設定當[!DNL Launch]程式庫載入時，會在網站的每個新頁面上觸發的事件。

   ![影像](assets/launch-make-a-rule.png)

1. 新增動作.

   若要設定動作，請告訴[!DNL Launch]在何處尋找資料層。 資料層是存在於頁面上的JavaScript物件，會從轉譯網頁的相同CMS傳送。 提供資料物件的JavaScript路徑。

   ![影像](assets/launch-add-aep-action.png)

   您傳送的資料物件必須是有效的XDM，該XDM會針對連接至您的設定ID的資料集所使用的架構傳遞驗證。

1. 選擇&#x200B;**[!UICONTROL 保留更改]**。

如需詳細資訊，請參閱[!DNL Launch]檔案中的[Rules](https://docs.adobe.com/content/help/en/launch/using/reference/manage-resources/rules.html)。

## 將擴充功能和規則整合在程式庫中

接著，[將擴充功能](https://docs.adobe.com/content/help/en/launch/using/reference/publish/overview.html)與新規則整合在程式庫中，並在開發環境中測試這些變更。

![影像](assets/launch-add-changes-to-library.png)

完成測試後，請透過工作流程升級程式庫，以便將它部署至生產網站。 現在，資料正從每位使用者流向Adobe Experience Platform。

![影像](assets/launch-promote-library.png)

如需詳細資訊，請參閱[!DNL Launch]檔案中的[程式庫](https://docs.adobe.com/content/help/zh-Hant/launch/using/reference/publish/libraries.html)。