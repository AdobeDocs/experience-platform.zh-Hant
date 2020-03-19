---
title: 教學課程使用Adobe Launch實作網站標籤
seo-title: 使用Adobe Launch實作網站標籤
description: 使用Adobe Launch在Adobe Experience Platform中實作網站標籤
seo-description: 使用Adobe Launch在Adobe Experience Platform中實作網站標籤
translation-type: tm+mt
source-git-commit: 3083f6fb25a331eb6dd1d9a63b65aa206481dcb3

---


# 教學課程：使用Adobe Launch實作網站標籤

本教學課程說明如何實作網站標籤，以便使用Adobe Launch將資料傳送至Adobe Experience Platform。

## 必要條件

* 必要的架構和資料集是在Platform中建立。
* 必要的設定已部署在Experience Edge中，且具有相符的設定ID和Edge網域。
* 公司CMS已設定為在每個頁面上提供JavaScript物件，並包含您傳送至平台所需的資料。

## 步驟

本教學課程包含下列步驟：

1. 安裝Adobe Experience Platform Web SDK擴充功能。
1. 建立規則，告知啟動要傳送的資料。
1. 將擴充功能和規則整合在程式庫中。

## 安裝Adobe Experience Platform Web SDK擴充功能

首先，安裝Adobe Experience Platform Web SDK擴充功能。

1. In Launch, open the **[!UICONTROL Extensions]** tab.

   ![影像](assets/launch-overview.png)

1. 從Launch Extension Catalog選取Adobe Experience Platform Web SDK擴充功能設定畫面隨即開啟。

   ![影像](assets/launch-extension-install.png)

   如需詳細資訊，請參 [閱Launch檔案](https://docs.adobe.com/content/help/en/launch/using/reference/manage-resources/extensions/overview.html) 中的擴充功能。

1. 設定擴充功能.

   您現在唯一需要的設定是：

   * **配置ID:** 指定您從Adobe代表取得的設定ID。
   * **邊緣網域：** 指定您從Adobe代表取得的邊緣網域。

1. 按一 **[!UICONTROL 下「儲存]** 」，然後繼續下一個步驟。

## 建立規則以告知啟動要傳送哪些資料

接著，建立規則讓Launch知道您要傳送哪些資料至Adobe Experience Platform，以及您要在何時傳送。

1. 在「規 **[!UICONTROL 則]** 」標籤下，設定在啟動程式庫載入時，會在網站的每個新頁面上觸發的事件。

   ![影像](assets/launch-make-a-rule.png)

1. 新增動作.

   若要設定動作，請告訴「啟動」尋找資料層的位置。 資料層是存在於頁面上的JavaScript物件，會從轉譯網頁的相同CMS傳送。 提供資料物件的JavaScript路徑。

   ![影像](assets/launch-add-aep-action.png)

   您傳送的資料物件必須是有效的XDM，該XDM會針對連接至您的設定ID的資料集所使用的架構傳遞驗證。

1. 按一下&#x200B;**[!UICONTROL 保留變更]**.

如需詳細資訊，請參 [閱](https://docs.adobe.com/content/help/en/launch/using/reference/manage-resources/rules.html) Launch檔案中的規則。

## 將擴充功能和規則整合在程式庫中

接著， [將擴充功能和新規則整合在程式庫中](https://docs.adobe.com/content/help/en/launch/using/reference/publish/overview.html) ，並在開發環境中測試這些變更。

![影像](assets/launch-add-changes-to-library.png)

完成測試後，請透過工作流程升級程式庫，以便將它部署至生產網站。 現在，資料正從每位個別使用者流向Adobe Experience Platform。

![影像](assets/launch-promote-library.png)

如需詳細資訊，請參 [閱Launch檔案中的](https://docs.adobe.com/content/help/en/launch/using/reference/publish/libraries.html) 「資料庫」。