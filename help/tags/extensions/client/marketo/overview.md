---
title: Marketo Munchkin擴充功能概觀
description: 瞭解Adobe Experience Platform中的Marketo Munchkin標籤擴充功能。
exl-id: 8efc5203-91fc-4e89-be8f-74bf1aeeee5f
source-git-commit: 88939d674c0002590939004e0235d3da8b072118
workflow-type: tm+mt
source-wordcount: '210'
ht-degree: 55%

---

# Marketo Munchkin擴充功能概觀

>[!NOTE]
>
>Adobe Experience Platform Launch已經過品牌重塑，現在是Adobe Experience Platform中的一套資料收集技術。 因此，所有產品檔案中出現了幾項術語變更。 請參閱下列[檔案](../../../term-updates.md)，以取得術語變更的彙總參考資料。

此擴充功能可整合 [!DNL Marketo Munchkin] JavaScript 追蹤程式碼與您的屬性。[!DNL Marketo Munchkin] JavaScript 可追蹤一般使用者頁面瀏覽次數，以及您 Marketo 登陸頁面和外部網頁的導覽次數。

## 安裝 Marketo Munchkin 擴充功能

如果尚未安裝[!DNL Marketo Munchkin]擴充功能，請開啟您的屬性，然後選取&#x200B;**[!UICONTROL 擴充功能>目錄]**，將游標暫留在[!DNL Marketo Munchkin]擴充功能上，然後選取&#x200B;**[!UICONTROL 安裝]**。

此擴充功能沒有必要的設定。

## Marketo Munchkin 擴充功能動作類型

本節說明[!DNL Marketo Munchkin]擴充功能中可用的動作型別。

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
