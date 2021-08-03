---
title: Adobe Experience Manager Forms擴充功能概述
description: 了解Adobe Experience Platform中的Adobe Experience Manager Forms標籤擴充功能。
source-git-commit: f31a1d2e84dee262e04f1db0415ffd76248ecb6c
workflow-type: tm+mt
source-wordcount: '316'
ht-degree: 6%

---

# Adobe Experience Manager Forms擴充功能概觀

本檔案概述Adobe Experience Platform中的Adobe Experience Manager Forms標籤擴充功能。

## 事件

擴充功能提供下列事件類型：

1. **呈現**:使用者轉譯（開啟）表單時觸發。
1. **錯誤**:使用者在表單上發生驗證錯誤時觸發。
1. **說明**:當使用者按一下欄位的說明圖示時觸發。
1. **提交**:表單提交時觸發。
1. **欄位造訪**:造訪欄位時觸發。
1. **放棄**:當使用者關閉標籤或導覽至不同URL時觸發。
1. **儲存**:表單儲存至入口網站時觸發。

>[!IMPORTANT]
>
>「儲存」事件目前無法用於Forms as a Cloud Service。 可使用核心事件「擷取自訂事件」來擷取適用性Forms中由規則編輯器發送的自訂事件。

## 資料元素

擴充功能提供數個資料元素，可用於傳送分析呼叫中的屬性。

## 快速入門

請依照下列步驟開始使用擴充功能。

1. 從擴充功能目錄安裝Adobe Experience Manager Forms擴充功能。 安裝後無需進一步配置。
2. 安裝並設定[Adobe Analytics擴充功能](../analytics/overview.md#Configure-the-Adobe-Analytics-extension)。

## 建立規則

使用Experience ManagerForms擴充功能的規則如下所示：

![動作設定](./images/rule.png)

請依照下列步驟，為您的實作建立類似規則。

### 新增事件

1. 在擴充功能下拉式清單中選取&#x200B;**Adobe Experience Manager Forms**。
2. 選取要擷取的事件。

![動作設定](./images/AEM-forms-event.png)

### 新增動作

1. 在擴充功能下拉式清單中選取「Adobe Analytics」。
2. 在動作類型下拉式清單中選取「設定變數」。
3. 在設定檢視中，選擇要傳送的屬性和事件。
4. 新增「傳送信標」動作，以傳送在步驟3中設定之事件和屬性的分析呼叫
   ![動作設定](./images/AEM-forms-sendBeacon.png)
5. 新增「清除變數」動作。

![動作設定](./images/AEM-forms-action.png)