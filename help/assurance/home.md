---
title: Adobe Experience Platform保障概述
description: Adobe Experience Platform Assurance 讓您可以檢查、證明、模擬和驗證您在行動應用程式中收集資料或服務體驗的方式。
exl-id: e887f5f6-3db0-4521-be2d-20ef3d08e7d0
source-git-commit: 05a7b73da610a30119b4719ae6b6d85f93cdc2ae
workflow-type: tm+mt
source-wordcount: '824'
ht-degree: 4%

---

# Adobe Experience Platform Assurance

Adobe Experience Platform保險是 [Adobe Experience Cloud](https://www.adobe.com/experience-cloud.html) 幫助您檢查、驗證、模擬和驗證如何收集資料或在移動應用中提供體驗。

>[!IMPORTANT]
>
> 格里芬項目現在被稱為 **保證**!
>
> Griffon項目現已正式提供 **全部** Adobe Experience Cloud客戶作為保證。 若要瞭解有關此過渡的更多資訊，請閱讀 [用戶訪問指南](./user-access.md)。

>[!INFO]
>
>有可用的Assurance Public API!
>
>[保障API](https://developer.adobe.com/adobe-assurance-public-apis/) 是一組API，它使用戶在配備Adobe保障移動軟體開發工具包時能夠test和調試其Web和移動應用。

## 全面發佈

自2022年10月15日起，保證一般向所有Adobe Experience Cloud提供。

### 有什麼變化？

10月15日，將通過Admin Console管理進入Assurance。 請閱讀 [用戶訪問指南](./user-access.md) 確保您繼續擁有不間斷的訪問權限。

現有的Assurance整合、會話和事件不會發生其他更改或中斷。 可繼續通過 [https://griffon.adobe.com](https://griffon.adobe.com) **或** 可以使用（和書籤） [https://experience.adobe.com/assurance](https://experience.adobe.com/assurance)。

## Assurance能為你做什麼？

### 快速設定

快點開始，只需幾行代碼。 對於移動應用，Assurance與Adobe Experience Platform移動SDK協作，幫助您檢查、模擬和驗證應用事件、位置信號、配置參數、SDK日誌、設備資訊等。

### 無障礙連接

借助Assurance，將您的應用程式與平台連接起來是簡單而可靠的。 您不需要使用網路代理， [米特姆](https://en.wikipedia.org/wiki/Man-in-the-middle_attack))和其他網路體操 — 將你的應用連接到Assurance就像掃描QR碼或點擊按鈕一樣簡單。

![](./images/index/no-hassle-connection.png)

### 即時檢查、模擬和驗證

連接到Assurance後，您可以檢查即時流式應用程式事件和活動，並過濾和搜索以消除噪音。 事件包含有關驗證、調試和排除移動應用實現故障的詳細資訊。 保證還允許您即時截圖、模擬位置信號等。

![](./images/index/real-time-insepction.png)

### 與Adobe Experience Cloud

客戶端資料和經驗是通過用戶如何在我們以營銷者為中心的用戶介面上設定報告規則、活動和市場活動來提供的。 為了幫助您將兩者之間的點聯繫起來，我們將與Adobe Experience Cloud解決方案整合，如Adobe Experience Platform、Adobe Analytics、Adobe Target、Places Service等。

![](./images/index/integration.png)

## 功能

### Adobe Experience Platform移動SDK事件、日誌等

保證可幫助您檢查由Adobe Experience Platform移動SDK生成的原始SDK事件。 SDK收集的所有事件都可供檢查。 SDK事件在清單視圖中載入，按時間排序。 每個事件都有一個詳細視圖，提供更詳細的資訊。 還提供了用於瀏覽SDK配置、資料元素、共用狀態和SDK擴展版本的其他視圖。

### Adobe Analytics

「Adobe Analytics」>「分析事件」視圖是一個集中的視圖，顯示與您的Adobe Analytics移動實施相關的事件。 清單視圖在特殊格式化視圖中顯示生命週期或操作/狀態事件、後處理「狀態」以及必備事件詳細資訊。 「後處理」狀態顯示在對事件應用處理規則後，Adobe Analytics如何處理該事件。

### 適用於串流媒體的 Adobe Analytics

「Adobe Analytics」>「媒體分析事件」視圖顯示用於音頻和視頻分析實施的事件。 事件詳細資訊視圖顯示每個回放會話跟蹤的標準和自定義元資料。 此外，您還可以查看後處理狀態和後處理的媒體分析資料，如所花費的媒體時間或總緩衝區持續時間。

### 位置（位置服務）

「位置服務」視圖是一個設備上視圖，顯示用戶位置輸入和退出事件，以便於驗證。 此方便的視圖提供了一個方便的介面，用於查看特定於位置的資料點，以便在客戶端上進行檢查以進行上下文調試。

## 保證是否安全？

保證有下列安全措施：

* 保證和保證Web UI都對連接具有基於PIN的安全握手。 用戶必須顯式建立握手，以防止最終用戶建立「意外」的保證連接。
* 只支援Assurance和Assurance Web UI之間屬於同一Adobe Experience Cloud組織ID的連接。
* Adobe Experience Platform移動SDK事件通過HTTPS傳輸。
* 保證和Adobe Experience Platform移動軟體開發工具包使用TLS 1.2
* 30天後將刪除保證會話。
* 保證會話資料在靜態時按照儲存最佳做法進行加密。

## 快速入門

要設定Assurance，您需要首先在應用程式中安裝Assurance擴展。 要瞭解如何執行此操作，請閱讀上的教程 [實施保證延期](https://developer.adobe.com/client-sdks/documentation/platform-assurance-sdk/#add-the-aep-assurance-extension-to-your-app)。

在將「保證」添加到應用後，您可以建立可連接到設備的「保證」會話。 要瞭解如何使用保證，請閱讀 [使用保障指南](./tutorials/using-assurance.md)。
