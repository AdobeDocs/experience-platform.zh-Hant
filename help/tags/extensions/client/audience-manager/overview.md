---
title: Adobe Audience Manager擴充功能概觀
description: 了解 Adobe Experience Platform 中的 Adobe Audience Manager 標記擴充功能。
exl-id: d345e145-fdb9-4ca3-88c2-9c2a247ea59a
source-git-commit: 88939d674c0002590939004e0235d3da8b072118
workflow-type: tm+mt
source-wordcount: '451'
ht-degree: 62%

---

# Adobe Audience Manager擴充功能概觀

>[!NOTE]
>
>Adobe Experience Platform Launch已經過品牌重塑，現在是Adobe Experience Platform中的一套資料收集技術。 因此，所有產品檔案中出現了幾項術語變更。 請參閱下列[檔案](../../../term-updates.md)，以取得術語變更的彙總參考資料。

透過Audience Manager標籤擴充功能，您可以整合Audience Manager所使用的DIL程式碼和Adobe Experience Platform中的屬性。

您可參閱此參考文件，了解使用此擴充功能建立規則時可使用哪些選項。

>[!NOTE]
>
>本擴充功能不適用於Adobe Analytics資料的事件轉送。 若要轉送事件，請使用[Adobe Analytics擴充功能](../analytics/overview.md)。

## 設定 Adobe Audience Manager 擴充功能

如果尚未安裝Adobe Audience Manager擴充功能，請開啟屬性，然後選取「**[!UICONTROL 擴充功能>目錄]**」，將游標停留在Adobe Audience Manager擴充功能上，然後選取「**[!UICONTROL 安裝]**」。

若要設定擴充功能，請開啟[!UICONTROL 擴充功能]標籤，將游標暫留在擴充功能上，然後選取&#x200B;**[!UICONTROL 設定]**。

### DIL 設定

設定您的 DIL 設定。下列組態選項可供使用：

![](../../../images/ext-aam-config.png)

#### DIL 版本

顯示資料整合程式庫 (DIL) 版本。

無法變更此設定。

#### 排除特定路徑

如果 URL 符合任何排除的路徑，則不會載入擴充功能。

選取&#x200B;**[!UICONTROL 新增路徑]**&#x200B;以指定排除的URL。

如果 URL 是規則運算式，請啟用「Regex」。

#### 使用 DIL Site Catalyst 模組

[SiteCatalyst 模組](https://experiencecloud.adobe.com/resources/help/en_US/aam/r_dil_sc_init.html)與 DIL 搭配使用，將 Analytics 標籤元素傳送至 Audience Manager。

使用程式碼編輯器來設定 siteCatalyst.init 檔案。

您也可以建立包含此設定相關資訊的備註。

#### 使用 DIL Google Analytics 模組

啟用 [Google Analytics 模組](https://experiencecloud.adobe.com/resources/help/en_US/aam/dil-google-universal-analytics.html)。

#### DIL.create 初始化屬性

新增 [DIL.create](https://experiencecloud.adobe.com/resources/help/en_US/aam/r_dil_create.html) 所使用的初始化屬性，以及新增 [visitorService 物件](https://experiencecloud.adobe.com/resources/help/en_US/aam/r_dil_visitor_service.html)的命名空間子屬性。程式碼編輯器的程式碼註解已加入兩個範例使用案例。

選取&#x200B;**[!UICONTROL 選擇專案]**&#x200B;以新增其他屬性。

將游標停留在「i」圖示上，即可了解每個屬性的用途。您可以在 [Audience Manager DIL 文件](https://experiencecloud.adobe.com/resources/help/en_US/aam/r_dil_create.html)中找到屬性的詳細資訊。

完成擴充功能設定後，選取&#x200B;**[!UICONTROL 儲存]**。

## Adobe Audience Manager 擴充功能動作類型

本主題說明 Audience Manager 擴充功能中可用的動作類型。

Adobe Audience Manager 擴充功能提供規則的「Then」部分中的下列動作：

### 執行自訂程式碼

執行在程式碼編輯器中設定的自訂程式碼。

在程式碼編輯器中輸入所需的程式碼，然後提供程式碼的名稱。此程式碼便可在規則產生器的「Then」部分中使用。

![](../../../images/ext-aam-then.png)

您也可以新增備註，包含設定的相關資訊。
