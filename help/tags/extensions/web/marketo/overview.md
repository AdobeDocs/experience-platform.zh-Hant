---
title: Marketo Munchkin 擴充功能 概覽
description: 了解Adobe Experience Platform中的Marketo Munchkin標籤擴充功能。
source-git-commit: 5f810ada57eeb12a56de603d974a091b888dc9d2
workflow-type: tm+mt
source-wordcount: '213'
ht-degree: 62%

---

# Marketo Munchkin擴充功能概觀

>[!NOTE]
>
>Adobe Experience Platform Launch已重新命名為Experience Platform中的資料收集技術套件。 因此，產品檔案中已推出數個術語變更。 有關術語更改的綜合參考，請參閱以下[document](../../../term-updates.md)。

此擴充功能可整合 [!DNL Marketo Munchkin] JavaScript 追蹤程式碼與您的屬性。[!DNL Marketo Munchkin] JavaScript 可追蹤一般使用者頁面瀏覽次數，以及您 Marketo 登陸頁面和外部網頁的導覽次數。

## 安裝 Marketo Munchkin 擴充功能

如果尚未安裝[!DNL Marketo Munchkin]擴充功能，請開啟屬性，然後選取&#x200B;**[!UICONTROL 擴充功能>目錄]**，將游標暫留在[!DNL Marketo Munchkin]擴充功能上，然後選取&#x200B;**[!UICONTROL 安裝]**。

此擴充功能沒有必要的設定。

## Marketo Munchkin 擴充功能動作類型

本節說明 [!DNL Marketo Munchkin] 擴充功能中可供使用的動作類型。

### 初始化

![](../../../images/munchkin-Init.png)

**Munchkin ID：(必填)**「Admin > Integration > Munchkin」選單之下的 Munchkin 帳戶 ID。

**Configurations：**&#x200B;所有可設定的參數都記錄在[這裡](https://developers.marketo.com/javascript-api/lead-tracking/configuration/)

### 造訪網頁

![](../../../images/munchkin-visit-page.png)

**url：(必要)** 用來記錄頁面瀏覽的 URL 檔案路徑。

**params：**&#x200B;要記錄的所需參數的查詢字串。

**name：**&#x200B;網頁資產的自訂名稱。

### 按一下連結

![](../../../images/munchkin-click-link.png)

**href：(必要)** 用來記錄所選連結的 URL 檔案路徑。
