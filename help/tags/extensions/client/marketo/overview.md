---
title: Marketo Munchkin 擴充功能 總覽
description: 瞭解Marketo在Adobe Experience Platform的Munchkin標籤擴展。
exl-id: 8efc5203-91fc-4e89-be8f-74bf1aeeee5f
source-git-commit: 88939d674c0002590939004e0235d3da8b072118
workflow-type: tm+mt
source-wordcount: '214'
ht-degree: 75%

---

# Marketo·蒙奇金分機概述

>[!NOTE]
>
>Adobe Experience Platform Launch已被改名為Adobe Experience Platform的一套資料收集技術。 因此，所有產品文件中出現了幾項術語變更。 如需術語變更的彙整參考資料，請參閱以下[文件](../../../term-updates.md)。

此擴充功能可整合 [!DNL Marketo Munchkin] JavaScript 追蹤程式碼與您的屬性。[!DNL Marketo Munchkin] JavaScript 可追蹤一般使用者頁面瀏覽次數，以及您 Marketo 登陸頁面和外部網頁的導覽次數。

## 安裝 Marketo Munchkin 擴充功能

如果 [!DNL Marketo Munchkin] 尚未安裝擴展，請開啟您的屬性，然後選擇 **[!UICONTROL 擴展>目錄]**，懸停在 [!DNL Marketo Munchkin] 擴展，然後選擇 **[!UICONTROL 安裝]**。

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
