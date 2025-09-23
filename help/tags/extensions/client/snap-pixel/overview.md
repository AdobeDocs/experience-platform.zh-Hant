---
title: 貼齊畫素延伸概述
description: 瞭解如何使用Snap Pixel標籤擴充功能，在Adobe Experience Platform中擷取寶貴的使用者互動。
last-substantial-update: 2025-09-17T00:00:00Z
source-git-commit: d846bd5dee5ce0ee8836dc25e20d9fd070714114
workflow-type: tm+mt
source-wordcount: '634'
ht-degree: 0%

---

# [!DNL Snap Pixel]擴充功能概觀

[[!DNL Snap Pixel]](https://businesshelp.snapchat.com/s/article/snap-pixel-about)是以JavaScript為基礎的分析工具，可讓您擷取網站上重要的使用者互動。 重要訪客動作（例如購買、註冊或其他轉換）會自動傳送給您的[廣告管理員](http://ads.snapchat.com/)，讓您測量並最佳化廣告、行銷活動、轉換路徑等效能。

[!DNL Snap Pixel]標籤擴充功能可讓您將[!DNL Snap Pixel]功能直接整合至使用者端標籤程式庫中。 本檔案概述如何安裝擴充功能，以及在標籤管理規則中實作其功能。

[!DNL Snap Pixel]標籤延伸簡化了[!DNL Snap Pixel]功能與您現有使用者端標籤程式庫的整合。 本檔案概述如何在您的標籤管理[規則](../../../ui/managing-resources/rules.md)中安裝擴充功能及設定其功能。

## 先決條件 {#prerequisites}

若要使用擴充功能，您必須具備有效的[!DNL Snap]帳戶，才能存取[!DNL Ads Manager]。 您必須[建立新的 [!DNL Snap Pixel]](https://forbusiness.snapchat.com/advertising/snap-pixel#about)並複製其畫素ID以設定您帳戶的延伸。 如果您有現有的[!DNL Snap Pixel]，則只需使用其ID即可。

建議同時使用[!DNL Snap Pixel]和[!DNL Snap Conversions API]，從使用者端和伺服器端傳送相同的事件。 此方法可協助復原[!DNL Snap Pixel]無法單獨擷取的事件。 如需如何在伺服器端實作中整合事件的步驟，請參閱[[!DNL Snap] Conversions API擴充功能，以取得事件轉送](../../server/snap/overview.md)。 請注意，您的組織必須擁有[事件轉送](../../../ui/event-forwarding/overview.md)的存取權，才能使用伺服器端擴充功能。

## 安裝擴充功能 {#install}

若要安裝[!DNL Snap Pixel]擴充功能，請導覽至資料收集UI或Experience Platform UI，然後從左側導覽中選取&#x200B;**[!UICONTROL 標籤]**。 從這裡，選取要新增擴充功能的屬性，或改為建立新屬性。

選取或建立所需的屬性後，在左側導覽中選取&#x200B;**[!UICONTROL 擴充功能]**，然後選取&#x200B;**[!UICONTROL 目錄]**&#x200B;索引標籤。 搜尋[!UICONTROL Snap Pixel]卡片，然後選取&#x200B;**[!UICONTROL 安裝]**。

![正在資料收集UI中選取[!UICONTROL Snap Pixel]延伸的[!UICONTROL 安裝]按鈕。](./images/install.png)

在出現的設定檢視中，您必須提供您先前複製的畫素ID，以將擴充功能連結至您的帳戶。 您可以直接將ID貼到輸入中，也可以改為選取現有的資料元素。

完成後，選取&#x200B;**[!UICONTROL 儲存]**。

![擴充功能組態檢視中作為資料元素提供的[!DNL Pixel] ID。](./images/configure.png)

擴充功能已安裝，您現在可以在標籤規則中運用其各種動作。

## 設定標籤規則 {#rule}

[!DNL Snap Pixel]支援一組預先定義的標準事件，每個事件都有特定的內容和接受的引數。 [!DNL Snap Pixel]擴充功能中可用的規則動作符合這些事件型別，可讓您根據事件型別輕鬆分類及設定傳送至[!DNL Snap]的事件。

為了示範，本節說明如何建立將購買事件傳送至[!DNL Snap]的規則。

若要開始，請建立新標籤規則，並視需要定義條件。 設定規則的動作時，請選擇[!DNL Snap Pixel]作為擴充功能，然後選取&#x200B;**[!UICONTROL 傳送購買事件]**&#x200B;作為動作型別。

完成設定[!UICONTROL 傳送購買事件]動作後，請選取&#x200B;**[!UICONTROL 保留變更]**&#x200B;以將其新增至規則設定。

![針對資料收集UI中的規則所選取的[!UICONTROL 傳送購買事件]動作型別。](./images/action-type.png)

當您對整體規則組態感到滿意時，請選取&#x200B;**[!UICONTROL 儲存至程式庫]**。

若要套用您的更新，請發佈新的標籤[組建](../../../ui/publishing/builds.md)以啟用程式庫的變更。

## 確認[!DNL Snap]正在接收資料 {#confirm}

將更新的組建部署到您的網站後，您可以在瀏覽器中觸發轉換事件，並檢查它們是否出現在[[!DNL Snap Events Manager]](https://businesshelp.snapchat.com/s/article/events-manager)中，藉此確認資料是否如預期傳送。

## 後續步驟 {#next-steps}

本指南涵蓋如何使用[!DNL Snap]標籤延伸將資料傳送至[!DNL Snap Pixel]。 如果您也打算將伺服器端事件傳送至[!DNL Snap]，您可以繼續安裝並設定[[!DNL Snap Conversions API event forwarding extension]](../../server/snap/overview.md)。
