---
title: Adobe Experience Platform發行說明2022年8月
description: 2022年8月發佈的Adobe Experience Platform說明。
source-git-commit: 2a507b4fe5b7c9dc523ceb5b2f39becf9e574ed9
workflow-type: tm+mt
source-wordcount: '317'
ht-degree: 14%

---

# Adobe Experience Platform 發行說明

**發行日期：2022 年 24 月 8 日**

Adobe Experience Platform 現有功能更新：

- [資料準備](#data-prep)
- [來源](#sources)

## [!DNL Data Prep] {#data-prep}

[!DNL Data Prep] 允許資料工程師將資料映射到體驗資料模型(XDM)並驗證資料。

**已更新功能**

| 功能 | 說明 |
| --- | --- |
| 支援插入帶警告的記錄 | Data Prep現在將警告（非嚴重錯誤）本地化到欄位，並允許接收行的其餘部分。 現在，所有映射器轉換錯誤都會報告為警告，部分攝取的行被視為成功，並帶有警告。  對包含警告和診斷詳細資訊的記錄也支援監視。 當前，只有流資料才能部分接收帶有警告的記錄。 查看文檔 [正在接收帶警告的記錄](../../sources/tutorials/ui/monitor-streaming.md) 的子菜單。 |

{style=&quot;table-layout:auto&quot;}

瞭解有關 [!DNL Data Prep]，請參見 [[!DNL Data Prep] 概述](../../data-prep/home.md)。

## 來源 {#sources}

Adobe Experience Platform可以從外部源接收資料，同時允許您使用平台服務來構建、標籤和增強資料。 您可以從多種來源(如Adobe應用程式、基於雲的儲存、第三方軟體和您的CRM系統)接收資料。

Experience Platform提供REST風格的API和互動式UI，讓您能夠輕鬆地為各種資料提供程式設定源連接。 通過這些源連接，您可以驗證並連接到外部儲存系統和CRM服務，設定接收運行時間，並管理資料接收吞吐量。

**新功能**

| 功能 | 說明 |
| --- | --- |
| 跨區域支助Adobe Analytics來源 | 您現在可以從任何區域擷取報告套裝 (美國、英國或新加坡)。報表套件必須映射到與正在其中建立源連接的Experience Platform沙盒實例相同的組織。 有關詳細資訊，請參閱上的指南 [在UI中建立Adobe Analytics源連接](../../sources/tutorials/ui/create/adobe-applications/analytics.md)。 |

{style=&quot;table-layout:auto&quot;&quot;

要瞭解有關源的詳細資訊，請參閱 [源概述](../../sources/home.md)。
