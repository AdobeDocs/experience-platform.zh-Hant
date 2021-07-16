---
title: Adobe隱私權擴充功能概觀
description: 了解Adobe Experience Platform中的Adobe隱私權標籤擴充功能。
source-git-commit: 5b8ef30b1d0e6d682c94453117677c806eba1e02
workflow-type: tm+mt
source-wordcount: '533'
ht-degree: 75%

---

# Adobe隱私權擴充功能概觀

>[!NOTE]
>
>Adobe Experience Platform Launch已重新命名為Experience Platform中的資料收集技術套件。 因此，產品檔案中已推出數個術語變更。 有關術語更改的綜合參考，請參閱以下[document](../../../term-updates.md)。

Adobe 隱私權擴充功能能夠收集和/或移除由 Adobe 解決方案指派給使用者的使用者 ID。

## 在安裝期間設定解決方案

當您從擴充功能目錄安裝 Adobe 隱私權擴充功能時，系統會提示您選取要更新的解決方案。目前可更新下列解決方案：

* Analytics (AA)
* Audience Manager (AAM)
* Target
* 訪客服務
* AdCloud
* 選取一或多個解決方案，然後選取「更新」。
* 選取並設定解決方案後，選取「儲存」。Adobe 隱私權擴充功能會新增至您已安裝的擴充功能清單中。

   各個解決方案的選項如下所述。

### Analytics

![](../../../images/ext-privacy-aa.jpg)

依預設，您必須輸入字串或選取資料元素，才能提供報表套裝。

要配置其他項目，請選擇&#x200B;**[!UICONTROL 選擇項目]**，選擇要配置的項目，然後選擇&#x200B;**[!UICONTROL 添加]**&#x200B;並輸入請求的參數或資料元素。

### Audience Manager

![](../../../images/ext-privacy-aam.jpg)

選擇&#x200B;**[!UICONTROL 選擇項目]**，選擇要配置的項目，然後選擇&#x200B;**[!UICONTROL 添加]**&#x200B;並輸入請求的參數或資料元素。 目前，您只能設定 `aamUUIDCookieName`。

### 目標

![](../../../images/ext-privacy-target.jpg)

輸入 Target 用戶端代碼。

### 訪客服務

![](../../../images/ext-privacy-visitor.jpg)

輸入您的 IMS 組織 ID。

### AdCloud

![](../../../images/ext-privacy-adcloud.jpg)

沒有須為 AdCloud 設定的特定參數。

## 設定 Adobe 隱私權擴充功能

安裝擴充功能後，您可以將其停用或加以刪除。在已安裝擴充功能的「Adobe隱私權」卡上，選取「**[!UICONTROL 設定]**」，然後選取「**[!UICONTROL 停用]**」或「**[!UICONTROL 解除安裝]**」。

## 動作

使用 Adobe 隱私權擴充功能設定規則時，可使用下列動作。

### 擷取身分

當事件和條件符合時，便擷取為訪客所儲存的身分資訊。

輸入資料傳遞目標的 JavaScript 函數名稱。此函數或方法會處理擷取的身分。不論您是儲存、顯示身分，還是將身分傳送至 Adobe GDPR API，都由您控制。

### 移除身分

當事件和條件符合時，便移除為訪客所儲存的身分資訊。

輸入資料傳遞目標的 JavaScript 函數名稱。此函數或方法會處理擷取的身分。不論您是儲存、顯示身分，還是將身分傳送至 Adobe GDPR API，都由您控制。

### 擷取然後移除身分

當事件和條件符合時，便擷取為訪客所儲存的身分資訊，隨後移除此等資訊。

## 教學課程：設定隱私權擴充功能

以下是如何設定資料元素並搭配隱私權擴充功能使用的簡短範例。

1. 建立資料元素 `privacyFunc`。

   ```JavaScript
   window.privacyFunc = function(a,b){
       console.log(a,b);
   }
   return window.privacyFunc
   ```

1. 建立規則以使用 Adobe 隱私權擴充功能的動作，在「程式庫負載」(頁面頂端) 上執行。資料元素請選取「`privacyFunc`」。

   * **擴充功能：** Adobe 隱私權
   * **動作類型：**擷取身分
此類動作會顯示已建立、已移除或未移除的身分。
   * **名稱：**&#x200B;擷取身分

1. 更新您的開發程式庫，然後發佈並測試。
