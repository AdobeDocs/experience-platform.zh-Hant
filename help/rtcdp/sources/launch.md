---
keywords: launch web tags;web tags launch;website tags;web tags;launch;Launch
title: 教學課程使用Adobe Launch實作網站標籤
seo-title: 使用Adobe Launch實作網站標籤
description: 使用Adobe Launch在Adobe Experience Platform中實作網站標籤
seo-description: 使用Adobe Launch在Adobe Experience Platform中實作網站標籤
translation-type: tm+mt
source-git-commit: 54df4778a025811504801306120bda78e04281c1
workflow-type: tm+mt
source-wordcount: '481'
ht-degree: 9%

---


# 教學課程：使用Adobe Launch實作網站標籤

本教學課程說明如何實作網站標籤，以便使用Adobe Launch將資料傳送至Adobe Experience Platform。

## 必要條件

* 必要的模式和資料集在中建立 [!DNL Platform]。
* 必要的設定已部署在Experience Edge中，且具有相符的設定ID和Edge網域。
* 公司CMS已設定為在每個頁面上提供JavaScript物件，並包含您傳送至平台所需的資料。

## 步驟

本教學課程包含下列步驟：

1. 安裝Adobe Experience Platform擴充 [!DNL Web SDK] 功能。
1. 建立規則，告知要 [!DNL Launch] 傳送哪些資料。
1. 將擴充功能和規則整合在程式庫中。

## 安裝Adobe Experience Platform擴充功 [!DNL Web SDK] 能

首先，安裝Adobe Experience Platform擴充 [!DNL Web SDK] 功能。

1. 在中 [!DNL Launch]，開啟「 **[!UICONTROL 擴展]** 」頁籤。

   ![image](assets/launch-overview.png)

1. 從Launch Extension Catalog選取Adobe Experience Platform Web SDK擴充功能設定畫面隨即開啟。

   ![image](assets/launch-extension-install.png)

   如需詳細資訊，請參 [閱檔案](https://docs.adobe.com/content/help/en/launch/using/reference/manage-resources/extensions/overview.html) 中的 [!DNL Launch] 擴充功能。

1. 設定擴充功能.

   您現在唯一需要的設定是：

   * **配置ID:** 指定您從Adobe代表取得的設定ID。
   * **邊緣網域：** 指定您從Adobe代表取得的邊緣網域。

1. 按一 **[!UICONTROL 下「儲存]** 」，然後繼續下一個步驟。

## 建立規則，告知要 [!DNL Launch] 傳送哪些資料

接著，建立規則以 [!DNL Launch] 告知您要傳送哪些資料至Adobe Experience Platform，以及何時要傳送。

1. 在「規 **[!UICONTROL 則]** 」標籤下，設定在程式庫載入時，會在網站的每個新頁面上觸發 [!DNL Launch] 的事件。

   ![image](assets/launch-make-a-rule.png)

1. 新增動作.

   若要設定動作，請告 [!DNL Launch] 訴何處尋找資料層。 資料層是存在於頁面上的JavaScript物件，會從轉譯網頁的相同CMS傳送。 提供資料物件的JavaScript路徑。

   ![image](assets/launch-add-aep-action.png)

   您傳送的資料物件必須是有效的XDM，該XDM會針對連接至您的設定ID的資料集所使用的架構傳遞驗證。

1. 按一下&#x200B;**[!UICONTROL 保留變更]**.

如需詳細資訊，請參 [閱檔案](https://docs.adobe.com/content/help/zh-Hant/launch/using/reference/manage-resources/rules.html) 中的 [!DNL Launch] 規則。

## 將擴充功能和規則整合在程式庫中

接著， [將擴充功能和新規則整合在程式庫中](https://docs.adobe.com/content/help/zh-Hant/launch/using/reference/publish/overview.html) ，並在開發環境中測試這些變更。

![image](assets/launch-add-changes-to-library.png)

完成測試後，請透過工作流程升級程式庫，以便將它部署至生產網站。 現在，資料正從每位使用者流向Adobe Experience Platform。

![image](assets/launch-promote-library.png)

如需詳細資訊，請參 [閱檔案](https://docs.adobe.com/content/help/zh-Hant/launch/using/reference/publish/libraries.html) 中的 [!DNL Launch] 資料庫。